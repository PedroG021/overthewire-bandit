# OverTheWire Bandit: Levels 0 to 7 Writeup

This document contains the documentation, methodology, and commands used to solve the initial block of the Bandit wargame, focusing on basic Linux file system navigation, text manipulation, and properties.

---

## Level 0 -> Level 1

### 🎯 Objective

Log into the game server using SSH and locate the initial flag.

### 🧠 Concepts & Commands

* `ssh`: Secure Shell client for logging into remote machines.
* `ls`: List directory contents.
* `cat`: Concatenate and display file contents.

### 💻 Solution

1. Connect to the host via SSH using the provided port and credentials:

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

2. List the files in the home directory to find the readme:

```bash
ls
```

3. Read the content of the file to retrieve the password for the next level:

```bash
cat readme
```

4. Password Secured: `[REDACTED]`

---


## Level 1 -> Level 2

### 🎯 Objective

Read the password stored in a file called `-` located in the current working directory.

### 🧠 Concepts & Commands

* **Special Filenames:** Relative paths `./-` to bypass command-line option processing.
* `ls`: List directory contents.
* `cat`: Concatenate and display file contents.

### 💻 Solution

1. List the files in the current directory to find the `-`:
```bash
ls
```

2. Read the content of the file which has a special name:
```bash
cat ./-
```

*(Note: The dash `-` normally represents stdin, so providing the relative path `./` forces the terminal to treat it as a literal file path).*


3. Password Secured: `[REDACTED]`

--- 

## Level 2 -> Level 3

### 🎯 Objective
Read the password stored in a file called `--spaces in this filename--` located in the working directory.

### 🧠 Concepts & Commands
* **Special Filenames (Dashes + Spaces):** Filenames starting with dashes (`--`) are incorrectly processed by CLI utilities as command options. Prepending a relative path (`./`) disables option processing, while double quotes (`""`) handle the spaces.
* `ls`: List directory contents.
* `cat`: Concatenate and display file contents.

### 💻 Solution

1. List the files in the working directory to find the target file:
```bash
ls
```

2. Read the content of the file which has a special name:
```bash
cat ./"--spaces in this filename--"
```
*(Note: Because the filename begins with `--`, the terminal mistakes it for a command flag. Prefixes like `./` force the system to treat it as a path, while double quotes preserve the spaces as a single argument).*

3. Password Secured: `[REDACTED]`

---

## Level 3 -> Level 4

### 🎯 Objective
Read the password stored in a hidden file located in the `inhere` directory.

### 🧠 Concepts & Commands
* **Hidden Files:** In Linux, files that start with a dot (`.`) are hidden by default and do not appear in standard directory listings.
* `ls`: List directory contents.
* `cd`: Change current working directory.
* `cat`: Concatenate and display file contents.

### 💻 Solution

1. List the files in the working directory to find the `inhere` directory:
```bash
ls
```

2. Change the working directory to the `inhere` directory:
```bash
cd inhere
```

3. List all files in the current directory using the long listing format:
```bash
ls -la
```
*(Note: The `-a` flag is required to display hidden files, while the `-l` flag provides the long listing format).*

4. Read the content of the hidden file:
```bash
cat ...Hiding-From-You
```
*(Note: In this scenario, you can write the filename without double quotes or prefixes like `./` because the filename starts with a dot (`.`), which cannot be misinterpreted by the CLI terminal).*

5. Password Secured: `[REDACTED]`

---

## Level 4 -> Level 5

### 🎯 Objective
Read the password stored in the only human-readable file in the `inhere` directory.

### 🧠 Concepts & Commands
* **Human-readable file:** A text file which can be read by humans.
* `ls`: List directory contents.
* `cd`: Change current working directory.
* `find`: Find specific files according to the given options in the working directory.
* `-exec`: Native option of the `find` command which allows you to execute a second command on all files found.
* `file`: Determines the file type of a given input.
* `|`: Pipe operator, used to connect commands, redirecting the stdout of the first command to the stdin of the next command.
* `grep`: Filters the specified content by keyword. 
* `cat`: Concatenate and display file contents.

### 💻 Solution

1. List the files in the working directory to find the `inhere` directory:
```bash
ls
```

2. Change the working directory to the `inhere` directory:
```bash
cd inhere
```

3. Find the only human-readable file in the working directory:
```bash
find . -type f -exec file {} + | grep text
```
*(Note: This command combines different utilities to provide a practical answer. It says "Use find to look for all files in the working directory, pass them to the `file` command to determine their type, take the results of all that and use `grep` to filter the output for the word `text`").*

4. Read the content of the target file:
```bash
cat ./-file07
```

5. Password Secured: `[REDACTED]`

---

## Level 5 -> Level 6

### 🎯 Objective
Read the password stored in the only human-readable file, which has 1033 bytes in size and is not executable in the `inhere` directory.

### 🧠 Concepts & Commands
* **Human-readable file:** A text file which can be read by humans.
* **1033 bytes in size:** The size in bytes of the file.
* **Not executable:** A file which is not executable. 
* `ls`: List directory contents.
* `cd`: Change current working directory.
* `find`: Find specific files according to the given options in the working directory.
* `-size`: Native option of the `find` command which allows you to specify the size of the target file.
* `!`: Native option of the `find` command which allows you to negate a filter. 
* `-exec`: Native option of the `find` command which allows you to execute a second command on all files found.
* `file`: Determines the file type of a given input.
* `|`: Pipe operator, used to connect commands, redirecting the stdout of the first command to the stdin of the next command.
* `grep`: Filters the specified content by keyword. 
* `cat`: Concatenate and display file contents.

### 💻 Solution

1. List the files in the working directory to find the `inhere` directory:
```bash
ls
```

2. Change the working directory to the `inhere` directory:
```bash
cd inhere
```

3. Find the only human-readable file with 1033 bytes in size and not executable in the working directory:
```bash
find . -type f -size 1033c ! -executable -exec file {} + | grep text
```
*(Note: This command combines different utilities to provide a practical answer. It says "Use find to look for all files in the working directory with 1033 bytes in size and not executable, pass them to the `file` command to determine their type, take the results of all that and use `grep` to filter the output for the word `text`").*

4. Read the content of the target file:
```bash
cat maybehere07/.file2
```

5. Password Secured: `[REDACTED]`

---

## Level 6 -> Level 7

### 🎯 Objective
Read the password stored in the file owned by user bandit7 and group bandit6, with 33 bytes in size, located somewhere on the server.

### 🧠 Concepts & Commands
* **Owner and group owner**: The user and group that own the file.
* **33 bytes in size:** The size in bytes of the file. 
* `find`: Find specific files according to the given options across a specified directory tree.
* `-user`: Native option of the `find` command which allows you to specify the user who owns the file.
* `-group`: Native option of the `find` command which allows you to specify the group who owns the file.
* `-size`: Native option of the `find` command which allows you to specify the size of the target file.
* `2>/dev/null`: A shell redirection mechanism that sends standard error (stderr) outputs (such as "permission denied") to the null device (`/dev/null`), effectively discarding them.  
* `cat`: Concatenate and display file contents.

### 💻 Solution

1. Find the file with 33 bytes in size, owned by user bandit7 and group bandit6 somewhere on the server:
```bash
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
```
*(Note: This command uses specific filters to provide a practical answer. It says "Use find to look for all files across the entire file system (`/`), owned by user bandit7 and group bandit6 with 33 bytes in size, and redirect all error messages to `/dev/null` to discard them").*

2. Read the content of the target file:
```bash
cat /var/lib/dpkg/info/bandit7.password
```

3. Password Secured: `[REDACTED]`

---












