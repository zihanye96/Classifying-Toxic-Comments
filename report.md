# Introduction
The goal of this project is to create a classifier that identifies whether or not a comment is toxic. The computer-automated identification of inappropriately toxic comments, which may contain expletives, offensive language, and/or group-targeted hate, is critical in a larger sociocultural battle against youth exposure to inappropriate language and against group-directed prejudice and discrimination. The dataset used in this project contains Wikipedia comments which have been labeled by human raters for toxicity. Here, we use the text of these thousands categorized comments in order to generate, train, and test a computational model to predict whether or not a given comment is toxic. To do this, we created 11 intuitive features used for modeling and constructed various classification models (Naive Bayes, Pruned Classification Tree, Random Forest, Logistic Regression, Neural Network, and Support Vector Machines). In the end, we selected a model using sensitivity and balanced accuracy as criteria, and the model was able to correctly classify toxic comments over 93\% of the time. 



## Method
 
### Overview

For this project, we used a dataset containing Wikipedia comments which have been labeled by human raters for toxic behavior. For the scope of this project, we would like to create a hard classifier that identifies whether or not a comment is toxic. We believe that such a model, which identifies only toxic comments from wikipedia pages, can be a good first step to filtering out all types of toxic comments from the internet. Our goal for this project is to build a model that best predicts whether or not a comment is toxic while having high sensitivity (proportion of toxic comments that are correctly identified as such). To do this, we considered the following models: Naive Bayes, GLM, Classification Tree, Random Forest, Neural Network, and Support Vector Machine (SVM) with linear, polynomial, and radial Kernels. We want to create a relatively simple model that contains only the most intuitive features that factor into classifying a comment as toxic or nontoxic. Therefore, we limited the number of features that our models use to around 10 features. We also want sensitivity to be the primary criterion in choosing our "best" model because we believe that for our purposes, it's better to identify as many toxic comments as possible, perhaps at the expense of incorrectly classifying some nontoxic comments as toxic, as we want to be on the conservative side and minimize internet users' exposures to toxicity. Therefore, we chose a model that had the highest sensitivity while being as accurate as possible, and therefore didn't weigh specificity as heavily in our model selection.
 
### Feature Engineering

Although the dataset contains varying levels of toxicity (toxic, severe toxic, obscene, threat, insult, and identity hate), we simplified the response variable by classifying a comment of any degree of toxicity as simply "toxic". Furthermore, after examining the comments and thinking about common features of toxic and nontoxic comments, we decided to use the following 11 features in our classification model:
1. N: the length of a comment in number of characters
2. PuncN: the number of punctuations used in a comment
3. PropC: whether or not the proportion of capitalized letters in a comment was greater than 0.4.
4. NumN: the number of numeric digits used in a comment
5. MaxWordLength: the length of the longest word in a comment
6. Fu: whether or not the word "fuck" or any word containing it is present in a comment
7. Sht: whether or not the word "shit" or any word containing it is present in a comment
8. You: whether or not the word "you" or any word starting with "you" is present in a comment
9. Excl: whether or not there are more than 2 exclamation points in a row in a comment
10. Curse: whether or not a word from our list of "curse" words or any word containing a word from our list of curse words is present in a comment (see below)
11. Nice: whether or not a word from our list of "nice" words or any word containing a word from our list of curse words is present in a comment (see below)           


For the last two features, the words in our lists were chosen through a combination of examining comments, brainstorming, and trial and error. We looked at the proportion of toxic comments that contained those words and the proportion of nontoxic comments that contained those words and chose the words where there was a significant difference in appearance between the two types of comments. Here are the lists we came up with (please note that these words are written here solely to explain our methods, not to endorse any offensive meaning they imply):
- Curse: fuck, f*ck, shit, cock, gay, sex, fag, ass, bitch, dick, arse, christ, cunt, lol, haha
- Nice: please, thank, apolog, welcome, hello, interest, great, agree, there

### Modelling

After the development and implementation of the aforementioned features, we used a naive Bayes approach, followed by GLM, Classification Tree, Random Forest, Neural Network, and Support Vector Machine (SVM) with linear, polynomial, and radial Kernels. We compared the performance of each model and selected the best one according to criteria discussed below. 

## Results

### Model Performance

We began with a naive Bayes approach to obtain a list of 500 of the most toxic-determining words among the comments; the construction of such a dictionary enabled toxicity prediction (accuracy: 0.8285, sensitivity: 0.7837, specificity: 0.8337). After the creation of 11 intuitive features, we turned to more automated forms of toxicity classification, including:

1. Logistic regression (accuracy: 0.9295, sensitivity: 0.9950, specificity: 0.3654)
2. Pruned classification tree (accuracy: 0.9265, sensitivity: 0.9978, specificity: 0.3125)
3. Random forest (accuracy: 0.9315, sensitivity: 0.9972, specificity: 0.3654)
4. Neural network (accuracy: 0.9315, sensitivity: 0.9955, specificity: 0.3798)
5. Support Vector Machine with Linear Kernel (accuracy: 0.9265, sensitivity: 0.9950, specificity: 0.3365)
6. Support Vector Machine with Polynomial Kernel (accuracy: 0.9240, sensitivity: 0.9983, specificity: 0.2837)
7. Support Vector Machine with Radial Kernel (accuracy: 0.8960, sensitivity: 1.0000, specificity: 0.0000)

Because we wanted to be more cautious than not in our comment toxicity classification, we chose in all models to maximize sensitivity. 


### Model Selection 

As stated in the introduction, we selected a model to be our "best" model using sensitivity as the primary criterion, while also considering how accurate the model is overall. We did this by examining sensitivity and the balanced accuracy. Looking at the test dataset, we found that 89.6\% of comments in our test dataset (1792 in total) were nontoxic, so there is an overrepresentation of nontoxic comments in our test dataset. Therefore, the balanced accuracy estimates the actual accuracy of the model if the dataset had equal proportions of toxic and nontoxic comments. We believe that this is a better estimate for the accuracy of our model. Ultimately, we chose the neural network as our "best" model, as it had the highest balanced accuracy (.6877) and an impressive sensitivity (.9955). It also had the highest specificity (.3798) of all of the models.

## Discussion

Our "best" model had an accuracy of 93.15\% on our test dataset, which means that 93.15\% of comments in our test dataset were correctly classified. The balanced accuracy was 68.77\%, which means that if our test dataset had equal numbers of toxic and nontoxic comments, the model would make accurate predictions for about 69\% of the comments. While this is not an ideal level accuracy, we believe that this number can be increased by adding more features to our model. We wanted to keep our model relatively simple and thus only included features that made the most sense for classifying a toxic or nontoxic comment, but had we included many more features (ex. 50 features), we imagine that our model would be able to perform better in all of the model diagnostics we used (accuracy, balanced accuracy, sensitivity, specificity). We are particularly happy with the fact that our final model had a sensitivity of 99.55\%, which means it was able to correctly identify 99.55\% of toxic comments as toxic. 
