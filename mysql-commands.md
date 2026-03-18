# 🗄️ MySQL — Guia Completo de Comandos
**github.com/felipeds-cdc**

---

## 🔌 1. CONEXÃO E ACESSO
```sql
-- Conectar ao MySQL
mysql -u root -p                          -- Login como root
mysql -u usuario -p banco_de_dados        -- Login direto em um banco
mysql -h 192.168.1.1 -u root -p          -- Conectar em host remoto
mysql -u root -p --port=3307             -- Porta customizada

-- Verificar versão
SELECT VERSION();
mysql --version                           -- No terminal, fora do MySQL

-- Sair
EXIT;
QUIT;
\q
```

---

## 📁 2. BANCOS DE DADOS
```sql
-- Listar e usar
SHOW DATABASES;                           -- Lista todos os bancos
USE nome_banco;                           -- Seleciona banco
SELECT DATABASE();                        -- Banco atual

-- Criar e remover
CREATE DATABASE nome_banco;
CREATE DATABASE nome_banco
  CHARACTER SET utf8mb4
  COLLATE utf8mb4_unicode_ci;            -- Com suporte a emojis e acentos
DROP DATABASE nome_banco;
DROP DATABASE IF EXISTS nome_banco;      -- Sem erro se não existir

-- Backup e restore
-- No terminal (fora do MySQL):
mysqldump -u root -p banco > backup.sql           -- Exporta banco
mysqldump -u root -p banco tabela > tabela.sql    -- Exporta só uma tabela
mysqldump -u root -p --all-databases > tudo.sql   -- Exporta tudo
mysql -u root -p banco < backup.sql               -- Importa banco
```

---

## 📋 3. TABELAS
```sql
-- Listar e descrever
SHOW TABLES;                              -- Lista tabelas do banco atual
DESCRIBE tabela;                          -- Estrutura da tabela
DESC tabela;                              -- Atalho para DESCRIBE
SHOW CREATE TABLE tabela;                 -- SQL que criou a tabela
SHOW TABLE STATUS;                        -- Info detalhada de todas as tabelas
SHOW TABLE STATUS LIKE 'nome%';          -- Filtra por nome

-- Criar tabela
CREATE TABLE usuarios (
    id         INT AUTO_INCREMENT PRIMARY KEY,
    nome       VARCHAR(100)     NOT NULL,
    email      VARCHAR(150)     UNIQUE NOT NULL,
    senha      VARCHAR(255)     NOT NULL,
    perfil     ENUM('admin','user','guest') DEFAULT 'user',
    ativo      TINYINT(1)       DEFAULT 1,
    criado_em  TIMESTAMP        DEFAULT CURRENT_TIMESTAMP,
    atualizado TIMESTAMP        DEFAULT CURRENT_TIMESTAMP
                                ON UPDATE CURRENT_TIMESTAMP
);

-- Remover tabela
DROP TABLE tabela;
DROP TABLE IF EXISTS tabela;
TRUNCATE TABLE tabela;                    -- Remove todos os dados, mantém estrutura

-- Renomear
RENAME TABLE nome_antigo TO nome_novo;

-- Copiar estrutura
CREATE TABLE tabela_nova LIKE tabela_original;

-- Copiar estrutura + dados
CREATE TABLE tabela_nova
  SELECT * FROM tabela_original;
```

---

