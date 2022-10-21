# Eternalblue Doublepulsar (MS17-010)

Explorando Windows com EternalBlue (MS17-010) sem Metasploit utilizando Kali Linux 2022.3.

Testado em:

- [como explorar](win7xp.md#anchortext) Windows 7 Ultimate 7601 Service Pack 1 (32 bits)
- [como explorar](win7xp.md#anchortext) Windows 7 Professional 7601 Service Pack 1 (64 bits)
- [como explorar](win7xp.md#anchortext) Windows XP Professional 2600 Service Pack 2 (32 bits)
- [como explorar](win8.md#anchortext) Windows Server 2008 Enterprise 6001 Service Pack 1 (32 bits)

#

### Preparando a máquina atacante:
Adicione a arquitetura i386 (para computadores 32 bits) no repositório.
```
dpkg --add-architecture i386
```
```
apt-get update
```
<br>

Realize a instalação dos pacotes libwine, wine, wine32 e winetricks.
```
apt-get install libwine wine wine32 winetricks
```
<br>

Após a instalação certifique-se que o **Wine** esteja instalado, em seguida execute o comando **exit** para sair do **Wine**.
```
wine cmd
```
<br>

Realize a correção do impacket utilizando pimpmykali (para utilizar os exploits python2)
<br>

https://github.com/Dewalt-arch/pimpmykali
