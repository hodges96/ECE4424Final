## Contributors

Luke Beckwith - luke98@vt.edu  
Ethan Hodges - hodges96@vt.edu  
Connor Rudy - cmrudy@vt.edu  
Adam Wilborn - adamw97@vt.edu  

## Overview

For our project, our goal was to reproduce and extend the results presented in the paper *A Hybrid Model for Role-related User Classification on Twitter* [1]. In this study, contributors proposed TwiRole, a multi-layered model for classifying Twitter users based on role. A user's role can be defined as male-related, female-related, or brand-related. The classification of Twitter roles has many benefits to both academic and industrial applications. For example, targeted advertisement can utilize user roles to reach a certain market or demographic.

The hybrid model introduced in this study used several layers of classification. First, the model applied a Basic Feature (BF) multi-classifier, assigning roles based on five common features: name, description, Twitter Follower-Friend ratio, profile image brightness, and tweet content. Next, an Advanced Feature (AF) multi-classifier further explored tweet content using the K-Top Words method. This method examines the most frequently used words across a collection of tweets. Finally, a Convolutional Neural Network (CNN) is applied to the user's profile picture. These classifications are used in conjunction with one another to produce a prediction of male, female, or brand-related role for each given user.

Our work focused on the AF multi-classifier within TwiRole. In order to verify the results from the original paper, we conducted a series of experiments. First, we attempted to reproduce the paper's results using the same classifiers and the same data. Next, we collected our own dataset of tweets and applied the original paper's classifiers. Finally, we explored several other classifiers to see if we could produce better results than the classifiers chosen in the original paper. A more in-depth approach and our results are detailed below.

## Approach

Our first step was to reproduce the original paper's results. The authors utilized a 10-fold cross-validation technique to train the model using five different classifiers: Decision Tree, SVM, AdaBoost, GradientBoost, and Random Forest. Each one was applied to both the Basic Features and Advanced Features detailed above. The code for running each of these classifiers was provided to us, so we ran it for ourselves against the Advanced Features to see if we produced similar accuracies.

After verifying the authors' data by reproducing their environment as best we could, we decided to run the model against a different dataset. This would allow us to further reinforce the conclusions reached by the original team. Unfortunately, we could not find any available datasets that met the requirements of this project, so we built our own using a technique similar to the one described in *Gender Classification using Twitter Feeds* [2]. The basic process we followed was to first retrieve common male and female names from the 2010 United States census, then use them to obtain Twitter handles that likely belonged to male or female Twitter users. Tweets for each user were scraped using Twitter's API. To obtain tweets from brand-related users, we consulted a list of Fortune 1000 companies' Twitter handles [3]. Similar to before, we made requests using Twitter's API to build a database of tweets. We recognize that the method that we applied to building our own database introduced bias, and we address these concerns below in the Issues and Concerns section.

Finally, we wished to extend the original paper’s results by using three other classifiers in the model. We used Linear Discriminant Analysis, K-Neighbors, and Gaussian Naive Bayes to see if we could find a classifier that performed better than those explored in the original study. To do this, we subsituted these classifiers into the provided code and followed the same process as before.

## Issues and Concerns

Before we present the results of our experimentation, we would like to address several potential concerns with this application of Machine Learning. First and foremost, any application that utilizes algorithmically assigned gender will be inherently biased. Even the best classifier implemented for the paper had less than a 90% accuracy rate when classifying users by role. The 10% percent of misclassified users could experience adverse effects ranging in severity stemming from this model. This issue must be kept at the forefront of any discussion when implementing a system such as the one described.

In addition, there are many Twitter users who identify as transgender or non-binary. Attempting to force these users into a binary box will create discriminatory effects targeting these individuals.

