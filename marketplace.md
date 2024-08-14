 **VSDebugPro** 
is an open source Visual Studio extension for Visual `C/C++, C#` that adds a `console` window with several debugging utilities such as dumping raw blocks of `memory` to a `file` without changing program code, loading binary data from a file to a specific memory location, `allocating` new memory in the debugged process, and more.

**Current supported VS versions:**  VS2019, VS2022

For older versions: VS2010, VS2012, VS2013, VS2015, VS2017, please visit  **[www.vsdebug.pro](https://www.vsdebug.pro)**

---
[![Build status](https://ci.appveyor.com/api/projects/status/y1b8p5ncabjbv4kn?svg=true)](https://ci.appveyor.com/project/ovidiuvio/vsdebugpro)

![](https://www.vsdebug.pro/assets/gif/dumpbuffer.gif)

**Features:**

---
- Commands console

  <img src="https://www.vsdebug.pro/assets/img/ft_console.webp" width="100%"/>

- Workspace and External tools integration

  <img src="https://www.vsdebug.pro/assets/img/ft_settings.webp" width="60%"/>

- Save memory blocks from `Minidumps`
- Supports `remote debugging` sessions
- Works with `Visual Studio` for `ARM`
- Works with ARM programs while debugging
- Works with x64 programs running emulated on `ARM64EC`
- Works with x86/x64 targets
- Compatible with any programming language in Visual Studio that implements the standard debugger interface
- Console commands:

    ```
        help	Provides help information for commands.
       about	Opens the about window.
       alias	Alias allows creating command shortcuts.
    settings	Opens product settings dialog.
   stackwalk	Performs a structured dump of the call stack.
     dumpmem	Memory dump utility.
     loadmem	Load memory utility.
     hexdump	Memory hex dump utility.
      memcpy	Memory copy utility.
      memset	Fills a block of memory with a pattern.
        diff	Diff utility.
      malloc	Allocates memory in the process heap.
        free	Free memory allocated with malloc.
       print	Evaluates and prints the value of a symbol or expression.
      export	Fully expands a symbol or expression to a file.
        exec	Executes commands from an YAML file with Mustache templating.
    ```

 - [Print & export symbols](https://www.vsdebug.pro/pages/docs/print.html)

    <img src="https://www.vsdebug.pro/assets/img/ft_repeat.webp" width="35%"/>

    <video src="https://www.vsdebug.pro/assets/webm/VSDebugPro-export-object.webm" width="640" height="480" controls></video>

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

- [Hex dump](https://www.vsdebug.pro/pages/docs/hexdump.html)

    `hexdump <optional flags> <filename> <address> <size> [columns] [bytesPerRow]`

- [Memory write](https://www.vsdebug.pro/pages/docs/loadmem.html)

    `loadmem <file> <address> <size>`

- [Memory copy](https://www.vsdebug.pro/pages/docs/memcpy.html)

    `memcpy <dst> <src> <size>`

- [Write memory with a pattern](https://www.vsdebug.pro/pages/docs/memset.html)

    `memset <dst> <val> <size>`

- [Memory allocation](https://www.vsdebug.pro/pages/docs/malloc.html)

    `malloc <size>`

- Memory diff

    `<diff> <addr1> <addr2> <size>`




[**Docs**](https://www.vsdebug.pro/pages/docs.html)

[**Video Tutorial**](https://youtu.be/u7JfatQdGs0)

**Contact**

 **www: [www.vsdebug.pro](https://www.vsdebug.pro)**

 **mail: [ovidiu@vsdebug.pro](mailto:ovidiu@vsdebug.pro?subject=VSDebugPro)**