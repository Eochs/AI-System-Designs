# Content Detection System

## Problem:
* Spam, scams, and abusive content have been increasing on all major platforms (TODO: add citation)
* Cannot scale a team of analysts to manually check every piece of content.

## Goals: 
* Detect bad content such as Spam, Abuse, and other violations of ToS. 
* Scrub the content from the site _as soon as possible_.
  * Reduce time needed for analyst to evaluate content.
  * Limit False Positives so analyst is not overwhelmed 

Based on this will have two systems:
1. build a recommender of possible violations that should be looked at by analysts. These are rank-ordered by certainty of violation.
2. If the violation is over a threshold of certainty, automatically remove content with an appeal flow for the user.
![alt text](https://github.com/Eochs/AI-System-Designs/blob/main/Content-Detection-SD.png?raw=true)

## Data:
Target Variable: whether an analyst explicitly flags the recommended violation. Negative is explicit or implicit if they ignore the recommendation.
Features:
* fake email
* flagged by platform admin
* closeness to existing high profile account (Levenshtein Distance or similar, profile image similarity)
* Known flagged IP
* matched flagged keywords (drugs, spam words, etc.)
* posting interval of account
* etc.

System:


Experiment Tracking:




