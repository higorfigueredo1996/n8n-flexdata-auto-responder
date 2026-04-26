# N8N Automação de Respostas com Groq e FAQs

Automação inteligente de respostas de email usando Groq API e N8N, baseada em perguntas frequentes (FAQs) da empresa FlexData.

## 📋 Sobre o Projeto

Este projeto implementa um **workflow automático** que:
- ✅ Recebe emails via Microsoft Outlook
- ✅ Processa a pergunta com IA (Groq - Llama 3.3 70B)
- ✅ Responde automaticamente com base nas FAQs da empresa
- ✅ Envia a resposta de volta para o cliente

**Diferencial**: Usa **Groq em vez de ChatGPT/OpenAI**, otimizando custos e velocidade.

---

## 🚀 Tecnologias Utilizadas

| Tecnologia | Versão | Propósito |
|------------|--------|----------|
| **N8N** | Latest | Orquestração do workflow |
| **Groq API** | v1 | Processamento de IA (Llama 3.3 70B) |
| **Microsoft Outlook** | Integrado | Gatilho e envio de emails |
| **HTTP Request** | Nativo | Chamadas à API Groq |

---

## 💡 Por que Groq em vez de ChatGPT/OpenAI?

| Aspecto | Groq | ChatGPT/OpenAI |
|--------|------|-----------------|
| **Custo** | ~$0 (quota educacional) ou <$0.10/1M tokens | $3-15/1M tokens |
| **Velocidade** | ⚡ Extremamente rápida (<1s) | Normal |
| **Modelo** | Llama 3.3 70B (excelente) | GPT-4/3.5 |
| **Para FAQ/Email** | ✅ Perfeito | ✅ Perfeito |
| **Custo mensal** | ~$0 | $50-200+ |

**Conclusão**: Para tarefas determinísticas como FAQ, Groq oferece a melhor relação custo-benefício.

---

## 📦 Pré-requisitos

Antes de começar, você precisa de:

