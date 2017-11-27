# Case Study 2
Section 403, Group 5:  
    Gregory Asamoah  
    Emil Ramos  
    Brian Coari  
December 03, 2017  



## Introduction

[some text here]

## Installing Necessary Libraries

##Code Book

CODE BOOK

Data Set Code Book: Procrastination
November 25, 2017

The Procrastination csv data set contains 4264 observations and 61 variables



```r
#class(Procrastination)
#sapply(Procrastination, class)
#summary(Procrastination)
```

Install necessary packages if not installed:




## Clean your Raw Data


```r
# a Read the csv into R and take a look at the data set. Output how many rows and columns the data.frame is.

library(readr)
Procrastination <- read.csv(".\\Data\\Procrastination.csv",header=TRUE, sep=",", fileEncoding="UTF-8-BOM")

str(Procrastination)
```

```
## 'data.frame':	4264 obs. of  61 variables:
##  $ Age                                                                                                                     : num  67.5 45 19 37.5 28 23 67.5 37.5 24 45 ...
##  $ Gender                                                                                                                  : Factor w/ 3 levels "","Female","Male": 3 3 2 3 2 2 2 3 2 3 ...
##  $ Kids                                                                                                                    : Factor w/ 3 levels "","No Kids","Yes Kids": 3 3 2 3 2 2 2 2 2 3 ...
##  $ Edu                                                                                                                     : Factor w/ 9 levels "","deg","dip",..: 8 2 3 8 2 2 8 4 8 8 ...
##  $ Work.Status                                                                                                             : Factor w/ 7 levels "","0","full-time",..: 5 4 6 3 3 3 4 4 3 3 ...
##  $ Annual.Income                                                                                                           : int  25000 35000 NA 45000 35000 15000 NA 10000 250000 87500 ...
##  $ Current.Occupation                                                                                                      : Factor w/ 676 levels "","'Utterly shiftless arts student'... at p",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ How.long.have.you.held.this.position...Years                                                                            : num  9.0 1.5e-19 0.0 1.4e+01 1.0 ...
##  $ How.long.have.you.held.this.position...Months                                                                           : int  0 0 0 0 0 0 0 0 0 0 ...
##  $ Community.size                                                                                                          : Factor w/ 10 levels "","0","8","Large-City",..: 4 10 5 5 10 9 5 10 10 10 ...
##  $ Country.of.residence                                                                                                    : Factor w/ 94 levels "","0","Afghanistan",..: 31 15 25 26 26 26 60 88 88 73 ...
##  $ Marital.Status                                                                                                          : Factor w/ 7 levels "","0","Divorced",..: 3 4 6 4 6 6 3 6 6 4 ...
##  $ Number.of.sons                                                                                                          : Factor w/ 9 levels "","0","10","3",..: 2 9 2 2 2 2 2 2 2 8 ...
##  $ Number.of.daughters                                                                                                     : int  5 1 0 1 0 0 0 0 0 0 ...
##  $ X.DP.1..I.waste.a.lot.of.time.on.trivial.matters.before.getting.to.the.final.decisions                                  : int  3 3 5 3 3 3 3 4 2 5 ...
##  $ X.DP.2..Even.after.I.make.a.decision.I.delay.acting.upon.it                                                             : int  1 4 5 3 3 4 4 3 2 5 ...
##  $ X.DP.3..I.don.t.make.decisions.unless.I.really.have.to                                                                  : int  1 3 2 3 2 3 3 4 4 5 ...
##  $ X.DP.4..I.delay.making.decisions.until.it.s.too.late                                                                    : int  1 3 3 3 1 2 2 4 4 5 ...
##  $ X.DP.5..I.put.off.making.decisions.until.it.s.too.late                                                                  : int  1 3 3 3 1 2 2 3 4 5 ...
##  $ X.AIP.1..I.pay.my.bills.on.time                                                                                         : int  1 3 5 2 1 2 3 4 3 3 ...
##  $ X.AIP.2.I.am.prompt.and.on.time.for.most.appointments.                                                                  : int  1 1 4 1 1 5 1 4 3 3 ...
##  $ X.AIP.3.I.lay.out.my.clothes.the.night.before.I.have.an.important.appointment..so.I.won.t.be.late                       : int  1 4 4 4 3 5 1 4 3 5 ...
##  $ X.AIP.4..I.find.myself.running.later.than.I.would.like.to.be                                                            : int  1 3 5 3 3 5 2 4 4 3 ...
##  $ X.AIP.5..I.don.t.get.things.done.on.time                                                                                : int  1 3 5 5 2 5 3 4 4 5 ...
##  $ X.AIP.6..If.someone.were.teaching.a.course.on.how.to.get.things.done.on.time..I.would.attend                            : int  1 4 5 3 2 3 3 2 2 1 ...
##  $ X.AIP.7..My.friends.and.family.think.I.wait.until.the.last.minute.                                                      : int  1 3 5 4 2 5 1 5 2 5 ...
##  $ X.AIP.8..I.get.important.things.done.with.time.to.spare                                                                 : int  1 3 4 5 2 4 4 2 4 5 ...
##  $ X.AIP.9..I.am.not.very.good.at.meeting.deadlines                                                                        : int  5 3 5 4 1 4 5 4 2 5 ...
##  $ X.AIP.10..I.find.myself.running.out.of.time.                                                                            : int  1 3 5 5 1 5 5 3 2 5 ...
##  $ X.AIP.11..I.schedule.doctor.s.appointments.when.I.am.supposed.to.without.delay                                          : int  1 4 4 4 2 3 3 2 4 4 ...
##  $ X.AIP.12..I.am.more.punctual.than.most.people.I.know                                                                    : int  1 2 3 3 1 5 2 4 4 4 ...
##  $ X.AIP.13..I.do.routine.maintenance..e.g...changing.the.car.oil..on.things.I.own.as.often.as.I.should                    : int  1 2 5 4 2 4 3 3 4 4 ...
##  $ X.AIP.14.When.I.have.to.be.somewhere.at.a.certain.time.my.friends.expect.me.to.run.a.bit.late                           : int  1 2 4 2 1 5 1 4 3 4 ...
##  $ X.AIP.15.Putting.things.off.till.the.last.minute.has.cost.me.money.in.the.past                                          : int  3 4 3 1 2 5 4 5 3 5 ...
##  $ X.GP.1.I.often.find.myself.performing.tasks.that.I.had.intended.to.do.days.before                                       : int  1 4 5 4 4 5 4 5 3 5 ...
##  $ X.GP2..I.often.miss.concerts..sporting.events..or.the.like.because.I.don.t.get.around.to.buying.tickets.on.time         : int  1 2 2 1 1 5 1 1 4 3 ...
##  $ X.GP.3..When.planning.a.party..I.make.the.necessary.arrangements.well.in.advance                                        : int  1 2 2 3 2 2 1 3 3 3 ...
##  $ X.GP.4..When.it.is.time.to.get.up.in.the.morning..I.most.often.get.right.out.of.bed                                     : int  1 2 4 3 4 5 1 4 4 1 ...
##  $ X.GP.5..A.letter.may.sit.for.days.after.I.write.it.before.mailing.it.possible                                           : int  1 2 3 2 5 4 1 3 2 5 ...
##  $ X.GP.6..I.generally.return.phone.calls.promptly                                                                         : int  1 2 1 3 2 4 2 3 2 5 ...
##  $ X.GP.7..Even.jobs.that.require.little.else.except.sitting.down.and.doing.them..I.find.that.they.seldom.get.done.for.days: int  1 4 3 4 4 5 3 4 4 5 ...
##  $ X.GP.8..I.usually.make.decisions.as.soon.as.possible                                                                    : int  1 2 2 5 2 4 2 3 2 4 ...
##  $ X.GP.9..I.generally.delay.before.starting.on.work.I.have.to.do                                                          : int  1 4 5 4 4 4 4 4 4 5 ...
##  $ X.GP.10..When.traveling..I.usually.have.to.rush.in.preparing.to.arrive.at.the.airport.or.station.at.the.appropriate.time: int  1 2 4 1 1 3 1 4 1 3 ...
##  $ X.GP.11..When.preparing.to.go.out..I.am.seldom.caught.having.to.do.something.at.the.last.minute                         : int  5 3 5 3 2 4 4 3 5 5 ...
##  $ X.GP.12..In.preparation.for.some.deadlines..I.often.waste.time.by.doing.other.things                                    : int  1 4 5 4 3 4 2 5 2 5 ...
##  $ X.GP.13..If.a.bill.for.a.small.amount.comes..I.pay.it.right.away                                                        : int  1 2 3 3 2 3 3 2 3 4 ...
##  $ X.GP.14..I.usually.return.a..RSVP..request.very.shortly.after.receiving.it                                              : int  1 2 4 3 4 4 2 2 2 4 ...
##  $ X.GP.15..I.often.have.a.task.finished.sooner.than.necessary                                                             : int  1 3 5 4 3 4 4 4 1 4 ...
##  $ X.GP.16..I.always.seem.to.end.up.shopping.for.birthday.gifts.at.the.last.minute                                         : int  1 4 2 4 2 4 3 4 5 5 ...
##  $ X.GP.17..I.usually.buy.even.an.essential.item.at.the.last.minute                                                        : int  1 3 3 3 3 4 1 3 5 3 ...
##  $ X.GP.18..I.usually.accomplish.all.the.things.I.plan.to.do.in.a.day                                                      : int  5 3 5 4 2 4 4 4 1 5 ...
##  $ X.GP.19..I.am.continually.saying..I.ll.do.it.tomorrow.                                                                  : int  1 4 5 5 3 4 4 4 1 5 ...
##  $ X.GP.20..I.usually.take.care.of.all.the.tasks.I.have.to.do.before.I.settle.down.and.relax.for.the.evening               : int  5 4 4 1 4 4 2 4 3 5 ...
##  $ X.SWLS.1..In.most.ways.my.life.is.close.to.my.ideal                                                                     : int  5 3 2 2 4 3 3 3 4 1 ...
##  $ X.SWLS.2.The.conditions.of.my.life.are.excellent                                                                        : int  5 4 2 4 4 2 4 3 4 4 ...
##  $ X.SWLS.3..I.am.satisfied.with.my.life.                                                                                  : int  5 4 2 2 4 4 3 3 5 2 ...
##  $ X.SWLS.4..So.far.I.have.gotten.the.important.things.I.want.in.life                                                      : int  5 4 3 2 3 4 3 2 4 4 ...
##  $ X.SWLS.5..If.I.could.live.my.life.over..I.would.change.almost.nothing                                                   : int  5 3 4 2 4 3 2 3 4 1 ...
##  $ Do.you.consider.yourself.a.procrastinator.                                                                              : Factor w/ 3 levels "","no","yes": 2 3 3 3 2 3 3 3 2 3 ...
##  $ Do.others.consider.you.a.procrastinator.                                                                                : Factor w/ 5 levels "","0","4","no",..: 4 5 5 5 4 5 5 5 4 5 ...
```

