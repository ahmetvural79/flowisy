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

Universal Connectors to any app, database, URL or API (JSON/XML)

Ingestion & Chunking of heterogeneous data into RAG-ready embeddings

Knowledge Graph & Indexing of structured/unstructured content

RBAC & MCP enforcement on data access

Multimodal RAG pipeline (text, image, diagrams)

Document-to-AI Automation (e.g. purchase orders → structured data)

A plug-in architecture so each capability can be extended independently

Below is a breakdown of roles, structure, and data-flow
---

## Features 
Key Responsibilities
Connector Layer

Discover and authenticate to arbitrary sources (databases, REST APIs, file stores, URLs)

Normalize incoming JSON/XML (and other formats) into a uniform internal schema

Pre-Processing & Chunking

Clean, parse and split large documents into semantically meaningful chunks (Chonkie-style)

Extract tables, fields and metadata for downstream ML

Indexing & Knowledge Graph

Build vector indexes (via FAISS, etc.) for semantic search (Morphik-style RAG)

Construct a lightweight knowledge graph to model entity relationships

Access Control & Data Security

Enforce RBAC policies on every query (per-document, per-field)

Support MCP (multi-customer partitioning) so each tenant sees only its data

Multimodal Retrieval & RAG

Support embeddings for text, images, tables and other modalities

Expose a unified "retrieve + generate" API to plug in any LLM 

High-Level Architecture
Connectors ingest data.

Normalizer standardizes JSON/XML to internal models.

Chunker & Extractor breaks docs into pieces and pulls out key fields.

Index & KG Builder creates embeddings and populates a graph DB.

RBAC & MCP layer filters at query time.

Retrieval Engine performs semantic search + graph queries.

AI Layer takes retrieved context and runs an LLM (via user's choice of model).

Pipelines let you string these together into an automated workflow.

### :link: **Universal Connectors**  
- Connect to REST APIs, SQL databases, GraphQL, or local files (PDF/Excel/CSV) with built-in **MCP** and **RBAC** support.  
```python
from flowisy.connectors import Client  
client = Client(source="salesforce", protocol="MCP")  
data = client.fetch(query="SELECT * FROM invoices WHERE year=2024")  

:page_facing_up: Smart Document Processing
Extract tables, prices, and entities from PDFs/purchase orders (Percival's AI models).

Split large documents into semantic chunks optimized for LLM token limits (Chonkie engine).

:brain: AI-Ready Structuring
Auto-build knowledge graphs from unstructured data.

Generate RAG-optimized outputs with hybrid vector + graph search (Morphik core).

:shield: Enterprise-Grade Security
Role-based access control (RBAC) for data streams.

Audit trails for all pipeline operations.