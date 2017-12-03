# CaseStudy2-Repo

#Introduction

Procrastination can basically be defined as the action of delaying  or postponing task that needs to be done.It's an inevitable part of human life and our various daily activities that are time bound. It has implications for performance, prevents you from meeting deadlines, can lead to disorganization and becomes the major reason for  failure on time bound projects and daily life activities.
We have finally finished data collection and it involved various measures of procrastination and the qualities of individuals in the sample.
The dataset included 4264 observations and 16 variables from the United States. The main outcome of this study is the empirical results on procrastination from  a data set of human task and activities using data analytics technique and a tool called R and Rstudio

The outcome and result of this study can help support actions that can lead to improve performance in daily task and activities, aid in meeting deadlines, lead to better organization and becomes the framework or model for success on various daily task and human activities.

The paper outlined the various codes used in  R and Rstudio in  cleaning the procrastination data set, the analysis and the results presented, including a visualization illustrations of the procrastination data set in an HTML and pushed to GitHub.

The paper closes with conclusions and implications of procrastination.


#Company

Name  of the organization




#Motivation

The reason behind delying activities and task that have to be done and their impilcations



#Installation

{r CaseStudy_2_1.R, eval=TRUE, echo=TRUE, message = FALSE, warning = FALSE}
# Find all packages that are not in the list of installed packages and install packages used if not yet installed
list.of.packages <- c('xml2','rvest', 'dplyr', 'tidyr', 'DT','readr', 'ggplot2')
new.packages <- list.of.packages[!(list.of.packages %in% installed.packages()[,"Package"])]
if(length(new.packages)) install.packages(new.packages)


library('xml2')
library('rvest')
library('dplyr')
library('tidyr')
library('DT')
library('readr')
library('ggplot2')


#API Reference
R for Data Science by Garrett Grolemund and Hadley Wickham

Automated Data Collection with R: A practical Guide to Web Scraping and Text Mining
by Simon Munzert, Christian Rubba, Peter Meissner, Dominnic Nyhuis

An Introduction to APIs by Zapier



#Contributors

Gregory Asamoah

Emil Ramos

Brian Coari

#Contact Information

Gregory Asamoah:gasamoah@mail.smu.edu

Emil Ramos:emilr@mail.smu.edu

Brian Coari:bcoari@mail.smu.edu


#Session Information

MSDS 6306 DOING DATA SCIENCE, Section 403


