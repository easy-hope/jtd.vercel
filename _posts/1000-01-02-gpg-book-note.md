---
layout: default
title: gpg读书笔记
---

# 《gpg》读书笔记

## 目录

- [Introduction](#Introduction)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/23/2022-06-23-gpg/#The-Story-of-PGP "The Story of PGP")The Story of PGP](#httpbjapsonic-motocn202206232022-06-23-gpgThe-Story-of-PGP-The-Story-of-PGPThe-Story-of-PGP)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/23/2022-06-23-gpg/#Stop-Wasting-My-Precious-Time-What-Do-I-Need-to-Read "Stop Wasting My Precious Time. What Do I Need to Read?")Stop Wasting My Precious Time. What Do I Need to Read?](#httpbjapsonic-motocn202206232022-06-23-gpgStop-Wasting-My-Precious-Time-What-Do-I-Need-to-Read-Stop-Wasting-My-Precious-Time-What-Do-I-Need-to-ReadStop-Wasting-My-Precious-Time-What-Do-I-Need-to-Read)
- [\[\](http://bj.apsonic-moto.cn/2022/06/23/2022-06-23-gpg/#ch01 "ch01")ch01](#httpbjapsonic-motocn202206232022-06-23-gpgch01-ch01ch01)
- [\[\](http://bj.apsonic-moto.cn/2022/06/23/2022-06-23-gpg/#%E9%99%84%E5%BD%95B "附录B")附录B](#httpbjapsonic-motocn202206232022-06-23-gpgE99984E5BD95B-附录B附录B)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/23/2022-06-23-gpg/#Output-Control "Output Control")Output Control](#httpbjapsonic-motocn202206232022-06-23-gpgOutput-Control-Output-ControlOutput-Control)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/23/2022-06-23-gpg/#Keypair-Creation-Revocation%EF%BC%88%E5%90%8A%E9%94%80%EF%BC%89-and-Exports "Keypair Creation, Revocation（吊销）, and Exports")Keypair Creation, Revocation（吊销）, and Exports](#httpbjapsonic-motocn202206232022-06-23-gpgKeypair-Creation-RevocationEFBC88E5908AE99480EFBC89-and-Exports-Keypair-Creation-Revocation吊销-and-ExportsKeypair-Creation-Revocation吊销-and-Exports)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/23/2022-06-23-gpg/#Revoking-a-Key "Revoking a Key")Revoking a Key](#httpbjapsonic-motocn202206232022-06-23-gpgRevoking-a-Key-Revoking-a-KeyRevoking-a-Key)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/23/2022-06-23-gpg/#Exporting-a-Key "Exporting a Key")Exporting a Key](#httpbjapsonic-motocn202206232022-06-23-gpgExporting-a-Key-Exporting-a-KeyExporting-a-Key)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/23/2022-06-23-gpg/#Sending-a-Key-to-a-Keyserver "Sending a Key to a Keyserver")Sending a Key to a Keyserver](#httpbjapsonic-motocn202206232022-06-23-gpgSending-a-Key-to-a-Keyserver-Sending-a-Key-to-a-KeyserverSending-a-Key-to-a-Keyserver)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/23/2022-06-23-gpg/#Managing-Keyrings "Managing Keyrings")Managing Keyrings](#httpbjapsonic-motocn202206232022-06-23-gpgManaging-Keyrings-Managing-KeyringsManaging-Keyrings)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/23/2022-06-23-gpg/#Viewing-Keys "Viewing Keys")Viewing Keys](#httpbjapsonic-motocn202206232022-06-23-gpgViewing-Keys-Viewing-KeysViewing-Keys)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/23/2022-06-23-gpg/#Adding-and-Removing-Keys "Adding and Removing Keys")Adding and Removing Keys](#httpbjapsonic-motocn202206232022-06-23-gpgAdding-and-Removing-Keys-Adding-and-Removing-KeysAdding-and-Removing-Keys)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/23/2022-06-23-gpg/#Key-Signatures "Key Signatures")Key Signatures](#httpbjapsonic-motocn202206232022-06-23-gpgKey-Signatures-Key-SignaturesKey-Signatures)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/23/2022-06-23-gpg/#Encryption-and-Decryption "Encryption and Decryption")Encryption and Decryption](#httpbjapsonic-motocn202206232022-06-23-gpgEncryption-and-Decryption-Encryption-and-DecryptionEncryption-and-Decryption)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/23/2022-06-23-gpg/#Signing-Files "Signing Files")Signing Files](#httpbjapsonic-motocn202206232022-06-23-gpgSigning-Files-Signing-FilesSigning-Files)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/23/2022-06-23-gpg/#Output-Formats "Output Formats")Output Formats](#httpbjapsonic-motocn202206232022-06-23-gpgOutput-Formats-Output-FormatsOutput-Formats)

## Introduction

This book is not meant to be the definitive tome（权威著作） on the  
subject. It will not teach you how to compute public encryption  
keys by hand, nor will it survey all the encryption algorithms  
and techniques available today. However, it will teach you  
enough about the ideas behind encryption and digital signatures that you’ll be able to make intelligent choices about  
which of the available options you should use in any given circumstance

### \[]\(<http://bj.apsonic-moto.cn/2022/06/23/2022-06-23-gpg/#The-Story-of-PGP> "The Story of PGP")The Story of PGP

跳过

### \[]\(<http://bj.apsonic-moto.cn/2022/06/23/2022-06-23-gpg/#Stop-Wasting-My-Precious-Time-What-Do-I-Need-to-Read> "Stop Wasting My Precious Time. What Do I Need to Read?")Stop Wasting My Precious Time. What Do I Need to Read?

If you choose GnuPG, read the general OpenPGP chapters and those dedicated to GnuPG: Chapters 1–2, 4–5, 7–8,  
and 11. GnuPG chapters tend to be longer than PGP chapters  
because GnuPG people must learn more.

## \[]\(<http://bj.apsonic-moto.cn/2022/06/23/2022-06-23-gpg/#ch01> "ch01")ch01

## \[]\(<http://bj.apsonic-moto.cn/2022/06/23/2022-06-23-gpg/#%E9%99%84%E5%BD%95B> "附录B")附录B

### \[]\(<http://bj.apsonic-moto.cn/2022/06/23/2022-06-23-gpg/#Output-Control> "Output Control")Output Control

The -a (or –armor) flag tells  
GnuPG to give output in human-readable format, instead  
of the default binary format. Similarly, the –output flag tells  
GnuPG to send its output to a file, rather than dumping it  
directly to the screen.

### \[]\(<http://bj.apsonic-moto.cn/2022/06/23/2022-06-23-gpg/#Keypair-Creation-Revocation%EF%BC%88%E5%90%8A%E9%94%80%EF%BC%89-and-Exports> "Keypair Creation, Revocation（吊销）, and Exports")Keypair Creation, Revocation（吊销）, and Exports

To create a new GnuPG keypair, use the interactive –gen-key  
option. GnuPG will walk you through the key-creation process. (We discussed key creation and management in detail in  
Chapter 4.)

#### \[]\(<http://bj.apsonic-moto.cn/2022/06/23/2022-06-23-gpg/#Revoking-a-Key> "Revoking a Key")Revoking a Key

跳过

#### \[]\(<http://bj.apsonic-moto.cn/2022/06/23/2022-06-23-gpg/#Exporting-a-Key> "Exporting a Key")Exporting a Key

`gpg --output pubkey.asc --armor --export UID`

#### \[]\(<http://bj.apsonic-moto.cn/2022/06/23/2022-06-23-gpg/#Sending-a-Key-to-a-Keyserver> "Sending a Key to a Keyserver")Sending a Key to a Keyserver

To send a public key to a keyserver, use the –send-keys option.  
The –keyserver option lets you choose to which keyserver you  
want to submit the key. If you don’t choose a keyserver, GnuPG  
will use the default keyserver specified in gpg.conf.

### \[]\(<http://bj.apsonic-moto.cn/2022/06/23/2022-06-23-gpg/#Managing-Keyrings> "Managing Keyrings")Managing Keyrings

#### \[]\(<http://bj.apsonic-moto.cn/2022/06/23/2022-06-23-gpg/#Viewing-Keys> "Viewing Keys")Viewing Keys

- option –list-keys. This will print all the keys on your keyring, so you can include a UID or portion thereof to list only particular keys.
- To see the secret keys on your keyring, use the option –list-secret-keys.
- To view the fingerprint of a key, use –fingerprint and the UID of the key or a subset thereof.
  #### \[]\(<http://bj.apsonic-moto.cn/2022/06/23/2022-06-23-gpg/#Adding-and-Removing-Keys> "Adding and Removing Keys")Adding and Removing Keys
  To import a public key from a file, use the –import option  

  and the name of the file. No other options are required.  

  To remove a key from your keyring, use the –delete-keys  

  option and give the UID or keyid of the key you want to  

  delete.

### \[]\(<http://bj.apsonic-moto.cn/2022/06/23/2022-06-23-gpg/#Key-Signatures> "Key Signatures")Key Signatures

### \[]\(<http://bj.apsonic-moto.cn/2022/06/23/2022-06-23-gpg/#Encryption-and-Decryption> "Encryption and Decryption")Encryption and Decryption

Use the –encrypt option to encrypt files, giving the name of  
the file you want to encrypt as an argument. GnuPG will interactively ask you for the UID of each public key you want to use  
in the encryption process and then encrypt the files so that  
they can only be read with the corresponding private key(s).

To decrypt a file, use the –decrypt option. GnuPG will  
prompt you for your passphrase and print the decrypted message to the terminal.

### \[]\(<http://bj.apsonic-moto.cn/2022/06/23/2022-06-23-gpg/#Signing-Files> "Signing Files")Signing Files

### \[]\(<http://bj.apsonic-moto.cn/2022/06/23/2022-06-23-gpg/#Output-Formats> "Output Formats")Output Formats

By default, GnuPG produces encrypted files and keys in binary  
format and uses filenames based on the original filenames. You  
can modify this with the –armor and –output options.

**The –armor and –output options must be used before either –sign or –encrypt.**

