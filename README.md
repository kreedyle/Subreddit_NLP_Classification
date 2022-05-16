## Project 3: Web APIs & NLP

### Problem statement: 
After using an API to 

### Data Chosen: 

 - [`act_2018.csv`](./data/act_2018.csv): 2018 ACT Scores by State
 - [`act_2019.csv`](./data/act_2019.csv): 2019 ACT Scores by State

 - [`sat_2018.csv`](./data/sat_2018.csv): 2018 SAT Scores by State
 - [`sat_2019.csv`](./data/sat_2019.csv): 2019 SAT Scores by State
 
Additional data collected at links listed below:
 - https://soflotutors.com/blog/sat-scores-by-state/ (2020 data)
 
 - https://blog.prepscholar.com/average-sat-scores-by-state-most-recent (2021 data)
 
 - https://www.act.org/content/dam/act/unsecured/documents/2020/2020-Average-ACT-Scores-by-State.pdf
 
 - https://www.act.org/content/dam/act/unsecured/documents/2021/2021-Average-ACT-Scores-by-State.pdf

Data chosen is available in the data folder which includes the raw files and merged files. 

### Outside research: 

   Before diving into my own analysis of the SAT & ACT scores, I would like to briefly provide a few considerations for context. My purpose for this context is to not only address the adversity students may have faced due to the pandemic such as school closures, health/safety concerns etc., but also account for the resislence of the human spirit to overcome obstacles.

   My problem statement looks to determine whether or not COVID-19 has had an impact on student's average performance on the SAT/ACT. A study conducted by ACT Research in August 2021, "...intended to give insight into several potential problems and challenges that high school students might experience and to assess how those are connected, if at all, to academic performance" (Schiel, pg. 1, 2021). 
   
   Although a large sample of nearly 4,000 students were surveyed, I feel the percentage of respondants is worth noting as this only represents "...12% of all students who were invited to participate" (Schiel, pg. 1, 2021). In this study, I examined two charts which analyzed categories of problems and challenges students faced and how those effects may have negatively impacted their academic performance broken into race/ethnicity, respectively. 

#### Note: 
 - outside_research folder contains a snapsnot from study cited below. The snapshot will serve as supplementary information to provide context of my analysis.
 
Works Cited 
 - https://www.act.org/content/dam/act/unsecured/documents/pdfs/R2123-problems-challenges-affecting-hs-students-2021-08.pdf Accessed on: 3/19/2022
 
### Data Dictionary:

|Feature|Type|Dataset|Description|
|---|---|---|---|
|state|object|act_scores|The state where test score participation and average score data was collected. Alphabetically sorted.| 
|participation_act_18|float64|act_scores|Participation percentage rate of students in 2018 from corresponding state.|
|composite_act_18|float64|act_scores|Average score of ACT test calculated from Math, Reading, English, and Science subtests in 2018. Range of scores from 1 to 36.|
|participation_act_19|float64|act_scores|Participation percentage rate of students in 2019 from corresponding state.|
|composite_act_19|float64|act_scores|Average score of ACT test calculated from Math, Reading, English, and Science subtests in 2019. Range of scores from 1 to 36.|
|participation_act_20|float64|act_scores|Participation percentage rate of students in 2020 from corresponding state.|
|composite_act_20|float64|act_scores|Average score of ACT test calculated from Math, Reading, English, and Science subtests in 2020. Range of scores from 1 to 36.|
|participation_act_21|float64|act_scores|Participation percentage rate of students in 2021 from corresponding state.|
|composite_act_21|float64|act_scores|Average score of ACT test calculated from Math, Reading, English, and Science subtests in 2021. Range of scores from 1 to 36.|
|state|object|sat_scores|The state where test score participation rate and average score data was collected. Alphabetically sorted.|
|participation_sat_18|float64|sat_scores|Participation percentage rate of students in 2018 from corresponding state.|
|composite_sat_18|int64|sat_scores|Average score of SAT test calculated from EBRW (Evidence-Based Reading & Writing) & Math subtests in 2018. Range of scores from 400 to 1600.|
|participation_sat_19|float64|sat_scores|Participation percentage rate of students in 2019 from corresponding state.|
|composite_sat_19|int64|sat_scores|Average score of SAT test calculated from EBRW (Evidence-Based Reading & Writing) & Math subtests in 2019. Range of scores from 400 to 1600.|
|participation_sat_20|float64|sat_scores|Participation percentage rate of students in 2020 from corresponding state.|
|composite_sat_20|int64|sat_scores|Average score of SAT test calculated from EBRW (Evidence-Based Reading & Writing) & Math subtests in 2020. Range of scores from 400 to 1600.|
|participation_sat_21|float64|sat_scores|Participation percentage rate of students in 2021 from corresponding state.|
|composite_sat_21|int64|sat_scores|Average score of SAT test calculated from EBRW (Evidence-Based Reading & Writing) & Math subtests in 2021. Range of scores from 400 to 1600.|

