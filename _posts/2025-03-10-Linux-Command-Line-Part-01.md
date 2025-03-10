# Learning the Shell
## 01 What is the Shell
Terminal Emulators

When using a graphical user interface (GUI), we need another program called a terminal emulator to interact with the shell. If we look through our desktop menus, we will probably find one. KDE uses konsole and GNOME uses gnome-terminal, though it's likely called simply “terminal” on our menu. A number of other terminal emulators are available for Linux, but they all basically do the same thing; give us access to the shell. You will probably develop a preference for one or another terminal emulator based on the number of bells and whistles it has.

## 02 Navigation
- pwd – Print name of current working directory
- cd – Change directory
- ls – List directory contents

## 03 Exploring the System
- ls – List directory contents
- file – Determine file type
- less – View file contents

Options and Arguments

This brings us to a very important point about how most commands work. Commands are often followed by one or more options that modify their behavior, and further, by one or more arguments, the items upon which the command acts. So most commands look kind of like this:

`command -options arguments`

## 04 Manipulating Files and Directories
- cp – Copy files and directories
- mv – Move/rename files and directories
- mkdir – Create directories
- rm – Remove files and directories
- ln – Create hard and symbolic links

### Wildcards
`cp -u *.html destination`

Before we begin using our commands, we need to talk about a shell feature that makes these commands so powerful. Since the shell uses filenames so much, it provides special characters to help us rapidly specify groups of filenames. These special characters are called wildcards. Using wildcards (which is also known as globbing) allows us to select filenames based on patterns of characters. Table 4-1 lists the wildcards and what they select.

`*` Matches any characters
`?` Matches any single character
`[characters]` Matches any character that is a member of the set characters
`[!characters]` or `[^characters]` Matches any character that is not a member of the set characters
`[[:class:]]` Matches any character that is a member of the specified class

#### Commonly Used Character Classes
`[:alnum:]` Matches any alphanumeric character
`[:alpha:]` Matches any alphabetic character
`[:digit:]` Matches any numeral
`[:lower:]` Matches any lowercase letter
`[:upper:]` Matches any uppercase letter

#### Wildcard Examples
`*` All files
`g*` Any file beginning with “g”
`b*.txt` Any file beginning with “b” followed by any characters and ending with “.txt”
`Data???` Any file beginning with “Data” followed by exactly three characters
`[abc]*` Any file beginning with either an “a”, a “b”, or a “c”
`BACKUP.[0-9][0-9][0-9]` Any file beginning with “BACKUP.” followed by exactly three numerals
`[[:upper:]]*` Any file beginning with an uppercase letter
`[![:digit:]]*` Any file not beginning with a numeral
`*[[:lower:]123]` Any file ending with a lowercase letter or the numerals “1”, “2”, or “3”

### mv – Move and Rename Files
The mv command performs both file moving and file renaming, depending on how it is used. In either case, the original filename no longer exists after the operation. mv is used in much the same way as cp, as shown here:

`mv item1 item2`

## 05 Working with Commands
- type – Indicate how a command name is interpreted
- which – Display which executable program will be executed
- help – Get help for shell builtins
- man – Display a command's manual page
- apropos – Display a list of appropriate commands
- info – Display a command's info entry
- whatis – Display one-line manual page descriptions
- alias – Create an alias for a command

### What Exactly Are Commands?
A command can be one of four different things:
1. An executable program like all those files we saw in /usr/bin. Within this category, programs can be compiled binaries such as programs written in C and C++, or programs written in scripting languages such as the shell, Perl, Python, Ruby, and so on.
2. A command built into the shell itself. bash supports a number of commands internally called shell builtins. The cd command, for example, is a shell builtin.
3. A shell function. Shell functions are miniature shell scripts incorporated into the environment. We will cover configuring the environment and writing shell functions in later chapters, but for now, just be aware that they exist.
4. An alias. Aliases are commands that we can define ourselves, built from other commands.

### Getting a Command's Documentation
`help` – Get Help for Shell Builtins
bash has a built-in help facility available for each of the shell builtins. To use it, type “help” followed by the name of the shell builtin.

