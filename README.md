# 🛑 Bloqueio de Acesso no Windows via Linux

### Bloquear acesso ao site www.iffarroupilha.edu.br e Conteúdo Adulto.

### 👨‍💻 Grupo 4 (Romeo, Gilberto e Iago)

<p align="center">
    <img src="assets/trabRedesCC.jpg" alt="redes">
</p>

<p align="center">
    <img src="assets/transferir.png" alt="quadro">
</p>

---

| 📝 Componente   | 🚀 Descrição                                                   |
|----------------|:-------------------------------------------------------------:|
| [🔐 SSH](#instalando-o-ssh-no-linux) | Acesso remoto e seguro ao servidor Linux            |
| [🌐 Apache2](#instalando-o-apache2-no-linux) | Servidor web para hospedar páginas e serviços web |
| [🌉 Sub-Interfaces](#criando-sub-interfaces-no-linux) | Segmentação de rede para diferentes serviços         |
| [🔀 Rotas]()     | Gerenciamento de tráfego entre redes                          |
| [🛡️ Proxy](#bloqueio-de-sites-usando-proxy) | Intermediário para controle de acesso a requisições externas |
| [🦑 Squid](#configurando-o-squid-no-linux) | Servidor proxy para filtragem e bloqueio de sites   |
| [🔥 IP Tables](#instalando-e-configurando-ip-tables-no-linux) | Firewall para controle de tráfego na rede             |

---

## 🔐 Instalando o SSH no Linux

```bash
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install openssh-client
```

### Criar um Novo Usuário
```bash
sudo adduser robertovargas
```

### Adicionar Usuário ao SUDO
```bash
sudo usermod -aG sudo robertovargas
```

### Acessar como Super Usuário
```bash
sudo su
```

### Logar como Novo Usuário
```bash
sudo su robertovargas
```

---

## 🌐 Instalando o Apache2 no Linux
```bash
sudo apt update
sudo apt install apache2
```

### Iniciar o Serviço Apache
```bash
sudo systemctl start apache2
```

### Criar Página de Redirecionamento
```bash
sudo nano /var/www/html/grupo4.html
```

```html
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
    </style>
</head>
<body>
    <div class="erro">
        <h1>Não foi possível conectar!</h1>
        <h2>Acesso bloqueado pelo grandioso Grupo 4.</h2>
    </div>
</body>
</html>
```

### Configurar Redirecionamento de Sites
```bash
sudo nano /etc/hosts
127.0.0.1 www.iffarroupilha.edu.br
127.0.0.1 sexo
sudo systemctl restart apache2
```

### Permissões de Arquivos
```bash
sudo chown -R www-data:www-data /var/www/html/
sudo chmod -R 755 /var/www/html/
```

### Habilitar no Firewall
```bash
sudo ufw allow 'Apache'
```

### Abrir a Página Criada
```bash
http://172.25.2.204/grupo4.html
```

---

## 🔥 Instalando e Configurando IP Tables no Linux
### Instalação do IP Tables
```bash
sudo apt install iptables
sudo apt install iptables-persistent
sudo systemctl enable netfilter-persistent
```

---

## 🌉 Criando Sub-Interfaces no Linux

### Instalar net-tools
```bash
sudo apt install net-tools
```

### Verificar Roteador
```bash
sudo ifconfig
```

### Adicionar Sub-Interface
```bash
sudo ifconfig enp0s31f6:0 192.168.1.33 netmask 255.255.255.252
```

---

## 🛡️ Bloqueio de Sites Usando Proxy
### Instalar o Squid
```bash
sudo apt-get install squid
```

### Verificar Status do Squid
```bash
sudo service squid status
```

---

## 🦑 Configurando o Squid no Linux
```bash
cd /etc/squid
```

### Fazer Backup do Arquivo de Configuração
```bash
sudo cp squid.conf squid.conf.backup
```

### Criar Nova Configuração
```bash
sudo rm squid.conf
sudo nano squid.conf
```

### Criar Arquivos de Bloqueio
```bash
sudo touch /etc/squid/sites_proibidos.txt
sudo touch /etc/squid/palavras_proibidas.txt
```

### Editar Arquivos de Bloqueio
```bash
sudo nano /etc/squid/sites_proibidos.txt
sudo nano /etc/squid/palavras_proibidas.txt
```

### Configuração do Squid
```bash
# Define a porta do proxy
http_port 3128

# Permite acesso apenas à rede local
acl sites_proibidos url_regex -i "/etc/squid/sites_proibidos.txt"
http_access deny sites_proibidos

# Bloqueia acesso a sites listados
deny_info http://172.25.2.214/grupo4 sites_proibidos
```

### Reiniciar o Serviço Squid
```bash
sudo systemctl stop squid
sudo systemctl start squid
```

---

## 💻 Configurar Proxy no Windows
1. Abra as configurações do Windows.
2. Vá em **Rede e Internet**.
3. Clique em **Proxy**.
4. Desmarque a opção **Detectar configurações automaticamente**.
5. Em **Configuração manual de proxy**, clique em **Editar**.
6. Ative o proxy.
7. No campo **Endereço de proxy**, insira o IP do Linux.
8. No campo **Porta**, coloque `3128`.

