# 🐙 Git & GitHub — Guia Completo de Comandos
**github.com/felipeds-cdc**

---

## ⚙️ 1. CONFIGURAÇÃO INICIAL
```bash
# Identidade — obrigatório antes do primeiro commit
git config --global user.name  "Felipe Diassis"
git config --global user.email "felipe.ds@uni9.edu.br"

# Editor padrão
git config --global core.editor "code --wait"   # VS Code
git config --global core.editor "nano"           # Nano

# Ver todas as configurações
git config --list
git config user.name                             # Ver config específica

# Configurar chave SSH (recomendado para GitHub)
ssh-keygen -t ed25519 -C "felipe.ds@uni9.edu.br"
cat ~/.ssh/id_ed25519.pub                        # Copiar e colar no GitHub
ssh -T git@github.com                            # Testar conexão SSH
```

---

## 🏁 2. INICIANDO REPOSITÓRIO
```bash
# Criar repositório local
git init                                         # Na pasta atual
git init nome-projeto                            # Cria pasta + repositório

# Clonar repositório existente
git clone https://github.com/user/repo.git
git clone git@github.com:user/repo.git           # Via SSH (recomendado)
git clone https://github.com/user/repo.git pasta # Clona em pasta específica
git clone --depth 1 https://github.com/user/repo # Clona só último commit
```

---

## 📸 3. COMMITS — O DIA A DIA
```bash
# Ver status atual
git status
git status -s                                    # Versão resumida

# Adicionar arquivos para commit
git add arquivo.py                               # Arquivo específico
git add pasta/                                   # Pasta inteira
git add .                                        # Tudo modificado
git add *.py                                     # Todos arquivos .py
git add -p                                       # Interativo — escolhe partes

# Remover da área de stage (desfaz git add)
git restore --staged arquivo.py
git reset HEAD arquivo.py                        # Alternativa mais antiga

# Fazer commit
git commit -m "feat: adiciona port scanner em python"
git commit -am "fix: corrige bug no scanner"     # Add + commit em um comando
git commit --amend -m "mensagem corrigida"       # Edita último commit

# Ver histórico
git log
git log --oneline                                # Resumido, uma linha por commit
git log --oneline --graph --all                  # Visual com branches
git log --author="Felipe"                        # Filtrar por autor
git log --since="2026-01-01"                     # A partir de uma data
git log -p arquivo.py                            # Histórico de um arquivo
git log --stat                                   # Arquivos alterados em cada commit
```

---

## 🌿 4. BRANCHES
```bash
# Listar branches
git branch                                       # Branches locais
git branch -r                                    # Branches remotas
git branch -a                                    # Todas

# Criar branch
git branch nome-branch
git checkout -b nome-branch                      # Cria e já muda para ela
git switch -c nome-branch                        # Forma moderna

# Mudar de branch
git checkout nome-branch
git switch nome-branch                           # Forma moderna

# Renomear branch
git branch -m nome-antigo nome-novo
git branch -m nome-novo                          # Renomeia a branch atual

# Deletar branch
git branch -d nome-branch                        # Seguro — só se já mergeada
git branch -D nome-branch                        # Força deletar

# Deletar branch remota
git push origin --delete nome-branch
```

---

## 🔀 5. MERGE E REBASE
```bash
# Merge — une branch na atual
git merge nome-branch
git merge --no-ff nome-branch                    # Força criar commit de merge
git merge --squash nome-branch                   # Une todos commits em um só
git merge --abort                                # Cancela merge com conflito

# Rebase — reescreve histórico
git rebase main                                  # Rebasa branch atual em main
git rebase --interactive HEAD~3                  # Edita últimos 3 commits
git rebase --abort                               # Cancela rebase
git rebase --continue                            # Continua após resolver conflito

# Cherry-pick — pega commit específico de outra branch
git cherry-pick abc1234                          # Aplica commit pelo hash
git cherry-pick abc1234..def5678                 # Range de commits
```

---

