# LLM POC

## Introduction

This project is PoC on LLM which would return list of matches based on a query. The data is list of big basket products list.

## Implementation

embed_save.py uses sentence transformer LLM model to vectorize the product list and saves the vectors in the quadrant DB (Also creating an output.csv file with vectors). The api.py provides an API endpoint "/query-search" with POST method with payload parameter "query".

Since sentence transformer only does similarity check on the parameters defined. The un-processed query is transformed into list of values based on the parameters defined for the products by openAI-GPT.

Then based on the values, similarity check is done on qdrant DB parameter vectors. The results are selected based on similarity.

### Installation & Run

Clone the repository to your local machine:

```bash
Activate venv: venv/Scripts/activate
Install the necessary dependencies : 
pip install -r requirements.txt

Now make sure Qdrant is running and accessible on the configured port.
First, download the latest Qdrant image from Dockerhub:
'docker pull qdrant/qdrant'

Then, run the service:
docker run -p 6333:6333 -p 6334:6334 \
    -v $(pwd)/qdrant_storage:/qdrant/storage:z \
    qdrant/qdrant

For vectorization Run: python -m embed_save.py
Run: uvicorn main:app --reload

```

### Prerequisites

Before you begin, ensure you have the following installed:
- Python 3.8+
- FastAPI
- Uvicorn (for serving the FastAPI application)
- Qdrant (running on localhost or a remote server)
- An OpenAI API key

## Results
The results are added in Query Search.postman_collection.json.
## Drawbacks

The code is a PoC on the tools and the code still needs to be improved to provide accurate results. The algorithm to select the right product based on query is naive and needs improvement.









