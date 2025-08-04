# Treinamentro-Infra-Administra-o-de-Servidores-Linux# 🧭 MÓDULO 1 – **Introdução ao SSH e Acesso Remoto**

📆 **Duração estimada:** 4h
🔐 **Servidor de exemplo:** `10.72.25.4`
👥 **Pré-requisito:** Cada participante deve ter acesso a um terminal (Linux/macOS) ou Git Bash/WSL (Windows).

---

## 🔹 1. O que é SSH (30 min)

### 📘 Explicação:

* SSH (Secure Shell) é um protocolo seguro para acessar máquinas remotamente.
* Funciona na porta padrão **22**.
* Usa **criptografia assimétrica** para autenticação (login/senha ou chave pública/privada).

---

## 🔹 2. Acesso Básico com Login e Senha (30 min)

### 🧪 Passo a passo:

1. Abra o terminal (Linux/macOS) ou Git Bash (Windows).

2. Execute:

   ```bash
   ssh usuario@10.72.25.4
   ```

   *(Substitua `usuario` pelo nome real do usuário)*

3. Digite a senha quando solicitado.

🔐 Dica:

* Se for a primeira conexão, o terminal pedirá para aceitar a chave do servidor. Digite `yes`.

---

## 🔹 3. Gerando e Usando Chaves SSH (1h)

### 🎯 Objetivo: Acessar o servidor sem digitar senha.

### 🧪 Passo a passo:

#### 🔧 No computador local:

1. Gere o par de chaves:

   ```bash
   ssh-keygen -t rsa -b 4096 -C "seuemail@exemplo.com"
   ```

2. Pressione `Enter` para salvar em `~/.ssh/id_rsa`

3. Opcional: Defina uma senha para proteger sua chave privada

4. Veja os arquivos:

   ```bash
   ls ~/.ssh
   ```

   * `id_rsa` → chave **privada**
   * `id_rsa.pub` → chave **pública**

---

#### 🔐 Copiando a chave pública para o servidor:

1. Execute:

   ```bash
   ssh-copy-id usuario@10.72.25.4
   ```

   Se não tiver o `ssh-copy-id`:

   ```bash
   cat ~/.ssh/id_rsa.pub | ssh usuario@10.72.25.4 'mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys'
   ```

2. Teste o acesso:

   ```bash
   ssh usuario@10.72.25.4
   ```

   Agora deve entrar **sem pedir senha**.

---

## 🔹 4. Automatizando com Arquivo `config` (30 min)

### 🧪 Passo a passo:

1. Abra ou crie o arquivo:

   ```bash
   nano ~/.ssh/config
   ```

2. Adicione:

   ```ssh
   Host servidor-treinamento
       HostName 10.72.25.4
       User usuario
       IdentityFile ~/.ssh/id_rsa
   ```

3. Salve e conecte com:

   ```bash
   ssh servidor-treinamento
   ```

---

## 🔹 5. Transferência de Arquivos com SCP e SFTP (30 min)

### 🧪 SCP – copiar arquivos:

* Do computador local para o servidor:

  ```bash
  scp arquivo.txt usuario@10.72.25.4:/home/usuario/
  ```

* Do servidor para o computador local:

  ```bash
  scp usuario@10.72.25.4:/home/usuario/arquivo.txt .
  ```

---

## 🔹 5. Práticas Finais e Desafios (30 min)

### ✔️ Desafios:

* Gerar chave e configurar o acesso sem senha
* Enviar um arquivo para o servidor e baixá-lo de volta
* Criar uma entrada personalizada no `~/.ssh/config`

---

## ✅ Dica Extra: Permissões do `.ssh`

Se o SSH estiver recusando a chave:

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

---

# 🧭 **Módulo 2 – Comandos Linux Essenciais (4h)**

🎯 **Objetivo:** Familiarizar os participantes com o terminal Linux e comandos básicos de administração.

---

## 📁 1. Navegação no Sistema de Arquivos (30 min)

### ✅ Comandos:

* `pwd` – mostra o diretório atual
* `ls` – lista arquivos e pastas
* `cd` – navega entre diretórios

### 🧪 Passos:

