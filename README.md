# Enterprise-Grade AI Document Querying System using AWS Bedrock

## Overview

This project implements an enterprise-grade, end-to-end **Retrieval-Augmented Generation (RAG)** system for intelligent document querying. The solution leverages **Amazon Bedrock Knowledge Bases**, **Aurora Serverless PostgreSQL**, and **Amazon S3** to enable accurate, scalable, and context-aware question answering over structured and unstructured documents.

The system is designed with a strong focus on **cloud-native architecture**, **infrastructure as code**, and **production readiness**, making it suitable for real-world enterprise deployments.

---

## Key Capabilities

* Automated document ingestion and storage using Amazon S3
* Vector-based semantic indexing using Aurora Serverless PostgreSQL
* Managed Knowledge Base creation using Amazon Bedrock
* Context-aware response generation using Bedrock foundation models
* Infrastructure provisioning using Terraform (modular and reusable)
* Secure IAM role and policy configuration
* Scalable, serverless architecture

---

## High-Level Architecture

Documents (PDFs)
→ Amazon S3 (Document Storage)
→ Aurora Serverless PostgreSQL (Vector Store)
→ Amazon Bedrock Knowledge Base
→ Foundation Model (LLM + Embeddings)
→ Contextual Answer Generation

---

## Technology Stack

* Programming Language: Python
* Infrastructure as Code: Terraform
* Cloud Provider: Amazon Web Services (AWS)
* LLM Platform: Amazon Bedrock
* Vector Database: Aurora Serverless PostgreSQL
* Object Storage: Amazon S3
* IAM & Security: AWS IAM Roles and Policies

---

## Project Structure

project-root/
│
├── stack1/                  # Core infrastructure
│   ├── VPC
│   ├── Aurora Serverless PostgreSQL
│   ├── Amazon S3 bucket
│   └── IAM roles and policies
│
├── stack2/                  # AI layer
│   ├── Amazon Bedrock Knowledge Base
│   └── Associated IAM roles
│
├── modules/                 # Reusable Terraform modules
│   ├── aurora_serverless/
│   └── bedrock_kb/
│
├── scripts/
│   ├── aurora_sql.sql       # Vector database preparation
│   └── upload_to_s3.py      # Document ingestion script
│
├── app.py                   # Chat application logic
├── bedrock_utils.py         # Bedrock interaction utilities
├── tests/                   # Unit tests
└── README.md

---

## Workflow Explanation

### Infrastructure Provisioning

Terraform is used to provision all cloud resources, including networking, storage, databases, and IAM permissions. The infrastructure is split into two logical stacks for better maintainability and separation of concerns.

### Document Ingestion

Documents are uploaded to Amazon S3 using a Python-based ingestion script. The folder structure is preserved to maintain metadata consistency.

### Vector Storage Preparation

Aurora PostgreSQL is prepared using SQL scripts to support vector storage and similarity search. This enables efficient semantic retrieval of document content.

### Knowledge Base Integration

Amazon Bedrock Knowledge Base is configured to reference data stored in Aurora and S3. The Knowledge Base orchestrates retrieval and grounding of responses.

### Query Processing and Response Generation

User queries are validated and classified before being processed. Relevant document context is retrieved from the Knowledge Base and passed to a Bedrock foundation model, which generates a grounded, context-aware response.

---

## Deployment Steps

1. Clone the repository.

2. Navigate to `stack1` and initialize Terraform:

   terraform init
   terraform apply

3. Record outputs such as Aurora endpoint and resource identifiers.

4. Prepare the Aurora database using `scripts/aurora_sql.sql`.

5. Navigate to `stack2`, update variables using Stack 1 outputs, and deploy:

   terraform init
   terraform apply

6. Upload documents to S3:

   python scripts/upload_to_s3.py

7. Sync the data source in the Bedrock Knowledge Base.

---

## Improvements Over Basic RAG Systems

* Fully managed cloud-native architecture
* Serverless database for cost-efficient scaling
* Modular Terraform design for reuse and extension
* Secure IAM configuration following least-privilege principles
* Prompt validation and query categorization for safer LLM usage

---

## Individual Contributions

* Designed the end-to-end RAG system architecture
* Implemented Terraform modules for scalable infrastructure provisioning
* Integrated Amazon Bedrock Knowledge Base with Aurora PostgreSQL
* Developed Python utilities for document ingestion and LLM interaction
* Added prompt validation and query categorization logic
* Enabled source document referencing in chatbot responses

---

## Future Enhancements

* Support for additional document formats and data sources
* Streaming responses from Bedrock models
* Enhanced query classification and safety controls
* Monitoring and observability integration
* CI/CD automation for infrastructure and application updates

---

## Project Context

This project was developed collaboratively as part of a technical initiative and later refined individually to improve architectural clarity, robustness, and enterprise readiness. The repository reflects personal contributions and enhancements aligned with industry best practices.
