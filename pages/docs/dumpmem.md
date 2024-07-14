---
layout: docs
title: Memory Dump | VSDebugPro - Enhanced debugging for Visual Studio
---
{::options parse_block_html="true" /}

##### dumpmem (Memory Dump Utility)
---

##### Description
The `dumpmem` command allows you to dump memory contents from the debugged process to a file. This feature is useful for offline analysis, comparison, or backup of memory regions.

{: .code-box}
>{: .code-header}
>Syntax
```code
dumpmem [options] <filename> <address> <size>
```

##### Parameters

- `<filename>`: Path and name of the output file where memory contents will be saved.
- `<address>`: Starting address in memory to begin the dump.
- `<size>`: Number of bytes to dump from the starting address.

##### Options

- `-f`: Force overwrite. Overwrites the output file if it already exists.
- `-a`: Append mode. Appends new data to the end of an existing file.

##### Usage Notes

1. The command uses the current process context in the debugger.
2. Address can be specified in various formats:
   - Hexadecimal: Prefixed with '0x' (e.g., 0x00656789)
   - Decimal: Plain number (e.g., 6789456)
   - Symbol name: If symbols are loaded (e.g., &myVariable)
3. Size can use expressions for convenience (e.g., 1024*1024 for 1 MB) (must not have spaces).
4. Without `-f` or `-a`, the command returns an error if the output file exists.

##### Examples

1. Basic usage:

   {: .code-box}
   ```
   dumpmem c:\temp\memdump.bin 0x00656789 200
   ```
   Dumps 200 bytes starting from address 0x00656789 to the file `c:\temp\memdump.bin`.

2. Using force overwrite:

   {: .code-box}
   ```
   dumpmem -f c:\temp\memdump.bin 0x00656789 200
   ```
   Overwrites `c:\temp\memdump.bin` if it already exists.

3. Appending to an existing file:

   {: .code-box}
   ```
   dumpmem -a c:\temp\memdump.bin 0x00656789 200
   ```
   Appends 200 bytes to the end of `c:\temp\memdump.bin` if it exists.

4. Using a symbol name:

   {: .code-box}
   ```
   dumpmem c:\temp\variable_dump.bin &myGlobalVar 256
   ```
   Dumps 256 bytes starting from the address of `myGlobalVar`.

5. Dumping a larger region:

   {: .code-box}
   ```
   dumpmem c:\temp\large_dump.bin 0x10000000 1024*1024
   ```
   Dumps 1 MB of memory starting from address 0x10000000.

##### Error Handling

- Invalid or inaccessible address: Displays an error message.
- Size exceeds available memory: Dumps as much as possible and reports actual bytes written.
- Output file creation/write issues: Shows appropriate error message.

##### Example Code and Usage

<div class="code-box">
>{: .code-header}
>Sample code
> <button onclick="copyCode(this)" class="copy-button">Copy</button>

```cpp
int main()
{
    // buffer size
    int   bufferSize   = 16;
    // create buffer
    void* buffer       = calloc(1, bufferSize);

    // set some bytes into the buffer
    memset(buffer, 0xAB, bufferSize);

    // release memory
    free(buffer);

    return 0;
}
```
</div>

After running to the point just before `free(buffer)`, you can use `dumpmem` to capture the buffer contents:

{: .code-box}
```
dumpmem buffer.bin buffer bufferSize
```

The resulting `buffer.bin` file will contain:

{: .code-box}
>{: .code-header}
>buffer.bin
```
AB AB AB AB AB AB AB AB AB AB AB AB AB AB AB AB
```

Check these tutorials for more:

[Save Memory](/pages/tutorials/dumpbuffer.html)

[Save Image](/pages/tutorials/dumpimg.html)
