---
title       : LondonCrime
subtitle    : An app for 'Developing Data Products' on Coursera
author      : AEKEYS
job         : Produced 2015-02-18 17:59:23
logo        : bigben.png
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [mathjax, quiz, bootstrap]            # {mathjax, quiz, bootstrap}
ext_widgets: {rCharts: [libraries/morris]}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides

--- .class #id
## Motivation

London's open data initiative makes it easy to obtain information.
But, the data are not always in formats that best address our interests.
 
* How do employment measures relate to crime in London's boroughs?
* Which boroughs have the highest crime?

<div style='text-align: center;'>
    <img src='assets/img/boroughsThumb.png' />
</div>


--- .class #id 

## Pitch
Now, with LondonCrime -- newly available on Shiny Apps -- 

**YOU** can compare crime rates with other important statistics!

<div align="center">
<a href="http://aekeys.shinyapps.io/LondonCrime">http://aekeys.shinyapps.io/LondonCrime</a>
</div>
<p></p>

<div align="center">
    <img src='assets/img/london_sky.jpg' />
</div>

---
## How it works

- LondonCrime obtains data from [http://data.london.gov.uk](http://data.london.gov.uk);  
- cleans it up using tidyr, reshape2, and dplyr;  

```r
boroughs <- melt(boroughs, id=c("Borough","InnerOuter"),
                 variable.name="type_year",
                 value.name="Value")

boroughs <- separate(boroughs, type_year, into=c("Type","Year"))

boroughs <- dcast(boroughs, Borough + InnerOuter + Year ~ Type,
                  value.var = "Value")
```
- and then generates awesome interactive charts using rCharts!  


```r
             m1 <- mPlot(x="date",y=c("Employment","Crime"),type="Line",
                         boroughs=subset(data, Borough=="Westminster"))
```


--- 

## Example Result!


 
### Crime, Youth Unemployment in Westminster
 
<iframe src="code/m1.html" width=100%, height=600></iframe>