1. **Conta N8N** (https://n8n.cloud)
2. **Conta Groq** (https://groq.com) com API Key
3. **Microsoft Outlook** conectado (para receber/enviar emails)
4. **Email de teste** para validar o fluxo

---

## 🔧 Configuração Passo a Passo

### Passo 1: Obter API Key do Groq

```bash
1. Acesse https://console.groq.com/keys
2. Faça login com sua conta
3. Clique em "Create API Key"
4. Copie a chave (você só vê uma vez!)
```

**Exemplo de API Key:**
```
gsk_abc123xyz...
```

### Passo 2: Configurar N8N

#### 2.1 Criar Novo Workflow

```
Dashboard N8N → + New → Workflow
```

#### 2.2 Adicionar Nó: Microsoft Outlook Trigger

- **Nó**: Microsoft Outlook Trigger
- **Operação**: New email received
- **Conexão**: Conecte sua conta Outlook

Este nó dispara o workflow quando um email chega.

#### 2.3 Adicionar Nó: Edit Fields

- **Nó**: Edit Fields
- **Operação**: Manual
- **Campos a extrair**:
  - Remetente (`Remetente`)
  - Assunto (`Assunto`)
  - Corpo da mensagem (`Mensagem`)

#### 2.4 Adicionar Nó: HTTP Request (Groq API)

**Configuração:**

| Campo | Valor |
|-------|-------|
| **Method** | POST |
| **URL** | https://api.groq.com/openai/v1/chat/completions |
| **Authentication** | Bearer Auth |
| **Bearer Token** | Sua API Key do Groq |
| **Send Body** | ON |
| **Body Type** | JSON |

**Body (JSON):**

```json
{
  "model": "llama-3.3-70b-versatile",
  "messages": [
    {
      "role": "system",
      "content": "Você é um assistente virtual da empresa FlexData. Responda educadamente aos clientes com base nas perguntas frequentes abaixo. Se a pergunta não estiver nas perguntas frequentes, diga que o time de atendimento já está lá em contato.\n\nFAQs:\n1. Nosso horário de atendimento é de segunda a sexta, das 8h às 18h.\n2. Para emitir a segunda via da fatura, acesse https://flexdata.com.br/fatura.\n3. Para cancelamento, envie uma solicitação para cancelamento@flexdata.com.br.\n4. Nosso telefone é (11) 4000-1234.\n5. O prazo de resposta para suporte técnico é de até 24 horas úteis."
    },
    {
      "role": "user",
      "content": "{{ $json.bodyText }}"
    }
  ],
  "max_tokens": 500,
  "temperature": 0.7
}
```

#### 2.5 Adicionar Nó: Send a message (Outlook)

| Campo | Valor |
|-------|-------|
| **To** | `{{ $('Edit Fields').item.json.Remetente }}` |
| **Subject** | `RE: {{ $('Edit Fields').item.json.Assunto }}` |
| **Message** | `{{ $('HTTP Request').first().json.choices[0].message.content }}` |
| **Operation** | Send |

---

## 🧪 Testando o Workflow

### 1. Publicar o Workflow

Clique em **"Publish"** no canto superior direito.

### 2. Enviar Email de Teste

**De**: seu_email@gmail.com  
**Para**: seu_email_outlook@hotmail.com  
**Assunto**: "Qual é o horário de atendimento?"  
**Corpo**: "Olá, q horas vcs atendem?" (com erros de propósito)

### 3. Verificar Resposta Automática

Aguarde alguns segundos. A resposta automática deve chegar em seu Outlook:

```
De: seu_email_outlook@hotmail.com
Assunto: RE: Qual é o horário de atendimento?
Corpo: Olá! Nosso horário de atendimento é de segunda a sexta, 
das 8h às 18h. Posso ajudar com mais alguma coisa?
```

**Resultado esperado:**
✅ IA identificou a pergunta mesmo com erros de português  
✅ Respondeu corretamente com FAQ #1  
✅ Email foi enviado automaticamente

---

## 📊 Fluxograma do Workflow

```
┌─────────────────────────┐
│ Microsoft Outlook       │
│ (Email chega)           │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│ Edit Fields             │
│ (Extrai dados)          │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│ HTTP Request            │
│ (Groq API)              │
│ Llama 3.3 70B           │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│ Send a message (Outlook)│
│ (Resposta automática)   │
└─────────────────────────┘
```

---

## 🎯 Exemplos de Uso

### Exemplo 1: Pergunta sobre Horário

**Email recebido:**
```
De: cliente@example.com
Assunto: Qual é o horário de funcionamento?
Corpo: Olá, que horas a empresa trabalha?
```

**Resposta automática:**
```
De: seu_email@outlook.com
Assunto: RE: Qual é o horário de funcionamento?
Corpo: Olá! Nosso horário de atendimento é de segunda a sexta, 
das 8h às 18h. Posso ajudar com mais alguma coisa?
```

### Exemplo 2: Pergunta sobre Fatura

**Email recebido:**
```
De: cliente@example.com
Assunto: Preciso da segunda via da fatura
Corpo: Oi, como faço pra pegar a 2ª via?
```

**Resposta automática:**
```
De: seu_email@outlook.com
Assunto: RE: Preciso da segunda via da fatura
Corpo: Olá! Para emitir a segunda via da fatura, acesse 
https://flexdata.com.br/fatura. Posso ajudar com mais alguma coisa?
```

### Exemplo 3: Pergunta Fora das FAQs

**Email recebido:**
```
De: cliente@example.com
Assunto: Qual é a cor do seu logo?
Corpo: Pessoal, qual a cor do logo de vocês?
```

**Resposta automática:**
```
De: seu_email@outlook.com
Assunto: RE: Qual é a cor do seu logo?
Corpo: Olá! Essa pergunta não está em nossas FAQs, mas o time 
de atendimento já está lá em contato para ajudá-lo!
```

---

## 📝 Personalizando as FAQs

Para adicionar/modificar FAQs, edite o campo **"content"** do nó HTTP Request:

```json
"content": "Você é um assistente virtual da empresa FlexData...

FAQs:
1. Seu texto customizado aqui
2. Outro FAQ
3. Mais um FAQ
..."
```

---

## 🔐 Segurança

⚠️ **Boas práticas:**

- ✅ Nunca compartilhe sua API Key do Groq publicamente
- ✅ Use variáveis de ambiente para armazenar credenciais
- ✅ Revise os emails antes de automatizar (principalmente de produção)
- ✅ Teste com conta de dev primeiro
- ✅ Monitore execuções no N8N (aba "Executions")

---

## 💰 Estimativa de Custos

**Cenário**: 1.000 emails/mês

| Serviço | Custo |
|---------|-------|
| Groq (1M tokens/mês) | $0-0.10 |
| N8N (cloud) | $10-25/mês |
| Outlook | Incluso em Office 365 |
| **Total** | **$10-25/mês** |

**Comparação com OpenAI:** $50-200/mês

**Economia**: **60-80%** ✅

---

## 🛠️ Troubleshooting

### Problema: Email não dispara o workflow

**Solução:**
1. Verifique se o Outlook Trigger está "Publish"
2. Teste manualmente: clique em "Execute step"
3. Veja os logs em "Executions"

### Problema: Resposta automática não chega

**Solução:**
1. Cheque a API Key do Groq (expirou?)
2. Verifique se "Send a message" está configurado corretamente
3. Olhe o campo "Message" — está pegando a resposta?

### Problema: IA responde errado

**Solução:**
1. Revise o prompt do "system" (pode estar confuso)
2. Aumente `max_tokens` se a resposta está cortada
3. Ajuste `temperature` (mais baixo = mais consistente)

---

## 📚 Recursos Úteis

- [N8N Documentation](https://docs.n8n.io)
- [Groq API Docs](https://console.groq.com/docs)
- [Groq Models](https://console.groq.com/docs/models)
- [Microsoft Outlook Integration](https://docs.n8n.io/integrations/microsoft-outlook/)

---

## 🎓 Créditos

Este projeto foi desenvolvido como atividade prática do curso de **Automação com Alura**, com foco em:
- Arquitetura de workflows
- Integração de APIs
- Otimização de custos em IA

**Instrutor Original**: Aula "Fluxo para responder automaticamente com ChatGPT usando FAQs da empresa"  
**Implementação com Groq**: Otimização técnica e redução de custos

---

## 📄 Licença

Este projeto é fornecido como é, para fins educacionais.

---

## ✉️ Contato & Suporte

Dúvidas sobre este projeto?
- Abra uma **Issue** no repositório
- Consulte a documentação do N8N
- Acesse o suporte do Groq

---

**Desenvolvido com ❤️ e muita automação!**

Last updated: Abril 2026
