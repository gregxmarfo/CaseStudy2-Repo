# Case Study 2
Section 403, Group 5:  
    Gregory Asamoah  
    Emil Ramos  
    Brian Coari  
December 03, 2017  

#Install necessary packages if not installed:


```r
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
```

## Introduction

#[some text here]


##Code Book for the raw Data

#CODE BOOK

#Data Set Code Book: Procrastination
#November 25, 2017

#The Procrastination csv data set contains 4264 observations and 61 variables



```r
stringsAsFactors=FALSE

Procrastination_Raw_Data <- read.csv(".\\Data\\Procrastination.csv",header=TRUE, sep=",", fileEncoding="UTF-8-BOM")

class(Procrastination_Raw_Data)
```

```
## [1] "data.frame"
```

```r
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


## Clean your Raw Data


```r
# a Read the csv into R and take a look at the data set. Output how many rows and columns the data.frame is.

#renaming the columns

names(Procrastination_Raw_Data)[5:61] = c("WorkStatus","Income","Occupation","PositionYrs","PositionMnth","CommSize","Country","MaritalStatus","NumofSons","NumofDaughters","XDP1","XDP2","XDP3","XDP4","XDP5","XAIP1","XAIP2","XAIP3","XAIP4","XAIP5","XAIP6","XAIP7","XAIP8","XAIP9","XAIP10","XAIP11","XAIP12","XAIP13","XAIP14","XAIP15","XGP1","XGP2","XGP3","XGP4","XGP5","XGP6","XGP7","XGP8","XGP9","XGP10","XGP11","XGP12","XGP13","XGP14","XGP15","XGP16","XGP17","XGP18","XGP19","XGP20","XSWLS1","XSWLS2","XSWLS3","XSWLS4","XSWLS5","Yourself","Others")

