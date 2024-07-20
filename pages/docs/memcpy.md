---
layout: docs
title: Memcpy | VSDebugPro
keywords: VSDebugPro, memcpy, copy memory, data duplication, memory manipulation, debugging tools
description: Manipulate memory efficiently with VSDebugPro's memcpy command. This documentation explains how to copy data between memory locations within your debugged process, enabling data duplication and manipulation for testing and debugging purposes.
---
{::options parse_block_html="true" /}

##### memcpy (Memory Copy Utility)
---

##### Description
The `memcpy` command allows you to copy data from one memory location to another within the debugged process. This feature is useful for duplicating memory regions, moving data, or creating backups of memory contents within the process's address space.

{: .code-box}
>{: .code-header}
>Syntax
```
memcpy <dst> <src> <size>
```

##### Parameters

- `<dst>`: Destination address where the data will be copied to.
- `<src>`: Source address where the data will be copied from.
- `<address>`: Number of bytes to copy from the source to the destination.

##### Usage Notes

1. The command uses the current process context in the debugger.
2. `Addresses` can be specified in various formats:
   - `Hexadecimal`: Prefixed with '0x' (e.g., 0x00656789)
   - `Decimal`: Plain number (e.g., 6789456)
   - `Symbol` name: If symbols are loaded (e.g., &myVariable)
3. Size can use expressions for convenience (e.g., 1024*1024 for 1 MB).
4. Ensure that both source and destination memory ranges are within the process's address space.
5. The destination range should be writable.
6. Be cautious when source and destination ranges overlap, as it may lead to unexpected results.

##### Examples

1. Basic usage:

   {: .code-box}
   ```
   memcpy 0x00656589 0x00656789 200
   ```
   Copies 200 bytes from address 0x00656789 to address 0x00656589.

2. Using symbol names:

   {: .code-box}
   ```
   memcpy &destBuffer &sourceBuffer 256
   ```
   Copies 256 bytes from the address of `sourceBuffer` to the address of `destBuffer`.

3. Copying a larger region:

   {: .code-box}
   ```
   memcpy 0x20000000 0x10000000 1024*1024
   ```
   Copies 1 MB of data from address 0x10000000 to address 0x20000000.

##### Error Handling

- Invalid or inaccessible address: Shows an error if either the source or destination address is invalid or not accessible.
- Destination not writable: Displays an error message if the destination range is not writable.
- Size exceeds available memory: Copies as much as possible and reports actual bytes copied.
- Memory read/write issues: Shows appropriate error messages if unable to read from source or write to destination.

##### Example Code and Usage

<div class="code-box">
>{: .code-header}
>Sample code
> <button onclick="copyCode(this)" class="copy-button">Copy</button>

```cpp
#include <cstdlib>
#include <cstring>
#include <cstdio>

int main()
{
    // Buffer sizes
    int sourceSize = 48;
    int destSize = 48;
    
    // Create buffers
    char* sourceBuffer = (char*)malloc(sourceSize);
    char* destBuffer = (char*)malloc(destSize);
    
    // Fill source buffer with a pattern
    for (int i = 0; i < sourceSize; i++) {
        sourceBuffer[i] = 'A' + (i % 26);
    }
    
    // Initialize destination buffer with 'X'
    memset(destBuffer, 'X', destSize);
    
    printf("Before memcpy:\n");
    printf("Source buffer: %.*s\n", sourceSize, sourceBuffer);
    printf("Dest buffer:   %.*s\n", destSize, destBuffer);
    
    // Use memcpy here to copy data from sourceBuffer to destBuffer
    
    printf("\nAfter memcpy:\n");
    printf("Source buffer: %.*s\n", sourceSize, sourceBuffer);
    printf("Dest buffer:   %.*s\n", destSize, destBuffer);
    
    // Release memory
    free(sourceBuffer);
    free(destBuffer);
    return 0;
}
```
</div>

After initializing the buffers and before the second print statement, you can use `memcpy` to copy the contents of `sourceBuffer` to `destBuffer`:

{: .code-box}
```
memcpy destBuffer sourceBuffer 48
```

When you run the program after using `memcpy`, it will output:

{: .code-box}
```
Before memcpy:
Source buffer: ABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUV
Dest buffer:   XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX

After memcpy:
Source buffer: ABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUV
Dest buffer:   ABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUV
```

This example demonstrates how `memcpy` can be used to copy data between different memory locations within a program, which can be particularly useful for manipulating data structures, creating backups, or setting up specific memory states for testing and debugging purposes.