## 🔧 4. ALTERAÇÕES EM TABELAS (ALTER)
```sql
-- Adicionar coluna
ALTER TABLE tabela ADD COLUMN telefone VARCHAR(20);
ALTER TABLE tabela ADD COLUMN idade INT AFTER nome;      -- Posição específica
ALTER TABLE tabela ADD COLUMN codigo INT FIRST;          -- Primeira posição

-- Modificar coluna
ALTER TABLE tabela MODIFY COLUMN nome VARCHAR(200) NOT NULL;
ALTER TABLE tabela CHANGE nome_antigo nome_novo VARCHAR(200);

-- Remover coluna
ALTER TABLE tabela DROP COLUMN coluna;

-- Adicionar índice
ALTER TABLE tabela ADD INDEX idx_email (email);
ALTER TABLE tabela ADD UNIQUE INDEX idx_cpf (cpf);
ALTER TABLE tabela ADD PRIMARY KEY (id);

-- Remover índice
ALTER TABLE tabela DROP INDEX idx_email;

-- Adicionar chave estrangeira
ALTER TABLE pedidos
  ADD CONSTRAINT fk_usuario
  FOREIGN KEY (usuario_id)
  REFERENCES usuarios(id)
  ON DELETE CASCADE
  ON UPDATE CASCADE;

-- Remover chave estrangeira
ALTER TABLE pedidos DROP FOREIGN KEY fk_usuario;
```

---

## 📝 5. CRUD — OPERAÇÕES BÁSICAS
```sql
-- ---- INSERT ----
INSERT INTO usuarios (nome, email, senha)
  VALUES ('Felipe', 'felipe@email.com', SHA2('senha123', 256));

-- Múltiplos registros de uma vez
INSERT INTO usuarios (nome, email, senha) VALUES
  ('Ana',   'ana@email.com',   SHA2('senha1', 256)),
  ('Bruno', 'bruno@email.com', SHA2('senha2', 256)),
  ('Carla', 'carla@email.com', SHA2('senha3', 256));

-- Inserir ou atualizar se já existir
INSERT INTO usuarios (id, nome, email)
  VALUES (1, 'Felipe Atualizado', 'felipe@email.com')
  ON DUPLICATE KEY UPDATE
    nome  = VALUES(nome),
    email = VALUES(email);

-- ---- SELECT ----
SELECT * FROM usuarios;
SELECT nome, email FROM usuarios;
SELECT DISTINCT perfil FROM usuarios;             -- Sem duplicatas
SELECT * FROM usuarios LIMIT 10;
SELECT * FROM usuarios LIMIT 10 OFFSET 20;       -- Paginação
SELECT * FROM usuarios ORDER BY nome ASC;
SELECT * FROM usuarios ORDER BY criado_em DESC;
SELECT * FROM usuarios WHERE ativo = 1;
SELECT * FROM usuarios WHERE nome LIKE 'Fe%';     -- Começa com Fe
SELECT * FROM usuarios WHERE email LIKE '%@gmail%';
SELECT * FROM usuarios WHERE id IN (1, 2, 3);
SELECT * FROM usuarios WHERE id BETWEEN 5 AND 10;
SELECT * FROM usuarios WHERE telefone IS NULL;
SELECT * FROM usuarios WHERE telefone IS NOT NULL;

-- ---- UPDATE ----
UPDATE usuarios SET ativo = 0 WHERE id = 5;
UPDATE usuarios SET
  nome  = 'Felipe Novo',
  email = 'novo@email.com'
WHERE id = 1;

-- Atualizar com base em outra tabela
UPDATE usuarios u
  JOIN pedidos p ON u.id = p.usuario_id
  SET u.ativo = 0
  WHERE p.status = 'cancelado';

-- ---- DELETE ----
DELETE FROM usuarios WHERE id = 5;
DELETE FROM usuarios WHERE ativo = 0;
DELETE FROM usuarios
  WHERE criado_em < DATE_SUB(NOW(), INTERVAL 1 YEAR);  -- Mais de 1 ano
```

---

