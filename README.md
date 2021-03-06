# Toxic Media

## About

*Disclaimer: This project contains text that is profane, vulgar, and offensive due to the nature of the dataset.*

We live in an age where people's lives have become intertwined with their online presence allowing humans to engage with one another on a larger scale than ever before.  However, not all of these interactions are friendly.  People exploit the fact that their identity remains hidden and choose to target one another with unwarranted abuse causing harm to people they will never meet in person.  For our society to truly prosper from the digital age we have to combat this toxic behavior.  This will enable more and more people who are scared of what other people think when they post on social media to engage freely without the fear of being the target of online hate.  

Our task is to improve civility on social media platforms (e.g., Twitter) and online comment forums (e.g., Reddit) by training a model that determines how likely a users comment will make another user leave a conversation.  With our model, we will create a web application that tracks how toxic each social media platform and online comment forum is to bring awareness to this issue and spark initiative to create a toxic free environment for all users.  

This issue can only be solved with the help of everyone encouraging kindness instead of spreading hate.

## Data Description
The dataset used in this project is from the kaggle competition: [Jigsaw Unintended Bias in Toxicity Classification](https://www.kaggle.com/c/jigsaw-unintended-bias-in-toxicity-classification/data).

In 2017 the Civil Comments platform shutdown and released their archive of ~2 million public comments for researchers to study in an effort to improve civility online. Jigsaw funded the annotation of this data by human raters. 

The column `toxicity` is our toxicity label which contains a number between 0-1 denoting the fraction of human labelers that believed the comment would make someone else leave a conversation. 

For our analysis we'll define the comment as toxic (denoted 1) when the value of our target `toxicity` is greater than or equal to 0.5 otherwise we'll assign the instance to the negative class (denoted 0).

There are a lot of additional labels denoting the fraction of human labelers who believed the comment depicted several other sub-toxic labels and whether specific identity attributes were mentioned in the comment. These subtype attributes are:
* severe_toxicity
* obscene
* threat
* insult
* identity_attack
* sexual_explicit
* male
* female
* transgender
* other_gender
* heterosexual
* homosexual_gay_or_lesbian
* bisexual
* other_sexual_orientation
* christian
* jewish
* muslim
* hindu
* buddhist
* atheist
* other_religion
* black
* white
* asian
* latino
* other_race_or_ethnicity
* physical_disability
* intellectual_or_learning_disability
* psychiatric_or_mental_illness
* other_disability

It was also mentioned that different comments might have the exact same text, but labeled with different targets or sybtype attributes.

These subtype attributes will be **removed** from the training schema because we will not have access to them in a production environment.  However, they will be very resourceful as tags used during error analysis to see where exactly our model is performing poorly on.

### Labeling Schema
As mentioned on Kaggle, each comment was shown to up to 10 human labelers.  The labelers were asked to rate how toxic each comment is. 
* Very Toxic
* Toxic
* Hard to Say
* Not Toxic

The ratings were then aggragated into the `target` column.

The subtype attributes were collected by asking the human labelers whether the attribute was mentioned in the comment.  Then, taking these responses and aggregating them into a value between 0-1 representing the fraction of human labelers who believed the subtype attribute was mentioned in the comment.

*Note: Some comments were shown to more than 10 human labelers because of sampling strategies to increase rating accuracy.*