As mentioned above, our process for building our dataset also introduced its own share of concerns. Primarily, we had to create our own labels for each Twitter handle by looking at common gendered names from the US census. According to our focus paper, name is the second most distinguishing feature between roles, right after analysis of a user's profile picture [1]. For that reason, we decided that a person's name was an acceptable identifier to group labels for learning. However, as our results below show, a significant decrease in model accuracy accompanied our substitution of new data. This is at least partly attributable to our over-simplified process for assigning role labels to our training data.

## Reproduction and Results

In this section, we present results for each of our reproduction methods described above.

### Reproducing Original Results

When running the analysis using a near-identical environment as the original authors, we found the results to be highly reproducible. As can be seen below in Table 1, the largest discrepancy occurred for the GradientBoosting classifier, with only a 0.3% difference between our results and the original.


| Classifier       | Original  | Reproduced | 
| ---------------- | --------- | ---------- |
| Decision Tree    | 0.618     | 0.618      |
| SVM              | 0.352     | 0.352      |
| AdaBoost         | 0.704     | 0.704      |
| GradientBoosting | 0.738     | 0.735      |
| Random Forest    | 0.708     | 0.707      |

**Table 1: Original and Reproduced Model Accuracies using only AF**


### Generating Results with New Data

When running the analysis using our compiled data, the accuracy was not as high as the original. Several factors could have played a role in this. First of all, the size of our dataset was much smaller than the data used in the original paper. Having less training data causes the model to make assumptions about the specified relationships, without fully identifying what data represents actionable trends and what data is just noise. Another issue was discussed above, where our data-collection method was inherently biased. Our results using our compiled dataset are presented below in Table 2.


| Classifier       | Original  | Reproduced | 
| ---------------- | --------- | ---------- |
| Decision Tree    | 0.618     | 0.571      |
| SVM              | 0.352     | 0.345      |
| AdaBoost         | 0.704     | 0.538      |
| GradientBoosting | 0.738     | 0.713      |
| Random Forest    | 0.708     | 0.688      |

**Table 2: Original and Reproduced Model Accuracies using New Dataset**


### Applying Different Classifiers

When running the analysis with our new classifiers on both the old data and new data, the differences in the calculated accuracies for Linear Discriminant Analysis and K-neighbors were very small. However, when using Gaussian Naive Bayes, the accuracy of the model trained with the original data was much higher than when our compiled data was substituted. Issues similar to those presented above may have been the cause of these differences. Overall, none of the new classifiers that we ran provided higher accuracies than the best classifier from the original paper. Linear Disciminant Analysis and K-Neighbors performed relatively well, but further analysis using the other classification rounds from TwiRole would be necessary to determine if they are better options than the originals. Our results are presented below in Table 3.


| Classifier                   | Original Data  | Compiled Data | 
| ---------------------------- | -------------- | ------------- |
| Linear Discriminant Analysis | 0.705          | 0.675         |
| K-Neighbors                  | 0.684          | 0.662         |
| Gaussian Naive Bayes         | 0.576          | 0.288         |

**Table 3: Model Accuracies for Original and New Datasets using Different Classifiers**


## Conclusion

Overall, our findings are fairly consistent with those of the original research paper. Our reproduction of model accuracies using the original data matched very closely to the findings initially presented, while running the models on our compiled data generated slightly lower accuracies. While our data collection had some issues, the accuracy trends matched generally with the original results. Although we were able to generate promising results using additional classifiers, we believe the authors of the original findings chose a well-rounded set of classifiers to reflect their dataset and produce a satisfactory and true result. For that reason, we believe that the findings originally presented are reasonable, and the authors' method for classification of users seems to have merit.

## References

[1] L. Li, Z. Song, X. Zhang, E. Fox. 2018. *A Hybrid Model for Role-related User Classification on Twitter*.  
[2] J. Avinash, R. Muniraju, S. Shaligraman. 2017. *Gender Classification using Twitter Feeds*.  
[3] Fortune-1000-Company-Twitter-Accounts.csv. https://gist.github.com/mbejda/45db05ea50e79bc42016