## 🔗 6. JOINS — COMBINANDO TABELAS
```sql
-- INNER JOIN — só registros que existem nos dois lados
SELECT u.nome, p.valor, p.status
  FROM usuarios u
  INNER JOIN pedidos p ON u.id = p.usuario_id;

-- LEFT JOIN — todos da esquerda, mesmo sem correspondência
SELECT u.nome, p.valor
  FROM usuarios u
  LEFT JOIN pedidos p ON u.id = p.usuario_id;

-- Usuários SEM pedidos
SELECT u.nome
  FROM usuarios u
  LEFT JOIN pedidos p ON u.id = p.usuario_id
  WHERE p.id IS NULL;

-- RIGHT JOIN — todos da direita
SELECT u.nome, p.valor
  FROM usuarios u
  RIGHT JOIN pedidos p ON u.id = p.usuario_id;

-- Múltiplos JOINs
SELECT
    u.nome       AS cliente,
    p.valor      AS valor_pedido,
    pr.nome      AS produto,
    e.status     AS entrega
  FROM usuarios u
  INNER JOIN pedidos     p  ON u.id  = p.usuario_id
  INNER JOIN produtos    pr ON pr.id = p.produto_id
  LEFT  JOIN entregas    e  ON e.id  = p.entrega_id
  WHERE u.ativo = 1
  ORDER BY p.criado_em DESC;
```

---

## 📊 7. FUNÇÕES DE AGREGAÇÃO
```sql
-- Contagem
SELECT COUNT(*)             FROM usuarios;
SELECT COUNT(telefone)      FROM usuarios;        -- Ignora NULL
SELECT COUNT(DISTINCT perfil) FROM usuarios;

-- Matemática
SELECT SUM(valor)           FROM pedidos;
SELECT AVG(valor)           FROM pedidos;
SELECT MAX(valor)           FROM pedidos;
SELECT MIN(valor)           FROM pedidos;

-- Agrupamento
SELECT perfil, COUNT(*) AS total
  FROM usuarios
  GROUP BY perfil;

SELECT
    u.nome,
    COUNT(p.id)   AS total_pedidos,
    SUM(p.valor)  AS valor_total,
    AVG(p.valor)  AS ticket_medio
  FROM usuarios u
  LEFT JOIN pedidos p ON u.id = p.usuario_id
  GROUP BY u.id
  HAVING total_pedidos > 5              -- Filtra APÓS agrupar
  ORDER BY valor_total DESC;
```

---

## 🧮 8. FUNÇÕES ÚTEIS
```sql
-- ---- Texto ----
SELECT UPPER(nome)                FROM usuarios;   -- Maiúsculas
SELECT LOWER(email)               FROM usuarios;   -- Minúsculas
SELECT LENGTH(nome)               FROM usuarios;   -- Tamanho
SELECT CONCAT(nome, ' - ', email) FROM usuarios;   -- Concatenar
SELECT SUBSTRING(nome, 1, 3)      FROM usuarios;   -- Primeiros 3 chars
SELECT TRIM(nome)                 FROM usuarios;   -- Remove espaços
SELECT REPLACE(email, '@', ' at ') FROM usuarios;  -- Substituir
SELECT LEFT(nome, 5)              FROM usuarios;   -- 5 primeiros chars
SELECT RIGHT(email, 10)           FROM usuarios;   -- 10 últimos chars

-- ---- Data e Hora ----
SELECT NOW();                                       -- Data e hora atual
SELECT CURDATE();                                   -- Data atual
SELECT CURTIME();                                   -- Hora atual
SELECT DATE(criado_em)           FROM usuarios;    -- Só a data
SELECT YEAR(criado_em)           FROM usuarios;    -- Só o ano
SELECT MONTH(criado_em)          FROM usuarios;    -- Só o mês
SELECT DAY(criado_em)            FROM usuarios;    -- Só o dia
SELECT DATEDIFF(NOW(), criado_em) FROM usuarios;   -- Dias desde criação
SELECT DATE_FORMAT(criado_em, '%d/%m/%Y %H:%i') FROM usuarios;
SELECT DATE_ADD(NOW(), INTERVAL 30 DAY);           -- Daqui 30 dias
SELECT DATE_SUB(NOW(), INTERVAL 1 YEAR);           -- 1 ano atrás

-- ---- Condicionais ----
SELECT nome,
  IF(ativo = 1, 'Ativo', 'Inativo') AS status
  FROM usuarios;

SELECT nome,
  CASE perfil
    WHEN 'admin' THEN '👑 Administrador'
    WHEN 'user'  THEN '👤 Usuário'
    ELSE              '👁 Visitante'
  END AS perfil_label
  FROM usuarios;

SELECT COALESCE(telefone, 'Não informado') FROM usuarios;  -- Substitui NULL
SELECT IFNULL(telefone, 'Sem telefone')    FROM usuarios;  -- Idem
SELECT NULLIF(status, 'pendente')          FROM pedidos;   -- Retorna NULL se igual
```

