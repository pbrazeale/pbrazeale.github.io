+++
tags = ['Linux', 'Bash']
title = 'Linux Command Line: Part 3 Common Tasks and Essential Tools'
date = 2025-03-10T18:34:07+01:00
+++

## 14 – Package Management

> Today, most people can satisfy all of their software needs by installing packages from their Linux distributor. This contrasts with the early days of Linux, when one had to download and compile source code to install software. There isn’t anything wrong with compiling source code; in fact, having access to source code is the great wonder of Linux. It gives us (and everybody else) the ability to examine and improve the system.

### Packaging Systems

Most distributions fall into one of two camps of packaging technologies: the **Debian .deb** camp and the **Red Hat .rpm** camp. There are some important exceptions such as Gentoo, Slackware, and **Arch** ...

#### Package Files

The basic unit of software in a packaging system is the package file. A package file is a compressed collection of files that comprise the software package. ... In addition to the files to be installed, the package file also includes metadata about the package ... many packages contain pre- and post-installation scripts that perform configuration tasks before and after the package installation.

**shared libraries**, which provide essential services to more than one program. If a package requires a shared resource such as a shared library, it is said to have a **dependency**. Modern package management systems all provide some method of dependency resolution to ensure that when a package is installed, all of its dependencies are installed, too.

### Distribution-Independent Package Formats

Over the last several years distribution vendors have come out with universal package formats that are not tied to a particular Linux distribution. These include **Snaps** (developed and promoted by Canonical), **Flatpaks** (pioneered by Red Hat, but now widely available) and **AppImages**. Though they each work a little differently, their goal is to have an application and all of its dependencies bundled together and installed in a single piece. This is not an entirely new idea. In the early days of Linux (think the late 1990s) the was a technique called static linking which combined an application and its required libraries into a single large binary.

> Users were not crying out for these packaging formats and they do little to enhance the open source community, thus until such time the various performance issues are resolved use of these formats is not recommended.

### The Linux Software Installation Myth

The Linux software ecosystem is based on the idea of open source code. If a program developer releases source code for a program, it is likely that a person associated with a distribution will package the program and include it in their repository. This method ensures that the program is well integrated into the distribution, and the user is given the convenience of “one-stop shopping” for software, rather than having to search for each program's website. Recently, major proprietary platform vendors have begun building application stores that mimic this idea.

#### A lack of driver support is usually caused by one of three things:

1. **The device is too new**.  ... it falls upon a member of the Linux community to write the kernel driver code. This takes time.
2. **The device is too exotic.**  Not all distributions include every possible device driver ...
3. **The hardware vendor is hiding something.**  It has neither released source code for a Linux driver, nor has it released the technical documentation for some-body to create one for them ...

## 15 – Storage Media

**mount** – Mount a file system
**umount** – Unmount a file system
**parted** – Partition manipulation program
**mkfs** – Create a file system
**fsck** – Check and repair a file system
**dd** – Convert and copy a file
**genisoimage** – Create an ISO 9660 image file
**wodim** – Write data to optical storage media
**sha256sum** – Compute and check SHA256 checksums

### Mounting and Unmounting Storage Devices

The first step in managing a storage device is attaching the device to the file system tree. This process, called mounting, allows the device to interact with the operating system.

### Why Unmounting Is Important

If you look at the output of the free command, which displays statistics about memory usage, you will see a statistic called buffers. Computer systems are designed to go as fast as possible. One of the impediments to system speed is slow devices. Printers are a good example ...

**Unmounting** a device entails writing all the remaining data to the device so that it can be safely removed. If the device is removed without unmounting it first, the possibility exists that not all the data destined for the device has been transferred.

### Creating New File Systems

**parted** is one of a host of programs (both command line and graphical) that allow us to interact directly with disk-like devices (such as hard disk drives and flash drives) at a very low level ...

#### Creating a New File System with mkfs

With our partition editing done, it’s time to create (i.e., format) the new file systems on our drive. To do this, we will use **mkfs** (short for “make file system”), which can create file systems in a variety of formats. To create the ext4 file system on the drive, we use the `-t` option to specify the ext4 file system type, followed by a descriptive volume label, and the name of the device containing the partition we want to format.

### Testing and Repairing File Systems

