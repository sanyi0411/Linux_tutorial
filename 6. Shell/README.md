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
- By default variables a global
- They can use the `local` keyword
```bash
GLOBAL_VAR=5

myfunc() {
    local LOCAL_VAR=6
}
```

## Special variables
- special variables outside of functions:
```bash
#!/bin/bash

echo "Script Name: $0"
echo "First Argument: $1"
echo "Second Argument: $2"
echo "All Arguments: $@"
echo "Number of Arguments: $#"
echo "Process ID: $$"
echo "Exit status of last executed command: $?"
echo "Process ID of last background command: $!"
```

- special variables inside a function:
```bash
#!/bin/bash

function print_args {
  echo "Function Name: $FUNCNAME"
  echo "Function first Argument: $1"
  echo "Function second Argument: $2"
  echo "Function all Arguments: $@"
  echo "Number of Arguments: $#"
}

print_args 1 two 3 four
```

### Difference between `"$@"` and `"$*"`
- `$@` and `"$@"` are not the same
- `$*` and `"$*"` are not the same
- `"$@"`treats each arguments as a separate entity, like an array, and arguments with spaces are preserved
- `$*` combines all arguments into a single string

## Read input
```bash
echo "Enter your name: "
read name
echo "Hello $(name)"
```

## Arrays
- In Bash arrays are defined by enclosing the elements in parentheses `()` and separating them with spaces

```bash
NAMES=("Alice" "Bob" "Claire" "Daniel")
NAMES[0]
NAMES[1]
NAMES[2]
NAMES[@] // All elements
```

## If statements
```bash
#!/bin/bash

if [ condition ]; then
  # code to be executed if the condition is true
fi
```
```bash
#!/bin/bash

if [ condition1 ]; then
  # code to be executed if the condition1 is true
elif [ condition2 ]; then
  # code to be executed if the condition2 is true
else
  # code to be executed if the other conditions are false
fi
```
- `-eq` equals
- `-lt` less than
- `-gt` greater than
- `-le` less than or equal to
- `-ge` greater than or equal to

```bash
name="Alice"
if [ $name -eq "Alice" ]; then
  echo "Hello, Alice"
fi
```

```bash
age=23
if [ $age -ge 18 ]; then
  echo "You can buy beer"
fi
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

a=(3 5 8 10 6)

for x in "${a[@]}"; do
    echo $x
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

## Functions
- Creating and calling a function without parameters:
```bash
#!/bin/bash

greet() {
  echo "Hello World!"
}

greet
```

- Function with parameters:
```bash
calculate() {
  echo "The sum of $1 and $2 is $(($1 + $2))"
}

calculate 5 3
```

- Functions is shell don't return values. They can either `echo` a value, that can be captured, or they can modify a global variable
- `echo`ing a result:
```bash
get_square() {
  echo $(($1 * $1))
}

result=$(get_square 5)
```
- modifying a global variable:
```bash
RESULT=0
set_global_result() {
  RESULT=$(($1 * $1))
}
```

## Switch case
```bash
#!/bin/bash

ENGLISH_CALC() {
  local num1=$1
  local operation=$2
  local num2=$3
  local result

  case $operation in
    plus)
      result=$((num1 + num2))
      echo "$num1 + $num2 = $result"
      ;;
    minus)
      result=$((num1 - num2))
      echo "$num1 - $num2 = $result"
      ;;
    times)
      result=$((num1 * num2))
      echo "$num1 * $num2 = $result"
      ;;
    *)
      echo "Invalid operation. Please use 'plus', 'minus', or 'times'."
      return 1
      ;;
  esac
}
```