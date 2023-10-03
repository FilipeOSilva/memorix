# Uso de apps do GNU/linux

Aqui estaram alguns "macetes" para o uso de programas no ***Shell***

## ZIP

Compactador de arquivos no padrão ***.zip**. "Zipando” uma pasta:
```
zip -r test.zip pasta/*
```

## UNZIP

Descompactador de arquivos no padrão  ***.zip**.

Utizado para “deszipar” um arquivo:
```
unzip test.zip -d pasta
```

Podemos “listar” o conteúdo dentro do arquivo “zipado”:
```
unzip -l test.zip
```

## SCP 

O scp é uma maneira rápida e pratica para transferir arquivos entre servidores Linux pelo terminal.

### Enviando Arquivo

Para enviar um arquivo da sua máquina para a destinataria basta saber o endereço, ter o login e senha. Um detalhe importante é definir onde o arquivo ficará no destino:
```
scp aquivo_enviado.txt [login]@[ip_destinatario]:[/home/pasta_destino/]
```

### Pegando Arquivo

Para pegar um arquivo de uma máquina temos que saber o endereço, ter o login e senha. Devemos definir aonde queremos o arquivo na nossa máquina:
```
scp [login]@[ip_destinatario]:[/home/pasta_do_arquivo/arquivo_recebido.txt] .
```
*OBS*.: Aqui iremos recerber o arquivo na pasta onde estamos.

## TAR

Tar é "orenador" de arquivos, seria semelhante a "unir" todos os arquivos em um só. Comumente utilizado com o Gz (GNU Zip) que fica responsavel por compactar essa "tira" em um unico arquivo.

### Compactando tar.gz
```
tar -czf [name].tar.gz dir/
```

### Descompactando tar.gz
```
tar -zxvf [name].tar.gz
```
