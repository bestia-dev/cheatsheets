# Terminal shortcuts

## Bestia changes to Wezterm terminal Shortcuts

I would like to use the terminal with the shortcuts I learned in VSCode. The terminal is so old, that some shortcuts are crazy. What I changed for my opinionated workflow:

- ctrl+c - Copy (like in VSCode)
- ctrl+v - Paste (like in VSCode)
- ctrl+q - Kill the current process (instead of ctrl+c)

code /c/Users/Luciano/.config/wezterm/wezterm.lua

```lua
config.keys = {
    -- The original shortcut ctrl+v: Input the next character literally.
    -- The original shortcut works badly with the Windows Clipboard Manager Win+v.
    -- New meaning ctrl+v: Paste from clipboard (just like in VSCode)
    -- Instead of old Ctrl + Shift + V or Shift + Insert or right-click
    { key = 'v', mods = 'CTRL', action = wezterm.action({ PasteFrom = "Clipboard" }) },

    -- The original shortcut ctrl+c: Kill the current process.
    -- New meaning ctrl+c: Copy to clipboard (just like in VSCode)
    { key = 'c', mods = 'CTRL', action = wezterm.action.CopyTo('ClipboardAndPrimarySelection') },
    
    -- The original shortcut ctrl+q: Resume terminal output after freezing.
    -- New meaning ctrl+q: Kill the current process (instead of ctrl+c).
    { key = 'q', mods = 'CTRL', action = wezterm.action.SendKey{ key='c', mods='CTRL' } },
    
    -- The original shortcut ctrl+s: Freeze the terminal output.
    -- It is now unusable. I don't use it and have changed the shortcut of ctrl+q Resume terminal output
    -- New meaning: nothing
    { key = 's', mods = 'CTRL', action = wezterm.action.DisableDefaultAssignment, },
    
    -- The original shortcut ctrl+z: Suspend the current process.
    -- I don't use it and it is used in VSCode as Undo. Potential confusion.
    -- New meaning: nothing
    { key = 'z', mods = 'CTRL', action = wezterm.action.DisableDefaultAssignment, },

    -- Remove a word to the left is useful. The terminal uses ctrl+w, but VSCode uses ctrl+backspace.
    -- New meaning ctrl+backspace: Remove word 
    { key = 'Backspace', mods = 'CTRL', action = wezterm.action.SendKey {key = 'w', mods = 'CTRL'} },
    
}
```

## Terminal Navigation Shortcuts

Ctrl + A – Move cursor to the beginning of the line.  
Ctrl + E – Move cursor to the end of the line.  
Ctrl + U – Cut everything from the cursor to the beginning of the line.  
Ctrl + K – Cut everything from the cursor to the end of the line.  
Ctrl + W – Delete the word before the cursor.  
Alt + B – Move cursor backward by one word.  
Alt + F – Move cursor forward by one word.  
Ctrl + Y – Paste the last cut text.  

## Command History Shortcuts

Ctrl + R – Reverse search in command history.  
Ctrl + G – Exit from history searching mode.  

## Process Management Shortcuts

Ctrl + Z – Suspend the current process.  
Ctrl + C – Kill the current process.  
Ctrl + D – Logout or end the terminal session.  
jobs – List all running jobs in the background.  
fg – Bring a background job to the foreground.  
bg – Resume a suspended job in the background.  

## Text Editing Shortcuts

Ctrl + Left/Right Arrow – Move left or right by one word in the line.  
Ctrl + Backspace – Delete the previous word.  
Ctrl + Shift + C – Copy selected text in the terminal.  
Ctrl + Shift + V – Paste text into the terminal.  
Shift + Insert – Paste text (alternative for Ctrl + Shift + V).  

## Miscellaneous

Ctrl + S – Freeze the terminal output.  
Ctrl + Q – Resume terminal output after freezing.  
Ctrl + T – Swap the last two characters before the cursor.  
Ctrl + X, Ctrl + E – Open the current command in the default editor for easier editing.  
