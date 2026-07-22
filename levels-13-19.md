# OverTheWire Bandit: Levels 13 to 19 Writeup

This document contains the documentation, technical methodologies, and command sequences utilized to solve the third block of the Bandit wargame, focusing on networking architecture, secure remote sessions via SSH, asymmetric cryptography, and network protocols.

---

## Level 13 -> Level 14

### 🎯 Objective
Extract the provided SSH private key using a temporary directory, and use it to log in to bandit14.

### 🧠 Concepts & Commands
* **SSH Private Key**: A cryptographically secure identity file.
* `ls`: Lists directory contents.
* `cat`: Concatenates and displays file contents.
* `mktemp -d`: Creates a temporary directory in `/tmp`, which gives you the necessary permissions to modify files.
* `vim`: Command-line text editor.
* `scp`: Copies files between hosts safely using the SSH protocol, which can be used with the `-P` flag to specify a connection port.
* `ssh`: Secure Shell client, which creates an encrypted session for logging into remote machines. It can identify specific files with the `-i` flag to be used as the private key for authentication.

### 💻 Solution

1. List the files in the current working directory to verify the presence of the private key:
```bash
ls
```

2. Read the file content:
```bash
cat sshkey.private
```
*(Note: The cat command will display the SSH private key block, which is used instead of a password to authenticate).*

3. Create a temporary directory to store your copy of the key:
```bash
mktemp -d
```

4. Copy the SSH key content into a new file inside the temporary directory using the text editor `vim`:
```bash
vim temporary_folder_path/chosen_filename
```
*(Note: The exact path generated will differ on your machine, but it should look like: `/tmp/tmp.KJgTQc0Ltl/ssh.private`).*

5. Exit the remote session:
```bash
exit
```

6. Download the file to your local machine:
```bash
scp -P 2220 bandit13@bandit.labs.overthewire.org:/tmp/tmp.KJgTQc0Ltl/ssh.private .
```

7. Use the downloaded identity file to authenticate and log in to bandit14:
```bash
ssh -i ssh.private bandit14@bandit.labs.overthewire.org -p 2220
```

8. Once logged into bandit14, read the password file located in the system directory to retrieve the standard password:
```bash
cat /etc/bandit_pass/bandit14
```

9. Password Secured: `[REDACTED]`

---

## Level 14 -> Level 15

### 🎯 Objective
Submit the current level password to port 30000 on localhost.

### 🧠 Concepts & Commands
* `cat`: Concatenates and displays file contents.
* `|`: Pipe operator, used to connect commands, redirecting the stdout of the first command to the stdin of the next command.
* `ncat`: A command-line networking utility used to read from and write to network connections using TCP or UDP sockets.

### 💻 Solution

1. Read the current password and pipe the output stream into port 30000 on localhost:
```bash
cat /etc/bandit_pass/bandit14 | ncat localhost 30000
```

2. Password Secured: `[REDACTED]`

---

## Level 15 -> Level 16

### 🎯 Objective
Submit the current level password to port 30001 on localhost using SSL/TLS encryption.

### 🧠 Concepts & Commands
* `cat`: Concatenates and displays file contents.
* `|`: Pipe operator, used to connect commands, redirecting the stdout of the first command to the stdin of the next command.
* `openssl s_client`: Specific tool to make a connection to servers which require SSL/TLS encryption. Can be used with `-ign_eof` to prevent the TLS socket from closing immediately.

### 💻 Solution

1. Read the current password and pipe the output stream into port 30001 on localhost using SSL/TLS encryption without letting it close the connection:
```bash
cat /etc/bandit_pass/bandit15 | openssl s_client -connect localhost:30001 -ign_eof
```

2. Password Secured: `[REDACTED]`

---

## Level 16 -> Level 17

### 🎯 Objective
Submit the current level password to a port in the range 31000 to 32000. You need to discover which ports in this range are listening, and which of those speak SSL/TLS encryption.

### 🧠 Concepts & Commands
* `nmap`: Network mapper utility, used to discover open ports, identify which services they are running (as well as their versions), and detect the operating system.
* `cat`: Concatenates and displays file contents.
* `|`: Pipe operator, used to connect commands, redirecting the stdout of the first command to the stdin of the next command.
* `openssl s_client`: Specific tool to make a connection to servers which require SSL/TLS encryption. Can be used with `-ign_eof` to prevent the TLS socket from closing immediately.
* `mktemp -d`: Creates a temporary directory in `/tmp`, which gives you the necessary permissions to modify files.
* `vim`: Command-line text editor.
* `scp`: Copies files between hosts safely using the SSH protocol, which can be used with the `-P` flag to specify a connection port.
* `ssh`: Secure Shell client, which creates an encrypted session for logging into remote machines. It can identify specific files with the `-i` flag to be used as the private key for authentication.


### 💻 Solution

1. Scan the current network in the specified ranges to discover which of them are listening and use SSL/TLS encryption:
```bash
nmap -p 31000-32000 -sV localhost
```
*(Note: You will get a list of ports in this range. You need to identify the one port which is listening and uses ssl/tls encryption).*

2. Read the current password and pipe the output stream into port 31790 on localhost using SSL/TLS encryption without letting it close the connection:
```bash
cat /etc/bandit_pass/bandit16 | openssl s_client -connect localhost:31790 -ign_eof
```
*(Note: On this level you get an SSH private key instead of a standard password).*

3. Create a temporary directory to store your copy of the key:
```bash
mktemp -d
```

4. Copy the SSH key content into a new file inside the temporary directory using the text editor `vim`:
```bash
vim /tmp/tmp.gcUQcUesul/sshkey.private
```

5. Exit the remote session:
```bash
exit
```

6. Download the file to your local machine:
```bash
scp -P 2220 bandit16@bandit.labs.overthewire.org:/tmp/tmp.gcUQcUesul/sshkey.private .
```

7. Use the downloaded identity file to authenticate and log in to bandit17:
```bash
ssh -i sshkey.private bandit17@bandit.labs.overthewire.org -p 2220
```

8. Once logged into bandit17, read the password file located in the system directory to retrieve the standard password:
```bash
cat /etc/bandit_pass/bandit17
```

9. Password Secured: `[REDACTED]`

---

## Level 17 -> Level 18

### 🎯 Objective
Retrieve the password by identifying the single differing line between the `passwords.old` and `passwords.new` files.

### 🧠 Concepts & Commands
* `ls`: Lists directory contents.
* `diff`: Compares files line by line and outputs the differences.

### 💻 Solution

1. List the files in the current working directory to verify the presence of both target files:
```bash
ls
```

2. Compare both files to identify the single line that differs between them:
```bash
diff passwords.old passwords.new
```

3. Password Secured: `[REDACTED]`

---

## Level 18 -> Level 19

### 🎯 Objective
Retrieve the password stored in the `readme` file located in the home directory. However, once you log in you are instantly disconnected.

### 🧠 Concepts & Commands
* `ssh`: Secure Shell client, which creates an encrypted session for logging into remote machines. It can accept an appended command to execute it directly on the remote host without opening an interactive shell.
* `cat`: Concatenates and displays file contents.

### 💻 Solution

1. Log into bandit18 with SSH and use the `cat` command to read the `readme` file without triggering the interactive shell's forced logout:
```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme
```

2. Password Secured: `[REDACTED]`

---








