## Instalações

### Linux

```bash
sudo apt install nginx
```

### MacOS

```bash
brew install nginx
```

### Windows
Para Windows, você pode baixar o Nginx do site oficial: [nginx.org](https://nginx.org/en/download.html). Após o download, extraia o conteúdo do arquivo ZIP e execute o arquivo `nginx.exe` na pasta extraída.

> Todo sistema operacional possui um arquivo de hosts. No Linux, por padrão fica em /etc/hosts. No Mac, /private/etc/hosts. Já no Windows, C:\Windows\System32\Drivers\Etc\hosts. Esse arquivo informa ao sistema operacional que quando uma conexão for estabelecida usando algum nome, o IP correspondente deve ser usado. Para o nome localhost, temos o IP da nossa própria máquina (127.0.0.1).

## Documentação
- [HTTP Load Balancing](https://docs.nginx.com/nginx/admin-guide/load-balancer/http-load-balancer/)
    - Round Robin é o método padrão de balanceamento de carga do Nginx. 
        - Weighted Round Robin é uma variação que permite atribuir pesos diferentes a cada servidor por meio da diretiva `weight`.
    - Least Connections é um método que envia a solicitação para o servidor com o menor número de conexões ativas.
    - IP Hash é um método que distribui as solicitações com base no endereço IP do cliente.
    - Generic Hash é um método que permite definir uma chave de hash personalizada para distribuir as solicitações.
    - Least Time é um método que envia a solicitação para o servidor com o menor tempo de resposta. Disponível apenas na versão Plus.
    - Random é um método que envia a solicitação para um servidor aleatório.
    - Slow Start é um método que aumenta gradualmente a carga em um servidor para evitar sobrecarga inicial por meio da diretiva `slow_start`. Disponível apenas na versão Plus.
    - Session Persistence é um método que garante que as solicitações de um cliente sejam sempre enviadas para o mesmo servidor, usando a diretiva `sticky`. Disponível apenas na versão Plus. Pode ser configurado com base em cookies, IP ou outros critérios.
    - Limiting connections é um método que limita o número de conexões simultâneas a um servidor usando a diretiva `max_conns` e `queue` para controlar o tráfego. Disponível apenas na versão Plus.

- CGI
    - CGI (Common Gateway Interface) é um protocolo que permite que servidores web executem scripts e aplicativos externos para gerar conteúdo dinâmico.
    - O processo CGI é iniciado pelo servidor web quando uma solicitação é feita para um script CGI (geralmente um arquivo executável ou script) e o servidor passa informações sobre a solicitação para o script por meio de variáveis de ambiente.
    - O script CGI processa a solicitação e gera uma resposta, que é enviada de volta ao servidor web, então, o processo CGI é finalizado.
    - O Nginx pode ser configurado para usar CGI por meio do módulo `cgi`, que permite a execução de scripts CGI.
    - O Nginx pode passar variáveis para o script CGI usando a diretiva `cgi_param`.
    - O Nginx pode manipular solicitações CGI usando a diretiva `cgi_split_path_info` para separar o caminho do script e os parâmetros da consulta.

- FastCGI
    - FastCGI é um protocolo de comunicação entre servidores web e aplicativos, permitindo que o Nginx se comunique com servidores de aplicativos como PHP, Python, Ruby, etc.
    - O processo FastCGI é iniciado pelo servidor web quando uma solicitação é feita para um script FastCGI (geralmente um arquivo executável ou script) e o servidor passa informações sobre a solicitação para o processo FastCGI por meio de variáveis de ambiente.
    - O processo FastCGI pode ser executado em um servidor separado ou no mesmo servidor do Nginx, permitindo que o Nginx se comunique com o processo FastCGI por meio de um socket Unix ou uma conexão TCP.
    - O processo FastCGI pode lidar com várias solicitações simultaneamente, o que melhora o desempenho em comparação com o CGI tradicional, que cria um novo processo para cada solicitação. Sendo assim, uma vez iniciado o processo FastCGI, ele permanece em execução e pode atender a várias solicitações, reduzindo a sobrecarga de criação de processos.
    - O Nginx pode ser configurado para usar o FastCGI por meio do módulo `fastcgi_pass`, que especifica o endereço do servidor FastCGI.
    - O Nginx pode passar variáveis para o servidor FastCGI usando a diretiva `fastcgi_param`.
    - O Nginx pode manipular solicitações FastCGI usando a diretiva `fastcgi_split_path_info` para separar o caminho do script e os parâmetros da consulta.

> Let's Encrypt é uma autoridade certificadora gratuita que fornece certificados SSL/TLS para sites. O Nginx pode ser configurado para usar certificados Let's Encrypt para habilitar HTTPS em sites, garantindo conexões seguras entre o servidor e os clientes. A configuração geralmente envolve a instalação do Certbot, que automatiza o processo de obtenção e renovação de certificados Let's Encrypt, e a configuração do Nginx para usar esses certificados.

## Comandos
- `openssl req -x509 -nodes -days 30 -newkey rsa:2048 -keyout C:/Server/nginx/localhost.key -out C:/Server/nginx/localhost.crt`
    - Gera um certificado SSL autoassinado válido por 30 dias.
- `certutil -A -d sql:~/.pki/nssdb -t C -n "Certificate Common Name" -i localhost.crt`
    - Instala o certificado SSL no Linux.
- `security add-certificate localhost.crt` e `security add-trusted-cert localhost.crt`
    - Instala o certificado SSL no MacOS.
- `certutil.exe -user -store root localhost.crt`
    - Instala o certificado SSL no Windows.

> [Managing security certificates from the console - on Windows, Mac OS X and Linux](https://sadique.io/blog/2012/06/05/managing-security-certificates-from-the-console-on-windows-mac-os-x-and-linux/)