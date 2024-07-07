# AI-Powered Research Paper Assistant: Function-wise Documentation

## Table of Contents

1. [Introduction](#1-introduction)
2. [Core Functions](#2-core-functions)
   - [2.1 model_generation](#21-model_generation)
   - [2.2 dynamic_prompt_generation](#22-dynamic_prompt_generation)
   - [2.3 search](#23-search)
   - [2.4 simpleinference](#24-simpleinference)
3. [Helper Functions](#3-helper-functions)
   - [3.1 infer_model_titles](#31-infer_model_titles)
   - [3.2 infer_model_abstract](#32-infer_model_abstract)
4. [API Endpoints](#4-api-endpoints)
5. [Configuration](#5-configuration)
6. [Error Handling](#6-error-handling)
7. [Security Considerations](#7-security-considerations)
8. [Troubleshooting](#8-troubleshooting)

## 1. Introduction

The AI-Powered Research Paper Assistant is a system designed to help with research paper tasks, specifically generating titles and optimizing abstracts. This documentation provides a detailed overview of the key functions that make up the system.

## 2. Core Functions

### 2.1 model_generation

**File**: `generationhandler.py`

**Purpose**: Orchestrates the overall process of generating titles or optimizing abstracts.

**Parameters**:
- `datadict` (dict): Contains input data and configuration for the generation process.

**Returns**: 
- dict: Contains generated titles or optimized abstract, depending on the input.

**Workflow**:
1. Calls `search` function to find similar abstracts and titles.
2. Calls `dynamic_prompt_generation` to create a prompt.
3. Calls either `infer_model_titles` or `infer_model_abstract` based on the generation type.
4. Processes and returns the generated output.

**Usage Example**:
```python
result = model_generation({
    'indata': {
        'typeofgeneration': 'titles',
        'data': {'abstract': 'Sample abstract text'},
        'confidence': 0.7
    }
})
```

### 2.2 dynamic_prompt_generation

**File**: `promptgenerator.py`

**Purpose**: Creates tailored prompts for the AI model based on input data and generation type.

**Parameters**:
- `new_dict` (dict): Contains input data and context for prompt generation.

**Returns**:
- str: A generated prompt for the AI model.

**Behavior**:
- For title generation: Creates a prompt instructing the model to generate 5 diverse titles.
- For abstract optimization: Creates a prompt instructing the model to enhance the technical detail of the abstract.

**Usage Example**:
```python
prompt = dynamic_prompt_generation({
    'indata': {'typeofgeneration': 'titles'},
    'addedcontext': {
        'ref_abstract': 'Reference abstract text',
        'ref_title': 'Reference title'
    }
})
```

### 2.3 search

**File**: `similaritysearch.py`

**Purpose**: Finds similar existing papers to provide context for generation.

**Parameters**:
- `query` (str): The input abstract to find similar papers for.
- `k` (int, optional): Number of similar papers to return. Default is 5.

**Returns**:
- tuple: Contains the most similar abstract and its title.

**Note**: The provided code for this function is commented out, suggesting that the actual implementation may have been moved or modified.

### 2.4 simpleinference

**File**: `simple_inference_endpoint.py`

**Purpose**: Handles the API request for model generation.

**Parameters**:
- `jsonpackage` (dict): Contains the request data.

**Returns**:
- dict: The result of the model generation process.

**Behavior**:
- Validates the input abstract.
- Calls `model_generation` function with the input data.
- Handles errors and returns appropriate HTTP responses.

**Usage Example**:
```python
result = simpleinference({
    "indata": {
        "typeofgeneration": "titles",
        "data": {"abstract": "Sample abstract text"},
        "confidence": 0.7
    }
})
```

## 3. Helper Functions

### 3.1 infer_model_titles

**File**: `model/model_inference.py`

**Purpose**: Generates titles using the AI model.

**Parameters**:
- `prompt` (str): The generated prompt for title creation.
- `confidence` (float): Confidence level for generation.
- `max_length` (int): Maximum length of generated titles.

**Returns**:
- list: A list of generated titles.

### 3.2 infer_model_abstract

**File**: `model/model_inference.py`

**Purpose**: Optimizes an abstract using the AI model.

**Parameters**:
- `prompt` (str): The generated prompt for abstract optimization.
- `confidence` (float): Confidence level for generation.
- `max_length` (int): Maximum length of the optimized abstract.

**Returns**:
- str: The optimized abstract.

## 4. API Endpoints

### POST /simpleinference/model_generation

**Purpose**: Endpoint for generating titles or optimizing abstracts.

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

## 5. Configuration

The system requires configuration for:
- AI model endpoints
- Embedding model and data
- FastAPI server settings

Ensure all necessary environment variables and configuration files are set up before deployment.

## 6. Error Handling

- Input validation is performed in the `simpleinference` function.
- A 400 Bad Request error is raised if the abstract is missing or invalid.
- Proper error handling should be implemented in all functions to catch and handle exceptions gracefully.

## 7. Security Considerations

- Implement input sanitization in all functions that accept user input.
- Use secure methods for storing and accessing any API keys or sensitive configuration.
- Regularly update dependencies to patch potential vulnerabilities.
- Implement rate limiting on API endpoints to prevent abuse.

## 8. Troubleshooting

- If receiving a 400 Bad Request error, ensure that a valid abstract is provided in the request.
- For issues with title generation or abstract optimization, check the logs for any errors in the `model_generation`, `dynamic_prompt_generation`, or inference functions.
- If similarity search is not working as expected, verify the implementation and data sources for the `search` function.