```r
# checking for Null values in the data set

anyNA(Procrastination)
```

```
## [1] TRUE
```

```r
# b The column names are either too much or not enough. Change the column names so that they do not have spaces, underscores, slashes, and the like. All column names should be under 12 characters. Make sure you're updating your codebook with information on the tidied data set as well.


# c Some columns are, due to Qualtrics, malfunctioning. Prime examples are the following columns: "How long have you held this position?: Years", Country of residence, Number of sons, and Current Occupation.

# i Some have impossible data values. Detail what you are doing to fix these columns in the raw data and why. It's a judgment call for each, but explain why. For example, most people have not been doing anything for over 100 years. For the "Years" columns, round to the nearest integer.

# ii Somehow, "Number of sons" was labeled with Male (1) and Female (2). Change these incorrect labels back to integers.

# iii There are no "0" country of residences. Treat this as missing.

# iv Current Occupation has no "please specify" or "0." Treat them as missing. Some jobs are quite similar. Use judgment calls to make overwrite them into the same category. It does not have to be 100% accurate, but right now "ESL Teacher" would not be counted as "teacher" if there were unique counts.


# d Make sure your columns are the proper data types (i.e., numeric, character, etc.). If they are incorrect, convert them.


# e Each variable that starts with either DP, AIP, GP, or SWLS is an individual item on a scale. For example, DP 1 through DP 5 are five different questions on the Decision Procrastination Scale. I've reverse-scored them for you already, but you should create a new column for each of them with their mean. To clarify, you'll need a DPMean column, an AIPMean column, a GPMean column, and a SWLSMean column. This represents the individual's average decisional procrastination (DP), procrastination behavior (AIP), generalized procrastination (GP), and life satisfaction (SWLS).
```


