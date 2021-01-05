#### Texas_Crime_Analysis
Analysis of Crime in the state of Texas
Members:
- Forrest Collier
- Cade Culver
- Jonathan Ezeugo
- Troy Youngblood


#### Project Description: 
Analyze trends in Texas crime data by utilizing CSV files on crime, population, and income.
 

#####  Project Questions
The information collected and presented provides a high-level look at some of the general demographics of individuals and/or their crimes in the Texas Department of Criminal Justice (TDCJ) system.  The challenge of the effort was to remain at a high level and not dive deeper into a specific case or a county for this first pass on the data.  There are many stories which could be investigated during a later evaluation of the data.  For the first pass on the data, the following questions were investigated:


#### Questions: 
1. How does the likelihood of the top five offenses vary based on County and Race? Is Income highly correlated with offenses?  

2. What is the average sentence per bin
    - Part 1: What are the top 5 highest-sentencing offenses in Texas?
	    - find the average sentence in years for all offense categories
	    - display results in a data frame and the top 5 in a bar graph 
    - Part 2: How does murder-sentencing around the major Texas cities compare to murder-sentencing in Texas as a whole?
	    - look at murder sentencing in 5 Texas counties containing major cities (Harris, Dallas, 	Tarrant, 	Bexar, Travis)
	    - obtain total count of murder offenses per county
	    - compare each county’s average murder sentence with Texas state average

3. What are the most likely crimes per age bracket
    - divide dataframe in age brackets
    - Count vs. age bracket 

4. County offense outliers
    - Use heat maps to present offenses per county; filter on offense
    - Baseline county population against offenses
    - Establish population bins to present the data on a relative county population basis


The original set of questions included evaluations on parole situations.  Based on reviewing the dataset from the State of Texas TDCJ, there were many inconsistencies in how the information was entered by State of Texas employees when populating the data fields.  The parole evaluation can be completed but would require additional research on each individual's case to identify case specifics.
The original data sets used in the project and their source.
    - Texas County Population: https://demographics.texas.gov/data/TPEPP/Projections/
    - Texas Department of Public Safety – Offense Codes: https://www.dps.texas.gov/administration/crime_records/pages/appndxKOffenseCodes.htm
    - Texas Department of Criminal Justice Offender List: October 28, 2020 Update: https://www.dps.texas.gov/administration/crime_records/pages/appndxKOffenseCodes.htm
    - As a point of reference – there were 120,707 individuals listed in the State of Texas TDCJ system October 28, 2020 update. 
    - Texas County Seat Coordinates: https://data.texas.gov/dataset/Texas-Counties-Centroid-Map/ups3-9e8m

# Part I – Data Cleanup
The initial data review was to evaluate the data to determine what was readily available for use, how the data was entered into the data sets, some of the issues that needed to be resolved and, finally, how the data could be used to answer the questions.
- As noted above, an initial review of the parole data columns revealed that there were many variations in how the data was entered by the respective organizations.  Without investigating each individual’s case, many assumptions would have to be made to make the data usable for this evaluation.  Therefore, parole evaluations were dropped from this initial project.
- The Sentence Years data contained a mixture of numbers, calendar references, and words describing an individual's sentence.
- The offense category data was very granular and needed to be moved into more generic categories so evaluations could be completed.
Many minor data cleanup activities were completed to allow for evaluation and visualization.  Only the primary activities are presented below.
Sentence Years data cleanup.  
 a) The data contained the following words – “Life”, “LWOP”, “Death”, “Capital Life” and “nan”.  LWOP is an acronym for Life Without Parole. Review of the TDCJ webpage revealed that an individual assigned a sentence of Life was available for parole after 40 years.  When looking at various sentence durations for similar type crimes, Life was assigned the value 50.9.  A similar process was used for the remaining changes. There were few similar situations readily identified for comparison so best estimates were used.    Death was assigned the value 150.9, Capital Life was assigned 101.9, and nan was assigned 10.0.  There were only a total of 5, one for each word, of the Sentence Years with the above assignments so minimal impact on the overall sentence year values should be observed.  
 b) To address the calendar references, the date the person was originally sentenced was compared against the calendar reference and a Sentence Year was assigned.  Example, if the date the person was originally sentenced contained the year 2015 and the calendar year reference in the Sentence Year column originally contained 2025, the value of 10 was assigned to the Sentence Year column for that individual.
