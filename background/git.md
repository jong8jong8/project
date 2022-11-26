# [Git](https://git-scm.com/)

### Git installation

```sh
sudo apt install git
```

- [생활코딩 - GIT1](https://opentutorials.org/course/3837)

### Github sign-in without passwords using `SSH`

- [생활코딩 - 암호학 (Cryptography)](https://opentutorials.org/module/5250)
- [Github Docs - Connecting to GitHub with SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)
- Check the two files exist (`id_ed25519` and `id_ed25519.pub`)

```sh
cd ~/
ssh-keygen -t ed25519 -C "your_email@example.com"
cd ~/.ssh
ls -al
cat id_ed25519      # private key
cat id_ed25519.pub  # public key 
```

- Copy the contents of `id_ed25519.pub` for Github setting
- At Github, go to `SSH and GPG keys` and add the public key



### Sync a Github repository with my local directory

- At Github, create a new repository in Github (e.g., `Test`)
- Copy the `SSH` file (e.g., `git@github.com:jong8jong8/Test.git`)
- At your local machine, go to a directory under which `Test` will be cloned

```sh
cd ~/  # go to my home directory
git clone git@github.com:jong8jong8/Test.git Test
```

### Push the work done at my local machine to Github

- Create `index.html` at the directory `Test`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Greetings!</title>
</head>
<body>
    <p>Hello Github.</p>
</body>
</html>
```
- Push to Github

```sh
git add index.html
git commit -m "index.html is created"
git push
```
- Check at Github


### Github to [Netlify](https://www.netlify.com/)
- [생활코딩 - netlify.com 으로 웹호스팅 하기](https://www.youtube.com/watch?v=3FRv6Vga698&ab_channel=%EC%83%9D%ED%99%9C%EC%BD%94%EB%94%A9)
