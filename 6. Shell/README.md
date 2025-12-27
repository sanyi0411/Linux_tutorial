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

There are commands that exist both as a Linux command (for POSIX compatibility) and as a shell built-in command (faster).

## TODO

## Variables

## Arrays

```bash
NAMES=("Alice" "Bob" "Claire" "Daniel")
NAMES[0]
NAMES[1]
NAMES[2]
NAMES[@] // All elements
```

## For loops

- For each item it this list, do something
- Loop through a range of numbers:
```bash
for i in {1..5}; do
    echo "Number: $i"
done
```

- Loop through an array:
```bash
NAMES=("Alice" "Bob" "Claire" "Daniel")

for name in "${NAMES[@]}"; do
    echo "Hello, $name!"
done
```

## While loops

- Executes a block of code as long as the specified condition is true
```bash
count=0
while [ $count -le 5 ]; do
    echo $count
    count=$((count + 1))
done
```

## Until loops

- Executes a block of code until the specified condition becomes true
```bash
count=1
until [ $count -gt 5 ]; do
    echo $count
    count=$((count + 1))
done
```

## Continue

- Skips the rest of the code in the current iteration and moves on to the next iteration
- To skip even numbers:
```bash
for i in {1..10}; do
  if [ $((i % 2)) -eq 0 ]; then
    continue
  fi
  echo $i
done
```
```
1
3
5
7
9
```

## Break
- Exits a loop early, thus skipping all other iterations
- To break out of the loop when the number reaches 6:
```bash
for i in {1..10}; do
  if [ $i -eq 6 ]; then
    echo "Break at $i"
    break
  fi
  echo $i
done
```
```
1
2
3
4
5
Break at 6
```