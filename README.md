# Terry Traffic Stops

## Introduction

A **_Terry stop_** is a seizure under both state and federal law. A _Terry_ stop is defined in policy as:


    A brief, minimally intrusive seizure of a subject based upon articulable reasonable
    suspicion in order to investigate possible criminal activity. The stop can apply to people
    as well as to vehicles. The subject of a *Terry* stop is not free to leave.
        
        
**_Reasonable suspicion_** requires:


    Specific, objective, articulable facts which, taken together with rational inferences, would
    create a well-founded suspicion that there is a substantial possibility that a subject has
    engaged, is engaging or is about to engage in criminal conduct.
    
    
The reasonableness of the _Terry_ stop is considered in view of the totality of the circumstances,
the officer’s training and experience, and what the officer knew before the stop. Information
learned during a stop can lead to additional reasonable suspicion or probable cause that a crime
has occurred, but cannot provide the justification for the original stop.
An officer may **_frisk_**, or pat-down, the subject of a *Terry* stop when, under the totality of the
circumstances and reasonable conclusions drawn from the officer’s training and experience, the
officer has reasonable suspicion that the subject may be armed and presently dangerous. A frisk
is strictly limited to a search (generally a pat-down of outer clothing) necessary to the discovery
of weapons that may be used to harm the officer or others nearby.
All data utilized was sourced [here](https://data.seattle.gov/Public-Safety/Terry-Stops/28ny-9ts8).


## Table of contents

- [Objectives and Steps](#objectives)
- [Data Understanding](#data-understanding)
    
- [EDA](#eda)
    - [Univariate Analysis](#univariate-analysis)
    - [Bivariate Analysis](#bivariate-analysis)
    - [Outliers](#outliers)
- [Model Analysis](#modeling)	
    - [Baseline Model](#baseline-model)
    - [Findings](#findings)
- [Recommendations](#recommendations)
- [Future Work](#future-work)


## Objectives
1. To investigate what factors would highly result to a person being arrested after a Terry Stop.
2. To predict whether an arrest was made after a Terry Stop.
3. To find out whether Terry Stops are biased towards minority groups.


## Data Understanding


| **Column**               | **Description**                                                                                                                                                                                                                                                          |
|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Subject Age Group        | Subject Age Group (10 year increments) as reported by the officer.                                                                                                                                                                                                       |
| Subject ID               | Key, generated daily, identifying unique subjects in the dataset using a character to character match of first name and last name. "Null" values indicate an "anonymous" or "unidentified" subject. Subjects of a Terry Stop are not required to present identification. |
| GO / SC Num              | General Offense or Street Check number, relating the Terry Stop to the parent report. This field may have a one to many relationship in the data.                                                                                                                        |
| Terry Stop ID            | Key identifying unique Terry Stop reports.                                                                                                                                                                                                                               |
| Stop Resolution          | Resolution of the stop as reported by the officer.                                                                                                                                                                                                                       |
| Weapon Type              | Type of weapon, if any, identified during a search or frisk of the subject. Indicates "None" if no weapons was found.                                                                                                                                                    |
| Officer ID               | Key identifying unique officers in the dataset.                                                                                                                                                                                                                          |
| Officer YOB              | Year of birth, as reported by the officer.                                                                                                                                                                                                                               |
| Officer Gender           | Gender of the officer, as reported by the officer.                                                                                                                                                                                                                       |
| Officer Race             | Race of the officer, as reported by the officer.                                                                                                                                                                                                                         |
| Subject Perceived Race   | Perceived race of the subject, as reported by the officer.                                                                                                                                                                                                               |
| Subject Perceived Gender | Perceived gender of the subject, as reported by the officer.                                                                                                                                                                                                             |
| Reported Date            | Date the report was filed in the Records Management System (RMS). Not necessarily the date the stop occurred but generally within 1 day.                                                                                                                                 |
| Reported Time            | Time the stop was reported in the Records Management System (RMS). Not the time the stop occurred but generally within 10 hours.                                                                                                                                         |
| Initial Call Type        | Initial classification of the call as assigned by 911.                                                                                                                                                                                                                   |
| Final Call Type          | Final classification of the call as assigned by the primary officer closing the event.                                                                                                                                                                                   |
| Call Type                | How the call was received by the communication center.                                                                                                                                                                                                                   |
| Officer Squad            | Functional squad assignment (not budget) of the officer as reported by the Data Analytics Platform (DAP).                                                                                                                                                                |
| Arrest Flag              | Indicator of whether a "physical arrest" was made, of the subject, during the Terry Stop. Does not necessarily reflect a report of an arrest in the Records Management System (RMS).                                                                                     |
| Frisk Flag               | Indicator of whether a "frisk" was conducted, by the officer, of the subject, during the Terry Stop.                                                                                                                                                                     |
| Precinct                 | Precinct of the address associated with the underlying Computer Aided Dispatch (CAD) event. Not necessarily where the Terry Stop occurred.                                                                                                                               |
| Sector                   | Sector of the address associated with the underlying Computer Aided Dispatch (CAD) event. Not necessarily where the Terry Stop occurred.                                                                                                                                 |
| Beat                     | Beat of the address associated with the underlying Computer Aided Dispatch (CAD) event. Not necessarily where the Terry Stop occurred.                                                                                                                                   |



## EDA
### Univariate Analysis
#### Subject Age Distribution
< img src = "images/subject_age_distribution.png" >


Majority of the subjects are aged between 26-35 years.


#### Weapon Type Distribution
< img src = "images/weapon_type_distribution.png" >

Most subjects were found not to have weapons of any type either non-firearms
(Club, Blackjack, Brass Knuckles, Mace/Pepper Spray, Knife/Cutting/Stabbing 
Instrument,Taser/Stun Gun) or firearms(handgun,automatic handgun,shotgun,rifle,incendiary Device).


#### Reported Month Distribution
< img src = "images/reported_month_distribution.png" >


Majority of reports take place during the second quarter of the year 
(May, June, July, August).


#### Reported Time Distribution
< img src = "images/reported_time_distribution.png" >


The difference in reports during daytime and nightime is marginal with majority reports during nightime.


#### Stop Resolution
< img src = "images/reported_time_distribution.png" >


In most cases no offence was reported nor was an arrest made.


#### Arrest Flag
< img src = "images/arrest_flag_distribution.png" >


No arrests were made during the majority of **_Terry stops_**


#### Frisk Flag Distribution
< img src = "images/frisk_flag_distribution.png" >


Most subjects were not frisked.


#### Officer Age Distribution
< img src = "images/officer_age_distribution.png" >


Most officers are aged between 26 and 31 years of age.


#### Subject Perceived Race Distribution
< img src = "images/subject_perceived_race_distribution.png" >

White and black subjects are the majority subject population.

#### Officer Race Distribution
< img src = "images/officer_race_distribution.png" >

Most officers are of white ethnicity.


### Bivariate Analysis
#### Distribution of Arrest Flag and Oficer Age
< img src = "images/arrest_flag_and_officer_age_distribution.png" >

Officers aged between 28 and 32 tend to issue more arrest flags.


#### Weapon Type by Subject Age Group
< img src = "images/weapon_type_by_subject_group_distribution.png" >

Subjects aged between 26 - 35 bear majority arms.


### Outliers
< img src = "images/officer_age_boxplot.png" >


Full retirement age in Seattle is 65 as per [this article](https://www.drs.wa.gov/plan/pers2/). 
Anyone aged above 65 is considered an outlier.


## Modeling
### Model Preprocessing
    1. Converting target variable to binary.
    2. Splitting the dataset into training and testing data.
    3. SMOTE analysis to deal with class imbalance.
    4. One Hot encoding of categorical data.
### Baseline Model
A random forest model was chosen as it uses more than one model to make a prediction
which makes it typically more effective when compared with single-model results for supervised learning tasks.


### Findings
        1. Factors that highly influence a Terry Stop arrests Reported Year Reported 
            Month Subject Age Group Weapon Type Reported Time
        2. Factors that highly result to a person being stoped, frisked, and arrested 
            after a Terry Stop? When we look at the data for frisks, we see that             
            the focus is really on just two precincts: the East and South. The number of frisks 
            during Terry stops increased in only those two precincts, and the likelihood that 
            a stop would lead to a frisk also increased in those same two places
        3. Whether Terry Stops are biased towards minority groups. Overall, the data skews 
            heavily male, and is almost entirely two racial groups: blacks/African Americans 
            and whites. Blacks continue to be over-represented in the Terry stops data compared 
            to their representation in the entire population of Seattle.


### Recommendations
        1. Combined Law Enforcement and Community Policing Members of the community join police 
            officers and observe the officers' activities while working their Beat.This can lead to 
            an increase in public trust, a better understanding of the people in their jurisdiction, 
            as well as educate people about why certain policies are in place.
        2. In determining whether probable cause exists, courts more readily accept the judgment 
            of a law enforcement officer if it is backed by evidence of a crime/weapon possession.


### Future Work
        1. The dataset contained a lot of NaN or incomplete information. Collect more data that adds
           more context o the nature of stops
        2. Audit record system and reduce redundant columns to reduce noise
        3. Look into data for police reported stops in other regions for comparison
        4. Collect and analyze data on those arrested and eventually found guilty in court

