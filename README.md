# Procedures
Procedimentos de ambiente de programação em geral

# Atualizar Servidor Node.js com Next

1 - Atualizar os components e libs usando o git-manage

2 - Atualizar o app usando o git-manage

3 - Parar o servidor (verifique o ID do processo, geralmente é o zero)

```
pm2 stop 0
```

4 - Apague a pasta .next e execute o build.

```
sudo rm -rf .next
```

```
npm run build
```

5 - Após o build entre como root e inicie o servidor.

```
sudo su
```

```
pm2 start "npm start"
```

# Forever / PM2

Serve para deixar um servidor node rodando para sempre. Para isso instale o forever. Passei a usar o PM2 pois funciona melhor do que o forever. É bom instalar o mesmo como usuário root para que possa ter acesso a porta 80, bloqueada para usuários comuns.

```
sudo su
```

```
npm install pm2 -g
```

Depois execute o comando abaixo para rodar o servidor dentro da pasta do app.

```
pm2 start "npm start"
```

Para listar os servidores rodando com pm2 use o comando abaixo.

```
pm2 list
```

Para parar o servidor execute o comando abaixo colocando o número do serviço no final.

```
pm2 stop 0
```

Para que o servidor seja executado logo após o servidor ser reinicializado, use o comando abaixo.

```
pm2 startup
```

# GIT

<b>Resumo de comandos (antes de executa-los leia atenciosamente cada um deles logo abaixo)</b>

OBS.: Onde tem "||" entenda como "OU", ou seja, pode ser usado um comando ou outro.

```
git branch name
```

```
git checkout name
```

```
git branch
```

```
git branch -D branch (para deletar uma branch se necessário)
```

```
git pull origin master
```

OBS.: Alterar a versão no arquivo version-app.js a cada pull origin master

```
git add . 		||		$ git add filename.ext		||		$ git reset HEAD filename.ext
```

```
git status
```

```
git commit -m "mensagem"
```

```
git push -u origin branch
```

```
git checkout --track origin/update_cleiton_24042020_1139 (para migrar para uma atualização especifica)
```

OBS.: Se houver algum problema do tipo "fatal: pathspec is in submodule" use o procedimento abaixo, inserindo o nome ou caminho do diretório no lugar de "directory".

```
git rm --cached directory
```

```
git add directory
```

OBS.: Se houver algum problema para realizar o "git pull origin master" use o procedimento abaixo.

```
git fetch --all
```

```
git reset --hard origin/master
```

```
git pull origin master
```

OBS.: Se precisar tirar algum arquivo do rastreio do git use o comando abaixo.

```
git rm -r --cached filename.ext
```

<b>1 - Criar branch (ramo)</b>

Sempre que for iniciar uma nova modificação no sistema, principalmente se essa modificação for específica de um modulo ou parte do sistema você deve criar uma nova branch (ramificação). Para criar um novo branch use o comando abaixo, não há necessidade de uso de aspas, e o nome deve manter o seguinte padrão update_seunome_YYYYMMDD_HHMM, por exemplo se eu fosse criar uma branch hoje dia 27 de março de 2020 as 09:38 da manhã, eu escreveria update_cleiton_20200327_0938. O uso de underline "_" é obrigatório pois o nome da branch não deve ter espaços. 

```
git branch name
```

<b>2 - Trocar de branch</b>

Após criar uma nova branch você deve migrar pra ela. Para isso use os comandos abaixo, o primeiro faz a troca, no lugar de "name" insira o nome da branch que acabou de criar. E o segundo verifica se você migrou para branch que acabou de criar, você saberá em qual branch está pois ela vai estar destacada em verde.

```
git checkout name
```

```
git branch
```

<b>3 - !!! IMPORTANTE !!! - Atualizar a nova branch com a versão mais recente</b>

Antes de fazer qualquer alteração de documento, é importante que você atualize a branch com a versão mais recente, a master remota, isso evita ramificações orfãs e sobreposições de código conflitante, e assim todo pull request que chegar no repositório remoto para mergear chega limpo e baseado na ultima versão válida.

```
git pull origin master
```

<b>4 - Adicionar arquivos alterados a nova branch</b>

Após fazer todas as alterações de arquivos e testar localmente você deve liberar essas alterações na branch, para isso você deve usar os comandos abaixo. O primeiro adiciona todos os arquivos alterados de uma só vez. O segundo adiciona um arquivo específico. O terceiro serve para você verificar o que foi adicionado ou não na branch, o que estiver em vermelho não foi adicionado, e o que estiver em verde foi adicionado. O quarto serve para você estornar um arquivo que não queira adicionar a sua branch por enquanto. 

