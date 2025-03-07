# Pinecone in Swarms-Memory

## Overview

Pinecone is a fully managed vector database service designed for scalable vector search. It's particularly well-suited for applications requiring real-time similarity search and high query throughput. Swarms-Memory integrates with Pinecone to provide a robust solution for managing and querying vector embeddings in the cloud.

## Key Features

- **Managed Service**: Pinecone handles infrastructure and scaling, allowing you to focus on your application.
- **Scalability**: Designed to scale to billions of vectors and high query volumes.
- **Real-time Querying**: Provides low-latency similarity search for real-time applications.
- **Hybrid Indexing**: Supports both sparse and dense vector indexing for improved search relevance.
- **Metadata Filtering**: Allows filtering of search results based on metadata.
- **Persistence**: Data is automatically persisted and backed up.

## Parameters

When initializing Pinecone in Swarms-Memory, you need to configure the following parameters:

| Parameter     | Description                                                                 | Required     |
|---------------|-----------------------------------------------------------------------------|--------------|
| `api_key`       | Pinecone API key for authentication.                                        | Yes          |
| `environment`   | Pinecone environment (e.g., "us-west1-gcp", "us-east1-aws").              | Yes          |
| `index_name`    | Name of the Pinecone index to connect to.                                   | Yes          |
| `embedding_function` | Custom function to generate embeddings (optional).                       | No           |
| `preprocess_function`| Custom function to preprocess text before embedding (optional).          | No           |
| `postprocess_function`| Custom function to postprocess query results (optional).             | No           |
| `logger_config` | Configuration for logging (optional).                                     | No           |

**Note**: You must set up a Pinecone index and obtain your API key and environment from the Pinecone dashboard before using Pinecone in Swarms-Memory.

## Usage Examples

### Basic Initialization

Before running the following examples, ensure you have set the `PINECONE_API_KEY` and `PINECONE_ENVIRONMENT` environment variables or pass them directly to the `PineconeMemory` constructor.

```python
import os
from swarms_memory import PineconeMemory

pinecone_memory = PineconeMemory(
    api_key=os.environ.get("PINECONE_API_KEY"),
    environment=os.environ.get("PINECONE_ENVIRONMENT"),
    index_name="your-index-name", # Replace with your Pinecone index name
)
```

### Adding and Querying Documents

```python
pinecone_memory.add(
    "Document about multi-agent systems.", {"category": "Multi-Agent"}
)
pinecone_memory.add(
    "Swarms enable complex AI workflows.", {"category": "Swarms"}
)

results = pinecone_memory.query(
    "What are multi-agent systems?", filter={"category": "Multi-Agent"}
)

for result in results:
    print(f"Score: {result['score']}")
    print(f"Text: {result['metadata']['text']}")
    print(f"Metadata: {result['metadata']}")
    print("---")
```

### Using Custom Functions

You can use custom embedding, preprocessing, and postprocessing functions as shown in the ChromaDB documentation. Simply pass these functions to the `PineconeMemory` constructor.

## Advanced Features

### Metadata Filtering

Pinecone supports rich metadata filtering capabilities. Refer to the Pinecone documentation for advanced filtering options.

### Scalability and Performance

Pinecone is designed for high scalability and performance. For large-scale applications, consider:

- Optimizing your Pinecone index configuration.
- Using appropriate index types and configurations for your data.
- Monitoring your Pinecone usage and scaling resources as needed.

## More Information

For more detailed information about Pinecone, refer to the official [Pinecone documentation](https://pinecone.io/docs).

---