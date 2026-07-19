\# OverTheWire Bandit: Levels 0 to 7 Writeup



This document contains the documentation, methodology, and commands used to solve the initial block of the Bandit wargame, focusing on basic Linux file system navigation, text manipulation, and properties.



\---



\## Level 0 -> Level 1



\### 🎯 Objective

Log into the game server using SSH and locate the initial flag.



\### 🧠 Concepts \& Commands

* &#x20;`ssh`: Secure Shell client for logging into remote machines.
* &#x20;`ls`: List directory contents.
* &#x20;`cat`: Concatenate and display file content.



\### 💻 Solution

1\. Connect to the host via SSH using the provided port and credentials:

&#x20;  ```bash

&#x20;  ssh bandit0@bandit.labs.overthewire.org -p 2220
   ```



2\. List the files in the home directory to find the readme:

&#x20;  ```bash

&#x20;  ls
   ```



3\. Read the content of the file to retrieve the password for the next level:

&#x20;  ```bash

&#x20;  cat readme
   ```



4\. Password Secured: 6y2...\[REDACTED]



\---



\## Level 1 -> Level 2



\### 🎯 Objective

Read the password stored in a file called `-` located in te home directory.



\### 🧠 Concepts \& Commands

* \*\*Special Filenames:\*\* Relative paths './-' to bypass command-line option processing.
* &#x20;`ls`: List directory contents.
* &#x20;`cat`: Concatenate and display file content.



\### 💻 Solution



1. List the files in the home directory to find the `-`:
```bash
ls
```

2. Read the content of the file wish has special name:
```bash
cat ./"-"
```

note:(the dash - normally represents stdin, so providing the relative path ./ forces the terminal to treat it as a file path)

3. Password Secured: PK8...\[REDACTED]


---





