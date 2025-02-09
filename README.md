# Language Model Vocabulary Optimization Pipeline

This repository provides a complete pipeline to optimize a language model by truncating its vocabulary based on corpus statistics. The pipeline analyzes multi-language datasets (English and Azerbaijani), filters out rarely used tokens to create a leaner SentencePiece model, updates the tokenizer accordingly, and maintains model performance while significantly reducing size.

## Features

- **Corpus Analysis:** Computes token frequency statistics from English and Azerbaijani text corpora
- **Vocabulary Truncation:** Filters out infrequent tokens based on predefined thresholds, reducing the overall vocabulary size
- **Tokenizer Update:** Modifies the SentencePiece model to reflect the truncated vocabulary and updates the tokenizer
- **Model Optimization:** Creates a smaller version of the model while preserving performance

## Installation

### Prerequisites

First, update your system and install required packages:

```bash
# Update package list
sudo apt-get update

# Install required system utilities
sudo apt-get install zip unzip
```

### Protocol Buffers Installation

Download and install Protocol Buffers compiler:

```bash
# Download protoc
wget https://github.com/protocolbuffers/protobuf/releases/download/v3.20.3/protoc-3.20.3-linux-x86_64.zip

# Unzip to a separate directory
unzip protoc-3.20.3-linux-x86_64.zip -d protoc3

# Move binary to system path
sudo mv protoc3/bin/protoc /usr/local/bin/

# Move includes to system include directory
sudo mv protoc3/include/* /usr/local/include/
```

### Python Dependencies

Install required Python packages:

```bash
pip install sentence_transformers pandas transformers protobuf torch tqdm
pip install --upgrade sentencepiece
```

## Usage

1. **Prepare Your Data**
   - Place your corpus files in the project directory:
     - `corpus.en` - English corpus
     - `corpus.az` - Azerbaijani corpus
   - Each file should contain one sentence per line, tab-separated

2. **Configure Model Settings**
   - Set the base model (default is 'BAAI/bge-m3')
   - Adjust token frequency thresholds in the code:
     - English: tokens appearing ≥10 times
     - Azerbaijani: tokens appearing ≥3 times
   - Special tokens and tokens with ID ≤100 are always preserved

3. **Run the Pipeline**
   - Execute the main script to:
     - Analyze your corpora
     - Create a truncated vocabulary
     - Update the model and tokenizer
     - Save the optimized model locally

## Results

The pipeline achieves impressive optimization results while maintaining performance:

### Size Reduction
- Vocabulary size reduced from 250,000 to 37,367 tokens (~85% reduction)
- Embedding layer size reduced by 82.35% (0.1765 ratio)
- Overall model size reduced by 38.35% (0.6165 ratio)

### Performance
- Semantic similarity scores remain identical between the original and optimized models
- Example comparison (English-Azerbaijani parallel sentences):
  ```python
  # Both models produce identical similarity score
  Original model similarity: 0.75040686
  Optimized model similarity: 0.75040686
  ```

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
