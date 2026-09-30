# Food Recommendation System with ChromaDB and RAG

A small collection of Python command-line apps that recommend foods using semantic search. A dataset of 185 dishes from 20 cuisines is embedded with a Sentence Transformers model (`all-MiniLM-L6-v2`) and stored in a ChromaDB vector database. You can then search it in plain language ("something spicy and light"), filter by cuisine or calories, or chat with a RAG chatbot that uses IBM Granite to turn search results into friendly recommendations.

## Project Structure

```
.
├── data/
│   └── FoodDataSet.json        # Food dataset (name, description, ingredients, cuisine, calories, nutrition)
├── shared_functions.py         # Data loading, ChromaDB collection setup and search helpers
├── interactive_search.py       # Interactive CLI for similarity search
├── advanced_search.py          # Search with cuisine and calorie filters
├── enhanced_rag_chatbot.py     # RAG chatbot using ChromaDB + IBM Granite (watsonx.ai)
├── calorie_checker.py          # Find foods that fit a calorie budget
├── results_limiter.py          # Shows how the number of results affects search quality
├── system_comparison.py        # Runs the same query through the different approaches
└── requirements.txt
```

## Setup

```bash
pip install -r requirements.txt
```

The core dependencies are `chromadb`, `sentence-transformers` and `ibm-watsonx-ai`. The RAG chatbot needs access to IBM watsonx.ai; it is configured for the course lab environment (`project_id="skills-network"`), so to run it elsewhere add your own API key and project ID in `enhanced_rag_chatbot.py`.

## Usage

Run any of the scripts directly, for example:

```bash
python interactive_search.py
python advanced_search.py
python enhanced_rag_chatbot.py
```

The dataset path is resolved relative to the project folder, so the scripts work from any working directory.

## How It Works

1. Each food item is turned into a text description (name, ingredients, cuisine, taste, nutrition).
2. The text is converted into embeddings and stored in a ChromaDB collection using cosine similarity.
3. A user query is embedded the same way and the closest foods are returned, optionally filtered by metadata such as cuisine or calories.
4. In the RAG chatbot, the retrieved foods are passed as context to the IBM Granite model, which writes the final answer.

## Acknowledgements

Built as part of the [IBM RAG and Agentic AI Professional Certificate](https://www.coursera.org/professional-certificates/ibm-rag-and-agentic-ai), offered by IBM through Coursera. The certificate covers LangChain, LangGraph, RAG pipelines, vector databases, multimodal AI, and agentic frameworks such as CrewAI, AG2, BeeAI, and the Model Context Protocol.
Model access is provided by [IBM watsonx.ai](https://www.ibm.com/products/watsonx-ai).