### Overview of Data Directory:

This directory contains the data I chose to use for this analysis - four years of average scores and participation percentage rates of the ACT & four years of average scores, and participation percentage rates of the SAT. Since my problem statement is an analysis of whether or not COVID-19 had an effect on student's average scores across the 50 states, I wanted to see if a pattern exists across the span of four years - two years prior to the pandemic 2018-2019 and two years during the pandemic 2020-2021. 

I merged the total four years of scores together for each separate test into one dataframe: 
    - act_scores.csv
    - sat_scores.csv
Finally, I merged all four years of ACT & SAT scores together into one dataframe for easier analysis of stats: 
    - act_sat_scores.csv
Since the scale of scores are not similar, when doing data visualizations I chose to look at the ACT and SAT dataframes separately. 

## Conclusions, Keytakeaways, & Recommendations:

  When doing a deep dive into the data, I didn’t see a shocking drop of the national mean scores for the ACT or SAT; however, the mean participation percentage rate of both saw a significant 15% drop from 2018-2021. In addition, the median participation rate got cut nearly in half.
   
   The next step I took in my analysis was zooming in on state level metrics for patterns. Not surprisingly, the states which took favor with a certain test often had a lower participation rate of the other. Interestingly, when looking at both standardized tests there was a distinct negative correlation between states with the lowest participation rates testing above the national average and vice versa. 

   My problem statement focused on the impact COVID-19 had on testing metrics for the ACT and SAT. From my analysis, I think the pandemic has shown an impact on the most crucial means of getting this data - participation. I conclude both metrics were disrupted slightly due to the pandemic with participation seeing a greater change overall; however, the shifts in achievement were not quite as dramatic as I initially thought. Some of my key takeaways include: the pandemics impact on participation with both tests seeing a 15% drop overall from 2018-2021. Also, the percent of increase trend we are seeing in the composite ACT scores nationally. Finally, the negative correlation which exists across all four years and with both standardized tests. 
   
   Although the data now is only showing a slight shift in patterns, I don’t believe we can truly know the ripple effect of this ongoing pandemic until elementary students of the pandemic begin taking the ACT/SAT 10-12 years from now. As I mentioned previously about the resilience of the human spirit though, these past two years have shown how well students and teachers alike are able to adapt and be resourceful in order to overcome adversity. COVID-19 has halted our usual patterns and has truly shown a light on the trends of inequities in this country. We must reevaluate institutions like education to see how we can begin to reverse the trends. We still have time, we must learn to prioritize these disparities. 
   
   Thankfully, we have the power of technology which in conjunction with our ability to adapt has allowed us to transform the workplace environment - now why can’t similar steps be taken to tackle the disparity we see in higher education related to standardized testing preparation and logistics. 
   
   My recommendations are to work with third party platforms such as Khan Academy <a href="https://www.khanacademy.org/test-prep">(source)</a> or Kumon <a href="https://www.kumon.com/resources/5-easy-tips-to-prepare-for-standardized-testing-season/">(source)</a> to provide students with preparation and test taking logistical help. Also, I think a focus on policy decisions related to funding STEM programs across ALL schools is crucial to closing those achievement gaps we are seeing. Next, take some time to appreciate the educators who rose to the occasion and the students who choose to continue forward even if the path is treacherous and unclear.  Finally, focus on the positive ways in which technology has helped immensely in allowing students to continue to be educated even through the pandemic because celebrating victories matters <a href="http://zoom.us">(Zoom for the win)</a>.