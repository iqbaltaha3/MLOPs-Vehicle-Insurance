# MLOps Project – Vehicle Insurance Data Pipeline

This repository presents a production-oriented MLOps system that implements the complete machine learning lifecycle using modular architecture, cloud-native services, and CI/CD automation.

The project demonstrates how raw data moves through data ingestion, validation, transformation, model training, evaluation, registry, and deployment, following industry-grade MLOps practices.

⸻

## Architecture Overview

The system follows a pipeline-driven architecture with clear separation between:

• Configuration layer
• Entity and artifact layer
• Component layer (ingestion, validation, transformation, training, evaluation)
• Orchestration layer (training and prediction pipelines)
• Deployment layer (Docker + EC2)
• Automation layer (GitHub Actions CI/CD)

Each pipeline stage produces versioned artifacts, enabling traceability and reproducibility.

⸻

## Core MLOps Capabilities

• Schema-driven data validation
• Artifact-based pipeline execution
• Config-driven architecture using YAML and constants
• Centralized logging and custom exception handling
• Model versioning and registry using AWS S3
• Automated model evaluation with threshold-based promotion
• Containerized inference service
• End-to-end CI/CD with self-hosted runners

⸻

## Technology Stack

Programming and ML
• Python 3.10
• Pandas, NumPy
• Scikit-learn

Data Layer
• MongoDB Atlas (NoSQL source)

Cloud and MLOps
• AWS IAM (Access control)
• AWS S3 (Model registry)
• AWS ECR (Docker image registry)
• AWS EC2 (Model serving)

DevOps and Automation
• Docker
• GitHub Actions
• Self-hosted GitHub Runner

Configuration and Utilities
• YAML-based schema validation
• Custom logging and exception modules

⸻

## Project Initialization

Step 1: Project Template Generation

The project structure is generated using template.py, creating a scalable and modular codebase with predefined folders for components, pipelines, entities, configurations, and utilities.

Step 2: Local Package Management

Local packages are installed using setup.py and pyproject.toml, enabling clean imports and version control of internal modules.
Refer to crashcourse.txt for implementation details.

Step 3: Environment Setup

conda create -n vehicle python=3.10 -y
conda activate vehicle
pip install -r requirements.txt

Verify installed packages:

pip list


⸻

MongoDB Atlas Integration

Data Source Configuration

• MongoDB Atlas is used as the external data source
• A free M0 cluster is deployed
• Network access is opened for controlled testing
• Python connection string is used via environment variables

Data Upload

Data is pushed to MongoDB using a Jupyter notebook and later accessed programmatically during the ingestion phase.

⸻

Observability and Error Handling

• Centralized logging for all pipeline stages
• Custom exception handling for debugging and traceability
• Demo execution using demo.py

This ensures failures are traceable and pipelines are debuggable.

⸻

Data Ingestion Pipeline

• MongoDB connection logic isolated in configuration layer
• Raw data fetched in key-value format
• Data converted into structured DataFrame
• Ingestion artifacts generated and stored
• Pipeline execution controlled via training pipeline

MongoDB URL is injected using environment variables to avoid hardcoding secrets.

⸻

Data Validation

• Schema defined in config.schema.yaml
• Column names, data types, and null checks enforced
• Validation reports generated as artifacts

This step ensures data consistency before model training.

⸻

Data Transformation

• Feature encoding and scaling
• Transformation objects saved for inference reuse
• Estimator abstraction used for clean design

⸻

Model Training

• Model training implemented as a pipeline component
• Performance metrics logged
• Trained model saved as an artifact

⸻

Model Evaluation and Registry

• AWS S3 acts as a centralized model registry
• New model compared with existing deployed model
• Threshold-based evaluation controls promotion
• Only approved models are pushed to the registry

⸻

Deployment Architecture

• Flask-based prediction service
• Dockerized application
• Image stored in AWS ECR
• Deployed on AWS EC2

The prediction service supports:
• Real-time inference
• Training trigger via API route

⸻

CI/CD Pipeline

• GitHub Actions handles build and deployment
• Self-hosted EC2 runner simulates real production environments
• Docker image built, tagged, and pushed to ECR
• EC2 pulls image and runs container automatically

Secrets are securely managed using GitHub Actions secrets.

⸻

End-to-End Workflow

Data Ingestion
→ Data Validation
→ Data Transformation
→ Model Training
→ Model Evaluation
→ Model Registry (S3)
→ Docker Image Build
→ CI/CD Deployment
→ Live Inference Service