```
git add .
```

```
git add filename.ext
```

```
git status
```

```
git reset HEAD filename.ext
```

<b>5 - Fazer um commit das alterações</b>

O commit é um comentário ou detalhamento das alterações feitas, sem fazer um commit não é possível enviar a branch para o repositório remoto. Você até pode fazer commit por arquivo, mas para o nosso sistema é melhor fazermos um commit geral. Para isso basta usar o comando abaixo, inserindo a mensagem de detalhamento no lugar de "mensagem". As aspas são obrigatória pois se trata de texto, e sempre inicio o commit com o nome da branch por exemplo $ git commit -m "update_cleiton_20200327_1038 - Feito alterações no README.md". Se preferir não inserir nenhum comentário adicional insira apenas o nome da branch. Obs.: Commit sem o nome da branch será recusado.

```
git commit -m "mensagem"
```

<b>6 - Enviar a branch para o repositório</b>

Após o commit você já pode enviar a branch. Para isso use o comando abaixo onde "branch" é o nome da sua branch. Atenção, certifique-se de que o nome da branch está correto para não haver divergencias.

```
git push -u origin branch
```

<b>7 - Como atualizar a mesma branch?</b>

Para atualizar a mesma branch, mesmo que você já tenha realizado o push, você pode repetir os passos 4, 5 e 6 novamente, apenas no passo 5 é bom descrever melhor a nova alteração para ser melhor rastreável.

# Instalação de Novo Servidor

É importante aumentar o limite de cache do processador para não bugar o node e npm.

```
cat /proc/sys/fs/inotify/max_user_watches
```

Retorno de ser: 8192

```
echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p
```

É importante lembrar que para rodar um app na porta 80 diretamente, é preciso fazer isso com o usuario root, e talvez seja necessário instalar o nvm, node, npm e forever novamente como root, para isso execute os comandos abaixo estando na pasta raiz do app.

```
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash
```

```
nvm install v12.18.3
```

Acesse a pasta do app e execute os comandos abaixo

```
npm run build
```

```
sudo su
```

```
npm install pm2 -g
```

```
pm2 start "npm start"
```

```
pm2 startup
```


# Instalação de Projetos Node do Padrão RCBUS
Ao baixar um repositório de um projeto node do RCBUS deve-se apagar o arquivo package-lock.json, apagar o diretório node_modules e apagar o diretório .next

Após fazer isso rodar o npm install dentro da pasta do projeto.

Depois renomeie o arquivo next.config.example.js para next.config.js e insira suas informações.

Depois renomeie o arquivo aws.config.example.json para aws.config.json e insira suas informações caso for usar recursos da AWS.

Verificar se a pasta components tem os arquivos de components. Caso não tenha, executar os seguintes comandos:

```
cd components
```

```
git init
```    

```
git remote add origin https://github.com/rcbus/components.git
```

```
git pull origin master
```
    
Verificar se a pasta libs tem os arquivos de libs. Caso não tenha, executar os seguintes comandos:

```
cd libs
```

```
git init
```

```
git remote add origin https://github.com/rcbus/libs.git
```

```
git pull origin master
```

Verificar se existe o arquivo .gitignore , caso não exista crie um arquivo com esse nome na raiz do seu projeto e copie e cole o exemplo de .gitignore acima neste repositório.

Depois rodar o npm run dev. Deve funcionar tudo certo, desde que você atenda ao requisitos de infraestrutura descritos no README.md do projeto que está usando.

# Instalar LAMP (Linux Apache MySQL PHP)

Execute a atualização do linux

```
sudo apt update

sudo apt upgrade

sudo apt update
```

Instale o Apache 2

```
sudo apt install -y apache2
```

Para testar se o Apache está funcionando corretamente, devemos digitar "localhost" na barra de endereços do navegador de sua preferência.

Se quiser mudar o diretório root do apache, acesso o arquivo /etc/apache2/apache2.conf com privilégios de administrador ou root. E altere a linha "<Directory /var/www>" pela linha abaixo

```
<Directory /caminho_da_pasta_da_sua_preferencia>
```

Depois acesso o arquivo /etc/apache2/sites-available/000-default.conf com privilégios de administrador ou root. E altere a linha "DocumentRoot /var/www/html" pela linha abaixo e reinicie o servidor

```
DocumentRoot /caminho_da_pasta_da_sua_preferencia
```

```
sudo service apache2 restart
```

