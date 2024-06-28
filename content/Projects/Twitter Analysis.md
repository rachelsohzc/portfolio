+++
title = "Twitter Analysis"
description = ""
type = ["posts","post"]
tags = [
    "APIs",
    "Data Prep",
    "Visualisation",
    "Data Analysis",
]
date = "2022-06-12"
categories = [
    "Data Analysis",
]
+++

[THIS IS A COMPLETED PROJECT](https://github.com/rachelsohzc/Twitter-Analytics)

Given how most events moved online during COVID-19, having a strong digital presence is a huge advantage for organisations. Therefore, in this project, I’ve decided to find out whether Twitter is a good social media platform for departments at the LSE. This was an academic project.

You can find some main features and code of this project below:

### Data Collection

A mix of Twitter APIs and web scraping were used to collect information about departments at LSE. The process was iterative with the concept of authenticating yourself, and then making an API call:

```
{{ with open('keys.json') as f:
keys = json.load(f)

bearer_token = keys['twitter']['bearer_token']
headers = {
'Authorization': f"Bearer {bearer_token}"
}

r = requests.get('https://api.twitter.com/2/users/by?usernames=LSE_Accounting,LSEAnthropology,LSEEcon,LSEEcHist,LSEfinance,LSEGenderTweet,LSEGeography,LSEGovernment,LSEHealthPolicy,LSE_ID,lsehistory,LSEIRDept,lselangcentre,LSELaw,LSEManagement,LSEMaths,MediaLSE,MethodologyLSE,LSEPhilosophy,LSEBehavioural,LSESocialPolicy,LSEsociology,LSEStatistics&user.fields=public_metrics', headers=headers)
r.text }}

```

### Data Visualisation

The scope of data visualisation has no limits. I picked a few cases that I saw relevant like sentiment analysis:

```
{{ def Subjectivity(tweet):
return TextBlob(tweet).sentiment.subjectivity

def Polarity(tweet):
return TextBlob(tweet).sentiment.polarity }}
```

and what kind of accounts interact with the departments, through a network diagram:

```
{{ g = nx.Graph()
for i in range(0, len(mentions)):
g.add_edge(mentions['User ID'][i], mentions['Department'][i])
plt.figure(3,figsize=(16,20))
nx.draw(g, with_labels = False, node_color = 'skyblue',
   node_shape = 'o', alpha = 0.5) }}
```

View the full project repository **[here](https://github.com/rachelsohzc/Twitter-Analytics)**