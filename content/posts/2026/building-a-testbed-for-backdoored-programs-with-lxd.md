---
title: "Building a testbed for backdoored programs with LXD"
date: "2026-03-06T06:03:50.000Z"
tags: ["reversing", "vm", "linux", "malware analysis"]
---

One task I occasionally do with the Program Understanding lab at Auburn is develop backdoored programs to test analysis tools and frameworks. These artifacts are useful when evaluating things like static analysis pipelines, control-flow recovery tools, or security scanners. If the ground truth is known—because you inserted the backdoor yourself—you can see exactly what the tool detects and what it misses.

💡

This post is largely inspired by my experiences with SECCDC and Nathan’s backdoor project (DOI coming soon).

Nginx is widely deployed, reasonably complex, and structured around a modular architecture. That makes it a good candidate for controlled modifications. Instead of writing a backdoor from scratch, we adapted ideas from RITSEC’s excellent [Headshot module](https://github.com/RITRedteam/Headshot), which demonstrates how to inject command execution through an HTTP header trigger. We elide the development of the backdoor here but encourage you to check out RITSEC’s beautifully written comments.

![](/images/2026/03/image-1.png)Example of RCE injected into a Nginx module

With the bootstrap, modification itself was fairly straightforward. The harder part turned out to be testing.

Developing these artifacts involves a loop:

  1. modify the source
  2. rebuild the program
  3. deploy the binary
  4. trigger the backdoor
  5. observe the behavior
  6. reset the environment
  7. repeat

When you are doing this dozens of times, the environment quickly becomes the bottleneck.

## The VM Problem

A common solution is to use a virtual machine, such as VMware or VirtualBox. There are problems however. It’s heavy, takes forever to boot, and for someone who likes to use Linux and VMWare, dealing with kernel module updates is like working with a BOFH.

<insert substack-esque comic strip about computer annoyance here or something.png>

Of course, when you are writing code that manipulates the kernel, VMs are essential. But when that’s not the case AND you are iterating rapidly, waiting for a full operating system to boot every time becomes painful. So what's something that behaves similarly to a VM but launches as quickly as a container?

## **LXD**

LXD is a system container and VM manager built on top of LXC (Linux Containers). Unlike Docker, LXD is explicitly designed to run full Linux system instances. Each container gets its own init system, process tree, network namespace, and filesystem. Most importantly, you aren’t encumbered with Docker’s opinionated yaml-isms.

Setting up LXD is almost embarrassingly easy on modern Ubuntu:
```
sudo snap install lxd
sudo lxd init # use defaults or whatever (this part is interactive)
sudo usermod -aG lxd $USER
newgrp lxd
```

## Build Orchestration

You’ll find many software projects have their own build scripts, and with C projects, it’s typically some `configure` script and a `Makefile` . Nginx is no different: it has its own `auto/configure` script which generates the `Makefile` needed to compile.

As a result, we need our own Makefile that can run the project’s build system without affecting ours. This is easy by placing our `Makefile` in a parent directory of Nginx’s.
```
.PHONY: all configure build backdoor clean
```

The implementation of the macros should be obvious. What isn’t obvious is how to toggle between building the backdoor and clean versions. To do this, we rely on patch files.

![](/images/2026/03/image.png)The makefile orchestration system

In this way, we can build both binaries for differential analysis or for sanity checks.

Once this system is in place, all we need to do is spin up a LXC instance. The workflow you can adopt is below:
```
lxc launch ubuntu:24.04 vuln-nginx
lxc exec vuln-nginx -- apt update
lxc exec vuln-nginx -- apt install -y build-essential libpcre2-dev libssl-dev zlib1g-dev
lxc file push -r . vuln-nginx/root/
lxc exec vuln-nginx -- bash -c "cd backdoored-nginx/ && make backdoor && cd nginx-release-1.29.5/ && make install && /usr/local/nginx/sbin/nginx"
IPADDR=$(lxc exec vuln-nginx -- ip a show eth0 | grep -oP '\\S+(?=/24)')
curl $IPADDR -H "SHOWMETHEMONEY: id"
lxc stop vuln-nginx
lxc delete vuln-nginx
```

This is all we really need. Each run starts from a clean Ubuntu instance, builds the modified artifact, executes the trigger, and leaves no persistent state once the container is deleted. The entire loop, especially the launch runs in seconds, which makes iterative testing much less painful.

* * *
