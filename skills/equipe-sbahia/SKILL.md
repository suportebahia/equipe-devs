---
name: Equipe SBahia
description: |
  Sistema de agentes IA para coordenação de projetos de desenvolvimento.
  Use este skill para iniciar qualquer projeto.

  Este skill orquestra automaticamente os agentes especializados conforme a necessidade:
  - Análise e planejamento de projetos
  - Coordenação de múltiplos agentes
  - Gestão de tasks e dependências

---

# Equipe SBahia - Orquestrador

## Como Usar

Para iniciar um novo projeto, basta descrever o que você precisa:

```
Preciso criar um sistema de [descrição do projeto]
```

O orquestrador irá:
1. Fazer perguntas de kickoff
2. Montar a equipe necessária
3. Planejar e executar as tasks

## Comandos Rápidos

- `/start` - Iniciar novo projeto
- `/team` - Ver agentes disponíveis
- `/status` - Ver status do projeto atual

## Fluxo de Trabalho

```
1. KICKOFF → 2. ANÁLISE → 3. PLANEJAMENTO → 4. EXECUÇÃO → 5. ENTREGA
```

---

# Agentes Disponíveis (usados internamente)

## TechLead
- Arquitetura MVC e padrões técnicos
- Definição de stack tecnológica
- Code review e boas práticas

## BackendController
- APIs RESTful
- Rotas e validação de dados
- Integração com frontend

## BackendModel
- Entidades e domínios
- Regras de negócio
- Validações e lógicas

## FrontendDeveloper
- Interface React/Next.js
- Componentes e用户体验
- Integração com APIs

## UXUIDesigner
- Design de interfaces
- Wireframes e protótipos
- Design system

## DBASpecialist
- Schema de banco
- Queries otimizadas
- Migrations

## SecuritySpecialist
- Autenticação e autorização
- Proteção de dados
- OWASP compliance

## DevOpsEngineer
- CI/CD
- Infraestrutura
- Deploy e monitoramento

## TestingSpecialist
- Testes unitários
- Testes de integração
- QA e qualidade

---

# Notas de Implementação

Este skill carrega os outros automaticamente via arquivo de configuração `.skillfish.json`.
Os agentes especializados podem ser invocados conforme necessidade do projeto.
