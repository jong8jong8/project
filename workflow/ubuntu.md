# [Ubuntu](https://ubuntu.com/)
- [Open terminal](#Open-terminal)
- [Install Google Chrome in Linux](#Install-Google-Chrome-in-Linux)
- [Install Brave in Linux](#Install-Brave-in-Linux)
- [Install Microsoft Edge in Linux](#Instal-Microsoft-Edge-in-Linux)
- [Install VScode in Linux](#Install-VScode-in-Linux)
- [Remove VScode in Linux](#Remove-VScode-in-Linux)
- [How to save console output to an image](#How-to-save-console-output-to-an-image)
- [Nvidia driver](#Nvidia-driver)
- [Python 3.11 upgrade](#python-upgrade)
- [Upgrade Google Chrome in Linux](#Upgrade-Google-Chrome-in-Linux)
- [Upgrade Brave in Linux](#Upgrade-Brave-in-Linux)

----


### <a name="Open-terminal">Open terminal</a>

`Ctrl` + `Alt` + `T`

### <a name="Install-Google-Chrome-in-Linux">Install Google Chrome in Linux</a>

```sh
sudo apt update
```

```sh
sudo apt install wget
```

```sh
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
```

```sh
sudo dpkg -i google-chrome-stable_current_amd64.deb
```

```sh
google-chrome
```

### <a name="Install-Brave-in-Linux">Install Brave in Linux</a>

```sh
sudo apt install apt-transport-https curl
```

```sh
sudo curl -fsSLo /usr/share/keyrings/brave-browser-archive-keyring.gpg https://brave-browser-apt-release.s3.brave.com/brave-browser-archive-keyring.gpg
```

```sh
echo "deb [signed-by=/usr/share/keyrings/brave-browser-archive-keyring.gpg arch=amd64] https://brave-browser-apt-release.s3.brave.com/ stable main"|sudo tee /etc/apt/sources.list.d/brave-browser-release.list
```

```sh
sudo apt update
```

```sh
sudo apt install brave-browser
```

### <a name="Install-Microsoft-Edge-in-Linux">Install Microsoft Edge in Linux</a>
- You need a MS Account.

```sh
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo mv microsoft.gpg /etc/apt/trusted.gpg.d/microsoft.gpg
```

```sh
echo "deb [arch=amd64] https://packages.microsoft.com/repos/edge stable main" | sudo tee /etc/apt/sources.list.d/microsoft-edge-dev.list
```

```sh
sudo apt update
```

```sh
sudo apt install microsoft-edge-dev
```

```sh
microsoft-edge
```

```sh
sudo apt remove microsoft-edge-stable
```

### <a name="Install-VScode-in-Linux">Install VScode in Linux</a>

```sh 
sudo apt install snapd 
```

```sh
sudo snap install code --classic
```



### <a name="Remove-VScode-in-Linux">Remove VScode in Linux</a>

```sh
sudo snap remove code
```

### <a name="How-to-save-console-output-to-an-image">How to save console output to an image</a>

- Install **ImageMagick**

```sh
sudo apt install imagemagick
```

- Save to a PNG image (e.g., `tree`)

```sh
sudo apt install tree
```

```sh
convert label:"$(tree)"  directory_image.png
```


### <a name="Nvidia-driver">Nvidia driver</a>

```sh
sudo lshw -c display # check display 
```

```sh
sudo apt install ubuntu-drivers-common 
```

```sh
sudo ubuntu-drivers devices
```

```sh
sudo ubuntu-drivers autoinstall
```

```sh
sudo reboot
```

### <a name="python-upgrade">Python 3.11 upgrade</a>

```sh
sudo apt search python3.11
```

```sh
sudo apt install python3.11
```

```sh
cd ~/           # move to home directory
ls .bashrc      # check .bashrc file
code .bashrc    # open with vscode
```

```sh
# In vscode, add the following at the end of the .bashrc file 
alias python=python3.11
```

```sh
source .bashrc             # apply the modified .bashrc 
python --version           # check the python version is 3.11 
python                     # use python instead of python3.11
```

### <a name="Upgrade-Google-Chrome-in-Linux">Upgrade Google Chrome in Linux</a>
```sh
sudo apt-get update
```

```sh
wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
sudo sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list'
```

```sh
sudo apt-get --only-upgrade install google-chrome-stable
```

### <a name="Upgrade-Brave-in-Linux">Upgrade Brave in Linux</a>
```sh
sudo apt install curl
```

```sh
sudo curl -fsSLo /usr/share/keyrings/brave-browser-archive-keyring.gpg https://brave-browser-apt-release.s3.brave.com/brave-browser-archive-keyring.gpg
```

```sh
echo "deb [signed-by=/usr/share/keyrings/brave-browser-archive-keyring.gpg] https://brave-browser-apt-release.s3.brave.com/ stable main"|sudo tee /etc/apt/sources.list.d/brave-browser-release.list
```

```sh
sudo apt update
```

```sh
sudo apt install brave-browser
```
