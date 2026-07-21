# OverTheWire Bandit: Levels 7 to 13 Writeup



This document contains the documentation, technical methodologies, and command sequences utilized to solve the second block of the Bandit wargame, focusing on stream redirection, advanced data processing pipelines, text encoding representations, and data compression utilities.


---

## Level 7 -> Level 8

### 🎯 Objective
Read the password stored in the file `data.txt` next to the word `millionth`.

### 🧠 Concepts & Commands
* `ls`: List directory contents.
* `grep`: Filters the specified content by keyword.

### 💻 Solution

1. List the files in the current working directory to verify the presence of the target file:
```bash
ls
```

2. Filter the contents of `data.txt` to isolate the line containing the specific string anchor `millionth`:
```bash
grep "millionth" data.txt
```

*(Note: The grep utility reads the target file line by line, evaluating the stream against the literal keyword argument and outputting only the precise matching line to stdout.)*

3. Password Secured: `[REDACTED]`

---

## Level 8 -> Level 9

### 🎯 Objective
Read the password stored in the file `data.txt`, which is the only line of text that occurs exactly once.

### 🧠 Concepts & Commands
* **Unique Lines**: Lines that appear only once in a file.
* `ls`: List directory contents.
* `sort`: Sorts the lines of text in a file.
* `|`: Pipe operator, used to connect commands, redirecting the stdout of the first command to the stdin of the next command.
* `uniq -u`: Compares lines in a text stream. Combined with the `-u` flag, it shows only the lines that are completely unique.

### 💻 Solution

1. List the files in the current working directory to verify the presence of the target file:
```bash
ls
```

2. Sort the file contents and pipe the output into `uniq -u` to find the one line that occurs exactly once:
```bash
sort data.txt | uniq -u
```

3. Password Secured: `[REDACTED]`

---

## Level 9 -> Level 10

### 🎯 Objective
Read the password stored in the file `data.txt`, which is one of the few human-readable strings, preceded by several `=` characters.

### 🧠 Concepts & Commands
* **Human-readable file:** A text file which can be read by humans.
* `ls`: List directory contents.
* `strings`: Searches through a non-human-readable file and extracts only the readable characters.
* `|`: Pipe operator, used to connect commands, redirecting the stdout of the first command to the stdin of the next command.
* `grep`: Filters the specified content by keyword.
* `^`: Regex anchor used to match the beginning of a line.

### 💻 Solution

1. List the files in the current working directory to verify the presence of the target file:
```bash
ls
```

2. Search through the file contents to extract the readable lines and pipe the output into `grep "^="` to find which lines start with the `=` character:
```bash
strings data.txt | grep "^="
```

3. Password Secured: `[REDACTED]`

---

## Level 10 -> Level 11

### 🎯 Objective
Read the password stored in the file `data.txt`, which contains base64 encoded data.

### 🧠 Concepts & Commands
* **Encoded data:** Data encoding turns a file into a non-human-readable file.
* `ls`: List directory contents.
* `base64 -d`: Decodes base64 encoded data when combined with the `-d` flag.

### 💻 Solution

1. List the files in the current working directory to verify the presence of the target file:
```bash
ls
```

2. Decode the base64 encoded file:
```bash
base64 -d data.txt
```

3. Password Secured: `[REDACTED]`

---

## Level 11 -> Level 12

### 🎯 Objective
Read the password stored in the file `data.txt`, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions.

### 🧠 Concepts & Commands
* **Rotated positions**: Shifts the alphabet letters by a fixed number of places. 
* `ls`: List directory contents.
* `cat`: Concatenate and display file contents.
* `tr`: Translates, replaces, or deletes specific characters from the stdin stream.

### 💻 Solution

1. List the files in the current working directory to verify the presence of the target file:
```bash
ls
```

2. Read the file contents and pipe the output to rotate all lowercase (a-z) and uppercase (A-Z) letters by 13 positions:
```bash
cat data.txt | tr "a-zA-Z" "n-za-mN-ZA-M"
```
*(Note: The `tr` command shifts the alphabet 13 spaces forward, starting with the letter N. Since the original `data.txt` file was already shifted by 13 spaces, doing this again reverts the process and decodes the text).*

3. Password Secured: `[REDACTED]`

---

## Level 12 -> Level 13

### 🎯 Objective
Read the password stored in the file `data.txt`, which is a hexdump of a file that has been repeatedly compressed.

*(Note: This level requires you to create a temporary directory and copy `data.txt` to it, so you get the correct permissions to revert and decompress the file).*

### 🧠 Concepts & Commands
* **Hexdump**: Hexadecimal visualization of a file.
* **Repeatedly compressed**: The target file was compressed many times, possibly by different compressors.
* **Permissions**: Some files or directories have specific permissions assigned to specific users, which can prevent you from reading or modifying them. 
* `ls`: List directory contents.
* `mktemp -d`: Creates a temporary directory in `/tmp`, which gives you the necessary permissions to modify the file of this level.
* `cp`: Copies a file/directory to a specified destination.
* `cd`: Changes the current working directory.
* `mv`: Moves or renames a file/directory.
* `file`: Determines the file type of a given input.
* `&&`: Operator that only executes the next command if the previous command was 100% finished with success.
* `xxd`: Creates a hexadecimal visualization of a file, or reverts it with the flag `-r`.
* `>`: Used to redirect a command output into a specified file.
* `gzip`: Compresses a file, or reverts a compression with the flag `-d`.
* `bzip2`: Just like gzip, compresses a file, or reverts a compression with the flag `-d`.
* `tar`: Merges multiple files into one, or extracts merged files with the flag `-xf`.
* `cat`: Concatenates and displays file contents.

### 💻 Solution

1. List the files in the current working directory to verify the presence of the target file:
```bash
ls
```

2. Create a temporary directory where you get the correct permissions to modify a file:
```bash
mktemp -d
```

3. Copy the target file to the temporary directory:
```bash
cp data.txt /tmp/tmp.muEOJKWzfi
```
*(Note: The path destination `/tmp/tmp.muEOJKWzfi` in your terminal will be different, replace it.)*

4. Change the current working directory to the temporary folder:
```bash
cd /tmp/tmp.muEOJKWzfi
```

5. Since the file is a hexdump visualization compressed repeatedly, start creating a new file with the hexdump visualization reverted:
```bash
xxd -r data.txt > reverted.bin
```
*(Note: Since `xxd` is a visualization, we need to create a new file with the visualization reverted. The redirector `>` will do this job).*

6. Discover what kind of file the new `reverted.bin` is so you can start decompressing it:
```bash
file reverted.bin
```

7. Once you discover it is a gzip file, you need to decompress it. To decompress a file, the filename needs to end with the compressor extension, in this case `.gz`:
```bash
mv reverted.bin reverted.gz
```

8. Decompress the `.gz` file and look for what kind of file it will be:
```bash
gzip -d reverted.gz && file reverted
```

9. Repeat the renaming to the current compressor:
```bash
mv reverted reverted.bz2
```

10. Decompress the `.bz2` file and look for what kind of file it will be:
```bash
bzip2 -d reverted.bz2 && file reverted
```

11. Extract the `.tar` file and list the files in the current directory to see the extracted file:
```bash
tar -xf reverted && ls
```

12. Discover what kind of file the new one is:
```bash
file data5.bin
```

13. Repeat the past processes until you reach `data8`, which is an ASCII text file, then read it:
```bash
cat data8
```

14. Password Secured: `[REDACTED]`

---