str(Procrastination_Raw_Data)
```

```
## 'data.frame':	4264 obs. of  61 variables:
##  $ Age           : num  67.5 45 19 37.5 28 23 67.5 37.5 24 45 ...
##  $ Gender        : Factor w/ 3 levels "","Female","Male": 3 3 2 3 2 2 2 3 2 3 ...
##  $ Kids          : Factor w/ 3 levels "","No Kids","Yes Kids": 3 3 2 3 2 2 2 2 2 3 ...
##  $ Edu           : Factor w/ 9 levels "","deg","dip",..: 8 2 3 8 2 2 8 4 8 8 ...
##  $ WorkStatus    : Factor w/ 7 levels "","0","full-time",..: 5 4 6 3 3 3 4 4 3 3 ...
##  $ Income        : int  25000 35000 NA 45000 35000 15000 NA 10000 250000 87500 ...
##  $ Occupation    : Factor w/ 676 levels "","'Utterly shiftless arts student'... at p",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ PositionYrs   : num  9.0 1.5e-19 0.0 1.4e+01 1.0 ...
##  $ PositionMnth  : int  0 0 0 0 0 0 0 0 0 0 ...
##  $ CommSize      : Factor w/ 10 levels "","0","8","Large-City",..: 4 10 5 5 10 9 5 10 10 10 ...
##  $ Country       : Factor w/ 94 levels "","0","Afghanistan",..: 31 15 25 26 26 26 60 88 88 73 ...
##  $ MaritalStatus : Factor w/ 7 levels "","0","Divorced",..: 3 4 6 4 6 6 3 6 6 4 ...
##  $ NumofSons     : Factor w/ 9 levels "","0","10","3",..: 2 9 2 2 2 2 2 2 2 8 ...
##  $ NumofDaughters: int  5 1 0 1 0 0 0 0 0 0 ...
##  $ XDP1          : int  3 3 5 3 3 3 3 4 2 5 ...
##  $ XDP2          : int  1 4 5 3 3 4 4 3 2 5 ...
##  $ XDP3          : int  1 3 2 3 2 3 3 4 4 5 ...
##  $ XDP4          : int  1 3 3 3 1 2 2 4 4 5 ...
##  $ XDP5          : int  1 3 3 3 1 2 2 3 4 5 ...
##  $ XAIP1         : int  1 3 5 2 1 2 3 4 3 3 ...
##  $ XAIP2         : int  1 1 4 1 1 5 1 4 3 3 ...
##  $ XAIP3         : int  1 4 4 4 3 5 1 4 3 5 ...
##  $ XAIP4         : int  1 3 5 3 3 5 2 4 4 3 ...
##  $ XAIP5         : int  1 3 5 5 2 5 3 4 4 5 ...
##  $ XAIP6         : int  1 4 5 3 2 3 3 2 2 1 ...
##  $ XAIP7         : int  1 3 5 4 2 5 1 5 2 5 ...
##  $ XAIP8         : int  1 3 4 5 2 4 4 2 4 5 ...
##  $ XAIP9         : int  5 3 5 4 1 4 5 4 2 5 ...
##  $ XAIP10        : int  1 3 5 5 1 5 5 3 2 5 ...
##  $ XAIP11        : int  1 4 4 4 2 3 3 2 4 4 ...
##  $ XAIP12        : int  1 2 3 3 1 5 2 4 4 4 ...
##  $ XAIP13        : int  1 2 5 4 2 4 3 3 4 4 ...
##  $ XAIP14        : int  1 2 4 2 1 5 1 4 3 4 ...
##  $ XAIP15        : int  3 4 3 1 2 5 4 5 3 5 ...
##  $ XGP1          : int  1 4 5 4 4 5 4 5 3 5 ...
##  $ XGP2          : int  1 2 2 1 1 5 1 1 4 3 ...
##  $ XGP3          : int  1 2 2 3 2 2 1 3 3 3 ...
##  $ XGP4          : int  1 2 4 3 4 5 1 4 4 1 ...
##  $ XGP5          : int  1 2 3 2 5 4 1 3 2 5 ...
##  $ XGP6          : int  1 2 1 3 2 4 2 3 2 5 ...
##  $ XGP7          : int  1 4 3 4 4 5 3 4 4 5 ...
##  $ XGP8          : int  1 2 2 5 2 4 2 3 2 4 ...
##  $ XGP9          : int  1 4 5 4 4 4 4 4 4 5 ...
##  $ XGP10         : int  1 2 4 1 1 3 1 4 1 3 ...
##  $ XGP11         : int  5 3 5 3 2 4 4 3 5 5 ...
##  $ XGP12         : int  1 4 5 4 3 4 2 5 2 5 ...
##  $ XGP13         : int  1 2 3 3 2 3 3 2 3 4 ...
##  $ XGP14         : int  1 2 4 3 4 4 2 2 2 4 ...
##  $ XGP15         : int  1 3 5 4 3 4 4 4 1 4 ...
##  $ XGP16         : int  1 4 2 4 2 4 3 4 5 5 ...
##  $ XGP17         : int  1 3 3 3 3 4 1 3 5 3 ...
##  $ XGP18         : int  5 3 5 4 2 4 4 4 1 5 ...
##  $ XGP19         : int  1 4 5 5 3 4 4 4 1 5 ...
##  $ XGP20         : int  5 4 4 1 4 4 2 4 3 5 ...
##  $ XSWLS1        : int  5 3 2 2 4 3 3 3 4 1 ...
##  $ XSWLS2        : int  5 4 2 4 4 2 4 3 4 4 ...
##  $ XSWLS3        : int  5 4 2 2 4 4 3 3 5 2 ...
##  $ XSWLS4        : int  5 4 3 2 3 4 3 2 4 4 ...
##  $ XSWLS5        : int  5 3 4 2 4 3 2 3 4 1 ...
##  $ Yourself      : Factor w/ 3 levels "","no","yes": 2 3 3 3 2 3 3 3 2 3 ...
##  $ Others        : Factor w/ 5 levels "","0","4","no",..: 4 5 5 5 4 5 5 5 4 5 ...
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
##  [1] "Age"            "Gender"         "Kids"           "Edu"           
##  [5] "WorkStatus"     "Income"         "Occupation"     "PositionYrs"   
##  [9] "PositionMnth"   "CommSize"       "Country"        "MaritalStatus" 
## [13] "NumofSons"      "NumofDaughters" "XDP1"           "XDP2"          
## [17] "XDP3"           "XDP4"           "XDP5"           "XAIP1"         
## [21] "XAIP2"          "XAIP3"          "XAIP4"          "XAIP5"         
## [25] "XAIP6"          "XAIP7"          "XAIP8"          "XAIP9"         
## [29] "XAIP10"         "XAIP11"         "XAIP12"         "XAIP13"        
## [33] "XAIP14"         "XAIP15"         "XGP1"           "XGP2"          
## [37] "XGP3"           "XGP4"           "XGP5"           "XGP6"          
## [41] "XGP7"           "XGP8"           "XGP9"           "XGP10"         
## [45] "XGP11"          "XGP12"          "XGP13"          "XGP14"         
## [49] "XGP15"          "XGP16"          "XGP17"          "XGP18"         
## [53] "XGP19"          "XGP20"          "XSWLS1"         "XSWLS2"        
## [57] "XSWLS3"         "XSWLS4"         "XSWLS5"         "Yourself"      
## [61] "Others"
```

```r
#structure of the data
glimpse(Procrastination_Raw_Data)
```

```
## Observations: 4,264
## Variables: 61
## $ Age            <dbl> 67.5, 45.0, 19.0, 37.5, 28.0, 23.0, 67.5, 37.5,...
## $ Gender         <fctr> Male, Male, Female, Male, Female, Female, Fema...
## $ Kids           <fctr> Yes Kids, Yes Kids, No Kids, Yes Kids, No Kids...
## $ Edu            <fctr> ma, deg, dip, ma, deg, deg, ma, grade, ma, ma,...
## $ WorkStatus     <fctr> retired, part-time, student, full-time, full-t...
## $ Income         <int> 25000, 35000, NA, 45000, 35000, 15000, NA, 1000...
## $ Occupation     <fctr> , , , , , , , , , , , , , , , , , , , , , , , , 
## $ PositionYrs    <dbl> 9.0e+00, 1.5e-19, 0.0e+00, 1.4e+01, 1.0e+00, 1....
## $ PositionMnth   <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 3, 0, 0,...
## $ CommSize       <fctr> Large-City, Village, Large Town, Large Town, V...
## $ Country        <fctr> El Salvador, Bolivia, Cyprus, Czech Republic, ...
## $ MaritalStatus  <fctr> Divorced, Married, Single, Married, Single, Si...
## $ NumofSons      <fctr> 0, Male, 0, 0, 0, 0, 0, 0, 0, Female, Female, ...
## $ NumofDaughters <int> 5, 1, 0, 1, 0, 0, 0, 0, 0, 0, 0, 2, 0, 0, 1, 0,...
## $ XDP1           <int> 3, 3, 5, 3, 3, 3, 3, 4, 2, 5, 3, 3, 5, 5, 2, 4,...
## $ XDP2           <int> 1, 4, 5, 3, 3, 4, 4, 3, 2, 5, 3, 3, 5, 4, 2, 4,...
## $ XDP3           <int> 1, 3, 2, 3, 2, 3, 3, 4, 4, 5, 3, 4, 5, 5, 1, 3,...
## $ XDP4           <int> 1, 3, 3, 3, 1, 2, 2, 4, 4, 5, 3, 2, 4, 4, 1, 3,...
## $ XDP5           <int> 1, 3, 3, 3, 1, 2, 2, 3, 4, 5, 3, 2, 4, 4, 1, 3,...
## $ XAIP1          <int> 1, 3, 5, 2, 1, 2, 3, 4, 3, 3, 3, 4, 1, 2, 2, 2,...
## $ XAIP2          <int> 1, 1, 4, 1, 1, 5, 1, 4, 3, 3, 3, 3, 1, 4, 2, 1,...
## $ XAIP3          <int> 1, 4, 4, 4, 3, 5, 1, 4, 3, 5, 3, 2, 4, 3, 3, 1,...
## $ XAIP4          <int> 1, 3, 5, 3, 3, 5, 2, 4, 4, 3, 3, 4, 1, 5, 2, 3,...
## $ XAIP5          <int> 1, 3, 5, 5, 2, 5, 3, 4, 4, 5, 3, 4, 2, 4, 1, 2,...
## $ XAIP6          <int> 1, 4, 5, 3, 2, 3, 3, 2, 2, 1, 3, 4, 5, 5, 2, 3,...
## $ XAIP7          <int> 1, 3, 5, 4, 2, 5, 1, 5, 2, 5, 3, 4, 5, 4, 2, 2,...
## $ XAIP8          <int> 1, 3, 4, 5, 2, 4, 4, 2, 4, 5, 3, 2, 4, 3, 3, 4,...
## $ XAIP9          <int> 5, 3, 5, 4, 1, 4, 5, 4, 2, 5, 3, 4, 4, 4, 2, 1,...
## $ XAIP10         <int> 1, 3, 5, 5, 1, 5, 5, 3, 2, 5, 3, 4, 5, 4, 2, 4,...
## $ XAIP11         <int> 1, 4, 4, 4, 2, 3, 3, 2, 4, 4, 3, 1, 4, 5, 4, 4,...
## $ XAIP12         <int> 1, 2, 3, 3, 1, 5, 2, 4, 4, 4, 3, 2, 3, 3, 3, 2,...
## $ XAIP13         <int> 1, 2, 5, 4, 2, 4, 3, 3, 4, 4, 3, 4, 1, 5, 3, 3,...
## $ XAIP14         <int> 1, 2, 4, 2, 1, 5, 1, 4, 3, 4, 3, 4, 1, 4, 2, 2,...
## $ XAIP15         <int> 3, 4, 3, 1, 2, 5, 4, 5, 3, 5, 3, 4, 5, 4, 2, 2,...
## $ XGP1           <int> 1, 4, 5, 4, 4, 5, 4, 5, 3, 5, 2, 3, 4, 4, 2, 4,...
## $ XGP2           <int> 1, 2, 2, 1, 1, 5, 1, 1, 4, 3, 2, 4, 3, 3, 2, 3,...
## $ XGP3           <int> 1, 2, 2, 3, 2, 2, 1, 3, 3, 3, 4, 2, 4, 4, 3, 1,...
## $ XGP4           <int> 1, 2, 4, 3, 4, 5, 1, 4, 4, 1, 4, 2, 4, 4, 3, 4,...
## $ XGP5           <int> 1, 2, 3, 2, 5, 4, 1, 3, 2, 5, 2, 4, 1, 3, 2, 3,...
## $ XGP6           <int> 1, 2, 1, 3, 2, 4, 2, 3, 2, 5, 4, 2, 4, 3, 3, 2,...
## $ XGP7           <int> 1, 4, 3, 4, 4, 5, 3, 4, 4, 5, 2, 3, 3, 3, 2, 4,...
## $ XGP8           <int> 1, 2, 2, 5, 2, 4, 2, 3, 2, 4, 4, 3, 5, 5, 3, 3,...
## $ XGP9           <int> 1, 4, 5, 4, 4, 4, 4, 4, 4, 5, 2, 4, 2, 4, 2, 4,...
## $ XGP10          <int> 1, 2, 4, 1, 1, 3, 1, 4, 1, 3, 2, 2, 1, 5, 1, 3,...
## $ XGP11          <int> 5, 3, 5, 3, 2, 4, 4, 3, 5, 5, 3, 2, 2, 4, 5, 3,...
## $ XGP12          <int> 1, 4, 5, 4, 3, 4, 2, 5, 2, 5, 3, 4, 4, 4, 2, 4,...
## $ XGP13          <int> 1, 2, 3, 3, 2, 3, 3, 2, 3, 4, 4, 4, 3, 3, 2, 2,...
## $ XGP14          <int> 1, 2, 4, 3, 4, 4, 2, 2, 2, 4, 4, 4, 2, 3, 2, 2,...
## $ XGP15          <int> 1, 3, 5, 4, 3, 4, 4, 4, 1, 4, 4, 4, 4, 4, 3, 3,...
## $ XGP16          <int> 1, 4, 2, 4, 2, 4, 3, 4, 5, 5, 2, 4, 5, 3, 2, 3,...
## $ XGP17          <int> 1, 3, 3, 3, 3, 4, 1, 3, 5, 3, 2, 4, 5, 4, 2, 3,...
## $ XGP18          <int> 5, 3, 5, 4, 2, 4, 4, 4, 1, 5, 4, 4, 4, 4, 3, 3,...
## $ XGP19          <int> 1, 4, 5, 5, 3, 4, 4, 4, 1, 5, 2, 4, 5, 3, 2, 4,...
## $ XGP20          <int> 5, 4, 4, 1, 4, 4, 2, 4, 3, 5, 4, 4, 4, 3, 3, 1,...
## $ XSWLS1         <int> 5, 3, 2, 2, 4, 3, 3, 3, 4, 1, 2, 4, 5, 3, 2, 1,...
## $ XSWLS2         <int> 5, 4, 2, 4, 4, 2, 4, 3, 4, 4, 2, 4, 5, 3, 1, 3,...
## $ XSWLS3         <int> 5, 4, 2, 2, 4, 4, 3, 3, 5, 2, 2, 4, 4, 4, 3, 2,...
## $ XSWLS4         <int> 5, 4, 3, 2, 3, 4, 3, 2, 4, 4, 2, 4, 5, 2, 2, 3,...
## $ XSWLS5         <int> 5, 3, 4, 2, 4, 3, 2, 3, 4, 1, 2, 4, 5, 2, 1, 2,...
## $ Yourself       <fctr> no, yes, yes, yes, no, yes, yes, yes, no, yes,...
## $ Others         <fctr> no, yes, yes, yes, no, yes, yes, yes, no, yes,...
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
##       WorkStatus       Income                   Occupation  
##            : 111   Min.   :     0                    :2162  
##  0         :   2   1st Qu.: 15000   0                : 488  
##  full-time :2266   Median : 45000   please specify   : 217  
##  part-time : 477   Mean   : 58916    teacher         :  74  
##  retired   : 175   3rd Qu.: 67500   college professor:  43  
##  student   : 971   Max.   :250000   engineer         :  32  
##  unemployed: 262   NA's   :548      (Other)          :1248  
##   PositionYrs      PositionMnth            CommSize  
##  Min.   :  0.00   Min.   : 0.000   Large-City  :876  
##  1st Qu.:  0.00   1st Qu.: 0.000   Village     :830  
##  Median :  2.00   Median : 0.000   Medium-Sized:669  
##  Mean   : 14.15   Mean   : 1.793   Small Town  :655  
##  3rd Qu.:  6.00   3rd Qu.: 3.000   Large Town  :466  
##  Max.   :999.00   Max.   :11.000   Small City  :311  
##  NA's   :94       NA's   :6        (Other)     :457  
##            Country       MaritalStatus    NumofSons    NumofDaughters   
##  United States :2893            : 174   0      :3272   Min.   : 0.0000  
##  Canada        : 250   0        :   6   Male   : 613   1st Qu.: 0.0000  
##  0             : 233   Divorced : 367   Female : 274   Median : 0.0000  
##  United Kingdom: 184   Married  :1599   3      :  69   Mean   : 0.3538  
##  Australia     : 104   Separated:  88   4      :  23   3rd Qu.: 0.0000  
##  India         :  78   Single   :1963   5      :   7   Max.   :10.0000  
##  (Other)       : 522   Widowed  :  67   (Other):   6   NA's   :4        
##       XDP1            XDP2            XDP3            XDP4      
##  Min.   :1.000   Min.   :1.000   Min.   :1.000   Min.   :1.000  
##  1st Qu.:3.000   1st Qu.:3.000   1st Qu.:2.000   1st Qu.:2.000  
##  Median :3.000   Median :3.000   Median :3.000   Median :3.000  
##  Mean   :3.392   Mean   :3.354   Mean   :3.198   Mean   :2.688  
##  3rd Qu.:4.000   3rd Qu.:4.000   3rd Qu.:4.000   3rd Qu.:3.000  
##  Max.   :5.000   Max.   :5.000   Max.   :5.000   Max.   :5.000  
##                                                                 
##       XDP5           XAIP1           XAIP2           XAIP3      
##  Min.   :1.000   Min.   :1.000   Min.   :1.000   Min.   :1.000  
##  1st Qu.:2.000   1st Qu.:1.000   1st Qu.:1.000   1st Qu.:2.000  
##  Median :3.000   Median :2.000   Median :2.000   Median :3.000  
##  Mean   :2.678   Mean   :2.054   Mean   :2.161   Mean   :3.371  
##  3rd Qu.:3.000   3rd Qu.:3.000   3rd Qu.:3.000   3rd Qu.:5.000  
##  Max.   :5.000   Max.   :5.000   Max.   :5.000   Max.   :5.000  
##                                                                 
##      XAIP4           XAIP5           XAIP6           XAIP7      
##  Min.   :1.000   Min.   :1.000   Min.   :1.000   Min.   :1.000  
##  1st Qu.:2.000   1st Qu.:2.000   1st Qu.:2.000   1st Qu.:2.000  
##  Median :3.000   Median :3.000   Median :3.000   Median :3.000  
##  Mean   :3.206   Mean   :3.068   Mean   :2.843   Mean   :3.218  
##  3rd Qu.:4.000   3rd Qu.:4.000   3rd Qu.:4.000   3rd Qu.:4.000  
##  Max.   :5.000   Max.   :5.000   Max.   :5.000   Max.   :5.000  
##                                                                 
##      XAIP8           XAIP9           XAIP10          XAIP11     
##  Min.   :1.000   Min.   :1.000   Min.   :1.000   Min.   :1.000  
##  1st Qu.:3.000   1st Qu.:2.000   1st Qu.:3.000   1st Qu.:2.000  
##  Median :3.000   Median :3.000   Median :4.000   Median :3.000  
##  Mean   :3.421   Mean   :2.757   Mean   :3.468   Mean   :3.045  
##  3rd Qu.:4.000   3rd Qu.:4.000   3rd Qu.:4.000   3rd Qu.:4.000  
##  Max.   :5.000   Max.   :5.000   Max.   :5.000   Max.   :5.000  
##                                                                 
##      XAIP12          XAIP13          XAIP14          XAIP15     
##  Min.   :1.000   Min.   :1.000   Min.   :1.000   Min.   :1.000  
##  1st Qu.:2.000   1st Qu.:2.000   1st Qu.:2.000   1st Qu.:2.000  
##  Median :3.000   Median :3.000   Median :2.000   Median :3.000  
##  Mean   :2.981   Mean   :3.118   Mean   :2.658   Mean   :3.193  
##  3rd Qu.:4.000   3rd Qu.:4.000   3rd Qu.:4.000   3rd Qu.:4.000  
##  Max.   :5.000   Max.   :5.000   Max.   :5.000   Max.   :5.000  
##                                                                 
##       XGP1            XGP2            XGP3            XGP4      
##  Min.   :1.000   Min.   :1.000   Min.   :1.000   Min.   :1.000  
##  1st Qu.:3.000   1st Qu.:1.000   1st Qu.:2.000   1st Qu.:2.000  
##  Median :4.000   Median :2.000   Median :3.000   Median :3.000  
##  Mean   :3.671   Mean   :2.307   Mean   :2.774   Mean   :3.321  
##  3rd Qu.:5.000   3rd Qu.:3.000   3rd Qu.:4.000   3rd Qu.:5.000  
##  Max.   :5.000   Max.   :5.000   Max.   :5.000   Max.   :5.000  
##                                                                 
##       XGP5            XGP6            XGP7            XGP8     
##  Min.   :1.000   Min.   :1.000   Min.   :1.000   Min.   :1.00  
##  1st Qu.:2.000   1st Qu.:2.000   1st Qu.:3.000   1st Qu.:3.00  
##  Median :3.000   Median :3.000   Median :3.000   Median :3.00  
##  Mean   :3.022   Mean   :2.802   Mean   :3.382   Mean   :3.27  
##  3rd Qu.:4.000   3rd Qu.:4.000   3rd Qu.:4.000   3rd Qu.:4.00  
##  Max.   :5.000   Max.   :5.000   Max.   :5.000   Max.   :5.00  
##                                                                
##       XGP9           XGP10         XGP11           XGP12      
##  Min.   :1.000   Min.   :1.0   Min.   :1.000   Min.   :1.000  
##  1st Qu.:3.000   1st Qu.:2.0   1st Qu.:2.000   1st Qu.:3.000  
##  Median :4.000   Median :3.0   Median :3.000   Median :4.000  
##  Mean   :3.749   Mean   :2.7   Mean   :3.257   Mean   :3.682  
##  3rd Qu.:5.000   3rd Qu.:4.0   3rd Qu.:4.000   3rd Qu.:4.000  
##  Max.   :5.000   Max.   :5.0   Max.   :5.000   Max.   :5.000  
##                                                               
##      XGP13           XGP14           XGP15           XGP16      
##  Min.   :1.000   Min.   :1.000   Min.   :1.000   Min.   :1.000  
##  1st Qu.:2.000   1st Qu.:2.000   1st Qu.:3.000   1st Qu.:3.000  
##  Median :3.000   Median :3.000   Median :4.000   Median :4.000  
##  Mean   :2.687   Mean   :3.095   Mean   :3.567   Mean   :3.663  
##  3rd Qu.:4.000   3rd Qu.:4.000   3rd Qu.:4.000   3rd Qu.:5.000  
##  Max.   :5.000   Max.   :5.000   Max.   :5.000   Max.   :5.000  
##                                                                 
##      XGP17           XGP18           XGP19           XGP20      
##  Min.   :1.000   Min.   :1.000   Min.   :1.000   Min.   :1.000  
##  1st Qu.:2.000   1st Qu.:3.000   1st Qu.:3.000   1st Qu.:3.000  
##  Median :3.000   Median :4.000   Median :4.000   Median :4.000  
##  Mean   :3.178   Mean   :3.634   Mean   :3.589   Mean   :3.531  
##  3rd Qu.:4.000   3rd Qu.:4.000   3rd Qu.:5.000   3rd Qu.:4.000  
##  Max.   :5.000   Max.   :5.000   Max.   :5.000   Max.   :5.000  
##                                                                 
##      XSWLS1          XSWLS2          XSWLS3         XSWLS4     
##  Min.   :1.000   Min.   :1.000   Min.   :1.00   Min.   :1.000  
##  1st Qu.:2.000   1st Qu.:3.000   1st Qu.:2.00   1st Qu.:2.000  
##  Median :3.000   Median :3.000   Median :3.00   Median :3.000  
##  Mean   :2.943   Mean   :3.199   Mean   :3.11   Mean   :3.244  
##  3rd Qu.:4.000   3rd Qu.:4.000   3rd Qu.:4.00   3rd Qu.:4.000  
##  Max.   :5.000   Max.   :5.000   Max.   :5.00   Max.   :5.000  
##                                                                
##      XSWLS5      Yourself   Others    
##  Min.   :1.000      :  14      :  42  
##  1st Qu.:2.000   no : 565   0  :   1  
##  Median :3.000   yes:3685   4  :   8  
##  Mean   :2.689              no :1652  
##  3rd Qu.:4.000              yes:2561  
##  Max.   :5.000                        
## 
```

```r
# b The column names are either too much or not enough. Change the column names so that they do not have spaces, underscores, slashes, and the like. All column names should be under 12 characters. Make sure you're updating your codebook with information on the tidied data set as well.

