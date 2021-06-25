# Stack Overflow tag Prediction
Predicting the tag of stackoverflow questions

## Table of contents

- [Business/Real-world problem](#business-and-real-world-problem)
- [Business Objective and constraints](#business-objective-and-constraints)
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

