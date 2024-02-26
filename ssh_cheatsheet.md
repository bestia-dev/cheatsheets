# ssh cheatsheet

It is annoying to type the passcode eveytime we use ssh.  
Fortunately there is ssh-agent to the rescue. 

## Read my SSH easy

<https://github.com/bestia-dev/docker_rust_development/blob/main/ssh_easy.md>

## Linux bash

```bash
# check if it is running
ps -F -C ssh-agent
```

## Windows Powershell

```powershell
# Get-Process ssh-agent
ssh-add -l
ssh-add -t 1h $home\.ssh\rustdevuser_key
# or make a powershell script ~\.ssh\sshadd.ps1 and alias it
New-Alias sshadd $home\.ssh\sshadd.ps1
```

Create powershell script ~\.ssh\sshadd.ps1
 
```ps1
echo Add ssh key identity to ssh-agent.
ssh-add -t 1h $home\.ssh\rustdevuser_key
ssh-add -l
```

Recreate the alias on every startup ~\profile.ps1:

```ps1
# $home\profile.ps1 should run on every startup
echo "Use sshadd to add ssh identity to the ssh-agent."

New-Alias sshadd $home\.ssh\sshadd.ps1
```

## Server fingerprints in ~/.ssh/known_hosts

Remove old fingerprints for a server and add new ones. No duplicates.

```bash
ssh-keygen -R bestia.dev
ssh-keyscan -H bestia.dev >> ~/.ssh/known_hosts
ssh-keygen -R github.com
ssh-keyscan -H github.com >> ~/.ssh/known_hosts
cat ~/.ssh/known_hosts
```

