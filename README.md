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
