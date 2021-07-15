# Add a Key to the ssh-agent

Sometime you need to add a private key to she SSH Agent to authenticate, here's how you can do:
```shell
$ ssh-add -K ~/.ssh/id_rsa_whatever
Identity added: /Users/me/.ssh/id_rsa_whatever (/Users/me/.ssh/id_rsa_whatever)

$ ssh-add -l
4096 SHA256:QHOP+123abc /Users/me/.ssh/id_rsa_whatever (RSA)
```
