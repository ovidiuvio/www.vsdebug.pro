---
layout: docs
title: Alias | VSDebugPro - Enhanced debugging for Visual Studio
keywords: VSDebugPro, alias command, custom shortcuts, debugging efficiency, command customization
description: Simplify your debugging workflow with VSDebugPro's alias command. Learn how to create custom shortcuts for frequently used commands, reducing typing and streamlining your debugging sessions.
---
{::options parse_block_html="true" /}

##### alias (Command Alias Utility)
---

##### Description
The `alias` command allows you to create, delete, and list aliases for other commands or command sequences in VSDebugPro. This feature is useful for creating shortcuts to frequently used commands, simplifying complex command sequences, or customizing your debugging environment.

{: .code-box}
>{: .code-header}
>Syntax
```code
alias <add/del/list> <name> <string>
```

##### Parameters

- `<add/del/list>`: The operation to perform (add a new alias, delete an existing alias, or list all aliases).
- `<name>`: The name of the alias (for add and del operations).
- `<string>`: The command or command sequence the alias represents (for add operation).

##### Usage Notes

1. Alias names must be unique and cannot override existing VSDebugPro commands.
2. Aliases can reference other aliases, but be cautious of creating circular references.

##### Examples

1. Adding a simple alias:

   {: .code-box}
   ```
   alias add dm dumpmem
   ```
   Creates an alias `dm` for the `dumpmem` command.

2. Adding a complex alias:

   {: .code-box}
   ```
   alias add imgcopy memcpy img1.data img0.data img0.height * img0.stride "
   ```
   Creates an alias `imgcopy` that copyes the img1 bytes data to img0.

3. Deleting an alias:

   {: .code-box}
   ```
   alias del dm
   ```
   Deletes the alias `dm`.

4. Listing all aliases:
   ```
   alias list
   ```
   Displays all currently defined aliases.

##### Error Handling

- Invalid operation: Shows an error if the operation is not `add`, `del`, or `list`.
- Duplicate alias: Displays an error when trying to add an alias that already exists.
- Non-existent alias: Reports an error when trying to delete an alias that doesn't exist.
- Reserved name: Shows an error if trying to create an alias with a name that conflicts with existing commands.

These examples demonstrate how the `alias` command can be used to create powerful shortcuts and custom commands, significantly enhancing your debugging workflow in VSDebugPro.