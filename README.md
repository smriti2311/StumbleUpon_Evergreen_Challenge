# StumbleUpon_Evergreen_Challenge

<h1>STEP 1- Data Cleaning and Preprocessing:</h1>
<ul>
<li>Importing the libraries such as numpy, pandas for mathematical operations, scikit learn for metrics calculations.</li>
<li>We have two datasets namely, the train dataset which I read into a dataframe as df_train and the test dataset which I read into a dataframe as df_test.</li>
<li>Rows in both test and train dataset contain certain records where the values are missing  and instead they’re filled with ‘?’. Thus replaced them with ‘0’ so as to denote there exists no null value in the datasets.</li>
</ul>
<h1>STEP 2- NLP:</h1>
<ul>
<li>The main task here is to perform NLP using the column boilerplate which is a json file. The column of ‘boilerplate’ in both train and test datasets contains an entire text file which needs to be vectorized.</li>
<li>The content from the boilerplate column of train dataset and the content from boilerplate column of test dataset are put in separate variables and for each row in boilerplate column, certain characters from the beginning and some from the end are removed so as to obtain the text  that matters in the boilerplate.</li>
<li>This is done for both datasets and now just the text of boilerplate is obtained in separate variables and then concatenated to count them as one column.
TF-IDF vectorizer is implemented to this concatenated text. Why TF-IDF? This stands for Term Frequency- Inverse Document Frequency.</li>
Where,<br>
			
  
    TF = (No. of times a word appears in a document / Total no. of terms in the document)
			
    IDF = log(No. of sentences/No. of sentences containing specific words) 
    
This technique is basically used to denote the importance or relevance of each word in the document. It’s done by multiplying the two metrics i.e: TF and IDF. <br>

<li>After the removal of stop words such as and, is, the, for etc. and ignoring the words that occur in less than 3 sentences (as min_df is set as 3 in the tf-idf vectorizer). 
With TF, the count or frequency of each word (after stop words are removed) are taken care of and with IDF, it’s checked how common or rare the word is in the document. The closer it is to 0, the more common is the word. Thus if the word is common, it will tend to 0 else to 1.</li>
<li>After these two metrics are multiplied we obtain a TF-IDF score which denotes the relevance or importance of each word in the document. Higher the score, more is the relevance of that word in the document.</li>
<li>TF-IDF helps vectorize the text, meaning, assigning numbers to each word to process them and identify their frequency and relevance.</li>
</ul>
<h1>STEP 3 - Creating a classifier using Logistic Regression:</h1>
<ul>
<li>Now that the concatenated text is vectorized and we know the frequency and importance of each word in the boilerplate text. Thus, the vectorized text is now divided into two parts namely X_train and X_test.</li>
<li>We create a Logistic Regression model for this problem as we need to build a classifier which is binary i.e: either 0 for non-evergreen or 1 for evergreen. Logistic regression is best used for binary classification problems.</li>
<li>With arguments passed in the model as, penalty=l2 which denotes Ridge Regression. We use l2 here because the independent features are highly correlated (multicollinearity). Thus, ridge regularization helps in reducing quality errors and the complexity of the model.</li>
<li>Now we want to print cross validation score, CV=5 denotes that 5 fold cross-validation is estimated to take care of bias- variance tradeoff. The model evaluated with k=5 or cv=5 helps in generating a model with neither very high bias nor very high variance.</li>
<li>The logistic regression model is fit on X_train (which was the vectorized text) and y_train which is the dependent feature.
  Y_pred is predicted as tested on the X_test dataset which is the vectorized test text.</li>
</ul>
<h1>STEP 4 - Precision, Recall</h1><br>
<li>The model is now fit and predicts the label of evergreen or non-evergreen against the url_id which we store in a dataframe and save it as a csv file.
But for calculating precision and recall we need original test values to compare the test values to the predicted values.</li>
For precision,<br>

    (True Positive) / (True Positive+False Positive)

It denotes that out of all the positive predicted results how many are actually correctly predicted. For this, we needed to divide the y_train column containing the label into a test and train dataset. <br>

For recall,<br>

	(True Positive) / (True Positive + False Negative)
It denotes how many are predicted correctly out of total actual positives.<br>


<h1>RESULTS</h1>
<ol>
<li>The accuracy of the model is 88%</li>
<li>Precision for class 0 is 85% and for class 1 is 91%</li>
<li>Recall for class 0 is 92% and for class 1 is 83%</li></ol>
