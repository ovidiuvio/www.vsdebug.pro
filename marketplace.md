 **VSDebugPro** 
is an open source Visual Studio extension for Visual `C/C++, C#` that adds a `console` window with several debugging utilities such as dumping raw blocks of `memory` to a `file` without changing program code, loading binary data from a file to a specific memory location, `allocating` new memory in the debugged process, and more.

**Current supported VS versions:**  VS2019, VS2022

For older versions: VS2010, VS2012, VS2013, VS2015, VS2017, please visit  **[www.vsdebug.pro](http://www.vsdebug.pro)**

---
[![Build status](https://ci.appveyor.com/api/projects/status/y1b8p5ncabjbv4kn?svg=true)](https://ci.appveyor.com/project/ovidiuvio/vsdebugpro)

![](http://www.vsdebug.pro/assets/gif/dumpbuffer.gif)

**Features:**

---

- Save memory blocks from `Minidumps`
- Supports remote debugging sessions
- Works with `Visual Studio` for `ARM`
- Works with ARM programs while debugging
- Works with x64 programs running emulated on `ARM64EC`
- Works with x86/x64 targets
- Compatible with any programming language in Visual Studio that implements the standard debugger interface
- Console commands:

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

 - [Batch commands](https://www.vsdebug.pro/pages/docs/exec.html)

    `exec <yamlFilePath> [arg1] [arg2] ... [argN]`

    ```
    variables:
    var1: value1
    var2: value2

    commands:
    - command1 {{var1}} {{var2}}
    - command2 {{var1}} {{var2}}
    ```
- [Memory dump](https://www.vsdebug.pro/pages/docs/dumpmem.html)

    `dumpmem [options] <filename> <address> <size>`

- [Memory write](https://www.vsdebug.pro/pages/docs/loadmem.html)

    `loadmem <file> <address> <size>`

- [Memory copy](https://www.vsdebug.pro/pages/docs/memcpy.html)

    `memcpy <dst> <src> <size>`

- [Write memory with a pattern](https://www.vsdebug.pro/pages/docs/memset.html)

    `memset <dst> <val> <size>`

- Memory diff

    `<diff> <addr1> <addr2> <size>`




[**Docs**](http://www.vsdebug.pro/pages/docs.html)

[**Video Tutorial**](https://youtu.be/u7JfatQdGs0)

**Contact**

 **www: [www.vsdebug.pro](http://www.vsdebug.pro)**

 **mail: [ovidiu@vsdebug.pro](mailto:ovidiu@vsdebug.pro?subject=VSDebugPro)**