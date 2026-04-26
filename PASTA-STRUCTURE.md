# 📁 Estrutura de Pastas Recomendada

Este documento descreve a estrutura de pastas recomendada para o repositório GitHub.

```
n8n-flexdata-auto-responder/
│
├── 📄 README.md                    # Documentação principal
├── 📄 QUICK_START.md              # Guia de início rápido
├── 📄 CHANGELOG.md                # Histórico de versões
├── 📄 LICENSE                     # Licença MIT
├── 📄 .gitignore                  # Arquivos a ignorar no git
├── 📄 .env.example                # Template de variáveis de ambiente
│
├── 📂 workflows/                  # Workflows N8N
│   ├── n8n-workflow.json          # Workflow principal exportado
│   └── README.md                  # Instruções para workflows
│
├── 📂 docs/                       # Documentação adicional
│   ├── SETUP.md                   # Guia de setup detalhado
│   ├── TROUBLESHOOTING.md         # Soluções de problemas
│   ├── ARCHITECTURE.md            # Explicação da arquitetura
│   ├── API_INTEGRATION.md         # Como integrar a API Groq
│   ├── CUSTOM_FAQS.md             # Como adicionar FAQs customizadas
│   ├── METRICS.md                 # Como coletar métricas
│   └── SECURITY.md                # Guia de segurança
│
├── 📂 examples/                   # Exemplos de uso
│   ├── email-test-1.txt           # Exemplo de email de teste
│   ├── email-test-2.txt           # Exemplo com erros de português
│   ├── faq-template.json          # Template de FAQs em JSON
│   └── response-samples.md        # Exemplos de respostas geradas
│
├── 📂 screenshots/                # Prints do workflow (documentação visual)
│   ├── 01-workflow-overview.png   # Visão geral do workflow
│   ├── 02-outlook-trigger.png     # Configuração do Outlook
│   ├── 03-http-request.png        # Configuração do HTTP Request
│   ├── 04-send-message.png        # Configuração do envio
│   └── 05-test-result.png         # Resultado do teste
│
├── 📂 scripts/                    # Scripts de automação
│   ├── setup.sh                   # Script de setup automático
│   ├── test-workflow.js           # Script para testar o workflow
│   └── backup-faqs.sh             # Script para backup de FAQs
│
├── 📂 config/                     # Arquivos de configuração
│   ├── faqs.json                  # FAQs em formato JSON
│   ├── prompts.json               # Prompts customizados
│   └── settings.json              # Configurações gerais
│
├── 📂 tests/                      # Testes
│   ├── unit/                      # Testes unitários
│   ├── integration/               # Testes de integração
│   └── README.md                  # Como rodar testes
│
├── 📂 assets/                     # Imagens, logos, etc
│   ├── logo.png                   # Logo do projeto
│   ├── banner.png                 # Banner para README
│   └── architecture-diagram.png   # Diagrama de arquitetura
│
└── 📂 .github/                    # Configurações do GitHub
    ├── workflows/                 # GitHub Actions
    │   ├── lint.yml              # Workflow de linting
    │   └── deploy.yml            # Workflow de deploy
    └── ISSUE_TEMPLATE/            # Templates de issues
        ├── bug_report.md
        └── feature_request.md
```

---

## 📝 Descrição de Cada Pasta

### 🔹 Raiz `/`
Arquivos principais e configuração:
- `README.md` - Documentação principal
- `CHANGELOG.md` - Histórico de versões
- `.gitignore` - Arquivos a ignorar
- `.env.example` - Template de variáveis

### 🔹 `/workflows`
Workflows N8N exportados e importáveis:
```
n8n-workflow.json    ← Importe isto no N8N para carregar o workflow
```

### 🔹 `/docs`
Documentação técnica em profundidade:
- `SETUP.md` - Guia passo a passo de setup
- `TROUBLESHOOTING.md` - Soluções de problemas comuns
- `ARCHITECTURE.md` - Como o sistema funciona internamente
- `CUSTOM_FAQS.md` - Como modificar as FAQs
- `SECURITY.md` - Boas práticas de segurança

### 🔹 `/examples`
Exemplos reais e templates:
```
email-test-1.txt      # Email de exemplo 1
email-test-2.txt      # Email com erros de português
faq-template.json     # Template para criar novas FAQs
```

### 🔹 `/screenshots`
Prints do workflow para documentação visual:
- Cada screenshot mostra uma parte do workflow
- Útil para quem prefere aprender visualmente

### 🔹 `/scripts`
Scripts de automação:
```bash
./setup.sh            # Instala dependências e configura
./test-workflow.js    # Testa o workflow
./backup-faqs.sh      # Faz backup das FAQs
```

### 🔹 `/config`
Arquivos de configuração:
```json
faqs.json             # Lista de FAQs em JSON
prompts.json          # Prompts customizados
settings.json         # Configurações gerais
```

### 🔹 `/tests`
Testes automáticos:
- `unit/` - Testes unitários
- `integration/` - Testes de integração completa

### 🔹 `/assets`
Recursos visuais:
- Logo, banners, diagramas

### 🔹 `/.github`
Configurações específicas do GitHub:
- GitHub Actions para CI/CD
- Templates de issues

---

## 🚀 Como Usar Esta Estrutura

### Passo 1: Clonar e Organizar

```bash
git clone https://github.com/seu-usuario/n8n-flexdata-auto-responder.git
cd n8n-flexdata-auto-responder
```

### Passo 2: Criar Pastas

```bash
mkdir -p workflows docs examples screenshots scripts config tests/{unit,integration} assets .github/workflows .github/ISSUE_TEMPLATE
```

### Passo 3: Populando Pastas

Coloque o conteúdo em cada pasta conforme descrito acima.

---

## 📊 Estrutura Ideal para Growth

### MVP (Versão 1.0)
```
📁 Apenas:
- README.md
- QUICK_START.md
- workflows/n8n-workflow.json
- .gitignore
- LICENSE
```

### v1.1 (Com mais funcionalidades)
```
📁 Adicionar:
- /docs (documentação)
- /examples (exemplos)
- /config (configurações)
```

### v2.0 (Produção)
```
📁 Adicionar tudo:
- /screenshots (visual docs)
- /scripts (automação)
- /tests (testes)
- /.github (CI/CD)
- /assets (branding)
```

---

## 💡 Boas Práticas

### Para README
- Mantenha conciso (leia em 5 min)
- Use emojis para scanear rápido
- Inclua badges (status, versão, etc)

### Para Documentação
- Use `/docs` para tudo técnico
- Cada documento tem um propósito
- Interlink entre documentos

### Para Exemplos
- Coloque em `/examples` com comentários
- Inclua casos de sucesso reais
- Mostre antes e depois

### Para Scripts
- Use em `/scripts` apenas
- Adicione comentários
- Inclua help (`script.sh --help`)

---

## 🔄 Exemplo de Fluxo de Contribuição

```
User clona repo
    ↓
Lê QUICK_START.md (5 min)
    ↓
Importa workflow.json no N8N
    ↓
Testa conforme docs/SETUP.md
    ↓
Customiza em config/faqs.json
    ↓
Faz Pull Request com melhorias
```

---

## 📝 Checklist para Publicar

Antes de fazer primeiro push:

- ✅ Adicionar LICENSE (MIT)
- ✅ Criar README.md principal
- ✅ Criar .gitignore
- ✅ Remover credenciais
- ✅ Adicionar screenshot
- ✅ Criar CHANGELOG.md
- ✅ Testar workflow.json

---

Estrutura criada para ser **clara, escalável e profissional**! 🎯

