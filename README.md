# Procedures
Procedimentos de ambiente de programação em geral

# Instalação de Projetos Node do Padrão RCBUS
Ao baixar um repositório de um projeto node do RCBUS deve-se apagar o arquivo package-lock.json, apagar o diretório node_modules e apagar o diretório .next

Após fazer isso rodar o npm install dentro da pasta do projeto e depois npm run dev. Deve funcionar tudo certo, desde que você atenda ao requisitos de infraestrutura descritos no README.md do projeto que está usando.

# Mongo DB
Para usar o mongodb é necessário criar previamente o banco de dados e o usuario
com privilégios para leitura e escrita no mesmo conforme instruções abaixo:

use dbName

db.createUser({user:"name",pwd:"senha123",roles:[{role:"readWrite",db:"dbName"}]})


Para criar collections use nome apenas com letras e não usar hífen "-", use underline "_"

Para apagar uma collection user o comando db.collection.drop()
