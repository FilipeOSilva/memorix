## Adicionando usuario ao grupo root
```
sudo su
echo "silva   ALL=(ALL:ALL) ALL" > /etc/sudoers.d/silva
```

## Editando fontes do *apt*

Acessar o arquivo e comentar a linha referente ao "CD de instalação"

```
vi /etc/apt/sources.list

#deb cdrom:[Debian GNU/Linux 12.0.0 _Bookworm_ - Official amd64 DVD Binary-1 with firmware 20230610-10:23]/ bookworm main non-free-firmware
```

## Problemas com *"boot"*

### GRUB

#### Recarregando configuração do GRUB

Na incialização, acessar o bash do GRUB (no meu caso é só apertar C na inicialização):

```
GRUB> configfile (hd0,gpt2)/boot/grub/grub.cfg
```

*obs.:* No meu caso eu "sabia" qual era a minha partição, caso não tenha ideia, pode-se usar o comando *ls* para listar as partições e dai ver qual é a que está correta.

```
GRUB> ls
(proc) (memory) (hd0) (hd0,gpt1) (hd0,gpt2)
```

### Verificando partição EFI e Gerando novo arquivo GRUB

#### Apenas atualizando o arquivo do GRUB

No terminal, ver se realmente já existe uma partição efi:
```
lsblk
NAME        MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
sda           8:0    0 223,6G  0 disk
├─sda1        8:1    0 111,8G  0 part /boot/efi
└─sda2        8:2    0 537,1M  0 part /
```
Nesse caso temos uma partição "efi" e podemos, "atualizar" para que tenha todos os possiveis boots. Para isso:
```
grub-install /dev/sda
```
Saída:
```
Instalando para a plataforma x86_64-efi.
Instalação terminada. Sem erros reportados.
```

Fazendo update do grub
```
update-grub
```
Saída:
```
Generating grub configuration file ...
Found background image: /usr/share/images/desktop-base/desktop-grub.png
Found linux image: /boot/vmlinuz-6.1.0-12-amd64
Found initrd image: /boot/initrd.img-6.1.0-12-amd64
Found linux image: /boot/vmlinuz-6.1.0-11-amd64
Found initrd image: /boot/initrd.img-6.1.0-11-amd64
Found linux image: /boot/vmlinuz-6.1.0-9-amd64
Found initrd image: /boot/initrd.img-6.1.0-9-amd64
Adding boot menu entry for UEFI Firmware Settings ...
done
```

Podemos ainda para garantir que a tabela está correta ver o conteudo do fstab

```
cat /etc/fstab
```
Saída:
```
# /etc/fstab: static file system information.
#
# Use 'blkid' to print the universally unique identifier for a
# device; this may be used with UUID= as a more robust way to name devices
# that works even if disks are added and removed. See fstab(5).
#
# systemd generates mount units based on this file, see systemd.mount(5).
# Please run 'systemctl daemon-reload' after making changes here.
#
# <file system> <mount point>   <type>  <options>       <dump>  <pass>
# /boot/efi was on /dev/sda1 during installation
UUID=AE0B-EB80  /boot/efi       vfat    umask=0077      0       1
# / was on /dev/sda2 during installation
UUID=fe0f6014-577d-4910-beaf-a65d1ecdf040 /               ext4    errors=remount-ro 0       1
```

#### Gerando nova partição do EFI e novo arquivo do GRUB

No terminal, ver as partições:
```
lsblk
NAME        MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
sda           8:0    0 223,6G  0 disk
└─sda1        8:2    0 537,1M  0 part /
```
Nesse caso temos uma partição apenas, teremos que criar uma partição efi e a tabela do GRUB.
*ATENÇÃO*:
* O particionamento necessita de extrema atenção, onde devemos sempre ter em mente que ele irá "Apagar" toda a partição, fazendo com que possamos não conseguir mais fazer o boot ou ainda deixando arquivos sem acesso;
* Cuidado com a questão de assinaturas, afinal é ela que "orienta a partição";
* Caso esteja com duvida, não salve o processo, deixe esse passo para o final, caso tenha duvida ou tenha feito algum particionamento de forma que não esteja de acordo com o esperado e não tenha salvado ainda, basta sair que não irá implicar em nenhuma mudança;

