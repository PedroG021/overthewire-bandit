# OverTheWire Bandit: Levels 19 to 27 Writeup

This document contains the documentation, methodology, and commands used to solve the fourth block of the Bandit wargame, focusing on local privilege escalation, setuid binary exploitation, scripting automation, and escaping restricted shells.

---

## Level 19 -> Level 20

### 🎯 Objective
Use the setuid binary in the home directory to retrieve bandit20 password.

### 🧠 Concepts & Commands
* **Setuid**: A permission flag that allows a user to execute an executable file with the permission of the file owner.
* `ls`: Lists directory contents.
* `cat`: Concatenates and displays file contents.

### 💻 Solution

1. List the files in the current working directory to verify the presence of the setuid program:
```bash
ls
```

2. Execute the program without arguments to see how it works:
```bash
./bandit20-do
```

3. Once you see that the binary runs commands as the file owner, which is bandit20, simply read the password:
```bash
./bandit20-do cat /etc/bandit_pass/bandit20
```
*(Note: `./bandit20-do` binary executes the command with bandit20 permissions, which gives you the necessary permissions to read the bandit20 password file).*

4. Password Secured: `[REDACTED]`

---

## Level 20 -> Level 21

### 🎯 Objective
Use the setuid binary in the home directory, which makes a connection to localhost on the port you specify as a commandline argument, reads a line of text from the connection and compares it to the previous level password, retrieving you the password for bandit21 if the received password matches.

### 🧠 Concepts & Commands
* **Setuid**: A permission flag that allows a user to execute an executable file with the permission of the file owner.
* `ls`: Lists directory contents.
* `cat`: Concatenates and displays file contents.
* `ncat`: A command-line networking utility used to read from and write to network connections using TCP or UDP sockets, which can be used with `-l` flag to create listening ports.
* `&`: Background execution operator.

### 💻 Solution

1. List the files in the current working directory to verify the presence of the setuid program:
```bash
ls
```

2. Start a background listener to send the bandit20 password:
```bash
cat /etc/bandit_pass/bandit20 | ncat -l 1557 &
```

3. Connect the setuid program to the listening port:
```bash
./suconnect 1557
```

4. Password Secured: `[REDACTED]`

---

## Level 21 -> Level 22

### 🎯 Objective
Read the cronjob configuration in /etc/cron.d to see what script it executes and retireve the bandit22 password.

### 🧠 Concepts & Commands
* **Cronjob**: Automated background task executed at specific times or recurring intervals.
* **Script**: A text file containing commands executed in sequence when run.
* `cd`: Change the current working directory.
* `ls`: Lists directory contents.
* `cat`: Concatenates and displays file contents.

### 💻 Solution

1. Change to the `/etc/cron.d` directory:
```bash
cd /etc/cron.d
```

2. List the files in the current working directory to verify the presence of the target cronjob:
```bash
ls
```

3. Read the bandit22 cronjob to see when and from where it is being executed:
```bash
cat cronjob_bandit22
```

4. Read the file which contains the script of what is being executed:
```bash
cat /usr/bin/cronjob_bandit22.sh
```

5. Once you inspect the script, you will see that it redirects the bandit22 password into a temporary file which anyone can read:
```bash
cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

6. Password Secured: `[REDACTED]`

---

## Level 22 -> Level 23

### 🎯 Objective
Read the cronjob configuration in /etc/cron.d to see what script it executes and retrieve the bandit23 password.

### 🧠 Concepts & Commands
* **Cronjob**: Automated background task executed at specific times or recurring intervals.
* **Script**: A text file containing commands executed in sequence when run.
* `cd`: Change the current working directory.
* `ls`: Lists directory contents.
* `cat`: Concatenates and displays file contents.

### 💻 Solution

1. Change to the `/etc/cron.d` directory:
```bash
cd /etc/cron.d
```

2. List the files in the current working directory to verify the presence of the target cronjob:
```bash
ls
```

3. Read the bandit23 cronjob to see when and from where it is being executed:
```bash
cat cronjob_bandit23
```

4. Read the file which contains the script of what is being executed:
```bash
cat /usr/bin/cronjob_bandit23.sh
```

5. Once you inspect the script, you will see that it redirects the current user level password into a temporary file which anyone can read:
```bash
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
```
*(Note: This script is owned by bandit23, but he uses the argument `myname=$(whoami)` which means it will have a different name depending on who is executing it).*

6. Running the original script creates a temporary file for the current user (bandit22), so we modify the script to set the target user to bandit23:
```bash
#!/bin/bash

