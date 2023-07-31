# Zellij

Zellij is a terminal multiplexer and I will use it instead of "gnu screen".
Zellij does not need a GUI (graphical use interface), because it works inside a text terminal.
Zellij uses NerdFonts to make it look pretty.

## Installation

I like to put my "personal" executables in ~/bin. So I can see what specific binaries I use over time.
If ~/bin does not exist, create the folder and add it to PATH into ~.bashrc and actual bash.

```bash
mkdir ~/bin
# check if path already exist?
echo $PATH
# run also inside the terminal without resetting bash
export PATH="$HOME/bin:$PATH"
# check if it is ok
echo $PATH
```
		
Append this line into ~/.bashrc, so it will be there after bash restarts:
```bash
nano ~/.bashrc
# appended by x on date xxx
export PATH="$HOME/bin:$PATH"
```

Download the latest release from GitHub, decompress it and make it executable.

```bash
curl -L https://github.com/zellij-org/zellij/releases/download/v0.37.2/zellij-x86_64-unknown-linux-musl.tar.gz --output /tmp/zellij-x86_64-unknown-linux-musl.tar.gz
tar -xzv -C ~/bin -f /tmp/zellij-x86_64-unknown-linux-musl.tar.gz 
rm /tmp/zellij-x86_64-unknown-linux-musl.tar.gz
chmod +x ~/bin/zellij
```