```
fdisk /dev/sda
```
Saída:
```
Bem-vindo ao fdisk (util-linux 2.38.1).
As alterações permanecerão apenas na memória, até que você decida gravá-las.
Tenha cuidado antes de usar o comando de gravação.

Este disco está em uso - reparticionar provavelmente é uma má ideia.
É recomendado desmontar todos os sistemas de arquivos e trocar todas
as partições de swap neste disco.

Comando (m para ajuda): 
```
Liste as partições, para se ter noção de onde elas começam e terminam:
```
Comando (m para ajuda): p

Disco /dev/sda: 223,58 GiB, 240065183744 bytes, 468877312 setores
Modelo de disco: WDC WDS240G2G0A-
Unidades: setor de 1 * 512 = 512 bytes
Tamanho de setor (lógico/físico): 512 bytes / 512 bytes
Tamanho E/S (mínimo/ótimo): 512 bytes / 512 bytes
Tipo de rótulo do disco: gpt
Identificador do disco: A01AF01F-016C-5942-9A0F-CD8968AA88A3

Dispositivo    Início       Fim   Setores Tamanho Tipo
/dev/sda1        2048 234375167 234373120  111,8G Linux sistema de arquivos

Comando (m para ajuda):
```
Crie um novo particionamento do tipo *gpt* (dica: a tecla m trás todas as opções):
```
Comando (m para ajuda): g
Criado um novo rótulo de disco GPT (GUID: E0A674D5-EAA7-C44D-A4EC-48CE826AD628).

Comando (m para ajuda):

```
Crie as partições (atenção para não sobre escrever a assinatura da partição onde está o /):
```
Comando (m para ajuda): n
Número da partição (1-128, padrão 1):
Primeiro setor (2048-468877278, padrão 2048):
Último setor, +/-setores ou +/-tamanho{K,M,G,T,P} (2048-468877278, padrão 468875263): 234375167

Criada uma nova partição 1 do tipo "Linux filesystem" e de tamanho 111,8 GiB.
Partição nº 1: contém uma assinatura de ext4.

Deseja remover a assinatura? [S]im/[N]ão: N

Comando (m para ajuda): n
Número da partição (2-128, padrão 2): 2
Primeiro setor (234375168-468877278, padrão 234375168):
Último setor, +/-setores ou +/-tamanho{K,M,G,T,P} (234375168-468877278, padrão 468875263): 235475168

Criada uma nova partição 2 do tipo "Linux filesystem" e de tamanho 537,1 MiB.

Comando (m para ajuda): t
Número da partição (1,2, padrão 2):
Tipo de partição ou apelido (digite L para listar todos): 1

O tipo da partição "Linux filesystem" foi alterado para "EFI System".

Comando (m para ajuda):w
```

Agora devemos criar uma "assinatura", ou melhor, dizer para a partição criada para o efi qual será o seu formato de trabalho
```
mkfs.vfat /dev/sda2
```

Pronto, agora devemos montar a partição e de fato fazer a alteração que irá criar o conjunto de diretorios e irá carregar os arquivos necessários:
```
mount /dev/sda2 /mnt
```

Gerando estrutura para o efi:
```
grub-install --efi-directory=/mnt
```

Pronto, agora podemos desmontar a partição, e fazer o update do GRUB:
```
umount /mnt/
update-grub
```
Saída:
```
Generating grub configuration file ...
Found background image: /usr/share/images/desktop-base/desktop-grub.png
Found linux image: /boot/vmlinuz-6.1.0-12-amd64
Found initrd image: /boot/initrd.img-6.1.0-12-amd64
Found linux image: /boot/vmlinuz-6.1.0-11-amd64
Found initrd image: /boot/initrd.img-6.1.0-11-amd64
Found linux image: /boot/vmlinuz-6.1.0-9-amd64
Found initrd image: /boot/initrd.img-6.1.0-9-amd64
Adding boot menu entry for UEFI Firmware Settings ...
done
```

Por ultimo é importante atualizar o arquivo das tabelas do fstab, para isso devemos listar o *id* da nova partição:
```
blkid
```
Saída:
```
/dev/nvme0n1p3: PARTLABEL="Microsoft reserved partition" PARTUUID="82780749-b38f-4528-8704-4a94fc9b7dec"
/dev/nvme0n1p1: LABEL="RecuperaM-CM-'M-CM-#o" BLOCK_SIZE="512" UUID="028EFA968EFA8189" TYPE="ntfs" PARTLABEL="Basic data partition" PARTUUID="f816c34c-d2ad-497f-b746-6cabda7aa537"
/dev/nvme0n1p4: BLOCK_SIZE="512" UUID="46FEFE3AFEFE21BB" TYPE="ntfs" PARTLABEL="Basic data partition" PARTUUID="85a44392-6273-43f5-a622-624ec517d4d6"
/dev/nvme0n1p2: UUID="C6FB-FD89" BLOCK_SIZE="512" TYPE="vfat" PARTLABEL="EFI system partition" PARTUUID="90a58418-e90d-442f-b064-0b804bcae98b"
/dev/sda2: UUID="4F31-31E5" BLOCK_SIZE="512" TYPE="vfat" PARTUUID="3954f091-cdad-3c48-8488-bb07c155db6e"
/dev/sda1: UUID="fe0f6014-577d-4910-beaf-a65d1ecdf040" BLOCK_SIZE="4096" TYPE="ext4" PARTUUID="015d94b5-c7a5-9d42-bd1d-fdc095669e01"
```

Atualizando a tabela:
```
echo "UUID=4F31-31E5	/boot/efi	vfat	umask=0077	0	1 " >> /etc/fstab
```

Para conferir a alteração:
```
cat /etc/fstab
```
Saída:
```
# /etc/fstab: static file system information.
#
# Use 'blkid' to print the universally unique identifier for a
# device; this may be used with UUID= as a more robust way to name devices
# that works even if disks are added and removed. See fstab(5).
#
# systemd generates mount units based on this file, see systemd.mount(5).
# Please run 'systemctl daemon-reload' after making changes here.
#
# <file system> <mount point>   <type>  <options>       <dump>  <pass>
# / was on /dev/sda1 during installation
UUID=fe0f6014-577d-4910-beaf-a65d1ecdf040 /               ext4    errors=remount-ro 0       1
UUID=4F31-31E5	/boot/efi	vfat	umask=0077	0	1
```

Reinicie o sistema, e o GRUB deverá iniciar corretamente, dando as opções de boot.