Offense code cleanup and bin assignment.
    a)	A listing of the current offense codes for the State of Texas was located and it was noted that similar offenses started with similar digits and then the rest of the number detailed the offense.  For the purposes of this review, only high-level grouping was needed.  

    b)	The current State of Texas offense code listing was then compared to the offense codes assigned to the individuals currently in the TDCJ system and it was determined that some individuals had codes assigned to them that were no longer being used.   

    c)	A two-step approach was used to assign the offenses codes for individuals currently in the TDCJ system to bins.  The bins were first assigned to the codes that are currently being used in the TDCJ system because the offense description was available for review.  Then, the individuals with archived offense codes were reviewed and best assigned to a bin based on their offense code number.  

County population addition.
    a)	To allow for the creation of offenses per county population, population information from the State of Texas was added to the prisoner data set.
The above data cleanup steps created the basis data set for the analysis to answer the questions.

# Part II – Data Visualization
The following information describes the primary steps completed to create the visualizations.
Q1) Bar charts identify which county/ race group combinations tend to commit one of the top five crimes. Income is then added to calculate a correlation and that income is overlayed on the stacked bar chart. 

Q3) Appropriate Texas crime and population data imported and cleaned, identifying, and resolving “Not-A-Number” (NaN) cells with appropriate calculations or entries, renaming specific columns, identifying possible duplicates and erroneous entries and either replacing them or removing duplicates as appropriate, to generate clean “DataFrames” for analysis. Sliced and diced the dataset as needed to answer key questions.

Q4) To identify outlier counties, setup steps were completed.  First, total offenses (offenders) per county were ratioed per 1,000 population.  Second, the counties were placed in various bins to create snapshots based on population.  The bins that best represented the data were counties with populations less than 10,000; counties with populations between 10,000 and 100,000; counties with populations between 100,000 and 500,000; and finally, counties with populations greater than 500,000.  The data was then grouped by offense and county.  
After the data was grouped by offense and county, different data sorts were completed to present data that could be used to visualize counties with the highest offense rates.  In the first data visualization, total counts of offenses were used.  In the remaining presentations, the offenses per county ratioed per 1,000 population was used to present a more representative impact on the respective counties. 
There were more than 40 different categories of offenses.  The top 5 offenses for individuals in the data set, on a total count basis, were used in the presentation to stay within the established time allotment.    The top 5 offense categories are Sexual Assault, Assault, Robbery, Murder and Drug related charges.
Based on the final population bins identified, the counties with the highest offense ratios were listed by name in the visualizations.  In many cases, a single county’s offense ratio for more than 1 of the top 5 categories would be high enough that it would result in the county being listed more than once in the top 10 ratios.  In those cases, only the offense category with the highest offense ratio would be used for the presentation and the remaining listings for the same county would be dropped out of the list.   This was done to allow for a greater representation of counties versus presenting dominance of a few.   
Heat maps were used to visualize the data.  
The first presentation is a set of heat maps showing the general population of Texas versus the Total Count of Offenses per county.  As expected, the counties with the higher populations, had the higher total counts of offenses.  
The second presentation is a set of heat maps showing the population of Texas versus the Offense Ratio per 1,000 population.  In this comparison, counties outside the major populations bases and those counties that are relatively isolated with the highest population for the area had the highest concentration of offenses.
The third presentation is a heat map identifying the counties with the highest offense ratios independent of population bin.  The counties with the smaller populations have the highest number of listings in this top 10. The reason for this is the larger counties populations dilute the offense ratios to relatively smaller values.  This was the reason for creating the population bins to allow for comparisons of relatively sized counties.  An interesting trend is identified in the heat map.  The majority (6 out of 10) of the counties in the table fall along or near either US 287 going from Fort Worth to Amarillo or US 281 going from San Antonio to Wichita Falls.  US 281 and US 287 meet in Wichita Falls.   Four of the counties are listed for Drug related charges and 2 are listed for Assault.  Kerr county is just northwest of San Antonio and if included in the count it would make 7 out if 10 counties from the table in the general location discussion.
The fourth presentation is a heat map identifying the counties with populations less than 10,000 with the highest offense ratios.  The data indicates most of the counties with population less than 10,000 are in west Texas.  Drugs and a form of assault are the primary offense categories in the smallest counties.
The fifth presentation is a heat map identifying the counties with populations greater than 10,000 and less than 100,000 with the highest offense ratios.  The data indicates most of the counties with population in the sort range are in central and east Texas.  Drugs are the highest percentage of offenses, followed by a form of assault.
The sixth presentation is a heat map identifying the counties with populations greater than 100,000 and less than 500,000 with the highest offense ratios.  The data indicates most of the counties with population in the sort range are on or north of I10.  Drugs are the highest percentage of offenses, followed by a form of assault.
The last presentation is a heat map identifying the counties with populations greater than 500,000 with the highest offense ratios. The data indicates most of the counties with population in the sort range are the major population centers along major travel arteries.  Crimes against a person are the primary offense categories.

