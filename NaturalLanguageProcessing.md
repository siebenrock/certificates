# Introduction

### Context is Everything

"I was lured to see this on the promise of a smart, witty slice of old fashioned fun and intrigue - I was conned"

- Starts with positive words, but strongly negative review

"The sofa didn't fit through the door because it was too wide" and "The sofa didn't fit through the door because it was too wide"

- What does "it" refer to in each case?

### High-level NLP Pipeline

- Text processing: *raw input text, clean, normalize, convert*
- Feature extraction: *extract features representations for model*
- Modeling

## Text Processing

- `pattern = re.compile(r'<.*?>')`
  - Remove HTML tags using RegEx, fails on included JavaScript
- `soup = BeautifulSoup(r.text, "html5lib")`
  - `summaries = soup.find_all("tr", class_="athing")`
  - Better: remove HTML tags using Beautiful Soup library and find articles

### Normalize

- `text = re.sub(r"[^a-zA-Z0-9]", " ", text) `
  - Remove punctuation
- `re.sub(r"[^a-zA-Z0-9]", " ", text.lower())`

### Tokenize

*NLTK: Natural language ToolKit*

- `words = text.split()`
  - Split text into tokens (words)
- `from nltk.tokenize import word_tokenize, sent_tokenize`

- `words = word_tokenize(text)`
  - Split text into words
- `sentences = sent_tokenize(text)`
  - Split text into sentences

### Remove Stop Words

- `from nltk.corpus import stopwords`
- `stopwords.words("english")`
  - Returns list of stop words
- `words = [w for w in words if w not in stopwords.words("english")]`

### Stemming

- `from nltk.stem.porter import PorterStemmer`
- `stemmed = [PorterStemmer().stem(w) for w in words]`
  - Reduce words to their stems
  - "branches", "branching", "branched" to "branch"

### Lemmatization

- `from nltk.stem.wordnet import WordNetLemmatizer`
- `lemmed = [WordNetLemmatizer().lemmatize(w) for w in words]`
  - Reduce words to their root form by using dictionary
  - "is", "was", "were" to "be"
- `lemmed = [WordNetLemmatizer().lemmatize(w, pos='v') for w in lemmed]`
  - Lemmatize verbs by specifying pos

### Part-of-Speech Tagging

Example: sentence parsing

```python
# Define a custom grammar
my_grammar = nltk.CFG.fromstring("""
S -> NP VP
PP -> P NP
NP -> Det N | Det N PP | 'I'
VP -> V NP | VP PP
Det -> 'an' | 'my'
N -> 'elephant' | 'pajamas'
V -> 'shot'
P -> 'in'
""")
parser = nltk.ChartParser(my_grammar)

# Parse a sentence
sentence = word_tokenize("I shot an elephant in my pajamas")
for tree in parser.parse(sentence):
    print(tree)
```

```
(S
  (NP I)
  (VP
    (VP (V shot) (NP (Det an) (N elephant)))
    (PP (P in) (NP (Det my) (N pajamas)))))
(S
  (NP I)
  (VP
    (V shot)
    (NP (Det an) (N elephant) (PP (P in) (NP (Det my) (N pajamas))))))
```

Example: named entity recognition

```python
from nltk import pos_tag, ne_chung
from nltk.tokenize import work_tokenize

# Recognize named entities in a tagged sentence
ne_chunk(pos_tag(word_tokenize("Antonio joined Udacity Inc. in California.")))
```

## Spam Classifier with Naivee Bayes

- Easy to implement and fast to train
- **Bayes' theorem** describes the probability of an event, based on prior knowledge of conditions that might be related to the event; calculates the probability of a certain event happening based on the joint probabilistic distributions of certain other events
- *Naive* in Naive Bayes means that algorithm considers features that it is using to make predictions to be independent of each other, which may not always be the case

### Using Scikit-learn