`man` – Display a Program's Manual Page
Most executable programs intended for command line use provide a formal piece of documentation called a manual or man page. A special paging program called man is used to view them.

`whatis` – Display One-line Manual Page Descriptions
The whatis program displays the name and a one-line description of a man page matching a specified keyword:

`info` – Display a Program's Info Entry
The GNU Project provides an alternative to man pages for their programs, called “info.” Info manuals are displayed with a reader program named, appropriately enough, info. Info pages are hyperlinked much like web pages.

`README` and Other Program Documentation Files
Many software packages installed on our system have documentation files residing in the /usr/share/doc directory. Most of these are stored in plain text format and can be viewed with less. Some of the files are in HTML format and can be viewed with a web browser. We may encounter some files ending with a “.gz” extension. This indicates that they have been compressed with the gzip compression program. The gzip package includes a special version of less called zless that will display the contents of gzip-compressed text files.


## 06 Redirection
In this lesson we are going to unleash what may be the coolest feature of the command line. It's called I/O redirection. The “I/O” stands for input/output and with this facility we can redirect the input and output of commands to and from files, as well as connect multiple commands together into powerful command pipelines. To show off this facility, we will introduce the following commands:
- cat – Concatenate files
- sort – Sort lines of text
- uniq – Report or omit repeated lines
- grep – Print lines matching a pattern
- wc – Print newline, word, and byte counts for each file
- head – Output the first part of a file
- tail – Output the last part of a file
- tee – Read from standard input and write to standard output and files

### Redirecting Standard Output
I/O redirection allows us to redefine where standard output goes. To redirect standard output to another file instead of the screen, we use the > redirection operator followed by the name of the file. Why would we want to do this? It's often useful to store the output of a command in a file. For example, we could tell the shell to send the output of the ls command to the file ls-output.txt instead of the screen:

`[me@linuxbox ~]$ ls -l /usr/bin > ls-output.txt`

### Group Commands
Let’s imagine a situation where we want to execute a series of commands and send the results to a log file. With we know already, we could do this:
{% highlight bash %}
[me@linuxbox ~]$ command1 > logfile.txt
[me@linuxbox ~]$ command2 >> logfile.txt
[me@linuxbox ~]$ command3 >> logfile.txt
{% endhighlight %}

The first command in this sequence creates/truncates a file named logfile.txt and each subsequent command appends its output to that file. This technique will work but there is a lot of redundant typing. There must be a better way.
As we saw in the previous chapter, we can put multiple commands on a single line like this:

`[me@linuxbox ~]$ command1; command2; command3`

So we could place all of our commands and redirections on a single line:

`[me@linuxbox ~]$ command1 > logfile.txt; command2 >> logfile.txt; command3 >> logfile.txt`

But what if we could treat the sequence as a single entity with a single output stream? We can do this by creating a group command. To do this, we surround our sequence with brace characters:

`[me@linuxbox ~]$ { command1; command2; command3; } > logfile.txt`

With our sequence surrounded by braces, the shell will consider it a single command in terms of redirection. Note that the shell requires whitespace around the braces and the final command in the sequence must be terminated with either a semicolon or a newline.

### Redirecting Standard Input
cat – Concatenate Files
The cat command reads one or more files and copies them to standard output like so:

`cat [file...]`

### Pipelines
The capability of commands to read data from standard input and send to standard output is utilized by a shell feature called pipelines. Using the pipe operator | (vertical bar), the standard output of one command can be piped into the standard input of another.

`command1 | command2`

#### The Difference Between `>` and `|`
At first glance, it may be hard to understand the redirection performed by the pipeline operator | versus the redirection operator >. Simply put, the redirection operator connects a command with a file, while the pipeline operator connects the output of one command with the input of a second command.

`command1 > file1`
`command1 | command2`

A lot of people will try the following when they are learning about pipelines, “just to see what happens”:
`command1 > command2`

Answer: sometimes something really bad.

Here is an actual example submitted by a reader who was administering a Linux-based server appliance. As the superuser, he did this:
`# cd /usr/bin`
`# ls > less`

