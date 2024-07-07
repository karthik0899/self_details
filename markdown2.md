# AI-Powered Research Paper Assistant: Technical Documentation

## Table of Contents

1. [System Overview](#1-system-overview)
2. [Architecture](#2-architecture)
3. [Components](#3-components)
   - [3.1 Generation Handler](#31-generation-handler)
   - [3.2 Prompt Generator](#32-prompt-generator)
   - [3.3 Similarity Search](#33-similarity-search)
   - [3.4 Simple Inference Endpoint](#34-simple-inference-endpoint)
4. [API Documentation](#4-api-documentation)
5. [Configuration](#5-configuration)
6. [Workflows](#6-workflows)
7. [Security Considerations](#7-security-considerations)
8. [Troubleshooting and FAQs](#8-troubleshooting-and-faqs)
9. [Maintenance and Contribution](#9-maintenance-and-contribution)

## 1. System Overview

This system is an AI-powered assistant designed to help with research paper tasks, specifically generating titles and optimizing abstracts. It uses natural language processing and machine learning techniques to provide intelligent suggestions based on input data and similar existing papers.

## 2. Architecture

The system follows a modular architecture with several key components:

- [Generation Handler](#31-generation-handler): Orchestrates the overall process of generating titles or optimizing abstracts.
- [Prompt Generator](#32-prompt-generator): Creates dynamic prompts for the AI model based on input data.
- [Similarity Search](#33-similarity-search): Finds similar existing papers to provide context for generation.
- [Simple Inference Endpoint](#34-simple-inference-endpoint): Provides an API endpoint for interacting with the system.

The system uses FastAPI for the web framework and relies on external AI models for text generation and similarity search.

## 3. Components

### 3.1 Generation Handler

**File**: `generationhandler.py`

**Purpose**: Coordinates the process of generating titles or optimizing abstracts.

**Key Functions**:
- `model_generation(datadict)`: Main function that orchestrates the generation process.

**Workflow**:
1. Performs similarity search to find reference materials.
2. Generates a dynamic prompt using the input and reference materials.
3. Calls the appropriate inference function based on the generation type (titles or abstract).
4. Processes and returns the generated output.

### 3.2 Prompt Generator

**File**: `promptgenerator.py`

**Purpose**: Creates tailored prompts for the AI model based on input data and generation type.

**Key Functions**:
- `dynamic_prompt_generation(new_dict)`: Generates a prompt for either title generation or abstract optimization.

**Features**:
- Uses reference materials to guide the generation process.
- Provides detailed instructions to the AI model for each task type.

### 3.3 Similarity Search

**File**: `similaritysearch.py`

**Purpose**: Finds similar existing papers to provide context for generation.

**Note**: The provided code is commented out, suggesting that the actual implementation may have been moved or modified. The documentation here describes the intended functionality based on the commented code.

**Intended Functionality**:
- Uses sentence transformers and FAISS for efficient similarity search.
- Loads pre-computed embeddings for a dataset of research papers.
- Performs fast similarity search to find the most relevant existing papers.

### 3.4 Simple Inference Endpoint

**File**: `simple_inference_endpoint.py`

**Purpose**: Provides an API endpoint for interacting with the system.

**Key Endpoints**:
- POST `/simpleinference/model_generation`: Accepts input data and triggers the generation process.

**Features**:
- Input validation to ensure the presence of a valid abstract.
- Error handling for missing or invalid input.

## 4. API Documentation

### POST /simpleinference/model_generation

Generates titles or optimizes abstracts based on input data.

**Request Body**:
```json
{
  "indata": {
    "typeofgeneration": "titles" | "abstract",
    "data": {
      "abstract": "string"
    },
    "confidence": number
  }
}
```

**Response**:
- For title generation: Returns a list of generated titles.
- For abstract optimization: Returns an optimized abstract.

**Error Responses**:
- 400 Bad Request: If the abstract is missing or invalid.

## 5. Configuration

The system requires configuration for:
- AI model endpoints (not visible in the provided code)
- Embedding model and data (referenced in commented code)
- FastAPI server settings

Ensure all necessary environment variables and configuration files are set up before deployment.

## 6. Workflows

1. **Title Generation**:
   - System receives input abstract
   - Performs [similarity search](#33-similarity-search) for context
   - Generates a prompt for title creation using the [Prompt Generator](#32-prompt-generator)
   - Uses AI model to generate titles
   - Returns list of generated titles

2. **Abstract Optimization**:
   - System receives input abstract
   - Performs [similarity search](#33-similarity-search) for context
   - Generates a prompt for abstract optimization using the [Prompt Generator](#32-prompt-generator)
   - Uses AI model to optimize the abstract
   - Returns the optimized abstract

## 7. Security Considerations

- Ensure proper input validation to prevent injection attacks.
- Implement rate limiting on [API endpoints](#4-api-documentation) to prevent abuse.
- Use secure methods for storing and accessing any API keys or sensitive configuration.
- Regularly update dependencies to patch potential vulnerabilities.

## 8. Troubleshooting and FAQs

**Q: Why am I getting a "400 Bad Request" error?**

A: Ensure that you're providing a valid abstract in your request. The abstract should not be empty and should contain alphabetic characters. See the [API Documentation](#4-api-documentation) for proper request format.

**Q: How can I adjust the number of titles generated?**

A: The current implementation generates a fixed number of titles. To modify this, you would need to adjust the prompt in the `dynamic_prompt_generation` function in the [Prompt Generator](#32-prompt-generator).

## 9. Maintenance and Contribution

To contribute to this project:
1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request with a clear description of your modifications

For bug reports or feature requests, please use the project's issue tracker.