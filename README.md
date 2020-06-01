BeerDataScienceAssignment
==============================

Beer Data Science exploratory data analysis.

Project Organization
------------

    ├── LICENSE
    ├── Makefile           <- Makefile with commands like `make data` or `make train`
    ├── README.md          <- The top-level README for developers using this project.
    ├── data
    │   ├── external       <- Data from third party sources.
    │   ├── interim        <- Intermediate data that has been transformed.
    │   ├── processed      <- The final, canonical data sets for modeling.
    │   └── raw            <- The original, immutable data dump.
    │
    ├── docs               <- A default Sphinx project; see sphinx-doc.org for details
    │
    ├── models             <- Trained and serialized models, model predictions, or model summaries
    │
    ├── notebooks          <- Jupyter notebooks. Naming convention is a number (for ordering),
    │                         the creator's initials, and a short `-` delimited description, e.g.
    │                         `1.0-jqp-initial-data-exploration`.
    │
    ├── references         <- Data dictionaries, manuals, and all other explanatory materials.
    │
    ├── reports            <- Generated analysis as HTML, PDF, LaTeX, etc.
    │   └── figures        <- Generated graphics and figures to be used in reporting
    │
    ├── requirements.txt   <- The requirements file for reproducing the analysis environment, e.g.
    │                         generated with `pip freeze > requirements.txt`
    │
    ├── setup.py           <- makes project pip installable (pip install -e .) so src can be imported
    ├── src                <- Source code for use in this project.
    │   ├── __init__.py    <- Makes src a Python module
    
 
Steps to Run:
=======================

    - Create environment using conda or venv with python 3.6
    - pip install -r requirements.txt
    - All the notebooks are present in notebooks folder.
    - There are 4 notebooks. First notebooks can be run locally and all others notebooks should be run 
       in google colab because of higher computation.
    - **02-Beer_review_natural_language_understanding.ipynb** contains the preprocessing of sentence embedding and its vector
       indexing in FAISS. It will take time to generate the index. I have shared **data** folder link in mail you have to put
       data folder inside My Drive in google drive to run all others notebook.
    - **03-Beer_recommendation_based_on_review.ipynb** Contain the beer recommendation based on riview similarity.
    
