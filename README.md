# Information Retrieval Project

This repository contains the code for an Information Retrieval project, part of the Information Retrieval course at Amirkabir University of Technology.
The project is supervised by Dr. Nik Abadi.

## Overview

The project is an information retrieval engine that uses the [Parsivar](https://github.com/ICTRC/Parsivar.git) library. It employs techniques such as normalization and stemming to create a positional index for its dataset.

## Dataset
The project's dataset is about 12000 news articles from different persian new agencies, in following format : 

```json
{
  "title": "Article Title",
  "content": "New Content",
  "tags": ["A List of Article Tags"],
  "date": "Date of Publication",
  "url": "URL to Article",
  "category": "Catogery of Article"
}
```

## [Phase 1](Phase_1/IR_Engine.ipynb)
This phase includes 3 tasks : 

- Processing dataset artcles in order to create the positional index
- Creating positional index using processed docs
- Implementing the "Boolean Query Processing Unit"


### Task 1_1
In this task, articles are loaded, normalized, tokenized and stemmed, stop words are also deleted from tokens.
the outpu of this task is a hashmap, relating each docID with a list of processed tokens.

### Task 1_2
In this task processed tokens are traversed to create a positional index. In this positional index,
we keep for each term, its overall frequency and postings lists of docs that contains this term.
In each postings list we keep for each doc, its docID, frequency of the term in the doc and a list of positions of term in the document.

### Task 1_3
In this task, a Boolean Query Processing Unit is Implmented, this unit is capable of rtreiving doc that contain  a term and exclude those taht certain terms or
phrases. the results are classified by how many terms each doc contains and the aggregated frequency of terms. <br>
<br>
A single output example : 

```
{
  docID : "the Articles ID"
  title : "Article Title",
  url : "URL to Article",
  frequency : "Aggregate Frequency of Terms",
  sentences : ["A list of sentences in each doc that contains the terms or phrases requested"]
}
```


## [Phase 2](Phase_2/IR_Engine.ipynb)
This phase includes 2 tasks :

- Enhancing positional index and Query Processing Unit to support ranked retreival
- Increasing efficiency using index elimination and champion lists



### Task 2_1
In this task, we enhance positional index to store IDF for each term and TF for each Doc_Term pair.
we can then use this enhanced version to implement Cosine and Jacquard similarity functions. <br>

IDF Formula :
```python
  IDF = math.log10(allDocsCount/ docFrequency)
```
TF Formula :
```python
  TF = (1 + math.log10(docNum))
```

### Task 2_2
To decrease the delay of Query Processing, we implement "Champion Lists" and use "Index Elimination"
to prune the docs that are less likely to end up in the "Top-K" list.
