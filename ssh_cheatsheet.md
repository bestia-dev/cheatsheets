# ssh cheatsheet

It is annoying to type the passcode eveytime we use ssh.  
Fortunately there is ssh-agent to the rescue. 

## Read my SSH easy

<https://github.com/bestia-dev/docker_rust_development/blob/main/ssh_easy.md>

## ssh-add and ssh-agent

In Linux bash:

```bash
# check if it is running
ps -F -C ssh-agent
```

Ssh-agent even works in Windows Powershell:

```powershell
# Get-Process ssh-agent
ssh-add -l
ssh-add -t 1h $home\.ssh\rustdevuser_key
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