The first command put him in the directory where most programs are stored and the second command told the shell to overwrite the file less with the output of the ls command. Since the /usr/bin directory already contained a file named less (the less program), the second command overwrote the less program file with the text from ls, thus destroying the less program on his system.

The lesson here is that the > redirection operator silently creates or overwrites files, so you need to treat it with a lot of respect.

#### Filters
Pipelines are often used to perform complex operations on data. It is possible to put several commands together into a pipeline. Frequently, the commands used this way are referred to as filters. Filters take input, change it somehow, and then output it. The first one we will try is sort. Imagine we wanted to make a combined list of all the executable programs in /bin and /usr/bin, put them in sorted order and view the resulting list:
`[me@linuxbox ~]$ ls /bin /usr/bin | sort | less`

### wc – Print Line, Word, and Byte Counts
The wc (word count) command is used to display the number of lines, words, and bytes contained in files.

### grep – Print Lines Matching a Pattern
grep is a powerful program used to find text patterns within files. It's used like this:
`grep pattern [file...]`

When grep encounters a “pattern” in the file, it prints out the lines containing it. The patterns that grep can match can be very complex, but for now we will concentrate on simple text matches. We'll cover the advanced patterns, called regular expressions in Chapter 19.

Here are a few handy options for grep:
- -i, causes grep to ignore case when performing the search (normally searches are case sensitive)
- -l, causes grep to only output the names of the files containing text that matches the pattern.
- -v, causes grep to print only those lines that do not match the pattern.
- -w, causes grep to only match whole words.

### head / tail – Print First / Last Part of Files
Sometimes we don't want all the output from a command. We may only want the first few lines or the last few lines. The head command prints the first ten lines of a file, and the tail command prints the last ten lines. While both commands print ten lines of text by default, this can be adjusted with the -n option.

### tee – Read from Stdin and Output to Stdout and Files
In keeping with our plumbing metaphor, Linux provides a command called tee which creates a “tee” fitting on our pipe. The tee program reads standard input and copies it to both standard output (allowing the data to continue down the pipeline) and to one or more files. This is useful for capturing a pipeline's contents at an intermediate stage of processing. Here we repeat one of our earlier examples, this time including tee to capture the entire directory listing to the file ls.txt before grep filters the pipeline's contents:
{% highlight bash linenos %}
[me@linuxbox ~]$ ls /usr/bin | tee ls.txt | grep 
bunzip2
bzip2
gunzip
gzip
unzip
zip
zipcloak
zipgrep
zipinfo
zipnote
zipsplit
{% endhighlight %}


## 07 Seeing the World as the Shell Sees It
### Expansion
Each time we type a command and press the Enter key, bash performs several substitutions upon the text before it carries out our command.

#### Tilde Expansion
As we may recall from our introduction to the cd command, the tilde character (~) has a special meaning. When used at the beginning of a word, it expands into the name of the home directory of the named user or, if no user is named, the home directory of the current user.

#### Parameter Expansion
We're going to touch only briefly on parameter expansion in this chapter, but we'll be covering it extensively later. It's a feature that is more useful in shell scripts than directly on the command line. Many of its capabilities have to do with the system's ability to store small chunks of data and to give each chunk a name. Many such chunks, more properly called variables, are available for our examination. For example, the variable named USER contains our username.


## 08 Advanced Keyboard Tricks
I often kiddingly describe Unix as “the operating system for people who like to type.”

clear – Clear the screen

history – Display the contents of the history list

#### Command Line Editing
**bash** uses a library (a shared collection of routines that different programs can use) called Readline to implement command line editing.

#### Cursor Movement
The following table lists the keys used to move the cursor:

{% highlight bash linenos %}
Ctrl-a
Move cursor to the beginning of the line.
Ctrl-e
Move cursor to the end of the line.
Ctrl-f
Move cursor forward one character; same as the right arrow key.
Ctrl-b
Move cursor backward one character; same as the left arrow key.
Alt-f
Move cursor forward one word.
Alt-b
Move cursor backward one word.
Ctrl-l
Clear the screen and move the cursor to the top-left corner. The clear command does the same thing.
{% endhighlight %}

