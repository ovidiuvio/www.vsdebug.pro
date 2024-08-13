---
layout: features
title: Memory | VSDebugPro
keywords: VSDebugPro documentation, debugging tutorials, memory manipulation, command reference, debugging techniques, Visual Studio extension guide
description: Learn how to use VSDebugPro with our comprehensive documentation. Discover powerful commands, explore common concepts, and unlock advanced debugging techniques to simplify even the most complex debugging tasks.
---
{::options parse_block_html="true" /}

### VSDebugPro Memory Features
---
VSDebugPro offers a robust set of memory manipulation features to enhance your debugging experience. These tools allow you to examine, modify, and analyze memory in various ways, providing deep insights into your application's behavior.

##### Memory Dump
- **Purpose**: Saves a specified region of memory to a file.
- **Command**: [dumpmem](/pages/docs/dumpmem.html)
- **Usage**:

  {: .code-box} 
  ```
  dumpmem <filename> <address> <size>
  ```

- **Example**: 

  {: .code-box}
  ```
  dumpmem c:\memdump.bin 0x00656789 200
  ```

- **Tutorial**: [Save memory](/pages/tutorials/dumpbuffer.html)

##### Hex Dump
- **Purpose**: Displays memory content in hexadecimal and ASCII format.
- **Command**: [hexdump](/pages/docs/hexdump.html)
- **Usage**: 

  {: .code-box}
  ```
  hexdump <filename> <address> <size> [columns] [bytesPerRow]
  ```

- **Example**: 

  {: .code-box}
  ```
  hexdump c:\hexdump.txt 0x00656789 200 8 32
  ```

- **Tutorial**: [C# hexdump](/pages/tutorials/dumpsharpbytes.html)

##### Memory Copy
- **Purpose**: Copies data from one memory region to another.
- **Command**: [memcpy](/pages/docs/memcpy.html)
- **Usage**: 

  {: .code-box}
  ```
  memcpy <dst> <src> <size>
  ```

- **Example**: 

  {: .code-box}
  ```
  memcpy 0x00656589 0x00656789 200
  ```

##### Memory Set
- **Purpose**: Fills a block of memory with a specified value.
- **Command**: [memset](/pages/docs/memset.html)
- **Usage**: 

  {: .code-box}
  ```
  memset <dst> <val> <size>
  ```

- **Example**: 

  {: .code-box}
  ```
  memset 0x00656589 0xFF 200
  ```

##### Memory Allocation
- **Purpose**: Allocates memory in the debugged process.
- **Command**: [malloc](/pages/docs/malloc.html)
- **Usage**: 

  {: .code-box}
  ```
  malloc <size>
  ```

- **Example**: 

  {: .code-box}
  ```
  malloc 200
  ```

##### Memory Deallocation
- **Purpose**: Releases previously allocated memory.
- **Command**: [free](/pages/docs/free.html)
- **Usage**: 

  {: .code-box}
  ```
  free <address>
  ```

- **Example**: 

  {: .code-box}
  ```
  free 0x00500000
  ```

##### Memory Load
- **Purpose**: Loads data from a file into memory.
- **Command**: [loadmem](/pages/docs/loadmem.html)
- **Usage**: 

  {: .code-box}
  ```
  loadmem <srcfile> <address> <size>
  ```

- **Example**: 

  {: .code-box}
  ```
  loadmem c:\memdata.bin 0x00656789 200
  ```

