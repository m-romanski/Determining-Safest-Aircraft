# Recommendations for Safest Aircrafts 

## Overview

  In this study, we aim to process, clean, understand, and produce statistically significant data in order to make evidence-based decisions in terms of operating the safest aircrafts.
  Starting from a large dataset, we will be able to determine a list of top 10 safest aircrafts from professional manufacturers worldwide.

  Our client is looking to enter the aviation industry and has asked us to determine how to maximize safety in this endeavor. Using data provided by the National Transportation Safety Board (NTSB) we have determined the following:

-Our client should invest in a Boeing aircraft that has at least two engines.

-Our client should fly on-demand, unscheduled operations under Federal Aviation Regulation Part 135.

-Our client should pursue regional business in the United States but outside of the Northeast.
  
## Business Understanding

Business owners that are looking to invest in commercial and private flight operations need to have a well-defined picture of the aircraft statistical spectrum in order to make purchases that will best fit their business model. Therefore, key questions related to the aircraft operations industry must be answered before the company proceeds with acquiring any flight aparatus. 

These questions include, but are not limited to:

-How many accidents are associated with the aircraft makes?

-How many fatal injuries are associated with each make?

-How many individuals have survived in accidents associated with each make?

-What are the percent chances of survival in case of an accident?

-How is the number of engines on an aircraft related to overall aircraft safety?

-How is flight protocol related to overall aircraft safety?

Our client's top concern is safety. They want to know what type of aircraft is safest and how to ensure it flies safely. This benefits their bottom line too, because a focus on safety can burnish their brand in the eyes of customers. Safe flights also protect their capital investment.

## Data Understanding and Analysis

This data represents about 85.000 aviation accidents and incidents documented by the NTSB from 1968 to present. It provides details about the make and model of the aircraft involved as well as the type and number of engines. The data include numbers of injuries, categorized by severity. Entries also detail the location of the accident, the rules the plane was flying under, the date of the incident, and whether the pilot could fly visually (good weather) or with instruments (poor weather).

The biggest limitation of this dataset is that it only includes flights that had a problem. Theoretically, a perfect plane would never crash and thus would not appear in this dataset. While the data did not allow us to determine the ratio of uneventful flights to crashes, we were able to find valuable information about the severity of crashes. Our analysis shows the likelihood of injury if a particular plane does crash. Realistically, accidents do happen and there are no perfect aircraft. We can tell our client which planes are the safest when things go wrong.

We quickly eliminated columns that were not germane to our analysis. For example, our client is not seeking to purchase an already existing commercial airline, so "Air.carrier" was not useful. "Broad.phase.of.flight" would probably yield good information about the relative safety of various parts of a flight, but we wouldn't be able to recommend to our client that they avoid takeoffs and landings altogether, should we discover they were the most dangerous phases. Some categories like "Registration.Number" and "Investigation.Type" were more connected to internal NTSB processes.

<img width="895" alt="Screenshot 2023-07-14 at 10 35 09 AM" src="https://github.com/m-romanski/dsc-phase1-project-LRM/assets/137821058/fefe9fc7-7bc5-4928-947d-3eb7559eb00d">



We made a new data frame of [U.S. states and their region](https://github.com/cphalpert/census-regions/blob/master/us%20census%20bureau%20regions%20and%20divisions.csv), and prepped the aviation_df to join it.



### Summary of conclusions including three relevant findings