#renaming the columns

names(Procrastination_Raw_Data)[5:61] = c("WorkStatus","Income","Occupation","PositionYrs","PositionMnth","CommSize","Country","MaritalStatus","NumofSons","NumofDaughters","XDP1","XDP2","XDP3","XDP4","XDP5","XAIP1","XAIP2","XAIP3","XAIP4","XAIP5","XAIP6","XAIP7","XAIP8","XAIP9","XAIP10","XAIP11","XAIP12","XAIP13","XAIP14","XAIP15","XGP1","XGP2","XGP3","XGP4","XGP5","XGP6","XGP7","XGP8","XGP9","XGP10","XGP11","XGP12","XGP13","XGP14","XGP15","XGP16","XGP17","XGP18","XGP19","XGP20","XSWLS1","XSWLS2","XSWLS3","XSWLS4","XSWLS5","Yourself","Others")


# c Some columns are, due to Qualtrics, malfunctioning. Prime examples are the following columns: "How long have you held this position?: Years", Country of residence, Number of sons, and Current Occupation.

# i Some have impossible data values. Detail what you are doing to fix these columns in the raw data and why. It's a judgment call for each, but explain why. For example, most people have not been doing anything for over 100 years. For the "Years" columns, round to the nearest integer.

#Note that the data frame has 61 columns and 4264 rows and some of the columns have Null values and impossible data values. E.g People doing nothing over 100 years might be dead and must be removed from the dataset

