# ChromaDB in Swarms-Memory

## Overview

ChromaDB is a powerful, open-source embedding database that is designed for AI applications. It allows you to store embeddings alongside their metadata and perform similarity searches to retrieve relevant information. Swarms-Memory provides seamless integration with ChromaDB, making it easy to incorporate vector storage and retrieval into your multi-agent systems.

## Key Features

- **Vector Storage**: Efficiently stores and indexes vector embeddings.
- **Similarity Search**: Performs fast and accurate similarity searches to retrieve relevant data based on vector similarity.
- **Metadata Filtering**: Allows you to filter search results based on metadata associated with embeddings.
- **Persistence**: Supports persistent storage of data to disk.
- **Client-Server and In-Memory Modes**: Can be used in both client-server and in-memory configurations.
- **Customizable**: Offers various options for customization, including distance metrics and indexing parameters.

## Parameters

When initializing ChromaDB in Swarms-Memory, you can configure the following parameters:

| Parameter     | Description                                                                 | Default Value |
|---------------|-----------------------------------------------------------------------------|---------------|
| `metric`        | Distance metric to use for similarity search (e.g., "cosine", "l2", "ip"). | `"cosine"`    |
| `output_dir`    | Directory to store ChromaDB data (for persistent storage).                 | `"results"`   |
| `limit_tokens`  | Maximum number of tokens to consider for document indexing.                | `1000`        |
| `n_results`     | Number of search results to return.                                        | `2`           |
| `docs_folder`   | Path to a folder containing documents to index (optional).                 | `None`        |
| `verbose`       | Enable verbose logging.                                                     | `False`       |

## Usage Examples

### Basic Initialization

```python
from swarms_memory import ChromaDB

chromadb = ChromaDB(
    metric="cosine",
    output_dir="results",
    verbose=True,
)
```

### Adding and Querying Documents

```python
chromadb.add("This is a document about Swarms agents.", {"source": "doc1"})
chromadb.add("Swarms framework enables multi-agent collaboration.", {"source": "doc2"})

results = chromadb.query("What are Swarms agents?", n_results=3)

for result in results:
    print(f"Document ID: {result['id']}")
    print(f"Text: {result['document']}")
    print(f"Metadata: {result['metadatas']}")
    print(f"Distance: {result['distances']}")
    print("---")
```

### Traversing a Directory of Documents

```python
chromadb = ChromaDB(docs_folder="path/to/your/documents")
chromadb.traverse_directory()

results = chromadb.query("Find information about Swarms.", n_results=5)
# ... process results ...
```

## Advanced Features

### Metadata Filtering

ChromaDB allows you to filter search results based on metadata. For example:

```python
results = chromadb.query(
    "Search for documents about agents.",
    n_results=3,
    filter={"source": "doc1"}
)
```

### Distance Metrics

You can choose different distance metrics based on your needs. Common metrics include:

- `"cosine"`: Cosine similarity (default).
- `"l2"`: L2 distance (Euclidean distance).
- `"ip"`: Inner product.

Specify the metric during ChromaDB initialization:

```python
chromadb = ChromaDB(metric="l2")
```

### Persistent Storage

By default, ChromaDB stores data in the `output_dir` specified during initialization. This ensures data persistence across sessions.

## More Information

For more detailed information about ChromaDB, refer to the official [ChromaDB documentation](https://chromadb.com/docs).

---