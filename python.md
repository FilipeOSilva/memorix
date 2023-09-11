# PYTHON

Notas e dicas de funcionamento da linguagem de progamação Python

## Ambiente

### Feramentas

#### Pipx

Ferramenta utilizada para instalação de "pacotes" python de forma "global" na maquina host. Geralmente utilizo o pipx para gerir pacotes "globais" na minha maquina.

##### Instalação

Pode ser intalado via "pip":
```
$ pip install pipx
```

Ou via gerenciador de pacotes do sistema (no meu caso distribuições "like Debian", via APT):
```
$ sudo apt install pipx
```

*_Obs_*.: No meu ambiente, acabei colocando dentro do script de instalação total de pacotes. Ver install.md [https://github.com/FilipeOSilva/memorix/blob/main/install.md]

##### Configuração

Pode-se adicionar o path do pipx para o seu usuario manualmente (editando o arquivo .bashrc) ou deixar que o proprio pipx faça isso, executando a instrução:

```
$ pipx ensurepath
```

#### Poetry

Gerenciador de pacotes (responsavel por gerir quais bibliotecas, Lint, documentação) para organizar o desenvolvimento de um projeto python.

##### Instalação

Como será global, utilizo o pipx
```
$ pipx install poetry
```

##### Iniciando um projeto

```
$ poetry new new-project
```


