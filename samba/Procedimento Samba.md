# Procedimento para resetar senha de acesso ao servidor

Redefinir senha
```
sudo passwd nomeusuario
```

Redefinir senha samba
```
sudo smbpasswd -a nomeusuario
```
Restart samba
```
sudo service smbd restart
```
