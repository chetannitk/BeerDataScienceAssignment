# BeerDataScienceAssignment

Beer Data Science exploratory data analysis.

## Project Organization


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
    
 
## Steps to Run:


* Create environment using conda or venv having python 3.6 ex: ```conda create -n env_name python=3.6```
* ```pip install -r requirements.txt```
* All the notebooks are present in notebooks folder.
* There are 4 notebooks. First notebooks can be run locally and all others notebooks should be run 
  in google colab because of higher computation.
* **02-Beer_review_natural_language_understanding.ipynb** contains the preprocessing of sentence embedding and its vector
       indexing in FAISS. It will take time to generate the index. I have shared **data** folder link in mail you have to put
       data folder inside My Drive in google drive to run all others notebook.
* **03-Beer_recommendation_based_on_review.ipynb** Contain the beer recommendation based on riview similarity.
* Click on the colab icon in 02, 03, 04, 05 notebook to run in Google Colab.
* **04-k-mean-clustering-to-find-similar-beer-drinkers.ipynb** contains similar beer group drinkers using spark-ml k-means.
* **05-sklearn-k-mean-clustering-to-find-similar-beer-drinkers.ipynb** contains similar beer group drinkers using sklearn k-means and 50 dim wordembedding.
    
    
    
    
    <!DOCTYPE html>
<html lang="en">
 <head>
<meta charset="utf-8">
 <link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Pacifico">
 <link rel="icon" href="http://obj-cache.cloud.ruanbekker.com/favicon.ico">
 <link href="//netdna.bootstrapcdn.com/bootstrap/3.0.0/css/bootstrap.min.css" rel="stylesheet">

 <script src="https://ajax.googleapis.com/ajax/libs/jquery/2.1.3/jquery.min.js"></script>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
 <link href="http://cdnjs.cloudflare.com/ajax/libs/normalize/3.0.1/normalize.css" rel="stylesheet" type="text/css">
 <link rel="stylesheet" href="http://ajax.googleapis.com/ajax/libs/jqueryui/1.10.3/themes/smoothness/jquery-ui.min.css">
 <link rel="stylesheet" href="http://netdna.bootstrapcdn.com/font-awesome/4.3.0/css/font-awesome.min.css">
 <link rel="stylesheet" href={{ url_for('static', filename="css/notify-flat.css") }}>



 <script type=text/javascript>
     $SCRIPT_ROOT = {{ request.script_root|tojson|safe }};
 </script>

<script>
$(document).ready(function() {          
    $('.btn').each(function(){
        var icd_added =  $(this).attr('id');
        $(this).click(function(){
	     $.post(`/v1/search_response?icd_tag=${icd_added}`);
               var notes = $('#notes').notify({
                removeIcon: '<i class="icon icon-remove"></i>'
               });
  
               notes.show(`${icd_added} added successfully`, {
                        title: 'Notification: ',
		        type: 'success',
                        sticky: false
                });
        });
    });
});


</script>

<title>ICD-10 Code Search Engine</title>
 </head>


<body>
  <img src="https://www.evolenthealth.com/sites/all/themes/evolentcorporate/logo.png" class="logo" align="right"></img>

  <div id="notes"></div>
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js"></script>
  <script src="http://code.jquery.com/ui/1.10.3/jquery-ui.js"></script>
  <script src="http://cdnjs.cloudflare.com/ajax/libs/jquery-easing/1.3/jquery.easing.min.js"></script>
  <script src= {{ url_for( 'static', filename="js/notify.js") }}></script>

  <!-- Flash messages -->
 {% with messages = get_flashed_messages(with_categories=true) %}
  {% if messages %}
        <script>
        var notes = $('#notes').notify({
                removeIcon: '<i class="icon icon-remove"></i>'
        });
  
        notes.show("{{ messages[0][1] }}", {
                        title: 'Notification: ',
                        type: '{{ messages[0][0] }}',
                        sticky: false
                });
       </script>
  {% endif %}
  {% endwith %}
  {% block body %}{% endblock %}
<div class="container">
 <div class="row">
<div class="col-md-12">
         <ul class="nav nav-pills">
         <li class="active"><a href="/v1/dashboard">Home</a></li>
         <li><a href="/v1/search">Search</a></li>
         </ul>
 </div>


 </div>
 <div style="background:transparent !important" class="jumbotron">
 <div style="font-family: 'Times New Roman'">
 <p>
 <center>
 <font size="6" style="color:rgb(239,127,26);">
         ICD-10 Code Search Engine</font>
 </center>
 </p>
 </div>
 </div>
<form action="/v1/search/results" method="post">
 <div class="input-group">
 <input type="text" class="form-control input-lg" name="input" placeholder="Search" autofocus>
 <div class="input-group-btn">
 <button class="btn btn-primary btn-lg" type="submit">
 <i class="glyphicon glyphicon-search"></i>
 </button>
 </div>
 </div>
 </form>
    <center>
 <br/> <h3>{{ res['hits']['total']['value'] }} results found for <em>"{{res['ST']}}" </em> </h3>
 </center>
 <br/>
<table class="table">
 <thead>
 <tr>
 <th>ICD Code</th>
 <th>Desc</th>
 <th>HCC</th>
 <th>Score</th>
 </tr>
 </thead>
    {% for hit in res['hits']['hits'] %}
       <tbody>
         <tr>
            <th scope="row">{{ hit['_source']['icd10_code'] }}</th>
            <td><a href="#">{{ hit['_source']['desc'] }}</a></td>
            <td> {{ hit['_source']['hcc']}} </td>
            <td>{{ hit['_score'] }}</td>
	    <td> <button id="{{ hit['_source']['icd10_code'] }}" type="button" class="btn btn-success btn-xs">Add <span class="glyphicon glyphicon-plus"></span></button> </td>
         </tr>
 </tbody>
{% endfor %}
</table>
</div>
 </div>
 </body>
</html>


