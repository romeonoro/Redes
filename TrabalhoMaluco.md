# Bloquear o Acesso de um PC Windows ao site iffarroupilha.edu.br e a Conteúdo Adulto Usando Linux

### 1. Instalar o SSH no Linux

Para permitir o acesso remoto via SSH ao seu servidor Linux, instale o cliente OpenSSH:

```bash
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install openssh-client
````
### 2. Criar um Usuário no Linux
```bash
sudo adduser robertovargas
````
### 3. Adicionar o Usuário à Lista do SUDO
```bash
sudo usermod -aG sudo robertovargas
````
### 4. Entrar como Super Usuário
```bash
sudo su
````
### 5. Logar como o Novo Usuário
```bash
sudo su robertovargas
````
### 6. Instalar o Apache2 no Linux
```bash
sudo apt update
sudo apt install apache2
````
### 7. Iniciar o Serviço Apache
```bash
sudo systemctl start apache2
````
### 8. Criar a Página de Redirecionamento
```bash
sudo nano /var/www/html/grupo4.html
````
```bash
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ERRO!</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f5f5f5;
            font-family: Arial, sans-serif;
        }

        .erro {
            text-align: center;
        }

        h1 {
            font-size: 2.5rem;
            color: #ed4213;
        }

        h2 {
            color: #333;
            font-size: 1.3rem;
        }

        p {
            font-size: 1.2rem;
            color: #777;
            margin-top: 10px;
        }

        a {
            display: inline-block;
            margin-top: 20px;
            padding: 10px 20px;
            background-color: #333;
            color: #fff;
            text-decoration: none;
            border-radius: 5px;
            transition: background-color 0.3s;
        }

        a:hover {
            background-color: #555;
        }
    </style>
</head>
<body>
    <div class="erro">
        <h1>Não foi possível conectar!</h1>
        <h2>Acesso bloqueado pelo grandioso Grupo 4.</h2>
    </div>
</body>
</html>

````