In addition to checking the integrity of file systems, **fsck** can also repair corrupt file systems with varying degrees of success, depending on the amount of damage.

#### What the fsck?

> In Unix culture, the word fsck is often used in place of a popular word with which it shares three letters. This is especially appropriate, given that you will probably be uttering the aforementioned word if you find yourself in a situation where you are forced to run fsck.

### Verifying Data

... tool we can use for this is sha256sum, a modern replacement for an earlier program called md5sum.

```bash
$ sha256sum -b linuxmint-22-cinnamon-64bit.iso
7a04b54830004e945c1eda6ed6ec8c57ff4b249de4b331bd021a849694f29b8f *lin uxmint-22-cinnamon-64bit.iso
```

The `-b` option tells sha256sum that we are looking at a binary file rather than text. As we can see, the checksum matches the one we saw in sha256sum.txt. However looking at the checksum this way is a little tedious. Another way we can check the file is to have sha256sum process the sha256sum.txt file to compare its checksums against ones it generates from the files on the list. We can do this by running the sha256sum program this way:

```bash
$ sha256sum -c --ignore-missing sha256sum.txt
linuxmint-22-cinnamon-64bit.iso: OK
```

## 16 – Networking

- `ping` – Send an ICMP ECHO_REQUEST to network hosts
- `traceroute` – Print the route packets trace to a network host
- `ip` – Show / manipulate routing, devices, policy routing and tunnels
- `netstat` – Print network connections, routing tables, interface statistics, mas-querade connections, and multicast memberships
- `ftp` – Internet file transfer program
- `curl` - Transfer a URL
- `wget` – Non-interactive network downloader
- `ssh` – OpenSSH SSH client (remote login program)

We’re going to assume a little background in networking. In this, the Internet age, everyone using a computer needs a basic understanding of networking concepts. To make full use of this chapter we should be familiar with the following terms:

- Internet protocol (IP) address
- Host and domain name
- Uniform resource identifier (URI)

### Examining and Monitoring a Network

The **ping** command sends a special network packet called an ICMP ECHO_REQUEST to a specified host.

The **traceroute** program (some systems use the similar **tracepath** program instead) lists all the “hops” network traffic takes to get from the local system to a specified host

The **ip** program is a multi-purpose network configuration tool that makes use of the full range of networking features available in modern Linux kernels. It replaces the earlier and now deprecated ifconfig program.

192.168.1.0 network is our LAN, but what is 169.254.0.0? Well, that’s a piece of network trickery called Automatic Private IP Addressing (APIPA).

### Transporting Files Over a Network

One of the true “classic” programs, **ftp** gets its name from the protocol it uses, the File Transfer Protocol. FTP was once the most widely used method of downloading files over the Internet. Some web browsers still support it, and we may see URIs starting with the protocol ftp://.

Another command-line program for file downloading is wget. It is useful for downloading content from both web and FTP sites. Single files, multiple files, and even entire sites can be downloaded. To download the first page of linuxcommand.org we could do this:

```shell
[me@linuxbox ~]$ wget http://linuxcommand.org/index.php
```

### Secure Communication with Remote Hosts

In the early days, before the general adoption of the Internet, there were a couple of popular programs used to log in to remote hosts. These were the _rlogin and telnet_ programs. These programs, however, suffer from the same fatal flaw that the ftp program does; they transmit all their communications (including login names and passwords) in cleartext.

To address this problem, a new protocol called Secure Shell (SSH) was developed. **SSH** solves the two basic problems of secure communication with a remote host.

1. It authenticates that the remote host is who it says it is (thus preventing so-called man-in-the-middle attacks).
2. It encrypts all of the communications between the local and remote hosts.

_by default, on port 22_

```shell
[me@linuxbox ~]$ ssh remote-sys 'ls *' > dirlist.txt
me@twin4's password:
[me@linuxbox ~]$
```

Notice the use of the single quotes in the command above. This is done because we do not want the pathname expansion performed on the local machine; rather, we want it to be performed on the remote system. Likewise, if we had wanted the output redirected to a file on the remote machine, we could have placed the redirection operator and the filename within the single quotes.

#### Tunneling with SSH

