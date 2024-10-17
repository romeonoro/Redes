**CC** <br>
bloquear o acesso de um pc windows a um site e a conteúdo adulto (palavra chave sexo) usando linux <br>
[www.iffarroupilha.edu.br](http://www.iffarroupilha.edu.br) e redirecionar para o nosso próprio site <br>


   - Instalar o SSH no Linux
     ```bash
     sudo apt-get update
     sudo apt-get upgrade
     sudo apt-get install openssh-client
     ```

   - Criar usuário
     ```bash
     sudo adduser username
     ```

   - Adicionar usuário na lista do SUDO
     ```bash
     sudo usermod -aG sudo username
     ```

   - Entrar como super usuário
     ```bash
     sudo su
     ```

   - Logar usuário e mudar usuário
     ```bash
     sudo su username
     ```


   - Instalar o Apache 2 no Linux
     ```bash
     sudo apt update
     sudo apt install apache2
     ```

   - Iniciar o serviço
     ```bash
     sudo systemctl start apache2
     ```

   - Criando site
     ```bash
     sudo nano /var/www/html/grupo4.html
     ```
     