#### Modifying Text
{% highlight bash linenos %}
Ctrl-d
Delete the character at the cursor location.
Ctrl-t
Transpose (exchange) the character at the cursor location with the one preceding it.
Alt-t
Transpose the word at the cursor location with the one preceding it.
Alt-l
Convert the characters from the cursor location to the end of the word to lowercase.
Alt-u
Convert the characters from the cursor location to the end of the word to uppercase.
{% endhighlight %}

#### Cutting and Pasting (Killing and Yanking) Text
The Readline documentation uses the terms killing and yanking to refer to what we would commonly call cutting and pasting. Items that are cut are stored in a buffer (a temporary storage area in memory) called the kill-ring.

{% highlight bash linenos %}
Ctrl-k
Kill text from the cursor location to the end of line.
Ctrl-u
Kill text from the cursor location to the beginning of the line.
Alt-d
Kill text from the cursor location to the end of the current word.
Alt-Backspace
Kill text from the cursor location to the beginning of the current word. If the cursor is at the beginning of a word, kill the previous word.
Ctrl-y
Yank text from the kill-ring and insert it at the cursor location.
{% endhighlight %}

#### The Meta Key
If you venture into the Readline documentation, which can be found in the “READLINE” section of the bash man page, you will encounter the term meta key. On modern keyboards this maps to the Alt key but it wasn't always so.

### Completion
Another way that the shell can help us is through a mechanism called completion. Completion occurs when we press the tab key while typing a command.

#### Programmable Completion
Recent versions of bash have a facility called programmable completion. Programmable completion allows you (or more likely, your distribution provider) to add additional completion rules. Usually this is done to add support for specific applications. For example, it is possible to add completions for the option list of a command or match particular file types that an application supports. Ubuntu has a fairly large set defined by default. Programmable completion is implemented by shell functions, a kind of mini shell script that we will cover in later chapters. If you are curious, try the following:
`set | less`
and see if you can find them. Not all distributions include them by default.

### Using History
This list of commands is kept in our home directory in a file called `.bash_history`. The history facility is a useful resource for reducing the amount of typing we have to do, especially when combined with command line editing.

#### History Commands
{% highlight %}
Ctrl-p
Move to the previous history entry. This is the same action as the up arrow.
Ctrl-n
Move to the next history entry. This is the same action as the down arrow.
Alt-<
Move to the beginning (top) of the history list.
Alt->
Move to the end (bottom) of the history list, i.e., the current command line.
Ctrl-r
Reverse incremental search. This searches incrementally from the current command line up the history list.
Alt-p
Reverse search, nonincremental. With this key, type in the search string and press enter before the search is performed.
Alt-n
Forward search, nonincremental.
Ctrl-o
Execute the current item in the history list and advance to the next
{% endhighlight %}

#### History Expansion Commands
{% highlight %}
!!
Repeat the last command. It is probably easier to press up arrow and enter.
!number
Repeat history list item number.
!string
Repeat last history list item starting with string.
!?string
Repeat last history list item containing string.
{% endhighlight %}

#### script
In addition to the command history feature in bash, most Linux distributions include a program called script that can be used to record an entire shell session and store it in a file. The basic syntax of the command is as follows:
`script [file]`
where file is the name of the file used for storing the recording. If no file is specified, the file typescript is used. See the script man page for a complete list of the program’s options and features.


## 09 Permissions
Operating systems in the Unix tradition differ from those in the MS-DOS tradition in that they are not only multitasking systems, but also multi-user systems.

### Users, Group Members, and Everybody Else
In the Unix security model, a user may own files and directories. When a user owns a file or directory, the user has control over its access.

When user accounts are created, users are assigned a number called a user ID (uid) which is then, for the sake of the humans, mapped to a username. The user is assigned a primary group ID (gid) and may belong to additional groups.

User accounts are defined in the /etc/passwd file and groups are defined in the /etc/group file. When user accounts and groups are created, these files are modified along with /etc/shadow which holds information about the user's password. For each user account, the /etc/passwd file defines the user (login) name, uid, gid, user’s real name, home directory, and login shell. If we examine the contents of /etc/passwd and /etc/group, we notice that besides the regular user accounts, there are accounts for the superuser (always uid 0) and various other system users.

