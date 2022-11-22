# [Git](https://git-scm.com/)

### Git installation

```sh
sudo apt install git
```


### Github sign-in without passwords using `SSH`

- [생활코딩 - 암호학 (Cryptography)](https://opentutorials.org/module/5250)
- [Github Docs - Connecting to GitHub with SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)
- Check the two files exist (`id_ed25519` and `id_ed25519.pub`)

```sh
cd ~/.ssh        
ls -al
cat id_ed25519      # private key
cat id_ed25519.pub  # public key 
```

- Copy the contents for Github setting
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


### Github Page Setting
- [생활코딩 - 웹호스팅 github pages (2022년 수정판)](https://opentutorials.org/course/3084/18891)
