# Recommendations for Safest Aircrafts 

## Overview

  In this study, we aim to process, clean, understand, and produce statistically significant data in order to make evidence-based decisions in terms of operating the safest aircrafts.
  Starting from a large dataset, we will be able to determine a list of top 10 safest aircrafts from professional manufacturers worldwide.

  Our client is looking to enter the aviation industry and has asked us to determine how to maximize safety in this endeavor. Using data provided by the National Transportation Safety Board (NTSB) we have determined the following:

-Our client should invest in a Boeing aircraft that has at least two engines.

-Our client should fly on-demand, unscheduled operations under Federal Aviation Regulation Part 135.

-Our client should pursue regional business in the United States but outside of the Northeast.
  
## Business Understanding

Business owners that are looking to invest in commercial and private flight operations need to have a well-defined picture of the aircraft statistical spectrum in order to make purchases that will best fit their business model. Therefore, key questions related to the aircraft operations industry must be answered before the company proceeds with acquiring any flight apparatus. 

These questions include, but are not limited to:

-How many accidents are associated with the aircraft makes?

-How many fatal injuries are associated with each make?

-How many individuals have survived in accidents associated with each make?

-What are the percent chances of survival in case of an accident?

-How is the number of engines on an aircraft related to overall aircraft safety?

-How is flight protocol related to overall aircraft safety?

Our client's top concern is safety. They want to know what type of aircraft is safest and how to ensure it flies safely. This benefits their bottom line too, because a focus on safety can burnish their brand in the eyes of customers. Safe flights also protect their capital investment.

## Data Understanding and Analysis

