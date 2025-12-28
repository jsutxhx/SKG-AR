# SKG-AR
This repository contains the annotated STM corpus with coreferences, populated knowledge graphs and source code for the paper:
Enhancing Academic Paper Recommendation via Fine-Grained Knowledge Entities and Multidimensional Document Embeddings

## Installation
Python 3.7 required. Install the requirements with:
- (in case pipenv isn't installed yet: `pip install pipenv`)
- `pipenv install`

## Fine-gained Knowledge Entities

### Datasets
- data/stm-coref: contains the annotated coreferences separated per domain BRAT/standoff format.
- data/stm-entities: contains the annotated concepts separated per domain in BRAT/standoff format.
- data/silver_labelled: contains predicted concepts and coreferences of the silver labelled corpus.
- data/STM coreference annotation guidelines.pdf: annotation guidelines for coreference annotions in the STM-corpus.

### Entity recognition
ner-cascade.py best model: SciBERT+BiLSTM(cascade).
ner-base.py run baseline models. Please utilize various pre-trained models by configuring the parameters in the Config class.

## Knowledge Graphs
The folder knowledge_graph/ contains various knowledge graphs.

### Test-STM-KG
- knowledge_graph/gold_kg_cross_domain.jsonl: Test-STM-KG (cross-domain)
- knowledge_graph/gold_kg_in_domain.jsonl: Test-STM-KG (in-domain)
  
To evaluate the effect of coreference resolution in knowledge graph population against the Test-STM-KG, run the following python script:
- evaluate_kgs_against_test_stm_kg.py: prints the evaluation metrics
  
### In-domain and cross-domain research knowledge graph 
- knowledge_graph/stm_silver_kg_cross_domain_with_corefs.jsonl: Contains the cross-domain KG populated from 55,485 abstracts
- knowledge_graph/stm_silver_kg_in_domain_with_corefs.jsonl: Contains the in-domain KG populated from 55,485 abstracts
  
### Build knowledge graphs
To build the in-domain and cross-domain Test-STM-KG and the research knowledge graphs, run the following python script:
- build_kgs.py: creates the knowledge graphs in knowledge_graph/

## Recommendation

### Datasets
The evaluation KG is based on the STM-KG.
We use the in-domain KG ('data/stm_silver_kg_in_domain_with_corefs.jsonl') and cross-domain KG ('data/stm_silver_kg_cross_domain_with_corefs.jsonl') for evaluation. 

The file 'data/documents_citations.jsonl' contains the citations and the file 'data/abstracts_specter.json' contains the abstracts for each paper in the STM-KG.

### Embeddings
The file 'data/abstracts_specter_embeddings.json' contains the SPECTER embeddings for each abstract. 
The embeddings can be recreated with the SPECTER library (see also 'embed_specter.py'): https://github.com/allenai/specter

The file 'data/abstracts_embeddings_average_word_embeddings_glove.840B.300d.jsonl' contains GloVe embeddings and the file 'data/abstracts_embeddings_allenai_scibert_scivocab_uncased.jsonl' SciBERT embeddings (averaged).
These embeddings can recreated with the sentence transformers library (see also 'embed_sentence_transformers.py'): https://github.com/UKPLab/sentence-transformers  

### Ranking of Recommendation
To build the citation graph and perform the ranking, run the script 'evaluate_citation_recommendation_ranking.py'.
Check the TODO statements to vary the evaluation (e.g. to change the KG).

## Citation
Please cite the following paper if you use this code and dataset in your work.
    
>Haixu Xi, Heng Zhang, Chengzhi Zhang\*. Enhancing Academic Paper Recommendations Using Fine-Grained Knowledge Entities and Multifaceted Document Embeddings. ***Scientometrics***, 2026. [[doi]]()  [[arXiv]]()
