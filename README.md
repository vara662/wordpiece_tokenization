
# WordPiece Tokenization From Scratch

A Python-based implementation of the WordPiece subword tokenization algorithm developed from scratch. This project demonstrates how raw words are converted into subword tokens through vocabulary construction, frequency analysis, WordPiece scoring, iterative token merging, longest-match tokenization, and token-to-ID mapping.

## Project Overview

WordPiece is a subword tokenization technique used in Natural Language Processing and transformer-based language models. Instead of representing every word as a single token, it divides words into smaller meaningful units.

This project implements the core WordPiece training and tokenization process without using an existing tokenizer library.

## Features

- Reads training words from a text file
- Calculates word frequencies
- Creates initial character-level WordPiece splits
- Builds the initial vocabulary
- Calculates token frequencies
- Calculates adjacent token-pair frequencies
- Computes WordPiece scores
- Selects the highest-scoring token pair
- Performs iterative token merging
- Generates the final vocabulary
- Performs longest-match tokenization
- Handles unknown tokens using `[UNK]`
- Converts tokens into numerical token IDs

## Project Structure

```text
WordPiece_Project/
│
├── wordpiece.py
├── rawdata.txt
├── WordPiece_Tokenization.ipynb
└── README.md
````

### Files

**wordpiece.py**
Contains the complete Python implementation of the WordPiece algorithm.

**rawdata.txt**
Contains the training data used to calculate frequencies and construct the vocabulary.

**WordPiece_Tokenization.ipynb**
Jupyter Notebook version containing the implementation along with the generated outputs.

**README.md**
Project documentation and usage information.

## Training Data

The project uses the following sample training data:

```text
hug
hug
hugs
pug
pug
pugs
mug
mugs
rug
rugs
```

The program calculates the frequency of each word automatically.

Example:

```text
hug : 2
hugs : 1
pug : 2
pugs : 1
mug : 1
mugs : 1
rug : 1
rugs : 1
```

## Initial Tokenization

Each word is initially divided into individual characters.

The first character is represented normally, while subsequent characters are prefixed with `##`.

For example:

```text
hug  -> ['h', '##u', '##g']
hugs -> ['h', '##u', '##g', '##s']
pug  -> ['p', '##u', '##g']
```

The `##` prefix identifies a token as a continuation of the same word.

## WordPiece Scoring

The implementation calculates the score of each adjacent token pair using:

```text
Score = Pair Frequency /
        (First Token Frequency × Second Token Frequency)
```

The pair with the highest score is selected for merging.

This process is repeated for a predefined number of merge operations.

## Training Process

The current implementation performs six merge operations.

Example merge sequence:

```text
Merge 1
Best Pair : ('h', '##u')
New Token : hu

Merge 2
Best Pair : ('p', '##u')
New Token : pu

Merge 3
Best Pair : ('m', '##u')
New Token : mu

Merge 4
Best Pair : ('r', '##u')
New Token : ru

Merge 5
Best Pair : ('hu', '##g')
New Token : hug

Merge 6
Best Pair : ('pu', '##g')
New Token : pug
```

## Final Word Splits

After the training process, the words are represented using the learned vocabulary:

```text
hug  -> ['hug']
hugs -> ['hug', '##s']
pug  -> ['pug']
pugs -> ['pug', '##s']
mug  -> ['mu', '##g']
mugs -> ['mu', '##g', '##s']
rug  -> ['ru', '##g']
rugs -> ['ru', '##g', '##s']
```

## Longest-Match Tokenization

The trained vocabulary is used to tokenize a new word using the longest-match strategy.

For the test word:

```text
mugs
```

the resulting tokens are:

```text
['mu', '##g', '##s']
```

The tokenizer searches for the longest available vocabulary token at each position before moving to the next part of the word.

## Unknown Token

The vocabulary includes a special token:

```text
[UNK]
```

If a word cannot be represented using the available vocabulary, the tokenizer returns:

```text
['[UNK]']
```

This provides a fallback mechanism for unknown or unsupported words.

## Token ID Mapping

Each vocabulary token is assigned a numerical ID.

Example:

```text
##g : 0
##s : 1
##u : 2
[UNK] : 3
h : 4
hu : 5
hug : 6
m : 7
mu : 8
p : 9
pu : 10
pug : 11
r : 12
ru : 13
```

For the test word `mugs`:

```text
Tokens:
['mu', '##g', '##s']

Token IDs:
[8, 0, 1]
```

## Execution

### Using Python

Make sure `wordpiece.py` and `rawdata.txt` are in the same directory.

Run:

```bash
python wordpiece.py
```

### Using Jupyter Notebook

Open:

```text
WordPiece_Tokenization.ipynb
```

Run each cell using:

```text
Shift + Enter
```

The Jupyter Notebook preserves both the source code and its generated output, making it useful for demonstrating the complete implementation.

## Requirements

* Python 3.x
* Jupyter Notebook or JupyterLab for notebook execution
* No external Python packages are required

The implementation uses Python's built-in `collections.Counter` module.

## Processing Pipeline

```text
Raw Training Data
        |
        v
Word Frequency Calculation
        |
        v
Initial Character Splitting
        |
        v
Initial Vocabulary
        |
        v
Token Frequency
        |
        v
Pair Frequency
        |
        v
WordPiece Score Calculation
        |
        v
Best Pair Selection
        |
        v
Token Pair Merging
        |
        v
Final Vocabulary
        |
        v
Longest-Match Tokenization
        |
        v
Token ID Generation
```

## Sample Output

```text
========== TEST TOKENIZATION ==========

Test Word : mugs
Tokens : ['mu', '##g', '##s']

========== TOKEN ID MAPPING ==========

##g : 0
##s : 1
##u : 2
[UNK] : 3
h : 4
hu : 5
hug : 6
m : 7
mu : 8
p : 9
pu : 10
pug : 11
r : 12
ru : 13

Input Tokens : ['mu', '##g', '##s']
Token IDs : [8, 0, 1]

========== PROGRAM COMPLETED ==========
```

## Technologies

* Python
* Natural Language Processing
* WordPiece Tokenization
* Subword Tokenization
* Jupyter Notebook

## Learning Outcomes

This project provides practical understanding of:

* Subword tokenization
* Vocabulary construction
* Token frequency calculation
* Pair frequency calculation
* WordPiece scoring
* Iterative vocabulary learning
* Longest-match tokenization
* Unknown token handling
* Token-to-ID conversion

## Future Enhancements

Possible improvements include:

* Support for complete sentences
* Punctuation and special-token handling
* Configurable vocabulary size
* Larger training datasets
* Vocabulary saving and loading
* Visualization of token merge operations
* Comparison with BPE and Unigram tokenization
* Integration with downstream NLP models

## Conclusion

This project demonstrates the internal working of WordPiece tokenization through a complete Python implementation. By implementing vocabulary creation, scoring, merging, tokenization, and token ID generation manually, it provides a practical foundation for understanding subword tokenization techniques used in modern Natural Language Processing systems.

## Author

**Varalakshmi K**

This project was developed to study and demonstrate the implementation of the WordPiece subword tokenization algorithm from scratch using Python.
