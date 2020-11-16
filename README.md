# An Analysis of Kickstarter Theater Campaigns (Kickstarting in Excel)

## Overview of Project

The process of using data from past crowdfunding projects that include lifestyle categories such as, food, film, technology, etc. to identify success/failure rates in order to support a new Kickstarter campaign with a focus in the theater category. 
	
The requestor, Louise, a playwright is looking to create a campaign to fund her upcoming project, a play ***"Fever"***. She has asked for assistance to understand how campaigns work and what key factors should she focus on in order to plan a successful campaign. 


### The Purpose

The purpose of this project is to learn how to use excel as a tool to analyze a dataset consisting of greater than 4,000 crowdfunding projects to identify trends and provide recommendations on how a new campaign should be approached based on historical outcomes. Within this exercise, I learned how to:

* convert **Unix Timestamps** into month/day/year format
* use **Pivot Tables** to condense and focus on specific data points (i.e. theaters)
* create **Pivot Charts** to provide a visual summary of outcomes
* apply **Statistical Formulas** to identify outliers and/or determine deviations
* use **V/HLookup and IFStatement** formulas to populate and/or calculate data from one worksheet to another based on specific metrics


## The Process of Analysis and Challenges Encountered

Majority of the analysis was done by condensing the dataset using **Pivot Tables** and creating **Pivot Charts** to plot the results. For a novice, these tools would be easy to follow, but anyone that is new to Excel, it can be overwhelming determining the correct metric and their placement to get the results you need.

#### Pivot Table	

