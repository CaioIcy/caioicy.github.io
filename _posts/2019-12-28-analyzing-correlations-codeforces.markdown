---
layout: post
title: Analyzing correlations of Codeforce users and their ratings
date: 2019-12-29 12:00:00 +0000
description: While browsing Codeforces I noticed that most high-rated users had seemingly better results in the beginning of their participation than most average-rated users
img: #cf-icon.png # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [codeforces, datascience, statistics, python]
---

[Originally posted to DEV.to](https://dev.to/caioicy/analyzing-correlations-of-codeforces-users-and-their-ratings-41no)

----
A social network and platform for competitive programming, [Codeforces](https://codeforces.com) is a popular place for both beginners and masters alike. Users can participate in regularly held contests to climb the ladder and increase their rating.

While not a regular participant [myself](https://codeforces.com/profile/caioicy), I have always been involved in competitive programming through my former university and friends made therein.

Recently I was browsing the website and noticed that most high-rated users had seemingly better results in the beginning of their participation than most average-rated users. 

![High-rated example](https://thepracticaldev.s3.amazonaws.com/i/6ok5xaaolerv2i5txkkj.png)
<figcaption>Rating over time for high-rated user Benq</figcaption>

----
## Codeforces API

Wondering if this perception could be backed by data, I decided to see if there were any interesting statistics to be found through [Codeforces' API](https://codeforces.com/apiHelp), using Python and lovely scientific packages like [pandas](https://pandas.pydata.org/), [numpy](https://numpy.org/), [scipy](https://www.scipy.org/) and [matplotlib](https://matplotlib.org/).

With [user.ratedList](https://codeforces.com/apiHelp/methods#user.ratedList) I gathered a list of all rated users, and with [user.rating](https://codeforces.com/apiHelp/methods#user.rating) I gathered every rating change data for each user. As a side note, I locally cached these responses to avoid making these 30k requests over and over again.

The code used for this can be found here: [CaioIcy/codeforces-analysis](https://github.com/CaioIcy/codeforces-analysis)

---
## Visualization

To understand if there was any merit to my initial hypothesis I plotted every user who had ever reached the [first division](https://codeforces.com/help#q8) (max rating >= 1900), with the x-axis being a user's maximum rating and the y-axis being the number of contests participated in order to reach div1 for the first time:

![scatter](https://thepracticaldev.s3.amazonaws.com/i/4jqlggjuigmh9la137s6.png)
<figcaption>Number of contests to reach div1 x Max rating</figcaption>

Interesting!

By glancing at the scatter plot there seems to be a correlation. Out of curiosity I searched for ways to measure just how correlated two variables really are, and landed on [Spearman's rank correlation coefficient](https://en.wikipedia.org/wiki/Spearman%27s_rank_correlation_coefficient). Using [scipy's spearmanr](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.spearmanr.html) we have about `-0.21` for a correlation coefficient which means there is an observable correlation, albeit moderate, as seen in the table below:

![Interpretation of correlation coeficient](https://thepracticaldev.s3.amazonaws.com/i/6c3wr70evj2zqypkff5f.png)
<figcaption>Reading the correlation coefficient. Excerpt from Nonparametric Statistics for Non-statisticians: A Step-by-Step Approach</figcaption>

To have another perspective on the data, I split the users into buckets based on their maximum rating to be able to visualize the data in a less cluttered way than the scatter plot:

![misc](https://thepracticaldev.s3.amazonaws.com/i/hfbwg6gv8jncvlxrgvvl.png)

----
## Conclusion

Indeed users of certain rating ranges had usually slightly better performances in their early contests when compared to lower rating ranges, but why? Well, I don't know! There could be a myriad of reasons, and I would like to hear what **you** think!

And remember, if you blasted through your early contests in Codeforces, it does not mean that you will have a breezy time moving forward, keep studying:

![xkcd](https://imgs.xkcd.com/comics/correlation.png)
<figcaption>Relevant XKCD</figcaption>

Thank you for reading!

----
### References

[Spearman's Rank-Order Correlation](https://statistics.laerd.com/statistical-guides/spearmans-rank-order-correlation-statistical-guide.php)  
[How to Calculate Nonparametric Rank Correlation in Python](https://machinelearningmastery.com/how-to-calculate-nonparametric-rank-correlation-in-python/)  
[Nonparametric Statistics for Non-statisticians: A Step-by-Step Approach](https://amzn.com/047045461X/)  
