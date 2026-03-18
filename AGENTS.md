# Equipe SBahia - Agentes IA

Este documento define os agentes disponíveis para orquestração de projetos de desenvolvimento.

## Agentes Disponíveis

| Agente | Função | Localização |
|--------|--------|-------------|
| **Orchestrator** | Coordenador principal | skills/orchestrator/ |
| **TechLead** | Arquitetura e liderança técnica | skills/leadership-tech/ |
| **UXUIDesigner** | Design de interface e experiência | skills/uxui-designer/ |
| **FrontendDev** | Desenvolvimento front-end (View) | skills/frontend-developer/ |
| **BackendController** | API, rotas, validação (Controller) | skills/backend-controller/ |
| **BackendModel** | Regras de negócio, DDD (Model) | skills/backend-model/ |
| **DBASpecialist** | Banco de dados e performance | skills/dba-specialist/ |
| **SecuritySpecialist** | Segurança, auth, OWASP | skills/security-specialist/ |
| **APIGatewaySpecialist** | API Gateway, rate limiting | skills/api-gateway-specialist/ |
| **MobileDev** | Desenvolvimento mobile | skills/mobile-developer/ |
| **DataEngineer** | ETL, data warehouse | skills/data-engineer/ |
| **MLEngineer** | Machine learning, MLOps | skills/machine-learning-engineer/ |
| **TestingSpecialist** | Testes automatizados | skills/testing-specialist/ |
| **ErrorHandlingSpecialist** | Debug, tratamento erros | skills/error-handling-specialist/ |
| **ProductOwner** | Gestão de produto | skills/product-owner/ |
| **DevOps** | Infraestrutura, CI/CD | skills/devops-engineer/ |

## Arquitetura MVC

```
        ┌─────────────┐
        │     VIEW    │  ← FrontendDev, UXUIDesigner
        └──────┬──────┘
               │
               ▼
        ┌─────────────┐
        │ CONTROLLER  │  ← BackendController
        └──────┬──────┘
               │
               ▼
        ┌─────────────┐
        │    MODEL    │  ← BackendModel, DBASpecialist
        └─────────────┘
```

## Exemplos de Uso

### CrewAI Format

```python
from crewai import Agent, Task, Crew

# Agentes
orchestrator = Agent(
    role="Project Orchestrator",
    goal="Coordenar projeto de desenvolvimento web",
    backstory="Especialista em gestão de projetos ágeis",
    tools=[...],
    allow_delegation=True
)

tech_lead = Agent(
    role="Tech Lead",
    goal="Definir arquitetura e padrões técnicos",
    backstory="Arquiteto de software experiente",
    tools=[...],
)

backend_controller = Agent(
    role="Backend Controller Developer",
    goal="Implementar APIs RESTful",
    backstory="Desenvolvedor back-end especializado em Node.js",
    tools=[...],
)

# Tarefas
task1 = Task(
    description="Criar arquitetura MVC para o projeto",
    agent=tech_lead,
)

task2 = Task(
    description="Implementar endpoints de autenticação",
    agent=backend_controller,
    depends_on=[task1],
)

# Crew
crew = Crew(
    agents=[orchestrator, tech_lead, backend_controller],
    tasks=[task1, task2],
    verbose=True
)

result = crew.kickoff()
```

### LangChain + AutoGen Format

```python
from autogen import ConversableAgent

# Definição de agentes
agents = {
    "orchestrator": ConversableAgent(
        name="Orchestrator",
        system_message="""Você é o orquestrador de um projeto de desenvolvimento.
Coordene os seguintes agentes especializados para entregar o projeto.""",
        llm_config={...},
    ),
    
    "tech_lead": ConversableAgent(
        name="TechLead",
        system_message="""Você é Tech Lead e Arquiteto de Software.
Defina a arquitetura do projeto seguindo padrões MVC.""",
        llm_config={...},
    ),
    
    "backend_dev": ConversableAgent(
        name="BackendDeveloper",
        system_message="""Você é desenvolvedor Back-end especializado em Node.js.
Implemente Models e Controllers seguindo boas práticas.""",
        llm_config={...},
    ),
}

# Orquestração
def run_project(project_requirements):
    # 1. Tech Lead define arquitetura
    architecture = agents["tech_lead"].generate_reply(
        messages=[{"content": f"Defina arquitetura para: {project_requirements}"}]
    )
    
    # 2. Backend implementa
    backend_result = agents["backend_dev"].generate_reply(
        messages=[{"content": f"Implemente: {architecture}"}]
    )
    
    # 3. Frontend implementa
    # ...
    
    return consolidated_result
```

## Matriz de Competências

| Agente | Frontend | Backend | Database | Mobile | ML | Data | Security | DevOps |
|--------|----------|---------|----------|--------|----|-----|----------|--------|
| TechLead | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| FrontendDev | ★ | ◐ | - | ◐ | - | - | ◐ | - |
| BackendController | ◐ | ★ | ◐ | - | - | - | ✓ | - |
| BackendModel | - | ★ | ✓ | - | ◐ | ◐ | - | - |
| DBASpecialist | - | ◐ | ★ | - | - | ✓ | - | ◐ |
| SecuritySpecialist | ✓ | ✓ | ✓ | ✓ | - | - | ★ | ✓ |
| MobileDev | ★ | ◐ | - | ★ | - | - | ◐ | - |
| MLEngineer | - | ◐ | - | - | ★ | ✓ | - | - |
| DataEngineer | - | ◐ | ✓ | - | ✓ | ★ | - | ◐ |
| TestingSpecialist | ✓ | ✓ | ✓ | ✓ | - | - | ✓ | - |
| DevOps | - | ◐ | ◐ | - | - | - | ✓ | ★ |

★ Especialidade | ✓ Conhece | ◐ Básico | - Não擅長

## Padrão de Comunicação

### Passagem de Contexto

```yaml
context:
  from: FrontendDev
  to: BackendController
  message: |
    Necessito endpoint para listar produtos:
    GET /api/v1/products?page=1&limit=20
    
    Response esperada:
    {
      "data": [...],
      "pagination": { "page": 1, "total": 100 }
    }
  
  priority: high
```

### Retorno de Task

```yaml
task_result:
  task_id: TASK-001
  agent: BackendController
  status: completed
  
  output:
    - endpoint_created: /api/v1/products
    - tested: true
    - documentation: /docs/products-api.md
    
  blockers: []
  notes: "Adicionei cache Redis para melhor performance"
```

## Inicialização de Projeto

```python
from equipe_sbahia import ProjectOrchestrator

# Definir projeto
project = {
    "name": "E-commerce Platform",
    "type": "web_app",  # web_app, api, mobile, ml, data
    "requirements": [
        "Autenticação JWT",
        "Catálogo produtos",
        "Carrinho compras",
        "Checkout",
    ],
    "team_size": 5,
    "timeline": "3 meses"
}

# Iniciar orquestrador
orchestrator = ProjectOrchestrator(project)
orchestrator.analyze()
orchestrator.plan()
orchestrator.execute()
orchestrator.deliver()
```

## Contributing

Para adicionar novo agente:
1. Criar skill em `skills/<agent-name>/SKILL.md`
2. Adicionar à matriz em AGENTS.md
3. Definir competências em skills.md

---

**Equipe SBahia** - Ecossistema de Agentes IA para Desenvolvimento de Software
