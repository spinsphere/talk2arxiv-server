# talk2arxiv-server
## Talk to any ArXiv paper using ChatGPT!
[Talk2arxiv](https://github.com/evanhu1/talk2arxiv) is an innovative open-source implementation of a standard RAG (Retrieval-Augmented Generation) system, designed to facilitate interactive conversations with academic papers. 

## Usage
Simply prepend any arxiv.org link with 'talk2' to load the paper into a responsive RAG chat application (e.g. www.arxiv.org/pdf/1706.03762.pdf -> www.talk2arxiv.org/pdf/1706.03762.pdf)

## Installation
This server has been tested on Linux only so far (including Amazon (AWS) Linux 2 on EC2 and Ubuntu 22.04 LTS on a Azure VM).
```
git clone https://github.com/evanhu1/talk2arxiv-server
cd talk2arxiv-server/
python3 -m pip install --user pipx
echo export PATH=$PATH:${HOME}/.local/bin >> ~/.bashrc
source ~/.bashrc
sudo apt install python3.10-venv (if running on Ubuntu)

(install dependencies:)
pip install pip-tools
python -m piptools compile -o requirements.txt pyproject.toml
pip install -r requirements.txt 

pipx install poetry
poetry install
poetry run python -m spacy download en_core_web_sm
poetry run gunicorn app:app -b 0.0.0.0:3001
```
You must also create a .env with the following defined:
```
COHERE_API_KEY=""
PINECONE_API_KEY=""
OPENAI_API_KEY="
```

## Features
- PDF Parsing: Utilizes GROBID for efficient text extraction from PDFs.
- Chunking Algorithm: Custom-built algorithm for optimal text chunking.
- Text Embedding: Implements Cohere's EmbedV3 model for accurate text embeddings.
- Vector Database Integration: Uses Pinecone for storing and querying embeddings.
- Contextual Relevance: Employs a reranking process to select the most relevant content based on user input.

## Technologies Used
* Poetry
* Python (tested with 3.10.12)
* Flask
* Gunicorn
* Nginx

## Credits
- SciPDF
- GROBID

## Roadmap
- Implement parallel processing
- Better caching of papers

## Known Issues
- The backend is not built to handle any level of scale, might fail with a lot of concurrent requests
