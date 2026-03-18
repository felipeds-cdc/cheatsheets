# 🐧 Kali Linux — Guia de Comandos
**github.com/felipeds-cdc**

---

## 📌 1. Comandos do Cotidiano

### Navegação e Arquivos
```bash
pwd                        # Mostra o diretório atual
ls -la                     # Lista arquivos com detalhes e ocultos
cd /caminho/pasta          # Navega para uma pasta
mkdir nome-pasta           # Cria uma pasta
rm -rf nome-pasta          # Remove pasta e tudo dentro (cuidado!)
cp arquivo destino         # Copia arquivo
mv arquivo destino         # Move ou renomeia arquivo
find / -name "arquivo"     # Busca arquivo no sistema inteiro
cat arquivo.txt            # Exibe conteúdo de arquivo
nano arquivo.txt           # Edita arquivo no terminal
chmod +x script.sh         # Torna script executável
```

### Sistema e Processos
```bash
sudo su                    # Vira root
whoami                     # Mostra usuário atual
uname -a                   # Info do sistema e kernel
top                        # Monitor de processos em tempo real
htop                       # Monitor visual (mais bonito que top)
ps aux                     # Lista todos os processos
kill -9 PID                # Força encerrar processo pelo ID
df -h                      # Espaço em disco
free -h                    # Uso de memória RAM
uptime                     # Tempo ligado + carga do sistema
history                    # Histórico de comandos usados
clear                      # Limpa o terminal
```

### Pacotes e Atualizações
```bash
sudo apt update            # Atualiza lista de pacotes
sudo apt upgrade -y        # Atualiza todos os pacotes
sudo apt install pacote    # Instala um pacote
sudo apt remove pacote     # Remove um pacote
sudo apt autoremove        # Remove pacotes desnecessários
dpkg -l | grep nome        # Verifica se pacote está instalado
```

---

## 🔧 2. Solução de Problemas

### Wi-Fi não está funcionando
```bash
ip a                              # Lista interfaces de rede
iwconfig                          # Mostra interfaces wireless
sudo ip link set wlan0 up         # Liga interface Wi-Fi
sudo systemctl restart NetworkManager  # Reinicia gerenciador de rede
nmcli dev status                  # Status de todas as conexões
nmcli radio wifi on               # Ativa rádio Wi-Fi
sudo rfkill list                  # Verifica se Wi-Fi está bloqueado
sudo rfkill unblock wifi          # Desbloqueia Wi-Fi
sudo rfkill unblock all           # Desbloqueia tudo (wifi + bluetooth)
dmesg | grep -i wifi              # Logs do sistema sobre Wi-Fi
lspci | grep -i wireless          # Detecta placa Wi-Fi
```

### Bluetooth não está funcionando
```bash
sudo systemctl start bluetooth     # Inicia serviço bluetooth
sudo systemctl enable bluetooth    # Ativa bluetooth no boot
sudo rfkill unblock bluetooth      # Desbloqueia bluetooth
bluetoothctl                       # Abre painel de controle bluetooth
  # Dentro do bluetoothctl:
  power on                         # Liga bluetooth
  scan on                          # Procura dispositivos
  pair XX:XX:XX:XX                 # Pareia dispositivo
  connect XX:XX:XX:XX              # Conecta dispositivo
hciconfig hci0 up                  # Ativa interface bluetooth manualmente
dmesg | grep -i bluetooth          # Logs do sistema sobre bluetooth
```

### Tela, Display e Driver
```bash
xrandr                             # Lista monitores e resoluções
xrandr --auto                      # Detecta monitores automaticamente
sudo apt install nvidia-driver     # Instala driver NVIDIA
lspci | grep -i vga                # Identifica placa de vídeo
sudo systemctl restart gdm3        # Reinicia interface gráfica
```

### Áudio não funciona
```bash
alsamixer                          # Mixer de áudio no terminal
pulseaudio --start                 # Inicia servidor de áudio
pulseaudio -k                      # Reinicia pulseaudio
pactl list sinks                   # Lista saídas de áudio
aplay -l                           # Lista dispositivos de áudio
```

---

## 🖥️ 3. Abrindo Aplicativos pelo Terminal

