# Quebrar Senha do Excel

IMPORTANTE! Faça esse procedimento em um computador windows, nunca testei ele no linux, deve dar certo também, mas no windows é garantido que da certo, portanto a minha explicação se baseia em um ambiente windows.

## PRÉ-REQUISITOS: 

1. Ter o Winrar instalado, facilita muito!

2. Ter um editor de texto bom, para esse caso eu usei o VSCODE, é gratuito e fácil de instalar.

## PROCEDIMENTO:

1. Faça uma copia do arquivo protegido.

2. Renomeie esse arquivo para um nome simples, exemplo "A", isso é só para facilitar o processo.

3. Copie esse arquivo para uma pasta de fácil acesso via prompt de comando (MS-DOS), exemplo "C:\Users\Jose\Documents" (é melhor que seja em uma pasta do usuário e não na raiz, para evitar problemas de permissão de leitura e escrita)

4. Abra o prompt de comando (MS-DOS) e navegue até a pasta onde você salvou o arquivo.

```
cd C:\Users\Jose\Documents
```

5. Renomeie o arquivo para transformá-lo em um arquivo ".zip" (OBS: Se o arquivo estiver em XLS salve-o como XLSX primeiro)

```
rename A.xlsx A.zip
```

6. Extraia o arquivo, deverá aparecer uma pasta com o nome "A"

7. Dentro dessa pasta deve ter uma pasta chamada "xl", e dentro dela deve ter uma pasta chamada "worksheets", e dentro dela deve ter arquivos .xml com nomes assim "sheet1.xml", "sheet2.xml" e assim por diante.

8. Um desses arquivos deve ser a sua planilha bloqueada por senha, de vc não mudou a ordem das planilhas no excel ela deve obdecer a mesma ordem, ou seja, se a planilha bloqueada é a planilha 2, então o arquivo é o "sheet2.xml".

9. Abra o arquivo com o VSCODE, depois usando o comando "Ctrl + F" (que abre o campo de pesquisa), digite a palavra "sheetProtection", ele deve localizar uma tag com esse nome.

10. Apague a tag inteira "<sheetProtection ... />"

11. Salve o arquivo e feche.

12. Dentro da pasta "A", crie um arquivo ".zip" pode ser com o nome "B.zip" e arraste todas as pastas e arquivos da pasta "A" para dentro do arquivo "B.zip". OBS.: Porque não copiar a pasta "A" inteira para o arquivo "B.zip"? Primeiro porque o arquivo "B.zip" está dentro da pasta "A", justamente para que você não copia a pasta inteira senão dará erro.

13. Renomeie o arquivo para transformá-lo novamente em ".xlsx".

```
rename B.zip B.xlsx
```

Pronto! Abrindo o arquivo "B.xlsx" a sua planilha já deve estar desbloqueada.
