# Roadmap - Fraud Detection Portfolio

Este documento define o plano de desenvolvimento completo para transformar o projeto de detecção de fraudes em uma aplicação profissional Django + React, adequada para portfólio.

## Visão Geral

```
Fase 0 (Prep)  →  Fase 1 (MVP)  →  Fase 2 (UX)  →  Fase 3 (Pro)  →  Fase 4 (Deploy)  →  Fase 5 (Portfolio)
1 semana       →  2 semanas     →  2 semanas    →  2 semanas    →  1 semana        →  1 semana
```

---

## Fase 0: Preparação do Ambiente (1 semana)

Objetivo: Estabelecer fundação sólida com stack definido, repositório organizado e documentação inicial.

### Issues

#### [0.1] Definir Stack Tecnológico e Requisitos
- [ ] Documentar stack: Django 4.2+, DRF, React 18+, PostgreSQL, Docker
- [ ] Listar requisitos funcionais e não-funcionais
- [ ] Definir padrões de código e naming conventions
- [ ] Criar documento de decisões arquiteturais (ADR)

**Estimate:** 4 horas | **Label:** `infra`, `planning`

---

#### [0.2] Estruturar Repositório em Monorepo
- [ ] Reorganizar repositório para monorepo (backend/, frontend/)
- [ ] Criar .gitignore apropriado
- [ ] Adicionar LICENSE e CONTRIBUTING.md
- [ ] Criar pasta /docs para documentação arquitetural

**Estimate:** 2 horas | **Label:** `infra`

---

#### [0.3] Configurar Docker e Docker Compose
- [ ] Dockerfile para backend (Django)
- [ ] Dockerfile para frontend (React)
- [ ] docker-compose.yml com services: backend, frontend, postgres, nginx
- [ ] Variáveis de ambiente (.env.example)
- [ ] Documentar como executar localmente

**Estimate:** 3 horas | **Label:** `infra`

---

#### [0.4] Criar README Inicial Detalhado
- [ ] Visão geral do projeto
- [ ] Quick start (Como clonar e rodar)
- [ ] Arquitetura em alto nível
- [ ] Stack tecnológico com links
- [ ] Roadmap resumido
- [ ] Como contribuir
- [ ] Licença e créditos

**Estimate:** 2 horas | **Label:** `doc`

---

## Fase 1: MVP Funcional (2 semanas)

Objetivo: Ter uma versão funcional com backend capaz de treinar e fazer predições, e frontend básico para interação.

### Backend

#### [1.1] Inicializar Django e Configurar DRF
- [ ] Criar projeto Django
- [ ] Instalar e configurar Django REST Framework
- [ ] Configurar CORS (django-cors-headers)
- [ ] Adicionar dotenv para variáveis de ambiente
- [ ] Estruturar apps (datasets, ml_models, predictions)
- [ ] Configurar logging estruturado

**Estimate:** 4 horas | **Label:** `backend`, `MVP`

---

#### [1.2] Criar Modelo e Endpoint de Upload de Dataset
- [ ] Modelar Django: Dataset (nome, arquivo, upload_date, status)
- [ ] Serializer para Dataset
- [ ] Endpoint POST /api/v1/datasets/upload/
- [ ] Validação de arquivo CSV
- [ ] Armazenar arquivo em storage local ou S3
- [ ] Retornar info básica do dataset (tamanho, colunas, preview)

**Estimate:** 5 horas | **Label:** `backend`, `MVP`

---

#### [1.3] Criar Endpoint de Análise Exploratória (EDA)
- [ ] Endpoint GET /api/v1/datasets/{id}/analysis/
- [ ] Retornar: estatísticas descritivas, distribuição de fraude, info de colunas
- [ ] Usar pandas para calcular stats
- [ ] Cache de resultados (opcional)
- [ ] Tratamento de datasets grandes (paginação)

**Estimate:** 4 horas | **Label:** `backend`, `MVP`

---

