# Modulo Realtek RTL8188FTV usb Wi-Fi Dongle

Esse pequeno tutorial, irá demonstrar como instalar o modulo e firmware no kernel para o funcionamento do Dongle Genérico de Wi-Fi da Realtek

## Repositório

Baixar o repositório do github com os pacotes necessários:
```
$ git clone https://github.com/kelebek333/rtl8188fu.git
```
Obs.: foi usado o commit 0fc73d1df6b9a71f70cc360ab816b30ce0a18ad4

## Instalação e configuração

No terminal, no mesmo local onde o repositório foi clonado, preparar os pacotes via dkms:
```
$ sudo dkms install ./rtl8188fu
$ sudo dkms status
rtl8188fu/1.0, 6.1.0-11-amd64, x86_64: installed
```

Adicionar o módulo:
```
$ sudo modprobe rtl8188fu
```

Listando o novo módulo:
```
$ lsmod | grep rtl
rtl8188fu            1429504  0
cfg80211             1134592  1 rtl8188fu
usbcore               348160  4 xhci_hcd,usbhid,xhci_pci,rtl8188fu
```

## Adicionando os firmwares

Crie a pasta que irá armazenar o firmware e mover para lá:
```
$ sudo mkdir -p /lib/firmware/iwlwifi
$ sudo cp rtl8188fu/firmware/rtl8188fufw.bin /lib/firmware/iwlwifi/
```

## Adicionando gerenciadores da Realtek

No terminal rode os comandos:
```
$ sudo apt install firmware-realtek 
$ sudo apt install firmware-misc-nonfree
```

## Configuração extra do modulo

É necessário a configuração que desabilita o gerenciamento de energia e questões de "plug e desplug":
```
echo "options rtl8188fu rtw_power_mgnt=0 rtw_enusbss=0 rtw_ips_mode=0" | sudo tee /etc/modprobe.d/rtl8188fu.conf
```

## Configurando a conexão com a rede

Por hora estou usando no terminal o aplicativo *nmtui*, que possui uma interface interessante e de fácil uso, basta adicionar uma conexão, colocar a senha e teremos acesso via WiFi.
