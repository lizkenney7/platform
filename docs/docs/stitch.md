# Data

## Stitch Overview

The problem in combining customer data with a disparate set of data sources, is that we can rarely find a common, unique key that links all records that belongs to an entity. This is the fundamental reason why identity resolution is required.

Graph-based entity resolution algorithms have emerged as a highly effective approach including utilization of Apache Spark  and GraphFrames. The technique will exhibit an example where efficacy can be achieved based on simple heuristics, and at the same time map a path to a machine-learning assisted entity resolution engine with a powerful knowledge graph at its center.

![Alt text](https://github.com/skypointcloud/platform/blob/master/docs/doc_snippets/stitch.PNG?raw=true)

SkyPoint’s approach to identity resolution produces rich, accurate, and precise customer 360 profiles. There are two phases in the process of building customer 360 profiles.

# Phase I: Data preparation 

All of the initial work needed to get data into a Common Data Model (CDM) environment and prepare it for the matching process.

In this process, we ingest data from multiple sources and then the first phase is to *map* the data columns with their semantic labels. These semantic labels help us to match the data semantically through the more advanced machine learning techniques.

# Phase II: Identity resolution

The records and identities are assigned to unique individuals.

The fundamental task that identity resolution is trying to accomplish is to identify the same individual person within and across all data sources that contain customer information.

There are two approaches that are generally used for this purpose:

## 1. Unique Identifier approach and the Static Rule approach. 

In this approach, the user has to manually select the rules that the algorithm will use. Here, the user can also select the level of match precision; For example: exact match, or high/medium/low match.
   1. Exact Match
      - When Exact match is selected, the rule will try to match the value exactly. The user can also select a transformation over the data such as removal of white space; However values will be considered an exact match only when they are exactly the same after the transformation has taken place.
   2. Partial/Fuzzy Match
      - When the user selects match precision as High/Medium/low, they will have the option to select which kind of algorithm they want to apply to the rule.
      - Currently SkyPoint supports Phonetic match and distance based Levenshtein match.
      - The user can select Phonetic match over the column in which a match would be considered true when both the matching values are phonetically similar (i.e. Dylan and Dillon).
      - Distance based Levenshtein matching is a dynamic programming based approach, and it is one of the most used approaches for high quality matches. In this approach, two values are considered to be a match when converting from one value to another requires less number of transactions, as exemplified by the two values Tony and Tonyy). Converting Tony to Tonyy requires the addition of 1 Y, which is a single transaction. This single transaction can be any of the following actions: update, delete, addition.  
      - ML based match is a work in progress. In this ML based approach, we are creating a statiscal model. This model creates a multiple dimentional projection (around 300 dimentional projection) of a value, which is then put into the locality sensitive hashing to put the similar values in the same bucket. More on this soon...
      - When choosing the desired algorithms, the user can apply more than 1 alorithm with logic AND/OR fashion between them to improve their search results.
      - Note: The selection of Levenshtein algorithm might increase the Match run time significantly.

## 2. Machine Learning approach 

In this approach, the algorithms are trying to find the record's match without any human involvement. 

In this approach, the user does not need to create any manual rule, but the algorithm will figure out (based on the semantic labels) whether 2 or more records should be considered a match based on its own learning.
