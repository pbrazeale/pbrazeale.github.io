## 4.3 Shebang
A ["shebang"](https://en.wikipedia.org/wiki/Shebang_\(Unix\)) is a special line at the top of a script that tells your shell which program to use to execute the file.

The format of a shebang is:

{% highlight shell %}
#! interpreter [optional-arg]
{% endhighlight %}

For example, if your script is a Python script and you want to use Python 3, your shebang might look like this:

{% highlight shell %}
#!/usr/bin/python3
{% endhighlight %}

This tells the system to use the Python 3 interpreter located at `/usr/bin/python3` to run the script.


## 4.4 Bourne Shell
To get hand-wavy about it, I want to explain the difference between the 3 shells you're likely to encounter:

- `sh`: The Bourne shell. This is the original Unix shell and is [POSIX-compliant](https://en.wikipedia.org/wiki/POSIX). It's very basic and doesn't have many quality-of-life features.
- `bash`: The Bourne Again shell. This is the most popular shell on Linux. It builds on `sh`, but also has a lot of extra features.
- `zsh`: The Z shell. This is the most popular shell on macOS. Like `bash`, it does what `sh` can do, but also has a lot of extra features.

Both `zsh` and `bash` are "sh-compatible" shells, meaning they can run `.sh` scripts, but they also have extra features that generally make them more pleasant to use. For your purposes, the differences between `zsh` and `bash` are not super significant. Everything we do in this course will work in both shells.

## 4.6 Environment Variables
You can view all of the environment variables that are currently set in your shell with the `env` command.

To set a variable in your shell, use the `export` command:

{% highlight shell %}
export NAME="Lane"
{% endhighlight %}

You can then use the variable in your shell, just as before:

{% highlight shell %}
echo $NAME
# Lane
{% endhighlight %}

The interesting part is that programs and scripts you run in your shell can _also_ use that variable:


## 4.7 PATH
**IMPORTANT**:
There are environment variables that are sort of "built-in" to your shell. By "built-in" I just mean that different programs and parts of your system know about them and use them. The `PATH` variable is one of those.

### PATH variables
Take a look at your current `PATH` variable:

{% highlight shell %}
echo $PATH
{% endhighlight %}

You should see a giant list of directories separated by colons (`:`). Each of those directories is a place where your shell will look for executables. For example, with a `PATH` like this:

{% highlight shell %}
/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin
{% endhighlight %}

Your shell will look for executables in the following directories:

- `/usr/local/bin`
- `/usr/bin`
- `/bin`
- `/usr/sbin`
- `/sbin`


## Change Your PATH
A common problem you'll run into in the future is that you install a new program on your machine, but when you try to run it from your terminal, you get an error like:

{% highlight shell %}
$ my-new-program
-bash: my-new-program: command not found
{% endhighlight %}

Nine times out of ten, it's because the program is installed in a directory that's not in your `PATH` variable. Oftentimes when you install a program using the CLI, it will print a message during the installation process that tells you where the command was installed. **Don't let your eyes glaze over when your terminal prints important messages!** Sometimes you just gotta [rtfm](https://www.dictionary.com/browse/rtfm).

To add a directory to your `PATH` without overwriting all of the existing directories, use the `export` command and reference the existing `PATH` variable:

{% highlight shell %}
export PATH="$PATH:/path/to/new"
{% endhighlight %}

The `$PATH` part is a reference to the existing `PATH` variable. The `:` separates the existing directories from the new directory (`/path/to/new`) that you're adding.
