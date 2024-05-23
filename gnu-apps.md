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

Tar é "ordenador" de arquivos, seria semelhante a "unir" todos os arquivos em um só. Comumente utilizado com o Gz (GNU Zip) que fica responsavel por compactar essa "tira" em um unico arquivo.

### Compactando tar.gz
```
tar -czf [name].tar.gz dir/
```

### Descompactando tar.gz
```
tar -zxvf [name].tar.gz
```

## TMUX

Multiplexador de terminais
*OBS*.: A tecla (ou combinação) para o PREFIXO é: ctrl + b

### Listando as seções
```
tmux ls
```

### Saindo de uma seção
Existem duas maneiras, mais usuais de sair de uma seção:

* PREFIXO + d # irá sair da seção sem finaliza-lá
* exit # irá "matar" a seção

### Criando seção
```
tmux new
```

### Criando seção com nome
```
tmux new -s NOME_SEÇÃO
```

### Criando seção sem entrar
```
tmux new -d
```
*OBS*.: Pode-se combinar comandos, criando seção com um nome
```
tmux new -s NOME_SEÇÃO -d
```

### Destruindo seções

#### Destruindo uma seção
```
tmux kill-session -t NOME_SEÇÃO
```
Ou abreveando:
```
tmux kill-sessi -t NOME_SEÇÃO
```

#### Destruindo todas as seções
```
tmux kill-server
```

### Entrando em uma seção
```
tmux a -t NOME_SEÇÃO
```

### Criando uma nova seção dentro de uma seção
PREFIXO + c

### Circulando entre seções
PREFIXO + n # proxima (NEXT) seção
PREFIXO + p # seção (PREVIOUS) anterior

### Divisão de janela na vertical
PREFIXO + %

### Divisão de janela na horizontal
PREFIXO + "

### Focando/desfocando de uma janela
prefixo + z

### Circulando entre as janelas
prefixo + [DIRECIONAIS DO TECLADO]
