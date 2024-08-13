---
layout: docs
title: Docs | VSDebugPro
keywords: VSDebugPro documentation, debugging tutorials, memory manipulation, command reference, debugging techniques, Visual Studio extension guide
description: Learn how to use VSDebugPro with our comprehensive documentation. Discover powerful commands, explore common concepts, and unlock advanced debugging techniques to simplify even the most complex debugging tasks.
---

#### VSDebugPro Common Concepts and Features
---

##### Overview

This document covers common concepts, features, and conventions used throughout VSDebugPro. Familiarizing yourself with these elements will help you navigate and use the tool more effectively.

##### Debug Console

VSDebugPro provides a [console](/pages/features/console.html) for executing commands and viewing output.

##### Console Basics
- Commands are entered at the prompt (typically `>`)
- Use `help` to see a list of available commands
- Use `help <command>` for detailed information on a specific command

##### Address Specification

`Addresses` can be specified in several formats:

- `Hexadecimal`: Prefixed with '0x' (e.g., 0x00656789)
- `Decimal`: Plain number (e.g., 6789456)
- `Symbol` names: If symbols are loaded (e.g., &myVariable)

##### Variables and Arguments Specification

`Variables` and `Arguments` can be specified as:

- `Decimal` numbers (e.g., 1024)
- `Hexadecimal` numbers (e.g., 0x400)
- `Expressions` (e.g., 1024*1024 for 1 MB)

##### File Paths

- Absolute paths are recommended (e.g., C:\temp\mydump.bin)
- Relative paths use the [Working Directory](/pages/features/workspace.html) <img src="/assets/img/wd.png" width="3%"/>  specified in [Settings](/pages/features/console.html#settings) <img src="/assets/img/settings.png" width="3%"/>

##### Debugging Context

VSDebugPro operates within the current debugging context of Visual Studio:

- Commands affect the currently debugged process
- Ensure you're at the correct breakpoint or execution point when using commands
- Some commands may not be available when debugging is not active

##### Expression Evaluation

Many commands support expression evaluation:

- Arithmetic expressions: e.g., `1024*1024`
- Symbol resolution: e.g., `&myVariable+0x10`

##### Error Handling

When errors occur:

- Error messages are displayed in the console
- Check command syntax and parameters
- Ensure the debugger is in the correct state for the command
- Verify memory addresses and sizes are valid

##### Customization

VSDebugPro offers several ways to customize your experience:

- [Settings UI](/pages/features/console.html#settings) <img src="/assets/img/settings.png" width="3%"/>: Configure global settings and file associations
- [Aliases](/pages/docs/alias.html): Create custom shortcuts for frequently used commands
- [Scripts](/pages/docs/exec.html): Use the [exec](/pages/docs/exec.html) command to run sequences of commands from YAML files

##### Performance Considerations

- Large memory operations may take time, especially on remote debugging sessions
- Be cautious with very large memory dumps or loads
- Use appropriate sizes when working with memory to avoid performance issues

##### Getting Help

- Use the `help` command in the console for command-specific information
- Refer to the VSDebugPro documentation for detailed guides and examples
- Check for tooltips and context-sensitive help in the UI
