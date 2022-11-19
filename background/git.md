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
cat id_rsa      # private key
cat id_rsa.pub  # public key 
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


