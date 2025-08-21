# SSH Connection 

Created SSH directory if not present:
mkdir -p ~/.ssh
Ensured proper permissions:
icacls "$env:USERPROFILE\.ssh" /grant "$env:USERNAME:F" /t
or,

attrib -r "$env:USERPROFILE\.ssh\*" /s
attrib A built-in Windows command that changes file/folder attributes

-r Removes the Read-only attribute

$env:USERPROFILE points to C:\Users\aanis

/s applies to subfolders/files too

Generate SSH Keys (if not already existing)
ssh-keygen -t ed25519 -C "your_email@example.com"
~/.ssh/id_ed25519 ← private key (keep this secret!)

~/.ssh/id_ed25519.pub ← public key (share this with GitHub, GitLab, etc.)

Created SSH Config File
notepad.exe C:\Users\aanis\.ssh\config.txt
Rename the .txt into conifg file :

Rename-Item "$env:USERPROFILE\.ssh\config.txt" "config"
In the config file :
Host gitlab.com
  HostName altssh.gitlab.com
  User git
  Port 443
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/id_ed25519

Host github.com
  HostName ssh.github.com
  User git
  Port 443
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/id_ed25519
- Verified SSH Connection
ssh -T git@gitlab.com
Welcome to GitLab, @1Z4t-R3p0!
ssh -T git@github.com
Hi 1Z4t-R3p0! You've successfully authenticated, but GitHub does not provide shell access.