glimpse(Procrastination_Raw_Data)
```

```
## Observations: 4,264
## Variables: 61
## $ Age            <dbl> 67.5, 45.0, 19.0, 37.5, 28.0, 23.0, 67.5, 37.5,...
## $ Gender         <fctr> Male, Male, Female, Male, Female, Female, Fema...
## $ Kids           <fctr> Yes Kids, Yes Kids, No Kids, Yes Kids, No Kids...
## $ Edu            <fctr> ma, deg, dip, ma, deg, deg, ma, grade, ma, ma,...
## $ WorkStatus     <fctr> retired, part-time, student, full-time, full-t...
## $ Income         <int> 25000, 35000, NA, 45000, 35000, 15000, NA, 1000...
## $ Occupation     <fctr> , , , , , , , , , , , , , , , , , , , , , , , , 
## $ PositionYrs    <dbl> 9.0e+00, 1.5e-19, 0.0e+00, 1.4e+01, 1.0e+00, 1....
## $ PositionMnth   <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 3, 0, 0,...
## $ CommSize       <fctr> Large-City, Village, Large Town, Large Town, V...
## $ Country        <fctr> El Salvador, Bolivia, Cyprus, Czech Republic, ...
## $ MaritalStatus  <fctr> Divorced, Married, Single, Married, Single, Si...
## $ NumofSons      <fctr> 0, Male, 0, 0, 0, 0, 0, 0, 0, Female, Female, ...
## $ NumofDaughters <int> 5, 1, 0, 1, 0, 0, 0, 0, 0, 0, 0, 2, 0, 0, 1, 0,...
## $ XDP1           <int> 3, 3, 5, 3, 3, 3, 3, 4, 2, 5, 3, 3, 5, 5, 2, 4,...
## $ XDP2           <int> 1, 4, 5, 3, 3, 4, 4, 3, 2, 5, 3, 3, 5, 4, 2, 4,...
## $ XDP3           <int> 1, 3, 2, 3, 2, 3, 3, 4, 4, 5, 3, 4, 5, 5, 1, 3,...
## $ XDP4           <int> 1, 3, 3, 3, 1, 2, 2, 4, 4, 5, 3, 2, 4, 4, 1, 3,...
## $ XDP5           <int> 1, 3, 3, 3, 1, 2, 2, 3, 4, 5, 3, 2, 4, 4, 1, 3,...
## $ XAIP1          <int> 1, 3, 5, 2, 1, 2, 3, 4, 3, 3, 3, 4, 1, 2, 2, 2,...
## $ XAIP2          <int> 1, 1, 4, 1, 1, 5, 1, 4, 3, 3, 3, 3, 1, 4, 2, 1,...
## $ XAIP3          <int> 1, 4, 4, 4, 3, 5, 1, 4, 3, 5, 3, 2, 4, 3, 3, 1,...
## $ XAIP4          <int> 1, 3, 5, 3, 3, 5, 2, 4, 4, 3, 3, 4, 1, 5, 2, 3,...
## $ XAIP5          <int> 1, 3, 5, 5, 2, 5, 3, 4, 4, 5, 3, 4, 2, 4, 1, 2,...
## $ XAIP6          <int> 1, 4, 5, 3, 2, 3, 3, 2, 2, 1, 3, 4, 5, 5, 2, 3,...
## $ XAIP7          <int> 1, 3, 5, 4, 2, 5, 1, 5, 2, 5, 3, 4, 5, 4, 2, 2,...
## $ XAIP8          <int> 1, 3, 4, 5, 2, 4, 4, 2, 4, 5, 3, 2, 4, 3, 3, 4,...
## $ XAIP9          <int> 5, 3, 5, 4, 1, 4, 5, 4, 2, 5, 3, 4, 4, 4, 2, 1,...
## $ XAIP10         <int> 1, 3, 5, 5, 1, 5, 5, 3, 2, 5, 3, 4, 5, 4, 2, 4,...
## $ XAIP11         <int> 1, 4, 4, 4, 2, 3, 3, 2, 4, 4, 3, 1, 4, 5, 4, 4,...
## $ XAIP12         <int> 1, 2, 3, 3, 1, 5, 2, 4, 4, 4, 3, 2, 3, 3, 3, 2,...
## $ XAIP13         <int> 1, 2, 5, 4, 2, 4, 3, 3, 4, 4, 3, 4, 1, 5, 3, 3,...
## $ XAIP14         <int> 1, 2, 4, 2, 1, 5, 1, 4, 3, 4, 3, 4, 1, 4, 2, 2,...
## $ XAIP15         <int> 3, 4, 3, 1, 2, 5, 4, 5, 3, 5, 3, 4, 5, 4, 2, 2,...
## $ XGP1           <int> 1, 4, 5, 4, 4, 5, 4, 5, 3, 5, 2, 3, 4, 4, 2, 4,...
## $ XGP2           <int> 1, 2, 2, 1, 1, 5, 1, 1, 4, 3, 2, 4, 3, 3, 2, 3,...
## $ XGP3           <int> 1, 2, 2, 3, 2, 2, 1, 3, 3, 3, 4, 2, 4, 4, 3, 1,...
## $ XGP4           <int> 1, 2, 4, 3, 4, 5, 1, 4, 4, 1, 4, 2, 4, 4, 3, 4,...
## $ XGP5           <int> 1, 2, 3, 2, 5, 4, 1, 3, 2, 5, 2, 4, 1, 3, 2, 3,...
## $ XGP6           <int> 1, 2, 1, 3, 2, 4, 2, 3, 2, 5, 4, 2, 4, 3, 3, 2,...
## $ XGP7           <int> 1, 4, 3, 4, 4, 5, 3, 4, 4, 5, 2, 3, 3, 3, 2, 4,...
## $ XGP8           <int> 1, 2, 2, 5, 2, 4, 2, 3, 2, 4, 4, 3, 5, 5, 3, 3,...
## $ XGP9           <int> 1, 4, 5, 4, 4, 4, 4, 4, 4, 5, 2, 4, 2, 4, 2, 4,...
## $ XGP10          <int> 1, 2, 4, 1, 1, 3, 1, 4, 1, 3, 2, 2, 1, 5, 1, 3,...
## $ XGP11          <int> 5, 3, 5, 3, 2, 4, 4, 3, 5, 5, 3, 2, 2, 4, 5, 3,...
## $ XGP12          <int> 1, 4, 5, 4, 3, 4, 2, 5, 2, 5, 3, 4, 4, 4, 2, 4,...
## $ XGP13          <int> 1, 2, 3, 3, 2, 3, 3, 2, 3, 4, 4, 4, 3, 3, 2, 2,...
## $ XGP14          <int> 1, 2, 4, 3, 4, 4, 2, 2, 2, 4, 4, 4, 2, 3, 2, 2,...
## $ XGP15          <int> 1, 3, 5, 4, 3, 4, 4, 4, 1, 4, 4, 4, 4, 4, 3, 3,...
## $ XGP16          <int> 1, 4, 2, 4, 2, 4, 3, 4, 5, 5, 2, 4, 5, 3, 2, 3,...
## $ XGP17          <int> 1, 3, 3, 3, 3, 4, 1, 3, 5, 3, 2, 4, 5, 4, 2, 3,...
## $ XGP18          <int> 5, 3, 5, 4, 2, 4, 4, 4, 1, 5, 4, 4, 4, 4, 3, 3,...
## $ XGP19          <int> 1, 4, 5, 5, 3, 4, 4, 4, 1, 5, 2, 4, 5, 3, 2, 4,...
## $ XGP20          <int> 5, 4, 4, 1, 4, 4, 2, 4, 3, 5, 4, 4, 4, 3, 3, 1,...
## $ XSWLS1         <int> 5, 3, 2, 2, 4, 3, 3, 3, 4, 1, 2, 4, 5, 3, 2, 1,...
## $ XSWLS2         <int> 5, 4, 2, 4, 4, 2, 4, 3, 4, 4, 2, 4, 5, 3, 1, 3,...
## $ XSWLS3         <int> 5, 4, 2, 2, 4, 4, 3, 3, 5, 2, 2, 4, 4, 4, 3, 2,...
## $ XSWLS4         <int> 5, 4, 3, 2, 3, 4, 3, 2, 4, 4, 2, 4, 5, 2, 2, 3,...
## $ XSWLS5         <int> 5, 3, 4, 2, 4, 3, 2, 3, 4, 1, 2, 4, 5, 2, 1, 2,...
## $ Yourself       <fctr> no, yes, yes, yes, no, yes, yes, yes, no, yes,...
## $ Others         <fctr> no, yes, yes, yes, no, yes, yes, yes, no, yes,...
```

```r
#Identify which variables are NA
all_na = sapply(Procrastination_Raw_Data, function(x)all(is.na(x)))
summary(all_na)
```

```
##    Mode   FALSE 
## logical      61
```

```r
NA_Sub=Procrastination_Raw_Data[!all_na]

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
#Create a simple histogram for two of these seven variables. Comment on the shape of the distribution in your markdown.
#summary(ProcrastinationHdiData_18_or_older$DP_Mean)
#summary(ProcrastinationHdiData_18_or_older$AIC_Mean)
#summary(ProcrastinationHdiData_18_or_older$GP_Mean)
#summary(ProcrastinationHdiData_18_or_older$SWLS_Mean)