Caso após reiniciar o apache dê erro 403 Forbidden pode ser que a pasta que você escolheu tem alguma pasta no caminho sem permissão de execução de arquivos, como por exemplo abaixo, rode o comando abaixo:

```
namei -m /caminho_da_pasta_da_sua_preferencia/www
```

O resultado desse comando provavelmente será esse:

```
f: /caminho_da_pasta_da_sua_preferencia/www
 drwxr-xr-x /
 drwxr-x--- caminho_da_pasta_da_sua_preferencia
 drwxrwxrwx www
```

As linhas de cada pasta do caminho tem que ter 3 "x", o "x" significa permissão de execução, repare que uma das linhas está faltando um "x". Para corrigir isso execute o comando abaixo para cada uma das pastas nessas condições:

```
sudo chmod o+x /caminho_da_pasta_da_sua_preferencia
```

Depois rode o comando abaixo novamente:

```
namei -m /caminho_da_pasta_da_sua_preferencia/www
```

E o resultado desse comando agora será esse:

```
f: /caminho_da_pasta_da_sua_preferencia/www
 drwxr-xr-x /
 drwxr-xr-x caminho_da_pasta_da_sua_preferencia
 drwxrwxrwx www
```

Pronto isso deve ser o suficiente para acabar com o erro 403 Forbidden

Configure o prefork conforme abaixo para um melhor desempenho do apache:

```
cd /etc/apache2/mods-enabled
```
```
sudo cp mpm_prefork.conf mpm_prefork.conf.cs
```
```
sudo vim mpm_prefork.conf
```

Deve estar assim:

```
<IfModule mpm_prefork_module>
        StartServers                     5
        MinSpareServers           5
        MaxSpareServers          10
        MaxRequestWorkers         150
        MaxConnectionsPerChild   0
</IfModule>
```

Configure assim:

```
<IfModule mpm_prefork_module>
        StartServers                     50
        MinSpareServers           50
        MaxSpareServers          100
        MaxRequestWorkers         1000
        MaxConnectionsPerChild   2000
</IfModule>
```
```
sudo service apache2 restart
```

Instale o PHP

```
sudo apt install -y php php-cli php-common php-gd php-mbstring php-intl php-xml php-zip php-pear libapache2-mod-php
```

Para testar use o procedimento abaixo

```
echo "<?php phpinfo(); ?>" | sudo tee /var/www/html/test.php | sudo service apache2 restart
```

Para testar o PHP no navegador, digite na página de endereços: localhost/test.php

Se precisar instalar uma versão específica acesse https://sempreupdate.com.br/instalar-versoes-diferentes-php-7-2-7-3-7-4-8-0-no-ubuntu/

Configure o PHP para uma melhor performance, acesse o arquivo /etc/php/7.2/apache2/php.ini encontre as linhas

```
max_execution_time = 30

max_input_time = 60

memory_limit = 128M

display_errors = Off

post_max_size = 8M

upload_max_filesize = 2M

default_socket_timeout = 60
```

Altere conforme abaixo

```
max_execution_time = 600

max_input_time = 600

memory_limit = 4096M / 16384M

display_errors = On

post_max_size = 256M

upload_max_filesize = 256M

default_socket_timeout = 600
```

Caso o servidor trabalhe com SQLServer inclua na sessão "Dinamic Extensions" a linha abaixo e baixe o módulo de comunicação aqui mesmo nesse reposítório

```
extension=/usr/lib/php/20170718/php_sqlsrv_72_nts.so
extension=/usr/lib/php/20170718/php_pdo_sqlsrv_72_nts.so
```

Ou

```
extension=php_sqlsrv_72_nts.so
extension=php_pdo_sqlsrv_72_nts.so
```

Siga as instruções da sessão UBUNTU no ODBC 17 em https://docs.microsoft.com/pt-br/sql/connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server?view=sql-server-ver15 para instalar o ODBC


Salve o arquivo e reinicie o servidor

```
sudo service apache2 restart
```

Instale o MySQL

```
sudo apt install -y mysql-server mysql-client php-mysql
```

Configure o MySQL seguindo o procedimento abaixo

```
sudo mysql
```

Ou com a senha se caso foi solicitado a criação de uma senha no momento da instalação

```
sudo mysql -p
```

Depois que estiver logado no mysql, um ponteiro deve aparecer assim "mysql> ", para digitar os comandos do mysql. Execute o procedimento abaixo para criar o usuário e conceder privilégios para o mesmo

