# AI Project

## Bookmark
- [Github Markdown](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
- [Ubuntu tutorial](./ubuntu_tutorial.md)
- [Netlify](https://www.netlify.com/)
- [TeraBox](https://www.terabox.com/)
- [생활코딩](https://opentutorials.org/course/1)
- [Teachable Machine](https://teachablemachine.withgoogle.com/)
- [TensorFlow.js](https://www.tensorflow.org/js/)
- [p5.js](https://p5js.org/)
- [ml5.js](https://ml5js.org/)

## How to sync my Github repository with Netlify

- Get Github token and save it to a `mypass.txt` file
- Create a Github repository (e.g., netlify)
- Execute the following shell commands from your local linux machine

```sh
echo "# netlify" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/jong8jong8/netlify.git
git push -u origin main
```

- Create `index.html`

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Getting Started with ml5.js</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <!-- p5 -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.0.0/p5.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.0.0/addons/p5.sound.min.js"></script>
    <!-- ml5 -->
    <script src="https://unpkg.com/ml5@latest/dist/ml5.min.js"></script>
  </head>

  <body>
    <script>
      // Your code will go here
      // open up your console - if everything loaded properly you should see the latest ml5 version
      console.log('ml5 version:', ml5.version);

      function setup() {
        createCanvas(400, 400);
      }

      function draw() {
        background(200);
      }
    </script>
  </body>
</html>
```
- Push to Github

```sh
git add .
git commit -m “index.html is created”
git push
```

- Sync in Netlify

## AI Practice
- [ ] Object Classification