Part of what happens when you establish a connection with a remote host via **SSH** is that an encrypted tunnel is created between the local and remote systems. Normally, this tunnel is used to allow commands typed at the local system to be transmitted safely to the remote system and for the results to be transmitted safely back. In addition to this basic function, _the SSH protocol allows most types of network traffic to be sent through the encrypted tunnel, creating a sort of virtual private network (VPN)_ between the local and remote systems.

#### scp and sftp

The OpenSSH package also includes two programs that can make use of an SSH-encrypted tunnel to copy files across the network. The first, **scp** (secure copy) is used much like the familiar cp program to copy files. The most notable difference is that the source or destination pathnames may be preceded with the name of a remote host, followed by a colon character. For example, if we wanted to copy a document named document.txt from our home directory on the remote system, remote-sys, to the current working directory on our local system, we could do this:

```shell
[me@linuxbox ~]$ scp remote-sys:document.txt .
me@remote-sys's password:
document.txt 100% 5581 5.5KB/s 00:00
[me@linuxbox ~]$
```

The second SSH file-copying program is **sftp** which, as its name implies, is a secure replacement for the ftp program. sftp works much like the original ftp program that we used earlier; however, instead of transmitting everything in cleartext, it uses an SSH encrypted tunnel.

**Tip:** The SFTP protocol is supported by many of the graphical file managers found in Linux distributions. Using either GNOME or KDE, we can enter a URI beginning with sftp:// into the location bar and operate on files stored on a remote system running an SSH server.

#### An SSH Client for Windows?

The most popular one is probably PuTTY by Simon Tatham and his team.

## 17 – Searching for Files

- `locate` – Find files by name
- `find` – Search for files in a directory hierarchy

We will also look at a command that is often used with file-search commands to process the resulting list of files.

- `xargs` – Build and execute command lines from standard input

In addition, we will introduce a couple of commands to assist us in our explorations.

- `touch` – Change file times
- `stat` – Display file or file system status

### locate – Find Files the Easy Way

```shell
[me@linuxbox ~]$ locate bin/zip
```

The **locate** program performs a rapid database search of pathnames, and then outputs every name that matches a given substring.

The two most common ones found in modern Linux distributions are **plocate** and **mlocate**, though they are usually accessed by a symbolic link named locate.

#### Where Does the locate Database Come From?

The locate database is created by another program named **updatedb**. Usually, it is run periodically as a **cron job**, that is, a task performed at regular intervals by the cron daemon. Most systems equipped with locate run updatedb once a day ... it’s possible to run the updatedb program manually by becoming the superuser and running updatedb at the prompt.

### find – Find Files the Hard Way

While the **locate** program can **find** a file based solely on its name, the find program searches a given directory (and its subdirectories) for files based on a variety of attributes.

Since the list is sent to standard output, we can pipe the list into other programs. Let’s use wc to count the number of files.

```shell
[me@linuxbox ~]$ find ~ | wc -l
47068
```

```shell
[me@linuxbox ~]$ find ~ -type d | wc -l
1695
```

- Adding the test -type d limited the search to directories.

#### find File Types

| File Type | Description                   |
| --------- | ----------------------------- |
| b         | Block special device file     |
| c         | Character special device file |
| d         | Directory                     |
| f         | Regular file                  |
| l         | Symbolic link                 |

We can also search by file size and filename by adding some additional tests. Let’s look for all the regular files that match the wildcard pattern `*.JPG` and are larger than one megabyte.

```shell
[me@linuxbox ~]$ find ~ -type f -name "*.JPG" -size +1M | wc -l 840
```

#### find Size Units

| Character | Unit                                                          |
| --------- | ------------------------------------------------------------- |
| b         | 512-byte blocks. This is the default if no unit is specified. |
| c         | Bytes.                                                        |
| w         | 2-byte words.                                                 |
| k         | Kilobytes (units of 1024 bytes).                              |
| M         | Megabytes (units of 1048576 bytes).                           |
| G         | Gigabytes (units of 1073741824 bytes).                        |

#### Dealing with Funny Filenames

Unix-like systems allow embedded spaces (and even newlines!) in filenames. This causes problems for programs like xargs that construct argument lists for other programs. An embedded space will be treated as a delimiter, and the resulting command will interpret each space-separated word as a separate argument. To overcome this, find and xargs allow the optional use of a null character as an argument separator. A null character is defined in ASCII as the character represented by the number zero (as opposed to, for example, the space character, which is defined in ASCII as the character represented by the number 32). The find command provides the action -print0, which produces null-separated output, and the **xargs** command has the `--null (or -0)` option, which accepts null separated input. Here’s an example:

