---
title: "Applied Cryptography"
date: "2021-09-27T18:03:01.000Z"
tags: ["cryptography"]
---


For our first topic of the Fall 2021 semester, we covered applied cryptography.

# Topics

Before the discussion of specific types of ciphers, there are two important terms to cover first. A **plaintext** message is just the original message, with no encryption done to it. A **ciphertext** message is one that has been encoded, and is supposed to be unreadable to people who do not have the decryption method.

One important rule for most cryptosystems is that the security of the system should not rely on the secrecy of the system. Or in other words, in a good cryptosystem, as long as the key is kept secret, an attacker could understand exactly how the system works and have access to ciphertext and would not be able to decrypt it without the key.

## Substitution Ciphers

Substitution ciphers are one of the most basic types of ciphers, and they work by simply taking characters from 1 alphabet and mapping each character to another alphabet. This mapping is done by use of a specific **key**.

An example of this can be shown with the character set `{ABCDEFGH}`. An example of a key for this could be `{DEACBGHF}`, where each letter in the original set would be replaced with the corresponding letter in the key (i.e. `A` would be replaced with `D` and so on). Using this key to encode the string `DEADBEEF` would looks something like this: `CBDCEBBG`. To someone who does not have the key, it would look like nonsense, but someone who has the key could easily convert it back.

This example shows another important property about substitution ciphers, they must be **invertible** , or in other words, the original message should be able to be converted from ciphertext back to the original message.

Substitution ciphers can sometimes be challenging to break, but that depends heavily on certain factors. When the amount of known ciphertext is very low, it makes it significantly harder to crack a cipher. This is because one good way to break substitution ciphers is to use language patterns to detect what characters are what. You can look for common words and phrases in the ciphertext. For example, if spaces are preserved, the assumption that single letters surrounded by spaces are either `a` or `I` is a fairly safe one to make. Additionally, the frequency of letters can be looked at, if a letter is incredibly common, there is a very good chance it is a vowel and not some uncommon character like `z`. Additionally, there is an attack called a known plaintext attack. This attack works by using some of the above techniques to replace all instances of characters in a ciphertext to see if recognizable phrases or words appear, showing that some progress was being made to breaking it.

## XOR Ciphers

XOR ciphers work by using the logical XOR operator, XORing each bit in a plaintext with each bit of a specific key to create the ciphertext. This cipher is not heavily used on its own, but it is used very often as a building block for other ciphers. Essentially, the XOR cipher is just a fancy bitwise substitution cipher.

However, this means that XOR ciphers are not perfect and still have clear limitations. One large disadvantage of them is that the key must always be the same length as the plaintext being encrypted, so variable length plaintexts do not work with it. One way to get around this is to just duplicate the key to fit the length of the plaintext, but then this leads to some of the same problems with substitution ciphers. Another common vulnerability is that if you have two ciphertexts that were encrypted using the same key and XOR those ciphertexts together it will leak information about both of the original plaintexts, as we will see in a lab later.

## S-boxes

S-boxes are cryptographic elements that are used to build substitution ciphers that work for an arbitrary number of bits. For an S-box, for any input octect that is passed in, it will output a different octect. What this essentially boils down to is that changes in the output should be incomparable to changes in the input. So say if a single bit is changed in the input, the output should still change dramatically. This is only one reason why S-boxes are typically better than XOR ciphers, as S-boxes scramble bits much better. S-boxes are also used very commonly in building larger, more complex cryptosystems.

## Part 1

## Part 2

<https://youtu.be/NIE0g90buRU>
