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

- Lots of vulnerabilities
- Hard to prioritise
- These are documented using CVE and scored with CVSS
- Stored in the NVD, widely used in research
- Enhance interpretability of CVE/CVSS using LDA, advantages:
    - Copying of abstract, data-driven perspective, as opposed to? LLM-based are also data-driven
    - Faster analysis times compared with LLM
    - Inherent groupings of the data

- Some interesting insights focused on INTEGRITY IMPACT:
    - Vulnerabilities classified as having no impact on data integrity relate highly to DoS/crashes
    - LOW -> XSS
    - HIGH -> SQL ( I believe this actually has changed to arbitrary code execution

## Background

### CVE
- Vulnerabilities are stored in CVEs
- Example of a CVE
- Explanation of CVE including mention of CNAs
- The explanation is from the standpoint of using within machine learning specifically, unsure if
that still makes full sense, though does add something extra in terms of keeping this in for people
who are already well aware of its existence
- Positing that people making use of the CVE are knowledgable around the subject, this may be true
for the people filling in the CVE but no necessarily the people who are reading them for their own
use

### CVSS

- High level overview of CVSS, specifically version 3.1
- Summarisation of the spec document for base metrics, could be removed possibly, though it is nice to be able to
specifically talk about aspects of the score as it is so related to the overall research
- Summarisation of the spec document for temporal metrics
- Conjecture as to why NVD do not include them in their database

### Data Options
- This section is messy in general and does not flow together as of yet
- Description of NVD, some mention of MITRE which is as of yet unknown if it will be added to the
report

## Clustering Analysis of CVSS Metrics and Vulnerability Descriptions

- Research question: "What are the important keywords for each class within the CVSS metrics?" 
- Important for these reasons:
    - Aids in understanding the patterns in the vulnerability descriptions specific to each CVSS
    rating
    - Keywords for use when scoring new vulnerabilities -> this is the first time this is mentioned
      and would be good for it to be brought up earlier, maybe this is a stronger reason than the
    aiding the LLM prediction
    - Insights into linguistic features of the security experts -> I guess true but could be putting the cart before the horse 
- Description of the process, state techniques
- Assumption that CVSS descriptions with similar ratings will share common linguistic features
- Start with K-Means
- Move on to LDA -> broad description
- Purity analysis -> probably could be cut as this is part of the LDA
- Probably replace above with stating the merging of clusters idea
- Preamble for clustering results section, though it relates to the LDA part and so is probably in
the wrong place, specifies that we are looking at CIA metrics

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
- Focus on cluster 4 (0 based indexing, unsure if that makes sense here...) Cluster with clear XSS
and wordpress plugin 
- Explanation of the findings in cluster 4, weak reasoning for the choice of numbers for figure 3,
choosing five of the words
- Points out the correlation between the trend in figure 4 and overall trend of increasing CVSS
numbers -> states as positive result as it points to the figure representing numbers which come
from a subsection of the same distribution