---

## ⚡ 9. ÍNDICES E PERFORMANCE
```sql
-- Verificar índices
SHOW INDEX FROM tabela;

-- Criar índices
CREATE INDEX idx_nome        ON usuarios(nome);
CREATE UNIQUE INDEX idx_email ON usuarios(email);
CREATE INDEX idx_composto     ON pedidos(usuario_id, status);  -- Índice composto

-- Remover índice
DROP INDEX idx_nome ON usuarios;

-- EXPLAIN — analisar performance de query
EXPLAIN SELECT * FROM usuarios WHERE email = 'teste@email.com';
EXPLAIN FORMAT=JSON SELECT * FROM usuarios WHERE email = 'teste@email.com';

-- Ver queries lentas
SET GLOBAL slow_query_log = 'ON';
SET GLOBAL long_query_time = 2;           -- Queries acima de 2 segundos
SHOW VARIABLES LIKE 'slow_query%';

-- Otimizar tabela
OPTIMIZE TABLE tabela;
ANALYZE TABLE tabela;

-- Cache de queries
SHOW STATUS LIKE 'Qcache%';
```

---

## 👤 10. USUÁRIOS E PERMISSÕES
```sql
-- Listar usuários
SELECT user, host FROM mysql.user;

-- Criar usuário
CREATE USER 'felipe'@'localhost' IDENTIFIED BY 'senha_forte';
CREATE USER 'felipe'@'%'         IDENTIFIED BY 'senha_forte'; -- Acesso remoto

-- Dar permissões
GRANT ALL PRIVILEGES ON *.* TO 'felipe'@'localhost';          -- Tudo em tudo
GRANT ALL PRIVILEGES ON banco.* TO 'felipe'@'localhost';      -- Tudo em um banco
GRANT SELECT, INSERT ON banco.tabela TO 'felipe'@'localhost'; -- Específico

-- Ver permissões
SHOW GRANTS FOR 'felipe'@'localhost';

-- Revogar permissões
REVOKE INSERT ON banco.tabela FROM 'felipe'@'localhost';
REVOKE ALL PRIVILEGES ON *.* FROM 'felipe'@'localhost';

-- Alterar senha
ALTER USER 'felipe'@'localhost' IDENTIFIED BY 'nova_senha';

-- Remover usuário
DROP USER 'felipe'@'localhost';

-- Aplicar mudanças
FLUSH PRIVILEGES;
```

---

## 🔍 11. SUBQUERIES E AVANÇADO
```sql
-- Subquery no WHERE
SELECT nome FROM usuarios
  WHERE id IN (
    SELECT usuario_id FROM pedidos WHERE valor > 500
  );

-- Subquery no FROM
SELECT avg_tabela.media
  FROM (
    SELECT AVG(valor) AS media FROM pedidos
  ) AS avg_tabela;

-- EXISTS
SELECT nome FROM usuarios u
  WHERE EXISTS (
    SELECT 1 FROM pedidos p
    WHERE p.usuario_id = u.id
    AND p.status = 'pago'
  );

-- CTE (Common Table Expression)
WITH pedidos_grandes AS (
  SELECT usuario_id, SUM(valor) AS total
    FROM pedidos
    WHERE status = 'pago'
    GROUP BY usuario_id
    HAVING total > 1000
)
SELECT u.nome, pg.total
  FROM usuarios u
  INNER JOIN pedidos_grandes pg ON u.id = pg.usuario_id;

-- WINDOW FUNCTIONS
SELECT
    nome,
    valor,
    RANK()       OVER (ORDER BY valor DESC) AS ranking,
    ROW_NUMBER() OVER (ORDER BY valor DESC) AS linha,
    SUM(valor)   OVER ()                    AS total_geral,
    AVG(valor)   OVER (PARTITION BY perfil) AS media_perfil
  FROM usuarios u
  JOIN pedidos p ON u.id = p.usuario_id;
```