```bash
pwd                      # Mostra onde estou
ls                       # Lista arquivos da pasta atual
ls -l                    # Lista detalhada
ls -a                    # Lista arquivos ocultos
cd /tmp                  # Vai para o diretório /tmp
cd ~                     # Vai para o diretório do usuário
cd ..                    # Volta uma pasta
```

---

## 📦 2. Manipulação de Arquivos e Diretórios (30 min)

### ✅ Comandos:

* `mkdir` – cria diretórios
* `touch` – cria arquivos vazios
* `cp`, `mv`, `rm` – copiar, mover e remover

### 🧪 Passos:

```bash
mkdir pasta_exemplo                  # Cria uma nova pasta
cd pasta_exemplo
touch arquivo1.txt                   # Cria um arquivo vazio
cp arquivo1.txt copia.txt            # Copia o arquivo
mv copia.txt renomeado.txt           # Renomeia ou move
rm renomeado.txt                     # Remove o arquivo
rm -r pasta_exemplo                  # Remove diretório recursivamente
```

---

## 🔐 3. Permissões e Usuários (45 min)

### ✅ Comandos:

* `chmod` – altera permissões
* `chown` – altera dono do arquivo
* `useradd`, `passwd`, `groups`

### 🧪 Permissões:

```bash
touch exemplo.txt
ls -l exemplo.txt                  # Veja as permissões padrão
chmod 755 exemplo.txt              # rwxr-xr-x
chmod u+x exemplo.txt              # Adiciona permissão de execução para o dono
chown root:root exemplo.txt        # Altera dono e grupo
```

### 🧪 Usuários:

```bash
sudo useradd aluno01              # Cria usuário
sudo passwd aluno01               # Define senha
sudo usermod -aG sudo aluno01     # Adiciona ao grupo sudo
groups aluno01                    # Verifica grupos
```

---

## 📖 4. Visualização de Arquivos (30 min)

### ✅ Comandos:

* `cat`, `less`, `more`, `tail`, `head`

### 🧪 Passos:

```bash
echo -e "linha 1\nlinha 2\nlinha 3" > texto.txt
cat texto.txt                     # Mostra todo o conteúdo
head texto.txt                    # Mostra as primeiras 10 linhas
tail texto.txt                    # Mostra as últimas 10 linhas
less texto.txt                    # Navegação interativa com barra de rolagem
```

---

## 🖥 5. Monitoramento e Processos (30 min)

### ✅ Comandos:

* `ps`, `top`, `htop`, `kill`

### 🧪 Passos:

```bash
ps aux                            # Lista todos os processos
ps -ef | grep nome                # Busca processo pelo nome
top                               # Interface de monitoramento em tempo real
htop                              # Interface amigável (instalar com apt/yum)
kill -9 PID                       # Força o encerramento de um processo
```

---

## 📦 6. Gerenciamento de Pacotes (30 min)

### ✅ Ubuntu/Debian:

```bash
sudo apt update                          # Atualiza lista de pacotes
sudo apt upgrade                         # Atualiza pacotes
sudo apt install htop                    # Instala um pacote
sudo apt remove htop                     # Remove um pacote
```

---

## 🧪 Atividades Práticas (45 min)

### 📝 Tarefas propostas:

1. Criar um diretório `projetos` e dentro dele:

   * Criar 3 arquivos (`a.txt`, `b.txt`, `c.txt`)
   * Copiar o conteúdo de `a.txt` para `b.txt`
   * Mover `c.txt` para fora da pasta

2. Alterar permissões de um arquivo para que:

   * Dono tenha leitura e escrita
   * Grupo tenha somente leitura
   * Outros não tenham acesso

3. Instalar o `htop` e abrir o monitoramento.

5. Criar um script de teste:

   ```bash
   echo -e "#!/bin/bash\nsleep 60" > script.sh
   chmod +x script.sh
   ./script.sh &
   ```

   * Localizar o processo com `ps`
   * Finalizar com `kill`

---

## ✅ Encerramento e Dicas Finais (15 min)

* Use `man comando` para ajuda de qualquer comando:

  ```bash
  man chmod
  ```
* Use `--help` para ver opções rápidas:

  ```bash
  cp --help
  ```
