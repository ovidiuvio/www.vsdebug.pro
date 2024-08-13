---
layout: features
title: Workspace | VSDebugPro
keywords: VSDebugPro features, debugging tutorials, memory manipulation, command reference, debugging techniques, Visual Studio extension guide
description: Learn how to use VSDebugPro with our comprehensive documentation. Discover powerful commands, explore common concepts, and unlock advanced debugging techniques to simplify even the most complex debugging tasks.
---
{::options parse_block_html="true" /}

### Workspace
---
The **Workspace** or `Working Directory` is an important concept in VSDebugPro that provides a default location for commands file operations, logs, and scripts. 
Here are the key points about the working directory:
- **Central location:** The working directory acts as a central, default location for saving files, loading data, and other file operations performed through VSDebugPro commands.
- **Configurable:** Users can set and change the working directory in the VSDebugPro [settings](/pages/features/console.html#settings) <img src="/assets/img/settings.png" width="3%"/>. This allows you to customize where files are saved/loaded by default.

    <img src="/assets/img/ft_settings_workspace.webp" width="60%"/>

- **Default for relative paths:** When using VSDebugPro commands that involve file paths, if you provide a relative path (not a full path), it will be relative to this working directory.
- **Convenience:** By setting up a working directory, you don't have to specify full file paths every time you use a command. You can just use filenames or relative paths.
- **Organization:** It helps keep files generated or used by VSDebugPro organized in one location, rather than scattered across your system.
- **Fallback location:** If no specific path is provided in a command, the working directory is used as the default location.
- **Accessibility:** The working directory can be quickly accessed using the "Explore Working Directory" <img src="/assets/img/wd.png" width="3%"/> command in VSDebugPro.

For example, if your working directory is set to `C:\DebugData` and you use [dumpmem](/pages/docs/dumpmem.html) command like this: `dumpmem output.bin 0x00656789 200`, the resulting file will be saved as `C:\DebugData\output.bin`.

Setting up and using a working directory can streamline your workflow when using VSDebugPro, especially if you frequently work with files in your debugging sessions.