# Criar disco GPT para instalar Windows

Pressione Shift + F10

Entre no disk part
```
diskpart
```

Ver lista de discos
```
list disk
```

Selecione o disco
```
select disk #
```

Limpe o disco
```
clean
```

Converta o disco para GPT
```
convert gpt
```

Feche a janela de comando e atualize a página de instalação