```python
from sklearn.naive_bayes import MultinomialNB

naive_bayes = MultinomialNB()
naive_bayes.fit(training_data, y_train)
predictions = naive_bayes.predict(testing_data)

from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score
print('Accuracy score: ', format(accuracy_score(y_test, predictions)))
print('Precision score: ', format(precision_score(y_test, predictions)))
print('Recall score: ', format(recall_score(y_test, predictions)))
print('F1 score: ', format(f1_score(y_test, predictions)))
```

## Part of Speech Tagging with HMMs

- Simple implementation with lookup table
- Improve by using bigrams or n-grams when single word can have two different tags
  - Example: "Mary will see Will", how to tag Will?
- Problem: some pair of words do not appear

### Hidden Markov Models

- *Transition probabilities*: How likely is the order of tags?
  - Example: How likely is it that noun - modal - verb - noun
- *Emission probabilities*: How likely is it that the actual word is the tag?
  - If a verb is a noun, what is the probability that the word then is "Jane"?
- Drop edges and connections with probability of zero 
- Find path of highest probability, meaning, of highest products of transition and emission probabilities
- **Viterbi algorithm**: from start to finish, for every state record highest probability path that ends in that state; winning path with highest probability can be found by tracing backwards from the end

## Ressource

- [Pandas: Working with Text data](https://pandas.pydata.org/pandas-docs/stable/text.html)
- [Regular Expressions in Python](https://docs.python.org/3/library/re.html)
- [Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)
- [NLTK Tokenize](http://www.nltk.org/api/nltk.tokenize.html)
- [Speech and Language Processing by Daniel Jurafsky and James H. Martin](https://web.stanford.edu/~jurafsky/slp3/)
- More NLP open source libraries: [NLTK](http://www.nltk.org/), [spaCy](https://spacy.io/), [Gensim](https://radimrehurek.com/gensim/)

# Computing with Natural Language

## Feature Extraction and Embeddings

### Bag of Words

- Treats document as unordered collection of words
- Store as vector of numbers, representing how many times each word occurs in document
- Words in columns; documents in rows; term frequency in cells
- Set of document is *corpus*
- Document similarity is reflected by dot product, but only captures overlap and no other factors that documents do have in common
  - Cosine similarity is better measure; equal to cosine of angle of arrows (vectors) in n-dimensional space between them

### TF-IDF

- Not all words are equally important, compensate by using document frequency to reflect in how many documents each word occurs
  - Divide term frequency in cells by document frequency of that term
  - Values no reflect how unique words are to the document; better for characterising
- TF-IDF is way to assigning weights to words that signify their relevance in documents
- `tdidf(t, d, D) = tf(t, d) * idf(t, D)`
  - `tf(t, d) = count(t, d) / |d|`
    - Raw count of term in document divided by total number of terms in document
  - `log(|D| / |{d∈D : t∈d}|)`
    - Logarithm of total number of documents in collection divided by number of documents where term is present
  - Term frequency multiplied by inverse document frequency

### One-Hot Encoding

- Inferences that can be made are currently on document level; allows to evaluate topics in document, document similarity, and sentiment
- Need numerical representation of each word for deeper analysis
- Assign word to vector that has 1 in pre-determined position for that word and 0 elsewhere; like bag of words but treating each words as individual bag

### Word Embeddings

- One-hot encoding breaks for large vocabulary
- Need to control size of word representation, limit it to fixed size vector
- Find embedding for each word in vector space; should have properties like:
  - Words with similar meaning should be close to each other (kid, child)
  - Words with similar difference in their meanings, they should be equally separated in embedded space (man and woman, king and queen)
- Use word the representation for purposes such as finding synonyms, analogies, classifying, alternative way of representing document, etc.

#### Word2Vec

- Most common example of word embedding
- Transforms word to vectors
- Idea to have a model that can predict word given neighbouring words (continuous bag of words) can or can predict neighbouring words for given word (continuous skip-gram); this model is likely to capture contextual meaning of word
- *Skip-gram model*: convert word from sentence to one-hot encoded vector and feed to neural network to predict surrounding and context words
  - Take one hidden layer from neural network, outputs of that layer become corresponding word vector
- Meaning of word is distributed throughout the vector
- Vector size is independent of vocabulary
  - Size is constant and independant on number of words trained on unlike bag of words
- Pre-trained word vectors can be stored and reused
- Use RNNs to learn better word embedding

#### GloVe

- *Global Vectors* for word representation
- Other type of word embedding
- Tries to optimize word representation using co-occurrence statistics
- Compute `P(j|i)`
  - Probability that word j appears in context (meaning in vicinity) of word i
  - For all word pairs in given corpus
- Then normalise to get probability
- Initialize two vectors for each word
  - One vector when words acts as context
  - One vector when words acts as target
- For any pair of words, dot product of vectors should equal co-occurrence probability
  - Iteratively optimize word vectors
  - Result is set of vectors that capture similarities and differences between individual words

#### Embeddings for Deep Learning

- For embeddings of large collection of sentences, words with common context words tend to get pulled closer together

- Example: coffee and tea are close along many dimensions in embedding
  - "Would you like a *cup* of _?"
  - "I like my _ *black*."
  - "I need my *morning* _ before I can do anything." 
- Add more dimensions to embedding to capture more similarities and differences
- Better representation of words for more dimensions
- Common to use word embedding layer with few hundret dimensions; significantly smaller than using one-hot encoding (size of vocabulary)
- Use pre-trained embedding as a lookup

#### t-SNE

- *t-Distributed Stochastic Neighbor Embedding*

- Word embeddings have high dimensionality, hence, hard to visualize
- Dimensionality reduction technique that can map high dimensional vectors to a lower dimensional space, tries to maintain relative distance between objects
- Great tool to visualize word embeddings, preserves relationships
- Helps to understand representation that network learns und to identify issues

## Topic Modeling

###  Latent Variables

- Latent variables are set of topics that drive generation of words in each document
-  Topic is mixure of terms that is likeley to generate
  - Examples: science, politics, sports
  - But algorithm will just generate some topics
- `P(z|d)`
  - Probability of topic z given document d
- `P(t|z)`
  - Probability of term t given topic z

- Probability of a document given a term expressed as sum over `P(z|d)` and `P(t|z)`

### Latent Dirichlet Allocation (LDA)

- Helps to reduce number of parameters as compared to bag of words model by introducing a aggregation to topics within bag of words which allocates documents and words directly

- Find two matrices (documents to topics and topics to words) whose product is very close to respective bag of words matrix

- **Dirichlet Distributions**: multinominal distribution is generalization of binomial distribution to more than two values
  - Generalization of formula for beta distribution
  - High values lead to a high density function in the middle; smaller values push towards edges

#### Generate Fake Documents with LDA

- Idea to generate fake documents from topic model, then compare generated documents to real documents; compute error and measure extend to which fake documents are getting closer to real documents; improve topic model

- Sample topic
  - Pick random point from Dirichlet distribution of topics and obtain values for each topic which represent mixture of topics for new document (repeat for all documents)
- Sample word
  - Pick random point, based on choosen topic, from different Dirichlet distribution of words from high dimensional simplex; point generates multinominal distribution including all possible words; sample random words from this distribution; likelyhood from distribution of words which in turn depends on previously selected topic point (repeat for all topics)
- Combining the models
  - Two matrices: documents to topics and topics to words; idea is to find best location of points in both distributions to get best factorization of matrix; generate points to create fake articles; compare with original documents; calculate error and backpropage; use maximum likelihood to figure out arrangements of points which will return the real articles with highest probability

## Sentiment Analysis

- Popular use of NLP: understand customer sentiment, getting feedback signal for social media and advertising, etc.

### Sentiment Analysis with Regular Classifier

- Classification (good/bad) or regression problem (0-5 stars)
- Process each review as document, extract set of features that represent it
  - Bag of words, TF-IDF, or sequence of word vectors
- Select classifier: decision tree, SVM , etc.
- Select loss function: categorical cross entropy, mean-squared error, etc. 

### Sentiment Analysis with RNN

- Problem: "I expected this movie to be much better" (negative review), "This movie was much better than I expected" (positive review)
  - With one-hot encoding or bag-of-words model, vectors and output would be very similar
  - Fix by considering the order of words with RNNs and LSTMs: take previous output as input joined with new words to produce new output; final output is encoding of sentence

## Sequence to Sequence

- Particular RNN architecture: feed in sequence of data and network will output another sequence
- Used for example in machine translation
- Sequential options: one-to-one, one-to-many, many-to-one, many-to-many
  - Many-to-many used for sequence to sequence

### Applications

- English phrase to French phrase
- News articles to summaries
- Train on dialogs for chatbot

### Architecture

- Both, sequential inputs and output by using two RNNs
- Two RNNs
  - Encoder reads input sequence
  - Hands understanding (fixed-size tenser, state, context) to decoder
  - Decoder generates output sequence and returns which elements is most likely generated
- Encoder and decoder have loops to process inputs

## Deep Learning Attention

- Recent innovation
- Attempt to mimic human perception: "Humans focus attention selectively on parts of the visual space to acquire information when and where it is needed, and combine infromation from different fixations over time to build up an internal representation of the scene, guiding future eye movements and decision making" (Recurrent Models of Visual Attention, 2014)
- Attention methods provide mechanism for adding selective focus into a machine learning model (with sequential processing)
- State of the art in neurall machine translation
- In sequence to sequence models, last hidden state become context vector for decoder; limitation: context is single vector no matter how long or short the initial input sequence is
  - One could use large number of hidden units to obtain large context vector in any case, but this would lead to overfit model with short sequences and performance hit

### Attention Overview

#### Encoder

- RNN and need to declare number of hidden units in RNN cell
- Pass input sequence through embedding process which translates each word into vector
- Feed in words step-by-step, at each time step, creates a hidden state for each word

- Instead of passing just the final state as context to the decoder, the encoder passes all of the hidden states; thereby flexibility in context size and longer sequences better capture the information from input sequence

#### Decoder

- Does not only receive the last context vector in addition to end token, instead all hidden states from encoder
- Uses **scoring function** to score each hidden state; feed scores into softmax function; multiply each vector by its softmax score and summing up produces attention context vector; attention context vector merges with decoder's hidden state to create real output at time step
- Decoder looks at input word, attention context vector, which focuses attention on place in input sequence; produces hidden state and first output word
  - Then takes previous output as input and generates new context vector and hidden state from previous; produces new hidden state and new output word
  - Continues until completion of output sequence

- Pays attention to part of input sequence via the context factor at every time step
  - Does not loop sequentially, instead learns in training phase
  - For translation task, model does not follow the exact order of words as in the input language

### Types of Attention

#### Multiplicative Attention

- *Luong Attention* proposed in [Effective Approaches to Attention-based Neural Machine Translation](https://arxiv.org/abs/1508.04025)

- **Scoring function**, to produce attention weights, takes in hidden state of decoder and set of hidden state of encoder at each time step
- Uses hidden state of current time step at decoder
- Simple method to calculate dot product of hidden state vector of decoder with each hidden state vector of encoder; dot product is higher for vectors with smaller angle between them (similarity measure)
  - Drawback: assuming encoder and decoder have same embedding space
- Introduce weight matrix between multiplication of decoder hidden states and encoder hidden states; allows for difference embedding size

- Concatenate context attention vector with hidden state of decoder at this time step; pass group through fully connected neural network; output would be output word in sequence
  - Continue with second step and passing the hidden state and output from frist time step; produce hidden state; compute scroe and attention context vector; group together and pass through neural net

#### Additive Attention

- *Bahdanau Attention* proposed in [Neural Machine Translation by Jointly Learning to Align and Translate](https://arxiv.org/abs/1409.0473)

- **Scoring function** concatenates vectors into one vector and inputs them into feed-forward neural network which outputs single score
- Uses hidden state of previous time step at decoder

#### Other Attention Method

- *The Transformer*, only use attention and no RNNs (feed-forward neural networks instead)
- Proved superior and requires less time to train since processes can be parallel ized without RNNs
- Does not take inputs step-by-step, instead, takes all of them in parallel; produces output one-by-one
- Concept of self attention
- [Attention Is All You Need](https://arxiv.org/abs/1706.03762), [Video](https://www.youtube.com/watch?v=rBCqOTEfxvg)

### Applications in Computer Vision

- [Show, Attend and Tell: Neural Image Caption Generation with Visual Attention](https://arxiv.org/pdf/1502.03044.pdf)
- [Bottom-Up and Top-Down Attention for Image Captioning and Visual Question Answering](https://arxiv.org/pdf/1707.07998.pdf)
- [Video Paragraph Captioning Using Hierarchical Recurrent Neural Networks](https://www.cv-foundation.org/openaccess/content_cvpr_2016/app/S19-04.pdf)
- [Every Moment Counts: Dense Detailed Labeling of Actions in Complex Videos](https://arxiv.org/pdf/1507.05738.pdf)
- [Tips and Tricks for Visual Question Answering: Learnings from the 2017 Challenge](https://arxiv.org/pdf/1708.02711.pdf)
- [Visual Question Answering: A Survey of Methods and Datasets](https://arxiv.org/pdf/1607.05910.pdf)

## RNN Keras

- Example of machine translation

### Input Representation

- Instead of single word vector or document vector, need to represent each sentence as sequence of word vectors
  - Therefore, convert each word into one-hot encoded vector; stack vectors as matrix
- Pad shorter sequences with special token to make all vectors the same length

### Basic RNN Architecture

- *Embedding layer*: helps to enhance word representation; produces more compact word vector for later layers
- *Recurrent layer(s)*: incorporates information from across the sequence; each output word affected by potentially any previous input word
  - Input word vector is multiplied by weight matrix
    - Add bias values to produce our first intermediate result
  - Meanwhile, state vector from previous time step is multiplied with another weight matrix to produce second intermediate result
  - Both intermediate results are added together and passed through an activation function such as ReLU, sigmoid, or tanh to produce the state for the current time step
  - This state vector is passed on as input to next fully-connected layer, that applies another weight matrix, bias, and activation to produce the new output
- *Dense layers*: output of last recurrent layer fed into one or more fully-connected dense layers that produce softmax output; can be interpreted as one-hot encoded words

#### Unrolling an RNN

- At any time step, the recurrent layer receives an input as well as the state vector from the previous step; continues until entire input is exhausted
- Drawback of simple model is that output is generated for each input word immediately; only works well when source and target language have one-to-one mapping between words

### Encoder-Decoder Architecture

- Ideally let the network learn internal represenation of entire input sentence, afterwads start generating output translation; therefor, two networks are needed
- *Encoder*: accepts source sentence, one word at a time, and capture overall meaning in single vector
- *Decoder*: interprets final vector and expands it into correspoing sentence in target language, one word at a time
  - Receives final sentence vector from encoder and given sentinel input to start; recurrent portion produces a state vector; with that, the fully-connected portion produces output word
  - At each subsequent time step, decoder uses previous state as well as own previous output to produce current output
  - Continues for fixed number of iterations; network will start producing special padding symbols at end; alternatively, train network to output stop symbol to indicate completion

#### Performance Variations

- Different kind of RNNs like LSTMs, GRUs, etc. instead of vanilla RNN units to better analyze the input sequence at cost of additional model complexity
- Improve number of recurrent layers to use; each layer incorporates information from input producing compacct state vector at each time step; additional layers can incorporate information across these state vectors
- Add backward encoder (bidirectional encoder-decoder model)
- Feed in the sentence vector to each time step of the decoder (attention mechanism)

## Ressource

- [Latent Dirichlet Allocation by David Blei, Andrew Ng, and Michael Jordan](http://www.jmlr.org/papers/volume3/blei03a/blei03a.pdf)
- [Dirichlet Distribution](https://towardsdatascience.com/dirichlet-distribution-a82ab942a879)
- [Blog by Jay Alammar](http://jalammar.github.io/)
- [The Unreasonable Effectiveness of Recurrent Neural Networks](http://karpathy.github.io/2015/05/21/rnn-effectiveness/)
- [Google’s Neural Machine Translation System: Bridging the Gap between Human and Machine Translation](https://arxiv.org/pdf/1609.08144.pdf)
- [Abstractive Text Summarization using Sequence-to-sequence RNNs and Beyond](https://arxiv.org/pdf/1602.06023.pdf)
- [Encoder-Decoder Models, Attention, and Contextual Embeddings](https://web.stanford.edu/~jurafsky/slp3/10.pdf)

# Communicating with Natural Language

### Voice User Interfaces

- **VUI**: speech platform that enables humans to communicate with machines by voice
- Human voice to text (speech recognition)
  - Sound vibrations to audio signal in microphone; samples to vectors of component frequency (feature extraction); decode and recognize
  - Acoustic model, language model, accent model
- Text input reasoning to text (reply)
  - Just map most probable request phrase; requests must be pre-mapped
- Text to speech
  - Speech synthesis; text to speech (TTS)

#### Applications

- Applications are more and more common: voice is natural for humans, effortless, fast
- Interfaces in cars
- Dictation applications
- Conversational AI technology

### Speech Recognition

- **ASR**: Automatic Speech Recognition
- Challenges
  - Noise in audio signal
  - Variability of pitch, volume, word speed
  - Word boundaries and separation
  - Language knowledge to avoid ambiguity (context matters)
  - Spoken versus written language (hesitations, repetitions, fragments)

#### Signal Analysis

- Sinusoidal vibrations in air; detected by microphone; audio signal
- Fourier transformation (FFT) to break signal into frequency components
  - Decomposing mathematical functions into sums of simpler trigonometric functions; decompose an audio signal into component sinusoidal functions at varying frequencies
  - Convert to spectrogram (frequency domain representation of the audio signal through time)
  - Each time frame represented as vector of amplitudes at each frequency
- Feature extraction to reduce noise and unnecessary information (dimensionality) with MFCC (Mel Frequency Cepstrum Coefficient Analysis)
  - *Mel Scale* shows what pitches human listeners can truly discern
    - Put frequencies of spectogram into bins; filter out sound that we can't hear
  - *Cepstral analysis* to separate source (unique to person; dropped) and filter (articulation of words) in human voice production model
  - Mel frequency analysis and cepstral analysis to obtain 12-13 MFCC features

#### Phonetics

- Study of sound in human speech
- Break down human words in small sound segments
  - 39-44 phonemes in U.S. English
- Grapheme is smallest distinct unit that can be written in a language
  - 26 letters in alphabet and space
- Letter may map to multiple phoneme sounds; phonemes map to more than one letter combination
  - Example: "cat", "chat", "circle" for grapheme *c* and "receive", "beet", "beat" for phoneme *IY*
- Lexical decoding: convert acoustic model to phonemes
  - Design choice whether to convert to phonemes first or directly to words; better performance with phonemes on large vocabulary

#### HMMs in Speech Recognition

- HMMs to detect patterns through time and convert features into phonemes
- Use in acoustic model to solve problem of time variability while speaking
- Train HMM model with phonememes; all phonemes combination have lower dimensionality than all word combinations

#### Language Model and N-grams

- Inject language knowledge into words to text conversion to solve ambiguity in spelling and context
  - Example: "here" and "here"
- N-grams to approximate the sequence probability with chain rule

#### Deep Neural Networks

- RNNs are today's go to solution for speech recognition with large data size; traditional ASR with HMMs levels of in acuracy
- CNN instead of MFCC to find relevant patterns and features in speech
- RNN instead of HMMs to track time series data 
- CTC (connectionist temporal classification) layer for sequencing
  - Sequencing problem: number of frames does not have a predictible correspondence to number the output symbols
  - By contrast, RNN produces probability distribution of output symbols for each frame

## Ressource

- [Udacity Project: Build an Alexa History Skill](https://github.com/udacity/NLPND-VUI-Alexa)
- [Build An Alexa Fact Skill](https://github.com/alexa/skill-sample-nodejs-fact)
- [Fourier Transforms – the most important tool in mathematics?](https://ibmathsresources.com/2014/08/14/fourier-transforms-the-most-important-tool-in-mathematics/)
- [Speech Recognition by Mitch Marcus](https://www.seas.upenn.edu/~cis391/Lectures/speech-rec.pdf)
- [Speech Feature Extraction Techniques: A Review](https://www.ijcsmc.com/docs/papers/March2015/V4I3201545.pdf)
- [Speech Technology: A Practical Introduction Topic: Spectrogram, Cepstrum and Mel-Frequency Analysis](http://www.speech.cs.cmu.edu/15-492/slides/03_mfcc.pdf)
- [Mel Frequency Cepstral Coefficient (MFCC) Tutorial](http://practicalcryptography.com/miscellaneous/machine-learning/guide-mel-frequency-cepstral-coefficients-mfccs/)

- [LibriSpeech ASR Corpus](http://www.openslr.org/12/)
- [Automatic Speech Recognition by Kai-Fu Lee](https://www.youtube.com/watch?v=PJ_KCTsOCrs)
- Design and Implementation of Speech Recognition Systems
  - [Class 7/8: HMMs](http://www.cs.cmu.edu/~bhiksha/courses/11-756.asr/spring2014/lectures/class7-8.hmm.pdf)
  - [Class 13: Continuous Speech](http://www.cs.cmu.edu/~bhiksha/courses/11-756.asr/spring2014/lectures/class9.continuousspeech.pdf)
  - [Class 19: Subword Units](http://asr.cs.cmu.edu/spring2011/class21.6apr/class21.subwordunits.pdf)
- [Language Modeling: Introduction to N-grams](http://web.stanford.edu/class/cs124/lec/languagemodeling2016.pdf)
- [Deep Speech 2: End-to-End Speech Recognition in English and Mandarin](https://arxiv.org/pdf/1512.02595v1.pdf), [Video](https://www.youtube.com/watch?v=g-sndkf7mCs)
- [Gram-CTC: Automatic Unit Selection and Target Decomposition for Sequence Labelling](https://arxiv.org/pdf/1703.00096.pdf)
- [EESEN: End-to-end speech recognition using deep RNN models and WFST-based decoding](https://arxiv.org/pdf/1507.08240.pdf)

# Python Snippets

#### String translate()

String is replaced by its vowel position

```python
from string import maketrans   # Required to call maketrans function.

intab = "aeiou"
outtab = "12345"
trantab = maketrans(intab, outtab)

str = "this is string example....wow!!!";
print str.translate(trantab)
```

Delete 'x' and 'm' characters from the string, replace others

```python
from string import maketrans   # Required to call maketrans function.

intab = "aeiou"
outtab = "12345"
trantab = maketrans(intab, outtab)

str = "this is string example....wow!!!";
print str.translate(trantab, 'xm')
```

#### Pretty-print Data Structures

```python
from pprint import pprint

local_data = [ 'a', 'b', 1, 2 ]
pprint(local_data)
```
