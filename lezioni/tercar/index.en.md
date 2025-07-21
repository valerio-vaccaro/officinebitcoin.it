# The character terminal

## Introduction
Linux (or better a GNU Linux system since linux is only the kernel that initializes the hardware and provides the primitives to use it) uses the concept of file for a vastity of activities. Files are sequences of data on a hard disk, configurations but not only, specific filesystems exist that create informational files with which to control the functioning of our computer and also many devices can be used as files, as character devices that process in various ways sequences of bytes.

The system loading process culminates with a graphical interface or in our case with a shell prompt, i.e., the character interface that we will use in our lessons.

Knowing the interface allows you to perform many operations on most Linux devices; in our course we will consider `bash` (bourne again shell), the most widespread shell for Linux; after login we will find ourselves in the home directory of our computer, i.e., in `\home\pippo` assuming that our username is pippo or in `\root` in case we entered with the superuser account (root indeed).

NEVER USE the root account as is customary in other operating systems.

To move between directories you can use the `cd` command (change directory) remembering that it accepts both absolute paths starting with `/` and relative paths from the current directory (indicated with `.` or without any indication) or from other directories such as home (`~`); if you want to have a list of all files present in the folder you can use the `ls` command (list) maybe with the ll argument, i.e., `ls -ll`

## Some useful commands

Some useful commands:

- `echo` prints to screen the content of a string passed as an argument,
- `man` calls up the manual of a certain command,
- `mc` console file manager,
- `nano` minimal text editor,
- `rm` removes a file,
- `mkdir` creates a directory,
- `rmdir` removes a directory (which must be empty),
- `touch` creates an empty file or changes the date of an existing file,
- `cat` prints to screen the content of a text file,
- `ncdu` allows you to navigate the filesystem ordered by the size of files and directories,
- `wget` allows you to download a file from the web,
- `dd` allows you to transfer information between files, devices, ...
- `tail` prints to screen the last lines of a file (useful for logs with the `-f` option (follow))
- `chmod` changes the properties of a file (for example the `+x` argument allows the execution of a file)

Executables present in the current folder can be executed by prefixing `./`, i.e., indicating that the path refers to the current directory.

## Input/output redirection
Input and output redirection can be done with the symbols `<` and `>`.

To write to a file we can execute

```
echo "pippo" > pippo.txt
```

This will create a file named pippo.txt with content pippo, if then we type

```
echo "pluto" > pippo.txt
```

The file content will be replaced with pluto. If we wanted to keep the previous content and append the new content at the end, we must use `>>` instead of `>`.

The `<` symbol works similarly for inputs.

## Pipe
The pipe `|` allows you to concatenate the output of one program with the input of another.

```
cowsay "good evening" | lolcat
```

The output of cowsay is fed to the lolcat command.

## Variables
Variables are names given to memory spaces that can contain strings, numbers, and more.

To set a variable, use the `=` command; to use it, simply prefix the `$` character. By convention, variables are written in uppercase.

```
VARIABLE="pippo"
echo $VARIABLE > pippo.txt
VARIABLE="pluto"
echo $VARIABLE >> pippo.txt
```

Creates a file with content

```
pippo
pluto
```

You can also launch a program and save the output in a variable

```
VARIABLE=$(ls)
```

The output of the ls command is saved in the variable named VARIABLE.

## Scripts
Scripts are lists of commands executed in sequence.

The first command is the interpreter used to launch the command, normally `#!/bin/sh`, i.e., the executable `/bin/sh` with the `#!` prefix.

Before executing them, they require execution permissions with the command `chmod +x filename`

## Repetitions
This lesson is repetitive and will be repeated every week. Below is a list of repetitions already held.

| Date        | Notes                                          |
|-------------|------------------------------------------------|
| 240122-2230 | First lesson                                   |
| 240129-2230 | Bash script                                    |
| 240205-2230 | Bash script                                    | 