#separate the summary from its class structure to be stored in a data frame 
dfAgeSummary<- data.frame(unclass(summary(ProcrastinationHdiData_18_or_older$Age)), check.names = FALSE)
dfIncomeSummary<- data.frame(unclass(summary(ProcrastinationHdiData_18_or_older$Income)), check.names = FALSE)
dfHDISummary<- data.frame(unclass(summary(ProcrastinationHdiData_18_or_older$HDI)), check.names = FALSE)

#Transpose to get the identifiers into columns
dfAgeSummaryT <- data.frame(round(t(dfAgeSummary),2))
dfIncomeSummaryT <- data.frame(round(t(dfIncomeSummary),2))
dfHDISummaryT <- data.frame(round(t(dfHDISummary),2))


#print the datatables in a pretty-fied format
datatable(dfAgeSummaryT, rownames = FALSE,
          caption = 'Summary of Age Statistics')
```

<!--html_preserve--><div id="htmlwidget-1ef46c0ba78f34569a60" style="width:100%;height:auto;" class="datatables html-widget"></div>
<script type="application/json" data-for="htmlwidget-1ef46c0ba78f34569a60">{"x":{"filter":"none","caption":"<caption>Summary of Age Statistics<\/caption>","data":[[19],[28],[37.5],[38.34],[45],[80]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th>Min.<\/th>\n      <th>X1st.Qu.<\/th>\n      <th>Median<\/th>\n      <th>Mean<\/th>\n      <th>X3rd.Qu.<\/th>\n      <th>Max.<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"columnDefs":[{"className":"dt-right","targets":[0,1,2,3,4,5]}],"order":[],"autoWidth":false,"orderClasses":false}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

```r
datatable(dfIncomeSummaryT, rownames = FALSE,
          caption = 'Summary of Income Statistics')
