# Configuration and the Environment
## 11 - The Environment

This shows an important rule regarding child processes: a child process cannot alter the environment of its parent.

### Launching a Program with a Temporary Environment
Another handy trick the shell provides is the ability to execute a command and give it a temporary environment variable. Sometimes we want to run a program and give it a special environment value. A good example is the man command which looks for an environment variable named MANWIDTH that tells man how wide to format its output.

### Modifying the Environment
As a general rule, to add directories to your PATH or define additional environment variables, place those changes in .bash_profile (or the equivalent, according to your distribution; for example, Ubuntu uses .profile). For everything else, place the changes in .bashrc.

**Note:** Unless you are the system administrator and need to change the defaults for all users of the system, restrict your modifications to the files in your home directory. It is certainly possible to change the files in /etc such as profile, and in many cases it would be sensible to do so, but for now, let's play it safe.

Let's fire up nano and edit the .bashrc file. But before we do that, let's practice some “safe computing.” Whenever we edit an important configuration file, it is always a good idea to create a backup copy of the file first. This protects us in case we mess up the file while editing. To create a backup of the .bashrc file, do this:

{% highlight shell %}
$ cp .bashrc .bashrc.bak
{% endhighlight %}

The extensions “.bak”, “.sav”, “.old”, and “.orig” are all popular ways of indicating a backup file. Oh, and remember that cp will overwrite existing files silently.

Whenever you modify configuration files it's a good idea to add some comments to document your changes.
Shell scripts and bash startup files use a “#” symbol to begin a comment.


## 12 – A Gentle Introduction to `vi(m)`
**Putting this off until I need it**


## 13 – Customizing the Prompt
### Escape Codes Used in Shell Prompts

| Sequence | Value Displayed                                                                                                                                                                                                                   |
|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| \a       | ASCII bell. This makes the computer beep when it is encountered.                                                                                                                                                                  |
| \d       | Current date in day, month, date format. For example, “Mon May 26.”                                                                                                                                                               |
| \h       | Hostname of the local machine minus the trailing domain name.                                                                                                                                                                     |
| \H       | Full hostname.                                                                                                                                                                                                                    |
| \j       | Number of jobs running in the current shell session.                                                                                                                                                                              |
| \l       | Name of the current terminal device.                                                                                                                                                                                              |
| \n       | A newline character.                                                                                                                                                                                                              |
| \r       | A carriage return.                                                                                                                                                                                                                |
| \s       | Name of the shell program.                                                                                                                                                                                                        |
| \t       | Current time in 24-hour hours:minutes:seconds format.                                                                                                                                                                             |
| \T       | Current time in 12-hour format.                                                                                                                                                                                                   |
| \@       | Current time in 12-hour AM/PM format.                                                                                                                                                                                             |
| \A       | Current time in 24-hour hours:minutes format.                                                                                                                                                                                     |
| \u       | Username of the current user.                                                                                                                                                                                                     |
| \v       | Version number of the shell.                                                                                                                                                                                                      |
| \V       | Version and release numbers of the shell.                                                                                                                                                                                         |
| \w       | Name of the current working directory.                                                                                                                                                                                            |
| \W       | Last part of the current working directory name.                                                                                                                                                                                  |
| \!       | History number of the current command.                                                                                                                                                                                            |
| \#       | Number of commands entered during this shell session.                                                                                                                                                                             |
| \$       | This displays a “$” character unless we have superuser privileges. In that case, it displays a “#” instead.                                                                                                                       |
| \[       | Signals the start of a series of one or more non-printing characters. This is used to embed non-printing control characters that manipulate the terminal emulator in some way, such as moving the cursor or changing text colors. |
