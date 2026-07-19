# AI_Research_Paper_Intelligence_System_using_NLP_Transformers_Semantic_Search_and_Agentic_AI


## Overview

The AI Research Paper Intelligence System is an NLP-powered application designed to simplify the process of exploring academic research papers. By integrating semantic search, transformer-based language models, and Agentic AI, the system enables users to search, summarize, compare, and analyze research papers using natural language queries.

Unlike traditional keyword-based search systems, this project retrieves papers based on semantic similarity, allowing users to discover relevant research even when different terminology is used.

---

## Features

- Semantic search for research papers using vector embeddings
- Automatic research paper summarization
- Keyword and keyphrase extraction
- Named Entity Recognition (NER)
- AI-powered research paper comparison
- Conversational memory for follow-up questions
- Intelligent tool selection using LangChain Agents

---

## Dataset

The project uses the **ML-ArXiv-Papers** dataset available on Hugging Face.

Dataset preprocessing includes:

- Selecting the **Title** and **Abstract** columns
- Using the first **15,000** research papers
- Combining title and abstract into a single searchable text field
- Cleaning unnecessary whitespace and newline characters

---

## Semantic Search

Semantic search is implemented using the Sentence Transformer model:

```text
all-MiniLM-L6-v2
```

Each research paper is converted into a dense embedding that captures its semantic meaning rather than relying on exact keyword matching.

Generated embeddings are stored locally as:

```text
paper_embeddings.npy
```

If embeddings already exist, they are loaded directly instead of being regenerated.

---

## Similarity Search with FAISS

The generated embeddings are indexed using **FAISS (Facebook AI Similarity Search)** to enable efficient retrieval of relevant research papers.

The search workflow is:

1. Convert the user query into an embedding.
2. Normalize the query embedding.
3. Compare it against stored paper embeddings.
4. Retrieve the most relevant papers with similarity scores.

The FAISS index is saved as:

```text
paper_faiss.index
```

---

## Research Paper Summarization

Research paper abstracts are summarized using the transformer model:

```text
facebook/bart-large-cnn
```

A dedicated summarization function generates concise summaries for retrieved papers, making it easier to understand their main contributions.

---

## Keyword Extraction

Keyword extraction is performed using **KeyBERT**.

The system extracts:

- Important keywords
- Multi-word keyphrases
- Relevance scores for extracted terms

This functionality is also exposed as a tool within the AI agent.

---

## Named Entity Recognition

Named Entity Recognition (NER) is implemented using the Hugging Face Transformers pipeline.

The system identifies entities such as:

- Models
- Frameworks
- Organizations
- Datasets
- Technical concepts

The implementation uses:

```python
aggregation_strategy="simple"
```

to combine related tokens into complete entities.

---

## Groq LLM Integration

The conversational AI component uses the following Large Language Model through Groq:

```text
llama-3.1-8b-instant
```

The model is integrated using **ChatGroq** and is responsible for:

- Agent interactions
- Research paper comparison
- Natural language responses

The API key is securely accessed using Google Colab Secrets.

---

## Agentic AI

The project leverages **LangChain** to build an intelligent AI agent capable of selecting the appropriate tool based on the user's request.

The available tools include:

### Search and Summarize

Searches research papers using semantic similarity and generates summaries of the retrieved papers.

### Extract Keywords

Extracts important keywords and keyphrases from user-provided text.

### Compare Papers

Retrieves two research papers, summarizes them, and compares them based on:

- Objective
- Methodology
- Key Contributions
- Advantages
- Limitations
- Applications

### Get Last Search

Retrieves papers stored from the most recent search, allowing users to continue previous interactions without repeating the query.

---

## Conversational Memory

The project incorporates conversational memory using **LangGraph MemorySaver**.

Conversation history is maintained using a unique thread ID, enabling the system to understand follow-up questions.

For example:

```text
User:
Find the top 2 papers on Reinforcement Learning.

User:
Show my last search.

User:
What was the title of the first paper?
```

The assistant can answer these questions without repeating the search process.

---

## Project Workflow

```text
Load Dataset
        │
        ▼
Data Preprocessing
        │
        ▼
Generate Embeddings
        │
        ▼
Build FAISS Index
        │
        ▼
Semantic Search
        │
        ▼
Paper Summarization
        │
        ▼
Keyword Extraction
        │
        ▼
Named Entity Recognition
        │
        ▼
LangChain Agent
        │
        ▼
Conversational Response
```

---

## Technologies Used

- Python
- Pandas
- NumPy
- Hugging Face Datasets
- Sentence Transformers
- Scikit-learn
- FAISS
- Hugging Face Transformers
- KeyBERT
- LangChain
- LangGraph
- Groq LLM

---

## Models Used

| Model | Purpose |
|--------|---------|
| all-MiniLM-L6-v2 | Semantic Embeddings |
| facebook/bart-large-cnn | Research Paper Summarization |
| Hugging Face NER Pipeline | Named Entity Recognition |
| llama-3.1-8b-instant | Agent Interaction and Paper Comparison |

---

## Project Structure

```text
AI_Research_Paper_Intelligence_System/
│
├── AI_Research_Paper_Intelligence_System.ipynb
├── README.md
└── requirements.txt
```

Generated during execution:

```text
paper_embeddings.npy
paper_faiss.index
```

These generated files are excluded from the repository because they can be recreated whenever required.

---

## API Key Configuration

To enable the Agentic AI functionality:

1. Open **Google Colab Secrets**
2. Add your Groq API key.
3. Save it using the name:

```text
GROQ_API_KEY
```

4. Allow notebook access to the secret.

The notebook securely retrieves the key without exposing it in the source code.

---

## Example Queries

- Find the top 2 research papers on Vision Transformers.
- Find the top 2 research papers on Reinforcement Learning.
- Summarize the retrieved research papers.
- Compare two research papers on Machine Learning.
- Extract keywords from the provided abstract.
- Show my last search.
- What was the title of the first paper?

---

## Future Enhancements

- Support for PDF-based research paper ingestion
- Integration with vector databases such as Pinecone or Chroma
- Citation analysis
- Research recommendation system
- Streamlit-based web application
- Multi-document summarization

---

## Conclusion

The AI Research Paper Intelligence System demonstrates how Semantic Search, Transformer-based NLP models, and Agentic AI can be integrated into a unified research assistant. By combining Sentence Transformers, FAISS, BART, KeyBERT, LangChain, LangGraph, and Groq LLM, the system enables users to efficiently search, summarize, compare, and interact with research papers through natural language while maintaining conversational context.
