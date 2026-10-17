# ShieldLog 🛡️

**Security Event Monitoring & Threat Detection**

> 🚧 **Status: Em desenvolvimento — Fase 1 (Configuração do ambiente)**

## Sobre o projeto

O **ShieldLog** é um projeto de Engenharia de Software aplicado à cibersegurança, voltado ao monitoramento e à análise de eventos de autenticação em servidores Linux.

O objetivo é desenvolver uma ferramenta capaz de coletar e interpretar logs de autenticação SSH, identificar padrões de comportamento suspeitos e gerar alertas que auxiliem na investigação de possíveis incidentes de segurança.

O projeto está sendo desenvolvido com foco no aprendizado prático de **Python, Linux, Docker, redes, processamento de logs e conceitos de Blue Team**.

## Problema

Servidores Linux registram eventos relacionados a tentativas de autenticação, conexões e acessos a serviços.

Embora esses registros contenham informações importantes para a segurança, analisar manualmente grandes quantidades de logs pode dificultar a identificação de atividades suspeitas.

Por exemplo, diversas tentativas malsucedidas de autenticação SSH, originadas de um mesmo endereço IP em um curto intervalo, podem indicar uma tentativa de ataque de força bruta.

O ShieldLog busca transformar esses registros em eventos estruturados e alertas que facilitem sua análise.

## Solução proposta

O sistema será desenvolvido para:

1. Coletar registros de autenticação SSH.
2. Extrair informações relevantes, como horário, usuário, endereço IP e resultado da autenticação.
3. Normalizar os registros em estruturas de dados.
4. Correlacionar eventos por origem e intervalo de tempo.
5. Identificar comportamentos suspeitos utilizando regras configuráveis.
6. Gerar alertas contendo as evidências associadas às detecções.
7. Armazenar e disponibilizar informações para consulta.

Uma das primeiras regras planejadas será identificar **cinco ou mais falhas de autenticação de um mesmo IP em uma janela de 60 segundos**.

Essa regra representa um indicador de atividade suspeita, não uma confirmação de invasão.

## Arquitetura planejada

O ambiente inicial utilizará Docker para executar um servidor OpenSSH isolado em um container Linux. Uma máquina virtual Kali Linux será utilizada como cliente para realizar conexões e gerar eventos de autenticação controlados.

O fluxo de processamento previsto é:

```text
Kali Linux (Cliente SSH)
         |
         v
Docker (Servidor OpenSSH)
         |
         v
Logs de Autenticação
         |
         v
Coletor e Parser Python
         |
         v
Motor de Detecção
         |
         v
Alertas de Segurança
         |
         v
Persistência + API REST
         |
         v
Dashboard
```

Os componentes serão implementados progressivamente, começando pela leitura e interpretação de logs.

## Tecnologias previstas

| Tecnologia | Finalidade |
|---|---|
| Python | Processamento de logs e detecção |
| Docker | Ambiente de laboratório reproduzível |
| Linux / OpenSSH | Servidor monitorado |
| pytest | Testes automatizados |
| PostgreSQL | Persistência de eventos e alertas |
| FastAPI | API REST para consultas |
| Git / GitHub | Versionamento e documentação |

**Observação:** nem todas essas tecnologias estão implementadas. Elas serão incorporadas conforme a evolução do projeto.

## Roadmap

- [ ] **Fase 1 — Laboratório SSH:** configurar o Docker, executar o OpenSSH e gerar registros reais de autenticação.
- [ ] **Fase 2 — Processamento de logs:** desenvolver um parser Python para extrair e normalizar eventos.
- [ ] **Fase 3 — Motor de detecção:** implementar regras de identificação de comportamentos suspeitos.
- [ ] **Fase 4 — Persistência e API:** integrar PostgreSQL e disponibilizar consultas com FastAPI.
- [ ] **Fase 5 — Dashboard:** construir uma interface para visualização de eventos e alertas.
- [ ] **Fase 6 — Melhorias opcionais:** avaliar novas regras, integrações e recursos de análise.

## MVP — Primeira versão funcional

A primeira entrega planejada será uma aplicação Python capaz de:

- Ler arquivos contendo logs de autenticação SSH.
- Identificar e estruturar eventos de autenticação.
- Detectar múltiplas falhas provenientes de um mesmo IP dentro de uma janela temporal.
- Produzir alertas com informações e evidências relevantes.
- Validar o comportamento do sistema por meio de testes automatizados.

O MVP não dependerá inicialmente de banco de dados, dashboard ou serviços externos.

## Segurança e limitações

O ShieldLog será desenvolvido e testado exclusivamente em ambientes próprios e controlados, utilizando containers Docker e máquinas virtuais.

O projeto possui finalidade educacional e experimental. Não deve ser considerado, em sua versão inicial, um SIEM completo, EDR ou solução de proteção pronta para ambientes de produção.

Os alertas gerados representarão indicadores de comportamento suspeito, sujeitos a investigação e possíveis falsos positivos.

## Estado atual

🚧 **O projeto está em fase inicial de desenvolvimento.**

A prioridade atual é configurar o laboratório SSH, compreender a estrutura dos registros de autenticação e reunir os primeiros exemplos que servirão de entrada para o processamento em Python.

A documentação, a arquitetura e as funcionalidades serão atualizadas conforme o desenvolvimento e a validação de cada etapa.