# Conclusion
- Question 1
• 	Race groups cannot be generalized on the state level. A more granular look at communities would be more appropriate to analyze crime. 
• 	Drugs have the highlest correlation with income and sexual assault the least
• 	Income has a relatively low correlation with the number of offenses

- Question 2 
•	The top 5 highest-sentencing offenses in Texas are: Murder, Pollution, Kidnapping, Organized Crime, and Sexual Assault. The odd offense in the data is Pollution. Two of these individuals had multiple violations and were given high sentences (about 48 years average) for “unauthorized disposal” of toxic waste and materials, in violation of an environmental act. This resulted in a big increase in the average sentence years. Other examples in this offense category are pollution of waterways, underground tank violations (causing leakage into groundwater), and disposal on government property such as state parks. 

•	Murder was the highest-sentencing crime in Texas. Murder sentences in five counties containing the major cities: Harris (Houston), Dallas (Dallas), Tarrant (Fort Worth), Bexar (San Antonio), and Travis (Austin) counties were evaluated. The average murder sentence in Texas is 56 years, and Harris, Dallas and Tarrant county are all above that state average at 58.8, 57.2 and 58.1, respectively. Bexar and Travis are below the state average at 49.8 and 54. When comparing the number of murder offenses for each county with the average sentence, Bexar county has a high number of offenses (1,272) and a lower-than-average sentence rate. Tarrant county only has 983 murder offenses but has an above average sentence rate at 58.1 years.

- Question 3 
•	The top 10 counties by prisoner population from database are: Harris, Dallas, Tarrant, Bexar, McLennan, Montgomery, Travis, Smith, El Paso, and Hidalgo counties.
•	The top 10 offences by inmate counts are: Sexual Assault, Assault, Robbery, Drugs, Murder, Burglary, Alcohol Incidents, Evading Arrest, Weapon Related, and Theft.
•	Prisoners under 20 years of age (precisely 15 to 19 years old) and up to 30 years old, were most in prison for robbery. For prisoners 31 to 40 years old, they are most 	in prison for drugs or drug related offences, but from ages 41 to 90 years of age, they are most in prison for sexual assault.
•	Almost 95% of inmates in the Texas prison system are male, incarcerated mostly for robbery, sexual assault, and murder. Harris County has the most male inmates
•	As a percentage of county population, McLennan county has over 4 percent of its population incarcerated mostly for sexual assault and drugs. Of these, those between 25 	to 44 years old make up over 2 percent by county population ratio. Smith county is close second with almost 4 percent of the county population, mostly in for drugs and 	assault. Of these, inmates between 25 to 44 years of age are about 1.8% of Smith County population for that age category.
- Question 4
•	The majority of the counties adjacent to metroplex locations and further out had drug related crimes as their primary offense.  The counties with the metroplex locations 	have crimes against a person as their primary offense.  
•	Also noted, there is an interesting trend identified in the heat map that only presented Offense ratios per 1,000 and did not filter for population bin.  The majority (6 	out of 10) of the counties listed in the table fall along or near either US 287 going from Fort Worth to Amarillo or US 281 going from San Antonio to Wichita Falls.  US 	281 and US 287 meet in Wichita Falls.   Four of the counties are listed for Drug related charges and 2 are listed for Assault.  Kerr county is just northwest of San 		Antonio and if included in the count it would make 7 out if 10 counties from the table in the general location discussion.