## Scrape the Human Development Index tables online



```r
# (https://en.wikipedia.org/wiki/List_of_countries_by_Human_Development_Index#Complete_list_of_countries). Read what it is, because you'll have to explain it to your clients. BIG TIP: This one's going to be weird looking-it's real scraping. Make sure you're looking between the webpage and R while you do this to find your footing. Unit 9's HW might help.

# a You will notice there are several sections, but you should only worry about the Complete List of Countries section of this Wikipedia entry. There are 8 tables in this section, but you should pull these eight, clean them as to be usable, and then find a way to bind them into one singular table. You only need Country and 2016 Estimates for 2015 (you can call this HDI) columns for the final table.
library('xml2')
library('rvest')
library('dplyr')
library('tidyr')

url <- 'https://en.wikipedia.org/wiki/List_of_countries_by_Human_Development_Index#Complete_list_of_countries'

#Read the webpage from the URL
hdiWebpage <- read_html(url)

#Grab all the table nodes from the page
hdiNodes <- html_nodes(hdiWebpage, "table")

#Convert the nodes to HTML tables
hdiTables <- html_table(hdiNodes, fill=TRUE)

#trial and error to find the right 8 tables
hdiDataFrame1 <- data.frame(hdiTables[4])
hdiDataFrame2 <- data.frame(hdiTables[5])
hdiDataFrame3 <- data.frame(hdiTables[7])
hdiDataFrame4 <- data.frame(hdiTables[8])
hdiDataFrame5 <- data.frame(hdiTables[10])
hdiDataFrame6 <- data.frame(hdiTables[11])
hdiDataFrame7 <- data.frame(hdiTables[13])
hdiDataFrame8 <- data.frame(hdiTables[14])

#The first data frame calls the Country field "Country.Territory", but the other 7 call this column "Country"
#Changing the first data frame for consistency and easy binding
colnames(hdiDataFrame1)[colnames(hdiDataFrame1)=="Country.Territory"] <- "Country"

#binding all of the data frames
hdiDataFrame_all <- bind_rows(hdiDataFrame1,hdiDataFrame2,hdiDataFrame3,hdiDataFrame4,hdiDataFrame5,hdiDataFrame6,hdiDataFrame7,hdiDataFrame8)

#Removing all header rows from the table, header rows all store the name "Rank" in the Rank.1 field
hdiDataFrame_all <- hdiDataFrame_all[which(hdiDataFrame_all$Rank.1 != "Rank"),]

#Removing all but the necessary "Country" and "HDI" fields
hdiDataFrame_all$Rank <- NULL
hdiDataFrame_all$Rank.1 <- NULL
hdiDataFrame_all$HDI.1 <- NULL

#converting HDI to numeric since it fits the data better than chr
hdiDataFrame_all$HDI <- as.numeric(hdiDataFrame_all$HDI)

# b Create a new column for this final scraped table which categories the Countries like the original page (Very high human development, High human development, Medium human development, Low human development). After these categories, output a csv file of this table to your repository.

#Initializing the new column to "Unknown"
hdiDataFrame_all$Development.Category <- "Unknown"

#Classifying the new variable based on the value of HDI
#Any Country with an HDI of between .8 and 1, inclusive, is considered "Very high human development"
hdiDataFrame_all$Development.Category[which(hdiDataFrame_all$HDI >= .8 & hdiDataFrame_all$HDI <= 1)] <- "Very high human development"

#Any Country with an HDI of between .7 inclusive and .8 exclusive is considered "High human development"
hdiDataFrame_all$Development.Category[which(hdiDataFrame_all$HDI >= .7 & hdiDataFrame_all$HDI < .8)] <- "High human development"

#Any Country with an HDI of between .55 inclusive and .7 exclusive is considered "Medium human development"
hdiDataFrame_all$Development.Category[which(hdiDataFrame_all$HDI >= .55 & hdiDataFrame_all$HDI < .7)] <- "Medium human development"

#Any Country with an HDI of between 0 inclusive and .55 exclusive is considered "Low human development"
hdiDataFrame_all$Development.Category[which(hdiDataFrame_all$HDI >= 0 & hdiDataFrame_all$HDI < .55)] <- "Low human development"
  
  
# c Merge this data frame to the Country of Residence column of Procrastination.csv so that your data now has an HDI column and HDI categories (Very high human development, etc.).

#After the first merge and verification, these countries did not have a match:
# Antigua (Corrected by renaming "Antigua and Barbuda" to "Antigua" in the merged HDI data)
# Bermuda
# Columbia
# Guam
# Isreal (Corrected with renaming to "Israel" below, the proper spelling)
# Macao
# Puerto Rico
# Taiwan
# Yugoslavia


#These 5 lines could go in data cleanup:
Procrastination <- Procrastination[which(Procrastination$Country.of.residence != ""),]
Procrastination <- Procrastination[which(Procrastination$Country.of.residence != "0"),]
Procrastination <- Procrastination[which(!is.na(Procrastination$Country.of.residence)),]
#changed to match merged HDI data
Procrastination$Country.of.residence[which(Procrastination$Country.of.residence == "Isreal")] <- "Israel"

#changed to match Procrastination
hdiDataFrame_all$Country[which(hdiDataFrame_all$Country == "Antigua and Barbuda")] <- "Antigua"

#Merge the data and keep all Procrastination, even if there is no match for HDI Data. We can revisit this later if it causes problems
ProcrastinationHdiData <- merge(Procrastination,hdiDataFrame_all,by.x = "Country.of.residence", by.y = "Country",all.x=TRUE)

ProcrastinationHdiDataErrors <- ProcrastinationHdiData[which(is.na(ProcrastinationHdiData$HDI)),]

#Rows with these countries listed in ProcrastinationData still have NA for their HDI scores and categories, and I am not sure what to do about it since they are legitimately not countries for which HDI is listed on this page for 2016:
# Bermuda
# Columbia
# Guam
# Macao
# Puerto Rico
# Taiwan
# Yugoslavia
```


