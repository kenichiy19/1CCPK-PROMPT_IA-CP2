# 1CCPK-PROMPT_IA-CP2

Ferramenta de linha de comando para comparação de técnicas de prompting (Zero-Shot, Few-Shot, Chain-of-Thought e Role Prompting) aplicadas a tarefas de e-commerce.

---

## Domínio

Reviews de smartphones em e-commerce brasileiro (produto: Samsung Galaxy A07).

**Tarefas implementadas:**
- `classificacao_sentimento` — classifica reviews como POSITIVO, NEGATIVO ou MISTO
- `extracao_entidades` — extrai produto, marca, pontos positivos e negativos
- `sumarizacao_reviews` — resume grupos de reviews em bullet points

---

## Requisitos

- Python 3.10+
- [Ollama](https://ollama.com/download) instalado e rodando localmente
- Modelo `llama3.2` baixado via Ollama

---

## Instalação

**1. Clone o repositório ou extraia o ZIP:**
```bash
cd checkpoint-2-PromptToolkit
```

**2. Instale as dependências:**
```bash
pip install requests python-dotenv tiktoken pandas matplotlib
```

**3. Instale e inicie o Ollama:**

Baixe em https://ollama.com/download e instale. O Ollama sobe automaticamente ao iniciar o Windows.

**4. Baixe o modelo:**
```bash
ollama pull llama3.2
```

---

## Configuração

Crie um arquivo `.env` na raiz do projeto com o seguinte conteúdo:

```
OLLAMA_HOST=http://localhost:11434
OLLAMA_MODEL=llama3.2
OLLAMA_TIMEOUT=120
OLLAMA_MAX_RETRIES=3
```

> O arquivo `.env.example` serve como modelo de referência.

---

## Estrutura do Projeto

```
checkpoint-2-PromptToolkit/
├── README.md
├── requirements.txt
├── .env.example
├── main.py
├── src/
│   ├── __init__.py
│   ├── llm_client.py
│   ├── prompt_builder.py
│   ├── techniques.py
│   ├── tasks.py
│   ├── evaluator.py
│   └── report.py
├── data/
│   ├── inputs.json
│   └── examples.json
├── prompts/
│   ├── system_prompts.json
│   └── templates.json
├── output/
│   ├── resultados.csv
│   └── graficos/
└── docs/
    └── CP02_NomeDoGrupo.pdf
```

---

## Execução

Na raiz do projeto, execute:

```bash
python main.py
```

O toolkit irá:
1. Carregar os dados de `data/inputs.json` e `prompts/`
2. Aplicar as 4 técnicas de prompting em cada tarefa e input
3. Medir acurácia, tokens e tempo de cada execução
4. Testar temperaturas (0.1, 0.5, 1.0) no melhor prompt
5. Gerar relatório CSV em `output/resultados.csv`
6. Gerar gráficos PNG em `output/graficos/`
7. Exibir recomendação da melhor técnica por tarefa

---

## Arquitetura

```
inputs.json → prompt_builder → techniques (ZS/FS/CoT/Role) → llm_client → evaluator → report → output/
```

| Módulo | Responsabilidade |
|---|---|
| `llm_client.py` | Conexão com a API REST do Ollama |
| `prompt_builder.py` | Montagem e estruturação dos prompts |
| `techniques.py` | Implementação das 4 técnicas de prompting |
| `tasks.py` | Definição das tarefas do domínio |
| `evaluator.py` | Métricas de acurácia, tokens e consistência |
| `report.py` | Geração de tabelas e gráficos comparativos |

---

## Stack

- **Linguagem:** Python 3.10+
- **LLM:** Ollama API (local) com modelo `llama3.2`
- **Tokens:** tiktoken
- **Visualização:** matplotlib + pandas
- **Sem API paga** — 100% gratuito e local
