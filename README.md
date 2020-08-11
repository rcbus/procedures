# Procedures
Procedimentos de ambiente de programação em geral

# Forever

Serve para deixar um servidor node rodando para sempre. Para isso instale o forever.

```
npm install forever -g
```

Depois execute o comando abaixo para rodar o servidor.

```
forever start -c "npm start" /path/to/app/dir/
```

Ou estando dentro da pasta do projeto.

```
forever start -c "npm start" ./
```

Para listar os servidores rodando com forever use o comando abaixo.

```
forever list
```

Para parar o servidor execute o comando abaixo colocando o número do serviço no final.

```
forever stop 0
```

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

```
npm run build
```

```
npm install forever -g
```

```
forever start -c "npm start" ./
```


# Instalação de Projetos Node do Padrão RCBUS
Ao baixar um repositório de um projeto node do RCBUS deve-se apagar o arquivo package-lock.json, apagar o diretório node_modules e apagar o diretório .next

Após fazer isso rodar o npm install dentro da pasta do projeto.

Depois renomeie o arquivo next.config.example.js para next.config.js e insira suas informações.

Depois renomeie o arquivo aws.config.example.json para aws.config.json e insira suas informações caso for usar recursos da AWS.

Verificar se a pasta components tem os arquivos de components. Caso não tenha, executar os seguintes comandos:

    - cd components
    
    - git init
    
    - git remote add origin https://github.com/rcbus/components.git

    - git pull origin master
    
Verificar se a pasta libs tem os arquivos de libs. Caso não tenha, executar os seguintes comandos:

    - cd libs
    
    - git init
    
    - git remote add origin https://github.com/rcbus/libs.git
    
    - git pull origin master

Verificar se existe o arquivo .gitignore , caso não exista crie um arquivo com esse nome na raiz do seu projeto e copie e cole o exemplo de .gitignore acima neste repositório.

Depois rodar o npm run dev. Deve funcionar tudo certo, desde que você atenda ao requisitos de infraestrutura descritos no README.md do projeto que está usando.

# Mongo DB
Para usar o mongodb é necessário criar previamente o banco de dados e o usuario
com privilégios para leitura e escrita no mesmo conforme instruções abaixo:

use dbName

db.createUser({user:"name",pwd:"senha123",roles:[{role:"readWrite",db:"dbName"}]})


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
