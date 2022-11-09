# 인공지능 프로젝트

## AI
- [생활코딩 머신러닝 이론편](https://opentutorials.org/course/4548)
  - [Google Teachable Machine](https://teachablemachine.withgoogle.com/) ([Github Community](https://github.com/googlecreativelab/teachablemachine-community))
  - [세상에서 가장 쉬운 인공지능 만들기 1탄](https://www.youtube.com/watch?v=USQGTW34lO8) 
  - [세상에서 가장 쉬운 인공지능 만들기 2탄](https://www.youtube.com/watch?v=9SwdGFzFb5Y) ([Github](https://github.com/youtube-jocoding/Teachable-Machine-AI-Fitness-Trainer))
  - [The Awesome Teachable Machine List](https://github.com/SashiDo/awesome-teachable-machine)
- [생활코딩 머신러닝 실습편 with 파이썬 텐서플로](https://elibrary.kyobobook.co.kr/dig/elb/elibrary)
  - [Google TensorFlow](https://www.tensorflow.org/)
  - [Tensorflow 101](https://opentutorials.org/module/4966) ([예제 코드](https://github.com/blackdew/tensorflow1))
  - [Tensorflow 102](https://opentutorials.org/module/5268) ([에제 코드](https://github.com/blackdew/ml-tensorflow))

## Ubuntu
### Open terminal
`Ctrl` + `Alt` + `T`

### Install Brave in Linux
```
sudo apt install apt-transport-https curl;
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
convert label:"$(tree)"  directory_image.png
```
