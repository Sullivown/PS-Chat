# PS-Chat
The code for delivering the ChatBot project for PS

# Install the Requirements in your terminal

```
pip install -r requirements.txt

```

# Upload your own documents
Put your documents into ``` ./docs/[cat_name]/ ``` for separate folders. The names of [cat_name] will appear as tickboxes so that you can choose one or multiple sources for chatting

# Upload your own questions
Create a  ```questions.txt``` file for each category of documents and put each question on a new line. Put your example questions in the ``` ./docs/[cat_name]/ ``` folder containing the relevent documents for that set of questions.

# Set your environment file as .env in the main folder

[See below regarding where to find your neo4j, OpenAI and Pinecone keys](#find-your-api-keys).

```
# This is the options that if you want to talk to your graph
NEO4J_URL="xxxxx"
NEO4J_USER="xxxxx"
NEO4J_PASSWORD="xxxxx"

# Your openai key
OPENAI_KEY="xxxxx"

# The pinecone of storing the embeddings of your pdf documents
PINECONE_KEY = "xxxxx"
PINECONE_ENV = "xxxxx"
PINECONE_INDEX = "xxxxx"

# The directory of storing your documents
PDF_DOC_DIR = "./docs" 

# Upload parameters change as you like
CHUNK_SIZE = 1000 
CHUNK_OVERLAP = 0

# Define the namespaces for customization. (You can ignore it)
PINECONE_PDF_NAMESPACE = "my-pdf" 
PINECONE_GRAPH_NAMESPACE = "my-graph" 

```

# Find your API keys

- Visit [OpenAI](https://help.openai.com/en/articles/4936850-where-do-i-find-my-secret-api-key) to retrieve API keys and insert into your .env file.
- Visit [Pinecone](https://docs.pinecone.io/docs/quickstart#2-get-and-verify-your-pinecone-api-key) to create and retrieve your API keys, and also retrieve your environment and index name from the dashboard.
- Visit [neo4j](https://neo4j.com/docs/browser-manual/current/operations/dbms-connection/) to retrieve URL


# Ingest your data
This could take a while if you have multiple documents. This function will upload the embeddings of your PDF documents and graph database to the cloud vector database.
You can uncomment the graph ingesting if you only want to upload a new pdf.

```
python ingest_data.py
```


# Launch your app
After ingesting your data, simply run main.py for local deployment and debugging.

```
python main.py
```

# Deploy your app using Gunicorn

```
gunicorn -w 2 -b :8000 main:app --timeout=120
```

# For port forwarding using Ngrok
Please refer https://ngrok.com/docs/getting-started/
