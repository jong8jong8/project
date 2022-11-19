# Git

### Git installation

```sh
sudo apt install git
```


### Github sign-in without passwords using `SSH`
- Generate Key

```sh
ssh-keygen
```

- Check the two files exist (`id_rsa` and `id_rsa.pub`)

```sh
cd ~/.ssh
ls -al
```



--- 

- At Github, create a new repository in Github (e.g., `Test`)
- Copy the SSH file (e.g., `git@github.com:jong8jong8/Test.git`)
- At your local machine, create the same named directory and move to it

```sh
mkdir Test
cd Test
```