#### [1.4] Criar Modelo de ML e Endpoint de Treinamento
- [ ] Modelar Django: MLModel (nome, algoritmo, dataset_id, status, metrics, created_at)
- [ ] Preprocessamento: codificação, normalização, train/test split
- [ ] Implementar treinamento com Random Forest
- [ ] Serializar modelo com joblib
- [ ] Endpoint POST /api/v1/models/train/ (aceita parâmetros de algoritmo)
- [ ] Retornar métricas de treinamento: accuracy, precision, recall, f1, roc_auc

**Estimate:** 6 horas | **Label:** `backend`, `MVP`

---

#### [1.5] Criar Endpoint de Predição
- [ ] Endpoint POST /api/v1/predictions/ (aceita dados de transação)
- [ ] Carregar modelo treinado
- [ ] Realizar predição (fraude/legítimo + confiança)
- [ ] Salvar histórico de predição
- [ ] Retornar resultado estruturado com explicação básica

**Estimate:** 4 horas | **Label:** `backend`, `MVP`

---

#### [1.6] Configurar PostgreSQL e Migrations
- [ ] Configurar Django para PostgreSQL
- [ ] Criar migrations para modelos
- [ ] Seeders básicos (opcional)
- [ ] Backup strategy documentada

**Estimate:** 2 horas | **Label:** `backend`, `infra`

---

### Frontend

#### [1.7] Inicializar React e Setup Básico
- [ ] Criar projeto React (Vite ou CRA)
- [ ] Instalar dependências: React Router, Axios, TailwindCSS
- [ ] Estruturar rotas principais
- [ ] Criar layout base (Navbar, Footer, Layout wrapper)
- [ ] Setup de contexto global para autenticação (preparado para depois)

**Estimate:** 3 horas | **Label:** `frontend`, `MVP`

---

#### [1.8] Criar Página de Upload e Análise EDA
- [ ] Componente de upload (drag & drop ou input)
- [ ] Exibir preview de dados após upload
- [ ] Tela de análise com estatísticas (tabelas e números principais)
- [ ] Integração com endpoint /api/v1/datasets/{id}/analysis/
- [ ] Loading states durante requisição

**Estimate:** 4 horas | **Label:** `frontend`, `MVP`

---

#### [1.9] Criar Página de Treinamento de Modelo
- [ ] Formulário para seleção de algoritmo
- [ ] Seleção de dataset (lista carregada)
- [ ] Botão para iniciar treinamento
- [ ] Display de progresso/status
- [ ] Exibir métricas após conclusão
- [ ] Integração com endpoint /api/v1/models/train/

**Estimate:** 4 horas | **Label:** `frontend`, `MVP`

---

#### [1.10] Criar Página de Predição
- [ ] Formulário com campos de entrada (amount, type, balances)
- [ ] Seleção de modelo treinado
- [ ] Botão para executar predição
- [ ] Exibir resultado (Fraude: Sim/Não, Confiança: %)
- [ ] Integração com endpoint /api/v1/predictions/

**Estimate:** 3 horas | **Label:** `frontend`, `MVP`

---

#### [1.11] Integração Básica Frontend-Backend
- [ ] Criar serviço api.js com cliente Axios configurado
- [ ] Conexão com endpoints do backend
- [ ] Tratamento de erros
- [ ] Loading states globais

**Estimate:** 2 horas | **Label:** `frontend`, `MVP`

---

**Fim Fase 1:** MVP funcional, usuário pode fazer upload, análise, treinar modelo e fazer predições.

---

## Fase 2: Experiência do Usuário e Expansão ML (2 semanas)

Objetivo: Melhorar UX, adicionar mais algoritmos, comparação de modelos e visualizações.

### Backend

#### [2.1] Suporte a Múltiplos Algoritmos
- [ ] Implementar treinamento com SVM
- [ ] Implementar treinamento com Gradient Boosting
- [ ] Implementar treinamento com Logistic Regression
- [ ] Refatorar código de treinamento (factory pattern)
- [ ] Endpoint parametrizado com escolha de algoritmo

**Estimate:** 5 horas | **Label:** `backend`, `ML`

---