```shell
find ~ -iname `'*.jpg'` -print0 | xargs --null ls -l
```

Using this technique, we can ensure that all files, even those containing embedded spaces in their names, are handled correctly.

## 18 – Archiving and Backup

One of the system administrator primary tasks is _keeping the system’s data secure_. One way this is done is by performing timely backups of the system’s files.

- `gzip` – Compress or expand files
- `bzip2` – A block sorting file compressor

These are the archiving programs:

- `tar` – Tape archiving utility
- `zip` – Package and compress files

This is the file synchronization program:

- `rsync` – Remote file and directory synchronization

### Compressing Files

**Data compression** is the process of removing _redundancy_ from data.

_Compression algorithms_ (the mathematical techniques used to carry out the compression) fall into two general categories.

1. **Lossless**: Lossless compression preserves all the data contained in the original.
2. **Lossy**: Lossy compression, on the other hand, removes data as the compression is performed to allow more compression to be applied. When a lossy file is restored, it does not match the original version; rather, it is a close approximation.

#### gzip

The **gzip** program is used to compress one or more files. When executed, it replaces the original file with a compressed version of the original. The corresponding **gunzip** program is used to restore compressed files to their original, uncompressed form.

#### bzip2

The **bzip2** program, by Julian Seward, is similar to gzip but uses a different compression algorithm that achieves higher levels of compression at the cost of compression speed.

### Archiving Files

A common file-management task often used in conjunction with compression is archiving. Archiving is the process of gathering up many files and bundling them together into a single large file. Archiving is often done as part of system backups. It is also used when old data is moved from a system to some type of long-term storage.

#### tar

We often see filenames that end with the extension .tar or .tgz, which indicate a “plain” tar archive and a gzipped archive, respectively. A **tar** archive can consist of a group of separate files, one or more directory hierarchies, or a mixture of both.

When specifying pathnames, wildcards are not normally supported; however, the GNU version of tar (which is the version most often found in Linux distributions) supports them with the `--wildcards` option. Here is an example using our previous playground.tar file:

```shell
[me@linuxbox ~]$ cd foo
[me@linuxbox foo]$ tar xf ../playground2.tar --wildcards 'home/me/playground/dir-*/file-A'
```

#### find + tar

```shell
[me@linuxbox ~]$ find playground -name 'file-A' -exec tar rf playground.tar '{}' '+'
```

Here we use **find** to match all the files in playground named file-A and then, using the `-exec` action, we invoke **tar** in the append mode (r) to add the matching files to the archive playground.tar.

Using tar with find is a _good way of creating incremental backups_ of a directory tree or an entire system. By using find to match files newer than a timestamp file, we could create an archive that contains only those files newer than the last archive, assuming that the timestamp file is updated right after each archive is created.

#### zip

The **zip** program is both a compression tool and an archiver. The file format used by the program is familiar to Windows users, as it reads and writes .zip files. In Linux, however, gzip is the predominant compression program, with bzip2 being a close second.

One thing to note about zip (as opposed to tar) is that if an existing archive is specified, it is updated rather than replaced. _This means the existing archive is preserved, but new files are added and matching files are replaced._

### Synchronizing Files and Directories

In the Unix-like world, the preferred tool for this task is rsync. This program can synchronize both local and remote directories by using the rsync remote-update protocol, which allows rsync to quickly detect the differences between two directories and perform the minimum amount of copying required to bring them into sync. This makes rsync very fast and economical to use, compared to other kinds of copy programs.

**rsync** _options source destination_

```shell
[me@linuxbox ~]$ rsync -av playground foo
```

#### Using rsync Over a Network

the r in rsync stands for “remote.”

```shell
[me@linuxbox ~]$ sudo rsync -av --delete --rsh=ssh /etc /home /usr/local remote-sys:/backup
```

We made two changes to our command to facilitate the network copy.

