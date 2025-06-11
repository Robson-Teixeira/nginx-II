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