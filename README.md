# Semantic Search for Clinical Study Data Using BioBERT and Qdrant

This project aims to create a semantic search engine for clinical study data using **BioBERT**, **spaCy**, and **Qdrant**. The system preprocesses clinical study data, vectorizes text descriptions, and uploads them to a Qdrant database for efficient similarity-based searching. The dataset used for this example is publicly available on the EMA Catalogue.

**⚠️ Note:** This project is **not yet fully tested** and may not work as intended. If you plan to fork or use it, expect potential issues, and further testing will be required.

---

## Features
- **Text Preprocessing**: Cleans and processes text using `spaCy` (e.g., lemmatization, stopword removal).
- **Vectorization**: Converts study titles, descriptions, and countries into dense vectors using BioBERT.
- **Vector Storage**: Leverages Qdrant for storing and querying vectorized data.
- **Semantic Search**: Enables searching for relevant clinical studies based on a natural language query, ranked by cosine similarity.

---

## Installation

### Prerequisites
- Python 3.7 or above
- Qdrant API access (with a valid URL and API key)
- Google Colab or a local Python environment for execution

### Install Required Libraries
```bash
pip install qdrant-client transformers spacy torch datasets torchvision torchaudio
pip install https://huggingface.co/spacy/en_core_web_sm/resolve/main/en_core_web_sm-any-py3-none-any.whl
```

---

## Data Processing Pipeline

### 1. **Preprocessing Text**
- Text fields from the clinical study dataset (e.g., titles, descriptions) are cleaned and processed:
  - Convert to lowercase and remove punctuation.
  - Lemmatize words and remove stopwords using spaCy.
  - Preserve named entities (e.g., locations, diseases) to retain critical context.

### 2. **Vectorizing Text**
- Uses BioBERT to tokenize and encode the text fields into dense vector representations.
- Mean pooling of the last hidden states is applied to produce a single vector per text input.

### 3. **Uploading Vectors to Qdrant**
- Vectorized data is formatted and uploaded to a Qdrant collection.
- Each data point includes a unique ID, vector, and payload (title, description, and study countries).

### 4. **Semantic Search**
- Queries are vectorized using BioBERT.
- Qdrant performs similarity-based searches using cosine distance to retrieve relevant results.

---

## How to Run

1. **Clone the Repository**
   ```bash
   git clone https://github.com/yourusername/semantic-search-clinical-studies.git
   cd semantic-search-clinical-studies
   ```

2. **Prepare Your Dataset**
   - Place your clinical study data CSV file in the working directory.
   - Update the `dataset_url` variable with the file path in the script.

3. **Setup Qdrant**
   - Replace placeholders for `url` and `api_key` in the Qdrant client initialization with your credentials.
   - Ensure the Qdrant server is running and accessible.

4. **Run the Script**
   Execute the script to preprocess data, vectorize text, and upload it to the Qdrant database.

5. **Test Semantic Search**
   Use the query functionality to test the search system.

---

## File Descriptions

- `semantic_search.py`: Main script with logic for preprocessing, vectorization, and Qdrant interaction.
- `vectorized_data.json`: Contains vectorized study data (generated during execution).
- `requirements.txt`: List of required Python packages for the project.

---

## Example Usage

### Sample Search Query
```python
test_query = "Cancer related studies"
display_search_results(test_query, tokenizer, model, cutoff_score=0.90)
```

### Expected Output
```plaintext
Title: "Study of New Cancer Treatments"
Study Description: "Exploring innovative therapies for metastatic cancer patients."
Study Countries: "United States"
Score: 0.95
-----------
```

---

## Known Issues and Limitations
1. **Unverified Functionality**: This project is still under development and has not been fully tested.
2. **Potential Errors**: Bugs may occur during vectorization, Qdrant integration, or search queries.
3. **Model Assumptions**: The BioBERT model and vector size assumptions might not suit all datasets.

---

## Dependencies

- [Qdrant](https://qdrant.tech)
- [Hugging Face Transformers](https://huggingface.co/transformers/)
- [spaCy](https://spacy.io/)
- [BioBERT](https://github.com/dmis-lab/biobert)

---

## Contributing

Contributions are welcome, but please note this project is in its early stages. Forks may require debugging and testing to ensure proper functionality. Open issues for suggestions or problems encountered.

---

## License

This project is licensed under the MIT License. See the LICENSE file for details.