```
CREATE USER 'seu_usuario'@'localhost' IDENTIFIED BY 'sua_senha';

GRANT ALL PRIVILEGES ON *.* TO 'seu_usuario'@'localhost' WITH GRANT OPTION;

ALTER USER 'seu_usuario'@'localhost' IDENTIFIED WITH mysql_native_password BY 'sua_senha';

FLUSH PRIVILEGES;

exit
```

Para facilitar o copia e cola, use linha por linha abaixo

```
CREATE USER ''@'' IDENTIFIED BY '';
```
```
GRANT ALL PRIVILEGES ON *.* TO ''@'' WITH GRANT OPTION;
```
```
ALTER USER ''@'' IDENTIFIED WITH mysql_native_password BY '';
```
```
FLUSH PRIVILEGES;
```
```
exit
```

Teste o acesso do usuario criado com o comando abaixo, insira a senha

```
sudo mysql -u seu_usuario -p
```

Configure a memoria ram que o mysql irá usar usando o código abaixo:

4GB / 8GB
```
SET GLOBAL innodb_buffer_pool_size=4294967296;
```

8GB / 16GB
```
SET GLOBAL innodb_buffer_pool_size=8589934592;
```

16GB / 32GB
```
SET GLOBAL innodb_buffer_pool_size=17179869184;
```

22GB / 32GB - Limite de 70% da RAM
```
SET GLOBAL innodb_buffer_pool_size=23622320128;
```

Confira se está certo:

```
SHOW VARIABLES LIKE 'innodb_buffer_pool_size';
```

Ajuste o sql_mode tirando o ONLY_FULL_GROUP_BY:

```
cd /etc/mysql/mysql.conf.d
```
```
sudo cp mysqld.cnf mysqld.cnf.cs
```
```
sudo vim mysqld.cnf
```

Altere:

```
bind-address            = 127.0.0.1
```

Para:

```
bind-address=0.0.0.0
```

Se tiver uma linha setada com innodb_buffer_pool_size como o exemplo abaixo:

```
innodb_buffer_pool_size=134217728
```

Para um desses de acordo com a memória do servidor:

4GB / 8GB
```
innodb_buffer_pool_size=4294967296;
```

8GB / 16GB
```
innodb_buffer_pool_size=8589934592;
```

16GB / 32GB
```
innodb_buffer_pool_size=17179869184;
```

22GB / 32GB - Limite de 70% da RAM
```
innodb_buffer_pool_size=23622320128;
```

Acrescente no final do aquivo:

```
sql_mode="STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION"
```
```
sudo service mysql restart
```

Caso dê algum erro mude para:

```
sql_mode="STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION"
```
```
sudo service mysql restart
```

Instale o pacote mysqli

```
sudo apt-get install php7.2-mysqlnd
```

Instale o PHPMyAdmin. Caso necessite, utilize a mesma senha criada para o MySQL

```
sudo apt install -y phpmyadmin
```

Acesse o arquivo /etc/apache2/sites-available/000-default.conf com privilégios de administrador ou root. E insira no início do arquivo a linha abaixo

```
Alias /phpmyadmin /usr/share/phpmyadmin/
```

Reinicie o servidor

```
sudo service apache2 restart
```

Para testá-lo no navegador, digite na barra de endereços: localhost/phpmyadmin

É bom instalar o SSH Server para poder acessar essa máquina remotamente

```
sudo apt-get install openssh-server
```

Talvez seja necessário liberar acesso à porta SSH que em geral por padrão é a porta 22

```
sudo iptables -I INPUT -p tcp --dport 22 -j ACCEPT
```

# Mongo DB
Para usar o mongodb é necessário criar previamente o banco de dados e o usuario
com privilégios para leitura e escrita no mesmo conforme instruções abaixo:

```
use dbName
```

```
db.createUser({user:"name",pwd:"senha123",roles:[{role:"readWrite",db:"dbName"}]})
```

Para criar collections use nome apenas com letras e não usar hífen "-", use underline "_"

Para apagar uma collection user o comando db.collection.drop()
<br>
Para fazer um dump (backup) de um banco mongodb execute o código abaixo.

```
mongodump --db=dbName --out=/home/user/www/app/backup/
```

Para restaurar um dump (backup) de um banco mongodb execute o código abaixo.

```
mongorestore /home/user/www/app/backup/
```

# RSYNC para servidor AWS com chave pública

```
sudo rsync -avz -e "ssh -i /home/user/documents/key.pem" /home/user/www/app/backup/ <user>@<domain/ip>:/home/user/www/app/backup/
```
