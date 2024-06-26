<i>
<h1>Introdução ao Gentoo Linux</h1><br>
<center>O Gentoo é uma distribuição linux de instalação manual, onde você tem liberdade para fazer configurações pré-instalação do kernel tanto quanto o grub.<br>
Você também tem liberdade de escolher o seu gerenciador de serviços, interface gráfica ou gerenciador de janelas.<br>
Um detalhe importante ao iniciar no gentoo é que a compilação de todos os pacotes e dependências são feitas localmente, trazendo mais estabilidade para o usuário.
</center>
<h1> 1. Particionando e formatando o disco </h1><br>
Vamos prosseguir utilizando um modelo simples de particionamento, onde vou criar uma partição para boot, uma para o root (raíz do sistema), e por fim<br>
uma partição swap, que será uma camada de proteção para o armazenamento do disco.<br>
Ferramenta utilizada para particionamento: fdisk</i><br><br>

```python
livecd ~ # fdisk -l /dev/sda
Disk /dev/sda: 49.79 GiB, 5000204 bytes, 1025352 sectors
Disk model: VBOX HARDDISK
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: 3E56EE74-0571-462B-A992-9872E3855D75

Device        Start        End    Sectors   Size Type
/dev/sda1      2048    2099199    2097152     1G EFI System
/dev/sda2   2099200   10487807    8388608     4G Linux swap
/dev/sda3  10487808 1953523711 1943035904 926.5G Linux root (x86-64)
```
<i>
Acima podemos visualizar meu particionamento e formatação atual do disco, no meu caso, irei instalar o gentoo em todo o disco<br>
portanto vou remover todas as partições, utilizando o comando "d"
</i><br><br>

```python
Command (m for help):d
Partition number (1-4): 1

Command (m for help):p
Disk /dev/sda: 49.79 GiB, 5000204 bytes, 1025352 sectors
Disk model: VBOX HARDDISK
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: 3E56EE74-0571-462B-A992-9872E3855D75
```
<i>
Feito isso, vamos começar a particionar novamente o disco, vou deixar uma tabela abaixo com os comandos e suas respectivas finalidades; Abaixo outro bloco com a sequência realizada.
</i><br><br>

```python
Command (m for help):n
 * Comando utilizado para criar uma nova particição, ele vai pedir para determinar o tipo
de partição (primary ou extended) e depois o seu tamanho.

Command (m for help):t
 * Comando utilizado para definir o tipo de uma partição (swap, filesystem, EFI...)

Command (m for help):w
 * Escreve todas as mudanças no disco.
```

<hr>

```python
Command (m for help):n 
Partition type
   p   primary (0 primary, 0 extended, 4 free)
   e   extended (container for logical partitions)
Select (default p): p
Partition number (1-4, default 1): 1
First sector (2048-1953525167, default 2048):
Last sector, +/-sectors or +/-size{K,M,G,T,P} (2048-1953525167, default 1953525167): +1G

Created a new partition 1 of type 'Linux' and of size 1 GiB.

Command (m for help):n 
Partition type
   p   primary (0 primary, 0 extended, 4 free)
   e   extended (container for logical partitions)
Select (default p): p
Partition number (2-4, default 1): 2
First sector (2099200-1953525167, default 2099200):
Last sector, +/-sectors or +/-size{K,M,G,T,P} (2099200-1953525167, default 1953525167): +4G

Created a new partition 2 of type 'Linux' and of size 4 GiB.

Command (m for help):t
Partition number (1,2, default 2): 2
Hex code (type L to list all codes):19

Changed type of partition 'Linux' to 'Linux swap'.

Command (m for help):n
Partition type
   p   primary (2 primary, 0 extended, 2 free)
   e   extended (container for logical partitions)
Select (default p): p
Partition number (3,4, default 3): 3
First sector (10487808-1953525167, default 10487808):
Last sector, +/-sectors or +/-size{K,M,G,T,P} (10487808-1953525167, default 1953525167):

Created a new partition 3 of type 'Linux' and of size 44.5 GiB.

Command (m for help):w
The partition table has been altered.
Calling ioctl() to re-read partition table.
Syncing disks.

```
