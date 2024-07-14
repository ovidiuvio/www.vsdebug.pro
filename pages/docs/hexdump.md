---
layout: docs
title: Hex Dump | VSDebugPro - Enhanced debugging for Visual Studio
---
{::options parse_block_html="true" /}

##### hexdump (Hex Dump Utility)
---

##### Description
The `hexdump` command in VSDebugPro allows you to dump a block of memory from the target process and save it as a formatted hex dump file. This is useful for inspecting raw memory contents in a human-readable format.

{: .code-box}
>{: .code-header}
>Syntax
```code
hexdump <optional flags> <filename> <address> <size> [columns] [bytesPerRow]
```

##### Parameters

- `<optional flags>`:
    - `-f`: Force file overwrite if the output file already exists.
    - `-a`: Append the hex dump to the existing output file.
- `<filename>`: The name of the output file where the hex dump will be saved. If no path is specified, the file will be created in the current working directory.
- `<address>`: The starting memory address to dump. This can be a hexadecimal value, a pointer, or an expression that evaluates to a valid memory address.
- `<size>`: The size in bytes of the memory block to dump. This can be a decimal or hexadecimal value, or an expression that evaluates to a valid size.
- `[columns]` (optional): The number of byte columns in the hex dump output. Defaults to 8 if not specified.
- `[bytesPerRow]` (optional): The number of bytes per row in the hex dump output. Defaults to 16 if not specified.

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
   hexdump c:\hexdump.txt 0x00656789 200
   ```
   Dump 200 bytes from address `0x00656789` to file `c:\hexdump.txt`.

2. Using force overwrite:

   {: .code-box}
   ```
   hexdump -f hexdump.txt 0x00656789 200
   ```
   Overwrites `hexdump.txt` if it already exists.

3. Appending to an existing file:

   {: .code-box}
   ```
   hexdump -a hexdump.txt 0x00656789 200
   ```
   Appends 200 bytes to the end of `hexdump.txt` if it exists.

4. Using a symbol name:

   {: .code-box}
   ```
   hexdump dump.txt myPointer 100
   ```
   Dumps 100 bytes starting from the address of `myPointer`.

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

After running to the point just before `free(buffer)`, you can use `hexdump` to capture the buffer contents:

{: .code-box}
```
hexdump buffer.txt buffer 32
```

The resulting `buffer.txt` file will contain:

{: .code-box}
>{: .code-header}
>buffer.txt
```
1D11ED5F300  AB AB AB AB AB AB AB AB  AB AB AB AB AB AB AB AB  |««««««««««««««««|
1D11ED5F310  AB AB AB AB AB AB AB AB  AB AB AB AB AB AB AB AB  |««««««««««««««««|
```

{: .code-box}
```
hexdump -f buffer.txt buffer 32 4
```

The resulting `buffer.txt` file will contain:

{: .code-box}
>{: .code-header}
>buffer.txt
```
1D11ED5F300  AB AB AB AB  AB AB AB AB  AB AB AB AB  AB AB AB AB  |««««««««««««««««|
1D11ED5F310  AB AB AB AB  AB AB AB AB  AB AB AB AB  AB AB AB AB  |««««««««««««««««|
```

{: .code-box}
```
hexdump -f buffer.txt buffer 32 2 8
```

The resulting `buffer.txt` file will contain:

{: .code-box}
>{: .code-header}
>buffer.txt
```
1D11ED5F300  AB AB  AB AB  AB AB  AB AB  |««««««««|
1D11ED5F308  AB AB  AB AB  AB AB  AB AB  |««««««««|
1D11ED5F310  AB AB  AB AB  AB AB  AB AB  |««««««««|
1D11ED5F318  AB AB  AB AB  AB AB  AB AB  |««««««««|
```

{: .code-box}
```
hexdump -f buffer.txt buffer 32 2 4
```

The resulting `buffer.txt` file will contain:

{: .code-box}
>{: .code-header}
>buffer.txt
```
1D11ED5F300  AB AB  AB AB  |««««|
1D11ED5F304  AB AB  AB AB  |««««|
1D11ED5F308  AB AB  AB AB  |««««|
1D11ED5F30C  AB AB  AB AB  |««««|
1D11ED5F310  AB AB  AB AB  |««««|
1D11ED5F314  AB AB  AB AB  |««««|
1D11ED5F318  AB AB  AB AB  |««««|
1D11ED5F31C  AB AB  AB AB  |««««|
```

Check these tutorials for more:

[Save Memory](/pages/tutorials/dumpbuffer.html)

[Save Image](/pages/tutorials/dumpimg.html)
