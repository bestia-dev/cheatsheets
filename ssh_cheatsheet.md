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
Get-Process ssh-agent
ssh-add -l
ssh-add -t 1h $home\.ssh\localhost_2201_rustdevuser_ssh_1
# or make a powershell script ~\.ssh\sshadd.ps1 and alias it
New-Alias sshadd $home\.ssh\sshadd.ps1
```

Create powershell script ~\.ssh\sshadd.ps1
 
```ps1
echo Add ssh key identity to ssh-agent.
ssh-add -t 1h $home\.ssh\localhost_2201_rustdevuser_ssh_1
ssh-add -l
```

Recreate the alias on every startup ~\Documents\PowerShell\Microsoft.PowerShell_profile.ps1:

```ps1
# $home\Documents\PowerShell\PowerShell_profile.ps1 should run on every startup

echo "Use sshadd to add often used ssh identities to the ssh-agent from $home\.ssh\sshadd.ps1."

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

## Different file formats for the same keys

Key generated with ssh-keygen by default makes 2 files:  
`~/.ssh/github_com_git_ssh_1` and 
`~/.ssh/github_com_git_ssh_1.pub`

It look that Openssl does not like these formats.  
The same keys must be converted just into another PEM format.

Convert the private key  
Warning: It will replace the same file ! SO make the copy first.

```bash
cp ~/.ssh/github_com_git_ssh_1 ~/.ssh/github_com_git_ssh_1.priv
ssh-keygen -p -m PEM -f ~/.ssh/github_com_git_ssh_1
cp ~/.ssh/github_com_git_ssh_1 ~/.ssh/github_com_git_ssh_1.priv.pem
mv ~/.ssh/github_com_git_ssh_1.priv ~/.ssh/github_com_git_ssh_1
```

Convert the public key

```bash
ssh-keygen -e -m PEM -f ~/.ssh/github_com_git_ssh_1.pub  > ~/.ssh/github_com_git_ssh_1.pub.pem
bash

