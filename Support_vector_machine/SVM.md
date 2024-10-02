# Exploreation SVM for classification


```{r setup, include=FALSE}
library(readr)
library(maptools)
library(ggplot2)
library(raster)
library(psych)
library(gmodels)
library(FactoMineR) #library for conducting PCA
library(factoextra) # library for plotting PCA
library(missMDA) #for imputing if you have missing data
library(hyperoverlap)
library(Rmisc)
library(car)
library(dplyr)
library(ggplot2)
library(MuMIn)
library(drc)
library(rcompanion)
library(nlstools)
library(kernlab)

```

## 1.	Import the data
```{r}
df <- read.csv("Dry_Bean_Dataset.csv")
head(df)
str(df)
summary(df)
df$Class=as.factor(df$Class)

```

## 2. Subset data for creating hyperplanes:
```{r}
ggplot(data=df,mapping=aes(x=Area,y=Eccentricity ,color=Class)) +
  geom_point() +
  theme_bw()+
  labs(title="Area x Eccentricity") +
  xlab("Area") +
  ylab("Eccentricity")

```
##3. Fit the SVM
```{r}
##  Setting default kernel parameters

library(e1071)
x <- df[,-1]
y <- df[,1]
model_svm <- svm(Class ~ ., data=df)
summary(model_svm)

pred <- predict(model_svm,x)
library(caret)
confusionMatrix(pred,y)


```


## R Markdown

This is an R Markdown document. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>.
