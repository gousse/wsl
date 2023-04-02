# About

Memo for my WSL setup on Windows 11 with Ubuntu

# dependencies

* git : https://git-scm.com/download/win

* font: https://github.com/powerline/fonts/tree/master/DejaVuSansMono

* vscode: https://code.visualstudio.com/download

  



# wsl install

https://learn.microsoft.com/en-us/windows/wsl/install

```powershell
wsl --install
```

## git config
```bash
git config --global user.name "Your Name"
git config --global user.email "youremail@domain.com"
git config --global credential.helper "/mnt/c/Program\ Files/Git/mingw64/bin/git-credential-manager.exe"
```

## install docker-ce

note : ca-certificates curl gnupg lsb-release are allready installed in Ubuntu 22.04

```bash
sudo apt install apt-transport-https
```

add repo

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null  
```

add gpg key

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg 
```



install docker-ce

```bash
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io 
```



test manual start

```bash
sudo service docker start
```



add  group docker to user

```bash
sudo usermod -a -G docker user
```

logoff and logon



## install oh-my-bash

```bash
bash -c "$(curl -fsSL https://raw.githubusercontent.com/ohmybash/oh-my-bash/master/tools/install.sh)"
```



edit ~/.bashrc   and choose your theme, completion and plugins

```bash
OSH_THEME="powerline"
[...]
completion=(
  git
  kubectl
)
[...]
plugins=(
  git
  bashmarks
  kubectl
)
```



activate it in actual shell after modif

```bash
source ~/.bashrc
```



## choose your default editor

```bash
sudo update-alternatives --config editor
```



## install dnsdist

```bash
sudo apt install dnsdist
```



## allow sudo for some services that need it

```bash
sudo visudo
```

add the lines you need

```
%sudo   ALL=(ALL) NOPASSWD: /usr/sbin/service dnsdist *
%sudo   ALL=(ALL) NOPASSWD: /usr/sbin/service docker *
```

(allow sudo service docker without password to allow starting by default)



## autostart services

in Windows 11 WSL2

create/edit /etc/wsl.conf

```bash
[boot]
command = "sudo service docker start"
command = "sudo service dnsdist start"
```



## vscode extensions

wsl

docker

gitlens