### Navegadores
```bash
firefox &                          # Abre Firefox
firefox https://google.com &       # Abre Firefox em um site
chromium &                         # Abre Chromium
tor-browser &                      # Abre Tor Browser
```

### Editores de Código
```bash
code .                             # Abre VS Code na pasta atual
code arquivo.py                    # Abre arquivo específico no VS Code
nano arquivo.py                    # Editor simples no terminal
vim arquivo.py                     # Editor avançado no terminal
mousepad arquivo.txt               # Editor gráfico padrão do Kali
```

### Ferramentas de Pentest
```bash
# Reconhecimento
nmap -sV 192.168.1.1              # Scan de versões de serviços
nmap -A 192.168.1.0/24            # Scan agressivo na rede
netdiscover -r 192.168.1.0/24    # Descobre hosts na rede
whois dominio.com                  # Info de domínio
dig dominio.com                    # Consulta DNS
theHarvester -d dominio.com -b google  # Coleta emails e subdomínios

# Análise de Rede
wireshark &                        # Abre Wireshark (GUI)
tcpdump -i eth0                    # Captura pacotes no terminal
netstat -tulnp                     # Portas abertas e processos
ss -tulnp                          # Alternativa moderna ao netstat

# Exploração
msfconsole                         # Abre Metasploit Framework
searchsploit termo                 # Busca exploits localmente
sqlmap -u "http://site.com?id=1"  # Testa SQL Injection

# Senhas e Hashes
hashcat -m 0 hash.txt wordlist.txt # Quebra hash MD5
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt  # John the Ripper
hydra -l admin -P senhas.txt ssh://192.168.1.1  # Força bruta SSH

# Web
nikto -h http://192.168.1.1       # Scanner de vulnerabilidades web
gobuster dir -u http://site.com -w /usr/share/wordlists/dirb/common.txt  # Força bruta de diretórios
burpsuite &                        # Abre Burp Suite (proxy web)

# Wireless
airmon-ng start wlan0             # Ativa modo monitor no Wi-Fi
airodump-ng wlan0mon              # Captura redes Wi-Fi
```

---

## 😮 4. Comandos Surpreendentes

### O sistema explicando o que você digitou errado
```bash
thefuck                            # Corrige automaticamente o último comando errado
# Exemplo: digitou "gut status" → thefuck → vira "git status"
```

### Terminal com efeito Matrix
```bash
cmatrix                            # Exibe chuva de caracteres estilo Matrix
cmatrix -C red                     # Em vermelho
```

### Ouvir o tráfego de rede como som
```bash
pingSounds                         # Converte pings em sons (raridade)
```

### Ver a previsão do tempo no terminal
```bash
curl wttr.in/SaoPaulo              # Previsão do tempo de SP no terminal
curl wttr.in/SaoPaulo?format=3    # Versão resumida em uma linha
```

### Fazer o terminal falar
```bash
espeak "texto aqui"                # Sintetiza voz no terminal
espeak "Sistema comprometido"      # Clássico hacker moment
```

### IP público direto no terminal
```bash
curl ifconfig.me                   # Mostra seu IP público
curl ipinfo.io                     # IP + localização + provedor
```

### Escanear vulnerabilidades com uma linha
```bash
nmap --script vuln 192.168.1.1    # Roda scripts de vulnerabilidades no alvo
```

### Ver rotas de rede de forma visual
```bash
traceroute google.com              # Mostra cada salto até o destino
mtr google.com                     # Traceroute em tempo real e interativo
```

### Monitorar rede em tempo real visualmente
```bash
iftop                              # Monitor de banda por conexão em tempo real
nethogs                            # Mostra qual processo consome mais rede
```

### Gerar senha forte no terminal
```bash
openssl rand -base64 32            # Gera senha aleatória de 32 caracteres
```

### Esconder um arquivo dentro de uma imagem
```bash
steghide embed -cf foto.jpg -ef segredo.txt   # Esconde arquivo em imagem
steghide extract -sf foto.jpg                  # Extrai arquivo escondido
```

---

## ⚠️ Aviso Legal
> Utilize estas ferramentas apenas em ambientes autorizados.
> O uso não autorizado configura crime (Lei 12.737/2012).