#### [2.2] Endpoint de Comparação de Modelos
- [ ] Endpoint GET /api/v1/models/comparison/
- [ ] Retornar lista com métricas de todos os modelos
- [ ] Filtros por dataset, algoritmo, data
- [ ] Ranking/sorting por métrica
- [ ] Suportar gráficos comparativos no frontend

**Estimate:** 3 horas | **Label:** `backend`

---

#### [2.3] Histórico e Persistência de Execuções
- [ ] Modelar PredictionLog (modelo_id, input, output, timestamp)
- [ ] Salvar todas as predições executadas
- [ ] Endpoint GET /api/v1/predictions/history/
- [ ] Paginação e filtros (por modelo, data, resultado)

**Estimate:** 3 horas | **Label:** `backend`

---

#### [2.4] Análise Detalhada e Métricas Avançadas
- [ ] Endpoint para retornar confusion matrix
- [ ] Endpoint para retornar ROC curve data (FPR, TPR)
- [ ] Endpoint para feature importance
- [ ] Endpoint para distribuição de predições

**Estimate:** 4 horas | **Label:** `backend`, `ML`

---

### Frontend

#### [2.5] Dashboard com Visualizações Interativas
- [ ] Página dashboard mostrando overview
- [ ] Cards com KPIs (total modelos, predições, acurácia média)
- [ ] Gráficos com Recharts: distribuição de fraude, acurácia por algoritmo
- [ ] Integração com dados do backend

**Estimate:** 5 horas | **Label:** `frontend`, `UI`

---

#### [2.6] Página de Comparação de Modelos
- [ ] Tabela comparativa com todos os modelos
- [ ] Colunas: algoritmo, acurácia, precision, recall, F1, ROC-AUC
- [ ] Gráfico radar para comparação visual
- [ ] Filtros e sorting
- [ ] Ação para deletar/exportar modelo

**Estimate:** 4 horas | **Label:** `frontend`, `UI`

---

#### [2.7] Melhorias no Upload (Drag & Drop)
- [ ] Componente de upload com drag & drop
- [ ] Validação de arquivo no frontend
- [ ] Mensagens de erro claras
- [ ] Preview detalhado dos dados carregados

**Estimate:** 3 horas | **Label:** `frontend`, `UI`

---

#### [2.8] Histórico de Operações
- [ ] Página de histórico com lista de predições
- [ ] Tabela com colunas: timestamp, modelo, input, resultado, confiança
- [ ] Paginação
- [ ] Filtros (por modelo, data, resultado)
- [ ] Opção de exportar para CSV

**Estimate:** 3 horas | **Label:** `frontend`, `UI`

---

**Fim Fase 2:** Aplicação mais completa, com múltiplos algoritmos, comparação e melhor UX.

---

## Fase 3: Robustez e Profissionalização (2 semanas)

Objetivo: Adicionar segurança, testes, documentação de API e tratamento de erros robusto.

### Backend

#### [3.1] Autenticação com JWT
- [ ] Modelar User (email, password, created_at)
- [ ] Endpoints de registro e login
- [ ] Gerar JWT token
- [ ] Validar token em endpoints protegidos
- [ ] Refresh token (opcional)
- [ ] Logout/blacklist de tokens

**Estimate:** 5 horas | **Label:** `backend`, `security`

---

#### [3.2] Autorização e Isolamento de Dados
- [ ] Cada usuário só vê seus datasets e modelos
- [ ] Adicionar user_id aos modelos Dataset, MLModel, PredictionLog
- [ ] Filtrar dados por usuário autenticado
- [ ] Testes de segurança básicos

**Estimate:** 3 horas | **Label:** `backend`, `security`

---

#### [3.3] Validação e Tratamento de Erros Avançados
- [ ] Criar exception handlers customizados
- [ ] Validar schema de input em todos endpoints
- [ ] Mensagens de erro informativas e estruturadas
- [ ] HTTP status codes apropriados
- [ ] Logging de erros (Sentry ou local)

**Estimate:** 4 horas | **Label:** `backend`

---

