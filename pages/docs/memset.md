---
layout: docs
---
{::options parse_block_html="true" /}

##### memset (Memory Set Utility)
---

##### Description
The `memset` command allows you to fill a block of memory with a specified value in the debugged process. This feature is useful for initializing memory regions, clearing data, or setting up specific memory patterns for testing and debugging purposes.

{: .code-box}
>{: .code-header}
>Syntax
```
memset <dst> <val> <size>
```

##### Parameters

- `<dst>`: Destination `address` where the memory will be set.
- `<val>`: The value to set (0x00 - 0xFF). This is treated as a byte value.
- `<size>`: Number of bytes to set starting from the destination address.

##### Usage Notes

1. The command uses the current process context in the debugger.
2. The destination `address` can be specified in various formats:
   - `Hexadecimal`: Prefixed with '0x' (e.g., 0x00656789)
   - `Decimal`: Plain number (e.g., 6789456)
   - `Symbol` name: If symbols are loaded (e.g., &myVariable)
3. The value parameter is interpreted as a byte (0-255 or 0x00-0xFF).
4. Size can use expressions for convenience (e.g., 1024*1024 for 1 MB).
5. Ensure that the destination memory range is within the process's address space and is writable.

##### Examples

1. Basic usage:

   {: .code-box}
   ```
   memset 0x00656589 0xFF 200
   ```
   Sets 200 bytes starting at address 0x00656589 to the value 0xFF.

2. Using a symbol name:

   {: .code-box}
   ```
   memset &myBuffer 0x00 1024
   ```
   Clears (sets to zero) 1024 bytes starting at the address of `myBuffer`.

3. Setting a larger region:

   {: .code-box}
   ```
   memset 0x20000000 0xAA 1024*1024
   ```
   Sets 1 MB of memory starting at address 0x20000000 to the value 0xAA.

##### Error Handling

- Invalid or inaccessible address: Shows an error if the destination address is invalid or not accessible.
- Destination not writable: Displays an error message if the destination range is not writable.
- Invalid value: Reports an error if the specified value is not within the valid range (0-255).
- Size exceeds available memory: Sets as much as possible and reports actual bytes set.
- Memory write issues: Shows appropriate error messages if unable to write to the specified memory range.

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
    // Buffer size
    int bufferSize = 48;
    
    // Create buffer
    char* buffer = (char*)malloc(bufferSize);
    
    // Initialize buffer with a pattern
    for (int i = 0; i < bufferSize; i++) {
        buffer[i] = 'A' + (i % 26);
    }
    
    printf("Before memset:\n");
    printf("Buffer: %.*s\n", bufferSize, buffer);
    
    // Use memset here to fill part of the buffer
    
    printf("\nAfter memset:\n");
    printf("Buffer: %.*s\n", bufferSize, buffer);
    
    // Release memory
    free(buffer);
    return 0;
}
```
</div>

After initializing the buffer and before the second print statement, you can use `memset` to fill part of the buffer with a specific value:

{: .code-box}
```
memset buffer+16 0x58 16
```

This command will set 16 bytes starting at `buffer+16` to the value 0x58 (ASCII 'X').

When you run the program after using `memset`, it will output:

{: .code-box}
```
Before memset:
Buffer: ABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUV

After memset:
Buffer: ABCDEFGHIJKLMNOPXXXXXXXXXXXXXXXXGHIJKLMNOPQRSTUV
```

This example demonstrates how `memset` can be used to fill a specific region of memory with a given value. This is particularly useful for initializing data structures, clearing sensitive information, or creating specific memory patterns for testing and debugging purposes.