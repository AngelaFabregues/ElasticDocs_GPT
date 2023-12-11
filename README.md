# ElasticDocs_GPT
Combining the search power of Elasticsearch with the Question Answering power of GPT

[Blog - ChatGPT and Elasticsearch: OpenAI meets private data](https://www.elastic.co/blog/chatgpt-elasticsearch-openai-meets-private-data)


![diagram](https://raw.githubusercontent.com/jeffvestal/ElasticDocs_GPT/main/images/ElasticChat%20GPT%20Diagram%20-%20No%20line%20text.jpeg)

1. Python interface accepts user questions
- Generate a hybrid search request for Elasticsearch
- BM25 match on the title field
- kNN search on the title-vector field
- Boost kNN search results to align scores
- Set size=1 to return only the top scored document
2. Search request is sent to Elasticsearch
3. Documentation body and original url are returned to python
4. API call is made to OpenAI ChatCompletion
- Prompt: "answer this question <question> using only this document <body_content from top search result>"
5. Generated response is returned to python
6. Python adds on original documentation source url to generated response and prints it to the screen for the user

# Examples
  ![autoscale](https://raw.githubusercontent.com/jeffvestal/ElasticDocs_GPT/main/images/elasticDocs%20GPT%20-%20elastic%20cloud%20autoscaling.png)
  
  ![apm](https://raw.githubusercontent.com/jeffvestal/ElasticDocs_GPT/main/images/elasticDocs%20GPT%20-%20elastic%20jvm%20apm.png)
  
  ![inference](https://github.com/jeffvestal/ElasticDocs_GPT/blob/main/images/elasticDocs%20GPT%20-%20inference%20processor.png)
  
  ![pii](https://raw.githubusercontent.com/jeffvestal/ElasticDocs_GPT/main/images/elasticDocs%20GPT%20-%20redact%20pii.png)

# Setup

1. Elasticsearch cluster (Elastic Cloud)
1. OpenAI account and API generation
1. Load an embedding model into Elasticsearch (Eland as bridge to load a Hugging Face model) <-- Does not work in local because of dependency issues with torch. Neither in Google colab.
1. Elasticsearch index creation and content ingestion (using a web crawler)
1. Search application with streamlit <-- adapted to work without embeddings.

# Run
1. Launch Elastic Cloud
1. Check there are documents in search-elastic-docs index
1. Export credentials (source credentials.source)
1. `pip install -r requirements.txt`
1. `streamlit run elasticdocs_gpt.py`
1. `open http://192.168.1.149:8501/` and test it with "Show me the API call for an inference processor"