#### [3.4] Testes Automatizados Backend
- [ ] Setup pytest + pytest-django
- [ ] Testes unitários para preprocessamento ML
- [ ] Testes de endpoints principais (POST upload, GET analysis, POST train, POST predict)
- [ ] Testes de autenticação
- [ ] Cobertura: mínimo 70%

**Estimate:** 6 horas | **Label:** `backend`, `QA`

---

#### [3.5] Documentação com Swagger/OpenAPI
- [ ] Instalar drf-spectacular
- [ ] Documentar todos endpoints com descrição, parâmetros, responses
- [ ] Gerar schema OpenAPI
- [ ] Disponibilizar UI Swagger em /api/docs/

**Estimate:** 3 horas | **Label:** `backend`, `doc`

---

### Frontend

#### [3.6] Sistema de Autenticação (Login/Logout)
- [ ] Página de login
- [ ] Armazenar JWT no localStorage
- [ ] Context para gerenciar estado de autenticação
- [ ] Redirecionar para login se não autenticado
- [ ] Logout com limpeza de token

**Estimate:** 4 horas | **Label:** `frontend`, `security`

---

#### [3.7] Páginas Protegidas e Redirecionamento
- [ ] Layout privado para usuários autenticados
- [ ] Route guards (PrivateRoute component)
- [ ] Redirecionar não-autenticados para login
- [ ] Exibir nome/email do usuário

**Estimate:** 2 horas | **Label:** `frontend`, `security`

---

#### [3.8] Loading States, Validações e UX Melhorada
- [ ] Loading skeletons em componentes pesados
- [ ] Validação de formulários (React Hook Form)
- [ ] Mensagens de erro e sucesso (toast/snackbar)
- [ ] Confirmação antes de ações destrutivas
- [ ] Foco em acessibilidade (ARIA labels, teclado)

**Estimate:** 4 horas | **Label:** `frontend`, `UI`

---

#### [3.9] Testes Automatizados Frontend
- [ ] Setup Jest + React Testing Library
- [ ] Testes de componentes principais
- [ ] Testes de integração (requisições mock)
- [ ] Testes de autenticação
- [ ] Cobertura: mínimo 60%

**Estimate:** 5 horas | **Label:** `frontend`, `QA`

---

#### [3.10] Documentação e Storybook (Opcional)
- [ ] Storybook para componentes reutilizáveis
- [ ] Documentação de cada página
- [ ] Guia de uso e padrões

**Estimate:** 3 horas | **Label:** `frontend`, `doc`

---

**Fim Fase 3:** Aplicação robusta, segura, testada e bem documentada.

---

## Fase 4: Deploy e CI/CD (1 semana)

Objetivo: Preparar aplicação para produção, automatizar builds/testes e fazer deploy.

