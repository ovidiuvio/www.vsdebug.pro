---
layout: docs
---
{::options parse_block_html="true" /}

##### loadmem (Memory Load Utility)
---

##### Description
The `loadmem` command allows you to load data from a file into the memory of the debugged process. This feature is useful for restoring saved memory states, injecting data, or setting up specific memory conditions for testing and debugging.

{: .code-box}
>{: .code-header}
>Syntax
```
loadmem <file> <address> <size>
```

##### Parameters

- `<file>`: Path and name of the input file containing the data to be loaded into memory.
- `<address>`: Destination address in memory where the data will be loaded.
- `<size>`: Number of bytes to load from the file into memory.

##### Usage Notes

1. The command uses the current process context in the debugger.
2. `Address` can be specified in various formats:
   - `Hexadecimal`: Prefixed with '0x' (e.g., 0x00656789)
   - `Decimal`: Plain number (e.g., 6789456)
   - `Symbol` name: If symbols are loaded (e.g., &myVariable)
3. Size can use expressions for convenience (e.g., 1024*1024 for 1 MB).
4. If the specified size is larger than the file size, only the available data will be loaded.
5. Ensure that the destination memory range is writable and within the process's address space.

##### Examples

1. Basic usage:

   {: .code-box}
   ```
   loadmem c:\temp\memdata.bin 0x00656789 200
   ```
   Loads 200 bytes from the file `c:\temp\memdata.bin` into memory starting at address 0x00656789.

2. Using a symbol name:

   {: .code-box}
   ```
   loadmem c:\temp\variable_data.bin &myGlobalVar 256
   ```
   Loads 256 bytes from the file `c:\temp\variable_data.bin` into memory starting at the address of `myGlobalVar`.

3. Loading a larger region:

   {: .code-box}
   ```
   loadmem c:\temp\large_data.bin 0x10000000 1024*1024
   ```
   Loads 1 MB of data from the file `c:\temp\large_data.bin` into memory starting at address 0x10000000.

##### Error Handling

- File not found: Displays an error message if the source file doesn't exist.
- Invalid or inaccessible address: Shows an error if the destination address is invalid or not writable.
- Size exceeds available file data: Loads as much as possible and reports actual bytes written.
- Memory write issues: Displays appropriate error message if unable to write to the specified memory range.