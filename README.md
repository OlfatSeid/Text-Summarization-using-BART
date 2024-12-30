
# Text Summarization 

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



### Acknowledgments
Hugging Face for the BART model and transformers library.
PyMuPDF for PDF text extraction.
Sentence-Transformers for embedding generation.

---------------------------------------------------------------------------------------------------------------
# README: Webpage and Text Summarization Tool

This project implements a summarization tool using a fine-tuned BART model for generating summaries of text and web content. The tool provides two functionalities: summarizing web pages by fetching their content via a URL and summarizing user-provided text.

## Features

1. **Webpage Summarization**:
   - Fetches the content of a webpage using its URL.
   - Generates a concise summary using the fine-tuned BART model.

2. **Text Summarization**:
   - Accepts user-inputted text.
   - Generates a summary of the text using the fine-tuned BART model.

3. **Interactive Widgets**:
   - Utilizes `ipywidgets` for a user-friendly interface.
   - Includes buttons for summarization and clearing inputs.

## Requirements

### Python Libraries

The following Python libraries are required:
- `transformers`: For the BART model and tokenizer.
- `ipywidgets`: For interactive input and output.
- `requests`: For fetching webpage content.
- `IPython.display`: For displaying widgets.

### Installation

To install the necessary libraries, run the following command:

```bash
pip install transformers ipywidgets requests
```

## Usage

### 1. Webpage Summarization

- Enter the URL of a webpage into the provided text input.
- Click the "Fetch & Summarize" button to fetch and summarize the webpage content.
- View the generated summary in the output area.

### 2. Text Summarization

- Enter the text to be summarized into the text area.
- Click the "Summarize Text" button to generate a summary.
- Clear the text area by clicking the "Clear Text" button if needed.

## Code Overview

### Model Setup

```python
model_name = "fine_tuned_bart"
tokenizer = BartTokenizer.from_pretrained(model_name)
model = BartForConditionalGeneration.from_pretrained(model_name)
```

### Summarization Functionality

#### Webpage Fetching and Summarization

```python
def fetch_text_from_url(url):
    try:
        response = requests.get(url)
        response.raise_for_status()
        return response.text
    except requests.exceptions.RequestException as e:
        return str(e)

def summarize_text(text):
    inputs = tokenizer.encode("summarize: " + text, return_tensors="pt", max_length=1024, truncation=True)
    summary_ids = model.generate(inputs, max_length=512, num_beams=4, early_stopping=True)
    summary = tokenizer.decode(summary_ids[0], skip_special_tokens=True)
    return summary
```

#### Interactive Widgets

```python
# Widgets for URL input
url_input = Text(placeholder='Enter URL of the webpage...')
button_fetch_summarize = Button(description="Fetch & Summarize", button_style='success', icon="link")
button_clear_url = Button(description="Clear URL", button_style='danger', icon="trash")

# Widgets for Text Input
input_text_area = Textarea(placeholder='Enter text here...')
button_summarize_text = Button(description="Summarize Text", button_style='success', icon="cogs")
button_clear_text = Button(description="Clear Text", button_style='danger', icon="trash")

# Output Area
output = Output()
```

### Event Handlers

- Fetch and summarize URL:

```python
def handle_fetch_summarize(b):
    output.clear_output()
    url = url_input.value.strip()
    if url:
        text = fetch_text_from_url(url)
        if isinstance(text, str):
            with output:
                print(f"Error fetching URL: {text}")
        else:
            summary = summarize_text(text)
            with output:
                print("Summary:", summary)
    else:
        with output:
            print("Please enter a valid URL.")
```

- Summarize text:

```python
def handle_summarize_text(b):
    output.clear_output()
    text = input_text_area.value.strip()
    if text:
        summary = summarize_text(text)
        with output:
            print("Summary:", summary)
```

## Future Enhancements

1. Add support for additional languages.
2. Enable file uploads for batch text summarization.
3. Enhance error handling and user feedback.

## License
This project is open-source and available under the MIT License.