```

<!--html_preserve--><div id="htmlwidget-60d56398dc07891bb6c3" style="width:100%;height:auto;" class="datatables html-widget"></div>
<script type="application/json" data-for="htmlwidget-60d56398dc07891bb6c3">{"x":{"filter":"none","caption":"<caption>Summary of Income Statistics<\/caption>","data":[[10000],[15000],[45000],[59680.05],[67500],[250000],[352]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th>Min.<\/th>\n      <th>X1st.Qu.<\/th>\n      <th>Median<\/th>\n      <th>Mean<\/th>\n      <th>X3rd.Qu.<\/th>\n      <th>Max.<\/th>\n      <th>NA.s<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"columnDefs":[{"className":"dt-right","targets":[0,1,2,3,4,5,6]}],"order":[],"autoWidth":false,"orderClasses":false}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

```r
datatable(dfHDISummaryT, rownames = FALSE,
          caption = 'Summary of HDI Statistics')
```

<!--html_preserve--><div id="htmlwidget-7f2a0d0ef111c6333e07" style="width:100%;height:auto;" class="datatables html-widget"></div>
<script type="application/json" data-for="htmlwidget-7f2a0d0ef111c6333e07">{"x":{"filter":"none","caption":"<caption>Summary of HDI Statistics<\/caption>","data":[[0.48],[0.92],[0.92],[0.91],[0.92],[0.95],[31]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th>Min.<\/th>\n      <th>X1st.Qu.<\/th>\n      <th>Median<\/th>\n      <th>Mean<\/th>\n      <th>X3rd.Qu.<\/th>\n      <th>Max.<\/th>\n      <th>NA.s<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"columnDefs":[{"className":"dt-right","targets":[0,1,2,3,4,5,6]}],"order":[],"autoWidth":false,"orderClasses":false}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

```r
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
