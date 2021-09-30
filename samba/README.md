# SAMBA

Comando CHMOD alterar permissões
RWX = 421 = 7 | Ex R-X = 5
Possui 3 numeros 777 permissao total, Proprietario, Grupo e Outros

Mudar permissão diretório
sudo chmod 777 pasta/ -R

Mudar permissão de arquivo
sudo chmod 777 nomedoarquivo.txt

Trocar proprietario diretorio
sudo chown nomeusuario pasta/ -R

Trocar proprietario de arquivo
sudo chown nomeusuario nomearquivo.txt

Trocar o grupo diretorio
sudo chgrp nomegrupo pasta/ -R

Trocar o grupo do arquivo
sudo chgrp nomegrupo nomearquivo.txt

Adicionar usuario

sudo adduser nomeusuario

Apagar usuario

sudo userdel nomeusuario

Redefinir senha

sudo passwd nomeusuario

Adicionar grupo
sudo addgroup nomegrupo

Apagar grupo
sudo delgroup nomegrupo

Adicionar usuario no grupo
sudo adduser nomeusuario nomegrupo

Remover usuario do grupo
sudo deluser nomeusuario nomegrupo

Ver todos os grupos
cat /etc/group

Ver apenas a linha do grupo que eu criei
grep nomegrupo /etc/group

Ver todos os usuarios
cat /etc/passwd

Ver apenas a linha do usuario
grep nomeusuario /etc/passwd

Adicionar usuario ao samba
smbpasswd -a nomeusuario


espaço no HD
df -h

tamanho da pasta
$ du -hs (nome do arquivo)