### Reading, Writing, and Executing
#### File Types
{% highlight %}
-
A regular file.
d
A directory.
l
A symbolic link. Notice that with symbolic links, the remaining file attributes are always “rwxrwxrwx” and are dummy values. The real file attributes are those of the file the symbolic link points to.
c
A character special file. This file type refers to a device that handles data as a stream of bytes, such as a terminal or /dev/null.
b
A block special file. This file type refers to a device that handles data in blocks, such as a hard disk or DVD drive.
{% endhighlight %}

#### Permission Attributes
{% highlight %}
r
Allows a file to be opened and read.
Allows a directory's contents to be listed, but no file information is available unless the execute attribute is also set.
w
Allows a file to be written to or truncated, however this attribute does not allow files to be renamed or deleted. The ability to delete or rename files is determined by directory attributes.
Allows files within a directory to be created, deleted, and renamed if the execute attribute is also set.
x
Allows a file to be treated as a program and executed. Program files written in scripting languages must also be set as readable to be executed.
Allows a directory to be entered (i.e., cd directory) and directory metadata (i.e, ls -l directory) to be accessed. File operations such cp, rm, and mv require this access to the directory.
{% endhighlight %}

##### Permission Attribute Examples
{% highlight %}
-rwx------
A regular file that is readable, writable, and executable by the file's owner. No one else has any access.
-rw-------
A regular file that is readable and writable by the file's owner. No one else has any access.
-rw-r--r--
A regular file that is readable and writable by the file's owner. Members of the file's owner group may read the file. The file is readable by others.
-rwxr-xr-x
A regular file that is readable, writable, and executable by the file's owner. The file may be read and executed by everybody else.
-rw-rw----
A regular file that is readable and writable by the file's owner and members of the file's group owner only.
lrwxrwxrwx
A symbolic link. All symbolic links have “dummy” permissions. The real permissions are kept with the actual file pointed to by the symbolic link.
drwxrwx---
A directory. The owner and the members of the owner group may enter the directory and create, rename and remove files within the directory.
drwxr-x---
A directory. The owner may enter the directory and create, rename, and delete files within the directory. Members of the owner group may enter the directory but cannot create, delete, or rename files.
{% endhighlight %}

#### chmod – Change File Mode
{% highlight %}
0
000
---

1
001
--x

2
010
-w-

3
011
-wx

4
100
r--

5
101
r-x

6
110
rw-

7
111
rwx
{% endhighlight %}

#### chmod Symbolic Notation
{% highlight %}
u
Short for “user” i.e. the file or directory’s owner.
g
Group owner.
o
Short for others.
a
Short for “all.” This is the combination of “u”, “g”, and “o”.
{% endhighlight %}

##### chmod Symbolic Notation Examples
{% highlight %}
u+x
Add execute permission for the owner.
u-x
Remove execute permission from the owner.
+x
Add execute permission for the user, group, and others. This is equivalent to a+x.
o-rw
Remove the read and write permissions from anyone besides the user and group owner.
go=rw
Set the group owner and anyone besides the user to have read and write permission. If either the group owner or others previously had execute permission, it is removed.
u+x,go=rx
Add execute permission for the user and set the permissions for the group and others to read and execute. Multiple specifications may be separated by commas.
{% endhighlight %}

#### umask – Set Default Permissions
The umask command controls the default permissions given to a file when it is created. It uses octal notation to express a mask of bits to be removed from a file's mode attributes.

### Changing Identities
Sometimes we may find it necessary to take on the identity of another user. Often we want to gain superuser privileges to carry out some administrative task, but it is also possible to “become” another regular user for such things as testing an account. There are three ways to take on an alternate identity.
1. Log out and log back in as the alternate user.
2. Use the su command.
3. Use the sudo command.

#### su – Run a Shell with Substitute User and Group IDs
The su command is used to start a shell as another user.

#### sudo – Execute a Command as Another User
The sudo command is like su in many ways but has some important additional capabilities. The administrator can configure sudo to allow an ordinary user to execute commands as a different user (usually the superuser) in a controlled way.

