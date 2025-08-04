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

