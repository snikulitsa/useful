# CREDENTIALS
#### SSH id_rsa.pub
Generate ssh key:..
```bash
ssh-keygen -t rsa -b 4096 -C "some.dude@gmail.com"
```
Set public ssh key to remote server for login without password:  
```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub RemoteUser@RemoteServer
```