---

## 🛠️ 12. PROBLEMAS COMPLEXOS
```sql
-- Encontrar registros duplicados
SELECT email, COUNT(*) AS total
  FROM usuarios
  GROUP BY email
  HAVING total > 1;

-- Remover duplicatas mantendo o mais recente
DELETE u1 FROM usuarios u1
  INNER JOIN usuarios u2
  WHERE u1.email = u2.email
  AND u1.id < u2.id;

-- Tabela crescendo muito — verificar tamanho
SELECT
    table_name                            AS tabela,
    ROUND(data_length / 1024 / 1024, 2)  AS dados_MB,
    ROUND(index_length / 1024 / 1024, 2) AS indices_MB,
    ROUND((data_length + index_length) / 1024 / 1024, 2) AS total_MB
  FROM information_schema.tables
  WHERE table_schema = DATABASE()
  ORDER BY total_MB DESC;

-- Conexões ativas
SHOW PROCESSLIST;
SHOW FULL PROCESSLIST;
KILL 123;                                 -- Mata processo pelo ID

-- Verificar deadlocks
SHOW ENGINE INNODB STATUS;

-- Resetar AUTO_INCREMENT
ALTER TABLE tabela AUTO_INCREMENT = 1;

-- Forçar recriar índices corrompidos
REPAIR TABLE tabela;

-- Verificar integridade
CHECK TABLE tabela;

-- Transações — garantir consistência
START TRANSACTION;
  UPDATE contas SET saldo = saldo - 500 WHERE id = 1;
  UPDATE contas SET saldo = saldo + 500 WHERE id = 2;
COMMIT;                                   -- Confirma tudo
-- ou
ROLLBACK;                                 -- Desfaz tudo se houver erro

-- Bloquear tabela durante operação crítica
LOCK TABLES tabela WRITE;
  -- operações críticas aqui
UNLOCK TABLES;

-- Ver variáveis do servidor
SHOW VARIABLES LIKE 'max_connections';
SHOW VARIABLES LIKE '%timeout%';
SHOW VARIABLES LIKE '%innodb%';
SHOW STATUS  LIKE 'Threads_connected';

-- Exportar resultado de query para CSV
SELECT * FROM usuarios
  INTO OUTFILE '/tmp/usuarios.csv'
  FIELDS TERMINATED BY ','
  ENCLOSED BY '"'
  LINES TERMINATED BY '\n';
```

---

## 🔐 13. SEGURANÇA (relevante para pentest)
```sql
-- Verificar usuários com senha vazia
SELECT user, host FROM mysql.user
  WHERE authentication_string = '';

-- Verificar permissões excessivas
SELECT user, host, Super_priv, File_priv, Grant_priv
  FROM mysql.user
  WHERE Super_priv = 'Y';

-- Verificar se aceita conexão remota
SELECT user, host FROM mysql.user
  WHERE host = '%';

-- Histórico de queries (se habilitado)
SELECT * FROM mysql.general_log
  ORDER BY event_time DESC LIMIT 20;

-- Verificar plugins de autenticação
SELECT user, plugin FROM mysql.user;
```

---

## ⚠️ Aviso Legal
> Este material é estritamente educacional.
> A seção de segurança é destinada a
> auditorias autorizadas e hardening de sistemas.
> Lei 12.737/2012.
