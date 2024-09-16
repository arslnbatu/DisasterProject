# Disaster Response Pipeline Project


# Table of Contents

1. [Instructions:](#instructions)
2. [Summary](#summary)
3. [File Description](#file-desc)
4. [Dataset](#data)
5. [Modeling Process](#model)
6. [Screenshots](#screenshots)
7. [Model results](#result)
8. [Effect of Imbalance](#effect)
### Instructions:  <a name="instructions"></a>
1. Run the following commands in the project's root directory to set up your database and model.

    - To run ETL pipeline that cleans data and stores in the database
        `python data/process_data.py data/disaster_messages.csv data/disaster_categories.csv data/DisasterResponse.db`
    - To run ML pipeline that trains classifier and saves
        `python models/train_classifier.py data/DisasterResponse.db models/classifier.pkl`

2. Run the following command in the app's directory to run your web app.
    `python run.py`

3. Go to http://0.0.0.0:3001/

### Summary: <a name="summary"></a>
In this project, I analyzed disaster data from Figure Eight to develop a model for an API that classifies disaster messages.

The dataset includes real messages sent during disaster events. I created a machine learning pipeline to categorize these events, enabling messages to be directed to the appropriate disaster relief agency.

The project includes a web app located in the app folder. This app allows emergency workers to input new messages and receive classification results across several categories. Additionally, the web app displays data visualizations.
## File Description <a name="file-desc"></a>

* [**ETL Pipeline Preparation.ipynb**](notebooks/ETL%20Pipeline%20Preparation.ipynb): 
Notebook contains ETL Pipeline.
* [**ML Pipeline Preparation.ipynb**](notebooks/ML%20Pipeline%20Preparation.ipynb): 
Notebook contains ML Pipeline.
* [**etl.db**](notebooks/etl.db): etl database.
* [**categories.csv**](notebooks/categories.csv): Categories data set.
* [**messages.csv**](notebooks/messages.csv): Messages data set.
* [**classifier.pkl**](models/classifier.pkl): Trained model pickle file.
* [**train_classifier.py**](models/train_classifier.py): Python file for model training.
* [**transformation.py**](models/transformation.py): Helper file for train_classifier.py
* [**disaster_categories.csv**](data/disaster_categories.csv): Disaster Categories data set.
* [**disaster_messages.csv**](data/disaster_messages.csv): Disaster Messages data set.
* [**process_data.py**](data/process_data.py): Python ETL script.
* [**app**](app/): Flask Web App
* [**run.py**](app/): Flask Web App main script.
* [**img**](img/): Image Folder
* [**requirements.txt**](/requirements.txt): Text file containing list of packages used.
* [**LICENSE**](/LICENSE): Project LICENSE file.


### Dataset <a name="data"></a>
This disaster data is from [Figure Eight](https://www.figure-eight.com/)
This dataset has two files messages.csv and categories.csv.
### Data Cleaning

Merged two datasets into a single DataFrame (df) based on their IDs.
Split the categories into separate columns.
Converted category values to binary (0 or 1).
Replaced the original categories column in the DataFrame with the new category columns.
Removed duplicate entries based on the message column.
Exported the cleaned DataFrame to the etl.db database.

### Modeling Process <a name="model"></a>

Developed a tokenization function to process text data.
Constructed a machine learning pipeline incorporating TfidfVectorizer, RandomForestClassifier, and Pipeline.
Split the data into training and test sets.
Trained and evaluated a basic RandomForestClassifier using the pipeline.
Conducted hyperparameter tuning with 5-fold cross-validation, fitting 100 models to identify the optimal random forest model for predicting disaster response categories. The best parameters for the Random Forest model were:
{
    'clf__criterion': 'entropy',
    'clf__max_depth': 40,
    'clf__max_features': 'auto',
    'clf__random_state': 42
}
Utilized this optimal model to create train_classifier.py.

### Screenshots <a name="screenshots"></a>

![Disaster Response Pipeline Home Page](img/page-1.png)

![Disaster Response Pipeline Result Page](img/page-2.png)

### Model results <a name="result"></a>

Our final RandomForestClassifier model with 5 fold cross-validation has the following results.

![Model Result](img/model-result.png)


### Effect of Imbalance: <a name="effect"></a>
The dataset is an imbalance. We can get an idea of an imbalance from the following image.

![Distribution of Response Category](img/distribution.png)

For imbalanced classes with fewer samples, the model will not generalize well. For various categories, we should focus on recall as all the categories has the same precision.
