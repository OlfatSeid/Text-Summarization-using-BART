
# Text Summarization Notebook

## Overview

This notebook provides a comprehensive solution for text summarization using the BART Large Language Model (LLM).
It includes functionality for extracting text from PDF files, generating embeddings,
performing Retrieval-Augmented Generation (RAG),
fine-tuning BART for improved performance, and displaying the output using the `ipywidgets` library.

## Features

- **Text Extraction from PDF**: Extracts text content from PDF files.
- **Embeddings**: Generates embeddings for the extracted text using a pre-trained model.
- **BART Model for Summarization**: Utilizes the BART model for generating summaries.
- **Retrieval-Augmented Generation (RAG)**: Enhances summarization by incorporating relevant retrieved documents.
- **Fine-Tuning BART**: Customizes the BART model for improved summarization performance on specific datasets.
- **Evaluating the fine-tuned model.
- **Interactive UI**: Uses the `ipywidgets` library for an interactive user interface to display the summarization results.

## Requirements

Before running the notebook, ensure you have the following dependencies installed:



## Acknowledgments
Hugging Face for the BART model and transformers library.
PyMuPDF for PDF text extraction.
Sentence-Transformers for embedding generation.
