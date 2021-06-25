# Stack Overflow tag Prediction
Predicting the tag of stackoverflow questions
![image](https://user-images.githubusercontent.com/32350208/123401592-91b81a00-d5c4-11eb-8d0b-1d93e14c2d91.png)


## Table of contents

- [Business/Real-world problem](#business-and-real-world-problem)
- [Business Objectives and constraints](#business-objectives-and-constraints)
- [Mapping to Machine Learning Problem](#mapping-to-machine-learning-problem)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Modeling Multilabel classification](#data-modeling-multilabel-classification)
- [Data Preparation](#data-preparation)
- [Data Split](#data-split)
- [Featurization](#featurization)
- [Machine Learning Modeling](#machine-learning-modeling)
- [Why Not use advanced techniques?](#why-not-use-advanced-techniques)
- [Team](#team)
- [Credit](#credit)

## Business and Real World Problem

### Description
Stack overflow is the largest, most trusted online community for developers to learn, share their progrmming knowledge, and build their careers.

Stack Overflow is something which  every programmer use one way or another. Each month, over 50 million developers come to Stack Overflow to lear, share their knowledge, and build their careers.
It features questions and answers on a wide range of topics in computer programming.
The website serves as a platform for users to ask and answer questions, and, through membership and active participation, to vote questions and answers up or down and edit questions and answers in a fashion similar to a wiki or Digg.
As of April 2014 Stack Overflow has over 4,000,000 registered users, and it exceeded 10,000,000 questions in late August 2015.
Based on the type of tags assigned to questions, the top eight most discussed topics on the site are: Java, JavaScript, C#, PHP, Android, jQuery, Python and HTML.

### Problem Statement
Suggest the tags based on the content that was there in the question posted on Stackoverflow.

__Source__: [See the problem on kaggle](https://www.kaggle.com/c/facebook-recruiting-iii-keyword-extraction/data)

### Source/ useful links
- Data Source: [Click to download the datset](https://www.kaggle.com/c/facebook-recruiting-iii-keyword-extraction/data)
- Youtube: [Click to watch video](https://youtu.be/nNDqbUhtIRg)
- Research Paper 1: [Click to read](https://www.microsoft.com/en-us/research/wp-content/uploads/2016/02/tagging-1.pdf)
- Research Paper 2: [Click to read](https://dl.acm.org/citation.cfm?id=2660970&dl=ACM&coll=DL)

## Business Objectives and Constraints
- Predict as many tags as possible with high precision and recall.
- Incorrect tags could impact customer experience on Stack overflow.
- No strict latency requirements


## Mapping to Machine Learning Problem

### Data

#### Data Overview
- __Refer__: [Click to see the dataset]
- All o fthe data is in 2 files: Train and Test.
    <pre>
    <b>Train.csv</b> contains 4 columns: Id,Title,Body,Tags.

    <b>Test.csv</b> contains the same columns but without the Tags, which you are to predict.

    Size of <b>Train.csv</b> - 6.75GB

    Size of <b>Test.csv</b> - 2GB

    Number of rows in <b>Train.csv</b> = 6034195
    </pre>
    
- The questions are randomized and contains a mix of verbose text sites as well as sites related to math and programming. The number of questions from each site may vary, and no filtering has been performed on the questions(such as closed questions).

__Data Field Explaination__

Dataset contains 6,034,195 rows. The columns in the table are:<br/>
<pre>
<b>Id</b> - Unique identifier for each question<br/>
<b>Title</b> - The question's title<br/>
<b>Body</b> - The body of the question<br/>
<b>Tags</b> - The tags associated with the question in a space-seperated format (all lowercase, should not contain tabs '\t' or ampersands '&')<br/>
</pre>

<br/>

#### Example Data Point
<pre>
<b>Title</b>:  Implementing Boundary Value Analysis of Software Testing in a C++ program?
<b>Body </b>: <pre><code>
        #include&lt;
        iostream&gt;\n
        #include&lt;
        stdlib.h&gt;\n\n
        using namespace std;\n\n
        int main()\n
        {\n
                 int n,a[n],x,c,u[n],m[n],e[n][4];\n         
                 cout&lt;&lt;"Enter the number of variables";\n         cin&gt;&gt;n;\n\n         
                 cout&lt;&lt;"Enter the Lower, and Upper Limits of the variables";\n         
                 for(int y=1; y&lt;n+1; y++)\n         
                 {\n                 
                    cin&gt;&gt;m[y];\n                 
                    cin&gt;&gt;u[y];\n         
                 }\n         
                 for(x=1; x&lt;n+1; x++)\n         
                 {\n                 
                    a[x] = (m[x] + u[x])/2;\n         
                 }\n         
                 c=(n*4)-4;\n         
                 for(int a1=1; a1&lt;n+1; a1++)\n         
                 {\n\n             
                    e[a1][0] = m[a1];\n             
                    e[a1][1] = m[a1]+1;\n             
                    e[a1][2] = u[a1]-1;\n             
                    e[a1][3] = u[a1];\n         
                 }\n         
                 for(int i=1; i&lt;n+1; i++)\n         
                 {\n            
                    for(int l=1; l&lt;=i; l++)\n            
                    {\n                 
                        if(l!=1)\n                 
                        {\n                    
                            cout&lt;&lt;a[l]&lt;&lt;"\\t";\n                 
                        }\n            
                    }\n            
                    for(int j=0; j&lt;4; j++)\n            
                    {\n                
                        cout&lt;&lt;e[i][j];\n                
                        for(int k=0; k&lt;n-(i+1); k++)\n                
                        {\n                    
                            cout&lt;&lt;a[k]&lt;&lt;"\\t";\n               
                        }\n                
                        cout&lt;&lt;"\\n";\n            
                    }\n        
                 }    \n\n        
                 system("PAUSE");\n        
                 return 0;    \n
        }\n
        </code></pre>\n\n
        <p>The answer should come in the form of a table like</p>\n\n
        <pre><code>       
        1            50              50\n       
        2            50              50\n       
        99           50              50\n       
        100          50              50\n       
        50           1               50\n       
        50           2               50\n       
        50           99              50\n       
        50           100             50\n       
        50           50              1\n       
        50           50              2\n       
        50           50              99\n       
        50           50              100\n
        </code></pre>\n\n
        <p>if the no of inputs is 3 and their ranges are\n
        1,100\n
        1,100\n
        1,100\n
        (could be varied too)</p>\n\n
        <p>The output is not coming,can anyone correct the code or tell me what\'s wrong?</p>\n'
<b>Tags </b>: 'c++ c'
</pre>

### Mapping the real-world problem to as Machine Learning problem

#### Type of Machine Learning problem
It is a multi-class classification problem.

__Multi-label Classification:__ Multilabel classification assigns to each sample a set of target labels. This can be thought as predicting properties of a data-point that are not mutually exclusive, such as topics that are relevant for a document. A question on stackoverflow might be about any of C, Pointer, FileIO and/or memory-mangement at the same time or none of these.

__Credit:__ [click to see multiclass](http://scikit-learn.org/stable/modules/multiclass.html)

#### Performance metric
<b>Micro-Averaged F1-Score (Mean F Score) </b>: 
The F1 score can be interpreted as a weighted average of the precision and recall, where an F1 score reaches its best value at 1 and worst score at 0. The relative contribution of precision and recall to the F1 score are equal. The formula for the F1 score is:

<i><b>F1 = 2 * (precision * recall) / (precision + recall)</b></i><br>

In the multi-class and multi-label case, this is the weighted average of the F1 score of each class. <br>

- __'Micro f1 score':__
Calculate metrics globally by counting the total true positives, false negatives and false positives. This is a better metric when we have class imbalance.

- __'Macro f1 score':__
Calculate metrics for each label, and find their unweighted mean. This does not take label imbalance into account.

- __Mean f1 Score:__[click to read about Mean f1 score](https://www.kaggle.com/wiki/MeanFScore)
- 
- __f1 Score:__[Click to read about Micro f1 score](http://scikit-learn.org/stable/modules/generated/sklearn.metrics.f1_score.html) <br>

- __Hamming loss:__ The Hamming loss is the fraction of labels that are incorrectly predicted.

[Click to read about Hamming Loss](https://www.kaggle.com/wiki/HammingLoss)


## Exploratory Data Analysis

### Data Loading and Cleaning

- __Using Pandas with SQLite to Load the data__
- __Counting the number of rows__
- __Checking for duplicates__
- __header of the dataset:__
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right">
      <th></th>
      <th>Title</th>
      <th>Body</th>
      <th>Tags</th>
      <th>cnt_dup</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Implementing Boundary Value Analysis of S...</td>
      <td>&lt;pre&gt;&lt;code&gt;#include&amp;lt;iostream&amp;gt;\n#include&amp;...</td>
      <td>c++ c</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Dynamic Datagrid Binding in Silverlight?</td>
      <td>&lt;p&gt;I should do binding for datagrid dynamicall...</td>
      <td>c# silverlight data-binding</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Dynamic Datagrid Binding in Silverlight?</td>
      <td>&lt;p&gt;I should do binding for datagrid dynamicall...</td>
      <td>c# silverlight data-binding columns</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>java.lang.NoClassDefFoundError: javax/serv...</td>
      <td>&lt;p&gt;I followed the guide in &lt;a href="http://sta...</td>
      <td>jsp jstl</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>java.sql.SQLException:[Microsoft][ODBC Dri...</td>
      <td>&lt;p&gt;I use the following code&lt;/p&gt;\n\n&lt;pre&gt;&lt;code&gt;...</td>
      <td>java jdbc</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
