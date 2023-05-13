# [Ubuntu](https://ubuntu.com/)

### Open terminal

`Ctrl` + `Alt` + `T`

### Install Brave in Linux

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

### Install VScode in Linux

```sh 
sudo apt install snapd 
```

```sh
sudo snap install code --classic
```



### Remove VScode in Linux

```sh
sudo snap remove code
```

### How to save console output to an image

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


### A Matrix Movie Screen Saver in a Terminal 

```sh
sudo apt install cmatrix
```

```sh
cmatrix -s
```

### Nvidia driver

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

### Python 3.11 upgrade

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


### How to install Microsoft Edge to use New Bing
- You need MS Account.

```sh
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg

sudo install -o root -g root -m 644 microsoft.gpg /etc/apt/trusted.gpg.d/

```
