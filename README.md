# OmniFlow :gear:  
**Unified Pipeline for AI-Ready Data**  
*Seamlessly connect, process, and optimize data for AI workflows*  

[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Python](https://img.shields.io/badge/Python-3.9%2B-brightgreen)](https://www.python.org/)
[![Documentation](https://img.shields.io/badge/Docs-Read%20Here-orange)](https://omniflow.dev/docs)

---

## Overview  
OmniFlow is an open-source Python library that unifies **data ingestion**, **processing**, and **AI optimization** across applications, databases, and documents. Built for developers tired of stitching together fragmented pipelines, it combines the strengths of:  
- **Airweave** (secure app/database connectors + RBAC)  
- **Percival** (document AI for PDFs/emails)  
- **Chonkie** (context-aware chunking)  
- **Morphik** (multimodal RAG & knowledge graphs)  

Transform messy JSON, XML, or PDFs into **AI-ready structured data** with one line of code.  

---

## Features  

### :link: **Universal Connectors**  
- Connect to REST APIs, SQL databases, GraphQL, or local files (PDF/Excel/CSV) with built-in **MCP** and **RBAC** support.  
```python
from omniflow.connectors import AirweaveClient  
client = AirweaveClient(source="salesforce", protocol="MCP")  
data = client.fetch(query="SELECT * FROM invoices WHERE year=2024")  