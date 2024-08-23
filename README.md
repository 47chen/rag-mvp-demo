# LLM w/ RAG-mvp-demo

## How to use?
`cd path/to/project`

`python3 -m venv venv #for virtual env`

`source venv/bin/activate`

`pip3 install -r requirements.txt`

`Pull your PDFs in the data folder`

`python3 populate_database.py #generate db or use --reset to clear db`

`python3 query_data.py "ASK YOU QUESTION HERE"`

![Screenshot 2024-08-22 at 17 47 46](https://github.com/user-attachments/assets/3ee3be8a-17fd-4b05-b8d7-1e537fb4d5e3)
![Screenshot 2024-08-22 at 18 00 57](https://github.com/user-attachments/assets/da3ec15e-d751-455e-9201-f677ae289dcf)
![Screenshot 2024-08-22 at 18 04 04](https://github.com/user-attachments/assets/83e21707-1928-4a11-affd-2a5faf695e2b)


## What is Retrieval-Augmented Generation (RAG)?
**Definition**:
RAG is a technique that combines information retrieval and text generation. It retrieves relevant documents or pieces of information from a database and uses them to generate a coherent and contextually response

**Purpose**: The goal is to enhance the _quality_ and _relevant_ of generated text by grounding it in actual data or documents.

## Embedding Generation - Chunk:
**Definition**:
"Chunk" refer to breaking down a larger document i.e large PDFs/txt/.. into smaller, manageable pieces or "chunks".

**Purpose**: This make it easier to process and retrieve specific information from large documents.

## Package Usage

### Ollama(LLaMa2):
Ollama is a package that provides access to the LLama2 model, a large language model designed for natural language understanding and generation.

### LangChain:
LangChain is a framework for building applications with language models. It provides tools to manage the flow of data and interactions between different components. _It helps in orchestrating the various steps involved in your RAG pipeline, such as retrieving documents, chunking them, and generating responses._

### ChromaDB:
Chroma DB is a _vector database_ that stores and retrieves high-dimensional vectors efficiently. In this project, it is used to store the embeddings (vector representations) of the chunks of PDF files. This allows for efficient retrieval of relevant chunks based on the input query.

### pyPDF:
Python libraray Read PDFs 

### LangChain-Ollama-Embedding:
This is a specific integration that allows LangChain to use Ollama for generating embeddings. It helps in converting the text chunks from your PDF into vector representations that can be stored in Chroma DB for efficient retrieval.

## Work Flow

#### PDF Ingestion:
Use pyPDF to read the content of the PDF files.
Chunk the content into smaller pieces for easier processing.

#### Embedding Generation:
Use LangChain-Ollama-Embedding to convert the text chunks into vector embeddings.
Store these embeddings in Chroma DB.

#### Query Processing:
When a query is received, convert it into an embedding using the same embedding model.
Retrieve the most relevant chunks from Chroma DB based on the query embedding.

#### Response Generation:
Use Ollama (LLama2) to generate a response based on the retrieved chunks.
The response is grounded in the actual content of the PDF files, making it more accurate and relevant.
