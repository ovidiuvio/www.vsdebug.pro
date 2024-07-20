---
layout: docs
title: Batch Commands | VSDebugPro
keywords: VSDebugPro, exec command, YAML scripts, batch commands, debugging automation, scripting, automated debugging tasks
description: Automate your debugging tasks with VSDebugPro's exec command. Learn how to create and run YAML scripts to execute sequences of commands, saving time and effort during complex debugging scenarios.
---
{::options parse_block_html="true" /}

##### exec (Execute Yaml Script)
---

##### Description
The `exec` command allows you to execute a series of commands defined in a YAML file. This feature enables you to create reusable scripts and automation for debugging tasks.

{: .code-box}
>{: .code-header}
>Syntax
```code
exec <yamlFilePath> [arg1] [arg2] ... [argN]
```

- `<yamlFilePath>`: Path to the YAML file containing the commands to execute.
- `[arg1] [arg2] ... [argN]`: Optional arguments that can be passed to the YAML script.


#####  YAML File Structure
---
The YAML script has following structure:

<div class="code-box">
>{: .code-header}
>YAML Structure
> <button onclick="copyCode(this)" class="copy-button">Copy</button>

```yaml
variables:
  var1: value1
  var2: value2

commands:
  - command1
  - command2
  - command3
```
</div>

- `variables`: A dictionary of key-value pairs that can be used in the commands with mustache templating. Can be a *constant*, *watch expression*, or script *argument* and must not contain any spaces.
- `commands`: A list of commands to be executed in order.

#####  Variables Definition & Templating
---
Variables can be defined and templated in the following ways:

###### Constants:

<div class="code-box">
```yaml
variables:
  var1: "filename.txt"
```
</div>

###### Watch / Debugger expression for evaluation:
<div class="code-box">
>{: .code-header}
>Sample code
```cpp
int main()
{
    // buffer size
    int   bufferSize   = 1024;
    // create buffer
    void* buffer       = calloc(1, bufferSize);
    // release memory
    free(buffer);
    return 0;
}
```
</div>
<div class="code-box">
>{: .code-header}
>Script variables using definitions in the code
```yaml
variables:
  # var1 is evaluated in debugger and replaced with 1024 (see code above)
  var1: "bufferSize"
  # var2 is evaluated in debugger as (512+512) and replaced with result: 1024 (see code above)
  # NOTE: expressions must not contain spaces! "(512 + 512)" will not work.
  var2: "512+512"
```
</div>

###### Script arguments:

{: .code-box}
```
exec dump.yaml buffer.bin buffer 1024
```


<div class="code-box">
>{: .code-header}
>dump.yaml
{% raw %}
```yaml
variables:
  file: "{{$1}}"
  address: "{{$2}}"
  size: "{{$3}}"

commands:
  - dumpmem -f {{file}} {{address}} {{size}}
```
{% endraw %}
</div>

The above script results in the following command execution:

{: .code-box}
```
dumpmem buffer.bin buffer 1024
```

#####  Example code and yaml script 
---
<div class="code-box">
>{: .code-header}
>CPP Code sample
> <button onclick="copyCode(this)" class="copy-button">Copy</button>

```cpp
#include <stdint.h>
#include <Windows.h>

int main()
{
    // buffer size
    int   segmentSize = 16;
    // number of segments
    int   numSegments = 3;
    // create buffer
    char* buffer = (char*)calloc(numSegments, segmentSize);
    
    memset(buffer + (0 * segmentSize), 0xA0, segmentSize);
    memset(buffer + (1 * segmentSize), 0xB0, segmentSize);
    memset(buffer + (2 * segmentSize), 0xC0, segmentSize);

    // release memory
    free(buffer);

    return 0;
}
```
</div>

[Download](https://dl.vsdebug.pro/CodeSamples/VSDebugProTestAppScripting.zip)

The script below will split the buffer in 3 segment files, and also write all 3 segments in reverse order in `segments.bin`:

<div class="code-box">
>{: .code-header}
>YAML Script
> <button onclick="copyCode(this)" class="copy-button">Copy</button>

{% raw %}
```yaml
variables:
  # 'buffer' is evaluated at runtime in debug engine api
  ptr_base: "buffer"
  # 'segmentSize' variable will be valuated at execution time in debug engine api
  size: "segmentSize"
  # expressions don't support spaces. 'buffer+(0*segmentSize)' is evaluated later in debug engine api
  # ptr_base mustache variable will be replaced  with 'buffer'
  segData0: "{{ptr_base}}+(0*segmentSize)"
  segFile0: "segment0.bin"
  # expressions don't support spaces.
  segData1: "{{ptr_base}}+(1*segmentSize)"
  segFile1: "segment1.bin"
  # expressions don't support spaces.
  segData2: "{{ptr_base}}+(2*segmentSize)"
  segFile2: "segment2.bin"

commands:
  # write each individual segment to a file
  - dumpmem -f {{segFile0}} {{segData0}} {{size}}
  - dumpmem -f {{segFile1}} {{segData1}} {{size}}
  - dumpmem -f {{segFile2}} {{segData2}} {{size}}
  # write all segments to a single file, but in reverse order
  - dumpmem -a segments.bin {{segData2}} {{size}}
  - dumpmem -a segments.bin {{segData1}} {{size}}
  - dumpmem -a segments.bin {{segData0}} {{size}}
```
{% endraw %}
</div>

<div class="code-box">
>{: .code-header}
>Script Execution
```console
>exec segments.yaml
Wrote: 16 bytes to: <file://E:\workspace\segment0.bin>.
Wrote: 16 bytes to: <file://E:\workspace\segment1.bin>.
Wrote: 16 bytes to: <file://E:\workspace\segment2.bin>.
Wrote: 16 bytes to: <file://E:\workspace\segments.bin>.
Wrote: 16 bytes to: <file://E:\workspace\segments.bin>.
Wrote: 16 bytes to: <file://E:\workspace\segments.bin>.
```
</div>

The resulting files have the following content:
<div class="code-box">
>{: .code-header}
>segment0.bin
```code
A0 A0 A0 A0 A0 A0 A0 A0 A0 A0 A0 A0 A0 A0 A0 A0
```
</div>
<div class="code-box">
>{: .code-header}
>segment1.bin
```code
B0 B0 B0 B0 B0 B0 B0 B0 B0 B0 B0 B0 B0 B0 B0 B0
```
</div>
<div class="code-box">
>{: .code-header}
>segment2.bin
```code
C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0
```
</div>
<div class="code-box">
>{: .code-header}
>segments.bin
```code
C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 
B0 B0 B0 B0 B0 B0 B0 B0 B0 B0 B0 B0 B0 B0 B0 B0 
A0 A0 A0 A0 A0 A0 A0 A0 A0 A0 A0 A0 A0 A0 A0 A0
```
</div>

