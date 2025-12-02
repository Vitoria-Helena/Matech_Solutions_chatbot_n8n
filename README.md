## 🤖 Chatbot RAG com n8n: Conhecimento Específico e Orquestração Eficiente

Este projeto demonstra a construção de um **Chatbot inteligente e factual** usando a plataforma de automação **n8n** como motor de orquestração e a arquitetura de **Geração Aumentada por Recuperação (RAG)**.

O RAG permite que o chatbot utilize uma **base de conhecimento privada/específica** (documentos, manuais, relatórios) para responder a perguntas, garantindo precisão e relevância, algo que os modelos de linguagem grandes (LLMs) por si só não conseguiriam fazer.

---

### ✨ Destaques do Projeto

* **Orquestração via n8n:** Todo o fluxo de trabalho (desde o recebimento da consulta até a entrega da resposta) é gerenciado por *workflows* visuais no n8n.
* **Arquitetura RAG:** Implementação que assegura que as respostas sejam **fundamentadas em dados reais** do seu domínio.
* **Escalabilidade e Integração:** Fácil conexão com Bancos de Dados Vetoriais (Supabase Vector Store.) e diversos provedores de LLM (Gemini , Gemini Embeddings.).

---

### ⚙️ Como Funciona (O Fluxo RAG)

O fluxo é dividido em duas etapas principais que o n8n coordena:

1.  **Recuperação (Retrieval):**
    * A consulta do usuário é convertida em um vetor (embedding).
    * O n8n consulta o **Banco de Dados Vetorial** e recupera os trechos de documentos mais semanticamente similares.
2.  **Geração Aumentada (Augmented Generation):**
    * O n8n constrói um *prompt* avançado, combinando a consulta original com o **contexto** (os trechos recuperados).
    * O LLM é instruído a gerar a resposta **apenas** com base nesse contexto, garantindo a fidelidade da informação.

```mermaid
graph TD
    A[Usuário: Envia Pergunta] --> B(n8n Webhook: Recebe);
    B --> C{Criar Embedding da Consulta};
    C --> D[Consultar DB Vetorial];
    D --> E(Recuperar Contexto Relevante);
    E --> F[n8n: Construir Prompt Aumentado];
    F --> G{LLM: Gerar Resposta Factual};
    G --> H[n8n: Retornar Resposta];
    H --> I[Usuário: Recebe Resposta];
