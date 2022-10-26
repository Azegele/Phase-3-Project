# Terry Traffic Stops

## Introduction

A (**Terry stop**) is a seizure under both state and federal law. A *Terry* stop is defined in policy as:


    A brief, minimally intrusive seizure of a subject based upon articulable reasonable
    suspicion in order to investigate possible criminal activity. The stop can apply to people
    as well as to vehicles. The subject of a *Terry* stop is not free to leave.
        
        
(**Reasonable suspicion**) requires:


    Specific, objective, articulable facts which, taken together with rational inferences, would
    create a well-founded suspicion that there is a substantial possibility that a subject has
    engaged, is engaging or is about to engage in criminal conduct.
    
    
The reasonableness of the *Terry* stop is considered in view of the totality of the circumstances,
the officer’s training and experience, and what the officer knew before the stop. Information
learned during a stop can lead to additional reasonable suspicion or probable cause that a crime
has occurred, but cannot provide the justification for the original stop.
An officer may (**frisk**), or pat-down, the subject of a *Terry* stop when, under the totality of the
circumstances and reasonable conclusions drawn from the officer’s training and experience, the
officer has reasonable suspicion that the subject may be armed and presently dangerous. A frisk
is strictly limited to a search (generally a pat-down of outer clothing) necessary to the discovery
of weapons that may be used to harm the officer or others nearby.
All data utilized was sourced [here](https://data.seattle.gov/Public-Safety/Terry-Stops/28ny-9ts8).


## Table of contents

- [Objectives and Steps](##Objectives)
- [Data Understanding](##Data Understanding)
    
- [EDA](##EDA)
    - [Univariate Analysis](##Univariate Analysis)
    - [Bivariate Analysis](##Bivariate Analysis)
    - [Outliers](#Outliers)
- [Model Analysis, RFC](#modeling)	
    - [Vanilla](#vanilla)
    - [Final](#final)
- [Recommendations](#recommendations)


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

##EDA
