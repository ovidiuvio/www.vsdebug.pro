---
layout: default
overview: true
title: Home | VSDebugPro - Enhanced debugging for Visual Studio
keywords: VSDebugPro, Visual Studio, C++, C#, debugging tools, memory dump, data loading, batch commands, debugging extension, developer tools
description: Debug like a pro with VSDebugPro, a powerful Visual Studio extension for C/C++ and C#. Dump memory, load data, execute batch commands, and streamline your debugging workflow. Download VSDebugPro for free and take control of your debugging sessions.
---

<p class="text-monospace">
VSDebugPro is a Visual Studio extension for Visual C/C++, C# that adds several usefull debugging utilities such as
dumping raw blocks of memory to a file without changing program code, loading binary data from a file to a specific memory location, allocating new memory in the debugged process, and more.
</p>
{: align="center"}

<p align="center">
    <img src="/assets/img/vsd_console.png" width="70%"/>
</p>   
<br />
<br />

---

###### **Available for:**

**`VS2010 - VS2022`, `C/C++`, `C#`, `x86/64`, `Arm64/Arm64EC`**

###### **Features:**

- Save memory blocks from `Minidumps`
- Supports `remote debugging` sessions
- Works with `Visual Studio` for `ARM`
- Works with ARM programs while debugging
- Works with x64 programs running emulated on `ARM64EC`
- Works with x86/x64 targets
- Compatible with any programming language in Visual Studio that implements the standard debugger interface
- Console commands:

    {: .code-box}
    ```
        help  Provides help information for commands.
       about  Opens the about window.
       alias  Alias allows a more familiar command or name to execute a long string
    settings  Opens product settings dialog.
     dumpmem  Memory dump utility.
     loadmem  Load memory utility.
      memcpy  Memory copy utility.
      memset  Fills a block of memory with a pattern.
        diff  Memory diff.
      malloc  Allocates memory in the process heap.
        free  Free memory allocated with malloc.
        exec  Executes commands from a specified YAML file with Mustache templating.
    ```

 - [**Batch commands**](https://www.vsdebug.pro/pages/docs/exec.html)

    {: .code-box}
    ```
    exec <yamlFilePath> [arg1] [arg2] ... [argN]
    ```

    {: .code-box}
    ```
    variables:
    var1: value1
    var2: value2

    commands:
    - command1 {{var1}} {{var2}}
    - command2 {{var1}} {{var2}}
    ```
- [**Memory dump**](https://www.vsdebug.pro/pages/docs/dumpmem.html)

    {: .code-box}
    ```
    dumpmem [options] <filename> <address> <size>
    ```

- [**Memory write**](https://www.vsdebug.pro/pages/docs/loadmem.html)

    {: .code-box}
    ```
    loadmem <file> <address> <size>
    ```

- [**Memory copy**](https://www.vsdebug.pro/pages/docs/memcpy.html)

    {: .code-box}
    ```
    memcpy <dst> <src> <size>
    ```

- [**Write memory with a pattern**](https://www.vsdebug.pro/pages/docs/memset.html)

    {: .code-box}
    ```
    memset <dst> <val> <size>
    ```

- [**Memory diff**]()

    {: .code-box}
    ```
    <diff> <addr1> <addr2> <size>
    ```



