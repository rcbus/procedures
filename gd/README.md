# Procedimento GD

GD é uma biblioteca gráfica que o PHP usa para manipular imagens dinamicamente

<br><br>

1 - Para funcionar tudo adequadamente, caso a GD não tenha sido instalada com o PHP, será necessário fazer isso manualmente. Acesso o php.ini, vá até "Extension" e libere a extensão ;extension=gd

2 - Copie o arquivo "20-gd.ini" para a pasta "/etc/php/<versão php>/apache2/conf.d/"

3 - Copie o arquivo "gd.so" para a pasta "/usr/lib/php/<pasta da versão php>/"

<br><br>

OBS: Para saber a versão do PHP consulte <?php phpinfo(); ?>
