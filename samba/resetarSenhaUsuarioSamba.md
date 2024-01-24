# Resetar Senha Usuário Samba

1. Reset a senha do usuário no linux
```
sudo passwd user
```
2. Reset a senha do usuário no samba
```
sudo smbpasswd -a user
```
3. Restart o serviço do samba
```
sudo service smbd restart
```
Se quiser ver em quais pastas o usuário tem permissão de acesso
```
grep user /etc/group
```
