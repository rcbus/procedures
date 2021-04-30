# Como Instalar e Usar o Imagick PHP

Execute o comando abaixo
```
sudo apt install php-imagick php-gd
```

Edite o arquivo abaixo 
```
cd /etc/ImageMagick-6
sudo vim policy.xml
```

Comente a linha
```
<!-- <policy domain="coder" rights="none" pattern="MVG" /> -->
```

Reescreva a linha
```
<policy domain="coder" rights="none" pattern="PDF" />
```
Para
```
<policy domain="coder" rights="read|write" pattern="PDF" />
```

Execute o comando
```
sudo apt-get install inkscape
```

Reinicie o apache e teste com o script abaixo
```
<?php
$imagick = new Imagick();

$imagick->setResolution(150, 150);

$imagick->readImage('teste.pdf');

$imagick = @$imagick->flattenImages(); 

$imagick->writeImages($_SERVER['DOCUMENT_ROOT'].'/teste/teste2.png', false);
```

OBS: A pasta onde você vai salvar a imagem precisa ter permissão de escrita
