# An Exploration of the Common Vulnerability Scoring System

## Abstract

- New software == more vulnerabilities 
- Increased difficulty of picking which vulnerabilities to manage
- Main theme -> enhance interpretability (apparently wrong word for that, unsure what it would be
though) of CVE/CVSS data using LDA
- Data driven, complements LLM-based prediction methods.... Why? Faster analysis and groupings, how
  could this be used to help 
- The clustering worked and found the data is organised which is good

## Introduction

- Lots of vulnerabilities,
- Hard to prioritise,
- These are documented using CVE and scored with CVSS,
- Stored in the NVD, widely used in research,
- Enhance interpretability of CVE/CVSS using LDA, advantages:,
    - Copying of abstract, data-driven perspective, as opposed to? LLM-based are also data-driven,
    - Faster analysis times compared with LLM,
    - Inherent groupings of the data,
,
- Some interesting insights focused on INTEGRITY IMPACT:,
    - Vulnerabilities classified as having no impact on data integrity relate highly to DoS/crashes,
    - LOW -> XSS,
    - HIGH -> SQL ( I believe this actually has changed to arbitrary code execution,

## Background

### CVE

- Vulnerabilities are stored in CVEs,
- Example of a CVE,
- Explanation of CVE including mention of CNAs,
- The explanation is from the standpoint of using within machine learning specifically, unsure if,
that still makes full sense, though does add something extra in terms of keeping this in for people who are already well aware of its existence, 
- Positing that people making use of the CVE are knowledgable around the subject, this may be true, for the people filling in the CVE but not necessarily the people who are reading them for their own,

### CVSS

- High level overview of CVSS, specifically version 3.1,
- Summarisation of the spec document for base metrics, could be removed possibly, though it is nice to be able to, specifically talk about aspects of the score as it is so related to the overall research,
- Summarisation of the spec document for temporal metrics,
- Conjecture as to why NVD do not include them in their database,

### Data Options

- This section is messy in general and does not flow together as of yet,
- Description of NVD, some mention of MITRE which is as of yet unknown if it will be added to the report,

No link here between the two, though as this is the primary focus that has already been mentioned
maybe thats fine?

## Clustering Analysis of CVSS Metrics and Vulnerability Descriptions

- Research question: "What are the important keywords for each class within the CVSS metrics?" 
- Important for these reasons:
    - Aids in understanding the patterns in the vulnerability descriptions specific to each CVSS rating

    - Keywords for use when scoring new vulnerabilities -> this is the first time this is mentioned and would be good for it to be brought up earlier, maybe this is a stronger reason than the aiding the LLM prediction

    - Insights into linguistic features of the security experts -> I guess true but could be putting the cart before the horse 
    - Description of the process, state techniques

- Assumption that CVSS descriptions with similar ratings will share common linguistic features
- Start with K-Means
- Move on to LDA -> broad description
- Purity analysis -> probably could be cut as this is part of the LDA
- Probably replace above with stating the merging of clusters idea

- Preamble for clustering results section, though it relates to the LDA part and so is probably in the wrong place, specifies that we are looking at CIA metrics

### K-Means Clustering of Vulnerability Descriptions

Four main steps:

#### Data Preparation

- Load vulnerability descriptions and use TF-IDF vectorisation 

#### Modelling

- Standard K-means algorithm
- Aim is to partition descriptions into 8 clusters of similar vulnerability descriptions
- Explanation of k-means and euclidean distance between TF-IDF vectors

#### Evaluation

- Experiment done multiple times with different seeds
- There is a coherency score but not included as not found useful
- Positive step of inquiry

#### Interpretation

- Example topics from a run of the k-means
- Focus on cluster 4 (0 based indexing, unsure if that makes sense here...) Cluster with clear XSS and wordpress plugin 

- Explanation of the findings in cluster 4, weak reasoning for the choice of numbers for figure 3, choosing five of the words

- Points out the correlation between the trend in figure 4 and overall trend of increasing CVSS numbers -> states as positive result as it points to the figure representing numbers which come from a subsection of the same distribution

### Latent Dirichlet Allocation Methodology

- Introduction of LDA 
- Uses word2vec, does not explain why, maybe does later
- unsupervised -> good for exploring large data, especially when you don't know the groupings
    - to some degree we do know some of the categories, though should we trust them? 
- Allows for CVE descriptions to be in multiple topics, beneficial as CVEs can straddle many
different topics
- Human interpretable topics
- Mentions the paper by neuhaus and zimmerman that I need to think about implementing maybe

Methodology is outlined next

#### Data Preprocessing

- Descriptions are filtered removing stop words and short tokens 
- Descriptions are tokenized -> don't explain how they are tokenized, unsure if that matters
- Dictionary is created, filtering out extremely rare and common terms

Processing step is necessary as the topics are based on word distributions, and stop words muddy the
water -> Should show some quick examples of stop words explaining why they aren't what we want

#### Word Embedding

Using word2vec embeddings -> again, I don't think this has been explained as to why we are doing.... Too much assumed ML/IR knowledge

Just saying it captures semantic relationships is probably not enough

Mention that these are just reasonable defaults -> I feel like in some papers they would just not
mention the exact parameters in this case as it looks better to omit rather than just have
semi-random values.

#### Latent Dirichlet Allocation Training

- Many iterations with different hyperparameters, broadly matching what we found to be best-> Defensive statement about hyperparameter choice.
- Favoured method of analysis came from looking at the clustering results and a human analysis and
purity score

- List of hyperparameters with descriptions of what they mean and how they effect the model
- Hyperparameters define a thorough exploration -> This seems a bit like fluff, might be able to be
  cut or shortened
- LDA was implemented using Gensim, mentioning how it was good to use

#### Topic Assignment and Analysis

Description of process for each saved model
Unsure if this needs its own section

#### Cluster-Class Association










