# Covid_Search_Trends_by_State

## Overview of Project

  ### Background
  
  December of 2019 marked the first record of an unknown pneumonia virus in Wuhan, China.  By mid-January, the virus was identified as a novel coronavirus and the first case is recorded in Washington State, USA.  The WHO declared a global pandemic on March 11, 2020.  The first Covid 19 vaccine was cleared throught the FDA Emergency Use Authorization in December 2020. (CDC 2022)  According to the New York Times, vaccination rates are clearly divided along political lines. (NYT 2021) 
  
  This begs the question, what other Covid-19 related behavior can be correlated along political lines? Knowing that humans tend towards confirmation bias, or a pattern of seeking out information that affirms their current beliefs (Britannica 2019), **can a state's dominant political party be predicted by Google search trends on Covid and vaccination?** 
  
  ### Deliverables
   - Presentation
   - Database
   - Machine Learning Model
   - Interactive Dashboard
 
  ### Resources
   - Technology: SQLite, SQL Alchemy, Visual Studio Code, Jupyter Notebook, Python 3.7, Tableau, Postgres, PGAdmin
   - Data Sources 
     - [Google Trends](https://trends.google.com/trends/?geo=US):  Google Trends outputs data that can be downloaded as CSV files based on input parameters determined by the user.  Various Covid-related search terms were viewed across state lines, from November 30, 2019 to April 21, 2022.  
     - [MIT Election Data + Science Lab](https://electionlab.mit.edu/data): Election results are available for federal, state, and local elections by state, district, county, or precinct. Historical presidential and senate election results were retrieved by state.  MAYBE NOT
     - [Cook Partisan Voting Index](https://worldpopulationreview.com/state-rankings/most-democratic-states): The Partisan Voting Index, PVI, is a measurement of how much a state leans Republican or Democratic compared to the nation as a whole. 

## Analysis
 ### Overview of Code
  - [ETL for Partisan Voting Index](https://github.com/aberloro/Covid_Search_Trends_by_State/blob/main/ETL/ETL_PVI_Data.ipynb)
  - [ETL for vaccine search trends](https://github.com/aberloro/Covid_Search_Trends_by_State/blob/main/ETL/ETL_Vaccine_Data.ipynb)
  - [ETL for what folks call the virus](https://github.com/aberloro/Covid_Search_Trends_by_State/blob/main/ETL/ETL_Virus_Search_Terms_Data.ipynb)
  - [ETL for related search terms](https://github.com/aberloro/Covid_Search_Trends_by_State/blob/main/ETL/ETL_Related_Search_Terms_Data.ipynb)
  - [ETL for past presidential election results](https://github.com/aberloro/Covid_Search_Trends_by_State/blob/main/ETL/ETL_Presidential_Data.ipynb)
  - [Logistic Regression and feature selection](https://github.com/aberloro/Covid_Search_Trends_by_State/blob/main/Machine_Learning/LogisticRegression.ipynb) 


 ### Initial Data Exploration 

  - A scatter plot shows some linear separation of political party (party_id) both with and without the state_rank feature.  There is expeced overlap which accounts for swing states. 

    Scatter plot *without* state_rank feature:
 
    ![features_vax_no_rank](https://user-images.githubusercontent.com/93740725/166132774-c10a2365-d2f7-4e8f-a533-d2429fe176d9.png)


    Scatter plot *with* state_rank feature:

    ![features_vax2_with_rank](https://user-images.githubusercontent.com/93740725/166132791-8d512d7a-a358-4977-9fe4-f3e21f5d7216.png)



 ### Postgres Database
 
  - This project utilized a locally hosted Postgres database accessed through the PGAdmin management tool. 
  - [Schema](https://github.com/aberloro/Covid_Search_Trends_by_State/blob/main/SQL/schema)
  - [Query](https://github.com/aberloro/Covid_Search_Trends_by_State/blob/main/SQL/queries) to join tables
  - [ERD](https://github.com/aberloro/Covid_Search_Trends_by_State/blob/main/SQL/ERD_Text.md) below:
  
    ![ERD](https://user-images.githubusercontent.com/93740725/165023810-e2e79ff1-15c1-4ff6-98b1-758576449b38.png)
   
 ### Machine Learning Model
  - Supervised learning is used when classes are known, in this case Republican or Democrat.
  - This project utilized a logistic regression classification model to predict a state's dominant political party based on covid vaccine srearch trends from that state.
  - Logistic regression was chosen for its ability to handle multiple independent variables and ease of setup compared to neural networks, but is limited by the assumption that relationships in the data are linear.
  - Initial feature selection was narrow, strictly vaccine-related search terms to reduce noise. Features were added iteratively to observe impact on the model. 

 ### Results 
  - A state's dominant political party can be predicted from vaccine search strends *with 85% accuracy* using a logistic regression model. 

  Map of each state's dominant political party as determined by PVI rank:

  ![PVI_map](https://user-images.githubusercontent.com/93740725/166405729-a3e44923-a6e6-47b9-bd37-55f39d38aac5.png)

  Logistic Regression Classification report Results:

  ![classificationReport](https://user-images.githubusercontent.com/93740725/166405775-c18a77b7-661f-43d4-ae2c-24ccb8950099.png)

 
 ### Tableau Dashboard
  - link: [Political Party Search Trends](https://public.tableau.com/views/draft_16514494708920/PVIRank_1?:language=en-US&:display_count=n&:origin=viz_share_link) 
  - storyboard
  
    ![storyboard](https://user-images.githubusercontent.com/93740725/166133020-076c8a16-c4a1-4094-9aa9-3fef9aa09ac2.png)

  - Final product:

    ![Dashboard](https://user-images.githubusercontent.com/93740725/166405788-1ab371f6-949a-4faf-b7ce-26d0bfa933cd.png)


### Presentation
 - Please click [here](https://docs.google.com/presentation/d/1wsX42ik5_tP_MOTY9e7HShyg4vSNRknh32vvGKSwO0c/edit?usp=sharing) to see the deck.
 
## Summary
  ### Conclusions
  ### Limitations
  ### Additional Analysis

## Citations
CDC 2022, *CDC COVID-19 Timeline*, accessed 2022-4-21, [<cdc.gov/museum/timeline/covid19>](https://www.cdc.gov/museum/timeline/covid19.html) 

The New York Times 2021-09-27, *Red Covid*, accessed 2022-04-21, [<nytimes.com/2021/09/27/briefing/covid-red-states-vaccinations>](https://www.nytimes.com/2021/09/27/briefing/covid-red-states-vaccinations.html)

Britannica 2019, *Confirmation Bias*, accessed 2022-04-21, [<britannica.com/science/confirmation-bias>](https://www.britannica.com/science/confirmation-bias)

Harvard Dataverse 2020, *U.S. President 1976–2020*, MIT Election Data and Science Lab, accessed 2022-04-21, [<electionlab.mit.edu/data>](https://electionlab.mit.edu/data)

Google Trends 2022, accessed 2022-04-21, [<trends.google.com/trends>](https://trends.google.com/trends/?geo=US)