myname=bandit23
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
```
*(Note: The only change was in the first line).*

7. Running the modified script reveals where the temporary file with the bandit23 password is, allowing you to read it:
```bash
cat /tmp/8ca319486bfbbc3663ea0fbe81326349
```

8. Password Secured: `[REDACTED]`

---

## Level 23 -> Level 24

### 🎯 Objective
Read the cronjob configuration in /etc/cron.d to see what script it executes and retrieve the bandit24 password.

### 🧠 Concepts & Commands
* **Cronjob**: Automated background task executed at specific times or recurring intervals.
* **Script**: A text file containing commands executed in sequence when run.
* `cd`: Change the current working directory.
* `ls`: Lists directory contents.
* `cat`: Concatenates and displays file contents.
* `mktemp -d`: Creates a temporary directory in `/tmp`, which gives you the necessary permissions to modify files.
* `chmod`: Changes the permissions to specific users in files and directories, which can be used with numbers or letters to specify what permissions will be given.
* `vim`: Command-line text editor.
* `cp`: Copies a file/directory to a specified destination.

### 💻 Solution

1. Change to the `/etc/cron.d` directory:
```bash
cd /etc/cron.d
```

2. List the files in the current working directory to verify the presence of the target cronjob:
```bash
ls
```

3. Read the bandit24 cronjob to see when and from where it is being executed:
```bash
cat cronjob_bandit24
```

4. Read the file which contains the script of what is being executed:
```bash
cat /usr/bin/cronjob_bandit24.sh
```

5. Once you inspect the script, you will see that this script is executing and deleting all files in `/var/spool/bandit24/foo` as bandit24. Then you need to place a script there for bandit24 to execute. We start by creating a temporary directory:
```bash
mktemp -d
```

6. Now you give this directory the right permissions to all users, considering bandit24 will execute your script in this directory, since by default any directory created has full permissions only for the owner:
```bash
chmod 777 /tmp/tmp.5BCYOLp0w6 
```

7. Once you have a "public directory", it's time to create the script that will be used as bandit24 with a text editor:
```bash
vim /tmp/tmp.5BCYOLp0w6/script.bash
```
*(Note: Adding a filename to the directory path creates a new file inside it with the chosen name).*

8. The script will run with bandit24 permissions, and the output needs to be read by you as bandit23:
```bash
#!/bin/bash

cat /etc/bandit_pass/bandit24 > /tmp/tmp.5BCYOLp0w6/senha.bandit24

chmod 777 /tmp/tmp.5BCYOLp0w6/senha.bandit24
```
*(Note: Cat successfully reads the bandit24 password since the script runs as bandit24. Since the file is created with bandit24 as the owner, using chmod on the new file gives the correct permissions to ensure bandit23 can read it).*

9. Once you have the script, it's time to grant execution permissions to the script:
```bash
chmod +x /tmp/tmp.5BCYOLp0w6/script.bash
```

10. Copy the script into the specific directory where bandit24 is executing everything inside every minute:
```bash
cp /tmp/tmp.5BCYOLp0w6/script.bash /var/spool/bandit24/foo
```

11. After one minute, the script must be executed by bandit24, creating the `senha.bandit24` file in the /tmp/tmp.5BCYOLp0w6 directory, allowing you to read the content:
```bash
cat /tmp/tmp.5BCYOLp0w6/senha.bandit24
```

12. Password Secured: `[REDACTED]`

---

## Level 24 -> Level 25

### 🎯 Objective
Retrieve the bandit25 password by sending the bandit24 password and a secret numeric 4-digit PIN into a daemon listening on port 30002.

### 🧠 Concepts & Commands
* **Brute-forcing**: A trial-and-error method that systematically checks all possible combinations until the correct one is found.
* `mktemp -d`: Creates a temporary directory in `/tmp`, which gives you the necessary permissions to modify files.
* `vim`: Command-line text editor.
* `bash`: Executes a bash script.
* `|`: Pipe operator, used to connect commands, redirecting the stdout of the first command to the stdin of the next command.
* `ncat`: A command-line networking utility used to read from and write to network connections using TCP or UDP sockets, which can be used with `-l` flag to create listening ports.

### 💻 Solution

1. Create a temporary directory so you can work:
```bash
mktemp -d
```

2. Create the script to use the brute-forcing method using a text editor:
```bash
vim /tmp/tmp.iIk7Z69ptL/script.bash
```

3. The script must combine the bandit24 password with all 10000 possible PIN combinations:
```bash
for morango in $(seq -w 0000 9999); do echo "bandit24_password_Redacted $morango"; done
```
*(Note: The brute-forcing method used here is numerical with `seq -w 0000 9999` which means trying all number combinations in this range).*

4. Once you have the script, execute it and pipe the output to the daemon listening on port 30002:
```bash
bash /tmp/tmp.iIk7Z69ptL/script.bash | ncat localhost 30002
```

5. Password Secured: `[REDACTED]`

---







