# NLP_demo

# Start Trial 
  1. [Parts-of-speech.Info](http://parts-of-speech.info)

  2. [Stanford parser](http://nlp.stanford.edu:8080/parser/index.jsp)

# Project 1: Spam detector

[spam data set](https://archive.ics.uci.edu/ml/datasets/Spambase)

# project 2: sentiment analysis
[sentiment data](https://www.cs.jhu.edu/~mdredze/datasets/sentiment/index2.html)

# NLTK

A example for all usage:
[textanalysis API](https://market.mashape.com/textanalysis/textanalysis#nltk-wordnet-word-lemmatizer)

## nltk download corresponding packages
need to download nltk package besides just install it, based on the run time error, install the missing 
```python
# First start ipython or python terminal
import nltk
nltk.download()
```
this command will start the GUI for NLTK package download, select the missing ones

## Pos Tag
```python
nltk.pos_tag("This is a test string".split())
#output will be
[('this', 'DT'), ('is', 'VBZ'), ('a', 'DT'), ('test', 'NN'), ('string', 'NN')]
```
for all the pos tag, can check this link [penn_treebank_pos](https://www.ling.upenn.edu/courses/Fall_2003/ling001/penn_treebank_pos.html)

## Stemming and Lemmatization
  * Basic idea: reduce the words into base form. for example, "dog" and "dogs" could be same, same for "jump" and "jumping".
  * stemming is more basic or "crude" version
### Stemmer
NLTK has several different stemmer. 
```python
from nltk.stem.porter import PorterStemmer
porter_stemmer = PorterStemmer()
porter_stemmer.stem("wolves")
#Output: 'wolv'
```
###lemmatizer
```python
from nltk.stem import WordNetLemmatizer
lemma = WordNetLemmatizer()
lemma.lemmatize("wolves")
#Output:'wolf'
```

## Token 
Get the token from NLTK
```python
from nltk.stem import WordNetLemmatizer
tokens = nltk.tokenize.word_tokenize(s) # split string into words (tokens)
#Change into basic format: jumping->jump dogs->dog
wordnet_lemmatizer = WordNetLemmatizer()
#remove stop words
tokens = [t for t in tokens if t not in stopwords]
```

##NER: Named entity recognization 
Entity example:
  * Albert Einstein: Name
  * Google: orgnization

```python
s = "albert Einstein was born on March 14, 1879"
tags = nltk.pos_tag(s)
tags:
[('a', 'DT'),
 ('l', 'NN'),
 ('b', 'NN'),
 ('e', 'NN'),
 ('r', 'NN'),
 ('t', 'NN'),
 (' ', 'NNP'),
 ('E', 'NNP'),
 ('i', 'NN'),
 ('n', 'VBP'),
 ('s', 'NN'),
 ('t', 'NN'),
 ('e', 'NN'),
 ('i', 'NN'),
 ('n', 'VBP'),
 (' ', 'NNP'),
 ('w', 'VBP'),
 ('a', 'DT'),
 ('s', 'NN'),
 (' ', 'NN'),
 ('b', 'NN'),
 ('o', 'NN'),
 ('r', 'NN'),
 ('n', 'JJ'),
 (' ', 'NNP'),
 ('o', 'NN'),
 ('n', 'NN'),
 (' ', 'NNP'),
 ('M', 'NNP'),
 ('a', 'DT'),
 ('r', 'NN'),
 ('c', 'NN'),
 ('h', 'NN'),
 (' ', 'VBD'),
 ('1', 'CD'),
 ('4', 'CD'),
 (',', ','),
 (' ', 'VBD'),
 ('1', 'CD'),
 ('8', 'CD'),
 ('7', 'CD'),
 ('9', 'CD')]
```

we do not want this, so split the string first
```python
s = "albert Einstein was born on March 14, 1879".split()
tags = nltk.pos_tag(s)
tags:
[('albert', 'JJ'),
 ('Einstein', 'NNP'),
 ('was', 'VBD'),
 ('born', 'VBN'),
 ('on', 'IN'),
 ('March', 'NNP'),
 ('14,', 'CD'),
 ('1879', 'CD')]
```
Now we want to use *NER* to chunk
```python
#install nltk package 
nltk.ne_chunk(tags)
# get the parse tree
Tree('S', [('albert', 'JJ'), Tree('PERSON', [('Einstein', 'NNP')]), ('was', 'VBD'), ('born', 'VBN'), ('on', 'IN'), ('March', 'NNP'), ('14,', 'CD'), ('1879', 'CD')])
# Or we can virtualize it
nltk.ne_chunk(tags).draw()
```

Another example
```python
s = "steve jobs was Apple CEO"
tags = nltk.pos_tag(s.split())
nltk.ne_chunk(tags)
```

# Latent Semantic Analysis(LSA)
  * synonym: 
    * Used for multiple words have same meaning. 
    Example:"buy" and "purchase", "big" and "large" "quick" and "speed"
  * Polysemy
    * One word has multiple meaning
    * "Man", "Milk"

we can assigne latent variables such as 
  * z = 0.7* computer + 0.5 * PC + 0.3*laptop
  
## underline Math for LSA
  * LSA is just **SVD** on the term document matrix
  * SVD simple version will be PCA
### PCA
  * decorrelate the data
  * transformed data is ordered by information latent
  * Dimension reduction
  
  > removing information != decreasing predictive probablity
  
  > denosing/ smooth / improving generilization 
### SVD

SVD just dose both PCAs on same time on **X^TX** and **XX^T**

## Example of LSA on Book Title 
some process we need to do: 

like book titles have something 3rd edition
```python
tokens = [t for t in tokens if not any(c.isdigit() for c in t)] # remove any digits, i.e. "3rd edition"
```



# Python 3 change

> use dict.items() instead of dict.iteritems()

> use range() instead of xrange()



