# OverTheWire Bandit: Levels 27 to 33 Writeup

This document contains the documentation, methodology, and commands used to solve the final block of the Bandit wargame, focusing on version control diagnostics, Git repository reverse engineering, and bypassing strict input-filtering environments.

---

## Level 27 -> Level 28

### 🎯 Objective
Clone a remote Git repository to your local machine using SSH and locate the bandit28 password inside the repository files.

### 🧠 Concepts & Commands
* **Git**: A distributed version control system used to track changes in source code.
* `mktemp -d`: Creates a temporary directory in `/tmp`, which gives you the necessary permissions to modify files.
* `cd`: Change the current working directory.
* `git clone`: Downloads a copy of a remote Git repository to your local machine.
* `ls`: Lists directory contents.
* `cat`: Concatenates and displays file contents.

### 💻 Solution

1. Ensure Git is installed on your local machine:
   * **Windows:** Download and install Git for Windows (which includes Git Bash).
   * **Linux/macOS:** Install via your package manager (`sudo apt install git`).

2. Open your local terminal (or Git Bash on Windows) and create a directory to work in:
```bash
mktemp -d
```

3. Change to the created temporary directory and clone the remote repository:
```bash
cd /tmp/tmp.FBFIb8Ojui
git clone ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo
```
*(Note: When prompted for the password, enter the bandit27 password).*

4. Change to the cloned `repo` directory:
```bash
cd repo
```

5. List the files in the new directory:
```bash
ls
```

6. Read the `README` file:
```bash
cat README
```

7. Password Secured: `[REDACTED]`

---

## Level 28 -> Level 29

### 🎯 Objective
Clone a remote Git repository to your local machine using SSH and locate the bandit29 password inside the repository files.

### 🧠 Concepts & Commands
* **Git**: A distributed version control system used to track changes in source code.
* `mktemp -d`: Creates a temporary directory in `/tmp`, which gives you the necessary permissions to modify files.
* `cd`: Change the current working directory.
* `git clone`: Downloads a copy of a remote Git repository to your local machine.
* `ls`: Lists directory contents.
* `cat`: Concatenates and displays file contents.
* `git show`: Displays what was added or deleted inside a commit.

### 💻 Solution

1. Ensure Git is installed on your local machine:
   * **Windows:** Download and install Git for Windows (which includes Git Bash).
   * **Linux/macOS:** Install via your package manager (`sudo apt install git`).

2. Open your local terminal (or Git Bash on Windows) and create a directory to work in:
```bash
mktemp -d
```

3. Change to the created temporary directory and clone the remote repository:
```bash
cd /tmp/tmp.oXVIp4jGgf
git clone ssh://bandit28-git@bandit.labs.overthewire.org:2220/home/bandit28-git/repo
```
*(Note: When prompted for the password, enter the bandit28 password).*

4. Change to the cloned `repo` directory:
```bash
cd repo
```

5. List the files in the new directory:
```bash
ls
```

6. Read the `README.md` file:
```bash
cat README.md
```

7. Since the current file shows a redacted password for bandit29, check the commit changes to reveal the previous contents:
```bash
git show
```

8. Password Secured: `[REDACTED]`

---

## Level 29 -> Level 30

### 🎯 Objective
Clone a remote Git repository to your local machine using SSH and locate the bandit30 password inside the repository files.

### 🧠 Concepts & Commands
* **Git**: A distributed version control system used to track changes in source code.
* `mktemp -d`: Creates a temporary directory in `/tmp`, which gives you the necessary permissions to modify files.
* `cd`: Change the current working directory.
* `git clone`: Downloads a copy of a remote Git repository to your local machine.
* `ls`: Lists directory contents.
* `cat`: Concatenates and displays file contents.
* `git show`: Displays what was added or deleted inside a commit.
* `git branch -a`: Lists all branches in the repository, which may contain different commits or files.
* `git checkout`: Switches the working tree to a specified branch or commit to inspect its contents.

### 💻 Solution

1. Ensure Git is installed on your local machine:
   * **Windows:** Download and install Git for Windows (which includes Git Bash).
   * **Linux/macOS:** Install via your package manager (`sudo apt install git`).

2. Open your local terminal (or Git Bash on Windows) and create a directory to work in:
```bash
mktemp -d
```

3. Change to the created temporary directory and clone the remote repository:
```bash
cd /tmp/tmp.hWQmI0PeQB
git clone ssh://bandit29-git@bandit.labs.overthewire.org:2220/home/bandit29-git/repo
```
*(Note: When prompted for the password, enter the bandit29 password).*

4. Change to the cloned `repo` directory:
```bash
cd repo
```

5. List the files in the new directory:
```bash
ls
```

6. Read the `README.md` file:
```bash
cat README.md
```

7. Since the current file does not contain the password for bandit30, check the commit changes to see the previous edits:
```bash
git show
```

8. Since `git show` reveals that the only change made was replacing the username, check for other available branches:
```bash
git branch -a
```

9. After listing the branches, switch to the `dev` branch to investigate it:
```bash
git checkout dev
``` 

10. Once on the `dev` branch, inspect the commit or read the updated file:
```bash
git show
```

11. Password Secured: `[REDACTED]`

---

## Level 30 -> Level 31

### 🎯 Objective
Clone a remote Git repository to your local machine using SSH and locate the bandit31 password inside the repository files.