![pivot_table](https://github.com/amylio/kickstarter-analysis/blob/main/Resources/Images/Pivot_table.png)

#### Pivot Charts

![Outcomes_vs_goals](https://github.com/amylio/kickstarter-analysis/blob/main/Resources/Outcomes_vs_Goals.png)

In order to complete the analysis, the data needed to have missing components added, such as, the Percent Funded `=ROUND(E2/D2*100,0)`, Average Donation (replacing errors with a zero) `=IFERROR(ROUND(E2/L2,2),0)` and convert the Unix Timestamp for the launch and deadline date `=(((J2/60)/60)/24)+DATE(1970,1,1)`.

There were a few challenges I came across when attempting to mirror the lesson plan as shown in the module.

1. Unix timestamp formula returned values, but the format did not appear as **mm/dd/yyyy**. Used the "date" format function in order to convert to the correct format.

![month_date](https://github.com/amylio/kickstarter-analysis/blob/main/Resources/Images/Month_date.png)

![month_date_converted](https://github.com/amylio/kickstarter-analysis/blob/main/Resources/Images/Month_date_converted.png)

2. When pivoting this data, my version of excel did not allow me to group the date field by month in order to display the "month" only. 

![grouping_month](https://github.com/amylio/kickstarter-analysis/blob/main/Resources/Images/Grouping_Month.png)

In order to overcome this challenge, I added another column to the dataset to parse out the month `=TEXT(S2,"mmmm")` from the results after the Unix Timestamp was converted. 

3. The process to use `COUNTIFS` formula to calculate the number of successful vs. failed campaigns by dollar range was very manual and cumbersome. When the range was greater than x, but less than x, I would end up with an error depending on how I wrote the formula.  For example, **">"** needs to be before **"="**. This can be an easy mistake to make for someone with little to no experience in Excel. A person can spend time trying figure out what is causing the error in order to correct it. Especially when the formula is a long string. Also I added a `MID` `=MID(C$1,8,6)` formula to speed up the process of manually changing the formula from "Number Successful" to "Number Failed".
`=COUNTIFS('kickstarter data'!$F:$F,MID(C$1,8,6),'kickstarter data'!$D:$D,">=5000",'kickstarter data'!$D:$D,"<=9999",'kickstarter data'!$R:$R,"plays")` 

## The Initial Findings

When reviewing the results at the highest level, **Parent Category**, the two most successful campaigns in the US were **Music** and **Theater**. Combined, these two categories represented 1015 (62%) out of 1651 funded campaigns.

![Parent_Company_Percent_Successful](https://github.com/amylio/kickstarter-analysis/blob/main/Resources/Images/Parent_Company_Percent_Successful.png)

When we drill down to the sub-category level for Theater specifically, the "Plays" category had 61% (412) out of 671 campaigns that were successfully funded.

![subcategory_plays](https://github.com/amylio/kickstarter-analysis/blob/main/Resources/Images/Subcategory_plays.png)

These results show that Louise would likely be able to get her Kickstarter campaign to funded, but there is still a risk if other factors are not taken into consideration since more than 30% of the campaigns in "Plays" failed (250 out of 671).  Let's review further to determine why. 

### How Time Will Determine the Outcome (Analysis of Outcomes based on Launch Date)

Campaigns launched in the Spring were more successful than those launched in the Winter. This means that the best time to start the campaign would be in May/June. In the chart below, we see that there were more than 100 campaigns in May and June that were successfully funded compared to less than 60 in November and less than 40 in December. We can only assume that people are less likely to support a campaign due to the Winter holiday season.

![Theater_Outcomes_vs_Launch](https://github.com/amylio/kickstarter-analysis/blob/main/Resources/Theater_Outcomes_vs_Launch.png)

### Does Setting a Reasonable Goal Make a Difference? (Analysis of Outcomes based on Goals)

Campaigns with goals less than $5000 saw an average of 74% `=AVERAGE(76%,74%)`success rate compared to the other ranges with an average of $5602 funded vs the average goal of $5049. The average pledged amount were 10% `=(5602-5049)/5602` better than the goal. When you analyze why campaigns failed, the results showed that the average goal for failed campaigns was greater than $10554 with only an average of $559 funded. This would mean that the higher the goal, the less likely it would succeed due to campaign length of time and number of backers that would be needed.

![outcomes_vs_goals](https://github.com/amylio/kickstarter-analysis/blob/main/Resources/Outcomes_vs_Goals.png)
 
![Goal_deviations](https://github.com/amylio/kickstarter-analysis/blob/main/Resources/Images/Goal_deviations.png)

### Challenges and Difficulties Encountered (not related to the analysis)

Challenges and difficulties encountered were mainly the learning curve of using Office 365 version of Excel on a MacOS vs. the windows version. The navigation was cumbersome and tasks took longer to complete due to the limitations I experienced with no keyboard shortcuts and having to be mouse/ribbon dependent.

Being new to GitHub, gitlab and virtual learning, I found it confusing at times getting set up and knowing what to do and where to go for a detail outline/instructions or maybe a "how-to" guide. Now that I am set up properly and completed this first challenge, I am hoping that the upcoming weeks will run a lot smoother.

## Results

#### What are two conclusions you can draw about the Outcomes based on Launch Date?  

1. The **best** time to launch a campaign would be in May or June as the results showed a higher success rate in these months.
2. Campaigns are **not** successful in the Winter months (i.e. November-January). This may be the result of Seasonal Holidays such as, Christmas and Winter breaks.

#### What can you conclude about the Outcomes based on Goals?

* Campaigns are more successful when reasonable goals are set. In the analysis, campaigns with an average goal of $5000 were successful whereas campaigns with average goals of greater than $10000 had a higher failure rate.

#### What are some limitations of this dataset?

Some of the limitations that would be helpful in making this dataset more robust are: 
* Identify the backers by gender. This may help to determine target audience.
* Provide references on why campaigns failed. Was it due to length of time, launch date or unreasonable goals?
* Determine what marketing tool was used to advertise the campaign (i.e. flyers, social media, TV Ads,etc.). Was one better than the other?

#### What are some other possible tables and/or graphs that we could create?

1. A comparison of US vs. GB by success rate compared to total campaigns. In this example, GB showed that the the total number of campaigns was significantly lower than the US. However, there was a 76% success rate in compared 61% in the US.

![us_vs_gb_pivot](https://github.com/amylio/kickstarter-analysis/blob/main/Resources/Images/US_vs_GB_Pivot.png)

![us_vs_gb](https://github.com/amylio/kickstarter-analysis/blob/main/Resources/Images/US_vs_GB.png)

2. A comparison of US vs. GB by launch date. Does GB follow a similar trend to the US? In this example, both countries showed similar success with campaigns launched in May and June. However, while US spiked in May and started to wind down, GB showed a steady pace with both May and June.

![US_vs_GB_Theater_Launch](https://github.com/amylio/kickstarter-analysis/blob/main/Resources/Images/US_vs_GB_Theater_Launch.png)

**Completed dataset with pivot tables and charts used for this analysis: [kickstarter_challenge](https://github.com/amylio/kickstarter-analysis/blob/main/Kickstarter_Challenge.xlsx)**

