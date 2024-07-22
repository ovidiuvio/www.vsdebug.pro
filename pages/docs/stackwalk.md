---
layout: docs
title: Stack Walk | VSDebugPro
keywords: VSDebugPro, debugging command, data analysis, program debugging, visual studio debugging, stack dump ,stack walk, program stack, callstack
description: Performs a structured dump of the callstack for the current thread or all threads in the debugged process.
---
{::options parse_block_html="true" /}

##### stackwalk (Stack walk utility)

##### Description

The `stackwalk` command in VSDebugPro performs a structured dump of the call stack for the current thread or all threads in the debugged process. It provides a detailed view of the program's execution state, which is crucial for understanding the flow of control and diagnosing issues.

{: .code-box}
>{: .code-header}
>Syntax
```
stackwalk [-o <filename>] [depth] [all]
```

##### Parameters

- `-o <filename>`: Optional. Specifies the output file to write the stack dump. If not provided, the output is displayed in the console.
- `depth`: Optional. Specifies the number of frames to dump per thread. If not provided, all frames are dumped.
- `all`: Optional. If specified, dumps the stack for all threads. Otherwise, only the current thread's stack is dumped.

##### Usage Examples

1. Dump current thread's stack to console:

   {: .code-box}
   ```
   stackwalk
   ```

2. Dump current thread's stack to a file:

   {: .code-box}
   ```
   stackwalk -o stack.txt
   ```

3. Dump the first 10 frames of the current thread's stack:

   {: .code-box}
   ```
   stackwalk 10
   ```

4. Dump all threads' stacks to a file:

   {: .code-box}
   ```
   stackwalk -o allstacks.txt all
   ```

5. Dump the first 5 frames of all threads' stacks:

   {: .code-box}
   ```
   stackwalk -o stacks.txt 5 all
   ```

<div class="code-box">
>{: .code-header}
>Sample code

```cpp
#include <Windows.h>
#include <string>
#include <iostream>

void five(const std::string& msg, int depth) {
    depth++;
    std::cout << msg << std::endl;
}

void four(const std::string& msg, int depth) {
    depth++;
    five(msg, depth);
}

void three(const std::string& msg, int depth) {
    depth++;
    four(msg, depth);
}

void two(const std::string& msg, int depth) {
    depth++;
    three(msg, depth);
}

void one(const std::string& msg, int depth) {
    depth++;
    two(msg, depth);
}

int main()
{
    int depth = 0;
    one("callstack", depth);

    return 0;
}
```
</div>


<div class="code-box">
>{: .code-header}
>Stack trace in function five:

```
Stack Dump:
===========
Thread ID: 14520, Name: 
-------------------------------------------
Frame 0:
  Function: five
  Local Variables:
    depth = 5 (int)
    msg = "callstack" (const std::string &)
  Parameters:
    msg = {...} (const std::string &)
    depth = 5 (int)

Frame 1:
  Function: four
  Local Variables:
    depth = 4 (int)
    msg = "callstack" (const std::string &)
  Parameters:
    msg = {...} (const std::string &)
    depth = 4 (int)

Frame 2:
  Function: three
  Local Variables:
    depth = 3 (int)
    msg = "callstack" (const std::string &)
  Parameters:
    msg = {...} (const std::string &)
    depth = 3 (int)

Frame 3:
  Function: two
  Local Variables:
    depth = 2 (int)
    msg = "callstack" (const std::string &)
  Parameters:
    msg = {...} (const std::string &)
    depth = 2 (int)

Frame 4:
  Function: one
  Local Variables:
    depth = 1 (int)
    msg = "callstack" (const std::string &)
  Parameters:
    msg = {...} (const std::string &)
    depth = 1 (int)

Frame 5:
  Function: main
  Local Variables:
    depth = 0 (int)
  Parameters:
```
</div>

##### Notes

- The `stackwalk` command requires the debugger to be in break mode. If the debugger is running, the command will fail.
- Symbol information must be available for best results. Without symbols, some information (like function names and source locations) may be missing.
- The depth of the stack dump may be limited by the debugger or the process being debugged.
- Large stack dumps, especially when dumping all threads, can take some time to generate.

##### Best Practices

1. Start with dumping only the current thread's stack before exploring all threads.
2. Use a reasonable depth limit when dealing with deep recursion or very large call stacks.
3. When investigating a specific issue, focus on the relevant threads rather than dumping all threads.
4. Save stack dumps to files for later analysis or comparison.

##### Troubleshooting

- If the output lacks detailed information, ensure that debug symbols are loaded correctly.
- If the command fails, make sure the debugger is in break mode and attached to a process.
- For very large applications with many threads, consider using depth limits to avoid excessive output.

By using the `stackwalk` command effectively, you can gain valuable insights into your program's execution state, making it easier to track down bugs and understand complex control flows.