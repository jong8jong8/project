# Git

### Git installation

```sh
sudo apt install git
```


### Github sign-in without passwords using `SSH`
- At Github, create a new repository in Github (e.g., `Test`)
- Copy the SSH file (e.g., `git@github.com:jong8jong8/Test.git`)
- At your local machine, create the same named directory and move to it

```sh
mkdir Test
cd Test
```

- Generate Key

```sh
ssh-keygen
```
