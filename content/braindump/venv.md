---
title: "Activate Virtual Environments in Powershell"
date: 2023-10-02T21:27:10+05:30
draft: false
---


I love the simplicity of Linux and Bash. Probably why I prefer it over the unneccesary complexities of powershell.
Nonetheless I am using it to familiarize myself with the commands.

I was using *Git Bash* that ships with git for Windows, until I discovered the power of Windows Terminal[^1], an exceptional terminal emulator that enhanced my "*Windows experience.*" 

I like the seamless integration between different shells and its customizability, in contrast to the uninspiring blue powershell. 

I have a fair share of issues with powershell. One of them was to active a python virtual environment. 


##### Simple fix

```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy Unrestricted
```

[^1]: https://github.com/microsoft/terminal