1. we added the --rsh=ssh option, which instructs rsync to use the ssh program as its remote shell. In this way, we were able to use an ssh-encrypted tunnel to securely transfer the data from the local system to the remote host.
2. we specified the remote host by prefixing its name (in this case the remote host is named remote-sys) to the destination pathname.

## 19 – Regular Expressions

For our discussion, we will limit ourselves to regular expressions as described in the POSIX standard (which will cover most of the command line tools), as opposed to many programming languages (most notably Perl), which use slightly larger and richer sets of notations.

### grep

characters b, z, i, and p are found in that order, with no other characters in between. The characters in the string bzip are all literal characters, in that they match themselves. In addition to literals, regular expressions may also include metacharacters that are used to specify more complex matches. Regular expression metacharacters consist of the following:
`^ $ . [ ] { } - ? * + ( ) | \`

**Note**: As we can see, many of the regular expression metacharacters are also characters that have meaning to the shell when expansion is performed. When we pass _regular expressions containing metacharacters on the command line, it is vital that they be enclosed in quotes_ to prevent the shell from attempting to expand them.

```shell
[me@linuxbox ~]$ grep -h '.zip' dirlist*.txt
```

We searched for any line in our files that matches the regular expression “.zip”. There are a couple of interesting things to note about the results. Notice that the zip program was not found. This is because the inclusion of the dot metacharacter in our regular expression increased the length of the required match to four characters, one of which must precede the “z”. Also, if any files in our lists had contained the file extension .zip, they would have been matched as well, because the period character in the file extension would be matched by the “any character,” too.

### Anchors

The caret `^` and dollar sign `$` characters are treated as anchors in regular expressions. This means they cause the match to occur only if the regular expression is found at the _beginning of the line_ `^` or at the _end of the line_ `$`.

In addition to matching any character at a given position in our regular expression, we can also match a single character from a specified set of characters by using **bracket expressions**. With bracket expressions, we can specify a set of characters (including characters that would otherwise be interpreted as metacharacters) to be matched. In this example, using a two-character set, we match any line that contains the string bzip or gzip:

```shell
[me@linuxbox ~]$ grep -h '[bg]zip' dirlist*.txtbzip2
```

#### Traditional Character Ranges

It’s just a matter of putting all 26 uppercase letters in a bracket expression. But the idea of all that typing is deeply troubling, so there is another way.

```shell
[me@linuxbox ~]$ grep -h '^[A-Z]' dirlist*.txt
```

```shell
[me@linuxbox ~]$ grep -h '^[A-Za-z0-9]' dirlist*.txt
```

#### POSIX Character Classes

The ASCII table was expanded to use a full eight bits, adding characters 128-255, which accommodated many more languages. To support this ability, the POSIX standards introduced a concept called a locale, which could be adjusted to select the character set needed for a particular location.

```shell
[me@linuxbox ~]$ echo $LANG
en_US.UTF-8
```

With this setting, POSIX-compliant applications will use a dictionary collation order rather than ASCII order. This explains the behavior of the previous commands. A character range of `[A-Z]` when interpreted in dictionary order includes all of the alphabetic characters except the lowercase a, hence our results.

#### Reverting to Traditional Collation Order

You can opt to have your system use the traditional (ASCII) collation order by changing the value of the LANG environment variable. As we saw earlier, the LANG variable contains the name of the language and character set used in your locale. This value was originally determined when you selected an installation language as your Linux version was installed.

To change the locale to use the traditional Unix behaviors, set the LANG variable to POSIX.

```shell
[me@linuxbox ~]$ export LANG=POSIX
```

Note that this change converts the system to use U.S. English (more specifically, ASCII) for its character set, so be sure if this is really what you want.

You can make this change permanent by adding this line to your _.bashrc_ file.
`export LANG=POSIX`

#### POSIX Basic vs. Extended Regular Expressions

POSIX also splits regular expression implementations into two kinds: basic regular expressions (BRE) and extended regular expressions (ERE). The features we have covered so far are supported by any application that is POSIX compliant and implements BRE. Our grep program is one such program.

##### POSIX HISTORY

During the 1980’s, Unix became a very popular commercial operating system, but by 1988, the Unix world was in turmoil. Many computer manufacturers had licensed the Unix source code from its creators, AT&T, and were supplying various versions of the operating system with their systems ... As always with proprietary vendors, each was trying to play a winning game of “lock-in” with their customers. This dark time in the history of Unix is known today as “_the Balkanization_.”

In the mid-1980s, the IEEE began developing a set of standards that would define how Unix (and Unix-like) systems would perform. These standards, formally known as IEEE 1003, define the application programming interfaces (APIs), shell and utilities that are to be found on a standard Unix-like system. The name POSIX, which stands for Portable Operating System Interface (with the X added to the end for extra snappiness), was suggested by Richard Stallman (yes, that Richard Stallman) and was adopted by the IEEE.

- See: **Linux Pocket Guide** pages 71-74

### Putting Regular Expressions to Work

```shell
[me@linuxbox ~]$ for i in {1..10}; do echo "(${RANDOM:0:3}) ${RANDOM:0:3}-${RANDOM:0:4}" >> phonelist.txt; done
```

This command will produce a file named phonelist.txt containing ten phone numbers. Each time the command is repeated, another ten numbers are added to the list. We can also change the value 10 near the beginning of the command to produce more or fewer phone numbers.

One useful method of validation would be to scan the file for invalid numbers and display the resulting list.

```shell
[me@linuxbox ~]$ grep -Ev '^\([0-9]{3}\) [0-9]{3}-[0-9]{4}$' phonelist.txt(292) 108-518 (129) 44-1379[me@linuxbox ~]$
```

#### Finding Ugly Filenames with find

```shell
[me@linuxbox ~]$ find . -regex '.*[^-_./0-9a-zA-Z].*'
```

Because of the requirement for an exact match of the entire pathname, we use .\* at both ends of the expression to match zero or more instances of any character. In the middle of the expression, we use a negated bracket expression containing our set of acceptable pathname characters.

#### Searching for Files with locate

The locate program supports both basic (the --regexp option) and extended (the --regex option) regular expressions. With it, we can perform many of the same operations that we performed earlier with our dirlist files.

```shell
[me@linuxbox ~]$ locate --regex 'bin/(bz|gz|zip)'
```

## 20 – Text Processing

- `cat` – Concatenate files and print on the standard output
- `sort` – Sort lines of text files
- `uniq` – Report or omit repeated lines
- `cut` – Remove sections from each line of files
- `paste` – Merge lines of files
- `join` – Join lines of two files on a common field
- `tac` – Concatenate and print files in reverse
- `rev` – Reverse lines characterwise
- `comm` – Compare two sorted files line by line
- `diff` – Compare files line by line
- `patch` – Apply a diff file to an original
- `tr` – Translate or delete characters
- `sed` – Stream editor for filtering and transforming text
- `aspell` – Interactive spell checker

### Applications of Text

#### Printer Output

On Unix-like systems, output destined for a printer is sent as plain text or, if the page contains graphics, is converted into a text format page description language known as **PostScript**, which is then sent to a program that generates the graphic dots to be printed.

### Revisiting Some Old Friends

#### MS-DOS Text vs. Unix Text

One of the reasons you may want to use cat to look for non-printing characters in text is to spot hidden carriage returns. Where do hidden carriage returns come from? DOS and Windows! Unix and DOS don’t define the end of a line the same way in text files. Unix ends a line with a linefeed character (ASCII 10) while MSDOS and its derivatives use the sequence carriage return (ASCII 13) and linefeed to terminate each line of text.

There are a several ways to convert files from DOS to Unix format. On many Linux systems, there are programs called dos2unix and unix2dos, which can convert text files to and from DOS format. However, if you don’t have dos2unix on your system, don’t worry. The process of converting text from DOS to Unix format is simple; it involves the removal of the offending carriage returns.

#### sort

```shell
sort file1.txt file2.txt file3.txt > final_sorted_list.txt
```

- See: **Linux Pocket Guide** pg. 77-79

Many uses of sort involve the processing of **tabular data**, such as the results of the previous ls command. If we apply database terminology to the previous table, we would say that each row is a record and that each record consists of multiple fields, such as the file attributes, link count, filename, file size, and so on. sort is able to process individual fields. In database terms, we are able to specify one or more key fields to use as sort keys. In the previous example, we specify the n and r options to perform a reverse numerical sort and specify -k 5 to make sort use the fifth field as the key for sorting.

_When using number titling, attempt to use decimal place numbers `01-10` instead of `1-10`_

#### uniq

Compared to sort, the uniq program is lightweight. uniq performs a seemingly trivial task. When given a sorted file (or standard input), it removes any duplicate lines and sends the results to standard output. It is often used in conjunction with sort to clean the output of duplicates.

**Tip**: While uniq is a traditional Unix tool often used with sort, the GNU version of sort supports a -u option, which removes duplicates from the sorted output.

### Slicing and Dicing

#### cut

The cut program is used to extract a section of text from a line and output the extracted section to standard output. It can accept multiple file arguments or input from standard input.

#### paste

The paste command does the opposite of cut. Rather than extracting a column of text from a file, it adds one or more columns of text to a file. It does this by reading multiple files and combining the fields found in each file into a single stream on standard output

#### join

In some ways, join is like paste in that it adds columns to a file, but it uses a unique way to do it. A join is an operation usually associated with relational databases where data from multiple tables with a shared key field is combined to form a desired result.

- _see my notes on [[SQL]]_

### Comparing Text

A system administrator may, for example, need to compare an existing configuration file to a previous version to diagnose a system problem. Likewise, a programmer frequently needs to see what changes have been made to programs over time.

#### comm

The comm program compares two text files and displays the lines that are unique to each one and the lines they have in common.

```shell
[me@linuxbox ~]$ comm file1.txt file2.txt
a
		b
		c
		d
	e
