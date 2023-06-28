# GNU Screen Cheat Sheet

https://www.gnu.org/software/screen/manual/screen.html#toc-Commands-1  

## Starting GNU screen sessions

| command | description |
| ----------- | ----------- |
|screen –S name        | create a named session  |
|screen –r             | list of detached sessions  |
|screen –r pid_or_name | attach detached screen session  |

## Inside a session

Inside a session, the command begins with "ctrl-a" or "c-a", and is followed by one other character.  
WARNING: the second character is very case-sensitive.   

| command | description |
| ----------- | ----------- |
|c-a d   | detach session  |

## Multiple split regions

One session can have multiple windows (shells) that can be displayed in split regions.  

| command | description |
| ----------- | ----------- |
|c-a \|     | create vertical split  |
|c-a TAB   | switch between regions  |
|c-a c     | new bash shell window in empty region  |
|c-a "     | choose a window for this region  |
|c-a k     | kill window (shell)  |
|c-a X     | remove active region  |

## Scroll and copy mode

| command | description |
| ----------- | ----------- |
|C-a ESC    |  Enter copy/scrollback mode  |
|arrows     |  Move cursor around  |
|SPACE      |  First marker  |
|ENTER      |  Second marker and copy into buffer  |
|c-a ]      | paste from buffer  |

## Configuration

nano  ~/.screenrc  

#This line makes Detach without losing the regions/windows layout  
layout save default  

#status bar with information  
hardstatus on  
hardstatus alwayslastline  
hardstatus string "%S - %Y-%m-%d %C:%s"  

#Enable selecting split regions with mouse clicks  
defmousetrack on  
mousetrack on  
