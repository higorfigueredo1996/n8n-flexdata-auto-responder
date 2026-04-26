# 🚀 Quick Start - Começar em 5 Minutos

Quer começar **agora mesmo** sem ler toda a documentação? Este guia é pra você!

---

## 1️⃣ Pré-requisitos Rápidos (2 min)

```bash
✅ Conta N8N (https://n8n.cloud)
✅ Conta Groq (https://groq.com)
✅ Microsoft Outlook conectado
```

---

## 2️⃣ Obter API Key Groq (1 min)

1. Vá em: https://console.groq.com/keys
2. Clique: **Create API Key**
3. Copie a chave (`gsk_...`)
4. **Guarde** em um lugar seguro

---

## 3️⃣ Criar Workflow no N8N (2 min)

### Opção A: Usar JSON (Super rápido!)

1. Abra N8N
2. Clique: **+ New Workflow**
3. Menu: **File → Import → From File**
4. Escolha o arquivo `n8n-workflow.json` deste repositório
5. **Pronto!** Workflow importado

### Opção B: Criar manualmente

Se preferir criar do zero, siga o `README.md` seção "Configuração Passo a Passo".

---

## 4️⃣ Configurar Credenciais (1 min)

**No nó HTTP Request:**
1. Clique em **Authentication**
2. Escolha **Bearer Auth**
3. Cole sua chave Groq: `gsk_...`
4. Salve ✅

**No Outlook Trigger:**
1. Escolha sua conta Microsoft Outlook
2. Pronto! ✅

---

## 5️⃣ Testar em 30 segundos

```bash
1. Clique: "Publish" (canto superior direito)
2. Abra Gmail
3. Envie email para sua conta Outlook com:
   Assunto: "Qual é o horário?"
   Corpo: "Que horas vocês atendem?"
4. Aguarde 5 segundos
5. Verifique resposta no Outlook 📧
```

**Resposta esperada:**
```
Olá! Nosso horário de atendimento é de segunda a sexta, 
das 8h às 18h. Posso ajudar com mais alguma coisa?
```

---

## 🎉 Pronto!

Seu workflow está ativo e respondendo automaticamente!

---

## ❓ Algo deu errado?

### Resposta não chega?

```bash
1. Verifique API Key (está correta?)
2. Veja logs no N8N: Executions → ver erro
3. Leia "Troubleshooting" no README.md
```

### Email não dispara workflow?

```bash
1. Workflow está "Published"?
2. Outlook trigger está ativo?
3. Email foi para a caixa correta?
```

### Resposta errada?

```bash
1. Edite o prompt no HTTP Request
2. Adicione/modifique as FAQs
3. Teste novamente
```

---

## 📚 Próximos Passos

Agora que funciona, leia:

1. **README.md** - Documentação completa
2. **CHANGELOG.md** - Histórico e roadmap
3. **Customizar FAQs** - Adicione suas próprias perguntas

---

## 💡 Dicas Profissionais

### 1. Teste antes de ir pra produção

```bash
1. Use TEST_MODE=true no .env
2. Configure TEST_EMAIL
3. Teste com emails falsos
4. Valide as respostas
5. Depois ativa pra verdade
```

### 2. Monitore as execuções

N8N Dashboard → Executions
- ✅ Verde = sucesso
- ❌ Vermelho = erro
- Clique para ver detalhes

### 3. Customize as FAQs

Edite o campo `"content"` do HTTP Request:
```json
"content": "Você é um assistente...

FAQs:
1. Seu texto aqui
2. Outro FAQ
..."
```

### 4. Controle a IA

No HTTP Request body:
```json
"temperature": 0.7,    // 0=robótico, 1=criativo
"max_tokens": 500      // comprimento máximo
```

---

## 🔐 Segurança

⚠️ **IMPORTANTE:**

```bash
❌ Nunca commite .env com API Keys
✅ Use .env.example como template
✅ Adicione .env ao .gitignore
✅ Revise logs regularmente
```

---

## 📊 Custos

**Estimativa para 1000 emails/mês:**

| Serviço | Custo |
|---------|-------|
| Groq | $0-0.10 |
| N8N Cloud | $10-25 |
| Outlook | Incluso |
| **Total** | **$10-25/mês** |

vs OpenAI: **$50-200/mês** 🎯

---

## 🆘 Precisa de Ajuda?

1. Verifique [Troubleshooting](./README.md#-troubleshooting) no README
2. Abra uma [Issue](../../issues)
3. Consulte [Documentação N8N](https://docs.n8n.io)
4. Consulte [Docs Groq](https://console.groq.com/docs)

---

## ✨ Parabéns!

Você tem um sistema de **automação de respostas baseado em IA** rodando! 🚀

**Próximo**: Customize as FAQs e coloque mais clientes para usar.

---

**Criado com ❤️ para quem ama automação**

Última atualização: Abril 2026
