##Adicionando usuario ao grupo root
```
sudo su
echo "silva   ALL=(ALL:ALL) ALL" > /etc/sudoers.d/silva
```

##Editando fontes do *apt*
Acessar o arquivo e comentar a linha referente ao live CD
```
vi /etc/apt/sources.list

#deb cdrom:[Debian GNU/Linux 12.0.0 _Bookworm_ - Official amd64 DVD Binary-1 with firmware 20230610-10:23]/ bookworm main non-free-firmware
```
