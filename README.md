# multiple-git-ssh-key

setup multiple git ssh key

## create rsa

```
ssh-keygen -t rsa -C "11****763@qq.com" -f ~/.ssh/id_rsa_git
```

```
ssh-keygen -t rsa -C "zy@400******28.com" -f ~/.ssh/id_rsa
```

[github](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

## add public key to github

[github](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)

## add private key

```
$ ssh-add ~/.ssh/id_rsa
$ ssh-add ~/.ssh/id_rsa_git
```

list private key

```
ssh-add -l
```

## ssh config

```
vim ~/.ssh/config
```

add config content

```
# Personal Account configuration

Host github.com
  HostName github.com
  User Minu*******sal
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/id_rsa_git


# Work Account Configuration

Host git.400*****28.com
  HostName git.400******28.com
  User zy
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/id_rsa
  KexAlgorithms +diffie-hellman-group1-sha1
  HostKeyAlgorithms ssh-rsa
  PubkeyAcceptedKeyTypes ssh-rsa
```

## test

```
ssh -T git@github.com
```

```
ssh -T git@git.400******28.com
```

## view finger print

md5

```
ssh-keygen -E md5 -lf ~/.ssh/id_rsa_git
```

sha 256

```
ssh-keygen -E md5 -lf ./id_rsa
```

## Unable to negotiate with xx.xx.xx.xx port 22: no matching key exchange method found.

Their offer:diffie-hellman-group1-sha1

add follow setting in ~/.ssh config file
```
Host xxx.xxx.xxx.xxx
   KexAlgorithms +diffie-hellman-group1-sha1
```
## Use user1's SSH key for pushing
```ssh
GIT_SSH_COMMAND="ssh -i ~/.ssh/id_rsa_user1" git push origin main
```

## Use user2's SSH key for pushing
```ssh
GIT_SSH_COMMAND="ssh -i ~/.ssh/id_rsa_user2" git push origin main
```
