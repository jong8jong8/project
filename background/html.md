# [HTML / CSS / DOM / JavaScript](https://developer.mozilla.org/ko/)
- [Local Server](https://github.com/processing/p5.js/wiki/Local-server)
- [Document Object Model](https://en.wikipedia.org/wiki/Document_Object_Model)
- [생활코딩 - WEB1 - HTML & Internet](https://opentutorials.org/course/3084) 
- [생활코딩 - WEB2 -  CSS](https://opentutorials.org/course/3086)
- [생활코딩 - WEB2 - JavaScript](https://opentutorials.org/course/3085)



---


- `index.html`

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>HTML 연습</title>
    <style>
        h1 {
            color: blue;
        }
    </style>
</head>
<body>
    <h1>The title of this page</h1>
    <p>This is a paragraph.</p>
    <canvas id="canvas" width="400" height="300"></canvas>
    <script>
        const canvas = document.getElementById("canvas");
        const ctx = canvas.getContext("2d");
        ctx.fillStyle = "green";
        ctx.fillRect(10, 10, 150, 100);
    </script>
</body>
</html>
```
