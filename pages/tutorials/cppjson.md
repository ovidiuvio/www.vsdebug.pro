---
layout: docs
overview: true
title: Tutorial - C++ Json serialization | VSDebugPro
keywords: VSDebugPro tutorial, memory dump tutorial, save memory to file, c++ json serialization, cpp json
description: This tutorial provides a step-by-step guide on serializing c++ objects to json at debug time
---

---
{::options parse_block_html="true" /}

##### Serialize C++ objects to json

This article shows how to serialize c++ objects to json in Visual Studio, while debugging the program,
without writing any code.

<img src="/assets/img/ft_json.webp" width="100%"/>

<div class="code-box">
>{: .code-header}
>Sample code
> <button onclick="copyCode(this)" class="copy-button">Copy</button>

{% raw %}
```cpp
// Nested container with custom class
std::vector<std::map<std::string, Person>> people_vector = {
    {{"person1", Person("Alice", 30)}, {"person2", Person("Bob", 25)}},
    {{"person3", Person("Charlie", 35)}, {"person4", Person("David", 28)}}
};
```
{% endraw %}
</div>

###### Steps to serialize `people_vector` to json:

1. Create a simple c++ program with the above code snippet.
1. Compile the program and place a breakpoint after the `people_vector` definition.
2. Start debugging the program and run it until it hits the breapoint.
3. Go to Extensions->VSDebugPro menu and open **Console**.
4. Print or export the object to json with the following command

<div class="code-box">
```
print -j people_vector
```
</div>

<div class="code-box">
```
export -j people.json people_vector
```
</div>

The [print](/pages/docs/print.html) and [export](/pages/docs/export.html) commands are using the Visual Studio C++ debugger interface to automatically evaluate and expand `people_vector` into a full json representation.