---
title: What's A Syscal
tags:
  - unix
  - windows
  - os
---
# System call In Nutshell

## Introduction

A syscall or system call, is an ABI (Application Binary Interface) to communicate with operating system's kernel.

Chaque system d'exploitation dispose ca propre ABI, pour la simple et bonne raison qu'ils, ou plus spécifiquement leur kernel respectif fonctionne/interagisse avec le `hardware` de façon plus ou moins différentes.

> [!NOTE] 
> $\text{ABI of Unix Kernel } \neq \text{ABI of Windows Kernel} \neq \text{ABI of MacOS Kernel} \neq \text{ABI of Android Kernel}$ 

## Application Binary Interface (ABI)

The **Application Binary Interface (ABI)** defines **how programs interact at the binary level**.s