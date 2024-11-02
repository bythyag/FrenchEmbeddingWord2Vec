# French Word2Vec Embeddings

A Python implementation for training Word2Vec embeddings on French Wikipedia articles using Gensim.

## Requirements

```bash
pip install datasets
pip install gensim
pip install pandas
pip install numpy
pip install scikit-learn
pip install tqdm
```

## Implementation Details

The model is trained with the following specifications:
- Vector size: 512 dimensions
- Training algorithm: Skip-gram (sg=1)
- Number of epochs: 3
- Number of worker threads: 4
- Dataset: French Wikipedia articles (20220301.fr)[1]

## Key Features

- Text preprocessing with regex to clean special characters
- Word vectors for 125,716 unique French words[1]
- Training performed on 10,000 Wikipedia articles with 80-20 train-test split[1]
- Supports similarity queries and vector representations for words

## Example Usage

```python
# Load and preprocess data
dataset = load_dataset("wikipedia", "20220301.fr", split='train[:10000]')

# Train model
model = Word2Vec(sentences=train_sentences, 
                sg=1, 
                vector_size=512, 
                epochs=3, 
                workers=4)

# Find similar words
model.wv.most_similar('scientifique')

# Get word vector
vector = model.wv.get_vector('scientifique')
```

## Model Output

The model can find semantically similar words. For example, words similar to "scientifique" include:
- vulgarisation
- multidisciplinaire
- interdisciplinaire
- expérimentale
- mathématique[1]

## Export Format

The trained embeddings are saved in a text format:
```python
model.wv.save_word2vec_format('frenchEmbedding.txt')
```

Citations:
[1] https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/13462189/e1270fc6-43d2-46a0-8dc3-522e03d3bc82/paste.txt