```

As we can see, comm produces three columns of output. The first column contains lines unique to the first file argument, the second column contains the lines unique to the second file argument, and the third column contains the lines shared by both files. comm supports options in the form -n, where n is either 1, 2, or 3. When used, these options specify which columns to suppress. For example, if we wanted to only output the lines shared by both files, we would suppress the output of the first and second columns.

```shell
[me@linuxbox ~]$ comm -12 file1.txt file2.txt
b
c
d
```

#### diff

Like the comm program, diff is used to detect the differences between files. However, diff is a much more complex tool, supporting many output formats and the ability to process large collections of text files at once.
_Precursor to [[git]]?_

#### patch

The patch program is used to apply changes to text files. It accepts output from diff and is generally used to convert older version files into newer versions. Let’s consider a famous example. The Linux kernel is developed by a large, loosely organized team of contributors who submit a constant stream of small changes to the source code. The Linux kernel consists of several million lines of code, while the changes that are made by one contributor at one time are quite small. It makes no sense for a contributor to send each developer an entire kernel source tree each time a small change is made. Instead, a diff file is submitted. The diff file contains the change from the previous version of the kernel to the new version with the contributor's changes. The receiver then uses the patch program to apply the change to his own source tree. Using diff/patch offers two significant advantages.
_This sounds like older version before git_

#### aspell

The aspell program is the successor to an earlier program named ispell and can be used, for the most part, as a drop-in replacement. While the aspell program is mostly used by other programs that require spell-checking capability, it can also be used effectively as a standalone tool from the command line. It has the ability to intelligently check various types of text files, including HTML documents, C/C++ programs, email messages, and other kinds of specialized texts.

## 21 – Formatting Output

- nl – Number lines
- fold – Wrap each line to a specified length
- fmt – A simple text formatter
- pr – Prepare text for printing
- printf – Format and print data
- groff – A document formatting system

### fold

Folding is the process of breaking lines of text at a specified width. Like our other commands, fold accepts either one or more text files or standard input. If we send fold a simple stream of text, we can see how it works.

### fmt

The fmt program also folds text, plus a lot more. It accepts either files or standard input and performs paragraph formatting on the text stream. Basically, it fills and joins lines in text while preserving blank lines and indentation.

### pr

The pr program is used to paginate text. When printing text, it is often desirable to separate the pages of output with several lines of whitespace, to provide a top margin and a bottom margin for each page. Further, this whitespace can be used to insert a header and footer on each page.

### printf – Format and Print Data

Unlike the other commands in this chapter, the printf command is not used for pipelines (it does not accept standard input) nor does it find frequent application directly on the command line (it’s mostly used in scripts). So why is it important? Because it is so widely used.

### Document Formatting Systems

Two main families of document formatters dominate the field: those descended from the original roff program, including nroff and troff, and those based on Donald Knuth’s TEX (pronounced “tek”) typesetting system.

- The later troff program formats documents for output on typesetters, devices used to produce “camera-ready” type for commercial printing.
- The TEX system (in stable form) first appeared in 1989 and has, to some degree, dis-placed troff as the tool of choice for typesetter output.

PostScript is a page description language that is used to describe the contents of a printed page to a typesetter-like device.

## 22 - Printing

- pr – Convert text files for printing
- lp / lpr – Print files
- a2ps – Format files for printing on a PostScript printer
- lpstat – Show printer status information
- lpq – Show printer queue status
- lprm – Cancel print jobs

#### Graphical Printers

The development of GUIs led to major changes in printer technology. As computers moved to more picture-based displays, printing moved from character-based to graphical techniques. This was facilitated by the advent of the low-cost laser printer which, instead of printing fixed characters, could print tiny dots anywhere in the printable area of the page. This made printing proportional fonts (like those used by typesetters), and even photographs and high-quality diagrams, possible.

The first major PDL was PostScript from Adobe Systems, which is still in wide use today. The PostScript language is a complete programming language tailored for typography and other kinds of graphics and imaging. It includes built-in support for 35 standard, high-quality fonts, plus the ability to accept additional font definitions at runtime.

- The generic name for this process of rendering something into a large bit pattern (called a bitmap) is raster image processor (RIP).

### Printing with Linux

Modern Linux systems employ two software suites to perform and manage printing. The first, _Common Unix Printing System_ (**CUPS**) provides print drivers and print-job management, and the second, _Ghostscript_, a PostScript interpreter, acts as a **RIP**.

### Preparing Files for Printing

- `pr` is used to adjust text to fit on a specific page size, with optional page headers and margins.

### Sending a Print Job to a Printer

The CUPS printing suite supports two methods of printing historically used on Unix-like systems. One method, called Berkeley or **LPD** (used in the Berkeley Software Distribution version of Unix), uses the `lpr` program, while the other method, called **SysV** (from the System V version of Unix), uses the `lp` program. Both programs do roughly the same thing. Choosing one over the other is a matter of personal taste.

##### TIP

Many Linux distributions allow you to specify a “printer” that outputs files in Portable Document Format (PDF), rather than printing on the physical printer. This is very handy for experimenting with printing commands. Check your printer configuration program to see whether it supports this configuration. On some distributions, you may need to install additional packages (such as cups-pdf) to enable this capability.

### Monitoring and Controlling Print Jobs

As Unix printing systems are designed to handle multiple print jobs from multiple users, CUPS is designed to do the same. Each printer is given a print queue, where jobs are parked until they can be spooled to the printer.

#### lpstat – Display Print System Status

The lpstat program is useful for determining the names and availability of printers on the system.

#### lpq – Display Printer Queue Status

To see the status of a printer queue, the lpq program is used. This allows us to view the status of the queue and the print jobs it contains.

#### lprm / cancel – Cancel Print Jobs

CUPS supplies two programs used to terminate print jobs and remove them from the print queue. One is Berkeley style (lprm) and the other is System V (cancel). They differ slightly in the options they support, but do basically the same thing.

## 23 – Compiling Programs

The entire ecosystem of Linux development relies on free exchange between developers. For many desktop users, compiling is a lost art.

So why compile software? There are two reasons:

1. **Availability**. Despite the number of precompiled programs in distribution repositories, some distributions may not include all the desired applications. In this case, the only way to get the desired program is to compile it from source.
2. **Timeliness**. While some distributions specialize in cutting-edge versions of programs, many do not. This means that to have the latest version of a program, compiling is necessary.

- make – Utility to maintain programs

### What is Compiling?

Simply put, compiling is the process of translating _source code_ (the human-readable description of a program written by a programmer) into the native language of the computer’s processor.

_assembly language_, which replaced the numeric codes with (slightly) easier to use character _mnemonics_ such as CPY (for copy) and MOV (for move). Programs written in assembly language are processed into machine language by a program called an _assembler_. Assembly language is still used today for certain specialized programming tasks, such as **device drivers and embedded systems**.

executed directly. These are written in what are known as scripting or interpreted languages. These languages have grown in popularity in recent years and include Perl, Python, PHP, Ruby, and many others.
