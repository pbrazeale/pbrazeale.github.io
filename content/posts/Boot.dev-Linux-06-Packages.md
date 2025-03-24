## 6.4 Webi
There is one more package manager (actually more of an anti-package manager) I want to introduce you to: [Webi](https://webinstall.dev/).

Webi lets you install command line tools directly from the web, with no need for a local command line tool like `apt` or `brew`. You don't need to install webi itself at all, instead, you just run a shell command that downloads and runs the tool's official installer script.
### Assignment
Let's install [lsd](https://github.com/lsd-rs/lsd), a more modern version of the `ls` command. It's essentially `ls` with a bunch of extra features.

***Note**: If you're using WSL (Windows Subsystem for Linux), you should follow the Linux instructions.*

1. [ ] Go to [Webi](https://webinstall.dev/) and look for the `lsd (LSDeluxe)` entry. Navigate to [its page](https://webinstall.dev/lsd/) and select the correct instructions to install it on your system (Linux/WSL or macOS). You should simply need to copy/paste and run a single command in your terminal.
2. [ ] Make sure `lsd` works by listing all the files in the `worldbanc/private/transactions` directory.
3. [ ] Try running `lsd` with the `--tree` flag on the `worldbanc/private` directory. One of the coolest features of `lsd` is that you can view your files in a tree-like structure.
4. [ ] Run it again with both `--tree` _and_ `--classic` flags on the `worldbanc/private/transactions` directory. _Paste the output into the input field and submit it._
_Optional Icons_: You must install [the nerdfont](https://webinstall.dev/nerdfont/) and update the font in your terminal's settings for `lsd` to show icons. Note that if you are using WSL, you will need to follow the specific installation instructions to download and configure Windows Terminal.
### Note on Security
As a general rule, it's not smart to pipe a shell script from the internet directly into your terminal, because that script could do malicious things. That said, as long as you're doing it via HTTPS (which you are), and you trust the source (in this case webinstall.dev), it's not as big of a concern. If you want to hear more about it, here's the [section of the Backend Banter podcast](https://youtu.be/zSkDandxcQ0?t=1447) episode where the creator talks about it more in detail.