#### Modern Linux Distributions and sudo
When Ubuntu was introduced, its creators took a different tack. By default, Ubuntu disables logins to the root account (by failing to set a password for the account) and instead uses sudo to grant superuser privileges. The initial user account is granted full access to superuser privileges via sudo and may grant similar powers to subsequent user accounts. This method of granting privileges is now the accepted standard is most modern distributions.

#### chown – Change File Owner and Group
The chown command is used to change the owner and group owner of a file or directory. Superuser privileges are required to use this command.

#### chgrp – Change Group Ownership
In older versions of Unix, the chown command only changed file ownership, not group ownership. For that purpose, a separate command, chgrp was used. It works much the same way as chown, except for being more limited.

### Changing Your Password
To set or change a password, the passwd command is used.
`passwd [user]`

The passwd, addgroup, and usermod commands are part of a suite of commands in the shadow-utils package

#### shadow-utils Commands
{% highlight %}
lastlog
Reports the most recent login of all users or of a given user.
useradd
Create a new user or update default new user information.
userdel
Delete a user account and related files.
usermod
Modify a user account.
groupadd
Create a new group.
groupdel
Delete a group.
groupmod
.Modify a group definition on the system.
{% endhighlight %}


## 10 Processes
Modern operating systems are usually multitasking, meaning they create the illusion of doing more than one thing at once by rapidly switching from one executing program to another. The Linux kernel manages this through the use of processes. Processes are how Linux organizes the different programs waiting for their turn at the CPU.
- ps – Report a snapshot of current processes
- top – Display tasks
- jobs – List active jobs
- bg – Place a job in the background
- fg – Place a job in the foreground
- kill – Send a signal to a process
- killall – Kill processes by name
- nice - Run a program with modified scheduling priority
- renice - Alter priority of running processes
- nohup - Run a command immune to hangups
- halt/poweroff/reboot - Halt, power-off, or reboot the system
- shutdown – Shutdown or reboot the system

### How a Process Works
When a system starts up, the kernel initiates a few of its own activities as processes and launches a program called init. init, in turn, starts systemd which starts all the system services. In older Linux distributions init runs a series of shell scripts (located in `/etc`) called init scripts to perform a similar function. Many system services are implemented as daemon programs, programs that just sit in the background and do their thing without having any user interface. So, even if we are not logged in, the system is at least a little busy performing routine stuff.

The fact that a program can launch other programs is expressed in the process scheme as a **parent process** producing a **child process**.

### Viewing Processes
The most commonly used tool to view processes (there are several) is the ps command.

#### Process States
{% highlight %}
R
Running. This means that the process is running or ready to run.
S
Sleeping. The process is not running; rather, it is waiting for an event, such as a keystroke or network packet.
D
Uninterruptible sleep. The process is waiting for I/O such as a disk drive.
T
Stopped. The process has been instructed to stop. More on this later in the chapter.
Z
A defunct or “zombie” process. This is a child process that has terminated but has not been cleaned up by its parent.
<
A high-priority process. It's possible to grant more importance to a process, giving it more time on the CPU. This property of a process is called niceness. A process with high priority is said to be less nice because it's taking more of the CPU's time, which leaves less for everybody else.
N
A low-priority process. A process with low priority (a “nice” process) will get processor time only after other processes with higher priority have been serviced.
{% endhighlight %}

#### Viewing Processes Dynamically with top
While the ps command can reveal a lot about what the machine is doing, it provides only a snapshot of the machine's state at the moment the ps command is executed. To see a more dynamic view of the machine's activity, we use the `top` command:

The top program displays a continuously updating (by default, every three seconds) display of the system processes listed in order of process activity. The name top comes from the fact that the top program is used to see the “top” processes on the system. The top display consists of two parts: a system summary at the top of the display, followed by a table of processes sorted by CPU activity:

The top program accepts a number of keyboard commands. The two most interesting are h, which displays the program's help screen, and q, which quits top.

Both major desktop environments provide graphical applications that display information similar to top (in much the same way that Task Manager in Windows works), but top is better than the graphical versions because it is faster and it consumes far fewer system resources. After all, our system monitor program shouldn't be the source of the system slowdown that we are trying to track.
