🔐 Projeto Prático: Simulação de Ataques de Força Bruta com Kali Linux e Medusa
📌 Objetivo do Projeto

Implementar, documentar e compartilhar um projeto prático utilizando o Kali Linux e a ferramenta Medusa, em conjunto com ambientes vulneráveis como Metasploitable 2 e DVWA (Damn Vulnerable Web Application), com o objetivo de simular cenários reais de ataque de força bruta e exercitar medidas de prevenção.

Este projeto tem fins exclusivamente educacionais e visa desenvolver competências em:

🔎 Enumeração de serviços

⚔️ Ataques de força bruta

🔐 Password Spraying

🌐 Testes em aplicações web vulneráveis

🛡️ Implementação de medidas de mitigação

🖥️ Ambiente de Laboratório

O ambiente foi configurado em rede isolada para garantir segurança durante os testes.

Hypervisor: VirtualBox

Máquina Atacante: Kali Linux

Máquina Alvo: Metasploitable 2

Aplicação Web Vulnerável: DVWA

Tipo de Rede: Host-Only

🔎 1️⃣ Enumeração Inicial com Nmap

A fase de reconhecimento é essencial para identificar portas abertas e serviços ativos no alvo.

A opção -sV foi utilizada para identificar as versões dos serviços em execução, permitindo análise mais precisa de possíveis vulnerabilidades.

🔧 Comando utilizado:
sudo nmap -sV 192.168.56.102
📊 Principais Serviços Identificados
Porta	Serviço	Versão	Nível de Risco
21	FTP	vsftpd 2.3.4	Crítico
23	Telnet	Linux telnetd	Crítico
80	HTTP	Apache 2.2.8	Médio
445	SMB	Samba 3.x	Alto
3306	MySQL	5.0.51a	Médio
⚔️ 2️⃣ Ataque de Força Bruta – FTP

Foi utilizado o Medusa para realizar um ataque de dicionário contra o serviço FTP.

🔧 Comando:
medusa -h 192.168.56.102 -U users.txt -P passwords.txt -M ftp
✅ Resultado

Usuário encontrado: msfadmin

Senha encontrada: msfadmin

Status: SUCCESS

🔎 Análise Técnica

O ataque foi bem-sucedido devido à:

Ausência de bloqueio de conta após múltiplas tentativas

Uso de credenciais padrão

Falta de política de senha forte

Esse cenário demonstra a importância do hardening básico em servidores e da aplicação de políticas adequadas de autenticação.

💻 3️⃣ Password Spraying – SMB

Foi aplicada a técnica de Password Spraying, testando uma única senha contra múltiplos usuários para evitar bloqueios automáticos.

🔧 Comando:
medusa -h 192.168.56.102 -U users.txt -p msfadmin -M smbnt
🔎 Análise

O teste confirmou reutilização de credenciais entre serviços.

Esse cenário evidencia risco de credential reuse, prática comum em ambientes corporativos e frequentemente explorada em ataques reais. Em um ambiente produtivo, isso poderia facilitar:

Movimentação lateral

Escalada de privilégios

Comprometimento de múltiplos sistemas

🌐 4️⃣ Testes em Aplicação Web – DVWA

Foi utilizado o DVWA (Damn Vulnerable Web Application) para simular ataques automatizados em formulários de login.

URL: http://192.168.56.102/dvwa

Cenário: Autenticação sem limitação de tentativas

Objetivo: Demonstrar vulnerabilidade à automação de login

O teste demonstra como aplicações web mal configuradas podem ser facilmente exploradas por ferramentas automatizadas.

📸 Evidências dos Testes
🔎 Enumeração com Nmap

01-nmap-network-discovery.png

02-nmap-target-exclusion.png

03-nmap-target-services-discovery.png

⚔️ Ataque de Força Bruta – FTP

04-setup-and-bruteforce-start.png

05-medusa-ftp-success.png

💻 Password Spraying – SMB

06-medusa-smb-spraying-start.png

07-medusa-smb-success.png

🌐 DVWA – Configuração de Segurança

08-dvwa-security-level-config.png

🛡️ Medidas de Mitigação Recomendadas

Com base nos testes realizados, recomenda-se:

✅ Implementação de políticas de senha forte

✅ Bloqueio de conta após múltiplas tentativas falhas

✅ Uso de MFA (Autenticação Multifator)

✅ Implementação de Fail2Ban

✅ Substituição de FTP e Telnet por protocolos seguros (SFTP e SSH)

✅ Monitoramento contínuo de logs

✅ Auditorias periódicas de segurança

🔍 Impacto em um Ambiente Real

Se exploradas em um ambiente corporativo real, essas vulnerabilidades poderiam resultar em:

Acesso não autorizado a dados sensíveis

Escalada de privilégios

Movimentação lateral na rede

Comprometimento completo da infraestrutura

📂 Estrutura do Repositório
📁 images
 ├── 01-nmap-network-discovery.png
 ├── 02-nmap-target-exclusion.png
 ├── 03-nmap-target-services-discovery.png
 ├── 04-setup-and-bruteforce-start.png
 ├── 05-medusa-ftp-success.png
 ├── 06-medusa-smb-spraying-start.png
 ├── 07-medusa-smb-success.png
 └── 08-dvwa-security-level-config.png

users.txt
passwords.txt
README.md
🚀 Competências Demonstradas

Pentest básico em ambiente controlado

Enumeração de serviços com Nmap

Exploração com Medusa

Identificação de vulnerabilidades

Análise de risco

Proposição de medidas de mitigação

Documentação técnica estruturada

Uso do GitHub como portfólio técnico

📚 Conclusão

Este projeto permitiu compreender, na prática, como ataques de força bruta podem ser executados e como podem ser mitigados por meio de boas práticas de segurança.

A experiência reforça a importância da segurança proativa, do monitoramento contínuo e da aplicação de controles adequados para proteger ambientes corporativos.

⚠️ Aviso: Todos os testes foram realizados em ambiente isolado e controlado, exclusivamente para fins educacionais.