## 🌐 6. REMOTO — GITHUB
```bash
# Gerenciar remotos
git remote -v                                    # Lista remotos configurados
git remote add origin git@github.com:user/repo.git
git remote remove origin
git remote rename origin upstream
git remote set-url origin git@github.com:user/novo-repo.git

# Enviar para o GitHub
git push origin main                             # Envia branch main
git push origin nome-branch                      # Envia branch específica
git push -u origin main                          # Define upstream (primeira vez)
git push --force                                 # Força push (cuidado!)
git push --force-with-lease                      # Force push seguro
git push origin --tags                           # Envia tags

# Receber do GitHub
git fetch origin                                 # Baixa mas não aplica
git fetch --all                                  # Baixa todos os remotos
git pull origin main                             # Fetch + merge
git pull --rebase origin main                    # Fetch + rebase

# Ver diferença entre local e remoto
git fetch origin
git diff main origin/main
```

---

## 🏷️ 7. TAGS — VERSÕES
```bash
# Criar tag
git tag v1.0                                     # Tag simples
git tag -a v1.0 -m "Versão 1.0 estável"        # Tag anotada (recomendada)
git tag -a v1.0 abc1234 -m "Tag em commit antigo"

# Listar e ver tags
git tag
git tag -l "v1.*"                                # Filtra por padrão
git show v1.0

# Enviar tags
git push origin v1.0                             # Tag específica
git push origin --tags                           # Todas as tags

# Deletar tag
git tag -d v1.0                                  # Local
git push origin --delete v1.0                    # Remota
```

---

## 💾 8. STASH — GUARDAR TRABALHO TEMPORÁRIO
```bash
# Guardar modificações sem commitar
git stash                                        # Guarda tudo
git stash push -m "trabalho em progresso"        # Com descrição
git stash push -u                                # Inclui arquivos novos

# Listar stashes
git stash list

# Recuperar stash
git stash pop                                    # Aplica e remove da lista
git stash apply stash@{0}                        # Aplica mas mantém na lista
git stash apply stash@{2}                        # Stash específico

# Remover stash
git stash drop stash@{0}                         # Remove um
git stash clear                                  # Remove todos
```

---

## 🔍 9. DIFF E COMPARAÇÕES
```bash
# Ver o que mudou
git diff                                         # Não staged vs working
git diff --staged                                # Staged vs último commit
git diff HEAD                                    # Tudo vs último commit
git diff main feature-branch                     # Entre duas branches
git diff abc1234 def5678                         # Entre dois commits
git diff HEAD~1 HEAD                             # Último vs penúltimo commit

# Ver arquivos modificados
git diff --name-only
git diff --name-status

# Comparar arquivo específico
git diff HEAD arquivo.py
git diff main..feature -- arquivo.py
```

---

## ⏪ 10. DESFAZENDO COISAS
```bash
# Descartar mudanças no arquivo (antes do git add)
git restore arquivo.py
git checkout -- arquivo.py                       # Forma antiga

# Desfazer git add
git restore --staged arquivo.py
git reset HEAD arquivo.py

# Desfazer último commit (mantém mudanças)
git reset --soft HEAD~1

# Desfazer último commit (descarta mudanças do stage)
git reset --mixed HEAD~1

# Desfazer último commit (descarta TUDO — irreversível)
git reset --hard HEAD~1

# Voltar para commit específico
git reset --hard abc1234

# Criar commit que desfaz outro (seguro para remoto)
git revert abc1234
git revert HEAD                                  # Reverte último commit
git revert HEAD~3..HEAD                          # Reverte últimos 3 commits

# Recuperar arquivo deletado
git checkout HEAD -- arquivo.py
git restore --source=HEAD~1 arquivo.py           # De commit anterior
```

---

## 🔎 11. BUSCA NO HISTÓRICO
```bash
# Buscar texto em todos os arquivos
git grep "senha"
git grep -n "TODO"                               # Mostra número da linha
git grep -i "password"                           # Case insensitive

# Buscar em qual commit um texto apareceu
git log -S "texto_buscado" --oneline

# Buscar por mensagem de commit
git log --grep="fix"
git log --grep="feat" --oneline

# Descobrir quem modificou uma linha (blame)
git blame arquivo.py
git blame -L 10,20 arquivo.py                    # Só linhas 10 a 20

# Bissect — encontrar qual commit causou um bug
git bisect start
git bisect bad                                   # Commit atual tem o bug
git bisect good abc1234                          # Esse commit estava bom
# Git vai navegando automaticamente
git bisect reset                                 # Finaliza bisect
```

---

## 📦 12. SUBMODULES
```bash
# Adicionar submodule
git submodule add https://github.com/user/repo libs/repo

# Clonar repositório com submodules
git clone --recurse-submodules https://github.com/user/repo

# Atualizar submodules
git submodule update --init --recursive
git submodule update --remote                    # Atualiza para último commit

# Remover submodule
git submodule deinit libs/repo
git rm libs/repo
```

