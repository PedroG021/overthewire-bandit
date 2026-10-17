🇺🇸 [English](README.md) | 🇧🇷 Português

# OverTheWire: Bandit Writeups

## Resumo

Este repositório documenta a conclusão dos 34 níveis do **OverTheWire: Bandit**, uma sequência de desafios práticos de segurança ofensiva básica em ambiente Linux. Cada nível exige encontrar uma falha de configuração, permissão ou codificação para conseguir acesso ao próximo, usando ferramentas de linha de comando como `grep`, `find`, `netcat`, `openssl`, `cron` e `nmap`.

> **Nota:** os writeups completos (os arquivos linkados no índice abaixo), com a metodologia detalhada de cada nível, estão em **inglês**.

---

## ⚠️ Uso Responsável e Política Educacional

Este repositório é desenvolvido estritamente para fins educacionais, auditoria de metodologia técnica e acompanhamento de competências pessoais. Em conformidade com os objetivos pedagógicos da comunidade do wargame:

* **Sanitização de Dados:** Todos os tokens de autenticação, flags e credenciais finais foram rigorosamente sanitizados e omitidos (`[REDACTED]`).
* **Sem Spoilers:** As soluções são estruturadas para demonstrar arquitetura de sistema, lógica e pipelines de comandos. Recomenda-se fortemente usar este material como referência *depois* de tentar os desafios de forma independente. Copiar comandos sem análise ativa anula o propósito de aprendizado.

---

## 🗺️ Índice do Repositório

| Arquivo do Writeup | Foco Conceitual Principal | Status |
| :--- | :--- | :--- |
| [**levels-00-07.md**](./levels-00-07.md) | Fundamentos, Navegação no Sistema de Arquivos, Propriedades de Objetos e Nomes de Arquivo Especiais | `Concluído` |
| [**levels-07-13.md**](./levels-07-13.md) | Redirecionamento de Streams, Processamento de Dados, Codificação e Utilitários de Compressão | `Concluído` |
| [**levels-13-19.md**](./levels-13-19.md) | Arquitetura de Redes, Sessões Remotas SSH e Hooks de Execução de Shell | `Concluído` |
| [**levels-19-27.md**](./levels-19-27.md) | Exploração de Setuid, Escalação de Privilégios Local, Automação com Scripts e Escapes de Shell | `Concluído` |
| [**levels-27-33.md**](./levels-27-33.md) | Exploração de Repositórios Git e Escapes de Ambientes Restritos | `Concluído` |

---

## 🧠 Competências Técnicas Principais

* **Auditoria de Sistema de Arquivos:** Validação aprofundada de atributos de objetos, matriz de permissões, alocações ocultas e tratamento de nomes de arquivo malformados ou iniciados por hífen.
* **Pipelines de Processamento de Dados:** Combinação de utilitários de manipulação de strings para executar filtragem, parsing e análise de streams com alta eficiência em alvos de dados densos.
* **Logística Criptográfica e de Redes:** Mapeamento de sistemas remotos, conexões seguras de terminal com chaves assimétricas e depuração de fluxos de dados brutos em sockets de rede.
* **Escalação de Privilégios e Auditoria de Automação:** Auditoria de rotinas agendadas do sistema (cron jobs), exploração de configurações incorretas em binários `setuid` e desenvolvimento de scripts bash para automatizar payloads de força bruta em rede.
* **Diagnóstico de Controle de Versão e Evasão de Shell:** Engenharia reversa do histórico de repositórios Git (branches não mescladas, commits desanexados, submódulos) e bypass de shells com filtragem rígida de entrada via expansão interna de parâmetros (`$0`).