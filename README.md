# STAT_433
---
title: "STAT_433_project1"
author: "Meng Luo"
date: "2021/9/20"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

## R Markdown

This is an R Markdown document. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>.

When you click the **Knit** button a document will be generated that includes both content as well as the output of any embedded R code chunks within the document. You can embed an R code chunk like this:

```{r cars}
summary(cars)
```

## Including Plots

You can also embed plots, for example:

```{r pressure, echo=FALSE}
plot(pressure)
install.packages("rvest")
install.packages("XML")
library(rvest) # 载入rvest包
library(stringr)
library(XML)

Murl = 'https://guide.wisc.edu/faculty/'
web = Murl %>% read_html(encoding="utf-8")  # utf-8
#use xpath to find the useful block
md4 = Murl %>% 
  read_html(encoding="utf-8") %>%
  html_nodes(xpath = '//ul[@class="uw-people"]')
#save
Nummd4 <- 1:26
for (i in Nummd4){
  print (i)
  md5 <- md4[i]
  # find each faculty
  People <- unlist(strsplit(md5, "</p></li>"))
  NumPeople <- 1:length(People)
  for (j in NumPeople){
    People1 = People[j]
    Peopleinfo <- unlist(strsplit(People1, "<br>"))
    Peopleinfotrans <- unlist(strsplit(Peopleinfo[1], "<p>"))
    Peopleinfo[1] <- Peopleinfotrans[2]
    Peopleinfo[5] <- LETTERS[i]
    if (i == 1 & j == 1){
      facultydata<-Peopleinfo
    }
    facultydata<-data.frame(facultydata,Peopleinfo)
  }
    
  
}
facultydata1<-t(facultydata1)
# plot

```

Note that the `echo = FALSE` parameter was added to the code chunk to prevent printing of the R code that generated the plot.