### 🧠 Concepts & Commands
* **Git**: A distributed version control system used to track changes in source code.
* `mktemp -d`: Creates a temporary directory in `/tmp`, which gives you the necessary permissions to modify files.
* `cd`: Change the current working directory.
* `git clone`: Downloads a copy of a remote Git repository to your local machine.
* `ls`: Lists directory contents.
* `cat`: Concatenates and displays file contents.
* `git show`: Displays what was added or deleted inside a commit.
* `git tag`: Lists or manages tags created to mark commits in history, which may contain hidden data.

### 💻 Solution

1. Ensure Git is installed on your local machine:
   * **Windows:** Download and install Git for Windows (which includes Git Bash).
   * **Linux/macOS:** Install via your package manager (`sudo apt install git`).

2. Open your local terminal (or Git Bash on Windows) and create a directory to work in:
```bash
mktemp -d
```

3. Change to the created temporary directory and clone the remote repository:
```bash
cd /tmp/tmp.SxPghnZwXF
git clone ssh://bandit30-git@bandit.labs.overthewire.org:2220/home/bandit30-git/repo
```
*(Note: When prompted for the password, enter the bandit30 password).*

4. Change to the cloned `repo` directory:
```bash
cd repo
```

5. List the files in the new directory:
```bash
ls
```

6. Read the `README.md` file:
```bash
cat README.md
```

7. Since the current file says "just an empty file", check the commit changes to see the previous edits:
```bash
git show
```

8. Since `git show` reveals the same message, we can use the `tag` option to look for hidden information which may not appear in the file just by using `ls` or `git show`:
```bash
git tag
```

9. Since `git tag` displays a tag called `secret`, inspect its contents:
```bash
git show secret
``` 

10. Password Secured: `[REDACTED]`

---

## Level 31 -> Level 32

### 🎯 Objective
Clone a remote Git repository to your local machine using SSH and locate the bandit32 password inside the repository files.

### 🧠 Concepts & Commands
* **Git**: A distributed version control system used to track changes in source code.
* `mktemp -d`: Creates a temporary directory in `/tmp`, which gives you the necessary permissions to modify files.
* `cd`: Change the current working directory.
* `git clone`: Downloads a copy of a remote Git repository to your local machine.
* `ls`: Lists directory contents.
* `cat`: Concatenates and displays file contents.
* `echo`: Prints the text you write in the terminal.
* `>`: Used to redirect a command output into a specified file or create a new file with the output.
* `git add`: Prepares a file to be included in the next commit, which may be used with the `-f` flag to force the file to be added.
* `git commit -m`: Permanently records the staged changes in the repository history with an explanatory note.
* `git push origin`: Sends the committed changes from your local machine to the remote repository.

### 💻 Solution

1. Ensure Git is installed on your local machine:
   * **Windows:** Download and install Git for Windows (which includes Git Bash).
   * **Linux/macOS:** Install via your package manager (`sudo apt install git`).

2. Open your local terminal (or Git Bash on Windows) and create a directory to work in:
```bash
mktemp -d
```

3. Change to the created temporary directory and clone the remote repository:
```bash
cd /tmp/tmp.g0es6vnXh8
git clone ssh://bandit31-git@bandit.labs.overthewire.org:2220/home/bandit31-git/repo
```
*(Note: When prompted for the password, enter the bandit31 password).*

4. Change to the cloned `repo` directory:
```bash
cd repo
```

5. List the files in the new directory:
```bash
ls
```

6. Read the `README.md` file:
```bash
cat README.md
```

7. Since the current file says the task is to push a detailed file to the remote repository, begin creating the file with the given details:
```bash
echo "May I come in?" > key.txt
```
*(Note: The repository contains a .gitignore file that ignores text files by default).*

8. With the file created, stage it to be included in the next commit:
```bash
git add -f key.txt
```
*(Note: If you try to add the file without the `-f` flag, Git ignores it because of the .gitignore rules).*

9. Once the file is staged, commit it with an explanatory note:
```bash
git commit -m "Adding the necessary file"
``` 

10. Now send the committed changes from your local machine to the remote repository:
```bash
git push origin master
```
*(Note: `master` specifies the target branch in the remote repository).*

11. Password Secured: `[REDACTED]`

---

## Level 32 -> Level 33

### 🎯 Objective
Escape the custom uppercase restricted shell (uppershell) and retrieve the bandit33 password.

### 🧠 Concepts & Commands
* **Restricted Shell:** A shell environment that limits user capabilities or alters typed input before execution.
* `$0`: A special positional parameter that holds the name or binary path of the currently executing shell or script.
* `sh`: The standard POSIX shell command language interpreter.
* `cat`: Concatenates and displays file contents.

### 💻 Solution

1. Upon connecting, observe that any typed command is automatically converted to uppercase and fails to execute (`ls` turns into `LS`):
```bash
WELCOME TO THE UPPERCASE SHELL
>> ls
sh: 1: LS: Permission Denied
```

2. Execute the positional parameter $0 to spawn the parent shell process:
```bash
$0
```
*(Note: Since `$0` evaluates to the executing shell binary path, running it executes /bin/sh directly, bypassing the uppercase input filter).*

3. Once inside the standard sh shell, read the bandit33 password:
```bash
cat /etc/bandit_pass/bandit33
```

4. Password Secured: `[REDACTED]`

---








