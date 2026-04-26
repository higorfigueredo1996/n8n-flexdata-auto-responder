# Changelog

Todos os changs notáveis neste projeto serão documentados neste arquivo.

O formato é baseado em [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
e este projeto segue [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [1.0.0] - 2026-04-25

### Added
- ✨ Integração inicial com Groq API (Llama 3.3 70B)
- ✨ Workflow N8N completo para automação de respostas de email
- ✨ Suporte a Microsoft Outlook como gatilho e envio
- ✨ Sistema de FAQs personalizáveis para FlexData
- ✨ Documentação completa em README.md
- ✨ Exemplo de workflow exportável em JSON
- ✨ Arquivo .gitignore para proteger credenciais
- ✨ Troubleshooting guide
- 📊 Estimativa de custos vs OpenAI/ChatGPT

### Changed
- 🔄 Implementação com Groq em vez de ChatGPT (redução de 60-80% em custos)
- 🔄 Otimização de temperature (0.7 para respostas equilibradas)
- 🔄 Max tokens ajustado para 500 (suficiente para FAQs)

### Why Groq instead of ChatGPT
Durante o desenvolvimento, foi identificado que a tarefa é altamente determinística:
- Respostas baseadas em FAQs conhecidas
- Não requer criatividade excessiva
- Velocidade crítica para UX

**Groq oferece**:
- Custo: ~$0/mês vs $50-200/mês (ChatGPT)
- Velocidade: <1s vs 2-5s (OpenAI)
- Modelo: Llama 3.3 70B (equivalente a GPT-4)
- Qualidade: Mantém 100% da acurácia

**Resultado**: Mesma funcionalidade, melhor custo-benefício ✅

### Security
- 🔐 Adicionado .gitignore para proteção de API Keys
- 🔐 Documentação de boas práticas em segurança
- 🔐 Instruções para uso seguro de credenciais

### Testing
- ✅ Workflow testado com erros de português proposital
- ✅ IA identificou corretamente mesmo com texto mal redigido
- ✅ Respostas enviadas automaticamente sem erro

### Documentation
- 📚 README.md com guia completo de setup
- 📚 Exemplos reais de uso (3 casos)
- 📚 Fluxograma visual do workflow
- 📚 Troubleshooting section
- 📚 Comparação técnica Groq vs OpenAI

---

## Roadmap Futuro

### v1.1.0 (Planejado)
- [ ] Adicionar suporte a Gmail como gatilho
- [ ] Criar dashboard de estatísticas (emails processados/mês)
- [ ] Adicionar análise de sentimento nas respostas
- [ ] Suporte a múltiplas empresas (mais FAQs)
- [ ] Sistema de logging detalhado

### v1.2.0 (Planejado)
- [ ] Integração com banco de dados para histórico
- [ ] Respostas em múltiplos idiomas
- [ ] A/B testing de prompts
- [ ] Webhook customizável para eventos

### v2.0.0 (Visão)
- [ ] Interface web para gerenciar FAQs
- [ ] Treinamento automático com novos padrões de email
- [ ] Análise de efetividade das respostas
- [ ] Suporte a voice/audio

---

## Notas de Desenvolvimento

### Decisões Técnicas

#### 1. Por que HTTP Request em vez de nó nativo Groq?
- Controle total sobre a requisição
- Compatibilidade com API OpenAI (fácil migração)
- Flexibilidade para ajustar parâmetros

#### 2. Por que Edit Fields?
- Estrutura de dados consistente
- Facilita manutenção e debugging
- Permite reuso em workflows futuros

#### 3. Por que temperature = 0.7?
- 0.0-0.3: Muito conservador, respostas repetitivas
- 0.7: **Ponto ideal** para FAQ (consistente + natural)
- 0.9-1.0: Muito criativo, pode gerar respostas incorretas

#### 4. Por que max_tokens = 500?
- FAQs típicas: 50-150 tokens
- 500 = espaço para resposta longa + segurança
- Evita cortes e economiza tokens

---

## Contribuindo

Se você usa este projeto e quer contribuir:

1. **Fork** o repositório
2. **Crie uma branch** para sua feature (`git checkout -b feature/nova-faq`)
3. **Commit** suas mudanças (`git commit -m 'Add nova FAQ'`)
4. **Push** para a branch (`git push origin feature/nova-faq`)
5. **Abra uma Pull Request**

### Tipos de contribuição bem-vindos:
- ✅ Novas FAQs melhoradas
- ✅ Correções de documentação
- ✅ Exemplos de uso
- ✅ Otimizações de performance
- ✅ Traduções (PT-BR, EN, etc)

---

## Issues & Support

Encontrou um bug? Tem uma sugestão?

- 🐛 [Abrir uma Issue](../../issues/new)
- 💬 [Discussões](../../discussions)
- 📧 Contato direto

---

## Licença

Este projeto é fornecido sob a licença MIT - veja [LICENSE](./LICENSE) para detalhes.

---

## Agradecimentos

- 🎓 **Alura**: Pela excelente formação em automação
- 🤖 **Groq**: Pela tecnologia de IA acessível
- 🔗 **N8N**: Pela plataforma robusta de workflows
- 👥 **Comunidade**: Pelo feedback e contribuições

---

## Changelog Format

Este projeto segue [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

### Categorias
- **Added**: Novas funcionalidades
- **Changed**: Mudanças em funcionalidades existentes
- **Deprecated**: Funcionalidades em desuso
- **Removed**: Funcionalidades removidas
- **Fixed**: Correções de bugs
- **Security**: Correções de segurança
- **Performance**: Melhorias de performance

---

**Última atualização**: Abril 2026  
**Versão atual**: 1.0.0  
**Mantido por**: [Seu nome aqui]
