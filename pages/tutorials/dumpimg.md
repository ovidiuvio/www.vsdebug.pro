---
layout: docs
overview: true
title: Tutorial - Save image | VSDebugPro - Enhanced debugging for Visual Studio
---

---
{::options parse_block_html="true" /}

##### Inspect an image in memory

This article shows how to visualize a data buffer as an image, while debugging the program,
without writing a debugging function into the program and without recompiling it.

For this purpose we will use the following simple c code:

<div class="code-box">
```cpp
#define STB_IMAGE_IMPLEMENTATION
#include "stb_image.h"

int main()
{
    // image width
    int w = 0;  
    // imege height
    int h = 0;
    // number of channels
    int c = 0;

    // image data
    BYTE* img = stbi_load("Lenna.png", &w, &h, &c, 0);

    // release image data
    stbi_image_free(img);

    return 0;
}
```
</div>
In order to visualize the contents of `img` byte buffer above,  we are going
to dump its contents to a file and open it with `IrfanView`.

<div class="code-box">
```console
dumpmem
Dump memory utility.
------------------------------------------------------------------
Syntax: <dumpmem> <optional flags> <filename> <address> <size>
	EX: dumpmem c:\memdump.bin 0x00656789 200
	EX: dumpmem -f c:\memdump.bin 0x00656789 200
	Flags:
		  -f   - Force file overwrite.
		  -a   - Append to the file.
	<filename> - output filename
	<address>  - read address, must be a hex address / pointer, can be an expression
	<size>     - size in bytes, can be an expression
------------------------------------------------------------------
```
</div>
###### Steps to write the image to a file and load it in the viewer:

1. Start debugging the program.
2. Place a breakpoint at a carefully select point in code, where our data is available.
3. Go to VSDebugPro menu and click **Settings**.
4. Specifiy a path to an image viewer that can open raw files. Click OK.
5. Go to VSDebugPro menu and open **Console**.
6. Dump image data with the following command:
<div class="code-box">
```
dumpmem lenna.raw img w * h * c
```
</div>
7. Click on the file link in `VSD Console` to open the image in viewer.

The `dumpmem` utility uses the Visual Studio C++ debugger interface to automatically evaluate
the address of `img` and the size from `w * h * c` expression.

<iframe width="560" height="315" src="https://www.youtube.com/embed/w9otfmAO46Q" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

###### References

---

*[HxD](https://mh-nexus.de/en/hxd/) a free hex editor.*

*[IrfanView](https://www.irfanview.com/) freeware for non-commercial use image viewer.*

*[Stb Image](https://github.com/nothings/stb) public domain image loader single file library.*

*[Lenna png image](https://en.wikipedia.org/wiki/Lenna)*