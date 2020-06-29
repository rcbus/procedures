# Procedures
Procedimentos de ambiente de programação em geral

# Mongo DB
Para usar o mongodb é necessário criar previamente o banco de dados e o usuario
com privilégios para leitura e escrita no mesmo conforme instruções abaixo:

use dbName

db.createUser({user:"name",pwd:"senha123",roles:[{role:"readWrite",db:"dbName"}]})
