# Case Study 2
Section 403, Group 5:  
    Gregory Asamoah  
    Emil Ramos  
    Brian Coari  
December 03, 2017  

#Install necessary packages if not installed:


```r
# Find all packages that are not in the list of installed packages and install packages used if not yet installed
list.of.packages <- c('xml2','rvest', 'dplyr', 'tidyr', 'DT','readr', 'ggplot2','plyr','reshape2')
new.packages <- list.of.packages[!(list.of.packages %in% installed.packages()[,"Package"])]
if(length(new.packages)) install.packages(new.packages)

library('xml2')
library('rvest')
library('dplyr')
library('tidyr')
library('DT')
library('readr')
library('ggplot2')
library('reshape2')
library('plyr')
```

## Introduction

Greetings Nintendo Marketing Team,

Our company, LazyLife Inc., is an expert an analyzing procrastination data and Life Satisfaction statistics for countries across the world. We have access to thousands of observations that give us insight into who in world considers themselves a procrastinator, and who is satisfied with their life. LazyLife Inc. differentiates itself from our competition by also including exerpts from the Human Development Index (HDI) to see which countries are happy, lazy, and developed.

Procrastination can basically be defined as the action of delaying  or postponing task that needs to be done. It's an inevitable part of human life and our various daily activities that are time bound. It has implications for performance, prevents you from meeting deadlines, can lead to disorganization and becomes the major reason for  failure on time bound projects and daily life activities. However, during this procrastination, what are people doing? I'll tell you what I'm doing... playing Nintendo!  

We believe that by leveraging our data, Nintendo will be able to target the laziest and most developed countries in order to get the most value for your marketing dollars. In addition, adding in life satisfaction will assure you that your customers are happy, wealthy, lazy, and ready to consume. This is what we feel is your ideal market, and will allow your product to thrive in perhaps new and lucrative markets.

If you purchase the results of our analysis we will provide you with quarterly updates on these markets so you can adjust and continue to be most effective in your marketing and advertising.

Thank you,

Brian Coari, Gergory Asamoah, and Emil Ramos

LazyLife Inc.

Email: datascience@lazylife.com

Phone: (555) 867-5309


##Code Book for the raw Data

#CODE BOOK

#Data Set Code Book: Procrastination
#November 25, 2017

#The Procrastination csv data set contains 4264 observations and 61 variables



```r
stringsAsFactors=FALSE

Procrastination_Raw_Data <- read.csv(".\\Data\\Procrastination.csv",header=TRUE, sep=",", fileEncoding="UTF-8-BOM")

#class(Procrastination_Raw_Data)
sapply(Procrastination_Raw_Data, class)
```

```
##                                                                                                                      Age 
##                                                                                                                "numeric" 
##                                                                                                                   Gender 
##                                                                                                                 "factor" 
##                                                                                                                     Kids 
##                                                                                                                 "factor" 
##                                                                                                                      Edu 
##                                                                                                                 "factor" 
##                                                                                                              Work.Status 
##                                                                                                                 "factor" 
##                                                                                                            Annual.Income 
##                                                                                                                "integer" 
##                                                                                                       Current.Occupation 
##                                                                                                                 "factor" 
##                                                                             How.long.have.you.held.this.position...Years 
##                                                                                                                "numeric" 
##                                                                            How.long.have.you.held.this.position...Months 
##                                                                                                                "integer" 
##                                                                                                           Community.size 
##                                                                                                                 "factor" 
##                                                                                                     Country.of.residence 
##                                                                                                                 "factor" 
##                                                                                                           Marital.Status 
##                                                                                                                 "factor" 
##                                                                                                           Number.of.sons 
##                                                                                                                 "factor" 
##                                                                                                      Number.of.daughters 
##                                                                                                                "integer" 
##                                   X.DP.1..I.waste.a.lot.of.time.on.trivial.matters.before.getting.to.the.final.decisions 
##                                                                                                                "integer" 
##                                                              X.DP.2..Even.after.I.make.a.decision.I.delay.acting.upon.it 
##                                                                                                                "integer" 
##                                                                   X.DP.3..I.don.t.make.decisions.unless.I.really.have.to 
##                                                                                                                "integer" 
##                                                                     X.DP.4..I.delay.making.decisions.until.it.s.too.late 
##                                                                                                                "integer" 
##                                                                   X.DP.5..I.put.off.making.decisions.until.it.s.too.late 
##                                                                                                                "integer" 
##                                                                                          X.AIP.1..I.pay.my.bills.on.time 
##                                                                                                                "integer" 
##                                                                   X.AIP.2.I.am.prompt.and.on.time.for.most.appointments. 
##                                                                                                                "integer" 
##                        X.AIP.3.I.lay.out.my.clothes.the.night.before.I.have.an.important.appointment..so.I.won.t.be.late 
##                                                                                                                "integer" 
##                                                             X.AIP.4..I.find.myself.running.later.than.I.would.like.to.be 
##                                                                                                                "integer" 
##                                                                                 X.AIP.5..I.don.t.get.things.done.on.time 
##                                                                                                                "integer" 
##                             X.AIP.6..If.someone.were.teaching.a.course.on.how.to.get.things.done.on.time..I.would.attend 
##                                                                                                                "integer" 
##                                                       X.AIP.7..My.friends.and.family.think.I.wait.until.the.last.minute. 
##                                                                                                                "integer" 
##                                                                  X.AIP.8..I.get.important.things.done.with.time.to.spare 
##                                                                                                                "integer" 
##                                                                         X.AIP.9..I.am.not.very.good.at.meeting.deadlines 
##                                                                                                                "integer" 
##                                                                             X.AIP.10..I.find.myself.running.out.of.time. 
##                                                                                                                "integer" 
##                                           X.AIP.11..I.schedule.doctor.s.appointments.when.I.am.supposed.to.without.delay 
##                                                                                                                "integer" 
##                                                                     X.AIP.12..I.am.more.punctual.than.most.people.I.know 
##                                                                                                                "integer" 
##                     X.AIP.13..I.do.routine.maintenance..e.g...changing.the.car.oil..on.things.I.own.as.often.as.I.should 
##                                                                                                                "integer" 
##                            X.AIP.14.When.I.have.to.be.somewhere.at.a.certain.time.my.friends.expect.me.to.run.a.bit.late 
##                                                                                                                "integer" 
##                                           X.AIP.15.Putting.things.off.till.the.last.minute.has.cost.me.money.in.the.past 
##                                                                                                                "integer" 
##                                        X.GP.1.I.often.find.myself.performing.tasks.that.I.had.intended.to.do.days.before 
##                                                                                                                "integer" 
##          X.GP2..I.often.miss.concerts..sporting.events..or.the.like.because.I.don.t.get.around.to.buying.tickets.on.time 
##                                                                                                                "integer" 
##                                         X.GP.3..When.planning.a.party..I.make.the.necessary.arrangements.well.in.advance 
##                                                                                                                "integer" 
##                                      X.GP.4..When.it.is.time.to.get.up.in.the.morning..I.most.often.get.right.out.of.bed 
##                                                                                                                "integer" 
##                                            X.GP.5..A.letter.may.sit.for.days.after.I.write.it.before.mailing.it.possible 
##                                                                                                                "integer" 
##                                                                          X.GP.6..I.generally.return.phone.calls.promptly 
##                                                                                                                "integer" 
## X.GP.7..Even.jobs.that.require.little.else.except.sitting.down.and.doing.them..I.find.that.they.seldom.get.done.for.days 
##                                                                                                                "integer" 
##                                                                     X.GP.8..I.usually.make.decisions.as.soon.as.possible 
##                                                                                                                "integer" 
##                                                           X.GP.9..I.generally.delay.before.starting.on.work.I.have.to.do 
##                                                                                                                "integer" 
## X.GP.10..When.traveling..I.usually.have.to.rush.in.preparing.to.arrive.at.the.airport.or.station.at.the.appropriate.time 
##                                                                                                                "integer" 
##                          X.GP.11..When.preparing.to.go.out..I.am.seldom.caught.having.to.do.something.at.the.last.minute 
##                                                                                                                "integer" 
##                                     X.GP.12..In.preparation.for.some.deadlines..I.often.waste.time.by.doing.other.things 
##                                                                                                                "integer" 
##                                                         X.GP.13..If.a.bill.for.a.small.amount.comes..I.pay.it.right.away 
##                                                                                                                "integer" 
##                                               X.GP.14..I.usually.return.a..RSVP..request.very.shortly.after.receiving.it 
##                                                                                                                "integer" 
##                                                              X.GP.15..I.often.have.a.task.finished.sooner.than.necessary 
##                                                                                                                "integer" 
##                                          X.GP.16..I.always.seem.to.end.up.shopping.for.birthday.gifts.at.the.last.minute 
##                                                                                                                "integer" 
##                                                         X.GP.17..I.usually.buy.even.an.essential.item.at.the.last.minute 
##                                                                                                                "integer" 
##                                                       X.GP.18..I.usually.accomplish.all.the.things.I.plan.to.do.in.a.day 
##                                                                                                                "integer" 
##                                                                   X.GP.19..I.am.continually.saying..I.ll.do.it.tomorrow. 
##                                                                                                                "integer" 
##                X.GP.20..I.usually.take.care.of.all.the.tasks.I.have.to.do.before.I.settle.down.and.relax.for.the.evening 
##                                                                                                                "integer" 
##                                                                      X.SWLS.1..In.most.ways.my.life.is.close.to.my.ideal 
##                                                                                                                "integer" 
##                                                                         X.SWLS.2.The.conditions.of.my.life.are.excellent 
##                                                                                                                "integer" 
##                                                                                   X.SWLS.3..I.am.satisfied.with.my.life. 
##                                                                                                                "integer" 
##                                                       X.SWLS.4..So.far.I.have.gotten.the.important.things.I.want.in.life 
##                                                                                                                "integer" 
##                                                    X.SWLS.5..If.I.could.live.my.life.over..I.would.change.almost.nothing 
##                                                                                                                "integer" 
##                                                                               Do.you.consider.yourself.a.procrastinator. 
##                                                                                                                 "factor" 
##                                                                                 Do.others.consider.you.a.procrastinator. 
##                                                                                                                 "factor"
```

```r
#summary(Procrastination_Raw_Data)
```


## Clean your Raw Data


```r
# a Read the csv into R and take a look at the data set. Output how many rows and columns the data.frame is.

str(Procrastination_Raw_Data)
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
anyNA(Procrastination_Raw_Data)
```

```
## [1] TRUE
```

```r
#view its class
class(Procrastination_Raw_Data)
```

```
## [1] "data.frame"
```

```r
# View its dimension
dim(Procrastination_Raw_Data)
```

```
## [1] 4264   61
```

```r
# look at the column names
names(Procrastination_Raw_Data)
```

```
##  [1] "Age"                                                                                                                     
##  [2] "Gender"                                                                                                                  
##  [3] "Kids"                                                                                                                    
##  [4] "Edu"                                                                                                                     
##  [5] "Work.Status"                                                                                                             
##  [6] "Annual.Income"                                                                                                           
##  [7] "Current.Occupation"                                                                                                      
##  [8] "How.long.have.you.held.this.position...Years"                                                                            
##  [9] "How.long.have.you.held.this.position...Months"                                                                           
## [10] "Community.size"                                                                                                          
## [11] "Country.of.residence"                                                                                                    
## [12] "Marital.Status"                                                                                                          
## [13] "Number.of.sons"                                                                                                          
## [14] "Number.of.daughters"                                                                                                     
## [15] "X.DP.1..I.waste.a.lot.of.time.on.trivial.matters.before.getting.to.the.final.decisions"                                  
## [16] "X.DP.2..Even.after.I.make.a.decision.I.delay.acting.upon.it"                                                             
## [17] "X.DP.3..I.don.t.make.decisions.unless.I.really.have.to"                                                                  
## [18] "X.DP.4..I.delay.making.decisions.until.it.s.too.late"                                                                    
## [19] "X.DP.5..I.put.off.making.decisions.until.it.s.too.late"                                                                  
## [20] "X.AIP.1..I.pay.my.bills.on.time"                                                                                         
## [21] "X.AIP.2.I.am.prompt.and.on.time.for.most.appointments."                                                                  
## [22] "X.AIP.3.I.lay.out.my.clothes.the.night.before.I.have.an.important.appointment..so.I.won.t.be.late"                       
## [23] "X.AIP.4..I.find.myself.running.later.than.I.would.like.to.be"                                                            
## [24] "X.AIP.5..I.don.t.get.things.done.on.time"                                                                                
## [25] "X.AIP.6..If.someone.were.teaching.a.course.on.how.to.get.things.done.on.time..I.would.attend"                            
## [26] "X.AIP.7..My.friends.and.family.think.I.wait.until.the.last.minute."                                                      
## [27] "X.AIP.8..I.get.important.things.done.with.time.to.spare"                                                                 
## [28] "X.AIP.9..I.am.not.very.good.at.meeting.deadlines"                                                                        
## [29] "X.AIP.10..I.find.myself.running.out.of.time."                                                                            
## [30] "X.AIP.11..I.schedule.doctor.s.appointments.when.I.am.supposed.to.without.delay"                                          
## [31] "X.AIP.12..I.am.more.punctual.than.most.people.I.know"                                                                    
## [32] "X.AIP.13..I.do.routine.maintenance..e.g...changing.the.car.oil..on.things.I.own.as.often.as.I.should"                    
## [33] "X.AIP.14.When.I.have.to.be.somewhere.at.a.certain.time.my.friends.expect.me.to.run.a.bit.late"                           
## [34] "X.AIP.15.Putting.things.off.till.the.last.minute.has.cost.me.money.in.the.past"                                          
## [35] "X.GP.1.I.often.find.myself.performing.tasks.that.I.had.intended.to.do.days.before"                                       
## [36] "X.GP2..I.often.miss.concerts..sporting.events..or.the.like.because.I.don.t.get.around.to.buying.tickets.on.time"         
## [37] "X.GP.3..When.planning.a.party..I.make.the.necessary.arrangements.well.in.advance"                                        
## [38] "X.GP.4..When.it.is.time.to.get.up.in.the.morning..I.most.often.get.right.out.of.bed"                                     
## [39] "X.GP.5..A.letter.may.sit.for.days.after.I.write.it.before.mailing.it.possible"                                           
## [40] "X.GP.6..I.generally.return.phone.calls.promptly"                                                                         
## [41] "X.GP.7..Even.jobs.that.require.little.else.except.sitting.down.and.doing.them..I.find.that.they.seldom.get.done.for.days"
## [42] "X.GP.8..I.usually.make.decisions.as.soon.as.possible"                                                                    
## [43] "X.GP.9..I.generally.delay.before.starting.on.work.I.have.to.do"                                                          
## [44] "X.GP.10..When.traveling..I.usually.have.to.rush.in.preparing.to.arrive.at.the.airport.or.station.at.the.appropriate.time"
## [45] "X.GP.11..When.preparing.to.go.out..I.am.seldom.caught.having.to.do.something.at.the.last.minute"                         
## [46] "X.GP.12..In.preparation.for.some.deadlines..I.often.waste.time.by.doing.other.things"                                    
## [47] "X.GP.13..If.a.bill.for.a.small.amount.comes..I.pay.it.right.away"                                                        
## [48] "X.GP.14..I.usually.return.a..RSVP..request.very.shortly.after.receiving.it"                                              
## [49] "X.GP.15..I.often.have.a.task.finished.sooner.than.necessary"                                                             
## [50] "X.GP.16..I.always.seem.to.end.up.shopping.for.birthday.gifts.at.the.last.minute"                                         
## [51] "X.GP.17..I.usually.buy.even.an.essential.item.at.the.last.minute"                                                        
## [52] "X.GP.18..I.usually.accomplish.all.the.things.I.plan.to.do.in.a.day"                                                      
## [53] "X.GP.19..I.am.continually.saying..I.ll.do.it.tomorrow."                                                                  
## [54] "X.GP.20..I.usually.take.care.of.all.the.tasks.I.have.to.do.before.I.settle.down.and.relax.for.the.evening"               
## [55] "X.SWLS.1..In.most.ways.my.life.is.close.to.my.ideal"                                                                     
## [56] "X.SWLS.2.The.conditions.of.my.life.are.excellent"                                                                        
## [57] "X.SWLS.3..I.am.satisfied.with.my.life."                                                                                  
## [58] "X.SWLS.4..So.far.I.have.gotten.the.important.things.I.want.in.life"                                                      
## [59] "X.SWLS.5..If.I.could.live.my.life.over..I.would.change.almost.nothing"                                                   
## [60] "Do.you.consider.yourself.a.procrastinator."                                                                              
## [61] "Do.others.consider.you.a.procrastinator."
```

```r
#structure of the data
glimpse(Procrastination_Raw_Data)
```

```
## Observations: 4,264
## Variables: 61
## $ Age                                                                                                                      <dbl> ...
## $ Gender                                                                                                                   <fctr> ...
## $ Kids                                                                                                                     <fctr> ...
## $ Edu                                                                                                                      <fctr> ...
## $ Work.Status                                                                                                              <fctr> ...
## $ Annual.Income                                                                                                            <int> ...
## $ Current.Occupation                                                                                                       <fctr> ...
## $ How.long.have.you.held.this.position...Years                                                                             <dbl> ...
## $ How.long.have.you.held.this.position...Months                                                                            <int> ...
## $ Community.size                                                                                                           <fctr> ...
## $ Country.of.residence                                                                                                     <fctr> ...
## $ Marital.Status                                                                                                           <fctr> ...
## $ Number.of.sons                                                                                                           <fctr> ...
## $ Number.of.daughters                                                                                                      <int> ...
## $ X.DP.1..I.waste.a.lot.of.time.on.trivial.matters.before.getting.to.the.final.decisions                                   <int> ...
## $ X.DP.2..Even.after.I.make.a.decision.I.delay.acting.upon.it                                                              <int> ...
## $ X.DP.3..I.don.t.make.decisions.unless.I.really.have.to                                                                   <int> ...
## $ X.DP.4..I.delay.making.decisions.until.it.s.too.late                                                                     <int> ...
## $ X.DP.5..I.put.off.making.decisions.until.it.s.too.late                                                                   <int> ...
## $ X.AIP.1..I.pay.my.bills.on.time                                                                                          <int> ...
## $ X.AIP.2.I.am.prompt.and.on.time.for.most.appointments.                                                                   <int> ...
## $ X.AIP.3.I.lay.out.my.clothes.the.night.before.I.have.an.important.appointment..so.I.won.t.be.late                        <int> ...
## $ X.AIP.4..I.find.myself.running.later.than.I.would.like.to.be                                                             <int> ...
## $ X.AIP.5..I.don.t.get.things.done.on.time                                                                                 <int> ...
## $ X.AIP.6..If.someone.were.teaching.a.course.on.how.to.get.things.done.on.time..I.would.attend                             <int> ...
## $ X.AIP.7..My.friends.and.family.think.I.wait.until.the.last.minute.                                                       <int> ...
## $ X.AIP.8..I.get.important.things.done.with.time.to.spare                                                                  <int> ...
## $ X.AIP.9..I.am.not.very.good.at.meeting.deadlines                                                                         <int> ...
## $ X.AIP.10..I.find.myself.running.out.of.time.                                                                             <int> ...
## $ X.AIP.11..I.schedule.doctor.s.appointments.when.I.am.supposed.to.without.delay                                           <int> ...
## $ X.AIP.12..I.am.more.punctual.than.most.people.I.know                                                                     <int> ...
## $ X.AIP.13..I.do.routine.maintenance..e.g...changing.the.car.oil..on.things.I.own.as.often.as.I.should                     <int> ...
## $ X.AIP.14.When.I.have.to.be.somewhere.at.a.certain.time.my.friends.expect.me.to.run.a.bit.late                            <int> ...
## $ X.AIP.15.Putting.things.off.till.the.last.minute.has.cost.me.money.in.the.past                                           <int> ...
## $ X.GP.1.I.often.find.myself.performing.tasks.that.I.had.intended.to.do.days.before                                        <int> ...
## $ X.GP2..I.often.miss.concerts..sporting.events..or.the.like.because.I.don.t.get.around.to.buying.tickets.on.time          <int> ...
## $ X.GP.3..When.planning.a.party..I.make.the.necessary.arrangements.well.in.advance                                         <int> ...
## $ X.GP.4..When.it.is.time.to.get.up.in.the.morning..I.most.often.get.right.out.of.bed                                      <int> ...
## $ X.GP.5..A.letter.may.sit.for.days.after.I.write.it.before.mailing.it.possible                                            <int> ...
## $ X.GP.6..I.generally.return.phone.calls.promptly                                                                          <int> ...
## $ X.GP.7..Even.jobs.that.require.little.else.except.sitting.down.and.doing.them..I.find.that.they.seldom.get.done.for.days <int> ...
## $ X.GP.8..I.usually.make.decisions.as.soon.as.possible                                                                     <int> ...
## $ X.GP.9..I.generally.delay.before.starting.on.work.I.have.to.do                                                           <int> ...
## $ X.GP.10..When.traveling..I.usually.have.to.rush.in.preparing.to.arrive.at.the.airport.or.station.at.the.appropriate.time <int> ...
## $ X.GP.11..When.preparing.to.go.out..I.am.seldom.caught.having.to.do.something.at.the.last.minute                          <int> ...
## $ X.GP.12..In.preparation.for.some.deadlines..I.often.waste.time.by.doing.other.things                                     <int> ...
## $ X.GP.13..If.a.bill.for.a.small.amount.comes..I.pay.it.right.away                                                         <int> ...
## $ X.GP.14..I.usually.return.a..RSVP..request.very.shortly.after.receiving.it                                               <int> ...
## $ X.GP.15..I.often.have.a.task.finished.sooner.than.necessary                                                              <int> ...
## $ X.GP.16..I.always.seem.to.end.up.shopping.for.birthday.gifts.at.the.last.minute                                          <int> ...
## $ X.GP.17..I.usually.buy.even.an.essential.item.at.the.last.minute                                                         <int> ...
## $ X.GP.18..I.usually.accomplish.all.the.things.I.plan.to.do.in.a.day                                                       <int> ...
## $ X.GP.19..I.am.continually.saying..I.ll.do.it.tomorrow.                                                                   <int> ...
## $ X.GP.20..I.usually.take.care.of.all.the.tasks.I.have.to.do.before.I.settle.down.and.relax.for.the.evening                <int> ...
## $ X.SWLS.1..In.most.ways.my.life.is.close.to.my.ideal                                                                      <int> ...
## $ X.SWLS.2.The.conditions.of.my.life.are.excellent                                                                         <int> ...
## $ X.SWLS.3..I.am.satisfied.with.my.life.                                                                                   <int> ...
## $ X.SWLS.4..So.far.I.have.gotten.the.important.things.I.want.in.life                                                       <int> ...
## $ X.SWLS.5..If.I.could.live.my.life.over..I.would.change.almost.nothing                                                    <int> ...
## $ Do.you.consider.yourself.a.procrastinator.                                                                               <fctr> ...
## $ Do.others.consider.you.a.procrastinator.                                                                                 <fctr> ...
```

```r
#view summary
summary(Procrastination_Raw_Data)
```

```
##       Age           Gender           Kids           Edu      
##  Min.   : 7.50         :  70           :   4   deg    :1199  
##  1st Qu.:28.00   Female:2408   No Kids :2901   ma     :1098  
##  Median :32.50   Male  :1786   Yes Kids:1359   ltuni  : 812  
##  Mean   :37.43                                 phd    : 609  
##  3rd Qu.:45.00                                 dip    : 205  
##  Max.   :80.00                                 high   : 122  
##  NA's   :71                                    (Other): 219  
##      Work.Status   Annual.Income            Current.Occupation
##            : 111   Min.   :     0                    :2162    
##  0         :   2   1st Qu.: 15000   0                : 488    
##  full-time :2266   Median : 45000   please specify   : 217    
##  part-time : 477   Mean   : 58916    teacher         :  74    
##  retired   : 175   3rd Qu.: 67500   college professor:  43    
##  student   : 971   Max.   :250000   engineer         :  32    
##  unemployed: 262   NA's   :548      (Other)          :1248    
##  How.long.have.you.held.this.position...Years
##  Min.   :  0.00                              
##  1st Qu.:  0.00                              
##  Median :  2.00                              
##  Mean   : 14.15                              
##  3rd Qu.:  6.00                              
##  Max.   :999.00                              
##  NA's   :94                                  
##  How.long.have.you.held.this.position...Months      Community.size
##  Min.   : 0.000                                Large-City  :876   
##  1st Qu.: 0.000                                Village     :830   
##  Median : 0.000                                Medium-Sized:669   
##  Mean   : 1.793                                Small Town  :655   
##  3rd Qu.: 3.000                                Large Town  :466   
##  Max.   :11.000                                Small City  :311   
##  NA's   :6                                     (Other)     :457   
##      Country.of.residence   Marital.Status Number.of.sons
##  United States :2893               : 174   0      :3272  
##  Canada        : 250      0        :   6   Male   : 613  
##  0             : 233      Divorced : 367   Female : 274  
##  United Kingdom: 184      Married  :1599   3      :  69  
##  Australia     : 104      Separated:  88   4      :  23  
##  India         :  78      Single   :1963   5      :   7  
##  (Other)       : 522      Widowed  :  67   (Other):   6  
##  Number.of.daughters
##  Min.   : 0.0000    
##  1st Qu.: 0.0000    
##  Median : 0.0000    
##  Mean   : 0.3538    
##  3rd Qu.: 0.0000    
##  Max.   :10.0000    
##  NA's   :4          
##  X.DP.1..I.waste.a.lot.of.time.on.trivial.matters.before.getting.to.the.final.decisions
##  Min.   :1.000                                                                         
##  1st Qu.:3.000                                                                         
##  Median :3.000                                                                         
##  Mean   :3.392                                                                         
##  3rd Qu.:4.000                                                                         
##  Max.   :5.000                                                                         
##                                                                                        
##  X.DP.2..Even.after.I.make.a.decision.I.delay.acting.upon.it
##  Min.   :1.000                                              
##  1st Qu.:3.000                                              
##  Median :3.000                                              
##  Mean   :3.354                                              
##  3rd Qu.:4.000                                              
##  Max.   :5.000                                              
##                                                             
##  X.DP.3..I.don.t.make.decisions.unless.I.really.have.to
##  Min.   :1.000                                         
##  1st Qu.:2.000                                         
##  Median :3.000                                         
##  Mean   :3.198                                         
##  3rd Qu.:4.000                                         
##  Max.   :5.000                                         
##                                                        
##  X.DP.4..I.delay.making.decisions.until.it.s.too.late
##  Min.   :1.000                                       
##  1st Qu.:2.000                                       
##  Median :3.000                                       
##  Mean   :2.688                                       
##  3rd Qu.:3.000                                       
##  Max.   :5.000                                       
##                                                      
##  X.DP.5..I.put.off.making.decisions.until.it.s.too.late
##  Min.   :1.000                                         
##  1st Qu.:2.000                                         
##  Median :3.000                                         
##  Mean   :2.678                                         
##  3rd Qu.:3.000                                         
##  Max.   :5.000                                         
##                                                        
##  X.AIP.1..I.pay.my.bills.on.time
##  Min.   :1.000                  
##  1st Qu.:1.000                  
##  Median :2.000                  
##  Mean   :2.054                  
##  3rd Qu.:3.000                  
##  Max.   :5.000                  
##                                 
##  X.AIP.2.I.am.prompt.and.on.time.for.most.appointments.
##  Min.   :1.000                                         
##  1st Qu.:1.000                                         
##  Median :2.000                                         
##  Mean   :2.161                                         
##  3rd Qu.:3.000                                         
##  Max.   :5.000                                         
##                                                        
##  X.AIP.3.I.lay.out.my.clothes.the.night.before.I.have.an.important.appointment..so.I.won.t.be.late
##  Min.   :1.000                                                                                    
##  1st Qu.:2.000                                                                                    
##  Median :3.000                                                                                    
##  Mean   :3.371                                                                                    
##  3rd Qu.:5.000                                                                                    
##  Max.   :5.000                                                                                    
##                                                                                                   
##  X.AIP.4..I.find.myself.running.later.than.I.would.like.to.be
##  Min.   :1.000                                               
##  1st Qu.:2.000                                               
##  Median :3.000                                               
##  Mean   :3.206                                               
##  3rd Qu.:4.000                                               
##  Max.   :5.000                                               
##                                                              
##  X.AIP.5..I.don.t.get.things.done.on.time
##  Min.   :1.000                           
##  1st Qu.:2.000                           
##  Median :3.000                           
##  Mean   :3.068                           
##  3rd Qu.:4.000                           
##  Max.   :5.000                           
##                                          
##  X.AIP.6..If.someone.were.teaching.a.course.on.how.to.get.things.done.on.time..I.would.attend
##  Min.   :1.000                                                                               
##  1st Qu.:2.000                                                                               
##  Median :3.000                                                                               
##  Mean   :2.843                                                                               
##  3rd Qu.:4.000                                                                               
##  Max.   :5.000                                                                               
##                                                                                              
##  X.AIP.7..My.friends.and.family.think.I.wait.until.the.last.minute.
##  Min.   :1.000                                                     
##  1st Qu.:2.000                                                     
##  Median :3.000                                                     
##  Mean   :3.218                                                     
##  3rd Qu.:4.000                                                     
##  Max.   :5.000                                                     
##                                                                    
##  X.AIP.8..I.get.important.things.done.with.time.to.spare
##  Min.   :1.000                                          
##  1st Qu.:3.000                                          
##  Median :3.000                                          
##  Mean   :3.421                                          
##  3rd Qu.:4.000                                          
##  Max.   :5.000                                          
##                                                         
##  X.AIP.9..I.am.not.very.good.at.meeting.deadlines
##  Min.   :1.000                                   
##  1st Qu.:2.000                                   
##  Median :3.000                                   
##  Mean   :2.757                                   
##  3rd Qu.:4.000                                   
##  Max.   :5.000                                   
##                                                  
##  X.AIP.10..I.find.myself.running.out.of.time.
##  Min.   :1.000                               
##  1st Qu.:3.000                               
##  Median :4.000                               
##  Mean   :3.468                               
##  3rd Qu.:4.000                               
##  Max.   :5.000                               
##                                              
##  X.AIP.11..I.schedule.doctor.s.appointments.when.I.am.supposed.to.without.delay
##  Min.   :1.000                                                                 
##  1st Qu.:2.000                                                                 
##  Median :3.000                                                                 
##  Mean   :3.045                                                                 
##  3rd Qu.:4.000                                                                 
##  Max.   :5.000                                                                 
##                                                                                
##  X.AIP.12..I.am.more.punctual.than.most.people.I.know
##  Min.   :1.000                                       
##  1st Qu.:2.000                                       
##  Median :3.000                                       
##  Mean   :2.981                                       
##  3rd Qu.:4.000                                       
##  Max.   :5.000                                       
##                                                      
##  X.AIP.13..I.do.routine.maintenance..e.g...changing.the.car.oil..on.things.I.own.as.often.as.I.should
##  Min.   :1.000                                                                                       
##  1st Qu.:2.000                                                                                       
##  Median :3.000                                                                                       
##  Mean   :3.118                                                                                       
##  3rd Qu.:4.000                                                                                       
##  Max.   :5.000                                                                                       
##                                                                                                      
##  X.AIP.14.When.I.have.to.be.somewhere.at.a.certain.time.my.friends.expect.me.to.run.a.bit.late
##  Min.   :1.000                                                                                
##  1st Qu.:2.000                                                                                
##  Median :2.000                                                                                
##  Mean   :2.658                                                                                
##  3rd Qu.:4.000                                                                                
##  Max.   :5.000                                                                                
##                                                                                               
##  X.AIP.15.Putting.things.off.till.the.last.minute.has.cost.me.money.in.the.past
##  Min.   :1.000                                                                 
##  1st Qu.:2.000                                                                 
##  Median :3.000                                                                 
##  Mean   :3.193                                                                 
##  3rd Qu.:4.000                                                                 
##  Max.   :5.000                                                                 
##                                                                                
##  X.GP.1.I.often.find.myself.performing.tasks.that.I.had.intended.to.do.days.before
##  Min.   :1.000                                                                    
##  1st Qu.:3.000                                                                    
##  Median :4.000                                                                    
##  Mean   :3.671                                                                    
##  3rd Qu.:5.000                                                                    
##  Max.   :5.000                                                                    
##                                                                                   
##  X.GP2..I.often.miss.concerts..sporting.events..or.the.like.because.I.don.t.get.around.to.buying.tickets.on.time
##  Min.   :1.000                                                                                                  
##  1st Qu.:1.000                                                                                                  
##  Median :2.000                                                                                                  
##  Mean   :2.307                                                                                                  
##  3rd Qu.:3.000                                                                                                  
##  Max.   :5.000                                                                                                  
##                                                                                                                 
##  X.GP.3..When.planning.a.party..I.make.the.necessary.arrangements.well.in.advance
##  Min.   :1.000                                                                   
##  1st Qu.:2.000                                                                   
##  Median :3.000                                                                   
##  Mean   :2.774                                                                   
##  3rd Qu.:4.000                                                                   
##  Max.   :5.000                                                                   
##                                                                                  
##  X.GP.4..When.it.is.time.to.get.up.in.the.morning..I.most.often.get.right.out.of.bed
##  Min.   :1.000                                                                      
##  1st Qu.:2.000                                                                      
##  Median :3.000                                                                      
##  Mean   :3.321                                                                      
##  3rd Qu.:5.000                                                                      
##  Max.   :5.000                                                                      
##                                                                                     
##  X.GP.5..A.letter.may.sit.for.days.after.I.write.it.before.mailing.it.possible
##  Min.   :1.000                                                                
##  1st Qu.:2.000                                                                
##  Median :3.000                                                                
##  Mean   :3.022                                                                
##  3rd Qu.:4.000                                                                
##  Max.   :5.000                                                                
##                                                                               
##  X.GP.6..I.generally.return.phone.calls.promptly
##  Min.   :1.000                                  
##  1st Qu.:2.000                                  
##  Median :3.000                                  
##  Mean   :2.802                                  
##  3rd Qu.:4.000                                  
##  Max.   :5.000                                  
##                                                 
##  X.GP.7..Even.jobs.that.require.little.else.except.sitting.down.and.doing.them..I.find.that.they.seldom.get.done.for.days
##  Min.   :1.000                                                                                                           
##  1st Qu.:3.000                                                                                                           
##  Median :3.000                                                                                                           
##  Mean   :3.382                                                                                                           
##  3rd Qu.:4.000                                                                                                           
##  Max.   :5.000                                                                                                           
##                                                                                                                          
##  X.GP.8..I.usually.make.decisions.as.soon.as.possible
##  Min.   :1.00                                        
##  1st Qu.:3.00                                        
##  Median :3.00                                        
##  Mean   :3.27                                        
##  3rd Qu.:4.00                                        
##  Max.   :5.00                                        
##                                                      
##  X.GP.9..I.generally.delay.before.starting.on.work.I.have.to.do
##  Min.   :1.000                                                 
##  1st Qu.:3.000                                                 
##  Median :4.000                                                 
##  Mean   :3.749                                                 
##  3rd Qu.:5.000                                                 
##  Max.   :5.000                                                 
##                                                                
##  X.GP.10..When.traveling..I.usually.have.to.rush.in.preparing.to.arrive.at.the.airport.or.station.at.the.appropriate.time
##  Min.   :1.0                                                                                                             
##  1st Qu.:2.0                                                                                                             
##  Median :3.0                                                                                                             
##  Mean   :2.7                                                                                                             
##  3rd Qu.:4.0                                                                                                             
##  Max.   :5.0                                                                                                             
##                                                                                                                          
##  X.GP.11..When.preparing.to.go.out..I.am.seldom.caught.having.to.do.something.at.the.last.minute
##  Min.   :1.000                                                                                  
##  1st Qu.:2.000                                                                                  
##  Median :3.000                                                                                  
##  Mean   :3.257                                                                                  
##  3rd Qu.:4.000                                                                                  
##  Max.   :5.000                                                                                  
##                                                                                                 
##  X.GP.12..In.preparation.for.some.deadlines..I.often.waste.time.by.doing.other.things
##  Min.   :1.000                                                                       
##  1st Qu.:3.000                                                                       
##  Median :4.000                                                                       
##  Mean   :3.682                                                                       
##  3rd Qu.:4.000                                                                       
##  Max.   :5.000                                                                       
##                                                                                      
##  X.GP.13..If.a.bill.for.a.small.amount.comes..I.pay.it.right.away
##  Min.   :1.000                                                   
##  1st Qu.:2.000                                                   
##  Median :3.000                                                   
##  Mean   :2.687                                                   
##  3rd Qu.:4.000                                                   
##  Max.   :5.000                                                   
##                                                                  
##  X.GP.14..I.usually.return.a..RSVP..request.very.shortly.after.receiving.it
##  Min.   :1.000                                                             
##  1st Qu.:2.000                                                             
##  Median :3.000                                                             
##  Mean   :3.095                                                             
##  3rd Qu.:4.000                                                             
##  Max.   :5.000                                                             
##                                                                            
##  X.GP.15..I.often.have.a.task.finished.sooner.than.necessary
##  Min.   :1.000                                              
##  1st Qu.:3.000                                              
##  Median :4.000                                              
##  Mean   :3.567                                              
##  3rd Qu.:4.000                                              
##  Max.   :5.000                                              
##                                                             
##  X.GP.16..I.always.seem.to.end.up.shopping.for.birthday.gifts.at.the.last.minute
##  Min.   :1.000                                                                  
##  1st Qu.:3.000                                                                  
##  Median :4.000                                                                  
##  Mean   :3.663                                                                  
##  3rd Qu.:5.000                                                                  
##  Max.   :5.000                                                                  
##                                                                                 
##  X.GP.17..I.usually.buy.even.an.essential.item.at.the.last.minute
##  Min.   :1.000                                                   
##  1st Qu.:2.000                                                   
##  Median :3.000                                                   
##  Mean   :3.178                                                   
##  3rd Qu.:4.000                                                   
##  Max.   :5.000                                                   
##                                                                  
##  X.GP.18..I.usually.accomplish.all.the.things.I.plan.to.do.in.a.day
##  Min.   :1.000                                                     
##  1st Qu.:3.000                                                     
##  Median :4.000                                                     
##  Mean   :3.634                                                     
##  3rd Qu.:4.000                                                     
##  Max.   :5.000                                                     
##                                                                    
##  X.GP.19..I.am.continually.saying..I.ll.do.it.tomorrow.
##  Min.   :1.000                                         
##  1st Qu.:3.000                                         
##  Median :4.000                                         
##  Mean   :3.589                                         
##  3rd Qu.:5.000                                         
##  Max.   :5.000                                         
##                                                        
##  X.GP.20..I.usually.take.care.of.all.the.tasks.I.have.to.do.before.I.settle.down.and.relax.for.the.evening
##  Min.   :1.000                                                                                            
##  1st Qu.:3.000                                                                                            
##  Median :4.000                                                                                            
##  Mean   :3.531                                                                                            
##  3rd Qu.:4.000                                                                                            
##  Max.   :5.000                                                                                            
##                                                                                                           
##  X.SWLS.1..In.most.ways.my.life.is.close.to.my.ideal
##  Min.   :1.000                                      
##  1st Qu.:2.000                                      
##  Median :3.000                                      
##  Mean   :2.943                                      
##  3rd Qu.:4.000                                      
##  Max.   :5.000                                      
##                                                     
##  X.SWLS.2.The.conditions.of.my.life.are.excellent
##  Min.   :1.000                                   
##  1st Qu.:3.000                                   
##  Median :3.000                                   
##  Mean   :3.199                                   
##  3rd Qu.:4.000                                   
##  Max.   :5.000                                   
##                                                  
##  X.SWLS.3..I.am.satisfied.with.my.life.
##  Min.   :1.00                          
##  1st Qu.:2.00                          
##  Median :3.00                          
##  Mean   :3.11                          
##  3rd Qu.:4.00                          
##  Max.   :5.00                          
##                                        
##  X.SWLS.4..So.far.I.have.gotten.the.important.things.I.want.in.life
##  Min.   :1.000                                                     
##  1st Qu.:2.000                                                     
##  Median :3.000                                                     
##  Mean   :3.244                                                     
##  3rd Qu.:4.000                                                     
##  Max.   :5.000                                                     
##                                                                    
##  X.SWLS.5..If.I.could.live.my.life.over..I.would.change.almost.nothing
##  Min.   :1.000                                                        
##  1st Qu.:2.000                                                        
##  Median :3.000                                                        
##  Mean   :2.689                                                        
##  3rd Qu.:4.000                                                        
##  Max.   :5.000                                                        
##                                                                       
##  Do.you.consider.yourself.a.procrastinator.
##     :  14                                  
##  no : 565                                  
##  yes:3685                                  
##                                            
##                                            
##                                            
##                                            
##  Do.others.consider.you.a.procrastinator.
##     :  42                                
##  0  :   1                                
##  4  :   8                                
##  no :1652                                
##  yes:2561                                
##                                          
## 
```

```r
# b The column names are either too much or not enough. Change the column names so that they do not have spaces, underscores, slashes, and the like. All column names should be under 12 characters. Make sure you're updating your codebook with information on the tidied data set as well.

#renaming the columns

names(Procrastination_Raw_Data)[5:61] = c("WorkStatus","Income","Occupation","PositionYrs","PositionMnth","CommSize","Country","MaritalStatus","NumofSons","NumofDaughters","XDP1","XDP2","XDP3","XDP4","XDP5","XAIP1","XAIP2","XAIP3","XAIP4","XAIP5","XAIP6","XAIP7","XAIP8","XAIP9","XAIP10","XAIP11","XAIP12","XAIP13","XAIP14","XAIP15","XGP1","XGP2","XGP3","XGP4","XGP5","XGP6","XGP7","XGP8","XGP9","XGP10","XGP11","XGP12","XGP13","XGP14","XGP15","XGP16","XGP17","XGP18","XGP19","XGP20","XSWLS1","XSWLS2","XSWLS3","XSWLS4","XSWLS5","Yourself","Others")


# c Some columns are, due to Qualtrics, malfunctioning. Prime examples are the following columns: "How long have you held this position?: Years", Country of residence, Number of sons, and Current Occupation.

# i Some have impossible data values. Detail what you are doing to fix these columns in the raw data and why. It's a judgment call for each, but explain why. For example, most people have not been doing anything for over 100 years. For the "Years" columns, round to the nearest integer.

#Data in the PostionYrs column that is 999 years or blank we will omit in our analysis, since 999 years is impossible and blank values are bad data. 
#Omitting the rows is better than assuming a different value, and we have enough data with valid values to complete our analysis.
Procrastination_Raw_Data <- Procrastination_Raw_Data[which(Procrastination_Raw_Data$PositionYrs != ""),]
Procrastination_Raw_Data <- Procrastination_Raw_Data[which(Procrastination_Raw_Data$PositionYrs != 999),]
Procrastination_Raw_Data$PositionYrs <- round(Procrastination_Raw_Data$PositionYrs,0)

#Note that the data frame has 61 columns and 4264 rows and some of the columns have Null values and impossible data values. E.g People doing nothing over 100 years might be dead and must be removed from the dataset
#glimpse(Procrastination_Raw_Data)

# ii Somehow, "Number of sons" was labeled with Male (1) and Female (2). Change these incorrect labels back to integers.
Procrastination_Raw_Data <- Procrastination_Raw_Data[which(Procrastination_Raw_Data$NumofSons == "Male"),]
Procrastination_Raw_Data$NumofSons[which(Procrastination_Raw_Data$NumofSons == "Male")] <- "1"
Procrastination_Raw_Data$NumofSons[which(Procrastination_Raw_Data$NumofSons == "Female")] <- "2"
Procrastination_Raw_Data$NumofSons <- as.integer(Procrastination_Raw_Data$NumofSons)

# iii There are no "0" country of residences. Treat this as missing.
Procrastination_Raw_Data$Country[which(Procrastination_Raw_Data$Country == "0")] <- NA


# iv Current Occupation has no "please specify" or "0." Treat them as missing. Some jobs are quite similar. Use judgment calls to make overwrite them into the same category. It does not have to be 100% accurate, but right now "ESL Teacher" would not be counted as "teacher" if there were unique counts.
Procrastination_Raw_Data$Occupation[which(Procrastination_Raw_Data$Occupation == "0")] <- NA
Procrastination_Raw_Data$Occupation[which(Procrastination_Raw_Data$Occupation == "please specify")] <- NA

# d Make sure your columns are the proper data types (i.e., numeric, character, etc.). If they are incorrect, convert them.

#Reclassifying variables to their logical types
#The "Yourself" and "Others" fields could be boolean, but there are some bad values in Others so we're just proceeding as characters for now, we only lose a slight performance gain given the size of our data.
Procrastination_Raw_Data$Gender <- as.character(Procrastination_Raw_Data$Gender)
Procrastination_Raw_Data$Kids <- as.character(Procrastination_Raw_Data$Kids)
Procrastination_Raw_Data$Edu <- as.character(Procrastination_Raw_Data$Edu)
Procrastination_Raw_Data$WorkStatus <- as.character(Procrastination_Raw_Data$WorkStatus)
Procrastination_Raw_Data$Occupation <- as.character(Procrastination_Raw_Data$Occupation)
Procrastination_Raw_Data$PositionYrs <- as.integer(Procrastination_Raw_Data$PositionYrs)
Procrastination_Raw_Data$CommSize <- as.character(Procrastination_Raw_Data$CommSize)
Procrastination_Raw_Data$Country <- as.character(Procrastination_Raw_Data$Country)
Procrastination_Raw_Data$MaritalStatus <- as.character(Procrastination_Raw_Data$MaritalStatus)
Procrastination_Raw_Data$Yourself <- as.character(Procrastination_Raw_Data$Yourself)
Procrastination_Raw_Data$Others <- as.character(Procrastination_Raw_Data$Others)


# e Each variable that starts with either DP, AIP, GP, or SWLS is an individual item on a scale. For example, DP 1 through DP 5 are five different questions on the Decision Procrastination Scale. I've reverse-scored them for you already, but you should create a new column for each of them with their mean. To clarify, you'll need a DPMean column, an AIPMean column, a GPMean column, and a SWLSMean column. This represents the individual's average decisional procrastination (DP), procrastination behavior (AIP), generalized procrastination (GP), and life satisfaction (SWLS).

#Grab average of all the  DP, AIP, GP, and SWLS fields in a simple and readable way, summing and dividing
Procrastination_Raw_Data$DP_Mean <- mean(c(Procrastination_Raw_Data$XDP1,Procrastination_Raw_Data$XDP2,Procrastination_Raw_Data$XDP3,Procrastination_Raw_Data$XDP4,Procrastination_Raw_Data$XDP5))

Procrastination_Raw_Data$DP_Mean <- (Procrastination_Raw_Data$XDP1 + Procrastination_Raw_Data$XDP2 + Procrastination_Raw_Data$XDP3 + Procrastination_Raw_Data$XDP4 + Procrastination_Raw_Data$XDP5)/5

Procrastination_Raw_Data$AIP_Mean <- (Procrastination_Raw_Data$XAIP1 + Procrastination_Raw_Data$XAIP2 + Procrastination_Raw_Data$XAIP3 + Procrastination_Raw_Data$XAIP4 + Procrastination_Raw_Data$XAIP5 + Procrastination_Raw_Data$XAIP6 + Procrastination_Raw_Data$XAIP7 + Procrastination_Raw_Data$XAIP8 + Procrastination_Raw_Data$XAIP9 + Procrastination_Raw_Data$XAIP10 + Procrastination_Raw_Data$XAIP11 + Procrastination_Raw_Data$XAIP12 + Procrastination_Raw_Data$XAIP13 + Procrastination_Raw_Data$XAIP14 + Procrastination_Raw_Data$XAIP15)/15

Procrastination_Raw_Data$GP_Mean <- (Procrastination_Raw_Data$XGP1 + Procrastination_Raw_Data$XGP2 + Procrastination_Raw_Data$XGP3 + Procrastination_Raw_Data$XGP4 + Procrastination_Raw_Data$XGP5 + Procrastination_Raw_Data$XGP6 + Procrastination_Raw_Data$XGP7 + Procrastination_Raw_Data$XGP8 + Procrastination_Raw_Data$XGP9 + Procrastination_Raw_Data$XGP10 + Procrastination_Raw_Data$XGP11 + Procrastination_Raw_Data$XGP12 + Procrastination_Raw_Data$XGP13 + Procrastination_Raw_Data$XGP14 + Procrastination_Raw_Data$XGP15 + Procrastination_Raw_Data$XGP16 + Procrastination_Raw_Data$XGP17 + Procrastination_Raw_Data$XGP18 + Procrastination_Raw_Data$XGP19 + Procrastination_Raw_Data$XGP20 )/20

Procrastination_Raw_Data$SWLS_Mean <- (Procrastination_Raw_Data$XSWLS1 + Procrastination_Raw_Data$XSWLS2 + Procrastination_Raw_Data$XSWLS3 + Procrastination_Raw_Data$XSWLS4 + Procrastination_Raw_Data$XSWLS5)/5
```


## Scrape the Human Development Index tables online



```r
# (https://en.wikipedia.org/wiki/List_of_countries_by_Human_Development_Index#Complete_list_of_countries). Read what it is, because you'll have to explain it to your clients. BIG TIP: This one's going to be weird looking-it's real scraping. Make sure you're looking between the webpage and R while you do this to find your footing. Unit 9's HW might help.

# a You will notice there are several sections, but you should only worry about the Complete List of Countries section of this Wikipedia entry. There are 8 tables in this section, but you should pull these eight, clean them as to be usable, and then find a way to bind them into one singular table. You only need Country and 2016 Estimates for 2015 (you can call this HDI) columns for the final table.

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
Procrastination_Raw_Data <- Procrastination_Raw_Data[which(Procrastination_Raw_Data$Country != ""),]
Procrastination_Raw_Data <- Procrastination_Raw_Data[which(Procrastination_Raw_Data$Country != "0"),]
Procrastination_Raw_Data <- Procrastination_Raw_Data[which(!is.na(Procrastination_Raw_Data$Country)),]
#changed to match merged HDI data
Procrastination_Raw_Data$Country[which(Procrastination_Raw_Data$Country == "Isreal")] <- "Israel"

#changed to match Procrastination
hdiDataFrame_all$Country[which(hdiDataFrame_all$Country == "Antigua and Barbuda")] <- "Antigua"

#Merge the data and keep all Procrastination, even if there is no match for HDI Data. We can revisit this later if it causes problems
ProcrastinationHdiData <- merge(Procrastination_Raw_Data,hdiDataFrame_all,by.x = "Country", by.y = "Country",all.x=TRUE)

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
# a Remove all observations where the participant is under age 18. No further analysis of underage individuals is permitted by your client. Remove any other age outliers as you see fit, but be sure to tell what you’re doing and why.
ProcrastinationHdiData_18_or_older <- ProcrastinationHdiData[which(ProcrastinationHdiData$Age >= 18),]

# b Please provide (in pretty-fied table format or similar), descriptive statistics on Age, Income, HDI, and the four mean columns (DP, etc.). 

#separate the summary from its class structure to be stored in a data frame 
dfAgeSummary<- data.frame(unclass(summary(ProcrastinationHdiData_18_or_older$Age)), check.names = FALSE)
dfIncomeSummary<- data.frame(unclass(summary(ProcrastinationHdiData_18_or_older$Income)), check.names = FALSE)
dfHDISummary<- data.frame(unclass(summary(ProcrastinationHdiData_18_or_older$HDI)), check.names = FALSE)
dfDPSummary<- data.frame(unclass(summary(ProcrastinationHdiData_18_or_older$DP_Mean)), check.names = FALSE)
dfAIPSummary<- data.frame(unclass(summary(ProcrastinationHdiData_18_or_older$AIP_Mean)), check.names = FALSE)
dfGPSummary<- data.frame(unclass(summary(ProcrastinationHdiData_18_or_older$GP_Mean)), check.names = FALSE)
dfSWLSSummary<- data.frame(unclass(summary(ProcrastinationHdiData_18_or_older$SWLS_Mean)), check.names = FALSE)

#Transpose to get the identifiers into columns
dfAgeSummaryT <- data.frame(round(t(dfAgeSummary),2))
dfIncomeSummaryT <- data.frame(round(t(dfIncomeSummary),2))
dfHDISummaryT <- data.frame(round(t(dfHDISummary),2))
dfDPSummaryT <- data.frame(round(t(dfDPSummary),2))
dfAIPSummaryT <- data.frame(round(t(dfAIPSummary),2))
dfGPSummaryT <- data.frame(round(t(dfGPSummary),2))
dfSWLSSummaryT <- data.frame(round(t(dfSWLSSummary),2))


#print the datatables in a pretty-fied format
datatable(dfAgeSummaryT, rownames = FALSE,
          caption = 'Summary of Age Statistics')
```

<!--html_preserve--><div id="htmlwidget-4c5b1491597ca4ece35d" style="width:100%;height:auto;" class="datatables html-widget"></div>
<script type="application/json" data-for="htmlwidget-4c5b1491597ca4ece35d">{"x":{"filter":"none","caption":"<caption>Summary of Age Statistics<\/caption>","data":[[20],[37.5],[45],[47.62],[55],[80]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th>Min.<\/th>\n      <th>X1st.Qu.<\/th>\n      <th>Median<\/th>\n      <th>Mean<\/th>\n      <th>X3rd.Qu.<\/th>\n      <th>Max.<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"columnDefs":[{"className":"dt-right","targets":[0,1,2,3,4,5]}],"order":[],"autoWidth":false,"orderClasses":false}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

```r
datatable(dfIncomeSummaryT, rownames = FALSE,
          caption = 'Summary of Income Statistics')
```

<!--html_preserve--><div id="htmlwidget-d166809e9d085f207afe" style="width:100%;height:auto;" class="datatables html-widget"></div>
<script type="application/json" data-for="htmlwidget-d166809e9d085f207afe">{"x":{"filter":"none","caption":"<caption>Summary of Income Statistics<\/caption>","data":[[10000],[35000],[67500],[81589.62],[87500],[250000],[38]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th>Min.<\/th>\n      <th>X1st.Qu.<\/th>\n      <th>Median<\/th>\n      <th>Mean<\/th>\n      <th>X3rd.Qu.<\/th>\n      <th>Max.<\/th>\n      <th>NA.s<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"columnDefs":[{"className":"dt-right","targets":[0,1,2,3,4,5,6]}],"order":[],"autoWidth":false,"orderClasses":false}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

```r
datatable(dfHDISummaryT, rownames = FALSE,
          caption = 'Summary of HDI Statistics')
```

<!--html_preserve--><div id="htmlwidget-18cdd26e24a29e50c8b8" style="width:100%;height:auto;" class="datatables html-widget"></div>
<script type="application/json" data-for="htmlwidget-18cdd26e24a29e50c8b8">{"x":{"filter":"none","caption":"<caption>Summary of HDI Statistics<\/caption>","data":[[0.55],[0.92],[0.92],[0.91],[0.92],[0.95],[1]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th>Min.<\/th>\n      <th>X1st.Qu.<\/th>\n      <th>Median<\/th>\n      <th>Mean<\/th>\n      <th>X3rd.Qu.<\/th>\n      <th>Max.<\/th>\n      <th>NA.s<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"columnDefs":[{"className":"dt-right","targets":[0,1,2,3,4,5,6]}],"order":[],"autoWidth":false,"orderClasses":false}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

```r
datatable(dfDPSummaryT, rownames = FALSE,
          caption = 'Summary of DP Statistics')
```

<!--html_preserve--><div id="htmlwidget-ee287e9e8b96b4305592" style="width:100%;height:auto;" class="datatables html-widget"></div>
<script type="application/json" data-for="htmlwidget-ee287e9e8b96b4305592">{"x":{"filter":"none","caption":"<caption>Summary of DP Statistics<\/caption>","data":[[1],[2.2],[3],[2.99],[3.6],[5]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th>Min.<\/th>\n      <th>X1st.Qu.<\/th>\n      <th>Median<\/th>\n      <th>Mean<\/th>\n      <th>X3rd.Qu.<\/th>\n      <th>Max.<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"columnDefs":[{"className":"dt-right","targets":[0,1,2,3,4,5]}],"order":[],"autoWidth":false,"orderClasses":false}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

```r
datatable(dfAIPSummaryT, rownames = FALSE,
          caption = 'Summary of AIP Statistics')
```

<!--html_preserve--><div id="htmlwidget-98d26777957b5758ee17" style="width:100%;height:auto;" class="datatables html-widget"></div>
<script type="application/json" data-for="htmlwidget-98d26777957b5758ee17">{"x":{"filter":"none","caption":"<caption>Summary of AIP Statistics<\/caption>","data":[[1],[2.33],[2.93],[2.96],[3.53],[5]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th>Min.<\/th>\n      <th>X1st.Qu.<\/th>\n      <th>Median<\/th>\n      <th>Mean<\/th>\n      <th>X3rd.Qu.<\/th>\n      <th>Max.<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"columnDefs":[{"className":"dt-right","targets":[0,1,2,3,4,5]}],"order":[],"autoWidth":false,"orderClasses":false}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

```r
datatable(dfGPSummaryT, rownames = FALSE,
          caption = 'Summary of GP Statistics')
```

<!--html_preserve--><div id="htmlwidget-9fa2ad013c033d1d99b2" style="width:100%;height:auto;" class="datatables html-widget"></div>
<script type="application/json" data-for="htmlwidget-9fa2ad013c033d1d99b2">{"x":{"filter":"none","caption":"<caption>Summary of GP Statistics<\/caption>","data":[[1.15],[2.7],[3.25],[3.19],[3.7],[4.95]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th>Min.<\/th>\n      <th>X1st.Qu.<\/th>\n      <th>Median<\/th>\n      <th>Mean<\/th>\n      <th>X3rd.Qu.<\/th>\n      <th>Max.<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"columnDefs":[{"className":"dt-right","targets":[0,1,2,3,4,5]}],"order":[],"autoWidth":false,"orderClasses":false}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

```r
datatable(dfSWLSSummaryT, rownames = FALSE,
          caption = 'Summary of SWLS Statistics')
```

<!--html_preserve--><div id="htmlwidget-43382e75c67181adae22" style="width:100%;height:auto;" class="datatables html-widget"></div>
<script type="application/json" data-for="htmlwidget-43382e75c67181adae22">{"x":{"filter":"none","caption":"<caption>Summary of SWLS Statistics<\/caption>","data":[[1],[2.4],[3.2],[3.1],[3.8],[5]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th>Min.<\/th>\n      <th>X1st.Qu.<\/th>\n      <th>Median<\/th>\n      <th>Mean<\/th>\n      <th>X3rd.Qu.<\/th>\n      <th>Max.<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"columnDefs":[{"className":"dt-right","targets":[0,1,2,3,4,5]}],"order":[],"autoWidth":false,"orderClasses":false}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

```r
#Create a simple histogram for two of these seven variables. Comment on the shape of the distribution in your markdown.
hist(ProcrastinationHdiData_18_or_older$Income, xlab="Income", ylab="count",  main="Count of Incomes")
```

![](C:\Users\Brian\Documents\GitHub\CaseStudy2-Repo\Paper\caseStudy2_files/figure-html/CaseStudy_2_6.R-8.png)<!-- -->

```r
hist(ProcrastinationHdiData_18_or_older$Age, xlab="Age", ylab="count",  main="Count of Ages")
```

![](C:\Users\Brian\Documents\GitHub\CaseStudy2-Repo\Paper\caseStudy2_files/figure-html/CaseStudy_2_6.R-9.png)<!-- -->


As we can see see from the Income histogram, most of our data comes from people with incomes less than 100,000 US Dollars per year. There is not a normal distribution of these data, since a large number of observations contain data that is 150,000 US Dollars per year, and some small number of respondents have an income at the right-tail end of 250,000 US Dollars per year which serves as a maximum for this dataset, with a minimum of 0. This data could either be viewed as an abnormal right skew, or possibly even bimodal data. 

For the ages we see a roughly normal distribution with a median/mode/mean around the 40-50 range. The extreme values are around 20 and 80, the min and max for the dataset.



```r
# c Give the frequencies (in table format or similar) for Gender, Work Status, and Occupation. They can be separate tables, if that's your choice.

ProcrastinationHdiData_18_or_older
```

```
##            Country  Age Gender     Kids    Edu WorkStatus Income
## 1        Argentina 45.0   Male Yes Kids    deg  full-time  55000
## 2        Australia 45.0   Male Yes Kids    deg  full-time  67500
## 3        Australia 37.5   Male Yes Kids    deg  full-time  55000
## 4        Australia 37.5   Male Yes Kids    deg  full-time 150000
## 5        Australia 45.0   Male Yes Kids    deg  full-time  87500
## 6        Australia 24.0 Female Yes Kids   high  part-time  25000
## 7        Australia 32.5   Male Yes Kids    phd  full-time  67500
## 8        Australia 45.0   Male Yes Kids    deg  full-time 150000
## 9        Australia 32.5 Female Yes Kids     ma  full-time  67500
## 10       Australia 45.0 Female Yes Kids    deg  full-time  55000
## 11       Australia 55.0   Male Yes Kids    phd  full-time  55000
## 12       Australia 45.0   Male Yes Kids   high  full-time 150000
## 13       Australia 45.0   Male Yes Kids  ltuni  full-time  87500
## 14       Australia 45.0 Female Yes Kids lthigh  full-time  55000
## 15       Australia 37.5   Male Yes Kids  ltuni  part-time  45000
## 16       Australia 37.5 Female Yes Kids    deg  full-time  45000
## 17       Australia 55.0 Female Yes Kids    deg  full-time  87500
## 18       Australia 37.5 Female Yes Kids    deg  part-time  67500
## 19       Australia 37.5   Male Yes Kids     ma  full-time 150000
## 21         Bermuda 37.5   Male Yes Kids    deg  full-time 150000
## 22         Bolivia 45.0   Male Yes Kids    deg  part-time  35000
## 23          Brazil 37.5   Male Yes Kids    phd  full-time 150000
## 24          Brazil 45.0 Female Yes Kids    deg  full-time  15000
## 25          Canada 37.5 Female Yes Kids     ma  full-time  87500
## 26          Canada 67.5   Male Yes Kids    deg  full-time  87500
## 27          Canada 32.5   Male Yes Kids    phd    student  25000
## 28          Canada 32.5   Male Yes Kids    phd    student  25000
## 29          Canada 37.5 Female Yes Kids  ltuni  full-time  45000
## 30          Canada 67.5 Female Yes Kids  ltuni    retired  87500
## 31          Canada 28.0   Male Yes Kids    deg  full-time  67500
## 32          Canada 45.0   Male Yes Kids    deg  part-time  25000
## 33          Canada 55.0   Male Yes Kids    deg  full-time  55000
## 34          Canada 55.0   Male Yes Kids    deg  full-time 150000
## 35          Canada 55.0 Female Yes Kids     ma  full-time  87500
## 36          Canada 55.0   Male Yes Kids    phd  full-time  55000
## 37          Canada 55.0   Male Yes Kids    deg  full-time  87500
## 38          Canada 55.0   Male Yes Kids     ma  part-time  67500
## 39          Canada 55.0   Male Yes Kids    phd  full-time  87500
## 40          Canada 37.5 Female Yes Kids  ltuni  full-time  55000
## 41          Canada 37.5   Male Yes Kids  ltuni  full-time  45000
## 42          Canada 37.5 Female Yes Kids    dip unemployed     NA
## 43          Canada 45.0 Female Yes Kids  ltuni  full-time  45000
## 44          Canada 55.0   Male Yes Kids    dip  part-time  15000
## 45          Canada 55.0 Female Yes Kids  ltuni  full-time  67500
## 46          Canada 28.0   Male Yes Kids   high  full-time  67500
## 47          Canada 37.5   Male Yes Kids    dip  full-time  87500
## 48          Canada 55.0   Male Yes Kids    dip  full-time  45000
## 49          Canada 45.0 Female Yes Kids  ltuni  part-time  35000
## 50          Canada 37.5 Female Yes Kids    deg  full-time  67500
## 51          Canada 55.0   Male Yes Kids     ma  full-time  87500
## 52          Canada 55.0 Female Yes Kids    phd  full-time  87500
## 53          Canada 55.0   Male Yes Kids     ma  full-time  25000
## 54          Canada 55.0   Male Yes Kids    phd  full-time  67500
## 55          Canada 67.5   Male Yes Kids  ltuni    retired  45000
## 56          Canada 37.5   Male Yes Kids    deg  full-time  87500
## 57          Canada 55.0 Female Yes Kids    deg  full-time  55000
## 58          Canada 55.0 Female Yes Kids  ltuni  full-time  55000
## 59          Canada 45.0 Female Yes Kids    deg  part-time     NA
## 60           China 28.0   Male Yes Kids     ma  full-time  10000
## 61         Croatia 45.0 Female Yes Kids    deg  part-time     NA
## 62         Denmark 45.0   Male Yes Kids     ma  full-time  67500
## 63         Denmark 45.0 Female Yes Kids  ltuni  full-time  55000
## 64         Ecuador 37.5   Male Yes Kids    dip  full-time  10000
## 65          France 45.0   Male Yes Kids     ma  full-time 150000
## 66         Germany 37.5   Male Yes Kids     ma  full-time 150000
## 67         Germany 55.0   Male Yes Kids     ma  full-time  67500
## 68          Greece 37.5   Male Yes Kids   high  full-time  25000
## 69          Greece 67.5   Male Yes Kids    phd    retired  25000
## 70           India 32.5   Male Yes Kids     ma  full-time  10000
## 71           India 32.5   Male Yes Kids     ma  full-time  35000
## 72           India 32.5   Male Yes Kids     ma  full-time  55000
## 73           India 45.0   Male Yes Kids    phd  full-time 150000
## 74           India 45.0   Male Yes Kids  ltuni  full-time     NA
## 75           India 32.5   Male Yes Kids     ma  full-time     NA
## 76           India 45.0   Male Yes Kids    deg  part-time  87500
## 77         Ireland 67.5   Male Yes Kids   high    retired  45000
## 78         Ireland 67.5   Male Yes Kids     ma    retired  35000
## 79         Ireland 37.5 Female Yes Kids lthigh  full-time     NA
## 80          Israel 55.0 Female Yes Kids    deg  full-time     NA
## 81          Israel 67.5   Male Yes Kids    deg    retired  35000
## 82           Italy 45.0   Male Yes Kids    deg  full-time 250000
## 83           Italy 67.5   Male Yes Kids    phd  full-time 250000
## 84           Italy 45.0   Male Yes Kids     ma  full-time  55000
## 85           Italy 55.0   Male Yes Kids    deg  full-time  67500
## 86           Italy 67.5   Male Yes Kids     ma    retired  67500
## 87           Italy 37.5 Female Yes Kids    phd  part-time 250000
## 88           Italy 55.0   Male Yes Kids     ma  full-time 150000
## 89           Italy 45.0 Female Yes Kids     ma  full-time  25000
## 90           Italy 37.5   Male Yes Kids    deg  full-time  55000
## 91           Italy 37.5   Male Yes Kids    deg  full-time     NA
## 92         Jamaica 67.5 Female Yes Kids    dip  full-time  25000
## 93           Japan 45.0   Male Yes Kids     ma  full-time 250000
## 94        Malaysia 32.5   Male Yes Kids    phd  full-time  45000
## 95          Mexico 67.5 Female Yes Kids     ma  part-time  35000
## 96          Mexico 45.0   Male Yes Kids    deg  full-time 150000
## 97          Mexico 45.0 Female Yes Kids    deg  full-time  25000
## 98     Netherlands 55.0 Female Yes Kids  ltuni unemployed  15000
## 99     Netherlands 37.5   Male Yes Kids     ma  full-time  55000
## 100    New Zealand 32.5 Female Yes Kids  ltuni  part-time  15000
## 101         Norway 45.0   Male Yes Kids     ma unemployed  87500
## 102         Norway 28.0 Female Yes Kids    dip  full-time  55000
## 103       Pakistan 37.5   Male Yes Kids     ma  full-time  10000
## 104    Philippines 45.0 Female Yes Kids    dip  full-time  87500
## 105    Philippines 28.0 Female Yes Kids  ltuni unemployed  10000
## 106         Poland 32.5   Male Yes Kids     ma  full-time     NA
## 107       Portugal 28.0 Female Yes Kids    phd  full-time  15000
## 108       Portugal 32.5 Female Yes Kids     ma  part-time  10000
## 109    South Korea 45.0 Female Yes Kids     ma  full-time  45000
## 110          Spain 37.5 Female Yes Kids    deg  full-time  35000
## 111         Sweden 45.0   Male Yes Kids    deg  full-time  55000
## 112    Switzerland 55.0   Male Yes Kids    phd  full-time 250000
## 113    Switzerland 45.0 Female Yes Kids    dip  full-time 150000
## 114    Switzerland 55.0 Female Yes Kids  ltuni  full-time  67500
## 115    Switzerland 80.0   Male Yes Kids    phd    retired  87500
## 116       Thailand 67.5   Male Yes Kids  ltuni    retired  45000
## 117 United Kingdom 45.0   Male Yes Kids    dip  full-time     NA
## 118 United Kingdom 37.5 Female Yes Kids     ma  part-time  10000
## 119 United Kingdom 45.0   Male Yes Kids    phd  full-time  55000
## 120 United Kingdom 45.0   Male Yes Kids     ma  full-time 150000
## 121 United Kingdom 55.0 Female Yes Kids   high    retired  10000
## 122 United Kingdom 45.0   Male Yes Kids    deg  full-time  87500
## 123 United Kingdom 45.0 Female Yes Kids  grade  full-time  35000
## 124 United Kingdom 37.5 Female Yes Kids     ma  part-time  45000
## 125 United Kingdom 45.0 Female Yes Kids    deg  part-time  35000
## 126 United Kingdom 45.0 Female Yes Kids    dip  part-time  25000
## 127 United Kingdom 45.0 Female Yes Kids     ma unemployed  15000
## 128 United Kingdom 37.5 Female Yes Kids     ma unemployed  10000
## 129 United Kingdom 28.0   Male Yes Kids   high  full-time  55000
## 130 United Kingdom 55.0   Male Yes Kids     ma  part-time  10000
## 131 United Kingdom 45.0   Male Yes Kids     ma  full-time 250000
## 132 United Kingdom 45.0   Male Yes Kids    deg  full-time  67500
## 133 United Kingdom 45.0   Male Yes Kids    dip  full-time  55000
## 134 United Kingdom 45.0   Male Yes Kids    deg  full-time 250000
## 135 United Kingdom 55.0   Male Yes Kids     ma  full-time  87500
## 136 United Kingdom 67.5   Male Yes Kids    deg    retired  55000
## 137 United Kingdom 55.0   Male Yes Kids    dip  full-time  67500
## 138 United Kingdom 32.5 Female Yes Kids    deg unemployed  10000
## 139 United Kingdom 55.0 Female Yes Kids   high  full-time  15000
## 140 United Kingdom 45.0   Male Yes Kids    deg  full-time  55000
## 141 United Kingdom 55.0   Male Yes Kids     ma  full-time  35000
## 142 United Kingdom 55.0   Male Yes Kids  ltuni unemployed  25000
## 143 United Kingdom 45.0 Female Yes Kids     ma  full-time  67500
## 144  United States 28.0 Female Yes Kids    dip  full-time  45000
## 145  United States 55.0 Female Yes Kids    deg  full-time  45000
## 146  United States 55.0 Female Yes Kids    deg  full-time  35000
## 147  United States 80.0 Female Yes Kids     ma    retired  45000
## 148  United States 32.5   Male Yes Kids  ltuni  full-time  45000
## 149  United States 55.0 Female Yes Kids    deg unemployed 250000
## 150  United States 45.0 Female Yes Kids    phd  full-time 150000
## 151  United States 45.0 Female Yes Kids     ma  full-time  25000
## 152  United States 45.0 Female Yes Kids    deg unemployed     NA
## 153  United States 45.0   Male Yes Kids    phd  full-time  67500
## 154  United States 45.0   Male Yes Kids    phd  full-time  87500
## 155  United States 55.0   Male Yes Kids     ma  full-time  67500
## 156  United States 67.5 Female Yes Kids     ma    retired 250000
## 157  United States 45.0   Male Yes Kids    phd  full-time 150000
## 158  United States 55.0 Female Yes Kids    phd  full-time  67500
## 159  United States 37.5 Female Yes Kids    deg    student  10000
## 160  United States 55.0 Female Yes Kids     ma  part-time 250000
## 161  United States 55.0   Male Yes Kids     ma  full-time  45000
## 162  United States 45.0 Female Yes Kids    deg  part-time  25000
## 163  United States 37.5 Female Yes Kids    phd  part-time  67500
## 164  United States 32.5 Female Yes Kids     ma  part-time  35000
## 165  United States 45.0   Male Yes Kids   high  full-time  25000
## 166  United States 55.0   Male Yes Kids    dip  full-time 150000
## 167  United States 37.5   Male Yes Kids     ma  full-time 150000
## 168  United States 32.5   Male Yes Kids  ltuni  full-time  45000
## 169  United States 32.5 Female Yes Kids    dip  part-time  15000
## 170  United States 55.0   Male Yes Kids     ma  full-time  45000
## 171  United States 55.0 Female Yes Kids  ltuni  full-time  25000
## 172  United States 45.0 Female Yes Kids     ma unemployed 150000
## 173  United States 32.5 Female Yes Kids     ma  full-time  87500
## 174  United States 55.0   Male Yes Kids     ma  full-time  45000
## 175  United States 55.0 Female Yes Kids     ma  full-time 150000
## 176  United States 55.0 Female Yes Kids  ltuni  part-time     NA
## 177  United States 45.0 Female Yes Kids     ma  full-time 150000
## 178  United States 45.0   Male Yes Kids    deg  full-time 150000
## 179  United States 55.0   Male Yes Kids  ltuni  full-time  55000
## 180  United States 55.0   Male Yes Kids    deg  full-time 150000
## 181  United States 32.5 Female Yes Kids    deg unemployed  10000
## 182  United States 37.5 Female Yes Kids    deg  part-time  35000
## 183  United States 55.0 Female Yes Kids    dip  full-time  35000
## 184  United States 32.5 Female Yes Kids     ma  full-time  45000
## 185  United States 55.0 Female Yes Kids    deg  full-time 150000
## 186  United States 37.5   Male Yes Kids    dip  full-time  67500
## 187  United States 45.0 Female Yes Kids    deg  full-time  87500
## 188  United States 28.0 Female Yes Kids  ltuni    student     NA
## 189  United States 32.5 Female Yes Kids    deg  full-time 150000
## 190  United States 67.5 Female Yes Kids     ma  part-time  55000
## 191  United States 32.5 Female Yes Kids    deg  full-time 150000
## 192  United States 32.5        Yes Kids    phd  full-time 150000
## 193  United States 45.0   Male Yes Kids    phd  full-time 150000
## 194  United States 32.5 Female Yes Kids  ltuni unemployed  67500
## 195  United States 37.5   Male Yes Kids    phd  full-time  45000
## 196  United States 67.5   Male Yes Kids    phd  full-time  87500
## 197  United States 45.0 Female Yes Kids    deg  full-time  35000
## 198  United States 37.5 Female Yes Kids  ltuni  full-time     NA
## 199  United States 80.0   Male Yes Kids     ma    retired     NA
## 200  United States 37.5 Female Yes Kids    phd  full-time  45000
## 201  United States 55.0   Male Yes Kids     ma  full-time  45000
## 202  United States 45.0   Male Yes Kids  ltuni  full-time 150000
## 203  United States 67.5 Female Yes Kids    deg    retired  25000
## 204  United States 45.0 Female Yes Kids  ltuni  full-time  67500
## 205  United States 67.5   Male Yes Kids    phd  part-time     NA
## 206  United States 55.0 Female Yes Kids  ltuni  full-time  35000
## 207  United States 55.0   Male Yes Kids     ma  full-time 150000
## 208  United States 45.0 Female Yes Kids  ltuni  full-time     NA
## 209  United States 55.0 Female Yes Kids     ma  full-time  55000
## 210  United States 67.5 Female Yes Kids    deg  full-time  55000
## 211  United States 45.0   Male Yes Kids  ltuni  full-time 150000
## 212  United States 45.0   Male Yes Kids    deg  full-time  67500
## 213  United States 32.5   Male Yes Kids    deg  full-time  87500
## 214  United States 37.5 Female Yes Kids   high unemployed  10000
## 215  United States 45.0 Female Yes Kids  ltuni  full-time  87500
## 216  United States 55.0 Female Yes Kids    deg unemployed     NA
## 217  United States 55.0   Male Yes Kids    phd  full-time  55000
## 218  United States 45.0 Female Yes Kids    deg  full-time  25000
## 219  United States 55.0   Male Yes Kids   high  full-time  15000
## 220  United States 55.0 Female Yes Kids  ltuni  full-time  35000
## 221  United States 45.0   Male Yes Kids     ma  full-time 250000
## 222  United States 67.5   Male Yes Kids    phd    retired 150000
## 223  United States 55.0 Female Yes Kids    deg  full-time  45000
## 224  United States 55.0 Female Yes Kids    dip  full-time  87500
## 225  United States 28.0   Male Yes Kids   high  full-time 150000
## 226  United States 55.0   Male Yes Kids     ma  full-time 150000
## 227  United States 67.5 Female Yes Kids     ma  part-time  35000
## 228  United States 55.0 Female Yes Kids    dip unemployed  87500
## 229  United States 55.0   Male Yes Kids    phd  full-time 150000
## 230  United States 37.5 Female Yes Kids  ltuni  full-time  55000
## 231  United States 37.5 Female Yes Kids     ma  part-time  25000
## 232  United States 45.0 Female Yes Kids    phd  full-time 150000
## 233  United States 37.5 Female Yes Kids    deg  full-time 250000
## 234  United States 37.5   Male Yes Kids     ma  full-time 150000
## 235  United States 80.0 Female Yes Kids  ltuni    retired  25000
## 236  United States 32.5   Male Yes Kids    deg  full-time  55000
## 237  United States 45.0 Female Yes Kids     ma    student  10000
## 238  United States 55.0   Male Yes Kids     ma  full-time  87500
## 239  United States 45.0 Female Yes Kids     ma  full-time     NA
## 240  United States 37.5 Female Yes Kids     ma                NA
## 241  United States 55.0 Female Yes Kids    phd    retired  55000
## 242  United States 55.0 Female Yes Kids    phd  full-time  45000
## 243  United States 32.5 Female Yes Kids  ltuni unemployed 250000
## 244  United States 55.0   Male Yes Kids     ma  full-time     NA
## 245  United States 67.5   Male Yes Kids  ltuni    retired     NA
## 246  United States 45.0   Male Yes Kids  ltuni  full-time  67500
## 247  United States 55.0 Female Yes Kids    phd    student  45000
## 248  United States 37.5   Male Yes Kids    phd  full-time  67500
## 249  United States 55.0   Male Yes Kids    phd  full-time 150000
## 250  United States 80.0 Female Yes Kids  ltuni    retired     NA
## 251  United States 55.0   Male Yes Kids    phd  full-time  87500
## 252  United States 45.0   Male Yes Kids    phd  full-time  67500
## 253  United States 37.5 Female Yes Kids     ma  full-time 150000
## 254  United States 37.5 Female Yes Kids    deg unemployed 150000
## 255  United States 55.0 Female Yes Kids    deg  part-time  87500
## 256  United States 67.5   Male Yes Kids  ltuni unemployed  55000
## 257  United States 37.5   Male Yes Kids     ma  full-time  55000
## 258  United States 67.5 Female Yes Kids    phd  full-time 150000
## 259  United States 55.0 Female Yes Kids    phd unemployed  35000
## 260  United States 55.0 Female Yes Kids    deg  full-time  35000
## 261  United States 32.5 Female Yes Kids  ltuni  full-time  15000
## 262  United States 55.0 Female Yes Kids    phd  full-time  67500
## 263  United States 55.0 Female Yes Kids     ma  full-time 150000
## 264  United States 45.0 Female Yes Kids    deg    retired     NA
## 265  United States 55.0   Male Yes Kids    phd  full-time 150000
## 266  United States 55.0 Female Yes Kids    phd  part-time  67500
## 267  United States 45.0   Male Yes Kids    deg unemployed 150000
## 268  United States 45.0 Female Yes Kids    deg  full-time  67500
## 269  United States 45.0   Male Yes Kids     ma  full-time 250000
## 270  United States 45.0   Male Yes Kids     ma  full-time  67500
## 271  United States 37.5   Male Yes Kids     ma    student  55000
## 272  United States 45.0 Female Yes Kids   high  full-time  35000
## 273  United States 28.0 Female Yes Kids lthigh unemployed     NA
## 274  United States 45.0   Male Yes Kids     ma  full-time  67500
## 275  United States 45.0 Female Yes Kids     ma  full-time  67500
## 276  United States 55.0   Male Yes Kids    phd  full-time 250000
## 277  United States 45.0   Male Yes Kids     ma  full-time 150000
## 278  United States 45.0 Female Yes Kids     ma  part-time  55000
## 279  United States 55.0 Female Yes Kids    deg  full-time  55000
## 280  United States 45.0   Male Yes Kids    phd  full-time  67500
## 281  United States 55.0   Male Yes Kids    phd  full-time 250000
## 282  United States 45.0 Female Yes Kids     ma  full-time  55000
## 283  United States 32.5   Male Yes Kids    phd  full-time  55000
## 284  United States 45.0   Male Yes Kids    deg  full-time  87500
## 285  United States 45.0   Male Yes Kids    phd  full-time  55000
## 286  United States 37.5 Female Yes Kids    phd  full-time 150000
## 287  United States 55.0 Female Yes Kids    phd unemployed  67500
## 288  United States 45.0 Female Yes Kids    deg  full-time  45000
## 289  United States 45.0 Female Yes Kids     ma  full-time 150000
## 290  United States 55.0 Female Yes Kids    deg  full-time  67500
## 291  United States 45.0 Female Yes Kids  ltuni  part-time  25000
## 292  United States 55.0 Female Yes Kids     ma  full-time  55000
## 293  United States 55.0   Male Yes Kids    deg  full-time  45000
## 294  United States 45.0 Female Yes Kids    deg unemployed 150000
## 295  United States 45.0   Male Yes Kids    phd  full-time 250000
## 296  United States 25.0   Male Yes Kids    deg unemployed  15000
## 297  United States 55.0 Female Yes Kids    phd  full-time  55000
## 298  United States 67.5 Female Yes Kids     ma  full-time  87500
## 299  United States 55.0 Female Yes Kids     ma  full-time 150000
## 300  United States 32.5 Female Yes Kids     ma  full-time  35000
## 301  United States 45.0   Male Yes Kids    phd  full-time  87500
## 302  United States 55.0 Female Yes Kids    dip  part-time  15000
## 303  United States 55.0 Female Yes Kids    deg  full-time  67500
## 304  United States 45.0   Male Yes Kids    deg  full-time 150000
## 305  United States 37.5 Female Yes Kids    deg  full-time  45000
## 306  United States 45.0 Female Yes Kids     ma    retired     NA
## 307  United States 45.0 Female Yes Kids     ma  full-time  87500
## 308  United States 45.0   Male Yes Kids    phd  full-time 150000
## 309  United States 80.0 Female Yes Kids     ma    retired  35000
## 310  United States 45.0   Male Yes Kids    phd  full-time     NA
## 311  United States 67.5   Male Yes Kids    deg  part-time  45000
## 312  United States 45.0   Male Yes Kids    deg  full-time  45000
## 313  United States 45.0 Female Yes Kids    deg  full-time  55000
## 314  United States 55.0 Female Yes Kids     ma  full-time 150000
## 315  United States 55.0 Female Yes Kids     ma  full-time  87500
## 316  United States 45.0 Female Yes Kids    deg  full-time  35000
## 317  United States 37.5   Male Yes Kids    deg  full-time  45000
## 318  United States 28.0   Male Yes Kids  ltuni  part-time  15000
## 319  United States 37.5   Male Yes Kids    phd  full-time  87500
## 320  United States 45.0 Female Yes Kids    phd  full-time 150000
## 321  United States 45.0 Female Yes Kids  ltuni  full-time  25000
## 322  United States 67.5   Male Yes Kids   high    retired  10000
## 323  United States 55.0 Female Yes Kids     ma  full-time  87500
## 324  United States 45.0   Male Yes Kids    deg  full-time 150000
## 325  United States 55.0 Female Yes Kids    deg  full-time 150000
## 326  United States 55.0   Male Yes Kids  ltuni  full-time 250000
## 327  United States 45.0   Male Yes Kids    phd  full-time 150000
## 328  United States 28.0 Female Yes Kids  ltuni  part-time  15000
## 329  United States 32.5 Female Yes Kids    deg  full-time  55000
## 330  United States 67.5 Female Yes Kids  ltuni  full-time  45000
## 331  United States 80.0   Male Yes Kids    deg    retired  67500
## 332  United States 32.5   Male Yes Kids     ma    student  45000
## 333  United States 67.5   Male Yes Kids    phd    retired 250000
## 334  United States 45.0   Male Yes Kids    phd  full-time  55000
## 335  United States 55.0   Male Yes Kids    deg  full-time 150000
## 336  United States 45.0 Female Yes Kids    phd  part-time  35000
## 337  United States 45.0   Male Yes Kids    phd unemployed  10000
## 338  United States 55.0 Female Yes Kids   high  full-time  35000
## 339  United States 55.0   Male Yes Kids  ltuni  full-time  87500
## 340  United States 67.5   Male Yes Kids  ltuni  part-time  15000
## 341  United States 55.0   Male Yes Kids  ltuni  full-time 150000
## 342  United States 67.5 Female Yes Kids    phd  full-time  67500
## 343  United States 45.0 Female Yes Kids    phd  full-time  67500
## 344  United States 45.0 Female Yes Kids    deg  full-time  87500
## 345  United States 67.5   Male Yes Kids    phd  full-time  87500
## 346  United States 55.0   Male Yes Kids    phd  full-time  87500
## 347  United States 55.0 Female Yes Kids     ma  full-time  67500
## 348  United States 28.0 Female Yes Kids    deg  full-time  35000
## 349  United States 55.0 Female Yes Kids    phd unemployed  87500
## 350  United States 37.5 Female Yes Kids    phd  full-time 150000
## 351  United States 55.0 Female Yes Kids    deg  part-time  10000
## 352  United States 67.5   Male Yes Kids     ma    retired  67500
## 353  United States 55.0 Female Yes Kids    deg  full-time  35000
## 354  United States 45.0 Female Yes Kids     ma    student  15000
## 355  United States 55.0   Male Yes Kids    phd    retired  25000
## 356  United States 45.0   Male Yes Kids    phd  full-time  55000
## 357  United States 67.5 Female Yes Kids  ltuni    retired  35000
## 358  United States 55.0   Male Yes Kids    deg  full-time 150000
## 359  United States 45.0   Male Yes Kids    phd  full-time  67500
## 360  United States 55.0   Male Yes Kids    dip  full-time  35000
## 361  United States 55.0   Male Yes Kids    deg  full-time 150000
## 362  United States 37.5 Female Yes Kids  ltuni  full-time  25000
## 363  United States 55.0   Male Yes Kids  ltuni  full-time     NA
## 364  United States 55.0   Male Yes Kids    phd  full-time  45000
## 365  United States 55.0 Female Yes Kids    deg unemployed 250000
## 366  United States 67.5 Female Yes Kids    deg  part-time  35000
## 367  United States 32.5 Female Yes Kids    deg unemployed  87500
## 368  United States 67.5 Female Yes Kids    deg    retired  67500
## 369  United States 45.0 Female Yes Kids    deg  full-time     NA
## 370  United States 37.5   Male Yes Kids     ma  full-time  87500
## 371  United States 55.0 Female Yes Kids  ltuni    student  35000
## 372  United States 45.0 Female Yes Kids     ma  full-time  55000
## 373  United States 80.0 Female Yes Kids     ma    retired 150000
## 374  United States 55.0 Female Yes Kids  ltuni    retired     NA
## 375  United States 80.0 Female Yes Kids  ltuni    retired  45000
## 376  United States 45.0 Female Yes Kids    deg  full-time  67500
## 377  United States 28.0 Female Yes Kids  ltuni  full-time  35000
## 378  United States 37.5 Female Yes Kids    phd unemployed  10000
## 379  United States 45.0   Male Yes Kids    deg  full-time 150000
## 380  United States 55.0 Female Yes Kids    deg    retired 150000
## 381  United States 37.5   Male Yes Kids  ltuni  full-time 150000
## 382  United States 55.0   Male Yes Kids    phd  full-time 250000
## 383  United States 55.0 Female Yes Kids     ma  full-time  45000
## 384  United States 45.0 Female Yes Kids    deg  part-time     NA
## 385  United States 37.5   Male Yes Kids    dip  full-time  55000
## 386  United States 45.0   Male Yes Kids    deg  full-time  67500
## 387  United States 45.0 Female Yes Kids    deg  part-time  67500
## 388  United States 32.5 Female Yes Kids     ma  full-time  35000
## 389  United States 45.0 Female Yes Kids     ma  full-time  55000
## 390  United States 37.5 Female Yes Kids    deg  full-time 150000
## 391  United States 45.0   Male Yes Kids    deg  full-time  87500
## 392  United States 67.5   Male Yes Kids         full-time  45000
## 393  United States 55.0 Female Yes Kids     ma  full-time  55000
## 394  United States 45.0 Female Yes Kids  ltuni  part-time  15000
## 395  United States 67.5   Male Yes Kids     ma  full-time  55000
## 396  United States 67.5 Female Yes Kids     ma  full-time  67500
## 397  United States 45.0 Female Yes Kids           retired 250000
## 398  United States 45.0   Male Yes Kids     ma  full-time 150000
## 399  United States 55.0   Male Yes Kids    deg    retired  45000
## 400  United States 32.5 Female Yes Kids  ltuni  full-time  45000
## 401  United States 55.0 Female Yes Kids    dip  part-time  87500
## 402  United States 45.0 Female Yes Kids    deg  full-time 150000
## 403  United States 55.0 Female Yes Kids    phd  full-time  55000
## 404  United States 55.0 Female Yes Kids    deg  full-time  55000
## 405  United States 32.5 Female Yes Kids     ma  full-time  55000
## 406  United States 55.0 Female Yes Kids     ma  full-time  67500
## 407  United States 67.5   Male Yes Kids  ltuni    retired  45000
## 408  United States 45.0 Female Yes Kids  ltuni    student  10000
## 409  United States 32.5 Female Yes Kids    deg  full-time  25000
## 410  United States 55.0 Female Yes Kids     ma  full-time  67500
## 411  United States 45.0 Female Yes Kids     ma  part-time     NA
## 412  United States 67.5   Male Yes Kids    phd  full-time  25000
## 413  United States 20.0 Female Yes Kids lthigh    student  25000
## 414  United States 45.0 Female Yes Kids  ltuni  full-time  45000
## 415  United States 45.0   Male Yes Kids  ltuni    retired  45000
## 416  United States 45.0   Male Yes Kids    deg  full-time 150000
## 417  United States 55.0 Female Yes Kids     ma unemployed  45000
## 418  United States 45.0 Female Yes Kids    phd  full-time     NA
## 419  United States 45.0   Male Yes Kids     ma  full-time  45000
## 420  United States 45.0   Male Yes Kids    deg  full-time 150000
## 421  United States 55.0 Female Yes Kids   high    retired  55000
## 422  United States 28.0 Female Yes Kids    deg  full-time  55000
## 423  United States 55.0 Female Yes Kids    deg unemployed  10000
## 424  United States 45.0   Male Yes Kids    deg  full-time  45000
## 426  United States 28.0   Male Yes Kids  ltuni  full-time  67500
## 427  United States 45.0 Female Yes Kids     ma  part-time  35000
## 428  United States 55.0 Female Yes Kids    deg  full-time  45000
## 429  United States 45.0 Female Yes Kids     ma  full-time  55000
## 430  United States 32.5   Male Yes Kids    phd  full-time  67500
## 431  United States 55.0 Female Yes Kids    deg            250000
## 432  United States 37.5   Male Yes Kids    phd  full-time  87500
## 433  United States 37.5   Male Yes Kids  ltuni  full-time  15000
## 434  United States 37.5   Male Yes Kids     ma  full-time  87500
## 435  United States 32.5 Female Yes Kids    deg  full-time     NA
## 436  United States 45.0 Female Yes Kids    phd  part-time  25000
## 437  United States 28.0 Female Yes Kids  ltuni  full-time  35000
## 438  United States 32.5   Male Yes Kids    dip  full-time  87500
## 439  United States 37.5   Male Yes Kids    deg  full-time  55000
## 440  United States 55.0 Female Yes Kids    phd unemployed  25000
## 441  United States 55.0   Male Yes Kids   high  full-time  25000
## 442  United States 45.0 Female Yes Kids    phd  part-time  25000
## 443  United States 45.0   Male Yes Kids    deg  full-time  67500
## 444  United States 55.0   Male Yes Kids         full-time 150000
## 445  United States 55.0 Female Yes Kids    phd  full-time  87500
## 446  United States 45.0 Female Yes Kids  ltuni  full-time  35000
## 447  United States 67.5 Female Yes Kids    phd  full-time  45000
## 448  United States 55.0   Male Yes Kids    phd  full-time 150000
## 449  United States 45.0   Male Yes Kids     ma  full-time  87500
## 450  United States 37.5   Male Yes Kids    phd  full-time  45000
## 451  United States 55.0 Female Yes Kids     ma  full-time  67500
## 452  United States 37.5 Female Yes Kids   high unemployed  67500
## 453  United States 32.5   Male Yes Kids    deg  full-time  87500
## 454  United States 55.0 Female Yes Kids   high    retired  15000
## 455  United States 55.0   Male Yes Kids    deg  part-time  87500
## 456  United States 45.0 Female Yes Kids    deg  full-time  35000
## 457  United States 55.0   Male Yes Kids    deg  full-time 150000
## 458  United States 37.5 Female Yes Kids    deg  part-time  25000
## 459  United States 67.5 Female Yes Kids     ma  part-time  45000
## 460  United States 80.0 Female Yes Kids    phd    retired  67500
## 461  United States 37.5   Male Yes Kids    phd  full-time 150000
## 462  United States 32.5 Female Yes Kids    deg  full-time  35000
## 463  United States 45.0 Female Yes Kids    dip  full-time  25000
## 464  United States 45.0 Female Yes Kids    deg  full-time  87500
## 465  United States 32.5 Female Yes Kids    phd  part-time  35000
## 466  United States 80.0   Male Yes Kids     ma    retired  55000
## 467  United States 55.0   Male Yes Kids    phd  full-time 150000
## 468  United States 45.0 Female Yes Kids    deg  full-time  45000
## 469  United States 67.5   Male Yes Kids    phd    retired  87500
## 470  United States 32.5   Male Yes Kids    phd  full-time 250000
## 471  United States 37.5 Female Yes Kids    phd  full-time  87500
## 472  United States 32.5 Female Yes Kids    dip  full-time  25000
## 473  United States 67.5   Male Yes Kids     ma  full-time 250000
## 474  United States 45.0        Yes Kids    deg  full-time  67500
## 475  United States 55.0 Female Yes Kids  ltuni    retired 150000
## 476  United States 45.0   Male Yes Kids     ma  full-time 150000
## 477  United States 45.0 Female Yes Kids    deg unemployed  87500
## 478  United States 55.0   Male Yes Kids    deg  full-time 150000
## 479  United States 55.0 Female Yes Kids     ma  full-time  67500
## 480  United States 28.0   Male Yes Kids     ma unemployed  10000
## 481  United States 67.5   Male Yes Kids    phd    retired 250000
## 482  United States 55.0 Female Yes Kids  ltuni  full-time  55000
## 483  United States 37.5 Female Yes Kids     ma    student  87500
## 484  United States 45.0   Male Yes Kids    deg  full-time 150000
## 485  United States 55.0 Female Yes Kids    dip unemployed  67500
## 486  United States 45.0 Female Yes Kids    deg  full-time  25000
## 487  United States 45.0 Female Yes Kids     ma  full-time  35000
## 488  United States 55.0 Female Yes Kids    dip    student     NA
## 489  United States 45.0 Female Yes Kids    deg  full-time  45000
## 490  United States 55.0 Female Yes Kids    deg  full-time  67500
## 491  United States 28.0 Female Yes Kids    deg  part-time  25000
## 492  United States 45.0   Male Yes Kids    deg  full-time  45000
## 493  United States 45.0   Male Yes Kids  ltuni  full-time  87500
## 494  United States 37.5 Female Yes Kids     ma  full-time  45000
## 495  United States 45.0   Male Yes Kids    phd  full-time 250000
## 496  United States 32.5   Male Yes Kids     ma  full-time  87500
## 497  United States 55.0 Female Yes Kids    deg  full-time  35000
## 498  United States 55.0 Female Yes Kids    phd  full-time 250000
## 499  United States 45.0 Female Yes Kids     ma  full-time 150000
## 500  United States 55.0   Male Yes Kids    deg  full-time 250000
## 501  United States 37.5 Female Yes Kids     ma  part-time  35000
## 502  United States 45.0   Male Yes Kids    phd  full-time 150000
## 503  United States 45.0 Female Yes Kids    phd  full-time  67500
## 504  United States 45.0   Male Yes Kids     ma  full-time 250000
## 505  United States 37.5 Female Yes Kids    phd  part-time  25000
## 506  United States 45.0 Female Yes Kids     ma  full-time  67500
## 507  United States 45.0   Male Yes Kids     ma  full-time  87500
## 508  United States 55.0   Male Yes Kids  ltuni  full-time 150000
## 509  United States 80.0   Male Yes Kids    deg    retired  87500
## 510  United States 28.0   Male Yes Kids    phd  full-time 150000
## 511  United States 37.5   Male Yes Kids  ltuni  full-time  15000
## 512  United States 45.0 Female Yes Kids   high  full-time  45000
## 513  United States 55.0 Female Yes Kids  ltuni  part-time  15000
## 514  United States 37.5   Male Yes Kids    deg  full-time  87500
## 515  United States 55.0   Male Yes Kids  ltuni    retired  25000
## 516  United States 55.0 Female Yes Kids     ma  full-time  55000
## 517  United States 28.0 Female Yes Kids  ltuni    student  10000
## 518  United States 45.0 Female Yes Kids     ma                NA
## 519  United States 45.0 Female Yes Kids     ma  full-time     NA
## 520  United States 55.0   Male Yes Kids     ma  full-time 150000
## 521  United States 55.0   Male Yes Kids  ltuni  full-time  55000
## 522  United States 55.0   Male Yes Kids     ma  full-time  55000
## 523  United States 25.0 Female Yes Kids     ma unemployed  10000
## 524  United States 55.0 Female Yes Kids  ltuni  full-time  35000
## 525  United States 55.0 Female Yes Kids     ma  part-time 150000
## 526  United States 55.0 Female Yes Kids    dip  full-time  45000
## 527  United States 45.0   Male Yes Kids  ltuni  full-time  25000
## 528  United States 67.5 Female Yes Kids    phd  full-time 150000
## 529  United States 55.0   Male Yes Kids  ltuni  part-time  25000
## 530  United States 67.5 Female Yes Kids   high    retired  55000
## 531  United States 55.0   Male Yes Kids     ma  full-time 150000
## 532  United States 37.5 Female Yes Kids    phd unemployed 150000
## 533  United States 32.5   Male Yes Kids     ma    student  15000
## 534  United States 67.5   Male Yes Kids    phd    retired 250000
## 535  United States 45.0 Female Yes Kids     ma    student     NA
## 536  United States 55.0 Female Yes Kids    dip unemployed 250000
## 537  United States 37.5   Male Yes Kids     ma  part-time 150000
## 538  United States 37.5   Male Yes Kids     ma  part-time  10000
## 539  United States 45.0 Female Yes Kids    deg  full-time 150000
## 540  United States 45.0 Female Yes Kids  ltuni  part-time  67500
## 541  United States 55.0   Male Yes Kids     ma  part-time  10000
## 542  United States 55.0   Male Yes Kids     ma  full-time  55000
## 543  United States 55.0   Male Yes Kids  ltuni    retired 150000
## 544  United States 45.0 Female Yes Kids    phd  full-time  67500
## 545  United States 55.0   Male Yes Kids    deg    retired  67500
## 546  United States 55.0   Male Yes Kids    phd  full-time 150000
## 547  United States 45.0   Male Yes Kids     ma  full-time 250000
## 548  United States 45.0 Female Yes Kids     ma  full-time  67500
## 549  United States 37.5   Male Yes Kids  ltuni  full-time  35000
## 550  United States 67.5 Female Yes Kids    phd  full-time 150000
## 551  United States 32.5   Male Yes Kids    deg  full-time  55000
## 552  United States 67.5 Female Yes Kids  ltuni  full-time  35000
## 553  United States 45.0   Male Yes Kids lthigh  full-time 150000
## 554  United States 45.0   Male Yes Kids    deg  part-time  67500
## 555  United States 67.5 Female Yes Kids     ma  full-time  67500
## 556  United States 32.5 Female Yes Kids     ma  full-time  87500
## 557  United States 28.0 Female Yes Kids  ltuni  full-time  35000
## 558  United States 37.5   Male Yes Kids    phd  full-time  87500
## 559  United States 45.0 Female Yes Kids    phd  full-time 150000
## 560  United States 45.0   Male Yes Kids    phd  full-time 150000
## 561  United States 37.5 Female Yes Kids     ma  full-time  87500
## 562  United States 37.5 Female Yes Kids     ma  part-time  55000
## 563  United States 55.0   Male Yes Kids    phd  part-time  35000
## 564  United States 32.5 Female Yes Kids    phd  full-time  67500
## 565  United States 45.0 Female Yes Kids     ma  full-time 150000
## 566  United States 25.0   Male Yes Kids  ltuni    student  15000
## 567  United States 45.0 Female Yes Kids    phd  full-time 250000
## 568  United States 55.0   Male Yes Kids     ma  full-time  25000
## 569  United States 32.5 Female Yes Kids  ltuni  full-time  25000
## 570      Venezuela 37.5   Male Yes Kids     ma  full-time 150000
##                                   Occupation PositionYrs PositionMnth
## 1                                                      7            0
## 2                             Physiotherapst          13            0
## 3                           Technical Writer           7            6
## 4                                   engineer           9            0
## 5                                 IT Manager          13            0
## 6                           Customer Service           6            2
## 7                                 IT Support           3            0
## 8                                   engineer          10            0
## 9                               veterinarian           7            0
## 10                                                     6            0
## 11                                                     0            0
## 12                                                     1            0
## 13                                                     0            0
## 14                                                     0            0
## 15                                                     3           10
## 16                                                     0            0
## 17                                                     5            0
## 18                                                     0            3
## 19                                                    14            0
## 21                                      <NA>           2            0
## 22                                                     0            0
## 23                                  engineer           8            0
## 24                                Translator          10           10
## 25                             Self Employed           0            8
## 26                                 President          30            0
## 27                                      <NA>           4            2
## 28                                      <NA>           4            2
## 29   Divisional Manager of a large cosmetics           4            5
## 30                                      <NA>           0            0
## 31                    Regional Sales Manager           1            0
## 32            Instructional Assistant Online           3            0
## 33                                 innkeeper          17            0
## 34         Deputy Chieif Information Officer           1           10
## 35                                  engineer          28            0
## 36                         college professor          23            0
## 37                Director,social Dvelopment           3            7
## 38                         Software engineer          17            0
## 39                                                     9            0
## 40                                                     3            6
## 41                                                    14            0
## 42                                                     8            0
## 43                                                     0            0
## 44                                                     6            0
## 45                                                     0            0
## 46                                                     4            0
## 47                                                    10            0
## 48                                                     7           11
## 49                                                    10            0
## 50                                                     1            4
## 51                                                     5            0
## 52                                                     0            0
## 53                                                     1            0
## 54                                                    10            0
## 55                                                    13            0
## 56                                                     2            0
## 57                                                     6            2
## 58                                                     6            0
## 59                                                     0            0
## 60                                                     3            0
## 61                                                    10            0
## 62                                                     1            0
## 63                                                     0            3
## 64                                                     3            0
## 65                                      <NA>           6            0
## 66                          Network Engineer           1            8
## 67                           Quality Manager           2            0
## 68                    airport ground handler           9            0
## 69                                                     0            0
## 70                                 Marketing           2            0
## 71                              Software Pro           2            0
## 72                                 Marketing           1            0
## 73                                                     7            0
## 74                                                     0            0
## 75                                                     9            0
## 76                                                     1            2
## 77                                   retired          10            6
## 78                                                     0            0
## 79                                                     6            0
## 80                                Journalist          23            0
## 81                                      <NA>           0            0
## 82                         Financial Advisor          23            0
## 83                        free professionist          30            0
## 84                                Agronomist          10            0
## 85                                   manager           7            0
## 86                                      <NA>           0            0
## 87                         college professor           4            0
## 88                         college professor          23            0
## 89                    coordinatore operativo          10            0
## 90                  self-employed translator           0            0
## 91                                                    10            0
## 92                                   manager          14            0
## 93                                                     1            0
## 94                                                     3            0
## 95                                                     5            0
## 96                                                     5            0
## 97                                                    10            0
## 98                                  houswife          30            0
## 99                                consultant           7            0
## 100                                                    1            0
## 101                                     <NA>           0            0
## 102                               consultant           1            6
## 103                                                    0            0
## 104                                                    6            3
## 105                                                    3            4
## 106                            HR generalist           8            0
## 107                                                    0            6
## 108                                                   10            0
## 109                                  teacher           5            0
## 110                                                    4            6
## 111                                                    0            0
## 112                                                    0            0
## 113                                                    3            4
## 114                                                    6            0
## 115                                                    0            0
## 116                                     <NA>           0            0
## 117                                     <NA>           5            0
## 118                            Administrator           6            0
## 119                      assistant professor           9            0
## 120                                 business          14            0
## 121                                     <NA>           0            0
## 122                                 engineer           8            0
## 123           treatment support co-ordinator           1            0
## 124                   IT security consultant           3            0
## 125                                  teacher           3            8
## 126                        Executive officer           5            0
## 127                               Journalist           0            1
## 128                                                   12            0
## 129                                                    6            1
## 130                                                   12            0
## 131                                                    6            0
## 132                                                    0            0
## 133                                                    6            0
## 134                                                    1            6
## 135                                                    1            0
## 136                                                    1            0
## 137                                                    5            0
## 138                                                    1            2
## 139                                                    0            6
## 140                                                    0            6
## 141                                                    1            0
## 142                                                    0            6
## 143                                                    0            0
## 144                special education teacher          10            0
## 145                        election services          23            0
## 146                                  manager          13            0
## 147                                     <NA>           0            0
## 148                        Computer Operator           5            4
## 149                                 houswife          23            0
## 150                                     <NA>           3            0
## 151                            acupuncturist           5            8
## 152                               home maker          17            0
## 153                      assistant professor           4            5
## 154                                Scientist           8            0
## 155               Labor Relations Specialist           3            0
## 156                                     <NA>           0            0
## 157     First VP & Associate General Counsel           1            7
## 158                                  teacher          17            0
## 159                                     <NA>           1            8
## 160                           Business Owner           1            8
## 161              Pastor ; Life coach  clergy           7            0
## 162                                  teacher           5            0
## 163                                      VMD          13            0
## 164                                    buyer           7            3
## 165                       landscape designer          10            0
## 166                                     <NA>          17            0
## 167                                Economist           8            0
## 168                              Bank Teller           3            3
## 169                   Professional Organizer           1            5
## 170                                Marketing           8            1
## 171                            Administrator           8            0
## 172                                 houswife           9            7
## 173                                  Analyst           4            9
## 174                                Librarian           3            6
## 175                                    Nurse          28            0
## 176                            museum docent           3            0
## 177                                  teacher           6            0
## 178                               Publishing          17            0
## 179                        maintenance tech.          28            0
## 180                           Communications           2            6
## 181                                 houswife           2            0
## 182                                    Nurse          13            5
## 183                     training Coordinator           4            0
## 184                          law enforcement           0            6
## 185                            Administrator          12            3
## 186                                       RN           6            0
## 187 owner - private practice physical therap          23            0
## 188                                     <NA>           0            0
## 189                                President           2            0
## 190                                    Tutor           7            0
## 191                         Network Engineer           1            0
## 192                                Scientist           3            0
## 193                                 engineer           2            6
## 194                                     <NA>           0            0
## 195                                Scientist           3            8
## 196                         Program Director           0            7
## 197                         Tech Analyst/GIS           3            0
## 198                                     <NA>           4            0
## 199                                     <NA>           3            0
## 200                        college professor           6            0
## 201                                     <NA>           4            0
## 202                                 engineer           0            5
## 203                                  retired          10            2
## 204                  Food Service Supervisor          17            0
## 205                                     <NA>           4            0
## 206                            Administrator           3            0
## 207                                 Diplomat          17            0
## 208                   Human Resource Manager           1            3
## 209                                  teacher          30            0
## 210                    laboratory technician           1            0
## 211                                Marketing           3            8
## 212                special education teacher          10            0
## 213                          project manager           0            9
## 214                               home maker          14            0
## 215                                  realtor          17            0
## 216                                                    0            0
## 217                              psychologis           9            0
## 218             Juvenile Corrections Officer          12            8
## 219                                  stocker           6            7
## 220                      Account Service Rep           5            3
## 221                                     <NA>           2            0
## 222                        college professor           4            0
## 223                                Librarian          10            0
## 224                                    Nurse          17            0
## 225                            Self Employed           4            0
## 226                                 Attorney          17            0
## 227                          psychotherapist          17            0
## 228                                 houswife          23            0
## 229                   In-house Legal Counsel           4            6
## 230                      Legislation Analyst           3            0
## 231                            Social Worker           4            5
## 232                        college professor          13            0
## 233          Vice President / program office           3            0
## 234                       Associate Director           1            0
## 235                                     <NA>           0            0
## 236                                     <NA>          10            0
## 237                                     <NA>           0            0
## 238                  Social Media consultant           0            5
## 239                                  teacher           1            0
## 240                                 houswife           1            1
## 241                                     <NA>           5            0
## 242                             chiropractor           5            0
## 243                                 houswife           6            3
## 244  P-T College Faculty & P-T Self-Employed          28            0
## 245                                     <NA>           0            0
## 246                             Web Designer           1            4
## 247                          retired/adjunct           1            0
## 248                       university faculty           0            8
## 249                                     <NA>          28            0
## 250                                  retired           0            0
## 251                                 Attorney          28            0
## 252                                Scientist           6            2
## 253                                      ceo           1            0
## 254                                     <NA>           0            0
## 255                          writer/musician          14            0
## 256                                 engineer          23            0
## 257              Pastor ; Life coach  clergy          10            0
## 258                        Doctor; Physician          28            0
## 259                               Unemployed           2            0
## 260                                Geologist           4            0
## 261                       Library technician           5            7
## 262                                  teacher           1            3
## 263                     Grants Administrator           5            0
## 264                                 houswife          14            0
## 265                                 attorney          28            0
## 266         Medical / Public Health Educator           6            0
## 267                                     <NA>           0            0
## 268                          Insurance Agent          17            0
## 269                                     <NA>           3            0
## 270 supervising program development speciali           4            0
## 271                                     <NA>           5            6
## 272                            manufacturing          12            0
## 273                                     <NA>           0            0
## 274                       Programmer Analyst          23            0
## 275           writer / lecturer / consultant           3            0
## 276                                       md          30            0
## 277                          Program Manager           2            0
## 278                                  teacher           2            0
## 279                    Real Estate Appraiser          14            0
## 280                        college professor           1            0
## 281                        Doctor; Physician          28            0
## 282                            Administrator           5            0
## 283                                     <NA>           5            0
## 284                                    Nurse          17            0
## 285                                Scientist          10            0
## 286                          Deputy Director           4            0
## 287                               Unemployed           0            4
## 288                                     <NA>           0            7
## 289                                Marketing           2            0
## 290                           Market Analyst          17            0
## 291 financial officer / small career-trainin           3            0
## 292                                  teacher          30            0
## 293                                  teacher          13            0
## 294                               home maker          10            0
## 295                        Doctor; Physician           3            7
## 296                                     <NA>           0            2
## 297                                  teacher           7            0
## 298 Please specify title Manager for Regulat           5            0
## 299                                     <NA>           5            0
## 300                                  teacher           6            0
## 301                        college professor           2            0
## 302                                President          17            0
## 303                       Medical Laboratory          17            0
## 304                                     <NA>          10            0
## 305                        Program Assistant           1            0
## 306                                     <NA>           0            0
## 307                                  teacher          17            0
## 308                                President          10            0
## 309                                     <NA>           0            0
## 310                        college professor           7            0
## 311                   Vetrans Representative           1            9
## 312               Product Field Test Manager           2            0
## 313                                  teacher           6            3
## 314                                President           5            0
## 315                                Counselor          30            0
## 316                          Insurance Agent           1            3
## 317                                Architect          17            0
## 318               Webmaster / Print Designer           0            4
## 319                                 attorney          10            0
## 320                        college professor          14            0
## 321                                 designer          10            0
## 322                                  retired           9            0
## 323                                  teacher          28            0
## 324                                  manager          23            0
## 325                  Chief Financial Officer           5            0
## 326                                     <NA>           7            0
## 327                        Doctor; Physician          17            0
## 328                 Early child hood teacher           2            2
## 329            Speech and language Assistant           3            8
## 330                                 engineer           9            0
## 331                                     <NA>           0            0
## 332                                     <NA>           5            0
## 333                                     <NA>           0            0
## 334                         IT Administrator           1            2
## 335 Executive Vice President / Senior Lender           2            4
## 336                                 Attorney          13            0
## 337                                     <NA>           2            0
## 338                         Graphic Designer           9            3
## 339             Plant Engineering Supervisor          17            0
## 340                                chauffeur          17            0
## 341                    Corporation President          28            0
## 342  academic/career coach & admin assistant           3            0
## 343                        college professor          10            7
## 344                       Software Developer           6            7
## 345                              psychologis          30            0
## 346                              psychologis          28            0
## 347                        college professor           9            0
## 348                                                    7            0
## 349                                                    0            0
## 350                                                    9            0
## 351                                                    0            3
## 352                                                    5            0
## 353                                                    4            0
## 354                                                    2            0
## 355                                                    6            3
## 356                                                   14            0
## 357                                                    5            0
## 358                                                    4           10
## 359                                                   13            0
## 360                                                    5            0
## 361                                                    0            3
## 362                                                    7            0
## 363                                                   10            0
## 364                                                   10            0
## 365                                                    0            0
## 366                                                    4            0
## 367                                                    2            0
## 368                                                    5            0
## 369                                                    4            0
## 370                                                    3            0
## 371                                                    5            6
## 372                                                    7            0
## 373                                                   13            0
## 374                                                    0            0
## 375                                                    0            0
## 376                                                   12            0
## 377                                                    3            0
## 378                                                    0            8
## 379                                                   12            0
## 380                                                    0            0
## 381                                                    0            0
## 382                                                    0            0
## 383                                                    0            0
## 384                                                    4            0
## 385                                                    5           10
## 386                                                   12            7
## 387                                                    1            0
## 388                                                   10            0
## 389                                                    6            0
## 390                                                    9            0
## 391                                                    9            8
## 392                                                    2            0
## 393                                                    1            6
## 394                                                    8            0
## 395                                                    0            0
## 396                                                    5            0
## 397                                                    0            0
## 398                                                    0            0
## 399                                                    7            0
## 400                                                    3            0
## 401                                                    0            0
## 402                                                    6            0
## 403                                                   14            0
## 404                                                    0            0
## 405                                                    0            3
## 406                                                    8            0
## 407                                                    0            0
## 408                                                    2            0
## 409                                                    2            0
## 410                                                    2            9
## 411                                                    6            6
## 412                                                    3            0
## 413                                                    0            0
## 414                                                   10            0
## 415                                                    6            0
## 416                                                    2            8
## 417                                                    0            0
## 418                                                    0            0
## 419                                                    0            7
## 420                                                    0            0
## 421                                                    0            0
## 422                                                    3            0
## 423                                                    0            0
## 424                                                   10            0
## 426                                                    0            9
## 427                                                    7            0
## 428                                                   10            0
## 429                                                    6            0
## 430                                                    1            0
## 431                                                    0            0
## 432                                                   10            0
## 433                                                    1            0
## 434                                                   10            0
## 435                                                    2            0
## 436                                                    4            6
## 437                                                    1            0
## 438                                                    0            8
## 439                                                    0            2
## 440                                                    4            0
## 441                                                    5            0
## 442                                                    1            3
## 443                                                    5            0
## 444                                                    4            0
## 445                                                    0            0
## 446                                                    9            0
## 447                                                   13            6
## 448                                                    0            0
## 449                                                    0            0
## 450                                                    4            0
## 451                                                    0            0
## 452                                                    0            0
## 453                                                    2            0
## 454                                                    6            0
## 455                                                    0            0
## 456                                                    2            0
## 457                                                    0            0
## 458                                                    0            6
## 459                                                    0            0
## 460                                                    0            0
## 461                                                    2            0
## 462                                                    0            9
## 463                                                    9            5
## 464                                                   10            0
## 465                                                    1            6
## 466                                                    0            0
## 467                                                    0            0
## 468                                                    0            0
## 469                                                    2            0
## 470                                                    2            0
## 471                                                    5            0
## 472                                                    2            0
## 473                                                   12            0
## 474                                                   10            0
## 475                                                    9            0
## 476                                                    0            0
## 477                                                    1            2
## 478                                                    0            1
## 479                                                    0            0
## 480                                                    1            5
## 481                                                    3            9
## 482                                                    0            0
## 483                                                    0            0
## 484                                                    1            6
## 485                                                    0            1
## 486                                                    1            7
## 487                                                    1            9
## 488                                                    8            0
## 489                                                    7            0
## 490                                                    0            0
## 491                                                    6            0
## 492                                                    1            0
## 493                                                    5            0
## 494                                                    0            6
## 495                                                    7            0
## 496                                                    1            8
## 497                                                    0            0
## 498                                                    0            0
## 499                                                    0            0
## 500                                                   12            0
## 501                                                    6            6
## 502                                                    9            0
## 503                                                    7            0
## 504                                                   10            0
## 505                                                    2            0
## 506                                                    0            0
## 507                                                   12            5
## 508                                                    0            5
## 509                                                    0            0
## 510                                                    3            0
## 511                                                    1            9
## 512                                                    0            0
## 513                                                    8           10
## 514                                                    4            9
## 515                                                    0            0
## 516                                                    5            0
## 517                                                    2            0
## 518                                                    0            0
## 519                                                   10            0
## 520                                                    0            0
## 521                                                    2            4
## 522                                                    0            0
## 523                                                    1            2
## 524                                                    3            7
## 525                                                   14            0
## 526                                                    0            0
## 527                                                    0            0
## 528                                                    0            0
## 529                                                    4            0
## 530                                                   10            0
## 531                                                    5            0
## 532                                                    3            8
## 533                                                    0            0
## 534                                                    1            0
## 535                                                   10            0
## 536                                                    0            0
## 537                                                   10            0
## 538                                                    3            7
## 539                                                    3            0
## 540                                                    8            0
## 541                                                    2            0
## 542                                                    5            0
## 543                                                    0            0
## 544                                                    5            2
## 545                                                    0            0
## 546                                                    0            0
## 547                                                    5            0
## 548                                                    4            0
## 549                                                    7            2
## 550                                                    0            0
## 551                                                    3            0
## 552                                                    6            0
## 553                                                    0            0
## 554                                                    4            0
## 555                                                    6            0
## 556                                                    3            0
## 557                                                    5            5
## 558                                                    0            0
## 559                                                   13            0
## 560                                                    5            7
## 561                                                    6            5
## 562                                                    0            3
## 563                                                   10            0
## 564                                                    0            4
## 565                                                   13            3
## 566                                                    1            0
## 567                                                    0            0
## 568                                                    0            0
## 569                                                    0            4
## 570                                  Economy           7            0
##          CommSize MaritalStatus NumofSons NumofDaughters XDP1 XDP2 XDP3
## 1         Village       Married        NA              2    4    4    4
## 2      Large-City       Married        NA              3    4    3    2
## 3      Large-City       Married        NA              1    3    2    3
## 4      Large-City       Married        NA              1    5    5    5
## 5      Small City       Married        NA              2    3    3    4
## 6      Large-City        Single        NA              0    3    3    5
## 7      Large-City       Married        NA              1    5    3    4
## 8      Large-City      Divorced        NA              1    4    4    4
## 9      Small City       Married        NA              0    4    5    3
## 10   Medium-Sized      Divorced        NA              2    3    3    2
## 11        Village       Married        NA              2    3    2    3
## 12  Rural/Country       Married        NA              2    1    2    1
## 13        Village      Divorced        NA              1    3    3    4
## 14   Medium-Sized       Married        NA              1    5    4    3
## 15        Village       Married        NA              3    4    4    3
## 16     Large Town       Married        NA              0    3    5    4
## 17        Village       Married        NA              1    5    5    3
## 18        Village       Married        NA              0    2    3    2
## 19        Village      Divorced        NA              1    2    5    3
## 21   Medium-Sized       Married        NA              2    3    3    3
## 22        Village       Married        NA              1    3    4    3
## 23   Medium-Sized       Married        NA              0    4    3    3
## 24     Large-City       Married        NA              1    5    5    4
## 25     Large-City       Married        NA              1    4    4    3
## 26   Medium-Sized       Married        NA              2    2    2    3
## 27     Large-City       Married        NA              0    3    3    4
## 28     Large-City       Married        NA              0    3    3    4
## 29     Small Town       Married        NA              0    5    5    3
## 30     Small City       Married        NA              0    3    2    3
## 31     Large-City       Married        NA              0    4    4    1
## 32   Medium-Sized       Married        NA              1    3    2    4
## 33  Rural/Country     Separated        NA              1    4    3    3
## 34     Large-City       Married        NA              1    2    2    3
## 35  Rural/Country       Married        NA              1    3    3    5
## 36     Large-City       Married        NA              0    4    4    4
## 37     Large-City       Married        NA              1    2    3    3
## 38     Large-City       Married        NA              2    2    2    3
## 39     Large-City       Married        NA              1    4    4    4
## 40     Large Town       Married        NA              1    5    4    4
## 41              8       Married        NA              2    4    4    3
## 42     Small Town       Married        NA              1    4    4    4
## 43     Small Town     Separated        NA              1    1    1    1
## 44   Medium-Sized       Married        NA              1    4    4    3
## 45     Small Town     Separated        NA              1    3    3    3
## 46        Village     Separated        NA              1    4    3    2
## 47     Small Town       Married        NA              2    3    3    1
## 48     Large Town     Separated        NA              3    3    2    2
## 49     Small Town       Married        NA              1    4    2    3
## 50     Small Town       Married        NA              1    4    5    4
## 51     Small Town       Married        NA              2    4    2    1
## 52        Village       Married        NA              1    5    4    4
## 53        Village       Married        NA              2    4    4    4
## 54        Village       Married        NA              0    2    4    3
## 55     Small Town       Married        NA              0    3    3    2
## 56     Small Town       Married        NA              2    5    4    4
## 57        Village       Married        NA              2    5    5    1
## 58        Village       Married        NA              2    5    5    5
## 59     Large Town       Married        NA              1    4    5    5
## 60        Village       Married        NA              0    5    5    3
## 61        Village       Married        NA              2    4    4    4
## 62     Large Town       Married        NA              3    5    4    4
## 63        Village       Married        NA              1    3    3    3
## 64        Village      Divorced        NA              0    4    4    4
## 65     Small City       Married        NA              1    2    5    4
## 66  Rural/Country       Married        NA              2    3    3    4
## 67     Large-City       Married        NA              1    4    4    4
## 68   Medium-Sized     Separated        NA              4    3    4    4
## 69        Village       Married        NA              1    4    4    4
## 70     Large-City       Married        NA              0    2    3    5
## 71     Large-City       Married        NA              0    4    3    3
## 72     Large-City       Married        NA              1    5    5    3
## 73        Village       Married        NA              1    3    2    2
## 74        Village       Married        NA              0    4    4    4
## 75        Village       Married        NA              0    3    4    2
## 76        Village       Married        NA              0    5    5    5
## 77  Rural/Country       Married        NA              7    4    5    5
## 78     Small Town      Divorced        NA              1    2    2    4
## 79  Rural/Country       Widowed        NA              2    5    5    3
## 80   Medium-Sized       Married        NA              2    3    4    4
## 81   Medium-Sized       Married        NA              2    3    1    1
## 82     Large-City       Married        NA              1    5    5    5
## 83     Small City       Married        NA              7    3    2    3
## 84   Medium-Sized       Married        NA              0    2    2    2
## 85   Medium-Sized       Married        NA              1    2    2    4
## 86   Medium-Sized       Married        NA             10    4    3    3
## 87     Large-City       Married        NA              0    4    4    4
## 88     Large-City       Married        NA              1    4    4    4
## 89   Medium-Sized       Married        NA              1    1    1    1
## 90     Large-City       Married        NA              0    4    2    5
## 91  Rural/Country       Married        NA              1    4    5    5
## 92     Small Town       Married        NA              2    4    4    4
## 93        Village      Divorced        NA              1    3    3    2
## 94        Village       Married        NA              0    3    2    3
## 95   Medium-Sized       Married        NA              1    2    3    3
## 96        Village       Married        NA              2    4    4    4
## 97        Village       Married        NA              0    1    1    2
## 98     Small Town       Married        NA              1    4    3    2
## 99     Large-City       Married        NA              1    3    4    3
## 100    Large-City       Married        NA              6    4    4    4
## 101    Large Town       Married        NA              0    5    5    5
## 102    Large-City       Married        NA              1    2    2    2
## 103    Small Town       Married        NA              1    3    4    4
## 104    Small Town       Married        NA              4    3    3    3
## 105    Large-City        Single        NA              0    5    5    5
## 106    Large-City       Married        NA              1    5    3    3
## 107       Village       Married        NA              0    3    3    4
## 108    Small Town       Married        NA              0    5    4    5
## 109  Medium-Sized       Widowed        NA              1    3    2    3
## 110    Small Town        Single        NA              0    4    4    4
## 111    Large Town       Married        NA              2    4    4    4
## 112    Small Town       Married        NA              1    3    2    2
## 113  Medium-Sized     Separated        NA              0    2    2    2
## 114    Small Town        Single        NA              0    1    1    1
## 115    Large Town       Married        NA              1    4    4    4
## 116  Medium-Sized       Married        NA              1    2    2    3
## 117    Small City       Married        NA              1    5    5    3
## 118  Medium-Sized       Married        NA              0    5    5    5
## 119    Large-City      Divorced        NA              0    3    4    3
## 120  Medium-Sized       Married        NA              0    3    4    3
## 121    Large Town       Married        NA              0    2    2    2
## 122  Medium-Sized       Married        NA              0    3    3    2
## 123    Large Town        Single        NA              1    2    3    4
## 124  Medium-Sized      Divorced        NA              0    3    3    3
## 125    Small Town     Separated        NA              0    5    5    5
## 126    Small Town       Married        NA              1    4    4    5
## 127 Rural/Country      Divorced        NA              2    5    5    3
## 128       Village     Separated        NA              0    5    5    5
## 129 Rural/Country       Married        NA              2    3    5    3
## 130    Large Town       Married        NA              1    2    1    2
## 131    Small Town       Married        NA              2    4    4    4
## 132  Medium-Sized       Married        NA              1    4    4    2
## 133  Medium-Sized      Divorced        NA              3    4    4    4
## 134 Rural/Country       Married        NA              2    3    4    4
## 135    Large Town       Married        NA              1    3    3    2
## 136    Large Town       Married        NA              3    4    2    4
## 137 Rural/Country       Married        NA              1    5    4    4
## 138       Village       Married        NA              0    3    3    3
## 139  Medium-Sized     Separated        NA              0    4    3    3
## 140    Large Town       Married        NA              2    5    5    3
## 141       Village        Single        NA              0    4    4    3
## 142    Small Town     Separated        NA              1    4    4    4
## 143  Medium-Sized       Married        NA              1    4    4    5
## 144    Large-City       Married        NA              1    4    4    4
## 145    Large-City       Married        NA              2    1    1    1
## 146    Small Town        Single        NA              1    4    3    4
## 147  Medium-Sized       Widowed        NA              1    5    5    4
## 148    Large-City       Married        NA              0    2    2    3
## 149    Large Town       Married        NA              1    3    2    1
## 150    Large-City       Married        NA              1    4    3    2
## 151    Small City       Married        NA              0    3    3    4
## 152    Large Town       Married        NA              2    3    2    3
## 153    Small Town       Married        NA              1    3    4    3
## 154    Large-City       Married        NA              0    4    3    3
## 155    Small City       Married        NA              0    4    2    4
## 156    Small City       Married        NA              1    4    4    4
## 157    Small Town      Divorced        NA              1    3    3    4
## 158  Medium-Sized       Married        NA              1    4    4    4
## 159    Large-City       Married        NA              0    2    4    3
## 160    Large-City      Divorced        NA              0    2    1    1
## 161    Small City       Married        NA              0    3    3    2
## 162  Medium-Sized      Divorced        NA              1    4    4    4
## 163    Small City       Married        NA              1    5    4    4
## 164    Small City       Married        NA              0    5    5    5
## 165       Village       Married        NA              0    3    3    4
## 166    Large Town      Divorced        NA              1    3    3    4
## 167 Rural/Country       Married        NA              1    2    4    3
## 168  Medium-Sized     Separated        NA              1    3    4    4
## 169  Medium-Sized       Married        NA              3    3    2    2
## 170  Medium-Sized       Married        NA              3    4    3    4
## 171  Medium-Sized       Married        NA              0    4    4    4
## 172    Small Town       Married        NA              1    5    3    4
## 173  Medium-Sized       Married        NA              2    4    4    3
## 174    Large-City       Married        NA              2    4    4    4
## 175    Large-City      Divorced        NA              0    5    4    4
## 176    Small Town       Married        NA              0    3    3    4
## 177    Small City       Married        NA              2    3    3    3
## 178    Small City       Married        NA              2    5    5    4
## 179  Medium-Sized      Divorced        NA              0    2    3    3
## 180    Small City       Married        NA              2    4    4    3
## 181  Medium-Sized       Married        NA              1    4    5    5
## 182    Small Town       Married        NA              2    2    1    1
## 183    Large Town      Divorced        NA              1    4    3    3
## 184    Small Town       Married        NA              0    5    5    4
## 185    Large-City     Separated        NA              1    4    4    4
## 186    Large Town       Married        NA              2    2    3    2
## 187    Small Town       Married        NA              1    5    4    4
## 188  Medium-Sized       Married        NA              1    3    5    5
## 189 Rural/Country       Married        NA              1    3    4    2
## 190    Large Town       Married        NA              2    2    2    2
## 191    Small City       Married        NA              0    3    4    4
## 192    Large-City       Married        NA              1    3    3    1
## 193    Large-City       Married        NA              0    5    4    4
## 194  Medium-Sized       Married        NA              2    2    2    1
## 195    Small City       Married        NA              0    4    5    4
## 196    Large-City       Married        NA              2    3    3    4
## 197  Medium-Sized       Married        NA              1    2    2    2
## 198    Large-City       Married        NA              0    4    4    4
## 199    Large-City       Married        NA              0    3    2    3
## 200    Small City       Married        NA              1    4    4    4
## 201    Large-City       Married        NA              1    4    4    5
## 202       Village       Married        NA              1    5    4    4
## 203    Small City       Married        NA              0    5    5    5
## 204    Small City        Single        NA              0    3    2    2
## 205    Large Town      Divorced        NA              2    5    5    5
## 206  Medium-Sized       Widowed        NA              1    4    4    4
## 207    Small Town       Married        NA              0    2    2    3
## 208    Small City       Married        NA              1    2    3    2
## 209    Small City       Married        NA              0    3    3    2
## 210    Large-City       Married        NA              1    4    4    4
## 211  Medium-Sized       Married        NA              3    3    4    3
## 212  Medium-Sized       Married        NA              0    5    5    5
## 213    Large-City       Married        NA              0    3    4    2
## 214  Medium-Sized       Married        NA              1    3    3    3
## 215    Small City        Single        NA              0    2    3    2
## 216    Small Town       Married        NA              1    1    1    2
## 217    Large-City       Married        NA              1    4    4    4
## 218    Small Town        Single        NA              1    3    5    4
## 219    Large-City      Divorced        NA              0    5    4    4
## 220    Small Town       Widowed        NA              1    2    3    3
## 221  Medium-Sized       Married        NA              1    3    3    3
## 222  Medium-Sized       Married        NA              2    2    3    3
## 223  Medium-Sized       Married        NA              2    3    3    4
## 224  Medium-Sized        Single        NA              0    3    2    2
## 225    Large-City       Married        NA              1    1    3    1
## 226    Large Town       Married        NA              1    4    4    4
## 227    Large-City       Widowed        NA              0    5    5    5
## 228    Large Town       Married        NA              2    2    1    1
## 229    Small City       Married        NA              1    3    3    3
## 230    Large-City      Divorced        NA              0    2    3    2
## 231  Medium-Sized       Married        NA              0    5    3    2
## 232    Large-City       Married        NA              1    3    2    3
## 233       Village       Married        NA              1    4    2    1
## 234    Large Town       Married        NA              1    3    4    4
## 235    Large-City      Divorced        NA              1    3    2    2
## 236    Small City       Married        NA              0    4    4    4
## 237  Medium-Sized       Married        NA              1    3    4    2
## 238    Large Town       Married        NA              0    2    1    2
## 239    Small City       Married        NA              1    5    3    5
## 240    Small City       Married        NA              0    2    2    2
## 241 Rural/Country       Married        NA              1    3    3    2
## 242    Large-City      Divorced        NA              0    5    4    5
## 243  Medium-Sized       Married        NA              1    5    5    5
## 244    Small Town       Married        NA              0    2    1    1
## 245  Medium-Sized       Married        NA              2    2    2    2
## 246    Large-City       Married        NA              0    2    2    2
## 247    Small City      Divorced        NA              2    5    4    5
## 248    Large-City       Married        NA              1    2    2    2
## 249    Large-City       Married        NA              1    2    2    1
## 250    Small City       Widowed        NA              1    4    4    2
## 251    Small City      Divorced        NA              1    4    3    4
## 252  Medium-Sized       Married        NA              1    3    4    3
## 253    Large-City       Married        NA              0    2    3    2
## 254    Large-City       Married        NA              1    3    3    2
## 255  Medium-Sized       Married        NA              1    3    3    3
## 256                     Married        NA              1    3    2    2
## 257  Medium-Sized       Married        NA              1    5    4    3
## 258    Large-City       Widowed        NA              0    3    3    3
## 259                     Married        NA              1    4    4    4
## 260    Large-City      Divorced        NA              1    4    2    4
## 261 Rural/Country     Separated        NA              1    4    5    3
## 262    Small City       Married        NA              2    1    3    3
## 263  Medium-Sized       Married        NA              1    2    2    2
## 264    Large-City       Married        NA              4    1    1    1
## 265  Medium-Sized       Married        NA              2    3    3    1
## 266    Large Town       Married        NA              1    4    3    4
## 267  Medium-Sized       Married        NA              1    2    2    2
## 268    Large Town       Married        NA              1    3    4    4
## 269  Medium-Sized       Married        NA              1    2    2    1
## 270    Small City       Married        NA              1    2    2    2
## 271    Large-City       Married        NA              0    3    4    4
## 272  Medium-Sized       Married        NA              2    4    2    4
## 273  Medium-Sized        Single        NA              0    3    4    3
## 274  Medium-Sized       Married        NA              1    2    3    2
## 275    Large-City      Divorced        NA              1    2    2    1
## 276    Large-City       Married        NA              1    2    1    1
## 277  Medium-Sized       Married        NA              1    4    4    3
## 278    Small City       Married        NA              0    4    5    4
## 279  Medium-Sized      Divorced        NA              1    4    3    2
## 280    Large-City       Married        NA              1    3    3    3
## 281    Large Town       Married        NA              0    4    4    5
## 282 Rural/Country       Married        NA              1    5    5    5
## 283  Medium-Sized       Married        NA              2    4    3    5
## 284    Large-City        Single        NA              0    4    4    3
## 285  Medium-Sized       Married        NA              1    5    5    5
## 286    Large-City       Married        NA              0    3    1    2
## 287    Large Town      Divorced        NA              2    3    3    2
## 288    Large-City      Divorced        NA              0    3    2    1
## 289  Medium-Sized      Divorced        NA              0    3    2    2
## 290    Large Town      Divorced        NA              0    3    2    4
## 291    Small City       Married        NA              1    3    5    5
## 292    Large Town      Divorced        NA              0    3    1    2
## 293    Small City       Married        NA              1    2    3    2
## 294    Small City       Married        NA              0    5    5    3
## 295  Medium-Sized       Married        NA              0    5    5    5
## 296    Small City       Married        NA              0    3    4    4
## 297    Small City      Divorced        NA              2    4    4    4
## 298    Large-City      Divorced        NA              1    2    1    1
## 299                    Divorced        NA              0    1    1    1
## 300    Small Town       Married        NA              2    4    5    4
## 301    Large Town       Married        NA              1    4    3    3
## 302    Large-City       Married        NA              1    3    4    3
## 303    Large-City       Married        NA              1    5    5    5
## 304    Small City     Separated        NA              1    2    2    2
## 305    Large-City       Married        NA              1    4    5    1
## 306    Small City       Married        NA              2    2    2    3
## 307    Large-City       Married        NA              1    3    3    3
## 308    Large-City       Married        NA              0    2    4    2
## 309    Small City      Divorced        NA              0    3    3    1
## 310    Small City       Married        NA              1    4    3    4
## 311    Small City       Married        NA              3    1    1    1
## 312    Small Town      Divorced        NA              1    4    5    3
## 313    Large Town       Married        NA              1    2    2    3
## 314    Large-City       Married        NA              2    4    4    4
## 315    Large-City       Married        NA              0    1    1    1
## 316       Village      Divorced        NA              1    5    4    2
## 317    Small City       Married        NA              1    4    4    2
## 318  Medium-Sized        Single        NA              0    4    5    4
## 319    Large-City       Married        NA              1    4    5    4
## 320    Small City       Married        NA              1    3    3    2
## 321    Large-City       Married        NA              1    3    3    3
## 322    Large-City      Divorced        NA              3    2    2    2
## 323    Large-City      Divorced        NA              0    4    4    3
## 324    Large Town       Married        NA              1    4    4    4
## 325    Large Town       Married        NA              1    4    3    4
## 326    Small City       Married        NA              0    1    1    2
## 327 Rural/Country       Married        NA              1    4    4    4
## 328    Small City     Separated        NA              0    3    4    2
## 329  Medium-Sized     Separated        NA              1    4    5    4
## 330    Large-City      Divorced        NA              3    5    5    4
## 331    Large-City       Widowed        NA              1    3    3    2
## 332    Large-City       Married        NA              0    2    4    2
## 333    Large Town       Married        NA              2    2    2    4
## 334    Small Town       Married        NA              3    3    3    4
## 335    Small Town       Married        NA              1    3    3    2
## 336  Medium-Sized       Married        NA              1    5    5    4
## 337  Medium-Sized       Married        NA              1    4    3    4
## 338  Medium-Sized      Divorced        NA              1    4    3    5
## 339    Small City       Widowed        NA              1    4    5    5
## 340 Rural/Country       Married        NA              3    3    5    4
## 341    Small City       Married        NA              1    2    2    1
## 342    Small City       Married        NA              1    3    3    2
## 343    Large Town       Married        NA              0    3    2    1
## 344    Large Town      Divorced        NA              1    2    3    3
## 345  Medium-Sized       Married        NA              1    3    3    2
## 346    Small City       Married        NA              1    4    2    1
## 347  Medium-Sized      Divorced        NA              0    4    4    4
## 348    Small Town      Divorced        NA              1    4    1    4
## 349    Small Town       Married        NA              1    2    2    2
## 350    Large Town       Married        NA              1    3    3    3
## 351    Large Town       Married        NA              3    5    4    4
## 352    Small Town       Married        NA              3    4    4    4
## 353    Small Town      Divorced        NA              0    5    4    3
## 354    Small Town       Married        NA              0    3    3    3
## 355    Small Town      Divorced        NA              1    2    2    2
## 356    Large Town      Divorced        NA              2    4    3    4
## 357    Small Town      Divorced        NA              1    2    2    2
## 358    Small Town       Married        NA              2    4    3    2
## 359    Small Town       Married        NA              2    4    4    2
## 360    Small Town      Divorced        NA              1    4    4    4
## 361       Village       Married        NA              2    1    1    1
## 362 Rural/Country       Married        NA              2    3    4    3
## 363    Large Town      Divorced        NA              1    4    3    2
## 364    Small Town       Married        NA              1    3    3    4
## 365       Village       Married        NA              1    1    1    2
## 366    Small Town      Divorced        NA              1    4    5    5
## 367       Village       Married        NA              1    5    5    5
## 368  Medium-Sized       Married        NA              3    5    5    5
## 369  Medium-Sized        Single        NA              0    4    4    5
## 370       Village       Married        NA              0    4    3    3
## 371  Medium-Sized       Married        NA              1    2    3    2
## 372    Large Town       Married        NA              1    2    2    1
## 373    Large Town       Widowed        NA              0    5    3    4
## 374  Medium-Sized       Married        NA              0    3    2    2
## 375       Village       Widowed        NA              1    4    3    3
## 376    Small Town       Married        NA              1    3    2    3
## 377       Village        Single        NA              0    5    5    5
## 378    Small Town       Married        NA              0    4    4    4
## 379    Small Town       Married        NA              0    3    2    2
## 380    Small Town       Married        NA              1    2    2    2
## 381 Rural/Country       Married        NA              1    4    4    4
## 382    Small Town       Married        NA              1    3    3    3
## 383    Large Town       Married        NA              2    3    3    3
## 384                     Married        NA              0    4    4    4
## 385    Large-City       Married        NA              1    4    4    2
## 386    Large Town       Married        NA              1    3    4    3
## 387    Small Town       Married        NA              0    3    4    3
## 388    Large Town       Married        NA              1    4    4    4
## 389    Small Town        Single        NA              1    1    1    1
## 390       Village     Separated        NA              2    3    3    3
## 391       Village       Married        NA              1    3    3    3
## 392       Village     Separated        NA              1    3    4    4
## 393       Village      Divorced        NA              0    4    4    4
## 394 Rural/Country       Married        NA              2    3    3    3
## 395       Village       Widowed        NA              0    4    5    4
## 396    Large Town       Married        NA              1    4    4    4
## 397       Village       Married        NA              2    3    2    2
## 398    Large Town       Married        NA              3    3    3    2
## 399    Large Town       Married        NA              0    3    3    3
## 400  Medium-Sized       Married        NA              0    3    3    1
## 401             8       Married        NA              2    2    3    2
## 402    Large Town       Married        NA              1    3    3    2
## 403    Small Town       Married        NA              1    2    4    2
## 404    Small Town        Single        NA              2    5    5    5
## 405    Large Town       Married        NA              0    2    2    3
## 406    Small Town      Divorced        NA              0    1    2    1
## 407    Large Town      Divorced        NA              1    5    5    5
## 408  Medium-Sized      Divorced        NA              1    1    2    1
## 409  Medium-Sized       Married        NA              1    2    2    2
## 410    Small Town       Married        NA              1    3    4    4
## 411    Small Town       Married        NA              0    4    3    3
## 412    Large Town       Married        NA              0    5    4    5
## 413    Large Town       Married        NA              0    3    3    3
## 414    Large Town        Single        NA              0    4    4    2
## 415       Village       Married        NA              1    4    4    4
## 416    Small Town       Married        NA              0    5    4    3
## 417             8       Married        NA              1    4    4    4
## 418             8       Married        NA              0    5    4    1
## 419       Village       Married        NA              1    4    2    4
## 420    Small Town       Married        NA              1    5    4    4
## 421       Village       Married        NA              1    5    5    5
## 422    Large Town       Married        NA              1    3    3    3
## 423    Large Town       Married        NA              2    3    3    5
## 424       Village      Divorced        NA              0    4    2    3
## 426    Small Town      Divorced        NA              0    4    5    5
## 427    Large Town       Married        NA              1    4    4    4
## 428       Village       Married        NA              1    2    2    2
## 429  Medium-Sized       Married        NA              0    3    4    4
## 430 Rural/Country       Married        NA              1    2    3    2
## 431 Rural/Country       Married        NA              1    5    3    2
## 432       Village       Married        NA              2    5    5    2
## 433    Large-City      Divorced        NA              3    1    1    1
## 434  Medium-Sized       Married        NA              1    4    4    4
## 435    Large Town       Married        NA              0    3    3    2
## 436    Small Town       Married        NA              0    3    3    3
## 437    Small Town      Divorced        NA              1    4    4    5
## 438 Rural/Country     Separated        NA              1    4    4    4
## 439 Rural/Country       Married        NA              0    3    3    4
## 440    Large Town      Divorced        NA              0    5    5    5
## 441    Large Town       Married        NA              1    2    2    2
## 442    Large Town       Married        NA              4    5    4    4
## 443 Rural/Country      Divorced        NA              2    1    1    3
## 444    Large Town       Married        NA              1    4    2    2
## 445  Medium-Sized       Married        NA              1    2    2    2
## 446    Small Town      Divorced        NA              1    4    4    4
## 447       Village       Married        NA              0    3    2    1
## 448    Small Town      Divorced        NA              0    3    3    3
## 449    Small Town       Married        NA              1    3    2    1
## 450    Large Town       Married        NA              1    3    2    4
## 451  Medium-Sized       Married        NA              1    3    3    3
## 452    Large Town       Married        NA              1    1    2    3
## 453    Small Town      Divorced        NA              0    5    5    5
## 454    Small Town      Divorced        NA              0    3    3    4
## 455       Village       Married        NA              2    3    3    3
## 456    Small Town      Divorced        NA              3    4    4    3
## 457  Medium-Sized      Divorced        NA              0    2    3    3
## 458 Rural/Country       Married        NA              2    5    5    5
## 459                     Married        NA              1    1    1    1
## 460 Rural/Country      Divorced        NA              0    3    2    1
## 461    Small Town       Married        NA              0    4    4    4
## 462    Small Town       Married        NA              0    5    5    5
## 463             8       Married        NA              1    4    5    4
## 464    Small Town       Married        NA              1    4    3    3
## 465    Small Town       Married        NA              1    2    2    3
## 466    Large Town       Married        NA              0    3    2    3
## 467    Small Town       Married        NA              1    3    3    2
## 468       Village       Married        NA              0    2    2    2
## 469    Small Town       Married        NA              1    4    4    4
## 470    Small Town       Married        NA              0    3    3    3
## 471    Large Town       Married        NA              1    4    3    4
## 472    Small Town       Married        NA              1    3    4    4
## 473    Large Town       Married        NA              3    4    3    3
## 474    Small Town       Married        NA              0    4    4    4
## 475  Medium-Sized       Married        NA              1    3    3    2
## 476    Small Town     Separated        NA              1    5    4    4
## 477    Small Town       Married        NA              0    5    5    5
## 478    Large Town       Married        NA              0    3    3    3
## 479    Small Town       Married        NA              1    5    5    5
## 480  Medium-Sized       Married        NA              0    4    5    5
## 481       Village       Married        NA              1    4    4    3
## 482       Village      Divorced        NA              1    3    3    3
## 483  Medium-Sized       Married        NA              3    4    4    4
## 484       Village       Married        NA              1    3    3    4
## 485  Medium-Sized       Married        NA              1    3    2    3
## 486       Village        Single        NA              0    3    3    3
## 487    Small Town       Married        NA              1    4    4    4
## 488    Small Town       Married        NA              2    1    4    1
## 489    Large Town        Single        NA              2    4    3    4
## 490    Small Town       Married        NA              0    3    3    4
## 491    Small Town        Single        NA              0    3    4    3
## 492       Village      Divorced        NA              2    3    3    5
## 493    Small Town       Married        NA              1    3    2    1
## 494       Village       Married        NA              2    4    5    4
## 495       Village       Married        NA              0    3    1    2
## 496    Small Town       Married        NA              1    4    4    4
## 497    Large Town       Married        NA              1    3    2    3
## 498    Large Town      Divorced        NA              1    3    3    2
## 499       Village       Married        NA              1    2    3    3
## 500    Large Town       Married        NA              1    5    4    5
## 501    Small Town       Married        NA              1    3    3    3
## 502    Small Town       Married        NA              1    4    4    4
## 503       Village       Married        NA              0    5    4    4
## 504       Village       Married        NA              1    4    3    3
## 505       Village     Separated        NA              0    2    2    2
## 506 Rural/Country       Married        NA              0    2    1    1
## 507    Small Town       Married        NA              1    2    2    2
## 508    Small Town       Married        NA              1    1    1    3
## 509    Large-City      Divorced        NA              2    3    2    2
## 510    Small Town       Married        NA              2    3    3    5
## 511       Village      Divorced        NA              2    1    1    1
## 512       Village       Married        NA              0    3    2    2
## 513    Large Town       Married        NA              1    5    4    4
## 514    Small Town       Married        NA              2    2    2    1
## 515    Large Town      Divorced        NA              0    5    5    3
## 516    Small Town       Widowed        NA              0    3    4    4
## 517       Village        Single        NA              2    4    3    3
## 518  Medium-Sized       Married        NA              1    4    3    3
## 519  Medium-Sized       Married        NA              1    1    1    3
## 520 Rural/Country       Married        NA              1    4    2    4
## 521    Large Town      Divorced        NA              0    4    4    3
## 522       Village       Married        NA              1    4    4    4
## 523       Village       Married        NA              0    2    4    3
## 524       Village       Married        NA              1    3    3    4
## 525    Small Town      Divorced        NA              1    3    2    2
## 526             8       Married        NA              2    1    3    4
## 527  Medium-Sized       Married        NA              4    1    1    1
## 528    Small Town       Married        NA              1    4    4    3
## 529    Large Town       Widowed        NA              1    4    3    3
## 530 Rural/Country       Married        NA              1    4    4    3
## 531    Small Town       Married        NA              1    2    2    2
## 532       Village     Separated        NA              0    3    3    3
## 533 Rural/Country       Married        NA              0    4    4    2
## 534       Village       Married        NA              1    4    5    5
## 535    Large-City       Married        NA              0    4    2    1
## 536  Medium-Sized       Married        NA              2    2    2    3
## 537       Village       Married        NA              1    4    4    4
## 538       Village       Married        NA              0    4    4    4
## 539       Village       Married        NA              1    3    3    3
## 540       Village       Married        NA              0    4    4    4
## 541    Small Town       Married        NA              1    3    3    2
## 542    Large Town       Married        NA              1    3    3    4
## 543 Rural/Country       Married        NA              1    3    3    2
## 544    Large Town       Married        NA              0    3    1    1
## 545    Small Town       Married        NA              1    2    2    1
## 546    Large Town       Married        NA              1    2    1    1
## 547    Small Town       Married        NA              1    4    3    3
## 548    Small Town      Divorced        NA              0    1    5    5
## 549       Village        Single        NA              0    4    3    4
## 550 Rural/Country       Widowed        NA              0    2    2    2
## 551 Rural/Country       Married        NA              0    3    4    5
## 552 Rural/Country      Divorced        NA              1    2    3    3
## 553    Large Town       Married        NA              2    2    2    2
## 554       Village       Married        NA              1    5    5    5
## 555 Rural/Country      Divorced        NA              1    3    5    3
## 556    Large Town       Married        NA              1    3    2    3
## 557    Large Town       Married        NA              0    5    4    4
## 558       Village       Married        NA              1    5    5    5
## 559 Rural/Country      Divorced        NA              0    2    2    2
## 560 Rural/Country       Married        NA              1    3    2    3
## 561       Village       Married        NA              0    2    2    1
## 562    Large Town       Married        NA              1    3    4    2
## 563    Large Town       Married        NA              1    2    2    2
## 564    Large Town       Married        NA              1    4    2    3
## 565       Village       Married        NA              0    3    3    2
## 566    Small Town        Single        NA              1    2    2    2
## 567    Large Town       Married        NA              1    3    3    2
## 568    Large Town     Separated        NA              2    2    3    2
## 569    Small Town        Single        NA              3    3    3    5
## 570    Large-City      Divorced        NA              1    2    2    2
##     XDP4 XDP5 XAIP1 XAIP2 XAIP3 XAIP4 XAIP5 XAIP6 XAIP7 XAIP8 XAIP9 XAIP10
## 1      3    2     1     1     3     4     3     5     5     3     4      3
## 2      3    3     1     3     3     3     4     4     4     4     4      5
## 3      1    1     1     1     2     2     3     3     3     3     2      3
## 4      5    5     2     2     3     2     5     3     5     5     5      5
## 5      3    3     2     3     5     4     3     4     4     4     3      4
## 6      2    2     1     1     1     4     4     1     2     3     3      5
## 7      4    5     4     2     3     3     4     1     3     3     4      5
## 8      4    4     4     4     4     4     4     4     4     4     4      4
## 9      3    3     2     2     5     2     2     1     5     3     1      5
## 10     2    2     1     1     1     3     2     1     3     2     2      3
## 11     2    1     1     1     3     4     3     1     1     3     4      3
## 12     1    1     1     1     1     1     1     1     1     1     1      1
## 13     5    4     4     2     4     3     5     3     4     4     4      5
## 14     2    3     4     1     4     4     4     3     3     2     2      5
## 15     3    2     2     3     4     4     4     5     3     5     3      4
## 16     5    5     2     2     1     5     5     5     2     3     2      5
## 17     2    2     1     5     5     5     5     5     5     3     5      5
## 18     2    2     1     1     4     3     2     2     2     2     2      3
## 19     3    3     3     2     5     4     4     3     5     4     3      3
## 21     3    3     2     2     3     3     3     3     3     3     2      3
## 22     3    3     3     1     4     3     3     4     3     3     3      3
## 23     3    2     2     2     4     2     3     3     2     4     2      4
## 24     3    3     2     3     3     3     3     4     2     4     3      4
## 25     3    3     3     4     4     5     3     3     4     3     2      3
## 26     1    1     3     1     1     1     2     3     3     2     1      2
## 27     3    3     1     1     2     3     3     4     3     3     4      3
## 28     3    3     1     1     2     3     3     4     3     3     4      3
## 29     5    5     5     5     5     1     5     5     5     5     5      5
## 30     3    3     1     1     3     2     2     1     2     4     3      4
## 31     3    3     2     2     5     5     2     5     4     5     3      5
## 32     4    4     3     2     2     5     4     4     5     3     5      5
## 33     3    3     3     2     3     2     3     3     3     3     3      3
## 34     1    1     1     1     1     2     3     2     1     2     2      1
## 35     3    3     1     2     5     5     4     5     4     5     4      4
## 36     4    4     5     5     5     5     5     1     5     5     5      5
## 37     2    2     4     2     3     3     3     2     4     3     2      3
## 38     2    3     1     1     3     4     3     2     2     3     2      3
## 39     4    4     3     2     5     5     5     5     5     3     5      5
## 40     4    4     1     1     1     3     4     4     4     4     3      4
## 41     3    3     2     3     5     4     4     3     5     3     2      5
## 42     4    4     3     2     3     3     4     4     4     4     5      5
## 43     3    3     3     2     3     3     3     5     3     4     3      3
## 44     3    3     2     3     4     4     5     5     5     5     4      4
## 45     3    3     4     1     2     1     3     3     1     3     3      3
## 46     2    2     3     2     3     4     3     2     3     3     3      3
## 47     3    3     5     1     5     5     5     2     5     5     5      5
## 48     2    3     3     3     5     2     3     3     2     3     1      2
## 49     2    2     2     5     5     5     5     5     5     4     3      5
## 50     3    3     4     5     5     5     5     5     5     5     5      5
## 51     1    1     1     1     5     2     4     5     4     3     2      4
## 52     2    2     1     1     1     1     1     1     2     3     1      3
## 53     2    2     1     2     4     3     3     4     3     3     3      5
## 54     2    2     4     4     2     4     5     4     4     4     5      5
## 55     1    1     1     1     1     3     3     2     2     3     2      3
## 56     3    3     2     3     3     4     3     2     3     4     3      4
## 57     5    5     4     2     5     5     5     5     5     5     5      5
## 58     5    5     4     3     5     5     5     5     4     4     5      5
## 59     5    5     5     3     5     4     5     5     5     5     5      5
## 60     3    3     3     2     4     4     5     5     3     5     5      5
## 61     3    2     1     1     2     1     1     1     4     4     2      3
## 62     3    3     1     3     5     5     4     5     5     1     5      5
## 63     3    3     2     2     3     3     3     3     3     4     3      3
## 64     4    4     5     3     5     5     4     4     3     4     2      4
## 65     2    2     4     4     3     4     4     1     5     4     5      2
## 66     4    4     3     2     5     3     4     3     4     2     4      4
## 67     5    5     3     2     5     3     4     5     4     5     4      4
## 68     3    3     3     2     4     4     4     3     2     5     4      3
## 69     3    3     1     1     1     2     2     4     5     4     3      3
## 70     3    2     1     2     2     3     1     2     3     2     2      1
## 71     2    2     2     3     4     3     3     4     3     4     3      4
## 72     3    3     4     2     5     2     4     4     4     3     3      3
## 73     2    2     4     2     5     2     3     4     3     4     3      3
## 74     4    4     2     4     4     4     5     5     5     4     4      4
## 75     3    3     3     2     2     2     4     4     4     4     2      4
## 76     5    5     5     3     3     4     5     5     5     5     5      5
## 77     4    4     5     1     5     4     4     2     5     5     5      5
## 78     2    2     3     3     5     3     3     1     2     3     2      2
## 79     2    3     3     3     4     5     5     5     5     4     3      5
## 80     3    3     1     2     4     4     3     2     4     3     2      4
## 81     1    1     1     1     3     2     1     1     1     2     1      2
## 82     5    5     1     1     1     5     4     4     2     2     2      3
## 83     2    2     1     1     2     1     1     4     2     3     2      2
## 84     2    3     3     3     3     4     4     4     4     1     1      5
## 85     2    2     2     4     4     2     1     2     2     5     3      2
## 86     2    2     1     1     2     2     1     4     1     2     1      1
## 87     4    4     3     3     3     3     3     3     3     4     3      3
## 88     4    4     2     3     3     3     3     2     4     4     4      4
## 89     1    1     4     5     4     4     3     5     3     4     3      3
## 90     3    3     2     5     4     1     3     2     5     5     3      3
## 91     4    4     3     5     5     5     5     5     5     4     4      5
## 92     3    3     2     1     3     3     3     5     4     3     2      3
## 93     3    3     1     1     3     3     3     1     4     3     3      3
## 94     2    2     1     2     4     2     3     1     1     3     2      3
## 95     2    2     2     2     4     4     2     2     2     3     2      2
## 96     3    3     1     1     2     3     4     4     3     3     2      3
## 97     1    1     1     1     1     1     1     5     1     1     1      1
## 98     2    5     1     1     5     2     3     1     2     1     2      2
## 99     2    2     3     4     5     4     4     4     4     5     2      4
## 100    4    4     4     2     3     2     4     5     5     4     5      5
## 101    2    2     1     1     3     3     4     5     3     3     4      4
## 102    1    1     1     1     2     3     1     1     2     3     1      1
## 103    3    3     1     1     4     3     4     4     4     3     2      3
## 104    2    2     3     2     3     3     3     3     3     2     3      3
## 105    5    5     1     1     1     5     5     5     5     1     5      5
## 106    4    4     2     2     2     4     4     5     5     4     5      5
## 107    3    3     3     2     2     2     4     4     3     4     4      4
## 108    4    4     3     2     3     1     4     4     4     5     4      5
## 109    1    1     1     1     1     1     1     1     1     1     1      3
## 110    4    4     4     2     5     5     5     5     5     4     4      4
## 111    4    4     2     2     3     3     4     4     4     4     4      4
## 112    2    2     1     1     5     3     3     1     3     3     2      3
## 113    2    2     4     1     5     1     2     1     2     3     1      1
## 114    1    1     1     1     3     1     1     1     1     1     1      1
## 115    2    2     1     1     5     2     2     1     1     3     1      2
## 116    1    1     1     1     1     2     2     2     2     2     2      2
## 117    4    4     1     1     1     3     3     4     2     4     3      4
## 118    5    5     4     4     4     2     2     5     5     4     4      4
## 119    3    3     5     1     3     4     5     4     5     5     5      4
## 120    3    4     5     1     4     2     5     5     3     4     4      5
## 121    2    2     3     1     4     1     1     1     1     1     1      1
## 122    2    2     4     1     3     2     4     4     4     5     3      3
## 123    2    2     3     1     4     3     3     3     3     4     2      3
## 124    4    4     2     4     4     5     4     5     4     5     4      5
## 125    3    3     3     4     5     5     4     5     5     5     5      5
## 126    4    4     2     2     4     3     3     1     3     4     2      2
## 127    3    4     4     3     2     3     4     3     4     3     3      3
## 128    5    5     3     5     2     5     5     5     5     5     5      5
## 129    3    3     4     3     3     2     4     5     4     5     5      5
## 130    1    1     1     1     4     1     1     2     1     3     2      2
## 131    4    4     4     4     4     2     4     2     4     4     4      4
## 132    3    3     1     1     3     3     4     3     2     4     4      4
## 133    3    3     2     4     4     4     3     3     3     3     3      3
## 134    3    3     2     2     4     4     4     2     4     4     4      4
## 135    2    1     1     1     3     1     1     1     2     1     1      2
## 136    3    3     1     1     5     2     4     1     4     3     5      3
## 137    4    4     2     2     2     1     4     4     4     5     4      4
## 138    2    3     2     2     3     2     2     2     2     5     2      3
## 139    3    3     1     4     4     5     4     3     3     3     3      5
## 140    3    3     1     1     1     3     4     3     1     3     3      3
## 141    3    3     2     3     3     4     4     3     3     3     3      4
## 142    4    4     2     2     2     4     4     3     3     4     4      5
## 143    4    4     1     3     5     5     5     4     4     4     5      5
## 144    5    5     4     4     5     5     4     4     4     4     5      5
## 145    1    1     2     2     2     1     1     4     1     2     2      1
## 146    3    3     3     1     3     1     3     5     1     3     3      3
## 147    3    3     1     2     5     3     4     1     1     3     2      4
## 148    2    2     1     1     5     1     2     3     2     2     1      2
## 149    1    1     1     1     1     4     1     3     2     3     1      2
## 150    2    2     1     1     1     3     2     1     1     2     2      4
## 151    3    3     3     2     5     4     3     4     3     4     4      4
## 152    3    3     3     3     3     2     3     3     3     4     2      3
## 153    4    4     3     4     5     5     4     5     4     5     4      4
## 154    3    4     2     2     4     4     5     3     4     4     4      4
## 155    3    3     2     1     5     5     3     3     3     4     3      4
## 156    3    3     1     3     2     4     4     5     4     4     3      4
## 157    3    3     1     5     5     5     4     1     5     5     5      5
## 158    4    4     1     1     2     3     5     3     2     4     5      4
## 159    3    3     3     2     3     3     4     1     4     5     4      4
## 160    1    1     1     1     2     2     1     2     1     2     1      1
## 161    2    2     2     1     4     2     3     4     4     2     2      3
## 162    3    3     2     3     5     4     4     1     5     4     4      4
## 163    4    4     2     2     5     4     4     1     4     4     4      4
## 164    4    4     1     2     2     4     3     3     2     3     2      3
## 165    2    2     2     1     4     3     2     1     2     3     2      2
## 166    3    3     2     3     3     4     4     4     4     4     4      4
## 167    3    3     1     1     5     3     3     2     4     4     4      4
## 168    2    2     2     4     2     4     4     2     4     4     4      4
## 169    2    2     3     1     2     1     2     2     2     2     1      2
## 170    2    2     1     1     1     1     3     5     2     2     2      1
## 171    3    3     1     2     5     4     2     4     4     2     2      3
## 172    4    4     1     4     5     4     4     4     4     5     2      5
## 173    3    3     1     4     2     4     4     4     4     4     4      4
## 174    3    4     1     3     5     5     5     2     5     4     5      5
## 175    4    4     1     1     2     2     2     2     2     4     2      4
## 176    2    2     1     1     1     3     2     2     3     2     4      3
## 177    3    3     3     3     4     4     3     4     3     4     3      4
## 178    4    4     3     2     2     3     3     4     2     4     3      3
## 179    3    3     2     2     4     3     3     3     3     3     3      3
## 180    3    2     2     4     4     3     3     2     3     5     3      3
## 181    5    5     5     4     5     1     5     5     5     5     5      5
## 182    1    1     2     1     1     1     1     2     1     2     1      1
## 183    3    3     3     2     5     4     4     5     3     4     3      5
## 184    3    3     1     1     4     5     5     5     4     4     4      5
## 185    3    3     4     4     4     5     5     5     4     4     5      5
## 186    2    2     1     1     2     2     3     2     2     2     2      3
## 187    3    3     3     3     5     4     4     3     4     4     4      5
## 188    5    5     1     2     1     3     3     5     5     3     5      5
## 189    2    2     3     2     5     4     3     1     3     4     3      2
## 190    2    2     1     1     5     1     3     2     1     2     3      2
## 191    4    4     1     1     2     3     4     4     4     3     4      4
## 192    1    2     1     2     4     3     4     2     4     4     3      4
## 193    3    3     2     4     5     4     4     4     4     4     4      5
## 194    1    1     1     2     2     3     3     2     2     3     3      2
## 195    5    4     2     3     5     4     5     4     5     5     5      5
## 196    2    2     1     1     4     2     2     3     3     3     2      3
## 197    2    2     2     2     2     2     3     3     2     2     1      3
## 198    3    3     1     1     5     4     2     3     5     4     3      5
## 199    2    2     1     1     4     4     2     1     3     2     1      3
## 200    4    4     2     2     4     4     4     2     3     3     4      4
## 201    5    5     4     3     5     4     4     5     5     5     2      3
## 202    3    3     2     3     2     4     4     4     4     4     4      4
## 203    4    4     3     3     5     3     3     4     3     3     4      4
## 204    2    2     4     4     5     4     4     3     3     3     4      4
## 205    5    5     4     1     5     4     5     3     5     5     3      5
## 206    4    4     3     2     3     2     3     4     4     5     3      5
## 207    2    1     1     2     2     2     2     3     2     2     1      1
## 208    1    1     2     4     3     5     3     4     3     3     3      5
## 209    2    2     1     1     2     3     2     1     2     1     1      2
## 210    3    3     1     1     1     4     2     3     3     3     2      2
## 211    2    2     3     1     1     2     5     4     4     3     3      4
## 212    5    5     4     5     5     5     5     4     4     5     5      5
## 213    2    2     1     2     5     3     2     3     5     4     2      5
## 214    3    3     1     1     5     3     4     3     4     4     1      3
## 215    1    1     1     2     5     2     2     3     1     4     1      4
## 216    1    1     1     1     3     5     4     3     1     3     3      4
## 217    4    4     1     3     5     5     5     4     5     5     5      5
## 218    5    5     5     3     1     2     5     5     5     3     3      5
## 219    3    3     3     2     4     3     4     1     4     4     4      4
## 220    2    3     3     3     1     3     2     1     3     3     2      3
## 221    3    3     1     2     4     3     2     4     3     3     2      3
## 222    2    2     2     4     3     3     3     2     3     3     2      2
## 223    3    3     1     1     1     3     3     1     2     3     2      4
## 224    4    4     3     2     5     5     4     1     3     5     1      4
## 225    1    1     4     2     5     3     3     1     2     3     2      4
## 226    3    3     2     2     4     4     4     4     4     4     2      4
## 227    5    5     2     1     2     3     5     5     5     1     3      5
## 228    1    1     1     1     1     1     1     1     1     1     1      1
## 229    3    3     2     2     4     3     3     3     2     3     3      4
## 230    4    4     4     1     4     3     4     2     3     4     3      3
## 231    1    1     2     4     5     5     4     4     5     4     4      4
## 232    2    2     2     2     2     3     2     1     2     4     2      5
## 233    2    2     2     3     5     5     3     4     3     4     4      5
## 234    2    2     3     3     2     4     3     4     3     2     3      3
## 235    2    2     1     1     5     2     1     1     1     1     1      1
## 236    3    3     2     3     5     4     3     4     3     2     3      4
## 237    3    3     2     2     4     3     3     4     3     4     3      3
## 238    1    1     2     4     3     4     2     2     4     3     1      3
## 239    2    2     2     1     3     4     2     4     3     3     2      4
## 240    2    3     1     2     2     5     4     3     2     2     3      4
## 241    1    1     1     2     3     4     4     2     4     3     1      1
## 242    4    4     2     2     3     5     4     3     4     5     4      5
## 243    5    5     3     5     5     5     5     5     5     5     3      5
## 244    1    1     2     2     5     2     3     2     3     3     2      2
## 245    1    1     1     1     2     3     2     2     2     2     1      3
## 246    2    2     2     1     5     3     2     1     3     3     1      2
## 247    4    4     1     1     1     2     4     5     2     4     4      5
## 248    2    2     5     3     4     5     5     3     4     5     4      5
## 249    1    1     1     2     5     3     2     1     1     4     1      3
## 250    3    2     2     1     2     2     3     4     4     4     3      4
## 251    3    3     2     2     5     5     3     3     4     4     2      2
## 252    3    3     1     1     3     3     3     3     3     3     3      4
## 253    2    2     1     2     5     4     5     5     5     5     5      5
## 254    2    2     1     1     5     4     3     1     2     4     4      3
## 255    2    3     1     1     2     3     3     2     3     4     3      4
## 256    2    2     1     1     4     2     2     2     2     2     2      2
## 257    4    4     2     2     5     4     5     4     4     5     5      5
## 258    2    2     1     1     4     3     2     3     3     3     2      4
## 259    3    3     2     3     4     5     4     5     4     4     3      4
## 260    2    2     1     1     5     3     3     1     3     3     1      3
## 261    2    1     4     4     5     5     4     5     5     2     3      5
## 262    2    2     1     1     2     4     4     1     1     5     2      4
## 263    2    2     2     1     2     1     2     1     1     2     2      1
## 264    1    1     2     1     4     5     2     5     1     3     1      5
## 265    2    2     1     1     4     2     2     1     1     2     1      1
## 266    3    3     4     4     3     5     4     3     4     4     4      5
## 267    2    2     3     1     3     1     1     1     1     3     1      3
## 268    4    4     4     4     5     5     5     4     3     4     5      5
## 269    1    1     1     1     2     2     2     2     1     3     1      1
## 270    1    1     1     2     5     2     2     3     3     2     2      2
## 271    3    3     2     1     5     3     3     4     2     4     3      4
## 272    3    4     4     1     4     4     2     2     2     4     2      3
## 273    3    3     3     4     4     2     5     5     5     5     5      5
## 274    2    2     1     1     3     3     2     2     2     3     2      2
## 275    1    1     4     3     2     4     3     1     3     3     3      3
## 276    1    1     1     2     3     3     1     1     1     2     2      2
## 277    3    3     1     1     4     2     4     4     2     5     2      4
## 278    3    3     3     3     4     3     4     1     4     5     4      4
## 279    3    3     4     4     5     5     4     3     5     3     4      5
## 280    2    2     3     2     5     3     3     3     4     4     4      4
## 281    4    4     3     3     4     4     4     3     4     3     5      5
## 282    4    4     1     5     3     5     5     4     5     5     5      5
## 283    1    1     1     2     2     3     1     2     5     4     2      2
## 284    3    3     2     4     4     5     2     4     5     4     3      4
## 285    4    3     2     3     5     4     4     1     5     3     2      2
## 286    1    1     1     1     1     1     1     1     1     1     1      1
## 287    3    3     1     1     3     2     1     2     1     4     2      2
## 288    2    2     2     2     5     2     2     1     2     3     1      3
## 289    2    2     2     2     5     3     3     3     3     4     3      4
## 290    4    4     4     5     5     5     4     2     4     4     3      4
## 291    3    3     3     3     3     4     4     1     5     4     4      4
## 292    1    2     1     1     2     3     2     2     1     4     2      2
## 293    2    2     2     1     3     2     2     1     1     2     2      3
## 294    2    2     2     1     2     1     2     2     1     3     2      2
## 295    5    5     1     3     5     5     4     1     4     3     3      4
## 296    3    4     1     1     5     2     4     3     2     4     3      5
## 297    2    2     2     2     1     3     3     3     3     3     3      4
## 298    1    1     1     1     1     2     1     5     1     2     1      3
## 299    1    1     1     1     3     2     1     1     1     1     1      1
## 300    4    4     4     3     5     4     5     4     5     5     3      5
## 301    1    1     1     1     5     3     2     5     1     2     2      3
## 302    3    3     3     2     2     3     5     2     4     4     4      4
## 303    5    5     3     2     5     4     4     3     3     5     4      4
## 304    2    2     1     1     2     3     4     2     2     2     2      2
## 305    1    1     1     1     2     2     4     4     1     5     3      4
## 306    3    2     1     1     4     1     2     2     2     3     2      2
## 307    2    2     3     1     4     3     2     1     2     3     2      3
## 308    2    2     1     1     4     2     5     5     5     4     5      5
## 309    3    2     1     1     4     3     1     1     1     2     1      2
## 310    3    2     3     3     5     5     5     2     5     5     5      5
## 311    1    1     1     1     5     1     1     1     1     3     1      1
## 312    2    2     3     3     5     5     5     5     4     4     5      5
## 313    2    2     2     2     3     3     3     3     2     3     3      3
## 314    3    3     1     1     1     4     3     4     2     3     2      5
## 315    1    1     3     2     5     2     3     3     1     3     2      2
## 316    2    2     2     5     5     5     5     5     5     5     4      4
## 317    3    2     1     2     5     3     3     3     3     4     3      4
## 318    4    4     3     3     4     5     5     2     4     5     5      5
## 319    2    2     5     5     4     5     5     2     5     5     5      5
## 320    2    4     2     1     3     3     2     1     2     5     1      1
## 321    2    2     1     1     4     2     1     3     2     3     1      3
## 322    2    3     3     3     2     4     3     2     3     2     5      4
## 323    4    4     5     5     4     4     4     4     4     5     5      5
## 324    4    4     4     1     4     3     4     4     4     3     4      4
## 325    3    3     1     1     2     4     2     4     2     3     1      4
## 326    2    2     3     1     3     2     2     3     4     2     1      1
## 327    4    4     3     5     5     5     4     5     5     5     5      5
## 328    3    3     3     1     3     3     3     5     2     3     2      4
## 329    1    1     3     2     3     3     3     4     1     3     3      2
## 330    4    4     1     1     3     5     5     2     2     4     3      3
## 331    2    2     1     1     1     2     2     4     1     3     2      3
## 332    2    2     1     1     2     2     4     4     2     4     4      4
## 333    3    3     1     1     5     3     2     1     3     1     2      3
## 334    4    4     5     5     5     5     4     3     5     4     4      4
## 335    2    2     2     2     5     2     2     2     2     3     3      3
## 336    4    4     2     3     5     5     3     3     5     4     3      5
## 337    4    4     1     1     2     3     2     2     4     2     1      3
## 338    3    3     1     1     4     2     2     1     2     2     1      3
## 339    5    5     2     2     5     3     4     4     5     2     2      3
## 340    3    4     2     1     5     1     4     2     2     2     2      4
## 341    1    1     1     4     2     5     3     5     3     3     2      4
## 342    2    2     1     3     2     3     2     4     1     3     2      3
## 343    1    1     2     2     2     3     3     4     3     4     4      4
## 344    1    1     1     1     4     3     2     3     3     4     2      5
## 345    1    1     1     2     2     3     2     2     3     2     2      3
## 346    2    2     2     2     2     4     4     4     4     4     1      4
## 347    3    3     2     5     4     5     5     5     5     5     3      5
## 348    1    1     1     1     5     5     1     3     5     5     1      5
## 349    1    1     1     1     1     4     1     1     3     2     1      2
## 350    2    2     1     2     4     4     3     4     4     4     2      4
## 351    3    3     2     2     2     4     4     3     4     2     2      4
## 352    2    2     1     1     3     1     1     1     3     5     1      2
## 353    2    2     1     4     5     5     5     5     5     5     5      5
## 354    2    2     2     1     4     2     2     2     2     2     2      2
## 355    1    1     1     1     5     2     2     1     1     3     2      2
## 356    3    3     2     2     3     3     3     1     4     4     3      3
## 357    2    2     1     1     3     1     1     3     1     2     1      1
## 358    3    3     4     2     5     4     3     2     4     4     2      4
## 359    2    2     1     1     5     4     2     3     4     4     3      4
## 360    4    4     4     3     4     4     4     2     4     4     4      4
## 361    1    1     1     1     3     1     1     1     1     1     1      1
## 362    4    3     5     1     3     2     4     4     3     3     2      4
## 363    2    2     3     3     4     5     3     1     5     3     2      4
## 364    3    3     3     2     5     4     3     3     4     4     3      4
## 365    2    2     1     1     5     5     2     1     1     3     2      2
## 366    4    3     3     2     1     5     3     5     5     4     2      4
## 367    4    4     4     4     4     1     4     5     4     5     4      4
## 368    3    3     1     2     2     4     4     1     4     2     3      5
## 369    5    5     4     4     5     4     4     4     5     4     4      4
## 370    2    1     1     1     4     3     2     1     2     3     2      3
## 371    2    2     2     1     4     2     2     4     3     4     1      3
## 372    1    1     1     1     2     4     2     1     2     4     1      2
## 373    3    1     1     1     4     1     2     5     1     3     1      5
## 374    2    2     1     1     4     4     2     2     3     3     3      4
## 375    1    1     1     1     5     4     1     4     2     3     1      5
## 376    3    2     1     1     1     3     3     2     3     3     2      3
## 377    5    5     5     5     5     1     1     1     5     5     1      1
## 378    4    4     1     3     4     4     3     4     5     4     2      4
## 379    2    2     1     1     5     2     2     3     2     3     2      2
## 380    1    1     1     2     2     4     2     1     3     3     1      4
## 381    4    4     4     3     5     4     3     3     3     4     3      3
## 382    2    2     1     2     5     2     4     3     2     3     2      3
## 383    2    2     2     2     4     4     2     2     4     4     3      4
## 384    4    4     3     1     5     1     4     3     4     5     4      4
## 385    3    3     4     4     2     4     4     2     3     5     3      4
## 386    3    2     1     2     2     3     3     4     4     3     3      4
## 387    3    3     2     3     3     3     3     3     3     4     3      3
## 388    3    3     2     3     4     4     3     3     3     4     4      4
## 389    1    1     1     1     5     1     1     1     1     3     1      5
## 390    2    2     3     3     4     5     4     1     3     3     3      4
## 391    1    1     1     1     3     1     1     1     1     5     1      1
## 392    2    3     1     1     4     1     3     2     2     4     3      3
## 393    4    4     1     1     3     2     4     2     4     3     3      3
## 394    3    3     2     3     5     3     3     1     4     4     3      4
## 395    5    5     5     2     4     5     5     4     4     2     4      5
## 396    3    3     3     3     3     3     3     2     3     4     3      3
## 397    2    2     2     3     5     4     2     1     5     4     2      4
## 398    2    2     1     1     1     3     2     1     5     3     1      1
## 399    3    3     3     2     4     2     3     3     3     3     3      3
## 400    1    1     2     2     4     3     2     3     2     2     2      3
## 401    2    2     1     1     2     2     2     2     2     2     2      2
## 402    2    2     3     3     4     3     3     3     2     4     2      2
## 403    3    3     3     3     5     4     4     5     4     3     4      4
## 404    5    5     5     5     5     5     5     3     5     5     5      5
## 405    2    2     1     2     2     3     2     5     4     3     2      4
## 406    2    2     1     3     4     4     4     1     1     4     2      3
## 407    5    5     1     1     1     5     5     2     3     5     4      5
## 408    1    1     3     1     3     3     3     3     2     3     3      5
## 409    2    2     2     2     1     2     2     3     2     1     1      1
## 410    3    3     1     1     4     4     2     1     2     3     2      2
## 411    2    2     2     3     5     4     3     1     3     4     1      2
## 412    3    2     1     1     2     3     3     4     2     5     1      3
## 413    2    2     1     2     3     4     2     2     2     3     2      3
## 414    3    3     1     2     5     5     5     3     4     4     4      4
## 415    4    4     3     2     2     3     4     2     3     2     3      3
## 416    3    3     3     3     5     4     4     4     5     4     5      5
## 417    3    3     1     1     5     3     2     2     3     4     2      2
## 418    1    1     1     1     4     2     2     2     1     4     2      3
## 419    4    4     3     3     3     4     4     3     5     4     5      5
## 420    4    4     3     2     4     4     4     4     5     5     4      5
## 421    5    5     1     3     5     5     5     5     5     5     5      5
## 422    3    3     2     3     2     4     2     1     3     4     2      4
## 423    3    3     2     1     3     4     3     5     4     3     3      4
## 424    1    1     2     1     1     2     2     1     2     3     1      2
## 426    3    3     3     2     3     2     1     4     3     2     1      3
## 427    3    3     3     4     2     4     3     3     3     3     3      2
## 428    1    1     5     5     5     5     3     1     3     5     3      3
## 429    3    3     1     3     5     5     5     4     3     4     5      4
## 430    1    1     1     2     2     4     3     1     5     3     3      1
## 431    3    3     3     4     4     5     4     2     4     4     4      4
## 432    3    3     5     1     2     2     4     4     5     5     5      5
## 433    1    1     1     1     5     1     1     1     3     1     1      1
## 434    4    4     4     1     2     3     4     3     3     3     3      5
## 435    2    2     2     3     4     5     3     2     5     4     3      5
## 436    3    3     1     2     5     3     2     1     2     3     3      3
## 437    3    3     2     3     3     4     3     3     2     3     2      4
## 438    3    3     3     3     3     4     3     5     3     3     3      4
## 439    3    3     2     2     2     4     3     3     2     4     3      4
## 440    3    2     1     5     4     5     5     5     5     5     5      5
## 441    2    2     2     2     4     2     2     2     2     3     2      2
## 442    3    3     3     4     5     5     4     4     5     4     4      4
## 443    2    1     2     2     5     3     2     4     1     3     1      1
## 444    1    1     1     1     1     5     5     1     1     1     1      1
## 445    3    2     1     3     3     5     3     3     3     4     3      5
## 446    3    2     3     5     5     5     3     3     3     3     3      3
## 447    2    2     1     2     3     3     2     2     1     2     2      2
## 448    3    3     2     3     3     4     3     3     4     3     3      4
## 449    1    1     4     1     1     3     4     4     2     2     2      3
## 450    3    3     1     1     5     3     4     4     5     4     5      5
## 451    2    2     2     2     3     5     1     2     3     2     2      3
## 452    1    1     1     2     5     2     2     2     3     3     3      4
## 453    5    5     2     2     2     5     5     1     5     4     4      5
## 454    3    2     2     1     4     2     1     1     4     3     2      4
## 455    3    3     2     2     2     3     3     4     4     3     2      3
## 456    3    3     2     1     5     2     3     3     4     4     3      5
## 457    2    2     1     2     3     2     2     2     2     2     2      2
## 458    4    4     4     2     5     5     4     5     5     5     3      4
## 459    1    1     1     1     2     1     1     1     1     1     1      1
## 460    2    2     1     1     3     3     3     3     2     3     2      3
## 461    3    3     1     1     5     3     2     1     2     2     1      2
## 462    4    4     1     2     5     4     4     5     5     3     5      5
## 463    4    4     5     4     5     5     5     4     5     4     2      5
## 464    2    2     2     1     2     2     2     4     2     3     2      3
## 465    2    2     1     2     1     3     2     5     2     3     2      3
## 466    1    1     1     2     4     3     3     4     2     2     2      3
## 467    2    2     1     1     1     1     2     3     3     3     3      4
## 468    2    1     1     3     2     3     2     1     3     2     1      3
## 469    2    2     1     2     3     4     4     3     5     3     4      4
## 470    3    3     1     1     5     2     2     2     4     3     2      2
## 471    2    2     3     1     1     2     1     1     1     2     1      4
## 472    3    3     3     3     3     5     5     5     5     5     4      4
## 473    2    2     2     2     5     4     2     3     5     3     2      2
## 474    3    2     4     2     5     3     3     3     2     3     3      3
## 475    2    2     1     3     4     4     3     4     4     4     3      4
## 476    2    2     2     2     5     2     3     5     2     4     2      4
## 477    5    5     4     1     5     2     5     5     3     3     2      5
## 478    2    2     2     2     5     2     3     3     3     3     3      3
## 479    5    5     1     5     4     5     4     5     5     3     4      5
## 480    5    5     1     4     4     4     5     5     5     5     5      5
## 481    3    4     1     1     5     1     4     4     4     1     5      5
## 482    2    2     3     1     3     3     1     1     2     2     1      3
## 483    3    3     1     1     4     3     2     1     5     4     3      4
## 484    2    2     1     1     1     3     3     2     4     3     3      3
## 485    2    2     2     2     4     4     2     3     3     2     3      3
## 486    3    3     3     3     4     3     3     2     4     4     3      3
## 487    3    3     2     1     1     5     5     5     5     5     2      5
## 488    1    1     4     3     3     3     3     4     4     3     2      4
## 489    4    3     1     2     2     3     3     4     3     3     2      3
## 490    2    2     1     2     4     4     3     4     3     4     1      2
## 491    3    2     3     3     5     4     2     1     3     4     2      3
## 492    3    3     3     3     1     3     3     3     3     3     3      3
## 493    1    1     1     1     2     1     2     2     1     3     3      3
## 494    5    4     3     1     3     3     4     2     5     3     2      3
## 495    2    2     2     2     4     3     3     3     2     3     3      3
## 496    3    3     3     4     5     5     4     5     4     4     4      4
## 497    2    2     4     1     4     3     5     3     3     3     4      3
## 498    2    2     1     2     5     3     3     3     3     4     3      2
## 499    3    3     1     3     4     4     4     2     4     3     3      5
## 500    3    3     2     2     3     4     4     2     3     4     3      3
## 501    2    2     2     3     1     3     1     1     3     1     1      2
## 502    3    3     2     5     4     5     5     4     5     4     5      5
## 503    3    3     2     3     5     3     3     4     5     5     4      5
## 504    3    3     1     1     5     4     3     4     2     5     2      5
## 505    2    2     1     2     2     3     3     2     2     2     2      2
## 506    1    1     1     1     5     2     1     1     1     3     1      1
## 507    1    1     1     1     5     3     2     5     3     2     1      1
## 508    1    1     1     1     3     2     1     2     2     2     1      3
## 509    1    1     1     1     5     3     2     1     1     2     1      1
## 510    2    2     3     3     2     4     3     4     4     4     2      3
## 511    1    1     3     1     2     1     3     2     1     1     2      2
## 512    2    2     1     5     5     5     4     2     5     3     4      5
## 513    3    3     2     4     4     5     5     2     5     4     4      5
## 514    1    1     2     1     3     3     2     1     4     3     1      3
## 515    4    4     5     3     5     5     5     2     5     5     5      5
## 516    2    2     2     2     3     3     4     3     3     4     3      4
## 517    1    1     1     1     1     1     1     2     1     3     1      1
## 518    3    2     3     2     2     4     2     1     3     3     3      5
## 519    1    1     1     1     2     2     1     1     1     2     2      2
## 520    3    3     1     1     1     1     3     5     4     3     2      3
## 521    2    3     3     2     5     4     3     3     2     3     3      3
## 522    2    2     2     1     5     4     1     3     4     4     2      2
## 523    4    4     1     2     3     3     3     1     2     4     2      3
## 524    3    3     2     4     4     4     4     2     4     3     3      4
## 525    1    1     2     2     5     2     3     1     1     3     2      3
## 526    3    3     1     1     1     1     1     1     1     1     5      1
## 527    1    1     2     2     1     1     1     1     1     2     1      5
## 528    3    2     1     3     5     5     4     4     5     4     4      5
## 529    3    3     2     2     3     3     3     4     4     3     4      4
## 530    2    2     1     1     3     2     2     1     2     2     5      5
## 531    2    2     1     1     1     2     1     1     1     2     1      2
## 532    3    3     1     4     4     5     5     5     5     5     3      5
## 533    2    3     1     4     4     5     5     2     5     5     3      5
## 534    2    2     2     2     3     4     3     1     3     3     4      3
## 535    1    2     1     4     5     4     2     1     3     4     2      4
## 536    2    1     2     2     3     3     3     2     2     2     2      2
## 537    3    3     2     2     4     4     5     5     5     5     5      5
## 538    4    4     3     1     5     1     5     4     4     4     5      4
## 539    2    2     1     1     3     3     2     3     2     3     2      5
## 540    4    4     1     1     5     1     1     2     3     3     1      1
## 541    2    3     2     1     2     1     3     3     2     3     2      3
## 542    1    1     1     1     5     1     1     1     2     2     1      1
## 543    2    2     1     1     2     2     1     3     1     2     1      1
## 544    1    1     1     1     2     3     2     3     1     1     2      3
## 545    1    1     1     1     5     2     1     1     1     2     1      1
## 546    1    1     1     1     1     1     3     1     1     2     1      2
## 547    2    2     3     3     4     4     3     2     2     3     2      3
## 548    2    5     5     5     5     5     5     1     1     4     5      5
## 549    2    2     1     2     5     3     2     2     3     3     2      2
## 550    2    2     1     2     1     2     2     2     2     2     2      2
## 551    2    2     1     1     4     2     3     1     3     3     1      2
## 552    3    3     2     1     5     1     2     1     1     5     4      3
## 553    2    2     1     2     5     4     3     3     4     3     4      4
## 554    5    5     5     5     5     5     5     5     5     5     5      5
## 555    4    4     1     4     5     5     5     3     4     4     5      5
## 556    2    3     4     3     3     2     3     2     3     3     3      2
## 557    2    2     1     1     2     3     4     4     3     4     4      4
## 558    5    5     5     1     5     3     5     5     5     5     4      5
## 559    2    2     1     1     5     2     2     1     1     2     1      1
## 560    2    2     1     1     2     2     2     1     2     2     2      3
## 561    1    1     1     2     2     3     2     1     1     3     2      3
## 562    2    2     1     2     5     4     3     1     3     3     2      3
## 563    2    2     2     3     3     4     3     1     3     3     1      2
## 564    2    2     1     1     3     2     2     1     3     5     1      4
## 565    2    2     1     3     5     4     3     2     4     4     3      4
## 566    1    1     2     1     2     1     2     2     2     2     2      1
## 567    1    1     3     2     5     3     4     1     3     3     2      3
## 568    1    1     2     1     5     1     2     1     2     2     5      2
## 569    1    1     2     3     3     4     3     5     3     5     1      5
## 570    2    2     4     4     4     2     2     2     2     4     2      2
##     XAIP11 XAIP12 XAIP13 XAIP14 XAIP15 XGP1 XGP2 XGP3 XGP4 XGP5 XGP6 XGP7
## 1        2      3      3      3      2    4    3    1    3    2    2    2
## 2        3      3      2      3      3    5    3    4    4    3    3    4
## 3        2      2      1      2      2    3    1    1    2    1    2    3
## 4        2      2      3      2      4    5    2    2    3    3    4    4
## 5        4      5      5      4      3    4    1    3    5    2    2    3
## 6        4      3      5      3      2    5    1    2    5    3    4    5
## 7        3      2      3      1      5    4    3    2    2    2    2    4
## 8        2      3      3      3      3    4    2    3    4    3    3    4
## 9        3      2      5      2      5    5    1    3    3    4    3    5
## 10       2      1      2      2      2    4    4    1    1    2    1    4
## 11       4      2      3      1      2    2    1    2    4    3    2    3
## 12       1      1      1      1      1    3    1    1    2    1    2    4
## 13       4      4      4      4      5    4    4    2    2    3    2    4
## 14       4      2      4      4      5    5    1    2    1    5    3    5
## 15       3      2      3      3      4    5    3    4    2    4    3    5
## 16       4      1      4      1      3    5    2    2    4    5    2    1
## 17       2      3      3      4      3    3    2    3    3    4    2    3
## 18       3      2      3      1      2    3    2    2    3    3    2    1
## 19       4      3      3      4      5    5    3    5    4    3    2    4
## 21       2      3      3      3      3    3    2    2    3    2    2    2
## 22       4      2      2      2      4    4    2    2    2    2    2    4
## 23       4      2      4      1      4    4    2    4    3    3    4    3
## 24       5      3      3      2      3    4    3    3    5    3    3    3
## 25       4      4      4      3      4    4    3    3    3    4    3    4
## 26       1      2      3      1      2    3    1    1    2    2    2    2
## 27       3      3      3      2      3    3    1    2    3    2    2    3
## 28       3      3      3      2      3    3    1    2    3    2    2    3
## 29       5      1      5      5      5    5    5    4    4    5    5    5
## 30       5      3      2      1      1    5    1    5    2    1    1    5
## 31       4      4      5      2      4    4    1    3    5    5    3    4
## 32       4      4      3      4      5    5    4    2    5    4    3    4
## 33       2      2      2      2      3    3    2    2    2    3    3    3
## 34       4      1      2      1      3    3    1    2    3    1    2    3
## 35       2      5      3      5      3    3    1    3    5    3    3    4
## 36       4      5      4      5      5    5    2    5    5    4    5    4
## 37       4      2      3      2      3    3    2    3    4    4    2    3
## 38       2      3      2      2      2    4    2    3    2    3    3    3
## 39       5      5      5      2      5    5    3    4    3    4    2    5
## 40       3      3      4      3      4    4    4    3    3    5    3    4
## 41       4      5      2      5      5    5    2    3    3    2    4    4
## 42       3      3      4      3      4    4    1    4    1    5    3    4
## 43       2      3      1      2      5    4    2    1    3    1    3    4
## 44       3      4      4      4      4    4    2    4    2    4    3    5
## 45       5      1      4      1      4    4    3    4    2    3    3    3
## 46       5      3      3      3      3    3    2    4    5    4    3    3
## 47       1      3      5      1      5    5    1    1    1    4    1    1
## 48       3      3      4      2      3    4    3    2    3    4    5    1
## 49       5      4      2      5      5    5    5    3    2    5    2    4
## 50       3      5      5      5      5    5    3    4    5    4    3    5
## 51       1      1      2      1      3    4    3    3    1    1    2    4
## 52       5      2      3      1      1    5    1    3    2    4    1    4
## 53       5      2      4      2      3    3    3    2    2    3    2    3
## 54       4      4      5      4      5    4    4    4    4    5    4    5
## 55       1      2      2      2      2    3    2    2    1    1    5    3
## 56       4      4      5      2      2    5    1    4    4    3    2    5
## 57       5      5      5      3      5    5    3    4    5    5    3    5
## 58       4      3      5      3      5    5    5    5    4    5    4    5
## 59       4      3      5      3      5    5    3    4    5    5    5    5
## 60       5      3      4      4      4    5    3    3    3    3    4    4
## 61       5      1      2      1      2    4    2    1    2    3    2    3
## 62       1      4      4      1      1    5    1    3    1    1    1    4
## 63       2      2      3      2      2    3    3    3    2    3    4    4
## 64       5      4      5      5      4    4    4    4    4    2    3    4
## 65       4      3      2      4      4    4    3    2    4    4    2    5
## 66       4      3      2      2      5    5    3    4    3    3    4    4
## 67       4      3      2      3      5    5    3    4    1    4    3    4
## 68       5      2      4      2      4    4    2    4    5    5    5    3
## 69       4      2      2      1      2    3    2    1    1    1    2    3
## 70       1      3      1      1      1    3    1    1    1    1    1    1
## 71       3      3      2      3      4    4    4    4    4    2    2    2
## 72       5      3      2      2      4    4    4    4    4    4    2    4
## 73       4      3      4      2      3    3    4    5    5    3    3    3
## 74       3      4      4      4      4    4    2    5    3    4    2    5
## 75       1      2      4      2      3    3    2    2    2    3    2    2
## 76       5      5      3      3      5    5    5    5    3    5    5    5
## 77       2      1      1      1      4    5    4    2    1    5    4    4
## 78       3      4      3      2      1    3    3    3    4    2    2    2
## 79       2      4      5      5      5    5    3    3    2    5    3    5
## 80       3      3      2      3      2    3    3    3    2    3    2    3
## 81       3      1      3      1      3    2    1    1    1    1    1    1
## 82       1      1      1      1      2    2    3    1    5    1    1    4
## 83       5      5      1      1      1    3    1    3    3    2    2    1
## 84       5      5      5      5      5    5    1    5    5    5    1    5
## 85       1      3      4      2      1    2    1    2    1    4    3    3
## 86       1      1      4      1      2    2    1    2    2    4    2    2
## 87       3      3      3      1      5    4    3    3    3    3    3    3
## 88       5      3      4      2      4    4    3    4    3    2    4    4
## 89       3      4      3      5      3    4    2    4    5    4    1    1
## 90       4      5      3      4      2    4    1    3    4    2    3    3
## 91       4      5      2      5      5    5    4    3    2    3    3    3
## 92       5      2      3      2      3    4    2    2    5    5    2    3
## 93       4      2      2      2      4    4    4    3    2    4    3    4
## 94       4      3      4      2      2    3    2    4    3    4    3    3
## 95       4      3      3      3      3    2    2    3    2    4    2    2
## 96       2      2      2      5      4    5    3    3    3    2    2    4
## 97       2      1      1      1      3    2    1    1    3    3    2    3
## 98       1      3      4      1      3    3    1    2    4    4    5    3
## 99       5      3      4      2      4    4    4    4    5    4    3    4
## 100      3      3      4      2      5    5    4    4    4    4    3    5
## 101      2      2      2      2      3    4    2    2    1    4    2    5
## 102      1      3      2      1      1    3    1    2    3    3    2    1
## 103      3      3      3      2      2    4    2    2    3    4    3    3
## 104      3      3      4      2      2    3    3    3    3    3    3    2
## 105      1      1      1      5      5    5    5    1    1    5    1    5
## 106      1      3      4      3      5    5    2    3    4    1    3    3
## 107      2      2      3      1      3    4    2    3    3    3    3    3
## 108      2      2      5      1      5    5    1    4    3    4    3    4
## 109      3      3      1      1      4    3    1    1    2    2    1    1
## 110      5      3      4      3      5    4    4    4    5    5    2    4
## 111      4      4      4      2      4    5    4    4    5    4    4    5
## 112      5      2      2      2      3    4    3    3    4    3    4    3
## 113      1      1      1      1      5    5    5    3    1    5    3    1
## 114      3      1      3      1      1    1    1    1    1    1    1    1
## 115      1      3      4      1      3    3    2    2    3    3    2    4
## 116      2      2      2      2      3    2    1    2    1    2    2    2
## 117      3      3      3      2      1    5    2    1    2    3    4    5
## 118      3      4      4      3      4    4    4    3    5    3    3    4
## 119      2      3      5      3      5    5    4    3    3    5    2    5
## 120      4      1      4      1      5    5    5    5    1    5    2    5
## 121      2      1      1      1      1    2    1    1    1    3    2    2
## 122      4      2      5      1      4    4    3    4    1    4    2    5
## 123      3      1      4      4      3    3    2    4    1    5    3    4
## 124      2      4      1      3      5    5    2    2    4    4    3    5
## 125      4      5      5      5      3    4    3    4    1    5    5    5
## 126      3      3      4      3      2    3    4    5    5    2    5    4
## 127      2      2      3      2      4    4    3    2    4    5    3    4
## 128      3      5      4      5      5    5    2    5    5    4    3    5
## 129      5      3      5      2      5    5    4    3    5    4    3    4
## 130      4      2      2      1      2    2    2    2    1    1    2    2
## 131      4      4      4      4      4    4    4    4    1    5    4    4
## 132      3      3      3      1      2    4    3    2    2    3    3    4
## 133      2      3      2      4      4    3    2    3    3    3    3    4
## 134      4      3      4      4      4    4    2    4    4    3    4    4
## 135      4      1      1      1      1    2    4    2    1    2    2    3
## 136      4      3      3      1      3    4    2    3    1    3    2    3
## 137      3      2      2      1      4    4    2    2    4    3    2    4
## 138      3      3      3      3      2    4    2    2    3    4    4    4
## 139      2      4      4      4      3    4    4    3    4    3    4    4
## 140      1      2      1      2      1    5    1    1    2    3    2    5
## 141      2      3      2      3      3    3    2    5    3    3    3    3
## 142      1      2      4      4      4    4    5    1    3    3    2    4
## 143      4      4      5      5      5    5    5    5    3    5    5    5
## 144      5      5      4      4      5    4    4    2    4    5    4    4
## 145      2      2      2      1      1    1    1    2    1    1    1    1
## 146      3      1      3      1      3    3    2    3    5    4    3    3
## 147      1      2      1      1      1    3    4    2    5    2    1    3
## 148      4      1      3      1      2    2    1    1    3    2    3    3
## 149      4      2      3      1      3    5    1    1    1    1    1    4
## 150      2      2      2      2      2    4    2    2    5    2    3    3
## 151      4      4      3      4      4    4    3    4    3    5    4    3
## 152      3      3      4      2      2    2    3    3    3    2    3    3
## 153      5      5      2      4      4    5    3    4    3    4    3    4
## 154      2      3      3      2      4    4    5    4    3    2    2    4
## 155      2      2      2      1      4    4    2    3    3    2    3    4
## 156      3      4      3      4      4    4    2    2    3    4    3    4
## 157      5      3      4      5      4    4    3    3    3    3    4    4
## 158      3      3      3      2      4    5    2    3    1    5    4    5
## 159      5      5      5      5      5    5    5    5    5    1    4    5
## 160      1      2      1      1      2    4    1    2    1    2    2    1
## 161      2      2      4      2      2    4    2    3    4    2    3    3
## 162      3      4      3      4      4    4    2    4    3    2    3    4
## 163      3      3      4      3      3    4    3    3    2    3    3    4
## 164      3      3      3      2      2    3    3    4    3    3    4    4
## 165      2      1      3      2      2    3    2    2    2    1    2    3
## 166      3      4      2      4      2    3    2    3    3    3    3    2
## 167      2      3      4      3      3    4    1    4    2    4    3    4
## 168      4      4      2      4      4    4    3    2    5    4    3    4
## 169      2      1      2      1      2    4    1    3    2    2    2    3
## 170      1      2      2      1      2    3    1    1    1    1    1    3
## 171      1      3      1      4      3    3    2    2    3    1    3    2
## 172      4      5      2      4      2    4    3    4    4    4    3    4
## 173      2      4      2      4      3    4    4    3    4    2    4    3
## 174      4      4      1      5      5    5    5    3    1    5    3    4
## 175      3      2      4      4      4    4    2    3    3    2    2    3
## 176      2      2      2      3      4    4    4    3    5    2    2    5
## 177      3      5      3      4      4    3    2    4    2    3    3    3
## 178      4      2      3      1      2    2    1    4    3    2    3    2
## 179      3      2      3      3      3    3    3    2    3    3    3    3
## 180      2      4      2      4      5    3    1    3    5    2    1    2
## 181      4      5      5      4      5    5    4    4    5    5    3    5
## 182      2      1      2      1      1    2    1    1    2    2    1    1
## 183      3      3      4      3      3    5    2    3    1    3    3    5
## 184      4      3      5      2      5    5    4    4    3    5    5    5
## 185      3      5      3      4      4    4    3    3    3    4    2    4
## 186      2      2      1      2      2    3    1    2    1    2    2    2
## 187      3      4      2      4      5    4    2    3    3    3    2    4
## 188      4      3      3      5      5    5    2    3    5    4    1    4
## 189      4      3      4      2      3    3    3    3    3    4    3    3
## 190      2      3      2      1      2    3    1    3    5    1    2    1
## 191      3      3      3      4      4    4    4    2    4    4    3    4
## 192      1      4      3      4      3    3    3    3    4    3    1    4
## 193      3      5      4      4      5    5    4    4    5    4    3    4
## 194      1      3      1      3      1    3    1    2    4    1    2    2
## 195      4      5      3      4      5    5    2    3    2    4    4    4
## 196      2      1      2      1      2    3    2    2    2    1    2    3
## 197      3      2      2      3      2    3    2    2    3    2    2    3
## 198      1      3      2      4      2    4    1    2    4    2    2    2
## 199      3      2      1      1      2    2    3    2    2    1    2    3
## 200      3      3      3      2      4    4    3    3    1    5    4    3
## 201      4      4      4      3      5    5    3    5    4    4    4    5
## 202      4      4      5      4      5    4    2    2    3    3    4    4
## 203      4      3      5      3      3    3    3    4    4    4    3    3
## 204      2      3      4      3      4    4    1    2    2    2    3    3
## 205      4      2      3      2      5    5    4    3    4    5    3    5
## 206      3      3      3      3      5    5    3    3    1    2    2    3
## 207      1      2      1      2      2    2    1    2    1    1    1    1
## 208      3      5      3      4      4    4    2    2    5    2    3    4
## 209      5      1      3      1      1    3    1    2    2    3    4    3
## 210      2      2      3      2      2    3    4    4    5    3    3    4
## 211      4      2      4      2      5    5    3    3    2    2    2    5
## 212      5      5      5      5      5    5    5    5    4    5    5    5
## 213      2      4      3      1      4    5    2    5    1    5    3    4
## 214      4      1      2      2      3    5    2    3    5    3    5    3
## 215      3      2      3      2      2    4    2    2    2    1    2    3
## 216      1      1      1      1      1    2    2    1    2    2    1    5
## 217      4      5      4      5      4    5    3    4    4    2    3    4
## 218      1      3      1      2      5    5    3    3    2    5    2    5
## 219      4      2      5      3      3    4    2    3    4    2    4    4
## 220      3      2      4      1      5    2    1    1    2    5    1    1
## 221      2      3      4      3      3    4    2    3    4    2    2    3
## 222      2      4      2      4      3    3    1    2    2    1    1    1
## 223      1      1      2      2      2    4    1    1    2    3    1    3
## 224      3      3      3      2      4    4    4    4    4    2    5    4
## 225      4      2      4      2      4    4    1    4    5    2    1    3
## 226      2      2      2      4      4    4    2    2    2    2    2    3
## 227      3      3      2      1      5    5    3    2    3    5    3    5
## 228      1      1      1      1      1    1    1    1    2    1    1    1
## 229      3      2      3      2      3    3    1    3    2    1    3    3
## 230      2      3      4      1      4    4    3    1    4    3    3    4
## 231      2      4      2      5      5    5    1    2    4    1    2    5
## 232      2      2      3      2      3    3    3    2    2    3    2    4
## 233      5      3      5      2      4    4    2    4    3    4    3    3
## 234      3      3      4      3      4    4    3    3    4    4    3    3
## 235      1      1      1      1      1    2    1    1    2    1    1    4
## 236      4      3      2      4      2    2    1    4    5    3    3    3
## 237      3      4      3      4      4    4    3    3    2    4    3    3
## 238      2      4      2      4      3    2    2    4    1    1    2    2
## 239      5      3      4      4      1    3    1    3    4    3    1    3
## 240      3      2      4      4      3    4    3    2    3    4    3    4
## 241      1      4      4      4      3    4    1    1    5    2    3    3
## 242      5      4      5      4      4    5    5    4    2    5    5    5
## 243      5      5      4      5      5    5    5    5    2    5    3    5
## 244      4      3      2      2      3    3    1    3    1    2    2    2
## 245      1      2      1      2      1    3    2    4    1    3    1    2
## 246      3      4      3      2      3    3    1    1    1    3    1    2
## 247      2      2      1      2      5    4    2    2    3    3    2    4
## 248      5      3      5      3      5    5    4    4    5    5    3    5
## 249      4      4      3      2      3    5    1    1    4    1    3    4
## 250      2      2      2      3      3    3    4    2    2    2    1    3
## 251      4      3      4      4      3    4    3    3    3    3    3    3
## 252      3      3      2      2      4    4    2    2    2    3    2    3
## 253      2      3      5      3      5    1    4    2    2    3    3    5
## 254      2      3      3      3      3    3    1    4    5    2    4    4
## 255      3      1      4      1      4    4    3    3    4    3    3    3
## 256      3      1      2      1      3    3    2    3    2    3    2    3
## 257      2      4      3      3      4    4    4    5    3    5    2    4
## 258      3      3      3      3      3    3    3    1    3    3    3    3
## 259      3      5      2      4      4    4    3    4    4    2    2    3
## 260      3      2      4      2      2    3    2    3    4    4    5    4
## 261      4      3      5      3      5    3    3    5    5    5    3    3
## 262      2      4      2      1      3    4    1    1    1    1    2    4
## 263      3      1      4      1      1    2    2    2    1    2    1    1
## 264      1      1      1      1      3    5    1    1    5    1    1    3
## 265      4      2      2      2      2    3    2    2    3    2    2    2
## 266      2      5      2      5      4    5    3    3    1    5    2    4
## 267      2      1      3      1      4    2    3    2    1    3    2    2
## 268      2      4      2      5      5    5    2    4    1    3    3    3
## 269      3      2      4      2      4    3    1    2    1    1    2    3
## 270      1      3      3      4      1    2    1    1    3    3    3    3
## 271      2      3      1      1      4    4    4    2    3    3    3    3
## 272      4      1      3      2      2    4    2    4    2    4    4    4
## 273      5      5      5      4      4    1    3    4    5    5    5    5
## 274      3      2      2      1      3    3    1    2    3    1    2    2
## 275      1      4      1      3      2    3    1    1    3    1    1    2
## 276      2      2      2      2      2    1    1    3    3    5    4    1
## 277      3      1      4      1      1    4    1    3    1    4    3    5
## 278      2      4      4      2      4    5    2    4    2    5    2    5
## 279      3      3      3      4      5    5    3    3    5    4    3    4
## 280      3      3      4      2      5    4    2    2    5    1    2    5
## 281      4      3      3      4      3    4    2    2    4    4    3    4
## 282      2      5      3      5      5    5    5    5    5    4    2    5
## 283      3      3      4      2      2    3    1    3    3    2    1    3
## 284      5      5      5      5      4    4    3    4    4    4    4    3
## 285      4      3      4      3      3    3    4    3    3    3    3    4
## 286      4      1      3      1      1    3    1    2    1    4    4    3
## 287      2      2      2      1      3    3    2    2    2    1    1    3
## 288      4      3      4      2      4    4    2    3    1    2    4    2
## 289      3      3      3      4      4    4    2    2    2    2    2    4
## 290      5      5      5      5      5    4    3    3    5    3    4    4
## 291      2      2      4      5      5    5    5    5    5    3    4    5
## 292      3      3      2      2      2    2    1    2    2    2    2    2
## 293      3      2      2      2      3    3    2    2    2    4    2    2
## 294      2      1      2      2      4    4    2    2    5    2    3    3
## 295      3      4      2      4      4    4    4    4    5    4    5    4
## 296      3      2      5      1      4    4    3    4    4    3    4    4
## 297      4      3      4      3      3    4    2    3    3    4    2    4
## 298      3      2      3      2      1    4    1    1    3    1    1    1
## 299      3      1      1      2      1    1    1    2    3    1    1    1
## 300      3      3      5      3      4    4    3    3    1    5    4    5
## 301      4      2      4      2      2    4    1    4    3    4    4    2
## 302      1      2      1      1      4    4    1    2    3    1    3    4
## 303      4      3      2      3      4    4    4    4    4    4    3    4
## 304      4      3      2      2      2    3    2    2    4    2    3    3
## 305      2      2      3      1      4    5    1    5    1    1    1    5
## 306      2      1      2      1      2    3    1    2    5    2    1    3
## 307      4      3      4      2      3    3    2    3    3    4    2    3
## 308      5      2      4      2      5    5    3    4    2    3    4    5
## 309      1      1      1      1      2    3    2    2    3    2    1    1
## 310      5      1      5      4      4    4    3    3    3    3    3    3
## 311      1      1      1      1      1    3    1    1    1    1    1    1
## 312      3      5      3      5      5    5    2    4    2    3    3    3
## 313      2      3      2      3      2    3    2    3    2    2    2    3
## 314      2      3      2      3      3    4    1    2    1    3    3    4
## 315      1      2      3      2      2    3    2    1    2    3    3    3
## 316      2      5      2      5      5    5    1    4    5    5    4    4
## 317      2      3      4      1      4    4    1    2    1    2    4    4
## 318      4      1      1      5      4    5    4    4    4    4    4    2
## 319      4      5      3      5      4    4    3    4    4    4    3    4
## 320      4      3      4      2      3    3    1    4    2    3    3    3
## 321      4      3      4      2      2    3    2    3    4    3    4    3
## 322      4      3      3      3      4    4    4    3    2    4    1    4
## 323      4      4      3      5      5    5    5    3    2    5    5    1
## 324      2      3      4      2      4    4    5    4    2    3    4    4
## 325      1      1      1      2      1    2    1    1    5    1    2    2
## 326      2      2      2      1      2    3    2    2    2    2    2    3
## 327      4      5      3      5      5    4    4    4    5    4    5    5
## 328      1      3      3      4      4    4    2    4    3    5    1    5
## 329      1      3      2      3      4    3    1    1    5    1    3    3
## 330      4      3      1      3      5    5    3    3    1    4    3    4
## 331      1      1      2      1      1    3    1    2    2    1    2    1
## 332      2      3      2      2      3    4    1    2    3    2    3    3
## 333      4      5      4      1      3    2    1    1    1    1    1    1
## 334      5      5      5      3      5    5    4    4    4    4    3    3
## 335      2      2      3      2      4    4    3    2    2    3    3    3
## 336      3      4      4      3      3    1    3    5    4    5    2    4
## 337      1      2      1      2      1    5    1    3    2    2    2    2
## 338      2      2      2      2      2    3    2    3    2    1    2    3
## 339      1      2      1      4      5    4    1    2    4    4    4    4
## 340      5      1      4      1      5    4    3    3    2    2    2    4
## 341      2      4      2      5      3    3    1    1    1    3    1    3
## 342      4      3      3      4      4    4    3    3    2    2    2    3
## 343      1      2      2      3      4    5    2    1    1    2    5    4
## 344      3      1      2      1      3    4    1    4    4    4    1    4
## 345      4      3      2      1      2    4    2    2    2    1    2    2
## 346      3      5      1      2      3    3    3    4    3    1    1    4
## 347      4      5      3      5      5    5    3    4    5    3    1    2
## 348      1      5      1      5      4    5    1    3    4    1    1    4
## 349      3      3      3      2      1    3    1    1    2    2    1    3
## 350      3      5      5      5      3    4    2    4    4    3    3    4
## 351      3      3      2      4      3    4    2    2    2    3    3    3
## 352      1      1      1      1      1    1    1    1    1    1    1    5
## 353      3      5      2      5      5    5    3    4    5    3    3    4
## 354      2      2      3      2      2    2    2    2    3    3    2    3
## 355      1      4      4      1      1    2    1    1    4    1    1    3
## 356      3      4      3      3      3    3    2    3    3    2    3    3
## 357      2      2      1      1      1    3    1    1    1    2    2    3
## 358      2      1      2      4      5    5    4    3    2    3    1    3
## 359      3      3      2      2      4    4    3    4    1    2    5    5
## 360      4      3      3      4      4    4    4    4    3    4    4    4
## 361      2      1      1      1      2    2    1    1    1    1    1    1
## 362      5      2      4      1      1    5    1    3    3    4    4    3
## 363      2      3      4      5      3    3    1    2    2    1    1    3
## 364      2      3      3      3      3    3    4    2    4    3    3    3
## 365      1      1      1      1      1    3    1    5    5    5    3    3
## 366      2      5      5      4      5    4    3    3    3    2    3    4
## 367      5      5      5      5      5    5    5    4    4    4    4    4
## 368      3      3      2      4      4    5    4    3    4    3    4    4
## 369      3      4      3      5      4    4    4    4    3    3    3    3
## 370      2      3      1      2      3    3    2    3    2    3    3    3
## 371      4      2      3      1      4    4    2    3    1    3    2    3
## 372      2      2      2      1      2    4    1    2    5    2    1    2
## 373      2      1      2      1      1    5    1    1    3    3    1    2
## 374      4      2      2      2      1    2    2    2    1    1    1    3
## 375      1      3      2      1      1    4    1    1    2    1    2    3
## 376      1      3      2      3      2    3    2    2    2    3    2    3
## 377      5      5      5      5      5    5    5    4    5    5    5    5
## 378      5      5      1      4      3    4    2    3    3    3    2    4
## 379      1      1      2      2      2    3    3    4    5    2    2    3
## 380      2      3      3      3      1    4    1    3    4    1    3    3
## 381      4      4      4      4      4    3    1    4    5    2    5    1
## 382      3      3      3      2      3    3    3    4    1    2    3    3
## 383      4      4      2      3      2    3    2    3    2    3    3    3
## 384      4      5      5      5      5    5    3    3    4    2    5    2
## 385      3      4      4      4      4    4    3    3    4    4    4    4
## 386      4      2      3      2      2    4    2    4    1    4    2    3
## 387      4      3      4      3      3    3    2    3    3    3    3    3
## 388      4      4      4      4      4    4    3    4    3    3    4    3
## 389      5      3      1      1      2    3    1    2    5    1    1    1
## 390      4      4      5      4      5    4    5    4    4    4    1    5
## 391      1      1      2      1      2    3    1    1    3    1    2    2
## 392      2      1      2      1      3    4    2    3    1    3    2    4
## 393      3      1      4      1      4    4    3    3    4    4    4    4
## 394      3      5      4      3      5    4    3    3    2    4    3    3
## 395      5      3      5      4      5    5    4    2    3    4    4    4
## 396      4      3      3      3      3    3    4    3    2    3    3    3
## 397      3      4      5      3      3    2    1    4    3    2    1    2
## 398      3      3      2      3      3    3    1    2    3    1    3    3
## 399      3      3      4      2      5    5    4    4    3    3    3    4
## 400      3      3      2      3      2    3    2    2    2    3    2    3
## 401      2      3      2      2      2    2    2    2    2    2    3    2
## 402      2      3      2      2      3    3    2    2    4    2    4    2
## 403      4      4      3      3      4    4    2    2    3    4    2    4
## 404      4      5      5      5      5    5    4    4    5    4    3    5
## 405      3      4      2      2      2    2    1    1    3    3    2    3
## 406      3      4      3      4      3    2    2    1    5    1    1    3
## 407      4      1      2      1      5    5    4    4    2    4    2    5
## 408      3      3      2      2      3    3    1    2    2    1    2    1
## 409      2      2      2      1      2    1    1    1    5    3    2    2
## 410      5      3      3      2      2    3    3    3    4    1    3    3
## 411      2      4      2      3      2    4    1    4    2    5    1    3
## 412      3      3      3      1      2    3    2    3    5    1    2    4
## 413      4      4      4      4      2    3    2    2    3    1    3    3
## 414      4      4      3      4      4    4    4    3    4    4    3    4
## 415      2      2      4      2      4    4    2    2    4    3    4    4
## 416      5      4      4      3      5    5    2    3    2    4    3    4
## 417      1      3      2      1      3    4    3    4    1    4    2    3
## 418      3      3      4      2      2    2    1    2    5    1    2    2
## 419      2      4      5      3      4    3    3    4    5    3    4    5
## 420      3      4      3      4      4    5    3    3    4    2    4    4
## 421      5      5      2      5      5    5    5    5    5    4    4    5
## 422      4      3      3      4      5    5    4    2    2    4    2    4
## 423      2      3      2      3      4    4    2    4    4    3    2    3
## 424      2      2      2      2      2    2    1    2    1    2    1    3
## 426      2      3      2      2      4    4    1    2    3    2    5    4
## 427      3      4      4      4      4    4    2    4    5    2    2    3
## 428      5      5      5      5      4    3    1    4    1    3    3    2
## 429      3      5      2      5      5    5    3    2    4    4    1    5
## 430      5      3      4      2      3    5    1    3    3    1    2    3
## 431      4      4      2      4      4    4    4    2    4    3    3    4
## 432      5      2      5      2      5    5    3    5    5    4    2    4
## 433      1      1      3      1      1    5    1    1    2    1    1    1
## 434      5      2      5      2      3    1    3    5    2    5    1    4
## 435      3      3      3      4      3    4    3    3    5    3    2    4
## 436      4      3      4      2      2    2    3    4    4    3    3    2
## 437      3      4      2      4      5    5    3    2    4    5    2    3
## 438      3      3      3      3      4    4    2    3    3    4    3    3
## 439      3      2      3      3      4    4    3    3    2    2    3    3
## 440      3      5      3      5      5    5    3    5    4    4    4    5
## 441      2      3      2      2      3    2    2    3    2    2    2    2
## 442      4      5      5      4      4    4    5    4    4    4    4    4
## 443      5      3      1      2      2    2    1    2    2    1    2    2
## 444      2      1      1      1      2    1    1    5    2    1    1    2
## 445      3      5      3      4      4    3    2    2    3    3    2    2
## 446      4      5      3      5      5    4    2    4    4    5    4    4
## 447      2      2      2      2      2    2    2    2    2    2    2    2
## 448      2      5      3      5      4    4    2    3    2    2    3    5
## 449      3      3      1      2      3    2    1    2    3    1    5    3
## 450      2      3      4      3      5    5    2    4    1    3    2    5
## 451      4      3      4      4      3    4    1    3    5    2    4    4
## 452      2      4      2      1      1    2    1    2    1    1    2    2
## 453      5      3      4      4      5    5    1    3    4    3    3    5
## 454      2      2      3      3      2    3    3    3    1    3    2    3
## 455      2      4      2      4      4    3    2    4    3    2    2    3
## 456      3      1      3      1      3    4    3    4    2    2    2    3
## 457      2      2      2      2      2    2    2    2    2    2    2    2
## 458      4      5      4      4      5    5    5    5    5    5    5    5
## 459      1      1      1      1      1    1    1    1    1    2    1    1
## 460      2      1      3      1      4    5    1    1    1    3    1    4
## 461      5      2      3      2      3    3    2    3    2    4    3    3
## 462      2      4      3      4      5    5    1    4    4    5    2    5
## 463      2      5      5      4      5    5    3    5    5    2    4    1
## 464      4      2      2      2      3    3    2    3    2    4    4    3
## 465      2      3      2      3      1    2    1    2    2    1    1    2
## 466      1      3      2      1      2    3    1    1    1    1    2    1
## 467      3      3      1      1      3    2    2    2    4    3    2    4
## 468      2      3      2      3      2    2    1    2    1    1    3    2
## 469      1      3      2      4      3    4    3    4    2    3    3    5
## 470      2      2      3      2      3    3    2    2    3    3    2    2
## 471      3      2      3      1      1    3    3    1    1    1    2    3
## 472      5      5      5      5      5    5    5    4    2    3    4    4
## 473      2      4      2      3      4    3    2    4    4    1    1    3
## 474      3      3      4      2      4    5    2    3    2    4    3    4
## 475      3      4      3      4      3    4    2    4    2    2    3    3
## 476      2      3      1      3      5    3    1    1    4    1    1    1
## 477      3      2      5      1      5    5    3    2    2    5    3    5
## 478      2      2      2      3      4    3    3    2    3    3    3    2
## 479      3      5      3      5      5    5    3    1    5    3    1    4
## 480      3      3      2      4      5    5    4    3    3    3    1    5
## 481      2      1      2      2      5    4    4    4    5    3    2    4
## 482      1      1      1      1      3    3    1    1    3    1    2    2
## 483      4      2      4      2      3    4    3    5    4    5    5    4
## 484      3      1      2      2      3    3    3    2    2    3    2    3
## 485      2      3      3      2      2    2    1    2    4    3    2    3
## 486      4      4      4      3      4    3    4    4    3    3    3    2
## 487      2      4      3      5      5    5    5    1    5    5    4    5
## 488      3      4      5      4      4    4    5    2    1    4    2    4
## 489      2      3      2      3      3    3    3    4    4    2    3    4
## 490      2      3      5      4      3    4    1    3    5    4    3    4
## 491      5      5      5      4      4    4    4    4    5    4    3    3
## 492      3      5      3      3      3    3    3    3    3    3    5    3
## 493      2      1      2      1      1    3    1    2    2    1    3    2
## 494      5      3      3      2      4    4    4    4    5    2    3    4
## 495      1      2      1      4      5    4    1    2    1    3    3    3
## 496      2      4      4      4      4    4    4    2    3    5    3    4
## 497      5      1      4      1      5    5    1    3    5    3    5    5
## 498      4      3      4      2      3    3    2    2    5    2    3    2
## 499      4      3      4      4      3    3    3    2    1    1    2    3
## 500      3      3      4      3      4    3    3    3    3    3    3    3
## 501      2      4      3      4      2    3    1    1    2    3    1    2
## 502      3      4      4      4      5    5    3    4    3    3    4    5
## 503      1      3      4      3      3    4    2    3    2    3    4    3
## 504      4      2      1      1      3    4    2    4    4    3    4    4
## 505      3      4      3      4      2    3    2    2    1    2    3    3
## 506      3      3      2      1      2    1    1    2    1    1    3    1
## 507      1      2      3      1      1    1    1    3    1    1    2    1
## 508      4      1      2      1      1    2    1    2    1    2    2    3
## 509      2      2      1      1      1    4    1    2    1    1    1    2
## 510      4      4      4      3      5    5    3    3    3    4    3    5
## 511      3      1      4      1      1    3    1    2    1    3    2    3
## 512      2      5      1      5      4    4    3    3    5    3    5    3
## 513      4      5      4      5      5    5    3    4    4    4    3    5
## 514      3      2      3      1      5    3    4    3    3    3    2    3
## 515      4      5      5      4      5    4    4    4    4    4    5    5
## 516      5      2      3      2      5    5    2    2    3    2    3    3
## 517      4      1      2      1      4    2    1    2    3    2    2    3
## 518      4      2      4      2      4    4    2    3    5    3    2    3
## 519      2      1      2      2      2    2    1    1    1    1    2    1
## 520      4      4      5      2      3    4    3    2    1    2    3    5
## 521      2      3      3      2      4    3    3    3    4    4    4    3
## 522      2      2      2      3      3    4    1    2    2    4    2    4
## 523      3      2      4      2      3    4    5    4    4    3    4    4
## 524      4      4      2      4      4    2    2    3    3    3    3    3
## 525      4      2      3      2      1    4    2    2    4    3    2    3
## 526      3      1      1      1      1    1    1    1    2    5    1    4
## 527      3      2      3      1      2    2    1    2    2    1    2    2
## 528      3      5      3      4      3    4    3    4    2    3    3    3
## 529      4      3      2      3      5    3    2    3    3    3    3    4
## 530      2      3      4      1      3    3    1    1    4    2    2    4
## 531      2      1      1      1      1    2    1    1    1    1    2    2
## 532      1      4      2      4      4    4    3    3    5    2    2    2
## 533      1      3      2      4      3    5    4    4    2    2    2    3
## 534      3      3      4      3      1    3    3    4    2    4    3    3
## 535      3      4      2      5      2    4    2    3    5    1    3    3
## 536      1      3      1      3      2    2    1    1    5    1    1    4
## 537      2      4      5      5      4    5    1    5    3    5    3    3
## 538      2      2      4      1      4    5    3    3    4    4    4    4
## 539      2      2      1      2      3    5    1    2    3    5    5    4
## 540      2      1      1      1      3    4    1    1    3    1    1    4
## 541      2      1      3      1      2    3    2    3    2    2    3    2
## 542      3      2      2      3      3    2    1    5    2    1    1    3
## 543      2      1      2      1      2    2    1    1    2    3    2    3
## 544      3      2      3      1      2    2    1    1    1    2    1    3
## 545      2      2      2      1      1    1    1    2    2    1    1    1
## 546      2      3      3      1      4    3    2    2    2    2    1    2
## 547      3      3      4      3      3    3    3    4    4    3    3    3
## 548      5      5      5      5      5    5    5    5    5    5    4    3
## 549      4      4      2      5      2    2    3    5    3    2    3    4
## 550      4      3      3      2      2    2    2    3    3    2    2    2
## 551      4      2      4      2      1    1    1    5    2    2    4    1
## 552      3      1      4      1      3    3    1    2    2    1    2    2
## 553      4      3      3      3      4    4    2    4    4    2    2    4
## 554      5      5      5      5      5    5    4    4    4    4    4    4
## 555      1      5      2      4      5    4    1    1    3    2    1    5
## 556      3      3      3      3      3    3    3    3    3    3    3    3
## 557      4      4      2      4      3    4    1    2    3    4    3    3
## 558      4      2      5      3      5    5    5    4    3    5    2    5
## 559      2      2      2      2      2    2    2    2    1    1    2    2
## 560      4      2      4      2      1    3    1    2    2    3    3    2
## 561      1      2      3      2      3    2    1    2    3    1    2    1
## 562      2      4      2      3      3    3    2    2    5    1    2    2
## 563      2      4      2      2      3    3    2    2    2    4    2    4
## 564      1      2      2      1      2    3    1    2    5    2    3    3
## 565      2      4      2      3      4    4    1    1    1    1    4    2
## 566      4      1      2      1      2    2    3    3    4    1    2    2
## 567      2      3      2      2      3    4    1    2    3    3    3    4
## 568      2      2      4      2      1    3    1    4    2    1    1    2
## 569      1      4      3      2      1    2    1    2    4    3    4    1
## 570      4      4      4      2      2    2    2    4    4    2    4    2
##     XGP8 XGP9 XGP10 XGP11 XGP12 XGP13 XGP14 XGP15 XGP16 XGP17 XGP18 XGP19
## 1      3    4     2     2     4     3     3     4     3     2     4     4
## 2      4    4     4     4     5     2     3     4     5     2     4     4
## 3      3    3     1     1     4     1     2     3     2     2     3     2
## 4      4    5     2     2     5     3     2     5     3     3     5     5
## 5      4    4     4     2     3     4     4     3     4     2     4     3
## 6      4    4     5     5     3     1     4     3     2     2     4     5
## 7      2    4     2     4     5     3     4     5     4     4     5     4
## 8      4    4     3     4     4     3     4     4     4     3     4     4
## 9      3    5     2     1     5     4     3     5     5     4     5     5
## 10     3    4     2     3     3     2     3     2     3     4     4     2
## 11     2    3     1     5     1     1     2     3     3     1     3     2
## 12     1    1     1     1     1     1     1     1     5     2     2     2
## 13     4    4     4     4     4     3     4     4     5     3     3     3
## 14     3    4     5     3     5     4     3     5     5     4     5     5
## 15     4    5     3     2     4     3     4     5     5     2     4     4
## 16     3    1     2     2     2     3     5     2     4     4     4     4
## 17     3    4     4     3     4     3     4     4     5     5     3     3
## 18     2    3     3     4     3     4     3     3     4     2     4     2
## 19     3    4     4     3     4     4     4     3     5     3     3     5
## 21     2    3     2     3     3     3     2     3     3     2     3     3
## 22     2    4     2     3     4     2     2     3     4     3     3     4
## 23     4    3     3     4     4     3     4     4     4     4     4     3
## 24     4    5     3     4     5     3     4     4     4     3     4     3
## 25     3    3     4     4     3     4     5     4     4     4     2     3
## 26     3    3     1     5     3     3     2     3     3     2     3     3
## 27     3    4     2     3     4     1     2     4     3     3     3     4
## 28     3    4     2     3     4     1     2     4     3     3     3     4
## 29     4    5     5     5     5     5     5     5     5     5     5     5
## 30     4    4     5     5     3     2     4     4     1     1     4     3
## 31     3    4     5     5     4     5     4     4     5     5     3     3
## 32     4    4     2     4     4     3     3     3     5     5     4     4
## 33     3    3     3     4     3     3     4     3     3     3     4     3
## 34     2    3     1     4     3     2     2     3     5     2     4     3
## 35     3    4     5     5     4     3     3     5     4     4     4     3
## 36     4    4     4     4     4     4     4     4     5     4     5     4
## 37     3    3     1     4     3     4     4     3     3     3     3     3
## 38     3    4     4     2     4     4     4     3     4     3     4     4
## 39     4    5     2     3     5     5     4     5     5     4     5     5
## 40     3    4     4     3     4     1     4     4     4     3     4     5
## 41     3    3     2     4     4     3     4     3     4     3     4     4
## 42     4    4     4     4     4     3     4     4     4     4     4     4
## 43     3    5     5     4     5     3     2     4     3     3     4     5
## 44     4    2     3     4     4     4     4     4     4     4     5     5
## 45     4    4     1     2     3     4     4     3     4     4     4     4
## 46     3    3     3     4     4     4     4     4     4     4     3     4
## 47     3    3     5     5     3     5     3     5     5     5     5     1
## 48     4    2     5     2     4     3     3     3     5     4     5     2
## 49     1    4     2     5     5     3     3     4     5     4     5     5
## 50     3    4     4     5     5     4     5     5     5     5     4     5
## 51     2    4     1     2     4     1     1     3     4     3     3     4
## 52     4    1     1     4     4     2     2     5     4     4     4     2
## 53     3    3     2     2     3     1     1     3     2     2     4     3
## 54     4    5     4     5     5     3     5     4     4     4     5     4
## 55     2    2     1     3     2     1     1     3     4     2     2     2
## 56     4    4     4     4     5     3     3     4     4     3     4     4
## 57     4    4     4     1     5     5     3     5     4     4     5     5
## 58     4    5     5     1     5     5     3     5     5     5     5     5
## 59     5    5     4     4     5     5     5     5     5     5     5     5
## 60     3    5     4     3     4     4     4     4     5     4     5     5
## 61     2    4     1     4     2     2     3     3     3     3     4     3
## 62     3    4     3     3     4     5     3     1     5     4     5     4
## 63     3    3     3     4     3     2     3     3     4     4     3     4
## 64     4    4     3     3     3     4     4     4     4     4     4     2
## 65     4    4     1     4     4     4     4     4     3     2     5     4
## 66     4    4     4     4     4     4     4     4     4     4     4     5
## 67     4    4     4     2     5     3     4     5     4     3     4     4
## 68     4    3     2     4     2     3     2     4     5     4     4     5
## 69     3    5     1     5     3     1     1     3     3     2     3     3
## 70     1    1     5     5     1     1     1     1     1     1     1     1
## 71     2    2     2     3     4     2     3     4     3     2     3     2
## 72     4    5     1     2     4     4     4     2     4     4     4     4
## 73     3    3     3     4     5     4     5     4     5     4     4     2
## 74     2    4     5     4     5     1     5     4     3     3     4     5
## 75     2    3     1     2     3     2     3     3     4     3     4     4
## 76     5    1     5     1     5     5     5     5     5     4     5     5
## 77     5    5     5     5     4     5     5     5     5     5     5     5
## 78     4    3     2     4     2     3     3     3     2     2     3     2
## 79     3    5     3     3     5     4     3     4     5     5     4     5
## 80     3    4     4     4     3     2     2     4     4     3     4     4
## 81     3    3     1     1     2     1     1     3     3     1     2     1
## 82     1    1     1     5     1     1     1     2     3     2     4     5
## 83     3    3     5     5     1     5     5     4     3     2     3     4
## 84     5    1     1     5     2     3     2     1     4     3     4     1
## 85     3    2     2     3     2     3     4     3     2     2     3     2
## 86     2    3     2     4     2     2     2     2     3     2     3     1
## 87     4    4     5     3     4     3     2     5     4     4     4     4
## 88     4    4     3     3     4     3     4     4     4     4     4     3
## 89     1    3     4     1     2     2     2     4     3     3     3     2
## 90     5    5     4     1     4     1     2     3     4     4     4     3
## 91     4    4     5     4     4     4     5     5     5     4     5     4
## 92     3    4     1     3     4     3     3     4     5     5     4     4
## 93     3    4     4     3     3     2     2     4     4     3     4     3
## 94     4    4     3     5     3     3     4     3     5     5     4     3
## 95     3    3     2     3     3     2     2     3     2     2     3     2
## 96     4    4     3     3     4     2     4     4     5     5     4     5
## 97     1    3     1     3     3     3     1     3     3     1     2     2
## 98     3    4     2     3     2     2     2     2     4     2     4     3
## 99     1    2     4     2     5     4     4     5     2     2     3     4
## 100    4    5     3     4     5     3     3     4     5     5     4     5
## 101    4    4     4     3     4     1     3     3     5     5     4     3
## 102    2    2     1     3     3     1     3     3     2     2     3     1
## 103    3    3     2     3     3     3     5     3     4     3     3     3
## 104    2    3     4     3     5     3     3     3     5     4     3     3
## 105    1    5     5     1     5     1     1     1     5     5     1     5
## 106    5    5     3     4     5     4     4     5     4     4     5     5
## 107    4    4     2     4     5     4     4     4     4     4     4     4
## 108    5    4     3     5     4     5     4     4     4     4     5     5
## 109    4    3     2     2     3     1     1     2     2     1     2     2
## 110    3    4     4     3     4     3     3     5     5     4     5     5
## 111    5    4     3     2     4     4     4     5     5     4     5     4
## 112    2    3     1     2     4     2     3     3     4     3     3     3
## 113    1    1     1     1     1     5     1     3     5     3     5     5
## 114    1    1     1     1     1     1     1     1     3     3     1     1
## 115    3    4     1     4     4     2     2     3     4     4     4     4
## 116    2    2     1     5     2     2     2     2     2     2     2     2
## 117    5    5     1     2     5     2     4     5     4     3     5     5
## 118    2    4     5     2     5     3     3     5     4     2     4     4
## 119    3    4     5     4     5     3     2     4     5     4     5     5
## 120    5    5     1     2     4     1     2     3     4     4     3     5
## 121    2    1     1     1     1     2     3     1     2     1     2     2
## 122    3    5     2     3     5     4     3     5     5     4     4     4
## 123    4    3     2     4     3     3     3     3     4     4     2     2
## 124    4    5     5     5     5     3     3     3     4     4     5     5
## 125    5    5     5     1     5     4     5     5     5     4     4     5
## 126    4    3     2     4     3     3     4     4     4     4     4     4
## 127    3    3     3     2     4     4     3     4     2     3     5     4
## 128    5    5     5     3     5     3     4     5     3     4     5     5
## 129    2    5     3     4     4     5     4     5     5     5     5     5
## 130    3    2     1     2     3     4     4     2     2     2     2     2
## 131    3    4     4     2     4     4     4     4     4     4     4     4
## 132    2    4     2     4     4     2     2     4     3     3     4     4
## 133    3    3     3     2     3     3     4     4     2     3     3     3
## 134    4    4     4     4     4     4     4     4     4     4     4     4
## 135    2    2     1     1     1     1     2     2     5     2     1     2
## 136    4    4     2     3     4     1     4     5     4     4     3     5
## 137    4    4     1     2     4     2     2     4     4     3     4     5
## 138    4    3     3     2     3     2     2     4     2     2     3     3
## 139    4    4     3     4     4     2     3     4     5     5     4     4
## 140    3    5     1     2     5     2     3     4     4     1     5     3
## 141    4    4     3     3     4     2     4     3     3     3     4     3
## 142    3    3     3     4     4     2     4     3     4     4     5     4
## 143    3    5     5     4     5     4     5     5     5     5     4     5
## 144    3    4     4     5     4     3     4     4     4     4     4     4
## 145    1    2     1     3     1     2     1     2     1     1     2     1
## 146    4    3     2     4     3     4     5     3     4     4     4     4
## 147    3    4     4     3     4     1     1     3     4     2     5     1
## 148    3    3     1     1     2     2     1     1     4     3     3     2
## 149    2    5     1     3     4     1     1     4     3     1     5     5
## 150    3    4     3     3     4     2     3     3     5     3     5     3
## 151    4    4     4     4     4     3     4     5     4     3     4     4
## 152    4    3     2     4     3     3     3     3     3     2     4     3
## 153    5    5     4     4     5     4     4     5     5     4     4     3
## 154    4    4     4     4     4     4     3     3     4     3     5     5
## 155    4    5     2     2     4     4     3     4     4     3     4     4
## 156    4    4     4     4     4     3     3     4     4     4     4     4
## 157    4    4     2     4     5     2     4     5     5     3     5     5
## 158    3    5     3     2     5     1     1     4     5     5     3     5
## 159    4    5     5     5     5     5     5     5     5     5     4     5
## 160    2    2     1     4     2     3     2     2     2     2     2     1
## 161    3    4     2     2     4     2     4     4     4     4     4     4
## 162    4    4     3     4     4     3     4     4     4     4     4     4
## 163    3    4     4     4     4     2     3     4     5     4     5     4
## 164    4    4     4     4     4     2     3     4     4     4     3     2
## 165    3    3     1     3     2     2     2     3     2     2     3     3
## 166    4    4     3     3     4     2     3     4     3     3     4     3
## 167    4    4     4     4     5     3     4     4     5     5     4     5
## 168    4    4     2     4     4     4     4     4     3     2     4     5
## 169    3    3     4     2     3     4     3     3     3     2     3     3
## 170    2    3     1     1     2     1     1     3     2     1     3     3
## 171    3    2     1     2     3     1     1     3     5     4     2     3
## 172    3    4     4     4     4     3     3     4     4     4     4     4
## 173    3    4     4     4     4     1     4     4     4     3     4     4
## 174    3    4     4     5     5     1     4     2     3     3     3     2
## 175    3    3     3     3     4     3     3     4     4     2     5     4
## 176    4    3     2     5     5     2     2     3     3     2     2     3
## 177    4    3     5     4     3     3     4     4     4     2     3     3
## 178    4    4     1     3     3     4     3     4     5     3     5     4
## 179    3    3     3     3     3     3     3     3     3     3     3     3
## 180    4    4     4     4     3     3     1     4     2     1     3     2
## 181    4    5     5     5     5     4     4     1     5     5     5     4
## 182    2    2     2     4     2     2     1     2     2     1     2     2
## 183    4    5     4     4     3     2     5     3     4     3     4     3
## 184    5    5     3     3     5     3     5     4     5     5     5     5
## 185    4    4     5     4     4     2     2     4     4     4     4     4
## 186    2    2     2     3     3     1     2     3     2     2     3     3
## 187    3    4     4     4     5     3     3     4     5     5     5     4
## 188    2    3     1     5     3     1     3     3     5     3     3     5
## 189    3    4     2     3     3     4     4     5     5     5     3     4
## 190    2    3     1     1     4     1     2     3     3     3     3     1
## 191    4    4     3     4     4     2     4     4     4     4     4     4
## 192    2    5     4     2     5     3     5     5     4     3     4     4
## 193    5    5     3     5     4     4     3     4     5     5     5     4
## 194    2    3     2     2     3     1     1     3     4     2     4     4
## 195    4    4     3     5     4     3     5     5     4     4     5     4
## 196    2    4     1     2     3     1     1     2     2     2     2     3
## 197    2    2     2     2     2     3     4     2     3     2     3     3
## 198    3    3     4     2     4     2     4     3     3     2     3     2
## 199    4    3     1     1     2     2     2     2     3     3     3     3
## 200    4    4     4     4     5     4     3     4     4     4     5     3
## 201    4    5     4     4     5     3     5     5     5     4     5     5
## 202    1    5     4     3     5     2     5     4     3     4     4     4
## 203    3    3     3     4     3     3     5     3     4     3     4     3
## 204    4    3     3     3     3     3     2     4     2     2     4     3
## 205    4    5     5     4     5     4     4     4     5     5     5     5
## 206    4    3     2     4     2     1     2     2     3     3     4     3
## 207    1    2     1     1     2     1     1     1     1     1     2     2
## 208    3    3     4     5     4     3     3     4     4     4     4     3
## 209    2    3     1     1     3     1     4     2     3     2     2     3
## 210    4    4     2     2     4     1     3     3     4     3     2     3
## 211    2    5     2     2     5     4     4     4     5     3     5     4
## 212    5    5     5     5     4     4     5     5     5     5     5     5
## 213    5    4     5     3     4     5     5     3     4     4     3     3
## 214    3    4     1     3     2     2     4     3     3     2     5     5
## 215    2    2     2     4     4     4     2     3     4     4     3     2
## 216    2    4     1     2     4     1     3     3     3     2     4     4
## 217    4    5     4     5     4     2     4     4     5     4     4     5
## 218    4    4     2     4     5     5     5     4     5     4     5     5
## 219    4    3     3     3     3     5     5     5     5     5     4     4
## 220    3    1     1     5     2     4     2     3     5     3     2     2
## 221    4    4     2     3     3     2     2     3     3     2     2     3
## 222    4    4     1     4     3     3     3     3     4     2     3     2
## 223    3    4     2     2     4     2     2     3     2     2     4     3
## 224    3    4     2     3     4     3     3     5     4     2     5     5
## 225    1    5     2     4     3     4     4     3     5     5     3     4
## 226    3    4     4     2     4     2     2     4     4     4     4     4
## 227    5    1     3     2     5     3     2     4     5     4     1     5
## 228    1    1     1     2     2     1     1     1     1     1     1     1
## 229    4    3     3     2     3     2     4     3     4     3     4     2
## 230    3    4     2     3     4     5     5     3     4     4     3     3
## 231    2    5     5     5     5     2     2     4     3     2     5     5
## 232    3    3     2     2     4     3     3     3     5     4     3     4
## 233    4    4     1     2     5     2     3     4     5     3     5     5
## 234    3    3     3     3     4     4     4     3     5     4     3     4
## 235    2    3     5     2     3     1     2     2     2     2     2     2
## 236    3    5     3     4     4     3     4     3     4     3     5     3
## 237    4    3     3     4     3     3     3     4     4     3     3     4
## 238    3    4     2     3     2     4     2     3     3     2     2     2
## 239    5    3     4     4     2     1     4     2     5     5     4     4
## 240    3    3     4     4     3     2     3     3     4     4     3     4
## 241    2    4     3     4     3     3     2     3     3     2     5     5
## 242    5    4     5     4     5     4     4     5     5     5     5     1
## 243    5    5     5     5     5     4     2     4     5     5     5     5
## 244    3    2     1     2     2     3     4     3     2     1     3     2
## 245    2    3     2     2     3     2     2     3     4     2     3     3
## 246    2    2     2     3     2     2     2     3     3     2     3     3
## 247    3    4     2     3     5     1     2     5     3     3     5     3
## 248    2    5     4     4     5     5     4     4     4     5     5     5
## 249    2    3     3     3     3     4     4     4     1     1     4     3
## 250    2    3     1     3     4     2     2     4     4     2     4     3
## 251    4    4     4     4     4     3     4     4     4     4     5     4
## 252    3    4     2     2     4     2     3     4     3     3     4     4
## 253    1    5     1     5     5     1     3     5     4     4     5     5
## 254    3    3     4     4     4     3     4     3     5     3     3     4
## 255    4    3     3     4     3     2     3     4     4     4     4     4
## 256    2    3     1     2     2     3     3     2     4     2     3     3
## 257    4    5     3     2     5     4     4     5     5     5     5     4
## 258    3    3     3     3     3     3     3     3     4     4     5     5
## 259    4    4     3     5     5     2     4     4     4     3     4     4
## 260    3    1     2     3     3     1     2     3     4     2     4     2
## 261    1    3     5     5     4     5     5     5     5     5     3     3
## 262    4    4     3     5     4     2     2     5     4     1     5     1
## 263    1    1     1     4     2     2     2     2     3     4     2     2
## 264    1    3     1     5     5     1     1     3     1     1     5     4
## 265    3    3     2     2     3     3     4     3     4     4     4     3
## 266    3    4     5     5     4     4     3     4     5     2     5     4
## 267    3    3     1     1     2     4     3     2     4     2     2     3
## 268    3    5     4     1     5     3     4     4     5     4     4     5
## 269    2    4     1     3     3     3     3     3     4     4     3     4
## 270    2    4     1     2     3     2     2     2     1     1     3     3
## 271    3    5     1     3     3     4     4     4     1     3     4     3
## 272    4    4     2     3     4     4     4     4     4     4     2     2
## 273    5    5     3     3     4     4     4     5     4     4     5     5
## 274    3    3     2     2     2     1     3     3     1     1     4     3
## 275    2    3     3     2     3     3     2     3     4     2     2     2
## 276    2    1     1     1     2     2     2     2     2     2     1     2
## 277    2    4     1     2     5     4     4     5     4     3     5     3
## 278    3    5     3     4     5     3     5     4     5     4     5     4
## 279    3    4     4     1     5     3     4     4     5     4     4     5
## 280    3    5     3     3     4     5     4     4     2     3     4     5
## 281    5    4     3     3     4     5     4     4     5     4     4     4
## 282    5    5     5     5     5     2     5     5     5     3     5     5
## 283    5    5     1     3     3     3     2     4     3     3     3     4
## 284    4    4     3     3     4     1     3     4     4     3     4     2
## 285    2    3     3     3     3     4     4     4     5     3     3     3
## 286    3    3     1     1     4     4     3     2     5     3     4     2
## 287    2    3     1     2     3     1     2     2     3     2     3     3
## 288    2    3     3     3     3     2     2     3     4     3     3     3
## 289    2    4     2     3     4     3     2     4     4     3     2     3
## 290    3    4     5     5     4     3     5     4     5     5     4     3
## 291    4    4     4     5     4     5     5     3     4     4     5     5
## 292    3    3     1     2     2     2     3     4     4     3     2     3
## 293    2    2     2     3     3     2     4     3     3     3     2     3
## 294    3    4     2     3     4     3     3     3     3     2     3     4
## 295    5    4     3     4     4     1     5     4     1     4     4     5
## 296    4    4     2     3     3     4     5     4     4     3     4     3
## 297    4    4     3     4     4     3     4     3     4     4     3     4
## 298    1    3     1     1     1     1     1     5     3     1     2     3
## 299    3    2     1     2     1     2     2     2     2     2     1     2
## 300    4    5     4     4     4     4     5     5     5     5     5     5
## 301    4    3     4     4     4     4     4     2     5     4     3     4
## 302    2    4     1     4     5     3     3     4     3     2     5     3
## 303    5    4     4     4     3     4     4     4     4     4     4     4
## 304    3    3     2     3     2     4     3     3     3     3     3     3
## 305    1    5     2     3     4     2     1     5     5     3     5     5
## 306    2    3     1     2     3     2     2     2     4     4     4     3
## 307    4    4     2     3     3     4     2     3     3     3     4     3
## 308    2    5     3     2     5     1     3     4     5     4     5     5
## 309    3    3     1     4     3     3     2     3     1     1     2     3
## 310    3    4     4     2     4     5     5     4     5     4     3     3
## 311    1    1     5     1     2     1     1     3     5     1     2     1
## 312    3    5     4     4     5     3     3     3     4     2     4     3
## 313    2    2     4     4     3     2     4     4     3     2     3     2
## 314    4    4     2     4     5     4     3     4     5     4     5     4
## 315    1    4     1     5     1     4     2     4     3     2     2     1
## 316    3    4     5     5     4     2     3     4     5     5     5     5
## 317    4    4     3     3     4     2     2     3     4     3     5     3
## 318    4    4     4     4     4     4     4     4     5     5     5     4
## 319    4    4     5     4     5     4     4     5     5     5     4     5
## 320    2    4     2     3     4     3     3     3     3     3     3     3
## 321    3    3     3     2     3     1     3     3     4     4     3     3
## 322    3    2     1     3     3     3     3     3     4     4     4     3
## 323    5    5     5     5     5     5     5     5     1     5     5     4
## 324    4    4     2     3     4     4     4     3     5     4     4     4
## 325    4    4     1     3     4     5     2     3     4     4     3     2
## 326    2    2     2     4     2     2     2     3     3     2     2     1
## 327    4    5     4     1     5     4     5     5     5     5     5     5
## 328    3    3     1     5     3     2     2     3     5     1     3     4
## 329    4    3     2     2     2     4     2     4     4     3     3     2
## 330    2    4     3     3     4     2     2     3     2     3     5     4
## 331    3    4     1     2     2     1     1     3     4     4     4     3
## 332    2    4     2     2     4     2     3     3     2     3     4     4
## 333    2    2     1     4     2     1     1     1     2     1     3     2
## 334    4    4     3     4     4     5     3     4     5     4     4     4
## 335    2    3     2     4     4     4     4     3     3     3     3     3
## 336    4    4     3     3     3     2     4     4     3     4     4     4
## 337    3    4     2     1     4     1     3     4     3     2     5     4
## 338    3    3     2     2     2     2     4     2     4     2     2     3
## 339    3    5     1     3     4     1     2     2     5     4     2     5
## 340    5    4     1     4     4     4     3     4     5     3     5     5
## 341    2    5     5     5     4     4     2     2     4     1     5     4
## 342    3    4     3     2     4     3     2     2     1     1     2     3
## 343    2    5     1     1     4     3     3     4     3     2     5     4
## 344    4    4     2     2     4     5     4     5     5     5     4     5
## 345    2    3     2     4     3     2     2     2     3     2     3     2
## 346    3    4     5     5     5     2     2     3     4     2     2     2
## 347    4    4     5     5     5     4     4     5     5     5     4     5
## 348    5    4     4     5     4     1     1     4     4     4     3     5
## 349    3    2     2     4     3     1     1     1     3     2     3     3
## 350    3    3     4     5     4     4     4     4     5     4     4     4
## 351    4    3     3     5     5     1     4     4     3     2     4     3
## 352    5    5     1     3     3     1     1     4     3     2     2     3
## 353    4    4     5     5     5     4     4     5     5     2     4     4
## 354    3    2     1     2     2     3     4     2     4     2     2     3
## 355    3    3     1     1     3     3     2     3     2     1     2     1
## 356    4    3     4     4     3     3     3     3     4     3     4     3
## 357    2    3     1     1     2     1     1     1     4     3     2     2
## 358    4    3     2     2     3     4     4     4     4     5     4     3
## 359    3    5     4     3     4     4     5     4     4     4     4     4
## 360    3    4     4     4     4     4     4     4     4     4     4     4
## 361    1    3     1     1     2     1     1     1     3     3     1     1
## 362    4    4     2     5     4     4     4     5     4     2     4     4
## 363    3    3     2     3     3     5     2     3     3     2     3     3
## 364    4    3     3     4     3     4     4     2     3     3     4     3
## 365    2    3     1     4     3     2     2     3     4     4     3     3
## 366    5    5     5     4     4     3     3     4     1     3     3     4
## 367    4    4     5     1     5     5     5     5     5     4     5     4
## 368    5    4     4     4     4     1     4     4     5     4     5     5
## 369    4    3     4     4     3     4     4     3     4     3     4     3
## 370    4    3     2     3     3     1     2     3     4     3     4     2
## 371    2    3     1     4     3     4     3     4     4     4     5     3
## 372    1    1     2     5     4     4     4     2     5     4     1     5
## 373    3    5     1     1     4     1     1     2     4     1     5     5
## 374    2    4     1     2     4     3     3     3     4     3     4     4
## 375    1    4     1     3     3     3     2     2     4     1     3     3
## 376    2    3     2     2     3     1     2     3     3     3     2     2
## 377    5    5     5     5     5     5     5     5     5     5     5     5
## 378    5    4     4     4     4     1     1     5     2     3     4     4
## 379    2    4     2     4     3     2     3     2     5     2     2     4
## 380    4    3     3     3     3     3     4     4     3     2     5     3
## 381    4    4     4     2     4     3     4     4     4     4     4     2
## 382    3    2     2     3     3     3     4     4     4     4     4     3
## 383    3    3     3     4     4     2     3     4     4     3     4     3
## 384    5    5     5     2     4     5     4     5     5     4     5     2
## 385    3    4     4     4     4     4     4     3     4     4     4     4
## 386    3    3     3     2     3     3     4     3     4     4     3     3
## 387    3    3     2     4     3     3     3     4     3     3     4     2
## 388    4    3     3     4     3     3     3     4     4     4     4     4
## 389    2    2     1     5     1     1     1     3     5     2     2     1
## 390    2    4     4     4     4     5     5     5     4     4     5     4
## 391    3    3     1     1     3     1     1     2     3     2     2     2
## 392    2    4     1     2     4     3     3     2     4     2     3     4
## 393    4    4     1     3     4     3     3     2     5     3     4     4
## 394    3    4     3     4     3     3     4     4     5     4     3     3
## 395    4    5     5     4     5     4     4     4     5     5     5     5
## 396    4    3     3     2     4     3     4     3     4     4     3     3
## 397    4    4     4     5     3     2     2     4     5     5     3     2
## 398    3    3     1     1     3     3     3     3     4     3     3     3
## 399    3    2     3     3     3     3     4     4     5     5     4     5
## 400    2    2     3     3     2     2     3     2     4     3     2     2
## 401    2    2     2     4     2     2     2     2     2     2     2     2
## 402    3    3     2     3     3     2     3     3     3     3     4     3
## 403    3    3     3     4     3     2     2     3     4     4     4     4
## 404    5    5     4     5     5     4     4     5     5     5     5     5
## 405    4    1     2     3     2     1     2     3     4     4     3     4
## 406    2    4     3     2     4     4     2     2     2     2     3     3
## 407    5    5     1     4     5     2     4     4     5     5     4     5
## 408    2    1     2     4     3     3     1     3     3     3     2     3
## 409    2    2     2     2     2     3     5     1     3     2     1     2
## 410    4    4     2     4     3     3     4     3     4     2     4     3
## 411    4    2     2     5     3     2     2     4     5     3     4     2
## 412    5    3     1     2     4     2     5     3     4     2     4     3
## 413    2    2     3     4     2     1     2     3     2     2     3     3
## 414    3    4     3     4     5     1     4     3     4     3     5     4
## 415    4    4     2     4     4     4     4     4     4     4     4     4
## 416    4    5     5     5     5     4     3     5     4     4     5     4
## 417    4    4     1     3     3     2     4     3     4     3     3     4
## 418    3    4     1     2     4     2     3     4     4     1     3     2
## 419    5    5     5     4     4     2     3     4     5     4     5     5
## 420    4    5     3     4     5     4     4     5     4     4     3     4
## 421    1    5     5     5     5     2     4     5     5     5     5     5
## 422    4    3     3     4     4     2     3     3     5     5     4     4
## 423    4    3     4     5     3     3     5     4     4     3     4     5
## 424    4    3     1     4     3     2     2     3     4     3     4     4
## 426    4    3     1     4     2     3     3     5     4     4     5     5
## 427    3    4     2     2     4     4     2     4     2     3     5     5
## 428    4    5     5     5     5     4     2     3     5     3     4     3
## 429    4    5     5     4     5     3     3     4     5     4     5     5
## 430    2    4     4     3     4     1     2     3     3     3     3     5
## 431    2    4     3     3     4     3     4     5     4     4     5     5
## 432    3    5     5     2     5     5     5     5     5     5     5     5
## 433    1    1     1     1     5     1     5     1     1     5     1     1
## 434    4    3     3     5     4     5     4     4     4     3     4     4
## 435    3    4     4     5     4     3     3     4     4     4     4     4
## 436    3    3     3     3     3     5     2     3     3     3     4     4
## 437    3    3     4     3     3     3     4     3     5     4     3     3
## 438    3    4     2     2     4     3     4     4     4     3     4     4
## 439    4    3     3     3     4     3     3     4     4     4     4     3
## 440    5    5     5     5     5     3     4     4     5     5     5     5
## 441    3    2     2     2     2     2     2     3     3     2     4     2
## 442    5    4     5     5     4     4     5     4     5     4     5     4
## 443    2    4     1     3     3     4     3     2     4     3     3     3
## 444    2    3     1     2     4     1     3     2     5     2     4     2
## 445    2    3     4     4     3     1     3     3     2     4     4     3
## 446    4    5     3     4     3     5     5     5     5     5     5     5
## 447    2    3     1     2     3     2     2     2     3     2     2     3
## 448    4    4     2     4     4     2     4     4     3     4     4     4
## 449    3    3     3     3     3     5     2     2     2     2     2     3
## 450    3    5     3     4     5     4     4     4     5     5     4     4
## 451    4    4     4     4     5     3     3     3     5     5     3     4
## 452    2    1     1     5     1     1     1     2     1     2     2     1
## 453    3    5     5     4     5     4     5     5     4     4     4     5
## 454    3    5     2     3     4     2     2     3     5     4     2     4
## 455    3    3     2     4     2     2     2     2     3     3     4     2
## 456    4    4     2     4     3     2     3     4     4     4     3     4
## 457    2    2     2     2     2     2     2     2     3     2     2     2
## 458    5    5     2     3     5     4     5     5     5     5     5     4
## 459    5    1     1     2     1     2     2     1     2     1     1     1
## 460    3    3     1     4     4     1     2     4     5     2     3     4
## 461    4    4     3     4     3     4     4     4     5     5     2     2
## 462    3    5     4     3     5     4     2     4     5     5     5     5
## 463    5    5     5     5     4     5     5     5     4     4     4     5
## 464    4    3     3     3     3     4     4     4     4     4     3     4
## 465    3    3     3     5     3     2     1     3     3     2     3     3
## 466    2    2     1     3     2     1     3     3     2     2     3     4
## 467    4    3     2     2     4     2     4     3     3     3     4     4
## 468    2    3     2     2     2     2     3     2     3     2     2     2
## 469    3    4     3     3     4     2     3     4     4     4     5     5
## 470    3    3     2     3     3     1     2     3     4     2     3     3
## 471    2    3     1     2     4     3     3     3     4     3     4     3
## 472    3    5     5     5     3     2     5     3     5     5     4     4
## 473    4    4     3     2     4     4     4     3     4     3     5     4
## 474    4    5     3     4     5     3     4     4     2     4     5     2
## 475    3    4     4     4     4     2     2     3     3     2     4     4
## 476    4    3     4     1     3     1     2     4     5     2     5     5
## 477    4    5     1     2     5     5     5     5     5     5     5     5
## 478    3    3     2     3     3     2     2     3     4     4     4     2
## 479    5    5     5     4     5     2     2     5     4     4     5     4
## 480    4    4     5     4     4     4     5     4     4     5     3     4
## 481    4    4     1     5     5     2     2     4     4     3     5     5
## 482    3    3     2     1     2     1     2     3     3     3     2     3
## 483    4    4     1     4     4     1     5     4     5     5     4     4
## 484    3    3     3     3     4     3     2     3     3     3     4     4
## 485    3    3     2     2     3     3     4     3     4     3     3     3
## 486    3    3     3     4     4     2     3     3     3     4     3     3
## 487    3    5     2     2     5     3     4     4     5     3     5     5
## 488    2    4     4     4     4     4     4     3     2     2     3     3
## 489    4    3     3     4     3     2     4     4     4     3     4     5
## 490    1    5     5     5     5     3     4     5     5     5     5     5
## 491    3    4     3     4     5     3     4     4     2     3     4     4
## 492    3    5     5     3     3     1     5     5     5     5     5     3
## 493    2    3     1     1     3     2     3     3     2     1     4     3
## 494    4    4     1     4     4     3     3     3     5     3     3     5
## 495    4    2     4     3     3     5     5     5     1     2     4     4
## 496    4    5     5     5     4     4     4     4     4     4     4     3
## 497    5    5     2     2     5     5     5     4     5     5     4     4
## 498    3    3     4     4     4     4     2     4     4     4     4     4
## 499    3    4     4     4     4     3     3     3     5     4     4     4
## 500    4    4     3     4     4     3     3     4     4     3     4     3
## 501    4    3     2     3     2     2     3     3     2     2     3     2
## 502    2    5     5     5     5     4     4     3     5     3     5     4
## 503    4    5     3     3     5     2     2     4     3     2     5     4
## 504    4    4     4     4     4     2     4     5     5     5     4     5
## 505    3    3     3     3     3     2     3     3     2     2     2     2
## 506    5    1     1     1     1     1     1     3     5     2     2     1
## 507    1    1     2     4     2     2     2     3     3     1     2     1
## 508    2    4     2     2     3     1     1     2     2     1     2     4
## 509    2    2     1     2     1     1     2     3     5     1     2     4
## 510    4    5     4     3     4     3     4     4     4     4     4     5
## 511    2    3     1     1     1     2     3     1     4     4     1     2
## 512    2    4     5     2     3     1     5     4     5     2     5     5
## 513    4    5     4     4     5     3     4     4     5     5     4     5
## 514    1    3     4     1     2     2     4     3     5     4     4     3
## 515    4    5     5     5     5     5     5     2     5     5     5     5
## 516    4    4     3     2     5     3     4     4     4     3     3     4
## 517    3    2     1     4     4     2     2     2     4     2     2     2
## 518    3    5     4     4     4     5     4     3     5     4     5     3
## 519    1    2     1     5     1     1     3     2     3     1     2     3
## 520    4    4     2     3     4     5     3     3     4     4     3     4
## 521    3    3     3     3     4     4     4     4     4     3     3     3
## 522    4    4     3     3     4     4     2     4     4     4     5     4
## 523    3    5     4     4     4     2     4     4     4     5     4     4
## 524    3    3     3     4     3     2     3     3     4     4     3     4
## 525    2    3     3     5     4     3     2     3     3     3     4     4
## 526    3    5     1     1     1     1     1     1     5     5     1     1
## 527    2    1     1     4     2     2     2     2     1     2     5     1
## 528    4    3     5     4     5     1     2     4     4     3     4     3
## 529    3    3     2     3     3     3     4     3     3     3     4     3
## 530    3    3     1     5     3     2     2     4     2     2     3     4
## 531    2    2     1     2     2     1     2     2     3     2     2     3
## 532    3    3     5     5     5     2     3     4     1     1     5     4
## 533    3    5     5     1     5     2     1     5     4     5     3     5
## 534    4    4     4     4     4     3     4     4     4     4     3     3
## 535    3    4     2     5     5     2     3     4     2     2     5     5
## 536    3    2     3     2     3     3     3     2     2     1     3     3
## 537    5    5     5     1     5     3     3     5     5     5     5     5
## 538    4    4     1     1     4     3     5     5     3     3     5     5
## 539    3    4     1     4     4     5     2     4     5     5     4     3
## 540    2    4     1     4     4     1     1     3     1     1     4     4
## 541    4    4     2     4     4     3     3     5     4     2     4     3
## 542    4    4     1     2     3     4     3     3     4     4     2     2
## 543    2    3     1     4     3     1     2     2     4     3     2     3
## 544    1    4     1     3     4     3     1     1     4     3     3     3
## 545    2    3     1     2     2     1     3     2     5     2     2     2
## 546    2    3     1     1     2     3     2     2     4     3     4     3
## 547    3    4     3     3     4     3     3     3     5     3     4     3
## 548    5    3     5     5     3     5     5     5     5     5     5     3
## 549    4    3     3     4     3     1     5     4     5     3     2     2
## 550    2    3     1     2     3     3     2     3     3     2     2     2
## 551    3    2     1     4     3     1     3     3     4     2     1     3
## 552    3    2     1     5     1     3     2     4     1     1     4     3
## 553    3    4     3     4     3     2     3     4     4     4     3     4
## 554    1    5     4     4     5     5     5     5     5     5     5     5
## 555    3    4     5     4     5     4     2     4     2     2     5     5
## 556    3    3     3     3     3     3     3     3     3     3     3     3
## 557    3    4     2     4     4     1     3     5     5     3     5     5
## 558    4    5     5     4     5     5     4     5     5     5     5     5
## 559    2    3     1     5     1     1     1     1     1     1     1     1
## 560    4    2     3     2     3     2     3     2     3     2     2     3
## 561    2    2     2     4     2     3     1     2     3     2     3     2
## 562    4    3     2     4     4     3     1     4     3     3     4     4
## 563    2    4     3     2     5     3     3     4     4     2     3     2
## 564    4    4     2     3     3     1     2     4     3     2     3     3
## 565    2    3     3     4     3     1     4     4     4     2     3     1
## 566    2    2     2     2     2     2     2     2     3     1     2     2
## 567    4    4     4     4     4     4     5     4     5     3     4     5
## 568    3    3     2     4     2     3     3     2     4     2     3     3
## 569    3    3     1     3     1     5     5     1     3     3     2     2
## 570    4    2     2     4     2     4     4     4     2     2     4     2
##     XGP20 XSWLS1 XSWLS2 XSWLS3 XSWLS4 XSWLS5 Yourself Others DP_Mean
## 1       4      4      4      3      4      3      yes    yes     3.4
## 2       5      3      4      3      5      3      yes    yes     3.0
## 3       3      2      2      2      4      2      yes    yes     2.0
## 4       4      2      2      2      2      2      yes    yes     5.0
## 5       4      4      4      4      4      3      yes    yes     3.2
## 6       5      4      4      4      4      5      yes    yes     3.0
## 7       4      3      3      2      4      5      yes     no     4.2
## 8       4      3      3      3      3      2      yes    yes     4.0
## 9       5      4      4      4      4      5      yes    yes     3.6
## 10      2      1      3      2      2      2      yes     no     2.4
## 11      2      2      2      3      4      4       no     no     2.2
## 12      2      3      2      2      3      3      yes     no     1.2
## 13      3      2      2      2      2      2      yes    yes     3.8
## 14      4      4      3      4      3      2      yes    yes     3.4
## 15      5      1      2      1      2      1      yes    yes     3.2
## 16      4      3      4      2      3      3      yes     no     4.4
## 17      3      4      3      3      5      4      yes    yes     3.4
## 18      3      3      3      3      4      3      yes     no     2.2
## 19      4      3      3      3      3      2      yes    yes     3.2
## 21      3      3      4      3      4      3      yes    yes     3.0
## 22      4      3      4      4      4      3      yes    yes     3.2
## 23      4      2      3      2      4      4      yes    yes     3.0
## 24      3      2      3      2      3      4      yes            4.0
## 25      1      3      3      3      4      4      yes     no     3.4
## 26      3      3      3      3      3      3      yes    yes     1.8
## 27      3      2      3      2      3      2      yes    yes     3.2
## 28      3      2      3      2      3      2      yes    yes     3.2
## 29      5      1      1      1      1      1      yes    yes     4.6
## 30      3      2      4      2      4      3      yes     no     2.8
## 31      4      2      2      2      2      2      yes    yes     3.0
## 32      3      1      1      2      3      1      yes    yes     3.4
## 33      4      3      3      3      3      3      yes    yes     3.2
## 34      3      4      4      4      4      3       no     no     1.8
## 35      1      3      3      3      3      1      yes    yes     3.4
## 36      4      1      3      2      1      1      yes    yes     4.0
## 37      3      4      4      4      4      4      yes    yes     2.4
## 38      4      2      2      4      3      3      yes    yes     2.4
## 39      4      2      2      2      4      2      yes    yes     4.0
## 40      3      5      5      4      5      3      yes     no     4.2
## 41      4      3      4      3      2      1      yes    yes     3.4
## 42      4      2      2      2      3      1      yes    yes     4.0
## 43      3      4      4      4      5      1      yes    yes     1.8
## 44      5      2      2      3      3      2      yes    yes     3.4
## 45      3      3      3      3      3      1      yes     no     3.0
## 46      4      2      3      2      3      1      yes     no     2.6
## 47      5      4      5      4      5      5      yes    yes     2.6
## 48      5      2      2      2      2      2      yes    yes     2.4
## 49      4      3      3      2      2      1      yes    yes     2.6
## 50      3      3      4      2      4      3      yes    yes     3.8
## 51      3      3      5      4      4      1      yes    yes     1.8
## 52      4      4      4      4      4      4      yes     no     3.4
## 53      4      2      1      1      3      1      yes     no     3.2
## 54      4      3      2      2      4      2      yes    yes     2.6
## 55      2      5      5      5      5      5       no     no     2.0
## 56      5      2      3      2      3      2      yes    yes     3.8
## 57      4      3      3      3      4      2      yes    yes     4.2
## 58      5      3      3      3      4      1      yes    yes     5.0
## 59      4      1      1      1      1      1      yes    yes     4.8
## 60      4      1      2      2      2      3      yes     no     3.8
## 61      3      2      3      4      3      5      yes    yes     3.4
## 62      5      1      1      1      2      2      yes    yes     3.8
## 63      3      4      4      4      3      3      yes     no     3.0
## 64      3      3      2      3      2      1      yes     no     4.0
## 65      4      2      5      3      3      4      yes    yes     3.0
## 66      5      3      3      3      3      2      yes    yes     3.6
## 67      4      3      2      4      3      1      yes    yes     4.4
## 68      4      1      2      2      1      1      yes     no     3.4
## 69      3      1      1      1      1      4      yes     no     3.6
## 70      1      4      1      2      2      1       no     no     3.0
## 71      3      3      3      4      4      2      yes    yes     2.8
## 72      4      4      4      2      4      2      yes    yes     3.8
## 73      5      4      4      4      5      2      yes    yes     2.2
## 74      4      3      3      1      4      2      yes    yes     4.0
## 75      4      4      4      4      4      2      yes    yes     3.0
## 76      5      1      2      1      1      1      yes    yes     5.0
## 77      5      2      4      4      4      1      yes    yes     4.4
## 78      4      4      4      4      4      4       no     no     2.4
## 79      4      3      4      3      4      3      yes    yes     3.6
## 80      3      3      4      3      3      3      yes    yes     3.4
## 81      3      5      5      5      5      5       no     no     1.4
## 82      1      1      1      1      1      1       no     no     5.0
## 83      2      1      4      4      3      3      yes     no     2.4
## 84      4      4      2      1      2      3      yes    yes     2.2
## 85      4      4      4      4      4      4      yes     no     2.4
## 86      3      4      4      4      4      3      yes     no     2.8
## 87      3      3      3      3      3      2      yes            4.0
## 88      4      3      3      4      4      4      yes    yes     4.0
## 89      1      5      5      5      5      4       no    yes     1.0
## 90      4      2      3      3      2      4      yes    yes     3.4
## 91      4      4      4      4      4      3      yes    yes     4.4
## 92      3      4      4      5      5      4      yes     no     3.6
## 93      4      2      2      2      3      2      yes    yes     2.8
## 94      5      3      4      4      3      3       no     no     2.4
## 95      4      4      4      4      4      3       no     no     2.4
## 96      3      4      4      2      3      3      yes     no     3.6
## 97      2      4      4      4      4      4      yes     no     1.2
## 98      3      3      3      4      4      3      yes    yes     3.2
## 99      5      4      4      4      5      2      yes    yes     2.8
## 100     3      2      2      2      2      2      yes    yes     4.0
## 101     3      2      2      2      3      2      yes    yes     3.8
## 102     3      4      5      5      5      5       no     no     1.6
## 103     4      4      4      4      4      4      yes    yes     3.4
## 104     3      3      3      4      4      3      yes    yes     2.6
## 105     1      5      5      5      5      5      yes    yes     5.0
## 106     5      2      3      3      4      2      yes    yes     3.8
## 107     4      3      4      3      3      4      yes    yes     3.2
## 108     5      1      1      1      2      1      yes    yes     4.4
## 109     1      3      3      3      3      3       no     no     2.0
## 110     5      3      3      3      3      3      yes     no     4.0
## 111     4      3      2      3      3      3      yes    yes     4.0
## 112     3      3      4      3      5      2      yes     no     2.2
## 113     5      3      4      3      5      3      yes     no     2.0
## 114     1      3      3      3      3      2       no     no     1.0
## 115     5      3      3      4      4      5      yes     no     3.2
## 116     2      4      4      4      4      3       no     no     1.8
## 117     5      2      2      2      3      1      yes    yes     4.2
## 118     4      3      3      3      3      3      yes    yes     5.0
## 119     3      4      4      3      4      1      yes    yes     3.2
## 120     4      2      2      2      3      1       no    yes     3.4
## 121     2      3      3      3      3      3       no     no     2.0
## 122     5      2      3      2      2      2      yes     no     2.4
## 123     3      4      4      4      5      4      yes     no     2.6
## 124     3      2      2      1      1      1      yes    yes     3.4
## 125     5      3      3      2      3      3      yes    yes     4.2
## 126     4      2      2      2      2      2      yes    yes     4.2
## 127     4      3      2      1      3      2      yes     no     4.0
## 128     3      1      1      1      2      1      yes    yes     5.0
## 129     4      4      4      5      4      2      yes    yes     3.4
## 130     3      3      4      4      4      2      yes     no     1.4
## 131     4      2      2      2      4      4      yes    yes     4.0
## 132     3      3      4      3      3      3      yes     no     3.2
## 133     2      2      2      2      4      2      yes    yes     3.6
## 134     4      2      2      2      4      4      yes    yes     3.4
## 135     2      4      4      3      4      2       no     no     2.2
## 136     4      4      4      4      4      2      yes    yes     3.2
## 137     4      2      1      1      2      1      yes    yes     4.2
## 138     3      4      4      4      4      4      yes    yes     2.8
## 139     3      2      2      2      2      2      yes     no     3.2
## 140     2      4      4      4      4      2      yes     no     3.8
## 141     4      3      3      3      2      2      yes     no     3.4
## 142     4      1      1      1      1      1      yes     no     4.0
## 143     3      3      3      3      3      2      yes    yes     4.2
## 144     5      2      4      2      3      2      yes    yes     4.4
## 145     1      2      2      3      3      2       no     no     1.0
## 146     4      2      3      3      3      2      yes    yes     3.4
## 147     4      1      2      1      3      3      yes     no     4.0
## 148     3      2      3      2      2      2       no    yes     2.2
## 149     5      4      5      4      5      4      yes     no     1.6
## 150     3      3      4      4      4      3      yes     no     2.6
## 151     4      2      3      3      2      1      yes    yes     3.2
## 152     4      3      4      5      3      2                     2.8
## 153     5      1      2      2      2      2                     3.6
## 154     4      3      4      3      2      2      yes    yes     3.4
## 155     3      2      3      2      3      2      yes    yes     3.2
## 156     4      2      2      2      3      1      yes     no     3.6
## 157     5      2      3      2      5      2      yes    yes     3.2
## 158     5      5      5      5      5      5      yes     no     4.0
## 159     3      5      5      5      5      3      yes     no     3.0
## 160     2      5      5      5      5      5       no     no     1.2
## 161     2      2      2      2      2      2      yes    yes     2.4
## 162     4      3      3      3      3      3      yes    yes     3.6
## 163     5      3      3      3      4      3      yes    yes     4.2
## 164     4      3      3      3      4      3      yes     no     4.6
## 165     3      3      3      3      4      1      yes    yes     2.8
## 166     3      3      3      3      3      2      yes    yes     3.2
## 167     3      4      4      3      4      2      yes    yes     3.0
## 168     4      1      1      3      3      1      yes    yes     3.0
## 169     2      4      4      4      4      4      yes     no     2.2
## 170     1      3      4      4      4      3      yes     no     3.0
## 171     1      4      3      4      4      1      yes    yes     3.6
## 172     4      3      3      3      3      2      yes    yes     4.0
## 173     4      2      4      2      4      2      yes    yes     3.4
## 174     2      4      4      4      4      3      yes    yes     3.8
## 175     5      4      4      4      4      4      yes     no     4.2
## 176     1      5      4      4      5      4      yes    yes     2.8
## 177     4      4      3      4      5      3      yes    yes     3.0
## 178     4      2      3      3      2      2      yes    yes     4.4
## 179     3      3      3      3      3      2      yes    yes     2.8
## 180     4      4      5      4      5      4      yes    yes     3.2
## 181     5      1      1      2      2      1      yes    yes     4.8
## 182     3      4      5      5      5      4      yes     no     1.2
## 183     4      2      2      3      1      1      yes    yes     3.2
## 184     5      4      3      4      5      5      yes     no     4.0
## 185     3      2      2      3      4      4      yes    yes     3.6
## 186     2      3      3      4      4      4       no     no     2.2
## 187     4      3      4      3      5      4      yes    yes     3.8
## 188     3      1      3      3      3      4      yes    yes     4.6
## 189     2      4      4      4      5      4      yes     no     2.6
## 190     4      3      3      3      4      3      yes     no     2.0
## 191     3      4      4      4      4      2      yes    yes     3.8
## 192     4      3      4      3      4      2      yes    yes     2.0
## 193     4      2      3      3      2      1      yes    yes     3.8
## 194     2      4      4      3      3      3      yes    yes     1.4
## 195     5      3      2      3      2      2      yes    yes     4.4
## 196     3      4      4      4      4      3      yes    yes     2.8
## 197     2      4      4      4      4      4       no     no     2.0
## 198     4      3      3      3      3      2      yes    yes     3.6
## 199     2      3      4      4      4      3       no     no     2.4
## 200     4      3      2      2      3      1      yes    yes     4.0
## 201     5      2      5      2      3      3      yes    yes     4.6
## 202     3      3      3      4      4      2      yes    yes     3.8
## 203     5      3      2      1      2      1      yes    yes     4.6
## 204     4      4      3      4      4      3      yes     no     2.2
## 205     5      3      3      3      4      4      yes    yes     5.0
## 206     4      1      1      2      1      1      yes    yes     4.0
## 207     2      4      3      4      4      4       no     no     2.0
## 208     3      3      4      4      4      3      yes    yes     1.8
## 209     2      1      2      2      2      2       no     no     2.4
## 210     1      4      4      4      5      1      yes     no     3.6
## 211     5      3      3      3      3      2      yes    yes     2.8
## 212     4      3      2      2      3      2      yes    yes     5.0
## 213     5      4      4      4      4      2      yes     no     2.6
## 214     5      2      3      3      4      2      yes    yes     3.0
## 215     1      5      5      5      5      3      yes     no     1.8
## 216     1      1      1      1      1      1      yes     no     1.2
## 217     4      2      2      2      1      1      yes    yes     4.0
## 218     4      2      1      1      3      1      yes    yes     4.4
## 219     4      2      1      2      1      1      yes    yes     3.8
## 220     2      3      3      3      5      5      yes    yes     2.6
## 221     4      5      4      5      5      4      yes    yes     3.0
## 222     3      4      4      4      5      4      yes    yes     2.4
## 223     2      3      4      4      4      4      yes     no     3.2
## 224     4      1      2      3      3      1      yes    yes     3.0
## 225     3      4      4      3      4      4      yes     no     1.4
## 226     4      4      4      3      4      2      yes    yes     3.6
## 227     1      1      1      1      3      4      yes            5.0
## 228     1      4      4      5      5      4       no     no     1.2
## 229     4      2      3      2      3      1      yes     no     3.0
## 230     4      3      3      4      3      2      yes    yes     3.0
## 231     3      2      4      3      4      1      yes    yes     2.4
## 232     2      3      3      3      3      3      yes     no     2.4
## 233     4      2      3      3      4      4      yes     no     2.2
## 234     3      4      4      3      4      3      yes     no     3.0
## 235     2      2      2      3      2      2       no     no     2.2
## 236     4      1      4      3      3      2      yes     no     3.6
## 237     4      3      2      3      2      1      yes     no     3.0
## 238     3      3      3      2      3      4      yes     no     1.4
## 239     2      3      3      3      5      4      yes     no     3.4
## 240     4      4      5      4      5      3      yes    yes     2.2
## 241     5      4      4      4      5      4      yes    yes     2.0
## 242     5      2      3      2      3      1      yes    yes     4.4
## 243     5      2      1      1      1      1      yes    yes     5.0
## 244     2      3      3      4      4      4      yes     no     1.2
## 245     2      4      4      4      4      2       no     no     1.6
## 246     4      1      3      2      3      1      yes    yes     2.0
## 247     1      4      5      4      4      5      yes     no     4.4
## 248     5      4      4      4      3      2      yes    yes     2.0
## 249     4      4      5      4      5      2       no     no     1.4
## 250     4      2      2      2      2      4      yes    yes     3.0
## 251     5      3      3      4      4      2      yes     no     3.4
## 252     3      3      3      3      2      2      yes    yes     3.2
## 253     5      3      5      2      2      2      yes    yes     2.2
## 254     3      4      4      4      5      3      yes     no     2.4
## 255     3      3      4      4      3      2      yes     no     2.8
## 256     3      2      2      2      4      2       no     no     2.2
## 257     5      2      2      4      4      1      yes    yes     4.0
## 258     3      3      3      3      3      3      yes     no     2.6
## 259     3      2      4      2      3      1      yes    yes     3.6
## 260     5      3      4      4      4      3      yes    yes     2.8
## 261     5      1      1      3      3      3      yes    yes     3.0
## 262     4      2      5      4      4      2      yes     no     2.2
## 263     3      4      4      4      4      4       no     no     2.0
## 264     5      5      5      5      5      3      yes     no     1.0
## 265     3      4      4      4      4      3       no     no     2.2
## 266     3      3      4      3      5      2      yes    yes     3.4
## 267     3      3      3      4      5      5       no     no     2.0
## 268     4      3      3      3      3      2      yes    yes     3.8
## 269     3      4      4      4      4      2       no     no     1.4
## 270     4      4      4      3      4      2      yes    yes     1.6
## 271     2      3      3      3      4      2      yes     no     3.4
## 272     3      2      1      3      2      2      yes    yes     3.4
## 273     5      1      1      1      1      1      yes    yes     3.2
## 274     4      2      2      2      2      2       no     no     2.2
## 275     3      5      4      5      5      4       no     no     1.4
## 276     2      3      4      4      5      2       no     no     1.2
## 277     4      4      4      4      4      2      yes     no     3.4
## 278     4      3      4      2      3      3      yes    yes     3.8
## 279     1      2      2      2      3      1      yes    yes     3.0
## 280     4      2      2      2      2      1      yes    yes     2.6
## 281     5      3      3      4      4      3      yes    yes     4.2
## 282     5      3      3      4      3      3       no    yes     4.6
## 283     3      5      5      4      4      5      yes    yes     2.8
## 284     4      3      3      3      2      2      yes    yes     3.4
## 285     3      3      2      1      3      2      yes    yes     4.4
## 286     1      5      5      5      5      5      yes     no     1.6
## 287     2      4      3      4      5      5      yes     no     2.8
## 288     2      3      4      4      4      3      yes     no     2.0
## 289     2      3      4      4      3      2      yes    yes     2.2
## 290     4      2      2      2      3      2      yes    yes     3.4
## 291     4      1      1      2      1      1      yes    yes     3.8
## 292     2      3      4      4      4      3      yes     no     1.8
## 293     2      3      3      3      3      3       no     no     2.2
## 294     3      3      5      4      3      2      yes     no     3.4
## 295     4      3      3      3      3      3      yes     no     5.0
## 296     4      2      3      1      1      1      yes    yes     3.6
## 297     3      3      2      2      3      2      yes    yes     3.2
## 298     3      3      4      3      5      2      yes     no     1.2
## 299     2      4      4      4      4      4       no     no     1.0
## 300     5      2      2      2      2      2      yes    yes     4.2
## 301     4      3      4      3      4      2      yes    yes     2.4
## 302     3      4      4      4      4      2      yes    yes     3.2
## 303     4      3      3      3      4      2      yes    yes     5.0
## 304     3      2      2      2      2      2       no     no     2.0
## 305     4      2      2      2      2      1      yes    yes     2.4
## 306     5      5      4      5      5      5      yes     no     2.4
## 307     3      4      4      3      5      3       no     no     2.6
## 308     5      2      2      2      4      2      yes    yes     2.4
## 309     4      2      3      3      3      2       no     no     2.4
## 310     3      3      3      3      3      3      yes    yes     3.2
## 311     2      4      4      4      4      3       no     no     1.0
## 312     3      2      2      2      3      3      yes    yes     3.2
## 313     2      3      4      4      4      4       no     no     2.2
## 314     5      4      3      5      4      5      yes     no     3.6
## 315     2      3      4      5      5      3      yes     no     1.0
## 316     4      1      1      1      1      1      yes    yes     3.0
## 317     3      5      5      4      4      1      yes     no     3.0
## 318     5      1      2      3      2      1      yes    yes     4.2
## 319     4      3      3      2      3      3      yes    yes     3.4
## 320     3      5      5      5      5      5      yes     no     2.8
## 321     3      4      4      4      4      3      yes     no     2.6
## 322     3      2      2      1      1      3      yes    yes     2.2
## 323     4      3      3      3      3      1      yes    yes     3.8
## 324     3      3      3      3      4      2      yes    yes     4.0
## 325     3      5      5      5      5      3      yes     no     3.4
## 326     1      3      3      2      4      2       no    yes     1.6
## 327     5      3      3      2      2      2      yes    yes     4.0
## 328     4      4      4      3      2      2      yes    yes     3.0
## 329     4      2      3      3      4      3      yes     no     3.0
## 330     4      3      4      4      4      3      yes    yes     4.4
## 331     4      4      4      4      4      2      yes     no     2.4
## 332     4      5      4      4      5      5      yes     no     2.4
## 333     2      5      5      5      5      5      yes     no     2.8
## 334     4      2      2      2      1      1      yes    yes     3.6
## 335     2      3      2      3      4      2      yes     no     2.4
## 336     4      1      1      2      1      1      yes    yes     4.4
## 337     4      4      3      5      5      4      yes     no     3.8
## 338     3      3      2      2      3      3      yes    yes     3.6
## 339     4      4      2      2      5      1      yes    yes     4.8
## 340     5      1      1      1      4      2      yes    yes     3.8
## 341     3      5      4      4      5      5      yes    yes     1.4
## 342     2      3      3      3      3      3      yes     no     2.4
## 343     4      3      3      4      5      5      yes    yes     1.6
## 344     4      4      4      4      4      3      yes    yes     2.0
## 345     2      3      3      3      4      3       no     no     2.0
## 346     4      4      4      4      4      4      yes     no     2.2
## 347     5      3      3      4      3      3      yes    yes     3.6
## 348     1      5      5      5      5      5      yes    yes     2.2
## 349     2      5      4      4      5      4       no     no     1.6
## 350     4      4      4      4      4      2      yes    yes     2.6
## 351     1      5      5      5      5      5       no     no     3.8
## 352     3      4      5      5      5      3       no    yes     3.2
## 353     4      3      4      4      3      1      yes    yes     3.2
## 354     3      3      4      3      4      3       no     no     2.6
## 355     2      1      4      5      5      4       no     no     1.6
## 356     3      3      3      3      3      2      yes    yes     3.4
## 357     2      4      4      5      4      4       no     no     2.0
## 358     5      5      5      5      5      5       no    yes     3.0
## 359     3      3      3      3      3      2      yes    yes     2.8
## 360     4      3      3      2      2      2      yes    yes     4.0
## 361     1      5      5      5      5      5       no     no     1.0
## 362     4      2      3      3      4      3      yes    yes     3.4
## 363     3      2      3      3      4      3      yes    yes     2.6
## 364     4      1      2      2      2      2      yes    yes     3.2
## 365     3      5      5      5      5      3       no     no     1.6
## 366     4      3      2      4      3      3      yes    yes     4.2
## 367     4      2      3      3      3      3      yes    yes     4.6
## 368     4      1      3      1      3      3      yes    yes     4.2
## 369     3      3      2      3      4      2      yes    yes     4.6
## 370     3      5      5      5      5      3      yes     no     2.6
## 371     4      3      5      3      4      3      yes    yes     2.2
## 372     2      4      4      4      5      4      yes    yes     1.4
## 373     4      5      5      5      4      5      yes     no     3.2
## 374     3      4      4      4      4      4      yes     no     2.2
## 375     3      3      4      4      4      2       no     no     2.4
## 376     2      4      3      4      4      3      yes     no     2.6
## 377     5      1      1      1      1      1      yes    yes     5.0
## 378     4      3      3      2      4      3      yes    yes     4.0
## 379     4      3      3      3      3      2      yes     no     2.2
## 380     3      3      3      3      4      4      yes     no     1.6
## 381     4      3      3      4      4      3      yes    yes     4.0
## 382     3      3      3      3      3      2      yes    yes     2.6
## 383     2      4      5      5      5      4      yes    yes     2.6
## 384     4      2      2      2      2      1      yes    yes     4.0
## 385     4      3      4      3      3      5      yes    yes     3.2
## 386     4      3      3      3      3      2      yes    yes     3.0
## 387     4      3      3      2      3      3      yes    yes     3.2
## 388     4      3      3      3      3      2      yes     no     3.6
## 389     3      3      5      5      5      4       no     no     1.0
## 390     3      2      3      3      2      2      yes    yes     2.6
## 391     2      4      4      4      4      4       no     no     2.2
## 392     4      3      4      4      4      4      yes     no     3.2
## 393     4      2      2      2      3      3      yes    yes     4.0
## 394     3      4      4      4      4      4      yes    yes     3.0
## 395     4      3      4      4      3      3      yes    yes     4.6
## 396     2      3      3      3      4      3       no    yes     3.6
## 397     3      4      5      2      3      3       no     no     2.2
## 398     2      4      4      4      4      4      yes     no     2.4
## 399     4      1      1      1      1      1      yes    yes     3.0
## 400     2      3      3      4      4      3      yes     no     1.8
## 401     2      4      4      4      4      4       no     no     2.2
## 402     3      3      3      3      3      3      yes     no     2.4
## 403     3      3      3      4      4      4      yes    yes     2.8
## 404     5      2      2      2      2      1      yes    yes     5.0
## 405     3      2      4      3      4      2      yes    yes     2.2
## 406     3      2      3      2      3      3      yes     no     1.6
## 407     4      2      2      2      2      1      yes     no     5.0
## 408     2      3      2      2      3      1      yes     no     1.2
## 409     2      4      2      1      3      3      yes     no     2.0
## 410     4      3      3      3      3      3       no     no     3.4
## 411     2      3      4      5      5      3      yes     no     2.8
## 412     4      2      2      2      3      2      yes     no     3.8
## 413     3      4      4      5      3      4      yes     no     2.6
## 414     5      3      3      3      3      3      yes    yes     3.2
## 415     4      3      3      3      4      2      yes    yes     4.0
## 416     4      4      4      4      4      4      yes    yes     3.6
## 417     3      3      3      3      2      1      yes     no     3.6
## 418     2      4      4      5      5      4      yes     no     2.4
## 419     5      3      4      4      3      2      yes    yes     3.6
## 420     3      4      4      3      4      3      yes    yes     4.2
## 421     5      3      2      2      2      1      yes    yes     5.0
## 422     3      3      3      3      3      1      yes     no     3.0
## 423     3      3      4      5      4      5      yes    yes     3.4
## 424     4      1      4      2      3      1      yes     no     2.2
## 426     5      3      4      4      3      2      yes    yes     4.0
## 427     4      2      1      2      2      1      yes     no     3.6
## 428     2      2      2      3      3      2      yes    yes     1.6
## 429     5      3      4      3      5      1      yes    yes     3.4
## 430     3      3      4      5      5      2      yes    yes     1.8
## 431     4      2      4      2      4      2      yes    yes     3.2
## 432     5      2      3      2      2      1      yes    yes     3.6
## 433     1      5      4      5      5      5      yes    yes     1.0
## 434     3      3      3      3      4      3      yes    yes     4.0
## 435     4      4      4      4      4      4      yes    yes     2.4
## 436     3      3      2      2      2      2       no     no     3.0
## 437     3      3      4      3      4      2      yes    yes     3.8
## 438     3      3      3      2      3      3      yes     no     3.6
## 439     4      3      3      3      4      3      yes    yes     3.2
## 440     5      2      2      2      3      2      yes    yes     4.0
## 441     3      3      3      4      3      2       no     no     2.0
## 442     3      1      2      2      3      2      yes    yes     3.8
## 443     3      4      4      4      4      1      yes     no     1.6
## 444     2      4      4      4      4      3       no     no     2.0
## 445     2      4      4      4      4      3      yes     no     2.2
## 446     1      1      3      3      3      2      yes    yes     3.4
## 447     2      4      4      4      4      3       no     no     2.0
## 448     4      3      3      3      3      2      yes    yes     3.0
## 449     2      4      4      5      5      5       no     no     1.6
## 450     3      4      4      4      3      3      yes    yes     3.0
## 451     3      5      5      5      5      5      yes     no     2.6
## 452     3      4      4      4      3      4       no    yes     1.6
## 453     5      3      4      3      3      3      yes    yes     5.0
## 454     3      3      2      2      3      4      yes    yes     3.0
## 455     3      3      3      3      4      4       no     no     3.0
## 456     3      3      4      4      4      3      yes    yes     3.4
## 457     2      4      4      4      4      4       no     no     2.4
## 458     5      1      1      1      1      1      yes    yes     4.6
## 459     3      5      5      5      5      4       no     no     1.0
## 460     3      3      3      4      5      3      yes    yes     2.0
## 461     3      4      4      4      4      4      yes     no     3.6
## 462     4      3      3      3      4      1      yes    yes     4.6
## 463     5      3      2      3      4      2      yes    yes     4.2
## 464     4      4      3      4      4      4      yes     no     2.8
## 465     2      4      4      5      5      5      yes     no     2.2
## 466     3      2      4      4      4      3      yes     no     2.0
## 467     3      3      4      3      4      3      yes     no     2.4
## 468     2      4      3      5      4      5       no     no     1.8
## 469     4      2      3      3      4      2      yes    yes     3.2
## 470     3      3      3      3      3      3      yes     no     3.0
## 471     3      4      4      5      5      4      yes     no     3.0
## 472     5      2      3      3      2      4      yes    yes     3.4
## 473     5      4      5      4      4      4      yes    yes     2.8
## 474     5      4      4      4      4      4      yes     no     3.4
## 475     4      2      4      2      3      2      yes    yes     2.4
## 476     5      3      4      3      4      2      yes    yes     3.4
## 477     5      2      2      2      2      3      yes    yes     5.0
## 478     3      3      3      2      4      2      yes     no     2.6
## 479     5      3      3      4      4      3      yes    yes     5.0
## 480     4      1      1      1      2      1      yes    yes     4.8
## 481     5      3      4      2      5      2      yes    yes     3.6
## 482     1      3      4      4      4      4      yes     no     2.6
## 483     2      4      4      4      4      4      yes    yes     3.6
## 484     4      4      4      5      5      4      yes    yes     2.8
## 485     4      3      3      4      5      5      yes     no     2.4
## 486     4      3      2      2      3      4      yes     no     3.0
## 487     5      4      5      3      5      4      yes    yes     3.6
## 488     3      1      1      1      2      1      yes    yes     1.6
## 489     4      3      2      3      4      2      yes     no     3.6
## 490     5      3      2      1      1      1      yes    yes     2.8
## 491     4      3      2      3      3      1      yes    yes     3.0
## 492     5      3      3      3      3      3       no    yes     3.4
## 493     3      2      3      2      2      1      yes     no     1.6
## 494     3      2      3      3      2      2      yes    yes     4.4
## 495     3      4      4      4      3      3      yes    yes     2.0
## 496     4      4      4      4      4      3      yes    yes     3.6
## 497     5      3      2      4      3      1      yes    yes     2.4
## 498     4      4      4      4      4      3      yes     no     2.4
## 499     2      3      3      1      4      3      yes    yes     2.8
## 500     3      3      4      3      4      3      yes     no     4.0
## 501     3      4      4      4      4      4       no     no     2.6
## 502     1      3      3      1      3      1      yes    yes     3.6
## 503     3      3      4      3      5      4      yes    yes     3.8
## 504     4      3      4      2      5      3      yes    yes     3.2
## 505     3      4      4      4      4      4       no     no     2.0
## 506     1      5      5      5      5      3       no     no     1.2
## 507     2      5      5      5      5      4       no     no     1.6
## 508     3      4      4      4      4      3      yes     no     1.4
## 509     2      4      4      4      5      4       no     no     1.8
## 510     4      5      5      5      5      2      yes    yes     3.0
## 511     2      4      3      4      4      4       no     no     1.0
## 512     5      4      4      4      5      4      yes    yes     2.2
## 513     4      4      4      4      4      2      yes    yes     3.8
## 514     3      4      4      4      4      4      yes    yes     1.4
## 515     5      1      3      3      2      1      yes    yes     4.2
## 516     4      2      2      2      2      2      yes    yes     3.0
## 517     2      4      4      4      3      3      yes     no     2.4
## 518     3      3      3      3      4      2      yes     no     3.0
## 519     1      3      3      4      4      3       no     no     1.4
## 520     4      2      3      3      3      1      yes     no     3.2
## 521     3      2      3      2      2      1      yes    yes     3.2
## 522     5      4      4      4      4      2      yes    yes     3.2
## 523     4      3      3      3      4      2      yes     no     3.4
## 524     2      3      3      3      3      2      yes    yes     3.2
## 525     4      1      1      3      2      1      yes     no     1.8
## 526     2      5      5      5      2      1       no     no     2.8
## 527     2      1      1      1      1      1       no     no     1.0
## 528     3      4      3      3      4      2      yes    yes     3.2
## 529     3      1      2      1      3      1      yes    yes     3.2
## 530     4      3      3      3      3      2       no     no     3.0
## 531     3      3      3      4      4      4       no     no     2.0
## 532     3      2      2      2      3      1      yes    yes     3.0
## 533     5      3      2      2      2      2      yes    yes     3.0
## 534     3      3      4      3      5      4      yes    yes     3.6
## 535     3      3      3      3      4      1      yes     no     2.0
## 536     2      4      4      4      5      4       no            2.0
## 537     5      1      5      2      5      3      yes    yes     3.6
## 538     5      2      3      2      2      2      yes    yes     4.0
## 539     4      3      4      4      4      2      yes     no     2.6
## 540     5      3      3      3      4      4      yes     no     4.0
## 541     4      3      3      3      2      2      yes     no     2.6
## 542     2      4      4      4      4      3       no     no     2.4
## 543     2      4      2      2      4      1       no     no     2.4
## 544     2      4      3      3      3      3       no     no     1.4
## 545     1      3      4      4      4      5      yes     no     1.4
## 546     3      3      4      5      4      1      yes     no     1.2
## 547     3      2      3      3      4      3      yes     no     2.8
## 548     5      3      3      3      3      3      yes     no     3.6
## 549     2      1      2      2      2      1      yes    yes     3.0
## 550     3      4      3      4      4      4       no     no     2.0
## 551     3      5      5      5      5      4      yes    yes     3.2
## 552     3      1      2      2      1      4      yes     no     2.8
## 553     3      4      4      4      4      4      yes    yes     2.0
## 554     5      1      1      1      1      2      yes    yes     5.0
## 555     4      4      4      5      3      1      yes    yes     3.8
## 556     3      3      3      3      3      3      yes     no     2.6
## 557     2      4      4      4      2      2      yes     no     3.4
## 558     5      1      4      1      1      1      yes    yes     5.0
## 559     1      4      4      4      4      3       no     no     2.0
## 560     3      4      4      3      4      4       no     no     2.4
## 561     1      4      3      4      4      3       no     no     1.4
## 562     5      4      3      4      5      1      yes    yes     2.6
## 563     2      4      4      4      4      4      yes    yes     2.0
## 564     2      4      4      4      3      3      yes     no     2.6
## 565     2      2      2      2      2      3       no    yes     2.4
## 566     2      2      3      1      4      5       no     no     1.6
## 567     5      3      4      3      3      1      yes    yes     2.0
## 568     3      3      3      3      3      3      yes    yes     1.8
## 569     5      1      1      3      2      1      yes     no     2.6
## 570     4      2      2      2      2      2      yes            2.0
##     AIP_Mean GP_Mean SWLS_Mean   HDI        Development.Category
## 1   3.000000    2.95       3.6 0.827 Very high human development
## 2   3.266667    3.80       3.6 0.939 Very high human development
## 3   2.133333    2.15       2.4 0.939 Very high human development
## 4   3.333333    3.55       2.0 0.939 Very high human development
## 5   3.800000    3.25       3.8 0.939 Very high human development
## 6   2.800000    3.60       4.2 0.939 Very high human development
## 7   3.066667    3.45       3.4 0.939 Very high human development
## 8   3.600000    3.60       2.8 0.939 Very high human development
## 9   3.000000    3.80       4.2 0.939 Very high human development
## 10  1.866667    2.70       2.0 0.939 Very high human development
## 11  2.400000    2.30       3.0 0.939 Very high human development
## 12  1.000000    1.75       2.6 0.939 Very high human development
## 13  3.933333    3.45       2.0 0.939 Very high human development
## 14  3.400000    3.85       3.2 0.939 Very high human development
## 15  3.466667    3.80       1.4 0.939 Very high human development
## 16  3.000000    3.05       3.0 0.939 Very high human development
## 17  3.933333    3.40       3.8 0.939 Very high human development
## 18  2.200000    2.80       3.2 0.939 Very high human development
## 19  3.666667    3.75       2.8 0.939 Very high human development
## 21  2.733333    2.55       3.4    NA                        <NA>
## 22  2.933333    2.90       3.6 0.674    Medium human development
## 23  2.866667    3.55       3.0 0.754      High human development
## 24  3.133333    3.65       2.8 0.754      High human development
## 25  3.533333    3.40       3.4 0.920 Very high human development
## 26  1.866667    2.50       3.0 0.920 Very high human development
## 27  2.733333    2.75       2.4 0.920 Very high human development
## 28  2.733333    2.75       2.4 0.920 Very high human development
## 29  4.466667    4.85       1.0 0.920 Very high human development
## 30  2.333333    3.15       3.0 0.920 Very high human development
## 31  3.800000    3.95       2.0 0.920 Very high human development
## 32  3.866667    3.75       1.6 0.920 Very high human development
## 33  2.600000    3.05       3.0 0.920 Very high human development
## 34  1.800000    2.60       3.8 0.920 Very high human development
## 35  3.800000    3.50       2.6 0.920 Very high human development
## 36  4.600000    4.20       1.6 0.920 Very high human development
## 37  2.866667    3.05       4.0 0.920 Very high human development
## 38  2.333333    3.35       2.8 0.920 Very high human development
## 39  4.333333    4.10       2.4 0.920 Very high human development
## 40  3.066667    3.60       4.4 0.920 Very high human development
## 41  3.800000    3.40       2.6 0.920 Very high human development
## 42  3.600000    3.65       2.0 0.920 Very high human development
## 43  3.000000    3.35       3.6 0.920 Very high human development
## 44  4.000000    3.80       2.4 0.920 Very high human development
## 45  2.600000    3.30       2.6 0.920 Very high human development
## 46  3.066667    3.60       2.2 0.920 Very high human development
## 47  3.866667    3.35       4.6 0.920 Very high human development
## 48  2.800000    3.45       2.0 0.920 Very high human development
## 49  4.333333    3.80       2.2 0.920 Very high human development
## 50  4.800000    4.30       3.2 0.920 Very high human development
## 51  2.600000    2.65       3.4 0.920 Very high human development
## 52  1.800000    3.05       4.0 0.920 Very high human development
## 53  3.133333    2.55       1.6 0.920 Very high human development
## 54  4.200000    4.30       2.6 0.920 Very high human development
## 55  2.000000    2.20       5.0 0.920 Very high human development
## 56  3.200000    3.75       2.4 0.920 Very high human development
## 57  4.600000    4.15       3.0 0.920 Very high human development
## 58  4.333333    4.55       2.8 0.920 Very high human development
## 59  4.466667    4.70       1.0 0.920 Very high human development
## 60  4.066667    3.95       2.0 0.738      High human development
## 61  2.066667    2.70       3.4 0.827 Very high human development
## 62  3.333333    3.25       1.4 0.925 Very high human development
## 63  2.666667    3.20       3.6 0.925 Very high human development
## 64  4.133333    3.55       2.2 0.739      High human development
## 65  3.533333    3.55       3.4 0.897 Very high human development
## 66  3.333333    4.00       2.8 0.926 Very high human development
## 67  3.733333    3.70       2.6 0.926 Very high human development
## 68  3.400000    3.70       1.4 0.866 Very high human development
## 69  2.466667    2.45       1.6 0.866 Very high human development
## 70  1.733333    1.50       2.0 0.624    Medium human development
## 71  3.200000    2.85       3.2 0.624    Medium human development
## 72  3.333333    3.60       3.2 0.624    Medium human development
## 73  3.266667    3.85       3.8 0.624    Medium human development
## 74  4.000000    3.70       2.6 0.624    Medium human development
## 75  2.866667    2.70       3.6 0.624    Medium human development
## 76  4.400000    4.45       1.2 0.624    Medium human development
## 77  3.333333    4.45       3.0 0.923 Very high human development
## 78  2.666667    2.80       4.0 0.923 Very high human development
## 79  4.200000    3.95       3.4 0.923 Very high human development
## 80  2.800000    3.15       3.2 0.899 Very high human development
## 81  1.733333    1.65       5.0 0.899 Very high human development
## 82  2.066667    2.25       1.0 0.887 Very high human development
## 83  2.133333    3.00       3.0 0.887 Very high human development
## 84  3.800000    3.15       2.4 0.887 Very high human development
## 85  2.533333    2.55       4.0 0.887 Very high human development
## 86  1.666667    2.30       3.8 0.887 Very high human development
## 87  3.066667    3.55       2.8 0.887 Very high human development
## 88  3.333333    3.60       3.6 0.887 Very high human development
## 89  3.733333    2.60       4.8 0.887 Very high human development
## 90  3.400000    3.20       2.8 0.887 Very high human development
## 91  4.466667    4.00       3.8 0.887 Very high human development
## 92  2.933333    3.45       4.4 0.730      High human development
## 93  2.600000    3.35       2.2 0.903 Very high human development
## 94  2.466667    3.65       3.4 0.789      High human development
## 95  2.733333    2.55       3.8 0.762      High human development
## 96  2.733333    3.60       3.2 0.762      High human development
## 97  1.466667    2.15       4.0 0.762      High human development
## 98  2.133333    2.90       3.4 0.924 Very high human development
## 99  3.800000    3.55       3.8 0.924 Very high human development
## 100 3.733333    4.10       2.0 0.915 Very high human development
## 101 2.800000    3.30       2.2 0.949 Very high human development
## 102 1.600000    2.20       4.8 0.949 Very high human development
## 103 2.800000    3.15       4.0 0.550    Medium human development
## 104 2.800000    3.20       3.4 0.682    Medium human development
## 105 3.133333    3.00       5.0 0.682    Medium human development
## 106 3.600000    3.95       2.8 0.855 Very high human development
## 107 2.866667    3.60       3.4 0.843 Very high human development
## 108 3.333333    4.05       1.2 0.843 Very high human development
## 109 1.600000    1.85       3.0 0.901 Very high human development
## 110 4.200000    4.05       3.0 0.884 Very high human development
## 111 3.466667    4.20       2.8 0.913 Very high human development
## 112 2.600000    3.00       3.4 0.939 Very high human development
## 113 2.000000    3.00       3.6 0.939 Very high human development
## 114 1.400000    1.20       2.8 0.939 Very high human development
## 115 2.066667    3.15       3.8 0.939 Very high human development
## 116 1.866667    2.00       3.8 0.740      High human development
## 117 2.533333    3.65       2.0 0.909 Very high human development
## 118 3.733333    3.65       3.0 0.909 Very high human development
## 119 3.933333    3.95       3.2 0.909 Very high human development
## 120 3.533333    3.55       2.0 0.909 Very high human development
## 121 1.400000    1.65       3.0 0.909 Very high human development
## 122 3.266667    3.75       2.2 0.909 Very high human development
## 123 2.933333    3.10       4.2 0.909 Very high human development
## 124 3.800000    3.95       1.4 0.909 Very high human development
## 125 4.533333    4.25       2.8 0.909 Very high human development
## 126 2.733333    3.75       2.0 0.909 Very high human development
## 127 3.000000    3.45       2.2 0.909 Very high human development
## 128 4.466667    4.20       1.2 0.909 Very high human development
## 129 4.000000    4.20       3.8 0.909 Very high human development
## 130 1.933333    2.20       3.4 0.909 Very high human development
## 131 3.733333    3.75       2.8 0.909 Very high human development
## 132 2.733333    3.10       3.2 0.909 Very high human development
## 133 3.133333    2.95       2.4 0.909 Very high human development
## 134 3.533333    3.85       2.8 0.909 Very high human development
## 135 1.466667    2.00       3.4 0.909 Very high human development
## 136 2.866667    3.25       3.6 0.909 Very high human development
## 137 2.933333    3.20       1.4 0.909 Very high human development
## 138 2.600000    2.95       4.0 0.909 Very high human development
## 139 3.466667    3.75       2.0 0.909 Very high human development
## 140 2.000000    2.95       3.6 0.909 Very high human development
## 141 3.000000    3.30       2.6 0.909 Very high human development
## 142 3.200000    3.45       1.0 0.909 Very high human development
## 143 4.266667    4.55       2.8 0.909 Very high human development
## 144 4.466667    3.95       2.6 0.920 Very high human development
## 145 1.733333    1.35       2.4 0.920 Very high human development
## 146 2.466667    3.55       2.6 0.920 Very high human development
## 147 2.133333    2.95       2.0 0.920 Very high human development
## 148 2.066667    2.20       2.2 0.920 Very high human development
## 149 2.133333    2.70       4.4 0.920 Very high human development
## 150 1.866667    3.25       3.6 0.920 Very high human development
## 151 3.666667    3.85       2.2 0.920 Very high human development
## 152 2.866667    3.00       3.4 0.920 Very high human development
## 153 4.200000    4.15       1.8 0.920 Very high human development
## 154 3.333333    3.75       2.8 0.920 Very high human development
## 155 2.933333    3.35       2.4 0.920 Very high human development
## 156 3.466667    3.60       2.0 0.920 Very high human development
## 157 4.133333    3.85       2.8 0.920 Very high human development
## 158 3.000000    3.60       5.0 0.920 Very high human development
## 159 3.866667    4.55       4.6 0.920 Very high human development
## 160 1.400000    2.00       5.0 0.920 Very high human development
## 161 2.600000    3.20       2.0 0.920 Very high human development
## 162 3.600000    3.60       3.0 0.920 Very high human development
## 163 3.333333    3.65       3.2 0.920 Very high human development
## 164 2.533333    3.50       3.2 0.920 Very high human development
## 165 2.133333    2.35       2.8 0.920 Very high human development
## 166 3.400000    3.10       2.8 0.920 Very high human development
## 167 3.066667    3.80       3.4 0.920 Very high human development
## 168 3.466667    3.65       1.8 0.920 Very high human development
## 169 1.733333    2.75       4.0 0.920 Very high human development
## 170 1.800000    1.75       3.6 0.920 Very high human development
## 171 2.733333    2.35       3.2 0.920 Very high human development
## 172 3.666667    3.75       2.8 0.920 Very high human development
## 173 3.333333    3.55       2.8 0.920 Very high human development
## 174 3.933333    3.35       3.8 0.920 Very high human development
## 175 2.600000    3.25       4.0 0.920 Very high human development
## 176 2.333333    3.10       4.4 0.920 Very high human development
## 177 3.600000    3.30       3.8 0.920 Very high human development
## 178 2.733333    3.20       2.4 0.920 Very high human development
## 179 2.866667    2.95       2.8 0.920 Very high human development
## 180 3.266667    2.80       4.4 0.920 Very high human development
## 181 4.533333    4.40       1.4 0.920 Very high human development
## 182 1.333333    1.85       4.6 0.920 Very high human development
## 183 3.600000    3.50       1.8 0.920 Very high human development
## 184 3.800000    4.45       4.2 0.920 Very high human development
## 185 4.266667    3.55       3.0 0.920 Very high human development
## 186 1.933333    2.15       3.6 0.920 Very high human development
## 187 3.800000    3.70       3.8 0.920 Very high human development
## 188 3.533333    3.20       2.8 0.920 Very high human development
## 189 3.066667    3.45       4.2 0.920 Very high human development
## 190 2.066667    2.35       3.2 0.920 Very high human development
## 191 3.133333    3.65       3.6 0.920 Very high human development
## 192 3.066667    3.55       3.2 0.920 Very high human development
## 193 4.066667    4.25       2.2 0.920 Very high human development
## 194 2.133333    2.40       3.4 0.920 Very high human development
## 195 4.266667    3.95       2.4 0.920 Very high human development
## 196 2.133333    2.15       3.8 0.920 Very high human development
## 197 2.266667    2.45       4.0 0.920 Very high human development
## 198 3.000000    2.80       2.8 0.920 Very high human development
## 199 2.066667    2.30       3.6 0.920 Very high human development
## 200 3.133333    3.75       2.2 0.920 Very high human development
## 201 4.000000    4.45       3.0 0.920 Very high human development
## 202 3.800000    3.45       3.2 0.920 Very high human development
## 203 3.533333    3.50       1.8 0.920 Very high human development
## 204 3.600000    2.85       3.6 0.920 Very high human development
## 205 3.733333    4.45       3.4 0.920 Very high human development
## 206 3.400000    2.80       1.2 0.920 Very high human development
## 207 1.733333    1.35       3.8 0.920 Very high human development
## 208 3.600000    3.45       3.6 0.920 Very high human development
## 209 1.800000    2.35       1.8 0.920 Very high human development
## 210 2.200000    3.10       3.6 0.920 Very high human development
## 211 3.133333    3.60       2.8 0.920 Very high human development
## 212 4.800000    4.80       2.4 0.920 Very high human development
## 213 3.066667    3.90       3.6 0.920 Very high human development
## 214 2.733333    3.40       2.8 0.920 Very high human development
## 215 2.466667    2.65       4.6 0.920 Very high human development
## 216 2.200000    2.45       1.0 0.920 Very high human development
## 217 4.333333    3.95       1.6 0.920 Very high human development
## 218 3.266667    4.05       1.6 0.920 Very high human development
## 219 3.333333    3.80       1.4 0.920 Very high human development
## 220 2.600000    2.40       3.8 0.920 Very high human development
## 221 2.800000    2.85       4.6 0.920 Very high human development
## 222 2.800000    2.50       4.2 0.920 Very high human development
## 223 1.933333    2.50       3.8 0.920 Very high human development
## 224 3.200000    3.70       2.0 0.920 Very high human development
## 225 3.000000    3.30       3.8 0.920 Very high human development
## 226 3.200000    3.10       3.4 0.920 Very high human development
## 227 3.066667    3.35       2.0 0.920 Very high human development
## 228 1.000000    1.15       4.4 0.920 Very high human development
## 229 2.800000    2.85       2.2 0.920 Very high human development
## 230 3.000000    3.45       3.0 0.920 Very high human development
## 231 3.933333    3.40       2.8 0.920 Very high human development
## 232 2.466667    3.00       3.0 0.920 Very high human development
## 233 3.800000    3.50       3.2 0.920 Very high human development
## 234 3.133333    3.50       3.6 0.920 Very high human development
## 235 1.333333    2.10       2.2 0.920 Very high human development
## 236 3.200000    3.45       2.6 0.920 Very high human development
## 237 3.266667    3.35       2.2 0.920 Very high human development
## 238 2.866667    2.45       3.0 0.920 Very high human development
## 239 3.000000    3.15       3.6 0.920 Very high human development
## 240 2.933333    3.35       4.2 0.920 Very high human development
## 241 2.733333    3.15       4.2 0.920 Very high human development
## 242 3.933333    4.40       2.2 0.920 Very high human development
## 243 4.666667    4.50       1.2 0.920 Very high human development
## 244 2.666667    2.20       3.6 0.920 Very high human development
## 245 1.733333    2.45       3.6 0.920 Very high human development
## 246 2.533333    2.25       2.0 0.920 Very high human development
## 247 2.733333    3.00       4.4 0.920 Very high human development
## 248 4.266667    4.40       3.4 0.920 Very high human development
## 249 2.600000    2.90       4.0 0.920 Very high human development
## 250 2.733333    2.75       2.4 0.920 Very high human development
## 251 3.333333    3.75       3.2 0.920 Very high human development
## 252 2.733333    2.95       2.6 0.920 Very high human development
## 253 4.000000    3.45       2.8 0.920 Very high human development
## 254 2.800000    3.45       4.0 0.920 Very high human development
## 255 2.600000    3.40       3.2 0.920 Very high human development
## 256 2.000000    2.55       2.4 0.920 Very high human development
## 257 3.800000    4.15       2.6 0.920 Very high human development
## 258 2.733333    3.20       3.0 0.920 Very high human development
## 259 3.733333    3.55       2.4 0.920 Very high human development
## 260 2.466667    3.00       3.6 0.920 Very high human development
## 261 4.133333    4.05       2.2 0.920 Very high human development
## 262 2.466667    2.90       3.4 0.920 Very high human development
## 263 1.666667    2.00       4.0 0.920 Very high human development
## 264 2.400000    2.65       4.6 0.920 Very high human development
## 265 1.866667    2.85       3.8 0.920 Very high human development
## 266 3.866667    3.70       3.4 0.920 Very high human development
## 267 1.933333    2.40       4.0 0.920 Very high human development
## 268 4.133333    3.60       2.8 0.920 Very high human development
## 269 2.066667    2.65       3.6 0.920 Very high human development
## 270 2.400000    2.30       3.4 0.920 Very high human development
## 271 2.800000    3.10       3.0 0.920 Very high human development
## 272 2.666667    3.40       2.0 0.920 Very high human development
## 273 4.400000    4.20       1.0 0.920 Very high human development
## 274 2.133333    2.30       2.0 0.920 Very high human development
## 275 2.666667    2.30       4.6 0.920 Very high human development
## 276 1.866667    2.00       3.6 0.920 Very high human development
## 277 2.600000    3.35       3.6 0.920 Very high human development
## 278 3.400000    3.95       3.0 0.920 Very high human development
## 279 4.000000    3.70       2.0 0.920 Very high human development
## 280 3.466667    3.50       1.8 0.920 Very high human development
## 281 3.666667    3.85       3.4 0.920 Very high human development
## 282 4.200000    4.55       3.2 0.920 Very high human development
## 283 2.533333    2.90       4.6 0.920 Very high human development
## 284 4.066667    3.45       2.6 0.920 Very high human development
## 285 3.200000    3.30       2.2 0.920 Very high human development
## 286 1.333333    2.70       5.0 0.920 Very high human development
## 287 1.933333    2.15       4.2 0.920 Very high human development
## 288 2.666667    2.70       3.6 0.920 Very high human development
## 289 3.266667    2.80       3.2 0.920 Very high human development
## 290 4.333333    4.00       2.2 0.920 Very high human development
## 291 3.533333    4.40       1.2 0.920 Very high human development
## 292 2.133333    2.35       3.6 0.920 Very high human development
## 293 2.066667    2.55       3.0 0.920 Very high human development
## 294 1.933333    3.05       3.4 0.920 Very high human development
## 295 3.333333    3.90       3.0 0.920 Very high human development
## 296 3.000000    3.65       1.6 0.920 Very high human development
## 297 2.933333    3.45       2.4 0.920 Very high human development
## 298 1.933333    1.90       3.4 0.920 Very high human development
## 299 1.400000    1.70       4.0 0.920 Very high human development
## 300 4.066667    4.25       2.0 0.920 Very high human development
## 301 2.600000    3.55       3.2 0.920 Very high human development
## 302 2.800000    3.00       3.6 0.920 Very high human development
## 303 3.533333    3.95       3.0 0.920 Very high human development
## 304 2.266667    2.85       2.0 0.920 Very high human development
## 305 2.600000    3.20       1.8 0.920 Very high human development
## 306 1.866667    2.70       4.8 0.920 Very high human development
## 307 2.666667    3.05       3.8 0.920 Very high human development
## 308 3.666667    3.75       2.4 0.920 Very high human development
## 309 1.533333    2.35       2.6 0.920 Very high human development
## 310 4.133333    3.55       3.0 0.920 Very high human development
## 311 1.400000    1.75       3.8 0.920 Very high human development
## 312 4.333333    3.40       2.4 0.920 Very high human development
## 313 2.600000    2.70       3.8 0.920 Very high human development
## 314 2.600000    3.55       4.2 0.920 Very high human development
## 315 2.400000    2.45       4.0 0.920 Very high human development
## 316 4.266667    4.10       1.0 0.920 Very high human development
## 317 3.000000    3.05       3.8 0.920 Very high human development
## 318 3.733333    4.15       1.8 0.920 Very high human development
## 319 4.466667    4.20       2.8 0.920 Very high human development
## 320 2.466667    2.90       5.0 0.920 Very high human development
## 321 2.400000    3.00       3.8 0.920 Very high human development
## 322 3.200000    3.05       1.8 0.920 Very high human development
## 323 4.400000    4.25       2.6 0.920 Very high human development
## 324 3.333333    3.70       3.0 0.920 Very high human development
## 325 2.000000    2.80       4.6 0.920 Very high human development
## 326 2.066667    2.20       2.8 0.920 Very high human development
## 327 4.600000    4.45       2.4 0.920 Very high human development
## 328 2.933333    3.15       3.0 0.920 Very high human development
## 329 2.666667    2.80       3.0 0.920 Very high human development
## 330 3.000000    3.20       3.6 0.920 Very high human development
## 331 1.733333    2.40       3.6 0.920 Very high human development
## 332 2.666667    2.85       4.6 0.920 Very high human development
## 333 2.600000    1.60       5.0 0.920 Very high human development
## 334 4.466667    3.95       1.6 0.920 Very high human development
## 335 2.600000    3.00       2.8 0.920 Very high human development
## 336 3.666667    3.50       1.2 0.920 Very high human development
## 337 1.866667    2.85       4.2 0.920 Very high human development
## 338 1.933333    2.50       2.6 0.920 Very high human development
## 339 3.000000    3.20       2.8 0.920 Very high human development
## 340 2.733333    3.60       1.8 0.920 Very high human development
## 341 3.200000    2.95       4.6 0.920 Very high human development
## 342 2.800000    2.55       3.0 0.920 Very high human development
## 343 2.866667    3.05       4.0 0.920 Very high human development
## 344 2.533333    3.75       3.8 0.920 Very high human development
## 345 2.266667    2.35       3.2 0.920 Very high human development
## 346 3.000000    3.10       4.0 0.920 Very high human development
## 347 4.400000    4.15       3.2 0.920 Very high human development
## 348 3.200000    3.20       5.0 0.920 Very high human development
## 349 1.933333    2.15       4.4 0.920 Very high human development
## 350 3.533333    3.80       3.6 0.920 Very high human development
## 351 2.933333    3.05       5.0 0.920 Very high human development
## 352 1.600000    2.35       4.4 0.920 Very high human development
## 353 4.333333    4.10       3.0 0.920 Very high human development
## 354 2.133333    2.50       3.4 0.920 Very high human development
## 355 2.066667    2.00       3.8 0.920 Very high human development
## 356 2.933333    3.15       2.8 0.920 Very high human development
## 357 1.466667    1.90       4.2 0.920 Very high human development
## 358 3.200000    3.40       5.0 0.920 Very high human development
## 359 3.000000    3.75       2.8 0.920 Very high human development
## 360 3.666667    3.90       2.4 0.920 Very high human development
## 361 1.266667    1.40       5.0 0.920 Very high human development
## 362 2.933333    3.65       3.0 0.920 Very high human development
## 363 3.333333    2.55       3.0 0.920 Very high human development
## 364 3.266667    3.30       1.8 0.920 Very high human development
## 365 1.866667    3.10       4.6 0.920 Very high human development
## 366 3.666667    3.50       3.0 0.920 Very high human development
## 367 4.266667    4.30       2.8 0.920 Very high human development
## 368 2.933333    4.00       2.2 0.920 Very high human development
## 369 4.066667    3.50       2.8 0.920 Very high human development
## 370 2.200000    2.80       4.6 0.920 Very high human development
## 371 2.666667    3.10       3.6 0.920 Very high human development
## 372 1.933333    2.85       4.2 0.920 Very high human development
## 373 2.066667    2.65       4.8 0.920 Very high human development
## 374 2.533333    2.60       4.0 0.920 Very high human development
## 375 2.333333    2.35       3.4 0.920 Very high human development
## 376 2.200000    2.35       3.6 0.920 Very high human development
## 377 3.666667    4.95       1.0 0.920 Very high human development
## 378 3.466667    3.30       3.0 0.920 Very high human development
## 379 2.066667    3.05       2.8 0.920 Very high human development
## 380 2.333333    3.10       3.4 0.920 Very high human development
## 381 3.666667    3.40       3.4 0.920 Very high human development
## 382 2.733333    3.05       2.8 0.920 Very high human development
## 383 3.066667    3.05       4.6 0.920 Very high human development
## 384 3.866667    3.95       1.8 0.920 Very high human development
## 385 3.600000    3.80       3.6 0.920 Very high human development
## 386 2.800000    3.10       2.8 0.920 Very high human development
## 387 3.133333    3.05       2.8 0.920 Very high human development
## 388 3.600000    3.55       2.8 0.920 Very high human development
## 389 2.133333    2.15       4.4 0.920 Very high human development
## 390 3.666667    4.00       2.4 0.920 Very high human development
## 391 1.533333    1.95       4.0 0.920 Very high human development
## 392 2.200000    2.85       3.8 0.920 Very high human development
## 393 2.600000    3.50       2.4 0.920 Very high human development
## 394 3.466667    3.40       4.0 0.920 Very high human development
## 395 4.133333    4.25       3.4 0.920 Very high human development
## 396 3.066667    3.15       3.2 0.920 Very high human development
## 397 3.333333    3.05       3.4 0.920 Very high human development
## 398 2.200000    2.55       4.0 0.920 Very high human development
## 399 3.066667    3.70       1.0 0.920 Very high human development
## 400 2.533333    2.45       3.4 0.920 Very high human development
## 401 1.933333    2.15       4.0 0.920 Very high human development
## 402 2.733333    2.85       3.0 0.920 Very high human development
## 403 3.800000    3.15       3.6 0.920 Very high human development
## 404 4.800000    4.60       1.8 0.920 Very high human development
## 405 2.733333    2.55       3.0 0.920 Very high human development
## 406 2.933333    2.55       2.6 0.920 Very high human development
## 407 3.000000    3.95       1.8 0.920 Very high human development
## 408 2.800000    2.20       2.2 0.920 Very high human development
## 409 1.733333    2.20       2.6 0.920 Very high human development
## 410 2.466667    3.20       3.0 0.920 Very high human development
## 411 2.733333    3.00       4.0 0.920 Very high human development
## 412 2.466667    3.10       2.2 0.920 Very high human development
## 413 2.800000    2.45       4.0 0.920 Very high human development
## 414 3.733333    3.70       3.0 0.920 Very high human development
## 415 2.733333    3.65       3.0 0.920 Very high human development
## 416 4.200000    4.00       4.0 0.920 Very high human development
## 417 2.333333    3.10       2.4 0.920 Very high human development
## 418 2.400000    2.50       4.4 0.920 Very high human development
## 419 3.800000    4.15       3.2 0.920 Very high human development
## 420 3.866667    3.85       3.6 0.920 Very high human development
## 421 4.400000    4.50       2.0 0.920 Very high human development
## 422 3.066667    3.50       2.6 0.920 Very high human development
## 423 3.066667    3.60       4.2 0.920 Very high human development
## 424 1.800000    2.65       2.2 0.920 Very high human development
## 426 2.466667    3.45       3.2 0.920 Very high human development
## 427 3.266667    3.30       1.6 0.920 Very high human development
## 428 4.133333    3.35       2.4 0.920 Very high human development
## 429 3.933333    4.05       3.2 0.920 Very high human development
## 430 2.800000    2.90       3.8 0.920 Very high human development
## 431 3.733333    3.70       2.8 0.920 Very high human development
## 432 3.800000    4.40       2.0 0.920 Very high human development
## 433 1.533333    1.85       4.8 0.920 Very high human development
## 434 3.200000    3.55       3.2 0.920 Very high human development
## 435 3.466667    3.70       4.0 0.920 Very high human development
## 436 2.666667    3.15       2.2 0.920 Very high human development
## 437 3.133333    3.40       3.2 0.920 Very high human development
## 438 3.333333    3.30       2.8 0.920 Very high human development
## 439 2.933333    3.30       3.2 0.920 Very high human development
## 440 4.400000    4.55       2.2 0.920 Very high human development
## 441 2.333333    2.35       3.0 0.920 Very high human development
## 442 4.266667    4.30       2.0 0.920 Very high human development
## 443 2.466667    2.50       3.4 0.920 Very high human development
## 444 1.666667    2.30       3.8 0.920 Very high human development
## 445 3.466667    2.75       3.8 0.920 Very high human development
## 446 3.866667    4.10       2.4 0.920 Very high human development
## 447 2.000000    2.15       3.8 0.920 Very high human development
## 448 3.400000    3.40       2.8 0.920 Very high human development
## 449 2.533333    2.60       4.6 0.920 Very high human development
## 450 3.600000    3.75       3.6 0.920 Very high human development
## 451 2.866667    3.65       5.0 0.920 Very high human development
## 452 2.466667    1.70       3.8 0.920 Very high human development
## 453 3.733333    4.10       3.2 0.920 Very high human development
## 454 2.400000    3.00       2.8 0.920 Very high human development
## 455 2.933333    2.70       3.4 0.920 Very high human development
## 456 2.866667    3.20       3.6 0.920 Very high human development
## 457 2.000000    2.05       4.0 0.920 Very high human development
## 458 4.266667    4.65       1.0 0.920 Very high human development
## 459 1.066667    1.55       4.8 0.920 Very high human development
## 460 2.333333    2.75       3.6 0.920 Very high human development
## 461 2.333333    3.35       4.0 0.920 Very high human development
## 462 3.800000    4.00       2.8 0.920 Very high human development
## 463 4.333333    4.30       2.8 0.920 Very high human development
## 464 2.400000    3.40       3.8 0.920 Very high human development
## 465 2.333333    2.35       4.6 0.920 Very high human development
## 466 2.333333    2.05       3.4 0.920 Very high human development
## 467 2.200000    3.00       3.4 0.920 Very high human development
## 468 2.200000    2.05       4.2 0.920 Very high human development
## 469 3.066667    3.60       2.8 0.920 Very high human development
## 470 2.400000    2.60       3.0 0.920 Very high human development
## 471 1.800000    2.60       4.4 0.920 Very high human development
## 472 4.466667    4.05       2.8 0.920 Very high human development
## 473 3.000000    3.35       4.2 0.920 Very high human development
## 474 3.133333    3.65       4.0 0.920 Very high human development
## 475 3.400000    3.15       2.6 0.920 Very high human development
## 476 3.000000    2.80       3.2 0.920 Very high human development
## 477 3.400000    4.10       2.2 0.920 Very high human development
## 478 2.800000    2.85       2.8 0.920 Very high human development
## 479 4.133333    3.85       3.4 0.920 Very high human development
## 480 4.000000    3.90       1.2 0.920 Very high human development
## 481 2.866667    3.75       3.2 0.920 Very high human development
## 482 1.800000    2.10       3.8 0.920 Very high human development
## 483 2.866667    3.85       4.0 0.920 Very high human development
## 484 2.333333    3.00       4.4 0.920 Very high human development
## 485 2.666667    2.85       4.0 0.920 Very high human development
## 486 3.400000    3.20       2.8 0.920 Very high human development
## 487 3.666667    4.05       4.2 0.920 Very high human development
## 488 3.533333    3.20       1.2 0.920 Very high human development
## 489 2.600000    3.50       2.8 0.920 Very high human development
## 490 3.000000    4.10       1.6 0.920 Very high human development
## 491 3.533333    3.70       2.4 0.920 Very high human development
## 492 3.000000    3.80       3.0 0.920 Very high human development
## 493 1.733333    2.25       2.0 0.920 Very high human development
## 494 3.066667    3.55       2.4 0.920 Very high human development
## 495 2.733333    3.10       3.6 0.920 Very high human development
## 496 4.000000    3.95       3.8 0.920 Very high human development
## 497 3.266667    4.15       2.6 0.920 Very high human development
## 498 3.000000    3.35       3.8 0.920 Very high human development
## 499 3.400000    3.10       2.8 0.920 Very high human development
## 500 3.133333    3.35       3.4 0.920 Very high human development
## 501 2.200000    2.35       4.0 0.920 Very high human development
## 502 4.266667    3.90       2.2 0.920 Very high human development
## 503 3.533333    3.30       3.8 0.920 Very high human development
## 504 2.866667    3.95       3.4 0.920 Very high human development
## 505 2.466667    2.50       4.0 0.920 Very high human development
## 506 1.866667    1.75       4.6 0.920 Very high human development
## 507 2.133333    1.80       4.8 0.920 Very high human development
## 508 1.800000    2.10       3.8 0.920 Very high human development
## 509 1.666667    2.00       4.2 0.920 Very high human development
## 510 3.466667    3.90       4.4 0.920 Very high human development
## 511 1.866667    2.10       3.8 0.920 Very high human development
## 512 3.733333    3.70       4.2 0.920 Very high human development
## 513 4.200000    4.20       3.6 0.920 Very high human development
## 514 2.466667    3.00       4.0 0.920 Very high human development
## 515 4.533333    4.55       2.0 0.920 Very high human development
## 516 3.200000    3.35       2.0 0.920 Very high human development
## 517 1.666667    2.35       3.6 0.920 Very high human development
## 518 2.933333    3.70       3.0 0.920 Very high human development
## 519 1.600000    1.75       3.4 0.920 Very high human development
## 520 2.800000    3.35       2.4 0.920 Very high human development
## 521 3.000000    3.40       2.0 0.920 Very high human development
## 522 2.666667    3.45       3.6 0.920 Very high human development
## 523 2.533333    3.95       3.0 0.920 Very high human development
## 524 3.466667    3.00       2.8 0.920 Very high human development
## 525 2.400000    3.15       1.6 0.920 Very high human development
## 526 1.400000    2.15       3.6 0.920 Very high human development
## 527 1.866667    1.95       1.0 0.920 Very high human development
## 528 3.866667    3.35       3.2 0.920 Very high human development
## 529 3.266667    3.05       1.6 0.920 Very high human development
## 530 2.466667    2.75       2.8 0.920 Very high human development
## 531 1.266667    1.85       3.6 0.920 Very high human development
## 532 3.800000    3.25       2.0 0.920 Very high human development
## 533 3.466667    3.55       2.2 0.920 Very high human development
## 534 2.800000    3.50       3.8 0.920 Very high human development
## 535 3.066667    3.30       2.8 0.920 Very high human development
## 536 2.200000    2.35       4.2 0.920 Very high human development
## 537 4.133333    4.10       3.2 0.920 Very high human development
## 538 3.266667    3.75       2.2 0.920 Very high human development
## 539 2.333333    3.65       3.4 0.920 Very high human development
## 540 1.800000    2.50       3.4 0.920 Very high human development
## 541 2.066667    3.15       2.6 0.920 Very high human development
## 542 1.933333    2.65       3.8 0.920 Very high human development
## 543 1.533333    2.30       2.6 0.920 Very high human development
## 544 2.000000    2.20       3.2 0.920 Very high human development
## 545 1.600000    1.85       4.0 0.920 Very high human development
## 546 1.800000    2.35       3.4 0.920 Very high human development
## 547 3.000000    3.35       3.0 0.920 Very high human development
## 548 4.400000    4.55       3.0 0.920 Very high human development
## 549 2.800000    3.15       1.6 0.920 Very high human development
## 550 2.133333    2.35       3.8 0.920 Very high human development
## 551 2.266667    2.45       4.8 0.920 Very high human development
## 552 2.466667    2.30       2.0 0.920 Very high human development
## 553 3.333333    3.30       4.0 0.920 Very high human development
## 554 5.000000    4.40       1.2 0.920 Very high human development
## 555 3.866667    3.30       3.4 0.920 Very high human development
## 556 2.866667    3.00       3.0 0.920 Very high human development
## 557 3.133333    3.30       3.2 0.920 Very high human development
## 558 4.133333    4.55       1.6 0.920 Very high human development
## 559 1.800000    1.60       3.8 0.920 Very high human development
## 560 2.066667    2.50       3.8 0.920 Very high human development
## 561 2.066667    2.05       3.6 0.920 Very high human development
## 562 2.733333    3.05       3.4 0.920 Very high human development
## 563 2.533333    2.90       4.0 0.920 Very high human development
## 564 2.066667    2.75       3.6 0.920 Very high human development
## 565 3.200000    2.50       2.2 0.920 Very high human development
## 566 1.800000    2.15       3.0 0.920 Very high human development
## 567 2.733333    3.75       2.8 0.920 Very high human development
## 568 2.266667    2.55       3.0 0.920 Very high human development
## 569 3.000000    2.70       1.6 0.920 Very high human development
## 570 2.933333    3.00       2.0 0.767      High human development
```

```r
barplot(height=table(ProcrastinationHdiData_18_or_older$Gender), xlab="Gender", ylab="Frequency",  main="Frequency of Genders")
```

![](C:\Users\Brian\Documents\GitHub\CaseStudy2-Repo\Paper\caseStudy2_files/figure-html/CaseStudy_2_6_2.R-1.png)<!-- -->

```r
barplot(height=table(ProcrastinationHdiData_18_or_older$WorkStatus), xlab="Work Status", ylab="Frequency",  main="Frequency of Work Status")
```

![](C:\Users\Brian\Documents\GitHub\CaseStudy2-Repo\Paper\caseStudy2_files/figure-html/CaseStudy_2_6_2.R-2.png)<!-- -->

```r
barplot(height=table(ProcrastinationHdiData_18_or_older$Gender), xlab="Occupations", ylab="Frequency",  main="Frequency of Occupations")
```

![](C:\Users\Brian\Documents\GitHub\CaseStudy2-Repo\Paper\caseStudy2_files/figure-html/CaseStudy_2_6_2.R-3.png)<!-- -->

```r
# d Give the counts (again, pretty table) of how many participants per country in descending order.
ProcrastinationCountryPlot <- ggplot(data=ProcrastinationHdiData_18_or_older, aes(x=reorder(Country,Country,length)))
ProcrastinationCountryPlot <- ProcrastinationCountryPlot + geom_bar(aes(y = (..count..))) + scale_y_continuous() + theme(axis.text.x = element_text(angle = 90, hjust = 1))
ProcrastinationCountryPlot <- ProcrastinationCountryPlot + xlab("Country") + ylab("Count of participants") + ggtitle("Count of participants by Country")
print(ProcrastinationCountryPlot)
```

![](C:\Users\Brian\Documents\GitHub\CaseStudy2-Repo\Paper\caseStudy2_files/figure-html/CaseStudy_2_6_2.R-4.png)<!-- -->

```r
# e There are two variables in the set: whether the person considers themselves a procrastinator (yes/no) and whether others consider them a procrastinator (yes/no). How many people matched their perceptions to others' (so, yes/yes and no/no)? To clarify: how many people said they felt they were procrastinators and also said others thought they were procrastinators? Likewise, how many said they were not procrastinators and others also did not think they were procrastinators?



yes_yes_match <- Procrastination_Raw_Data[which(ProcrastinationHdiData_18_or_older$Yourself == "yes" & ProcrastinationHdiData_18_or_older$Others == "yes"),]
no_no_match <- Procrastination_Raw_Data[which(ProcrastinationHdiData_18_or_older$Yourself == "no" & ProcrastinationHdiData_18_or_older$Others == "no"),]

#Get the number of matches from yes_yes_match
length(yes_yes_match$Yourself)
```

```
## [1] 308
```

```r
#Get the number of matches from no_no_match
length(no_no_match$Yourself)
```

```
## [1] 83
```

## Deeper Analysis and Visualization


```r
# a Note: You should make all of these appealing looking. Remember to include things like a clean, informative title, axis labels that are in plain English, and readable axis values that do not overlap.


# b Create a barchart in ggplot or similar which displays the top 15 nations in average procrastination scores, using one measure of the following: DP, AIP, or GP. The bars should be in descending order, with the number 1 most procrastinating nation at the top and 15th most procrastinating at the bottom. Omit all other nations. Color the bars by HDI category (see 3B). Use any color palette of your choice other than the default.

# 
# ProcrastinationCountryPlot <- ggplot(data=ProcrastinationHdiData_18_or_older, aes(x=reorder(Country,Country,length)))
# ProcrastinationCountryPlot <- ProcrastinationCountryPlot + geom_bar(aes(y = (..count..))) + scale_y_continuous() + theme(axis.text.x = element_text(angle = 90, hjust = 1))
# ProcrastinationCountryPlot <- ProcrastinationCountryPlot + xlab("Country") + ylab("Count of participants") + ggtitle("Count of participants by Country")
# print(ProcrastinationCountryPlot)


#Get the average DP Mean by country
CountryByDPMean <- ddply(ProcrastinationHdiData_18_or_older, c("Country"), summarise,DP_Mean = mean(DP_Mean))

#Create the order of the countries ranked by DP_Mean in a data frame and rename the column to Country
CountryByDPMeanOrdered <- CountryByDPMean$Country [order (CountryByDPMean$DP_Mean, decreasing = TRUE)]
CountryByDPMeanOrdered_df = data.frame(CountryByDPMeanOrdered)
CountryByDPMeanOrdered_df<-rename(CountryByDPMeanOrdered_df, c("CountryByDPMeanOrdered"="Country"))

#Merge the ordered data frame with the DP Mean data
CountryByDPMeanOrdered_df_merged = merge(CountryByDPMeanOrdered_df,CountryByDPMean,by.x = "Country", by.y = "Country",all.x=TRUE,sort=FALSE)
CountryByDPMeanTop15 = subset(CountryByDPMeanOrdered_df_merged, Country %in% CountryByDPMeanOrdered [1:15])

#Create an HDI Data Frame to merge with
CountryByHDICategory <- unique(ProcrastinationHdiData_18_or_older[,c('Country','Development.Category')])
CountryByDPMeanTop15Hdi <- merge(CountryByDPMeanTop15,CountryByHDICategory,by.x = "Country", by.y = "Country",all.x=TRUE,sort=FALSE)

#Plot the graph with custom colors ordering by DPMean
Custom_colors <- c("#ffb6c1", "#ffd700", "#000080", "#ff0000")
CountryByDPMeanTop15HdiPlot <- ggplot(data=CountryByDPMeanTop15Hdi, aes(x=reorder(Country, -DP_Mean), y=DP_Mean, fill=Development.Category))
CountryByDPMeanTop15HdiPlot <- CountryByDPMeanTop15HdiPlot + geom_bar(stat="identity") + theme(axis.text.x = element_text(angle = 90, hjust = 1))
CountryByDPMeanTop15HdiPlot <- CountryByDPMeanTop15HdiPlot + xlab("Country") + ylab("Average DP Score") + ggtitle("Average DP Score by Country")
CountryByDPMeanTop15HdiPlot <- CountryByDPMeanTop15HdiPlot + scale_fill_manual(values=Custom_colors)
print(CountryByDPMeanTop15HdiPlot)
```

![](C:\Users\Brian\Documents\GitHub\CaseStudy2-Repo\Paper\caseStudy2_files/figure-html/CaseStudy_2_7.R-1.png)<!-- -->

```r
# c Create another barchart identical in features to 5B, but use another one of the three variables: DP, AIP, or GP. How many nations show up both in 5B's plot and 5C's? Which, if any?
CountryByGPMean <- ddply(ProcrastinationHdiData_18_or_older, c("Country"), summarise,GP_Mean = mean(GP_Mean))

#Create the order of the countries ranked by GP_Mean in a data frame and rename the column to Country
CountryByGPMeanOrdered <- CountryByGPMean$Country [order (CountryByGPMean$GP_Mean, decreasing = TRUE)]
CountryByGPMeanOrdered_df = data.frame(CountryByGPMeanOrdered)
CountryByGPMeanOrdered_df<-rename(CountryByGPMeanOrdered_df, c("CountryByGPMeanOrdered"="Country"))

#Merge the ordered data frame with the GP Mean data
CountryByGPMeanOrdered_df_merged = merge(CountryByGPMeanOrdered_df,CountryByGPMean,by.x = "Country", by.y = "Country",all.x=TRUE,sort=FALSE)
CountryByGPMeanTop15 = subset(CountryByGPMeanOrdered_df_merged, Country %in% CountryByGPMeanOrdered [1:15])

#Create an HDI Data Frame to merge with
CountryByHDICategory <- unique(ProcrastinationHdiData_18_or_older[,c('Country','Development.Category')])
CountryByGPMeanTop15Hdi <- merge(CountryByGPMeanTop15,CountryByHDICategory,by.x = "Country", by.y = "Country",all.x=TRUE,sort=FALSE)

#Plot the graph with custom colors ordering by GPMean
Custom_colors <- c("#ffb6c1", "#ffd700", "#000080", "#ff0000")
CountryByGPMeanTop15HdiPlot <- ggplot(data=CountryByGPMeanTop15Hdi, aes(x=reorder(Country, -GP_Mean), y=GP_Mean, fill=Development.Category))
CountryByGPMeanTop15HdiPlot <- CountryByGPMeanTop15HdiPlot + geom_bar(stat="identity") + theme(axis.text.x = element_text(angle = 90, hjust = 1))
CountryByGPMeanTop15HdiPlot <- CountryByGPMeanTop15HdiPlot + xlab("Country") + ylab("Average GP Score") + ggtitle("Average GP Score by Country")
CountryByGPMeanTop15HdiPlot <- CountryByGPMeanTop15HdiPlot + scale_fill_manual(values=Custom_colors)
print(CountryByGPMeanTop15HdiPlot)
```

![](C:\Users\Brian\Documents\GitHub\CaseStudy2-Repo\Paper\caseStudy2_files/figure-html/CaseStudy_2_7.R-2.png)<!-- -->

```r
CountryByGP_DPMeanTop15Hdi <- merge(CountryByGPMeanTop15Hdi,CountryByDPMeanTop15Hdi,by.x = "Country", by.y = "Country",all.x=FALSE,all.y=FALSE,sort=FALSE)

print(CountryByGP_DPMeanTop15Hdi$Country)
```

```
##  [1] Sweden         New Zealand    Spain          China         
##  [5] Poland         Germany        Portugal       Ireland       
##  [9] Brazil         Ecuador        Jamaica        United Kingdom
## 36 Levels: Argentina Australia Bermuda Bolivia Brazil Canada ... Venezuela
```
###These 12 countries are on both the top 15 DP and top 15 GP lists


```r
# d Is there a relationship between Age and Income? Create a scatterplot and make an assessment of whether there is a relationship. Color each point based on the Gender of the participant. You're welcome to use lm() or similar functions to back up your claims.
AgeIncomePlot <- ggplot(data=ProcrastinationHdiData_18_or_older, aes(x=Age, y=Income, color=Gender))
AgeIncomePlot <- AgeIncomePlot + geom_point() + theme(axis.text.x = element_text(angle = 90, hjust = 1))
AgeIncomePlot <- AgeIncomePlot + xlab("Age") + ylab("Income") + ggtitle("Income by age")
AgeIncomePlot <- AgeIncomePlot + theme(plot.title = element_text(hjust = 0.5))

print(AgeIncomePlot)
```

```
## Warning: Removed 38 rows containing missing values (geom_point).
```

![](C:\Users\Brian\Documents\GitHub\CaseStudy2-Repo\Paper\caseStudy2_files/figure-html/unnamed-chunk-2-1.png)<!-- -->

###Given the shape of the data there appears to be a possibly parabolic relationship between age and income, with high-earners between 25-65 and low earners on both sides


```r
# e What about Life Satisfaction and HDI? Create another scatterplot. Is there a discernible relationship there? What about if you used the HDI category instead and made a barplot?
SWLSMeanHdiPlot <- ggplot(data=ProcrastinationHdiData_18_or_older, aes(x=HDI, y=SWLS_Mean))
SWLSMeanHdiPlot <- SWLSMeanHdiPlot + geom_point() + theme(axis.text.x = element_text(angle = 90, hjust = 1))
SWLSMeanHdiPlot <- SWLSMeanHdiPlot + ylab("Life Satisfaction Mean Score") + xlab("Country Human Development Index") + ggtitle("Human Development Index by Life Satisfaction")
SWLSMeanHdiPlot <- SWLSMeanHdiPlot + theme(plot.title = element_text(hjust = 0.5))

print(SWLSMeanHdiPlot)
```

```
## Warning: Removed 1 rows containing missing values (geom_point).
```

![](C:\Users\Brian\Documents\GitHub\CaseStudy2-Repo\Paper\caseStudy2_files/figure-html/unnamed-chunk-3-1.png)<!-- -->

###The Life Satisfaction Score seems to be independant of the Country's Human Development index, with a fairly even distribution of life satisfaction scores regardless of the HDI


```r
HdiCategoryBySWLSMean <- ddply(ProcrastinationHdiData_18_or_older, c("Development.Category"), summarise,SWLS_Mean = mean(SWLS_Mean))


SWLSMeanHdiCategoryPlot <- ggplot(data=HdiCategoryBySWLSMean, aes(y=SWLS_Mean, x=Development.Category))
SWLSMeanHdiCategoryPlot <- SWLSMeanHdiCategoryPlot + geom_col() + theme(axis.text.x = element_text(angle = 90, hjust = 1))
SWLSMeanHdiCategoryPlot <- SWLSMeanHdiCategoryPlot + ylab("Life Satisfaction Mean Score") + xlab("Country Human Development Category") + ggtitle("Human Development by Life Satisfaction")
SWLSMeanHdiCategoryPlot <- SWLSMeanHdiCategoryPlot + theme(plot.title = element_text(hjust = 0.5))

print(SWLSMeanHdiCategoryPlot)
```

![](C:\Users\Brian\Documents\GitHub\CaseStudy2-Repo\Paper\caseStudy2_files/figure-html/unnamed-chunk-4-1.png)<!-- -->

###Given the barchart there appears to be a slightly than higher average Life Satisfaction Score in countrie with a medium Human Development Index Category



## Outputting to CSV format - Make sure there are no index numbers


```r
# a The client would like the finalized HDI table (3A and 3B)
write.csv(hdiDataFrame_all, file = ".\\Paper\\FinalizedHdiTable.csv",row.names=FALSE)

# b The client would like the Tidied version of the original input to be output in the repository, including the merged HDI data (3C).
write.csv(ProcrastinationHdiData_18_or_older, file = ".\\Paper\\TidiedProcrastinationHdiData.csv",row.names=FALSE)

# c The client would like a dataset (or two) that shows the Top 15 nations (in 5B and 5C), as well as their HDI scores.
write.csv(CountryByDPMeanTop15Hdi, file = ".\\Paper\\Top15CountriesByDpWithHdi.csv",row.names=FALSE)
write.csv(CountryByGPMeanTop15Hdi, file = ".\\Paper\\Top15CountriesByGpWithHdi.csv",row.names=FALSE)

# d All output should be in plain English or translated in the Codebook.
```

## Conclusion

Greetings Nintendo Marketing Team,

From our analysis we provided you the 12 laziest countries:
Sweden, New Zealand, Spain, China, Poland, Germany, Portugal, Ireland, Brazil, Ecuador, Jamaica, United Kingdom

From this list, the countries with a very high Human Development index are:
Sweden, New Zealand, Spain, Poland, Germany, Portugal, Ireland, and United Kingdom

We deduce that the Very Highly Developed and very highly procrastinating humans in these countries would be ideal cadidates for Nintendo marketing. Please let us knwo if you find our services valuable and would like to invest in more information now and in the future.

Thank you,

Brian Coari, Gergory Asamoah, and Emil Ramos

LazyLife Inc.

Email: datascience@lazylife.com

Phone: (555) 867-5309


