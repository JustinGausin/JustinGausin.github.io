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

###Objectives
The scope of the analysis was limited to these primary objectives:
To find interesting 'stories' that can be mined from the data set.
To understand key data points of a company.
To understand the topics of positive and negative reviews by each company (Benefits, compensation, etc.)


Each review scraped contains the following elements: Company name, Occupation of Employee, Status (Current or Former), Location, Date, Pros, and Cons. For this analysis, I did not scrape the main body of the review due to it not being part of my objectives.  
![image-center](/assets/images/web/Snip20200709_2.png){: .align-center}

#### At a Glance:

I gathered around approximately 26,000 reviews from the five firms, notably Boeing having the highest reviews at 7,800. See CSV file below.



#### Cleaning:
Some reviews were unusable as a result of the scraping: either from duplicated reviews or mismatch data row to its column (e.g. a Job Title inside the Date column).  I cleaned the data using the combination of Python and R.  Python curated the duplicates, and R allowed to strip the Dates into its columns using regex. 
```
///insert code hurrrr
```
#### Results: 
One of the most simple yet efficient methods of presenting data is using Wordclouds. Python and R have libraries that allow for simple wordcloud presentation.  For this project, I used Python as a testing ground for creating the wordcloud files of each company. 
<figure class="half">
    <a href="/assets/images/wordclouds/BoeingderivedUPDATED_Pros.png"><img src="/assets/images/wordclouds/BoeingderivedUPDATED_Pros.png"></a>
    <a href="/assets/images/wordclouds/BoeingderivedUPDATED_Cons.png"><img src="/assets/images/wordclouds/BoeingderivedUPDATED_Cons.png"></a>
    <figcaption>Left: Boeing Pros, Right: Boeing Cons</figcaption>
</figure>


<figure class="half">
    <a href="/assets/images/wordclouds/SpacexderivedUPDATED_Pros.png"><img src="/assets/images/wordclouds/SpacexderivedUPDATED_Pros.png"></a>
    <a href="/assets/images/wordclouds/SpacexderivedUPDATED_Cons.png"><img src="/assets/images/wordclouds/SpacexderivedUPDATED_Cons.png"></a>
    <figcaption>Left: SpaceX Pros, Right: SpaceX Cons</figcaption>
</figure>



#### Using R for more analysis:

As seen below, the number of reviews has peaked in 2018, with the numbers decreasing again in 2019-2020.  Additionally, the reviews are more likely to be posted at the beginning of the week, with Saturday being the last day of posting. 

<figure class="third">
	<a href="/assets/images/R/CountofReviewsbyCompany& Year.png"><img src="/assets/images/R/CountofReviewsbyCompany& Year.png"></a>
	<a href="Count of Reviews by weekdays per Year.png"><img src="/assets/images/R/Count of Reviews by weekdays per Year.png"></a>
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