---

## 🛠️ 13. RESOLVENDO PROBLEMAS
```bash
# ---- Conflito de merge ----
# 1. Abrir arquivo com conflito
# 2. Editar manualmente — remover marcações <<< === >>>
# 3. Salvar o arquivo
git add arquivo_resolvido.py
git commit -m "fix: resolve conflito no merge"

# ---- Commit no branch errado ----
# Mover último commit para outra branch
git checkout branch-correta
git cherry-pick main
git checkout main
git reset --hard HEAD~1

# ---- Esqueceu de adicionar arquivo no último commit ----
git add arquivo_esquecido.py
git commit --amend --no-edit                     # Adiciona sem mudar mensagem

# ---- Push rejeitado (remote à frente do local) ----
git pull --rebase origin main
git push origin main

# ---- Repositório corrompido ----
git fsck                                         # Verifica integridade
git gc                                           # Coleta lixo e otimiza

# ---- Limpar arquivos não rastreados ----
git clean -n                                     # Simula o que seria removido
git clean -f                                     # Remove arquivos não rastreados
git clean -fd                                    # Remove arquivos e pastas
git clean -fdx                                   # Inclui arquivos no .gitignore

# ---- Recuperar branch deletada por acidente ----
git reflog                                       # Mostra todo o histórico
git checkout -b branch-recuperada abc1234        # Recria do hash encontrado

# ---- Desfazer push já enviado ao GitHub ----
git revert HEAD
git push origin main
# Nunca usar git push --force em branch compartilhada

# ---- Arquivo grande bloqueando push ----
git rm --cached arquivo-grande.zip
echo "arquivo-grande.zip" >> .gitignore
git commit -m "fix: remove arquivo grande do tracking"

# ---- Ver o que foi deletado no histórico ----
git log --diff-filter=D --summary               # Commits que deletaram arquivos
git show abc1234 -- arquivo-deletado.py         # Ver conteúdo antes de deletar
```

---

## 📄 14. .GITIGNORE
```bash
# Criar .gitignore
touch .gitignore

# Parar de rastrear arquivo já commitado
git rm --cached arquivo.py
git rm --cached -r pasta/

# Verificar por que um arquivo está sendo ignorado
git check-ignore -v arquivo.py

# Modelo de .gitignore para projetos de segurança / Python:
```
```gitignore
# Python
__pycache__/
*.py[cod]
*.egg-info/
.env
venv/
.venv/

# Segurança — NUNCA commitar
*.key
*.pem
*.cert
*.pfx
id_rsa
id_ed25519
.env
config.ini
secrets.yaml
passwords.txt

# Capturas de rede
*.pcap
*.pcapng

# Sistemas
.DS_Store
Thumbs.db
*.log

# IDEs
.vscode/
.idea/
*.swp
```

---

## 💡 15. BOAS PRÁTICAS DE COMMIT
```bash
# Padrão Conventional Commits — muito usado na área
feat:     nova funcionalidade
fix:      correção de bug
docs:     documentação
style:    formatação, sem mudança de lógica
refactor: refatoração de código
test:     adição de testes
chore:    tarefas de manutenção

# Exemplos reais:
git commit -m "feat: adiciona port scanner com threading"
git commit -m "fix: corrige timeout no scan UDP"
git commit -m "docs: adiciona README do xor_encryptor"
git commit -m "chore: adiciona .gitignore para arquivos .pcap"
```

---

## 🚀 16. FLUXO COMPLETO — DO ZERO AO GITHUB
```bash
# 1. Criar repositório local
git init meu-projeto
cd meu-projeto

# 2. Criar arquivo inicial
echo "# Meu Projeto" > README.md

# 3. Primeiro commit
git add .
git commit -m "feat: commit inicial"

# 4. Conectar ao GitHub
git remote add origin git@github.com:felipeds-cdc/meu-projeto.git

# 5. Enviar
git push -u origin main

# --- Fluxo diário ---
git pull origin main                             # Sempre atualizar antes
# ... faz modificações ...
git add .
git commit -m "feat: descreve o que fez"
git push origin main
```

---

## ⚠️ Aviso Legal
> Nunca commitar senhas, chaves privadas,
> tokens de API ou arquivos .env.
> Use sempre o .gitignore para proteger
> informações sensíveis.
