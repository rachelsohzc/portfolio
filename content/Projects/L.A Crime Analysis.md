+++
title = "L.A Crime Analysis"
description = ""
type = ["posts","post"]
tags = [
    "Data Analysis",
    "Random Forests",
    "Logistic Regression",
    "Decision Trees",
    "R",
]
date = "2022-03-31"
categories = [
    "Data Analysis",
    "AI/ML",
]
+++

[THIS IS AN COMPLETED PROJECT](https://github.com/rachelsohzc/L.A-Crime-Analysis)

Predictive policing is becoming an important part for fair policing today. We wanted to find out if we could predict which areas would have crimes based on factors like victim’s age, sex, descent, premise types etc. using decision trees and logistic regression models. The final product of this projects was to find out which inputs heavily influence severe crimes in Los Angeles.

I used multiple methods to cross-check the predictors in this project. You can find some of the methods below:

### Random Forests

Random forests are typically used for classification and regression. Considering the fact that our expected output was either severe or not severe crime, I chose to use random forests:

```
{{ tree1 = tree(Severity ~., data = crime)
summary(tree1)
plot(tree1) }}
```

### Logistic regression

Logistic regression is a statistical model that is also often used for classification and predictive analysis. It returns a probability of an outcome happening, so the outcome is always bounded between 0 and 1.

```
{{ logistic.crime6=glm(Severity~VictAge+Female+Weapon+SFamDwelling+Street+MUDwelling+Parking+Sidewalk+Vehicle+UnderParking+Black+Hispanic+Morning+Day+Night+Central+South+West, data=traindatafinal,family=binomial)
summary(logistic.crime6)

logistic.crime7=glm(Severity~VictAge+Female+Weapon+SFamDwelling+Street+MUDwelling+Parking+Sidewalk+Vehicle+Black+Hispanic+Morning+Day+Night+Central+South+West, data=traindatafinal,family=binomial)
summary(logistic.crime7) }}
```

The iterations above are done to find the most optimal model by removing variables.

View the full project repository **[here](https://github.com/rachelsohzc/L.A-Crime-Analysis)**