This [data](https://www.kaggle.com/datasets/khsamaha/aviation-accident-database-synopses) represents about 85.000 aviation accidents and incidents documented by the NTSB from 1968 to present. It provides details about the make and model of the aircraft involved as well as the type and number of engines. The data include numbers of injuries, categorized by severity. Entries also detail the location of the accident, the rules the plane was flying under, the date of the incident, and whether the pilot could fly visually (good weather) or with instruments (poor weather).

The biggest limitation of this dataset is that it only includes flights that had a problem. Theoretically, a perfect plane would never crash and thus would not appear in this dataset. While the data did not allow us to determine the ratio of uneventful flights to crashes, we were able to find valuable information about the severity of crashes. Our analysis shows the likelihood of injury if a particular plane does crash. Realistically, accidents do happen and there are no perfect aircraft. We can tell our client which planes are the safest when things go wrong.

We quickly eliminated columns that were not germane to our analysis. For example, our client is not seeking to purchase an already existing commercial airline, so "Air.carrier" was not useful. "Broad.phase.of.flight" would probably yield good information about the relative safety of various parts of a flight, but we wouldn't be able to recommend to our client that they avoid takeoffs and landings altogether, should we discover they were the most dangerous phases. Some categories like "Registration.Number" and "Investigation.Type" were more connected to internal NTSB processes.

<img width="895" alt="Screenshot 2023-07-14 at 10 35 09 AM" src="https://github.com/m-romanski/dsc-phase1-project-LRM/assets/137821058/fefe9fc7-7bc5-4928-947d-3eb7559eb00d">



We made a new data frame of [U.S. states and their region](https://github.com/cphalpert/census-regions/blob/master/us%20census%20bureau%20regions%20and%20divisions.csv), and prepped the aviation_df to join it.

The FAR descriptions were messy and inconsistent. We needed to do a lot of renaming to properly categorize them.




<img width="866" alt="Screenshot 2023-07-14 at 10 48 36 AM" src="https://github.com/m-romanski/dsc-phase1-project-LRM/assets/137821058/a61ce1e0-9aa9-444f-9369-a4fe7e0a0cdb">



Our client values safety above all, and we cannot really determine the safety of unique aircraft. It is unlikely that our client would have the opportunity to purchase a rare or limited-production plane anyway, so we dropped all "Make" values that were less than 1% of the total dataset. Such planes are too unusual to make a good assessment of their safety. We also dropped entries that did not list "Make" because we cannot recommend a plane if we don't know what type it is.

We wanted to determine the chance of injury if a plane was in a crash, so we estimated total passengers per flight by adding all the injured passenger counts to the uninjured count. Each category ("fatal," "serious," "minor," and "uninjured") seemed exclusive, so adding them together gives a good indication of the number of passengers on board.

With our new metrics for injuries, we looked at percentage chance of injury by number of engines.



<img width="874" alt="Screenshot 2023-07-14 at 10 51 06 AM" src="https://github.com/m-romanski/dsc-phase1-project-LRM/assets/137821058/3c5d3740-7149-47c7-bdc3-e0f07ab43a2c">



Yikes! Passengers on one-engine planes have a way higher chance of fatality and any other kind of injury. The same is true of zero-engine aircraft, though it was unlikely we would recommend our client invest in hot air balloons. We opted to exclude zero and one engine aircraft from our data set, because as a category they were far more dangerous.

With our curated list of planes, we then figured out which make was the safest.

Some planes had an injury rate of zero, but the make had only ever recorded one accident. We excluded models that had not reported many incidents because we did not have sufficient data to determine if they were consistently safe.




<img width="835" alt="Screenshot 2023-07-14 at 10 56 56 AM" src="https://github.com/m-romanski/dsc-phase1-project-LRM/assets/137821058/7c47ffff-e2e3-4f5b-9316-e250f6e443e1">



It looks like if you're going to be in a plane crash, you want to do it in a Boeing! They have recorded a high number of injuries, but that's because there are so many Boeings flying each day. Per incident, the injury rate is very low, as is the fatality rate. Mcdonnell Douglas and Airbus also posted very low overall injury percentages.




<img width="381" alt="Screenshot 2023-07-14 at 10 58 04 AM" src="https://github.com/m-romanski/dsc-phase1-project-LRM/assets/137821058/942a73a5-8b5e-4f61-99e8-9cc929d4b933">



We then took our top ten safest makes and looked back at number of engines.




<img width="891" alt="Screenshot 2023-07-14 at 11 00 29 AM" src="https://github.com/m-romanski/dsc-phase1-project-LRM/assets/137821058/cb597a34-f52f-40e4-8302-4f71b4e84a7e">



Our top five safest aircraft are the four-engine Airbus, four-engine De Havilland, two-engine Boeing, two-engine McDonnell Douglas, and the three-engine Boeing. The four-engine Boeings were just outside the top five. We opted to recommend the Boeings and the two-engine McDonnell Douglas because the AirBus and De Havilland had substantially lower incident counts. We wanted to recommend a plane that was repeatedly proven to protect its passengers in the event of an accident.

After determining our pick for safest aircraft, we went back to our regional data to determine how many injuries were associated with a crash in each of our regions.

We determined that a crash in the Northeast had a higher chance of injury. (The "Unknown" category includes incidents outside the U.S. as well as any incident that did not list a location.)

An early exploration of the FAR description data showed that planes flying under Part 91 by far had the most injuries. But Part 91 is also very likely to be one-engine planes, since it is for general aviation, or non-commercial flying. We looked into the data without single-engine planes to see how many accidents were associated with crashes under each FAR protocol.




<img width="299" alt="Screenshot 2023-07-14 at 11 02 20 AM" src="https://github.com/m-romanski/dsc-phase1-project-LRM/assets/137821058/b8e2dde3-5219-4204-a4e9-5d5b66412102">



The highest injury rates were for Part 129 and for Non-U.S., Commercial, both of which apply to foreign flights. Some of the categories. like military and public use, are not relevant to our client. Of commercial and domestic options, Part 135 had the highest record of safety.

## Recommendations

We offer our client the following recommendations:

-Invest in Boeing airplanes with two, three, or four engines. A two-engine McDonnell Douglas is also proven safe.

-Focus operations in the United States outside of the Northeast.

-Fly unscheduled, on-demand flights under Federal Aviation Regulation Part 135.

## Next Steps

Next steps for data analysis could include further investigation of the safest models of Boeing aircraft. We could also look more deeply into what might lead to accidents in the Northeast having more severe outcomes. We could use the weather data included in this dataset or seek other data to help us dig into that question.

Next steps for our client would involve researching price and availability of our recommended aircraft. They also might consider opportunities to align this new venture with their commercial interests and their social responsibility values. Many Part 135 operations serve isolated or underserved areas. This offers the company a chance to find untapped markets and possibly to also demonstrate their business' commitment to giving back.


## Conclusion

The [dasboard](https://public.tableau.com/app/profile/michael.romanski/viz/ChanceofInjuryTypebyMakeandNumberofEngines/Dashboard1) below summarizes our conclusions that drove our recommendations meantioned earlier. We see a clear breakdown of our top safest aircrafts based on make, engine number, and FAR protocols, chance of overall injury, and chance of fatal injury. Therefore, the safest aircrafts are manufactured by Boeing, McDonnell (now under Boeing operations since 1997), and Airbus. In order to further increase customers' safety, these aircrafts should be operated under Federal Aviation Regulation Part 135, outside of the Northeast of the United States.

Note that a further investigation is necessary to draw conclusions on why the Northeast presents a higher danger for flights. It might be relevant to analyze the different weather conditions across multiple geographical regions for such an investigation.



![Dashboard 1](https://github.com/m-romanski/dsc-phase1-project-LRM/assets/137821058/692a7195-8250-4f00-841f-8d58446d63c4)


