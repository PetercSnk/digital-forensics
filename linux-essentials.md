# Linux Essentials

## Basics

| Command | Description |
|---------|-------------|
|echo|Displays text to the command line|
|whoami|Displays the username of who you're logged in as|
|su|Logs in as root|
|man|Displays the manual page for a command|

### Examples

Display the manual page for the ls command:

`man ls`

## File System

| Command | Description |
|---------|-------------|
|ls|Lists files in current directory|
|cd|Changes the current directory|
|cat|Outputs the contents of a file|
|pwd|Prints the working directory|

## Searching

| Command | Description |
|---------|-------------|
|find|Finds files|
|grep|Searches the contents of files|

### Examples

Find the text document passwords.txt:

`find -name passwords.txt`

Find all text documents in current directory:

`find -name *.txt`

Find audit.log in the root directory:

`find / -name audit.log`

Search for the string "root" in audit.log

`grep "root" /var/log/audit/audit.log`

## Shell Operators

| Command | Description |
|---------|-------------|
|&|Runs commands in the background|
|&&|Used to combine multiple commands in one line|
|>|Redirects output from a command (replace)|
|>>|Redirects output from a command (append)|
|\||Used to pipe one command into another|

## File Operating

| Command | Description |
|---------|-------------|
|touch|Creates a file|
|mkdir|Creates a directory|
|cp|Copies a file or directory|
|mv|Moves or renames a file or directory|
|file|Determines the file type|
|rm|Removes a file or directory|

### Examples

Create a file named passwords.txt:

`touch passwords.txt`

Create a directory named secrets:

`mkdir secrets`

Copy passwords.txt to secrets:

`cp passwords.txt secrets`

Move passwords.txt to secrets and rename to secrets.txt:

`mv passwords.txt secrets/secrets.txt`

Determine the file type of secrets.txt:

`file secrets/secrets.txt`

Remove passwords.txt:

`rm passwords.txt`

Remove the directory secrets:

`rm -rf secrets`

## Hashing

| Command | Description |
|---------|-------------|
|md5sum|Calculates the md5 hash|

### Examples

Calculate the md5 hash of audit.log:

`md5sum /var/log/audit/audit.log`

## Disk Analysis

| Command | Description |
|---------|-------------|
|fdisk|Creates, manipulates, and displays partition tables|
|dd|Converts and copies files|

### Examples

Display partition tables:

`fdisk -l`

Create a bit-by-bit image of /dev/sdb1 and output it to the file fat32.dd:

`dd if=/dev/sdb1 of=fat32.dd`

Create a bit-by-bit image of /dev/sdb1 and output it to the file fat32.dd. This time copy only 1 block with a 
block with a size of 512 and skip the first block:

`dd if=/dev/sdb1 bs=512 count=1 skip=1 of=fat32.dd`
