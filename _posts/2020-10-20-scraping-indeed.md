---
title: "Indeed Scraping"
categories:
  - projects
tags:
  - data analysis
  - project
  - programming
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---


## Welcome to Indeed Scraping project



### Web Scraping:
For this project, I wanted to analyze aerospace and defense-related firms using company reviews from Indeed, a job aggregator site that updates frequently.  I scraped the company reviews for 5 AeroDefense Companies (Boeing, Raytheon Tech., SpaceX, Northrop Grumman, and Lockheed Martin) using the libraries, such as requests, BeautifulSoup, and pandas. 

#### Objectives
- The scope of the analysis was limited to these primary objectives:
- To find interesting 'stories' that can be mined from the data set.
- To understand key data points of a company.
- To understand the topics of positive and negative reviews by each company (Benefits, compensation, etc.)


Each review scraped contains the following elements: Company name, Occupation of Employee, Status (Current or Former), Location, Date, Pros, and Cons. For this analysis, I did not scrape the main body of the review due to it not being part of my objectives.  
![image-center](/assets/images/web/Snip20200709_2.png){: .align-center}

#### At a Glance:

I gathered around approximately 26,000 reviews from the five firms, notably Lockheed Martin having the highest reviews at 7,800.
An excerpt of the Python code is shown below:
~~~ Python
for x in results:
	# strips the employee position from the html page
        position = x.find('span', attrs={"class":"cmp-ReviewAuthor"})
        if position:
            #print('Position:', position.text.strip() )			
            companyPosition = position.text.strip()
	# strips the rating from the review from the html page
        rating = x.find('div', attrs={'class': "cmp-ReviewRating-text"})
        if rating:
            #print('Rating:', rating.text.strip() )
            companyRating = rating.text.strip()
~~~


#### Cleaning:
Some reviews were unusable as a result of the scraping: either from duplicated reviews or mismatch data row to its column (e.g. a Job Title inside the Date column).  I cleaned the data using the combination of Python and R.  Python curated the duplicates, and R allowed to strip the Dates into its columns using regex. An excerpt of the code below to create independent columns of day, month, year, and weekday using R. 
~~~ R
#mydata = read.csv("Indeed_records.csv", sep =";")
rawdata <- fread('Indeed/filtered.csv', fill = TRUE)
# extract year, month, date from fulldate
rawdata$year <- format(as.Date(rawdata$Date, format="%B %d, %Y"),"%Y")
rawdata$month <- format(as.Date(rawdata$Date, format="%B %d, %Y"),"%m")
rawdata$day <- format(as.Date(rawdata$Date, format="%B %d, %Y"),"%d")
#rawdata$weekdays <- weekdays(as.Date(rawdata$Date, format="%B %d, %Y"),label = TRUE)
rawdata$weekdays = format(as.Date(rawdata$Date,format="%B %d, %Y"), "%A")

# remove reviews with NA year/month/day (only 5 observations removed)
rawdata <- rawdata[!is.na(rawdata$year),]
rawdata <- rawdata[!is.na(rawdata$month),]
rawdata <- rawdata[!is.na(rawdata$day),]
~~~
#### Results: 
One of the most simple yet efficient methods of presenting data is using Wordclouds. Python and R have libraries that allow for simple wordcloud presentation.  For this project, I used Python as a testing ground for creating the wordcloud files of each company.

##### Boeing Pros
<figure class="half">
    <a href="/assets/images/wordclouds/BoeingProsExcel.png"><img src="/assets/images/wordclouds/BoeingProsExcel.png"></a>
    <a href="/assets/images/wordclouds/BoeingderivedUPDATED_Pros.png"><img src="/assets/images/wordclouds/BoeingderivedUPDATED_Pros.png"></a>
    <figcaption>An overwhelming Pros in Boeing are the benefits and pay </figcaption>
</figure>

##### Boeing Cons
<figure class="half">
    <a href="/assets/images/wordclouds/BoeingConsExcel.png"><img src="/assets/images/wordclouds/BoeingConsExcel.png"></a>
    <a href="/assets/images/wordclouds/BoeingderivedUPDATED_Cons.png"><img src="/assets/images/wordclouds/BoeingderivedUPDATED_Cons.png"></a>
    <figcaption> Management is a significant Con for Boeing</figcaption>
</figure>

##### SpaceX Pros
<figure class="half">
    <a href="/assets/images/wordclouds/SpaceXProsExcel.png"><img src="/assets/images/wordclouds/SpaceXProsExcel.png"></a>
    <a href="/assets/images/wordclouds/SpacexderivedUPDATED_Pros.png"><img src="/assets/images/wordclouds/SpacexderivedUPDATED_Pros.png"></a>
    <figcaption> Almost 1/3 of the top 30 words consists of food related benefits and perks </figcaption>
</figure>

##### SpaceX Cons
<figure class="half">
    <a href="/assets/images/wordclouds/SpaceXConsExcel.png"><img src="/assets/images/wordclouds/SpaceXConsExcel.png"></a>
    <a href="/assets/images/wordclouds/SpacexderivedUPDATED_Cons.png"><img src="/assets/images/wordclouds/SpacexderivedUPDATED_Cons.png"></a>
    <figcaption>The number of hours is a significant Con in SpaceX</figcaption>
</figure>

#### Using R for more analysis:

As seen below, the number of reviews has peaked in 2018, with the numbers decreasing again in 2019-2020.  Additionally, the reviews are more likely to be posted at the beginning of the week, with Saturday being the least day of posting. 

<figure class="third">
	<a href="/assets/images/R/CountofReviewsbyCompany& Year.png"><img src="/assets/images/R/CountofReviewsbyCompany& Year.png"></a>
	<a href="/assets/images/R/Count of Reviews by weekdays per Year.png"><img src="/assets/images/R/Count of Reviews by weekdays per Year.png"></a>
	<a href="/assets/images/R/totalreviews.png"><img src="/assets/images/R/totalreviews.png"></a>
	<figcaption>Several Visualization that can be done in R</figcaption>
</figure>



A majority of the reviews came from former employees. Likewise, contrary to my expectations, Former Employees tend to view their past employers more favorably.  The exception of this find is SpaceX, which might be due to the low number of reviews. 
<figure class="half">
    <a href="/assets/images/R/CurrentvsFormer.png"><img src="/assets/images/R/CurrentvsFormer.png"></a>
    <a href="/assets/images/R/CurrentvsFormerRatings.png"><img src="/assets/images/R/CurrentvsFormerRatings.png"></a>
    <figcaption>Left: Current vs Former Employee breakdown</figcaption>
</figure>


#### Other Visuals
  <div class = "notice--primary">
    <p> See other Visuals </p>
    <a href="/assets/images/R/Average Rating by Month per Year.png" class="btn btn--inverse .btn--small"> Average Rating by Month per Year</a> 
 <a href="/assets/images/R/Average Rating by weekdays per Year.png" class="btn btn--inverse .btn--small"> Average Rating by weekdays per Year</a> 
 <a href="/assets/images/R/Count of Reviews by Company and Weekday.png" class="btn btn--inverse .btn--small"> Count of Reviews by Company and Weekday</a> 
<a href="/assets/images/R/averageRatingMonth.png" class="btn btn--inverse .btn--small"> averageRatingMonth</a> 
  </div>


