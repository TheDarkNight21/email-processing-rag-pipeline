# Email RAG Pipeline

A simple RAG (Retrieval-Augmented Generation) pipeline for processing downloaded Outlook emails.

## Features

- **Email Parsing**: Supports `.eml` and `.msg` email formats
- **Text Extraction**: Extracts subject, sender, recipient, date, and body content
- **Text Chunking**: Splits emails into overlapping chunks for RAG processing
- **Jupyter Notebook**: Interactive notebook for Google Colab or local Jupyter
- **Standalone Script**: Python module for programmatic usage

## Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd email_rag_pipeline
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

## Usage

### Option 1: Jupyter Notebook (Google Colab)

1. Open `email_rag_pipeline.ipynb` in Google Colab
2. Upload your email files using the file upload widget
3. Run the cells to process your emails

### Option 2: Standalone Python Script

1. Place your email files in the `data/raw_emails/` directory
2. Run the email loader:

```python
from src.email_parser import load_emails_from_directory, create_email_summary

# Load emails from directory
email_data = load_emails_from_directory("data/raw_emails")

# Create summary
summary_df = create_email_summary(email_data)
print(summary_df)
```

### Option 3: Direct File Processing

```python
from src.email_parser import parse_email_file

# Parse individual email file
email_data = parse_email_file("path/to/email.eml")
print(f"Subject: {email_data['subject']}")
print(f"From: {email_data['from']}")
print(f"Body: {email_data['body'][:200]}...")
```

## File Formats Supported

- **`.eml`**: Standard email format (RFC 2822)
- **`.msg`**: Microsoft Outlook message format (requires `python-msg-parser`)

## Project Structure

```
email_rag_pipeline/
├── data/
│   ├── raw_emails/          # Place your email files here
│   └── processed/           # Processed data output
├── src/
│   └── email_parser/        # Email parsing utilities
│       ├── __init__.py
│       └── email_loader.py
├── email_rag_pipeline.ipynb # Jupyter notebook
├── requirements.txt         # Python dependencies
└── README.md               # This file
```

## Next Steps for Full RAG Pipeline

To complete the RAG pipeline, you would typically add:

1. **Vector Embeddings**: Use Sentence-BERT or similar models
2. **Vector Store**: FAISS, Pinecone, or ChromaDB
3. **Retrieval**: Similarity search functionality
4. **Generation**: LLM integration for response generation

## Example Output

```
Processing email1.eml...
  Extracted 245 words from email1.eml
  Subject: Meeting Request for Next Week...

Processing email2.msg...
  Extracted 189 words from email2.msg
  Subject: Project Update and Timeline...

Successfully processed 2 emails

Email Summary:
           subject                    from                     date
Email-1  Meeting Request for Next Week  john@example.com  Mon, 15 Jan 2024 10:30:00 +0000
Email-2  Project Update and Timeline    jane@example.com  Tue, 16 Jan 2024 14:15:00 +0000

Word Counts:
  Email-1: 245 words
  Email-2: 189 words

Creating text chunks...
  Email-1: 2 chunks
  Email-2: 1 chunks

Total chunks created: 3
```

## Dependencies

- `pandas`: Data manipulation and analysis
- `python-msg-parser`: For parsing .msg files
- `jupyter`: For notebook support
- `numpy`: Numerical operations (optional, for vector operations)

## License

MIT License
