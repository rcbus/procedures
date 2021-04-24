# Chave SSH Github

1 - Comando para gerar a chave no computador de origem da conexão
```
ssh-keygen
```

2 - Deve aparecer isso, apenas aperte enter
```
Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa):
```

3 - Caso apareça isso, é porque já existe uma chave, <b>NÃO</b> recomendo que sobrescreva ela, execute o passo 4
```
/root/.ssh/id_rsa already exists.
Overwrite (y/n)?
```

4 - Para pegar a chave use esse comando
```
cat ~/.ssh/id_rsa.pub
```

5 - Deve aparecer algo assim, copia tudo desde o "ssh-rsa" até o final que deve ser algo como "user@domain"
```
ssh-rsa AABAQCmZln3DCX8pMtxxoB/aXT4vPZ1TtpHAbPYntdZEkn/KIbpYYy+5HE76V0Q0oeB0vHbFuI9esZlB+gd8ik9MoJnuu5E/kVxPeJuSmUUyeKaEm5YYrXkYJmg0R9a4VI7yR0o5pUJwOhVhUGVG1JsX0AjWTBpJLjryWxqmWpdKCzlBVMCwKoHx8tGrcoJ8hboufk5za634PJYYb6XY0NcJGi5SwYVz7inxiGKWN8DJXiXvtqxq+v0nSvfmbmVDSv1tEuG3Hut89vGi1xSqHgZ1aoAtIPZPW/nXBW68qTjgjoISlBa user@domain
```

6 - Acesse https://github.com/settings/keys e clique em "New SSH Key". Dê um titulo e cole a sua chave no campo "Key"

7 - Agora no computador da origem da conexão na pasta do repositório que deseja interagir com o Github execute o comando, substituindo o "user" pelo nome do seu usuário no Github e "repository.git" pelo nome do seu repositório no Github
```
git remote set-url origin git@github.com:user/repository.git
```

Pronto, agora você já pode interagir com o Github normalmente. Se você colocou uma senha na sua chave, essa senha será solicitada todas as vezes. É altamente recomendado colocar senha na chave, assim você tem uma camada a mais de proteção.
