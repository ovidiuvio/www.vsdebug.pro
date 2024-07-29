---
layout: docs
title: Export | VSDebugPro
keywords: VSDebugPro, debugging command, data analysis, serialize object, visual studio debugging, export object, print symbol
description: Performs a structured dump of the callstack for the current thread or all threads in the debugged process.
---
{::options parse_block_html="true" /}

##### export (Export Symbol Command)
---

##### Description
The `export` command in VSDebugPro evaluates and saves to a file the value of a symbol or expression in the current debug context. It's a versatile tool for quick inspection of complex objects during a debugging session. \
It is similar with the [print](/pages/docs/print.html) command, but it outputs data to a file instead of printing to console.

{: .code-box}
>{: .code-header}
>Syntax
```
export [options] <filename> <expression>
```

##### Parameters

- `[options]`: Optional flags to modify the command behavior.
  - `-f`: Force overwrite if the output file already exists.
  - `-a`: Append to the file if it already exists.
- `<filename>`: The name of the file where the expanded expression will be saved.
- `<expression>`: The symbol or expression to evaluate and export.

##### Usage Examples

1. Export a simple variable:

    {: .code-box}
    ```
    export myVar.txt myVariable
    ```

2. Force overwrite an existing file:

   {: .code-box}
   ```
   export -f existingFile.txt myExpression
   ```

3. Append to an existing file:

   {: .code-box}
   ```
   export -a logFile.txt newData
   ```

3. Export the result of an expression:

    {: .code-box}
    ```
    export result.txt (ptr->value * 100 + offset)
    ```
##### Video tutorial

The following clip highlights a very simple usecase for the export command.

<iframe width="560" height="315" src="https://www.youtube.com/embed/pi65gkGqQjk?si=ZE7_lkAmE1xfh9ed" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

Check the [print](/pages/docs/print.html) command page for more information.