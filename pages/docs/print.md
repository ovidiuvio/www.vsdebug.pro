---
layout: docs
title: Print | VSDebugPro
keywords: VSDebugPro, debugging command, data analysis, program debugging, visual studio debugging, print, print symbol, c++ print
description: Performs a structured dump of the callstack for the current thread or all threads in the debugged process.
---
{::options parse_block_html="true" /}

##### print (Print Symbol Command)
---

##### Description
The `print` command in VSDebugPro evaluates and displays the value of a symbol or expression in the current debug context. It's a versatile tool for quick inspection of variables, memory, and complex expressions during a debugging session.

{: .code-box}
>{: .code-header}
>Syntax
```
print <expression>
```

##### Parameters

- `<expression>`: The symbol, variable, or expression to evaluate and print.

##### Usage Examples

1. Print a simple variable:

    {: .code-box}
    ```
    print myVariable
    ```

2. Print a member of a structure:

    {: .code-box}
    ```
    print myObject.memberVariable
    ```

3. Print an array element:

    {: .code-box}
    ```
    print myArray[5]
    ```

4. Print the result of an expression:

    {: .code-box}
    ```
    print (x * y + z)
    ```

5. Print a dereferenced pointer:

    {: .code-box}
    ```
    print *myPointer
    ```

6. Print the address of a variable:

    {: .code-box}
    ```
    print &myVariable
    ```

7. Print a cast expression:

    {: .code-box}
    ```
    print (int*)myVoidPointer
    ```

8. Print a function call result (be cautious with side effects):

    {: .code-box}
    ```
    print myObject.calculateValue()
    ```

##### Output Format

The output format depends on the type of the evaluated expression:

- For basic types (int, float, char, etc.), it prints the value directly.
- For strings, it prints the content of the string.
- For pointers, it prints the memory address.
- For complex types (structs, classes), it prints a structured view of the object's contents.
- For arrays, it prints the elements (up to a certain limit).

##### Best Practices

1. Use `print` for quick inspection of variables and expressions.
2. For complex data structures, consider using `print` to inspect specific members rather than the entire object.
3. When debugging, use `print` to verify assumptions about variable values or expression results.
4. Combine `print` with conditional breakpoints to print values only when specific conditions are met.
5. Remember that function calls in `print` expressions will execute in the debugged process, which may have side effects.
6. Printing large objects will take some time and currently blocks the ui.