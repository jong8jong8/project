# 인공지능 프로젝트

## 기본 지식

### 웹하드 
- [TeraBox](https://www.terabox.com/)

### HTML 기초
- [조코딩 HTML 기초 강좌 1강](https://www.youtube.com/watch?v=JMLBBv05ORw)
  - [생활코딩](https://opentutorials.org/course/1) 
- [조코딩 HTML 기초 강좌 2강](https://www.youtube.com/watch?v=LnGgndT308Q)
  - [Netlify](https://www.netlify.com/) 
  - [Free CSS](https://www.free-css.com/free-css-templates)
- [MDN HTML](https://developer.mozilla.org/ko/docs/Web/HTML)

### JavaScript 기초
- [생활코딩 JavaScript](https://opentutorials.org/course/743)
- [MDN JavaScript](https://developer.mozilla.org/ko/docs/Web/JavaScript)



## AI
- [생활코딩 머신러닝 이론편](https://opentutorials.org/course/4548)
  - [Google Teachable Machine](https://teachablemachine.withgoogle.com/) 
  - [세상에서 가장 쉬운 인공지능 만들기 1탄](https://www.youtube.com/watch?v=USQGTW34lO8) ([실습 예제 01](./example01.md))
  - [세상에서 가장 쉬운 인공지능 만들기 2탄](https://www.youtube.com/watch?v=9SwdGFzFb5Y) ([실습 예제 02](./example02.md))
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
