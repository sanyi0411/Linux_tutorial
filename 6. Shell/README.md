## What is a shell?

The core of an operation system is called the `kernel`. For example Linux is a kernel.

A `shell` sits around this core and lets the user give commands to the computer. It is an interface between the user and the operating system.

A shell takes a command, interprests it and tells the operating system what to do. After that it shows the user the output and the errors, if there are any.

There are text based shells:
- Linux:
    - `sh` is the most basic shell, and a list of specifications and detailed descriptions
    - `bash` is a different shell, derived from `sh`, a superset of `sh` but with more features and better syntax
- Windows:
    - `cmd` or command prompt
    - `powershell`

And there are graphical shells:
- Linux:
    - GNOME
    - KDE
- Windows:
    - Windows Desktop

## Basic architecture

```
+-----+       +-------+       +-----------+      +----------+
| You | --->  | Shell |  ---> | OS Kernel | ---> | Hardware |
+-----+       +-------+       +-----------+      +----------+
```

## Shell commands
Shell commands are implemented inside the shell itself.

Unlike [Linux commands](../5.%20Linux%20commands/), they are not separate executables and using them does not require creating a new process.

There are commands that exist both as a Linux commands (for POSIX compatibility) and as a shell built-in command (faster). 