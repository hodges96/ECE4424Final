## Contributors

Luke Beckwith - luke98@vt.edu  
Ethan Hodges - hodges96@vt.edu  
Connor Rudy - cmrudy@vt.edu  
Adam Wilborn - adamw97@vt.edu  

## Overview

For our project, our goal was to reproduce and extend the results found in the paper "A Hybrid Model for Role-related User Classification on Twitter" [1]. In this study, contributors proposed TwiRole, a multi-layered model for classifying Twitter users based on role. A user's role can be defined as male-related, female-related, or brand-related. The classification of Twitter roles has many benefits to both academic and industrial applications. For example, targeted advertisement can utilize role to reach a certain market or demographic.

The hybrid model introduced in this study used several layers of classification. First, the model applied a Basic Feature (BF) multi-classifier, assigning roles based on five common features: name, description, Twitter Follower-Friend ratio, profile image brightness, and tweet content. Next, an Advanced Feature (AF) multi-classifier further explored tweet contents using the K-Top Words method. This method examines the most frequently used words across a collection of tweets. Finally, a Convolutional Neural Network (CNN) is applied to the user's profile picture. These classifications are used in conjunction with one another to produce a prediction of male, female, or brand-related role for the given users.

Our work focused on the AF multi-classifier within TwiRole. In order to verify the results from the original paper, we conducted a series of experiments. First, we attempted to reproduce the paper's results using the same classifiers and the same data. Next, we collected our own dataset of Tweets and applied the original paper's classifiers. Finally, we explored several other classifiers to see if we could produce better results than the classifiers chosen in the original paper. A more in-depth approach and our results are detailed below.

## Approach

Approach

## Concerns and Issues

Concerns

## Reproduction and Results

Reproduction

#### Reproducing Original Results

Running

#### Generating Results with New Data

Data Changes

#### Applying Different Classifiers

New Classifiers

## Conclusion

Conclusion

## References

References
