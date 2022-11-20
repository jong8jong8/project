# [Ubuntu](https://ubuntu.com/)

### Open terminal

`Ctrl` + `Alt` + `T`

### Install Brave in Linux

```
sudo apt install apt-transport-https curl
```

```
sudo curl -fsSLo /usr/share/keyrings/brave-browser-archive-keyring.gpg https://brave-browser-apt-release.s3.brave.com/brave-browser-archive-keyring.gpg
```

```
echo "deb [signed-by=/usr/share/keyrings/brave-browser-archive-keyring.gpg arch=amd64] https://brave-browser-apt-release.s3.brave.com/ stable main"|sudo tee /etc/apt/sources.list.d/brave-browser-release.list
```

```
sudo apt update
```

```
sudo apt install brave-browser
```

### Install VScode in Linux

``` 
sudo apt install snapd 
```

```
sudo snap install code --classic
```



### Remove VScode in Linux

```
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

### [How to install Python 3.11 on Ubuntu 22.04 LTS](https://www.the-analytics.club/python-3-11-ubuntu)
- [노마드 코더 - 아직도 파이썬을 이렇게 쓰고 있다구?](https://youtu.be/fJeGAx27-vU) 
