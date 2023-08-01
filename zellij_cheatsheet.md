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

Download the latest release from GitHub, unpack it and make it executable.  

```bash
curl -L https://github.com/zellij-org/zellij/releases/download/v0.37.2/zellij-x86_64-unknown-linux-musl.tar.gz --output /tmp/zellij-x86_64-unknown-linux-musl.tar.gz
tar -xzv -C ~/bin -f /tmp/zellij-x86_64-unknown-linux-musl.tar.gz 
rm /tmp/zellij-x86_64-unknown-linux-musl.tar.gz
chmod +x ~/bin/zellij
```

# Run a new named session with layout

```bash
zellij --layout ~/.config/zellij/layouts/layout_web_server.kdl --session web_server
```

Layout specific for my web-server:

```kdl
// layout_web_server.kdl for my Google VM
// 5 tabs for different webapps and utils

layout {
	default_tab_template {
        pane size=1 borderless=true {
            plugin location="zellij:tab-bar"
        }
        children
        pane size=2 borderless=true {
            plugin location="zellij:status-bar"
        }
    }
	tab name="mem6_8086"{	
		pane{
			cwd "/var/www/webapps/mem6_game"		
			command "sudo"
			args "./mem6_server" "127.0.0.1" "8086"
		}
	}
	tab name="cargo_crev_web_8051" {
		pane{
			cwd "/var/www/webapps/cargo_crev_web"		
			command "./cargo_crev_web"
		}
	}
	tab name="cargo_crev_web_git"{	
		pane{
			cwd "$HOME"		
			command "foreground_scheduler"
			args "25" "cargo-crev" "crev repo fetch trusted"
		}
	}
	tab name="cargo_crev_web_admin" {
		pane{
			cwd "$HOME"	
			command "bash"			
			args "-ci" "cargo_crev_web_admin list_new_repos ; history -s cargo_crev_web_admin list_new_repos ; exec bash ;"
		}
	}
	tab name="podman_hit_counter" {
		pane{
			cwd "/var/www/transfer_folder/webpage_hit_counter"
			command "bash"
			args "-ci" "sh webpage_hit_counter_pod_create.sh ; podman logs webpage_hit_counter_cnt ; history -s podman logs webpage_hit_counter_cnt ; exec bash ;"
		}
	}
}
```

When Zellij layouts opens a pane with a "command", then only this command will execute, not the interactive bash. This is ok for most purposes.  
That command can be closed with ctrl-c then we can use ENTER to re-run it. But only this one command that is configured for that pane.  
If I need an interactive bash, than I will use a sequence of commands finishing with `exec bash`.  

## Detach and attach

Inside Zellij use ctrl-o and alt-d to DETACH. All the tabs and panes will continue running in the background. Great !  
To list open sessions and then attach use:  

```bash
zellij ls

zellij attach web_server
```
