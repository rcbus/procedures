# Instalando e Configurando SSL

Instale o módulo openssl

```
sudo su

apt-get update

apt-get install apache2 openssl

a2enmod ssl

a2enmod rewrite
```

Altere o /etc/apache2/apache2.conf para a o seguinte:

```
<Directory /var/www/html>
  AllowOverride All
</Directory>
```

Altere o /etc/apache2/sites-available/000-default.conf para o seguinte:

```
<VirtualHost *:80>
        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/html
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>

<VirtualHost *:80>
        RewriteEngine On
        RewriteCond %{HTTPS} !=on
        RewriteRule ^/?(.*) https://%{SERVER_NAME}/$1 [R=301,L]
</virtualhost>

<VirtualHost *:443>
        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/html
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
        SSLEngine on
        SSLCertificateFile /etc/apache2/certificate/apache-certificate.crt
        SSLCertificateKeyFile /etc/apache2/certificate/apache.key
</VirtualHost>
```

Agora instale o snap e verifique se precisa ser atualizado.

Instale o certbot: (Se precisar consulte https://certbot.eff.org/lets-encrypt/ubuntuxenial-apache)

```
snap install --classic certbot
```

Crie, instale e habilite o certificado: (Obs.: Siga as instruções que são solicitadas, principalmente quando pede o domínio)

```
certbot --apache
```

Reinicie o servidor

```
service apache2 restart
```

Com esse procedimento, já deve estar funcionando o HTTPS seguro e reconhecido pelo browser, e também se o usuário tentar entrar pelo HTTP será redirecionado para o HTTPS
