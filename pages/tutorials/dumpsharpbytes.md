---
layout: docs
overview: true
title:  Tutorial - Save c# array | VSDebugPro - Enhanced debugging for Visual Studio
keywords: VSDebugPro tutorial, C# debugging, save byte array to file, data inspection, offline analysis, C# array manipulation
description: Effortlessly save C# byte arrays to disk during debugging with VSDebugPro. This tutorial guides you through the process of dumping array contents to a file, allowing for convenient offline analysis and data inspection.
---

---
{::options parse_block_html="true" /}

##### Save a c# array to disk

This article shows how to dump a C# byte array to a file, while debugging the program and without writing any code to save the data.

<div class="code-box">
>{: .code-header}
>Sample C# code
> <button onclick="copyCode(this)" class="copy-button">Copy</button>

```csharp
// See https://aka.ms/new-console-template for more information
var bytes = new byte[1024];
for (int i = 0; i < bytes.Length; i++)
    bytes[i] = (byte)i;

Console.WriteLine(bytes);
```
</div>

###### Steps to dump `bytes` contents to disk:

1. Start debugging the program.
2. Place a breakpoint at a carefully select point in code, where our data is available (on `Console.WriteLine(bytes)`).
3. Go to VSDebugPro menu and open **Console**.

<div class="code-box">
```
dumpmem bytes.bin &bytes[0] 1024 
```
</div>

The `dumpmem` utility uses the Visual Studio debugger interface to automatically evaluate
the address of `&bytes[0]`

The `hexdump` command (very similar to dumpmem) can be used to dump bytes in hex format in a text file

<div class="code-box">
```
hexdump bytes.txt &bytes[0] 1024 256 256
```
</div>

<div class="code-box">
>{: .code-header}
>bytes.txt
```code
2096F50D2E0  00 01 02 03 04 05 06 07 08 09 0A 0B 0C 0D 0E 0F 10 11 12 13 14 15 16
2096F50D3E0  00 01 02 03 04 05 06 07 08 09 0A 0B 0C 0D 0E 0F 10 11 12 13 14 15 16
2096F50D4E0  00 01 02 03 04 05 06 07 08 09 0A 0B 0C 0D 0E 0F 10 11 12 13 14 15 16
2096F50D5E0  00 01 02 03 04 05 06 07 08 09 0A 0B 0C 0D 0E 0F 10 11 12 13 14 15 16
```
</div>

##### Usage Notes
- C# objects are stored on the managed heap, which is managed by the .NET runtime.
- The memory layout of an object includes its header, type information, and the values of its fields.
  Ex:
  The bytes array in the example has the following view in the memory window:
  <img src="/assets/img/sharpmem.png" width="70%"/> \
  The first 16 bytes are the header, and the data starts at offset 16. \
  `bytes (0x000002096F50D2D0)` \
  `&bytes[0] (0x000002096f50d2e0)`
- Every object in C# has a header, which is not visible to the programmer.
- For reference types (classes), the object's memory contains the header and instance fields, while the reference itself is a pointer to this memory.
- Object Size Estimation: Estimating the object size can be tricky, especially for complex objects with nested structures.
- For value types (structs), when used as fields in a class, their data is embedded directly in the containing object's memory.
- Memory Layout Changes: The memory layout of C# objects can change between .NET versions or even between runs of your program.