# Habilitar Sendmail

## Estas instruções servem para usar o gmail (ou qualquer outro servidor de SMTP) para fazer a função mail() do PHP funcionar em localhost

Instale o pacote

```
sudo apt-get install ssmtp
```

Edite o arquivo /etc/ssmtp/ssmtp.conf, comente a linha com mailhub e adicione as linhas abaixo. Não esqueça de trocar as marcações pelos seus dados de acesso

```
sudo vim /etc/ssmtp/ssmtp.conf
```
```
mailhub=smtp.gmail.com:587
UseSTARTTLS=YES
AuthUser=<YOUR-EMAIL>@gmail.com
AuthPass=<YOUR-PASSWORD>
```

Neste mesmo arquivo ative a linha FromLineOverride=YES que vem comentada por padrão

Edite o valor de sendmail_path no seu php.ini como na linha abaixo

```
sendmail_path = /usr/sbin/ssmtp -t
```

Reinicie o apache

OBS: Na sua conta google precisa habilitar a opção "Permitir aplicativos menos seguros"

Não esqueça de habilitar a porta
iptables -A INPUT -p tcp --dport 587 -j ACCEPT
