# 🔐 Brute Force Attack Lab – Kali Linux & Medusa

## 📌 Sobre o Projeto

Este projeto documenta a simulação de ataques de força bruta em ambiente controlado utilizando Kali Linux contra a máquina vulnerável Metasploitable 2.

O objetivo é demonstrar conhecimentos em:

- Enumeração de serviços
- Ataques de força bruta
- Password spraying
- Validação de credenciais
- Análise de vulnerabilidades
- Proposição de medidas de mitigação

---

## 🖥️ Ambiente de Laboratório

- VirtualBox
- Kali Linux (Máquina Atacante)
- Metasploitable 2 (Máquina Alvo)
- Rede Host-Only (Ambiente isolado)

---

## 🔎 1️⃣ Enumeração Inicial

Ferramenta utilizada: Nmap

Comando executado:

nmap -sV 192.168.56.102

### Serviços Identificados

| Porta | Serviço | Versão | Risco |
|-------|---------|--------|-------|
| 21 | FTP | vsftpd 2.3.4 | Alto |
| 23 | Telnet | Linux telnetd | Alto |
| 80 | HTTP | Apache 2.2.8 | Médio |
| 139/445 | SMB | Samba 3.x | Alto |
| 3306 | MySQL | 5.0.51a | Médio |

A enumeração revelou múltiplos serviços legados e vulneráveis, aumentando significativamente a superfície de ataque.

---

# ⚔️ 2️⃣ Ataque de Força Bruta – FTP

Ferramenta: Medusa

Comando:

medusa -h 192.168.56.102 -U users.txt -P passwords.txt -M ftp

### 🎯 Resultado

Credenciais encontradas com sucesso:

Usuário: msfadmin  
Senha: msfadmin  

Validação realizada manualmente via login FTP.

### 🔎 Análise

- Não há limitação de tentativas de login
- Não existe política de senha forte
- Serviço FTP transmite credenciais em texto plano

Impacto: Alto

---

# 💻 3️⃣ Password Spraying – SMB

Após enumeração de usuários via enum4linux, foi realizado teste de password spraying.

Comando:

medusa -h 192.168.56.102 -U users.txt -p password -M smbnt

Objetivo: testar uma única senha comum contra múltiplos usuários.

Esse tipo de ataque é eficiente contra ambientes corporativos com políticas fracas de senha.

---

# 🌐 4️⃣ Força Bruta em Aplicação Web (DVWA)

A aplicação DVWA foi acessada via:

http://192.168.56.102/dvwa

Configuração de segurança: LOW

Foi testado o módulo de Brute Force para simular automação de tentativas de login.

---

# 🛡️ Medidas de Mitigação Recomendadas

- Implementação de política de senha forte
- Bloqueio de conta após múltiplas tentativas falhas
- Implementação de autenticação multifator (MFA)
- Monitoramento e análise de logs
- Implementação de Fail2Ban
- Desativação de serviços legados (Telnet, FTP)
- Atualização de versões vulneráveis de serviços

---

# 📊 Lições Aprendidas

- A enumeração é etapa crítica antes de qualquer exploração.
- Serviços legados representam alto risco.
- Senhas fracas continuam sendo uma das principais vulnerabilidades.
- Controles de segurança básicos poderiam impedir o ataque.

---

# 📚 Conclusão

Este laboratório permitiu compreender na prática como ataques automatizados de força bruta funcionam e como ambientes mal configurados podem ser comprometidos rapidamente.

O projeto reforça a importância de controles preventivos, monitoramento e boas práticas de segurança da informação.

---

⚠️ Todos os testes foram realizados em ambiente isolado e controlado para fins exclusivamente educacionais.
