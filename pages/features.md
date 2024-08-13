---
layout: features
title: Features | VSDebugPro
keywords: VSDebugPro documentation, debugging tutorials, memory manipulation, command reference, debugging techniques, Visual Studio extension guide
description: Learn how to use VSDebugPro with our comprehensive documentation. Discover powerful commands, explore common concepts, and unlock advanced debugging techniques to simplify even the most complex debugging tasks.
---
{::options parse_block_html="true" /}

#### VSDebugPro Features
---

- [Console](/pages/features/console.html) commands:

  {: .code-box}
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

- [Save memory](/pages/features/memory.html#memory-dump) blocks from `Minidumps`
- Supports `remote debugging` sessions
- Works with `Visual Studio` for `ARM`
- Works with ARM programs while debugging
- Works with x64 programs running emulated on `ARM64EC`
- Works with x86/x64 targets
- Compatible with any programming language in Visual Studio that implements the standard debugger interface