## Preliminary Analysis


```r
# a Remove all observations where the participant is under age 18. No further analysis of underage individuals is permitted by your client. Remove any other age outliers as you see fit, but be sure to tell what you're doing and why.


# b Please provide (in pretty-fied table format or similar), descriptive statistics on Age, Income, HDI, and the four mean columns (DP, etc.). Create a simple histogram for two of these seven variables. Comment on the shape of the distribution in your markdown.


# c Give the frequencies (in table format or similar) for Gender, Work Status, and Occupation. They can be separate tables, if that's your choice.


# d Give the counts (again, pretty table) of how many participants per country in descending order.


# e There are two variables in the set: whether the person considers themselves a procrastinator (yes/no) and whether others consider them a procrastinator (yes/no). How many people matched their perceptions to others' (so, yes/yes and no/no)? To clarify: how many people said they felt they were procrastinators and also said others thought they were procrastinators? Likewise, how many said they were not procrastinators and others also did not think they were procrastinators?
```

## Deeper Analysis and Visualization


```r
# a Note: You should make all of these appealing looking. Remember to include things like a clean, informative title, axis labels that are in plain English, and readable axis values that do not overlap.


# b Create a barchart in ggplot or similar which displays the top 15 nations in average procrastination scores, using one measure of the following: DP, AIP, or GP. The bars should be in descending order, with the number 1 most procrastinating nation at the top and 15th most procrastinating at the bottom. Omit all other nations. Color the bars by HDI category (see 3B). Use any color palette of your choice other than the default.


# c Create another barchart identical in features to 5B, but use another one of the three variables: DP, AIP, or GP. How many nations show up both in 5B's plot and 5C's? Which, if any?


# d Is there a relationship between Age and Income? Create a scatterplot and make an assessment of whether there is a relationship. Color each point based on the Gender of the participant. You're welcome to use lm() or similar functions to back up your claims.


# e What about Life Satisfaction and HDI? Create another scatterplot. Is there a discernible relationship there? What about if you used the HDI category instead and made a barplot?
```

## Outputting to CSV format - Make sure there are no index numbers


```r
# a The client would like the finalized HDI table (3A and 3B)


# b The client would like the Tidied version of the original input to be output in the repository, including the merged HDI data (3C).


# c The client would like a dataset (or two) that shows the Top 15 nations (in 5B and 5C), as well as their HDI scores.


# d All output should be in plain English or translated in the Codebook.
```

## Conclusion