#### [4.1] Setup de Ambiente de Produção
- [ ] Docker Compose PRD (otimizações)
- [ ] Variáveis de ambiente separadas (dev/prod)
- [ ] Nginx como reverse proxy
- [ ] SSL/HTTPS (certificado auto-assinado local ou Let's Encrypt)
- [ ] Backup strategy para banco de dados

**Estimate:** 4 horas | **Label:** `infra`, `deployment`

---

#### [4.2] Configurar CI/CD com GitHub Actions
- [ ] Workflow para testar backend (pytest)
- [ ] Workflow para testar frontend (Jest)
- [ ] Workflow para build Docker
- [ ] Validação de linting e formatting
- [ ] Documentar em /docs/ci-cd.md

**Estimate:** 5 horas | **Label:** `infra`, `deployment`

---

#### [4.3] Deploy em Plataforma Cloud
- [ ] Escolher plataforma (Railway, Render, Fly.io, AWS, Heroku)
- [ ] Deploy backend
- [ ] Deploy frontend
- [ ] Configurar domínio
- [ ] Testes de smoke em produção

**Estimate:** 4 horas | **Label:** `infra`, `deployment`

---

#### [4.4] Monitoramento e Observabilidade
- [ ] Setup Sentry para erro tracking
- [ ] Logs estruturados
- [ ] Health checks (/health endpoint)
- [ ] Documentação de troubleshooting

**Estimate:** 3 horas | **Label:** `infra`, `ops`

---

#### [4.5] Documentação Final
- [ ] README com link de demo ao vivo
- [ ] Guia de deployment
- [ ] Guia de troubleshooting
- [ ] Documentação de arquitetura atualizada
- [ ] CHANGELOG

**Estimate:** 3 horas | **Label:** `doc`

---

**Fim Fase 4:** Aplicação em produção, pronta para uso e demo.

---

## Fase 5: Diferenciais de Portfólio (1 semana)

Objetivo: Adicionar funcionalidades que destaquem no portfólio e demonstrem expertise.

#### [5.1] Explicabilidade de Predições (LIME/SHAP)
- [ ] Integrar LIME ou SHAP no backend
- [ ] Endpoint para explicação de predição individual
- [ ] Frontend: visualizar feature importance da predição
- [ ] Documentar limite de interpretabilidade

**Estimate:** 5 horas | **Label:** `enhancement`, `ML`

---

#### [5.2] Relatórios e Exportação
- [ ] Gerar relatório PDF com análise completa
- [ ] Exportar dados em CSV/JSON
- [ ] Endpoint para gerar relatório
- [ ] Visualização de relatórios gerados

**Estimate:** 3 horas | **Label:** `enhancement`

---

#### [5.3] Notificações por Email
- [ ] Enviar email quando treinamento completa
- [ ] Alertas de predição suspeita
- [ ] Celery + Redis para tasks assíncronas (opcional)
- [ ] Template de emails

**Estimate:** 3 horas | **Label:** `enhancement`

---

#### [5.4] Onboarding e Tutorial Interativo
- [ ] Tutorial passo-a-passo na primeira vez
- [ ] Tooltips em funcionalidades principais
- [ ] Vídeo embed de demo (YouTube)
- [ ] FAQ com respostas a perguntas comuns

**Estimate:** 3 horas | **Label:** `enhancement`, `UX`

---

#### [5.5] Analytics e Monitoramento
- [ ] Integrar Google Analytics ou Plausible
- [ ] Rastrear eventos principais (upload, treinamento, predição)
- [ ] Dashboard de uso
- [ ] Relatório de performance

**Estimate:** 2 horas | **Label:** `enhancement`, `ops`

---

#### [5.6] Community e Documentação Avançada
- [ ] CONTRIBUTING.md
- [ ] CODE_OF_CONDUCT.md
- [ ] GitHub Issues templates
- [ ] Discussion forum ou Discord (opcional)
- [ ] Blog post sobre o projeto

**Estimate:** 3 horas | **Label:** `doc`

---

**Fim Fase 5:** Projeto pronto e destacado para portfólio, com extra features que demonstram expertise.

---

## Resumo de Estimativas

| Fase | Tempo | Issues | Peso |
|------|-------|--------|------|
| Fase 0 | 1 semana | 4 | Preparação |
| Fase 1 | 2 semanas | 11 | MVP |
| Fase 2 | 2 semanas | 8 | Expansão |
| Fase 3 | 2 semanas | 10 | Profissionalização |
| Fase 4 | 1 semana | 5 | Deploy |
| Fase 5 | 1 semana | 6 | Portfólio |
| **Total** | **9 semanas** | **44** | **Production-Ready** |

---

## Como Usar Este Roadmap

1. **Criar Milestones no GitHub** para cada fase
2. **Converter cada [X.X] em uma Issue** com descripção, labels e estimate
3. **Usar Project Board** para visualizar progresso (Kanban: To Do, In Progress, Done)
4. **Revisar regularmente** (weekly/bi-weekly) e ajustar conforme necessário
5. **Documentar decisões** em ADRs quando mudar direção

---

## Links Úteis

- [Django REST Framework Docs](https://www.django-rest-framework.org/)
- [React Docs](https://react.dev/)
- [GitHub Project Management](https://docs.github.com/en/issues/planning-and-tracking-with-projects)
- [Semantic Versioning](https://semver.org/)

---

**Versão:** 1.0  
**Última Atualização:** 14 de maio de 2026  
**Mantido por:** Yuri Komuta

