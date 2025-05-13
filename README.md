# Flowisy :gear:  
**Unified Pipeline for AI-Ready Data**  
*Seamlessly connect, process, and optimize data for AI workflows*  

## About Flowisy
Flowisy is a powerful open-source library that emerged from our MVP development agency's real-world projects. During our journey of building various AI applications, we identified a common need for a unified data processing pipeline that could handle diverse data sources and prepare them for AI workflows efficiently.

What started as an internal tool to streamline our development process has evolved into a comprehensive solution that we're now excited to share with the open-source community. We're currently in the process of cleaning up the codebase, improving documentation, and preparing it for public release. As we continue to refine and document each component, we'll be sharing more of the codebase with the community.

Our goal is to help other developers avoid the common pitfalls of building fragmented data pipelines and provide them with a robust, production-ready solution that combines the best practices we've learned through our extensive experience in AI application development.

[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Python](https://img.shields.io/badge/Python-3.9%2B-brightgreen)](https://www.python.org/)
[![Documentation](https://img.shields.io/badge/Docs-Read%20Here-orange)](https://omniflow.dev/docs)

---

## Overview  
Flowisy is an open-source Python library that unifies **data ingestion**, **processing**, and **AI optimization** across applications, databases, and documents. Built for developers tired of stitching together fragmented pipelines, it combines the strengths of:  
 

Transform messy JSON, XML, or PDFs into **AI-ready structured data** with one line of code.  
# Flowisy: AI-Ready Operations Framework

## Overview

Flowisy (AI-Ready Operations) is an open-source Python library that combines the core functionalities of Airweave, Morphik, Percival, and Chonkie into a unified framework. The primary purpose is to prepare API-sourced JSON and XML data for AI processing and querying, with additional capabilities for document processing, knowledge graph creation, and intelligent data retrieval.

## Core Components

### 1. Data Connector Module (`flowisy.connect`)
Inspired by Airweave's connectivity features:
- Universal connectors for applications, databases, URLs, and APIs
- Support for multiple authentication methods
- MCP (Multi-Cloud Platform) integration
- RBAC (Role-Based Access Control) for data security
- Standardized data extraction from various sources

### 2. Document Processing Module (`flowisy.document`)
Based on Percival and Chonkie's capabilities:
- Intelligent document parsing (PDFs, spreadsheets, images)
- Document chunking for optimal AI processing
- Data structure preservation during chunking
- Automatic field extraction and classification
- Purchase order and price list specialized processing

### 3. Knowledge Engine Module (`flowisy.knowledge`)
Drawing from Morphik's knowledge graph capabilities:
- Automated knowledge graph construction
- Entity and relationship extraction
- Multimodal data ingestion (text, images, audio)
- Semantic linking between data points
- Graph-based query interfaces

### 4. AI Integration Module (`flowisy.ai`)
The core for preparing data for AI:
- Context optimization for LLM token limits
- Query transformation and enhancement
- Embedding generation and management
- Vector store integration
- Response synthesis and validation

### 5. Workflow Orchestration (`flowisy.flow`)
For building automated data pipelines:
- Configurable workflow definitions
- Event-based triggering
- Parallel and sequential processing
- Error handling and retry mechanisms
- Monitoring and logging

## Key Features

1. **Universal Data Preparation**
   - Convert any source data (JSON, XML, CSV, etc.) into AI-ready formats
   - Normalize inconsistent data structures
   - Detect and handle schema variations

2. **Intelligent Chunking**
   - Context-aware document segmentation
   - Preservation of semantic relationships across chunks
   - Customizable chunking strategies based on content type
   - Automatic metadata generation for chunks

3. **Knowledge Graph Integration**
   - Automatic generation of knowledge graphs from processed data
   - Entity resolution across multiple data sources
   - Relationship inference and confidence scoring
   - Graph-based retrieval for enhanced context

4. **API First Design**
   - RESTful and GraphQL interfaces for all components
   - Webhook support for integration with external systems
   - Streaming capabilities for real-time data processing
   - SDK clients for popular programming languages

5. **Security and Compliance**
   - Fine-grained access control
   - Data lineage tracking
   - PII detection and anonymization
   - Audit logging for compliance

## Architecture Design

```
                           ┌───────────────────┐
                           │   Flowisy Core    │
                           └─────────┬─────────┘
                                     │
        ┌──────────────────┬─────────┼─────────┬──────────────────┐
        │                  │                   │                  │
┌───────▼───────┐  ┌───────▼───────┐  ┌───────▼───────┐  ┌───────▼───────┐
│  Data Connect  │  │Document Process│  │Knowledge Engine│  │ AI Integration│
└───────┬───────┘  └───────┬───────┘  └───────┬───────┘  └───────┬───────┘
        │                  │                   │                  │
        └──────────────────┴─────────┬─────────┴──────────────────┘
                                     │
                           ┌─────────▼─────────┐
                           │Flow Orchestration │
                           └─────────┬─────────┘
                                     │
                           ┌─────────▼─────────┐
                           │  Client Apps/API  │
                           └───────────────────┘
```

## Implementation Approach

### Core Data Models

```python
# Key data models that will be used throughout the library

class Document:
    """Represents a processed document with metadata and content"""
    id: str
    content: Union[str, bytes]
    metadata: Dict[str, Any]
    chunks: List["DocumentChunk"]
    
class DocumentChunk:
    """A semantically meaningful segment of a document"""
    id: str
    content: str
    metadata: Dict[str, Any]
    embedding: Optional[List[float]]
    relationships: List["ChunkRelationship"]

class Entity:
    """A recognized entity within the knowledge graph"""
    id: str
    type: str
    attributes: Dict[str, Any]
    sources: List[DocumentChunk]
    
class Relationship:
    """A connection between entities in the knowledge graph"""
    source_entity: Entity
    target_entity: Entity
    type: str
    confidence: float
    metadata: Dict[str, Any]
```

### Key Public APIs

```python
# Examples of the main APIs the library will expose

# Data Connection
connector = flowisy.connect.create_connector(
    source_type="api",
    connection_params={
        "url": "https://api.example.com/data",
        "auth_type": "oauth2",
        "credentials": {...}
    }
)
data = connector.fetch_data(query_params={...})

# Document Processing
processor = flowisy.document.create_processor(
    document_type="purchase_order",
    processing_options={
        "extraction_fields": ["vendor", "items", "total"],
        "language": "en"
    }
)
processed_doc = processor.process(raw_document)

# Chunking
chunker = flowisy.document.create_chunker(
    strategy="semantic",
    options={
        "max_chunk_size": 1000,
        "overlap": 100
    }
)
chunks = chunker.chunk(processed_doc)

# Knowledge Graph
knowledge_engine = flowisy.knowledge.create_engine()
knowledge_engine.ingest(chunks)
query_result = knowledge_engine.query(
    "What vendors have price increases in the last quarter?"
)

# AI Integration
ai_processor = flowisy.ai.create_processor(
    model="gpt-4",
    options={
        "max_tokens": 8192,
        "temperature": 0.7
    }
)
enhanced_data = ai_processor.prepare_context(chunks, query)
response = ai_processor.generate_response(enhanced_data)

# Workflow Orchestration
workflow = flowisy.flow.create_workflow("document_processing")
workflow.add_step("connect", connector.fetch_data)
workflow.add_step("process", processor.process, depends_on=["connect"])
workflow.add_step("chunk", chunker.chunk, depends_on=["process"])
workflow.add_step("ingest", knowledge_engine.ingest, depends_on=["chunk"])
workflow.execute()
```

## Data Flow Examples

### Example 1: Processing JSON API Data

```python
# Example workflow for processing JSON API data

import flowisy

# 1. Connect to API source
connector = flowisy.connect.APIConnector(
    url="https://api.example.com/products", 
    auth=flowisy.connect.OAuth2Auth(client_id="...", client_secret="...")
)

# 2. Extract and normalize JSON data
raw_data = connector.fetch()
normalized_data = flowisy.transform.normalize_json(
    raw_data, 
    schema_mapping={"product_id": "id", "product_name": "name"}
)

# 3. Create chunks optimized for AI processing
chunks = flowisy.document.chunk_json(
    normalized_data,
    strategy="semantic",
    max_chunk_size=1000
)

# 4. Create knowledge graph from chunks
knowledge = flowisy.knowledge.create_graph(chunks)

# 5. Prepare for AI integration
ai_ready_data = flowisy.ai.prepare_context(
    query="Find products with price increases",
    knowledge_graph=knowledge,
    chunks=chunks
)

# 6. Query using AI capabilities
results = flowisy.ai.query(ai_ready_data, model="gpt-4")
```

### Example 2: Processing XML Data from Enterprise API

```python
# Example for processing XML data from enterprise systems

# 1. Connect to enterprise XML API
connector = flowisy.connect.EnterpriseConnector(
    source_type="xml_api",
    connection_string="...",
    rbac_profile="read_only"
)

# 2. Extract and transform XML to structured format
xml_data = connector.fetch(query="//Orders[date > '2023-01-01']")
structured_data = flowisy.transform.xml_to_structured(xml_data)

# 3. Process with document understanding
processed_data = flowisy.document.process(
    structured_data,
    processor_type="order_processor",
    extraction_fields=["customer", "items", "pricing"]
)

# 4. Build knowledge representation
knowledge = flowisy.knowledge.build(
    processed_data,
    entity_types=["Customer", "Product", "Order"],
    relationship_types=["Ordered", "Contains"]
)

# 5. Create AI-optimized context
context = flowisy.ai.create_context(
    knowledge=knowledge,
    query_intent="pricing_analysis"
)

# 6. Generate insights
insights = flowisy.ai.generate_insights(context)
```

## Extensibility and Plugins

Flowisy is designed with a plugin architecture to allow for easy extension:

- Custom connectors for proprietary systems
- Custom document processors for specialized formats
- Domain-specific knowledge graph schemas
- Custom AI model integrations
- Industry-specific workflows

Plugins can be registered using:

```python
flowisy.register_plugin(
    plugin_type="connector",
    name="my_custom_connector",
    implementation=MyCustomConnector
)
```

## Deployment Options

1. **Python Library**
   - Install via pip: `pip install flowisy`
   - Import in Python applications

2. **Containerized Service**
   - Docker image with all dependencies
   - Kubernetes deployment templates

3. **API Service**
   - RESTful API server
   - GraphQL endpoint

4. **Command Line Interface**
   - For batch processing and automation

## Development Roadmap

1. **Phase 1: Core Framework**
   - Data connection module
   - Basic document processing
   - Simple chunking strategies
   - Initial AI integration

2. **Phase 2: Advanced Features**
   - Knowledge graph implementation
   - Advanced document understanding
   - Workflow orchestration
   - Expanded connector ecosystem

3. **Phase 3: Enterprise Features**
   - Advanced security and RBAC
   - Scalability improvements
   - Monitoring and observability
   - Enterprise integration patterns

4. **Phase 4: Ecosystem**
   - Plugin marketplace
   - Community contributions
   - Industry-specific solutions
   - Integration with popular AI frameworks
# Flowisy: AI-Ready Operations Framework

## Overview

Flowisy (AI-Ready Operations) is an open-source Python library that combines the core functionalities of Airweave, Morphik, Percival, and Chonkie into a unified framework. The primary purpose is to prepare API-sourced JSON and XML data for AI processing and querying, with additional capabilities for document processing, knowledge graph creation, and intelligent data retrieval.

## Core Components

### 1. Data Connector Module (`flowisy.connect`)
Inspired by Airweave's connectivity features:
- Universal connectors for applications, databases, URLs, and APIs
- Support for multiple authentication methods
- MCP (Multi-Cloud Platform) integration
- RBAC (Role-Based Access Control) for data security
- Standardized data extraction from various sources

### 2. Document Processing Module (`flowisy.document`)
Based on Percival and Chonkie's capabilities:
- Intelligent document parsing (PDFs, spreadsheets, images)
- Document chunking for optimal AI processing
- Data structure preservation during chunking
- Automatic field extraction and classification
- Purchase order and price list specialized processing

### 3. Knowledge Engine Module (`flowisy.knowledge`)
Drawing from Morphik's knowledge graph capabilities:
- Automated knowledge graph construction
- Entity and relationship extraction
- Multimodal data ingestion (text, images, audio)
- Semantic linking between data points
- Graph-based query interfaces

### 4. AI Integration Module (`flowisy.ai`)
The core for preparing data for AI:
- Context optimization for LLM token limits
- Query transformation and enhancement
- Embedding generation and management
- Vector store integration
- Response synthesis and validation

### 5. Workflow Orchestration (`flowisy.flow`)
For building automated data pipelines:
- Configurable workflow definitions
- Event-based triggering
- Parallel and sequential processing
- Error handling and retry mechanisms
- Monitoring and logging

## Key Features

1. **Universal Data Preparation**
   - Convert any source data (JSON, XML, CSV, etc.) into AI-ready formats
   - Normalize inconsistent data structures
   - Detect and handle schema variations

2. **Intelligent Chunking**
   - Context-aware document segmentation
   - Preservation of semantic relationships across chunks
   - Customizable chunking strategies based on content type
   - Automatic metadata generation for chunks

3. **Knowledge Graph Integration**
   - Automatic generation of knowledge graphs from processed data
   - Entity resolution across multiple data sources
   - Relationship inference and confidence scoring
   - Graph-based retrieval for enhanced context

4. **API First Design**
   - RESTful and GraphQL interfaces for all components
   - Webhook support for integration with external systems
   - Streaming capabilities for real-time data processing
   - SDK clients for popular programming languages

5. **Security and Compliance**
   - Fine-grained access control
   - Data lineage tracking
   - PII detection and anonymization
   - Audit logging for compliance

## Architecture Design

```
                           ┌───────────────────┐
                           │   Flowisy Core    │
                           └─────────┬─────────┘
                                     │
        ┌──────────────────┬─────────┼─────────┬──────────────────┐
        │                  │                   │                  │
┌───────▼───────┐  ┌───────▼───────┐  ┌───────▼───────┐  ┌───────▼───────┐
│  Data Connect  │  │Document Process│  │Knowledge Engine│  │ AI Integration│
└───────┬───────┘  └───────┬───────┘  └───────┬───────┘  └───────┬───────┘
        │                  │                   │                  │
        └──────────────────┴─────────┬─────────┴──────────────────┘
                                     │
                           ┌─────────▼─────────┐
                           │Flow Orchestration │
                           └─────────┬─────────┘
                                     │
                           ┌─────────▼─────────┐
                           │  Client Apps/API  │
                           └───────────────────┘
```

## Implementation Approach

### Core Data Models

```python
# Key data models that will be used throughout the library

class Document:
    """Represents a processed document with metadata and content"""
    id: str
    content: Union[str, bytes]
    metadata: Dict[str, Any]
    chunks: List["DocumentChunk"]
    
class DocumentChunk:
    """A semantically meaningful segment of a document"""
    id: str
    content: str
    metadata: Dict[str, Any]
    embedding: Optional[List[float]]
    relationships: List["ChunkRelationship"]

class Entity:
    """A recognized entity within the knowledge graph"""
    id: str
    type: str
    attributes: Dict[str, Any]
    sources: List[DocumentChunk]
    
class Relationship:
    """A connection between entities in the knowledge graph"""
    source_entity: Entity
    target_entity: Entity
    type: str
    confidence: float
    metadata: Dict[str, Any]
```

### Key Public APIs

```python
# Examples of the main APIs the library will expose

# Data Connection
connector = flowisy.connect.create_connector(
    source_type="api",
    connection_params={
        "url": "https://api.example.com/data",
        "auth_type": "oauth2",
        "credentials": {...}
    }
)
data = connector.fetch_data(query_params={...})

# Document Processing
processor = flowisy.document.create_processor(
    document_type="purchase_order",
    processing_options={
        "extraction_fields": ["vendor", "items", "total"],
        "language": "en"
    }
)
processed_doc = processor.process(raw_document)

# Chunking
chunker = flowisy.document.create_chunker(
    strategy="semantic",
    options={
        "max_chunk_size": 1000,
        "overlap": 100
    }
)
chunks = chunker.chunk(processed_doc)

# Knowledge Graph
knowledge_engine = flowisy.knowledge.create_engine()
knowledge_engine.ingest(chunks)
query_result = knowledge_engine.query(
    "What vendors have price increases in the last quarter?"
)

# AI Integration
ai_processor = flowisy.ai.create_processor(
    model="gpt-4",
    options={
        "max_tokens": 8192,
        "temperature": 0.7
    }
)
enhanced_data = ai_processor.prepare_context(chunks, query)
response = ai_processor.generate_response(enhanced_data)

# Workflow Orchestration
workflow = flowisy.flow.create_workflow("document_processing")
workflow.add_step("connect", connector.fetch_data)
workflow.add_step("process", processor.process, depends_on=["connect"])
workflow.add_step("chunk", chunker.chunk, depends_on=["process"])
workflow.add_step("ingest", knowledge_engine.ingest, depends_on=["chunk"])
workflow.execute()
```

## Data Flow Examples

### Example 1: Processing JSON API Data

```python
# Example workflow for processing JSON API data

import flowisy

# 1. Connect to API source
connector = flowisy.connect.APIConnector(
    url="https://api.example.com/products", 
    auth=flowisy.connect.OAuth2Auth(client_id="...", client_secret="...")
)

# 2. Extract and normalize JSON data
raw_data = connector.fetch()
normalized_data = flowisy.transform.normalize_json(
    raw_data, 
    schema_mapping={"product_id": "id", "product_name": "name"}
)

# 3. Create chunks optimized for AI processing
chunks = flowisy.document.chunk_json(
    normalized_data,
    strategy="semantic",
    max_chunk_size=1000
)

# 4. Create knowledge graph from chunks
knowledge = flowisy.knowledge.create_graph(chunks)

# 5. Prepare for AI integration
ai_ready_data = flowisy.ai.prepare_context(
    query="Find products with price increases",
    knowledge_graph=knowledge,
    chunks=chunks
)

# 6. Query using AI capabilities
results = flowisy.ai.query(ai_ready_data, model="gpt-4")
```

### Example 2: Processing XML Data from Enterprise API

```python
# Example for processing XML data from enterprise systems

# 1. Connect to enterprise XML API
connector = flowisy.connect.EnterpriseConnector(
    source_type="xml_api",
    connection_string="...",
    rbac_profile="read_only"
)

# 2. Extract and transform XML to structured format
xml_data = connector.fetch(query="//Orders[date > '2023-01-01']")
structured_data = flowisy.transform.xml_to_structured(xml_data)

# 3. Process with document understanding
processed_data = flowisy.document.process(
    structured_data,
    processor_type="order_processor",
    extraction_fields=["customer", "items", "pricing"]
)

# 4. Build knowledge representation
knowledge = flowisy.knowledge.build(
    processed_data,
    entity_types=["Customer", "Product", "Order"],
    relationship_types=["Ordered", "Contains"]
)

# 5. Create AI-optimized context
context = flowisy.ai.create_context(
    knowledge=knowledge,
    query_intent="pricing_analysis"
)

# 6. Generate insights
insights = flowisy.ai.generate_insights(context)
```

## Extensibility and Plugins

Flowisy is designed with a plugin architecture to allow for easy extension:

- Custom connectors for proprietary systems
- Custom document processors for specialized formats
- Domain-specific knowledge graph schemas
- Custom AI model integrations
- Industry-specific workflows

Plugins can be registered using:

```python
flowisy.register_plugin(
    plugin_type="connector",
    name="my_custom_connector",
    implementation=MyCustomConnector
)
```

## Deployment Options

1. **Python Library**
   - Install via pip: `pip install flowisy`
   - Import in Python applications

2. **Containerized Service**
   - Docker image with all dependencies
   - Kubernetes deployment templates

3. **API Service**
   - RESTful API server
   - GraphQL endpoint

4. **Command Line Interface**
   - For batch processing and automation

## Development Roadmap

1. **Phase 1: Core Framework**
   - Data connection module
   - Basic document processing
   - Simple chunking strategies
   - Initial AI integration

2. **Phase 2: Advanced Features**
   - Knowledge graph implementation
   - Advanced document understanding
   - Workflow orchestration
   - Expanded connector ecosystem

3. **Phase 3: Enterprise Features**
   - Advanced security and RBAC
   - Scalability improvements
   - Monitoring and observability
   - Enterprise integration patterns

4. **Phase 4: Ecosystem**
   - Plugin marketplace
   - Community contributions
   - Industry-specific solutions
   - Integration with popular AI frameworks
