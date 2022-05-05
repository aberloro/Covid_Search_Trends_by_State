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
     - [MIT Election Data + Science Lab](https://electionlab.mit.edu/data): Election results are available for federal, state, and local elections by state, district, county, or precinct. Historical presidential and senate election results were retrieved by state.  
     - [Cook Partisan Voting Index](https://worldpopulationreview.com/state-rankings/most-democratic-states): The Partisan Voting Index, PVI, is a measurement of how much a state leans Republican or Democratic compared to the nation as a whole. 

## Analysis
 ### Overview of Code
  - [ETL for Partisan Voting Index](https://github.com/aberloro/Covid_Search_Trends_by_State/blob/main/ETL/ETL_PVI_Data.ipynb)
  - [ETL for vaccine search trends](https://github.com/aberloro/Covid_Search_Trends_by_State/blob/main/ETL/ETL_Vaccine_Data.ipynb)
  - [ETL for what folks call the virus](https://github.com/aberloro/Covid_Search_Trends_by_State/blob/main/ETL/ETL_Virus_Search_Terms_Data.ipynb)
  - [ETL for related search terms](https://github.com/aberloro/Covid_Search_Trends_by_State/blob/main/ETL/ETL_Related_Search_Terms_Data.ipynb)
  - [ETL for past presidential election results](https://github.com/aberloro/Covid_Search_Trends_by_State/blob/main/ETL/ETL_Presidential_Data.ipynb)
  - [Logistic Regression model and feature selection](https://github.com/aberloro/Covid_Search_Trends_by_State/blob/main/Machine_Learning/LogisticRegression_Segment4.ipynb) 
  - [Random Forest model and feature selection](https://github.com/aberloro/Covid_Search_Trends_by_State/blob/main/Machine_Learning/RandomForest_Segment4.ipynb)


 ### Initial Data Exploration 
  - A map of each state's dominant political party as determined by PVI rank:

    ![PVI_map](https://user-images.githubusercontent.com/93740725/166861714-ca7f0adf-6a14-43d5-a0a0-a53b61de0b53.png)

  - A scatter plot shows some linear separation of political party (party_id) with vaccine search features.  There is expected overlap which accounts for swing states. 

    ![features_vax](https://user-images.githubusercontent.com/93740725/166858322-05b36b6b-e920-4202-aa35-de4f8cb69794.png)

  - A bar chart shows the relative importance of each vaccine search term in the most democratic state (Vermont) compared to the most repblican state (Wyoming). 

    ![exploratory_bar](https://user-images.githubusercontent.com/93740725/166859172-f622e032-6823-4260-858a-ac2c18ae7dcc.png)

 ### Postgres Database
 
  - This project utilized a locally hosted Postgres database accessed through the PGAdmin management tool. 
  - [Schema](https://github.com/aberloro/Covid_Search_Trends_by_State/blob/main/SQL/schema)
  - [Queries](https://github.com/aberloro/Covid_Search_Trends_by_State/blob/main/SQL/queries) to join tables
  - [ERD](https://github.com/aberloro/Covid_Search_Trends_by_State/blob/main/SQL/ERD_Text.md) below:
  
    ![ERD](https://user-images.githubusercontent.com/93740725/165023810-e2e79ff1-15c1-4ff6-98b1-758576449b38.png)
   
 ### Machine Learning 
  - Logistic Regression Classfication Model
    - Supervised learning is used when classes are known, in this case Republican or Democrat.
    - Model was trained to predict a state's dominant political party based on covid vaccine search trends from that state.
    - Chosen for its ability to handle multiple independent variables and ease of setup compared to neural networks.
    - Limited by the assumption that relationships in the data are linear.
  - Feature Selection: 3 main categories
    - What do folks call the virus?
    - How do folks look up vaccine info?
    - Other related Covid searches? 
  - All 3 categories were important to training the logistic regression model:
 
    ![accuracy_summary_logistic_regression](https://user-images.githubusercontent.com/93740725/166861132-aa3896ad-722a-4a57-8734-98d94aa9a884.png)
  - A Random Forest algorithm was also trained and tested for comparison against logistic regression, with similar accuracy:
    
    ![accuracy_summary_random_forest](https://user-images.githubusercontent.com/93740725/166861194-617010e8-f115-43b3-8153-95e213fbec1c.png)


 ### Results 
  - A state's dominant political party can be predicted from covid relates search strends *with 92% accuracy* using a logistic regression model. 
  - Logistic regression confusion matrix:
     
     ![confusion_matric_logistic_regression](https://user-images.githubusercontent.com/93740725/166861954-b85b5996-9304-417d-b19c-00b2449c65af.png)

  - Logistic regression classification report results:

    ![classification_report_logistic_regression](https://user-images.githubusercontent.com/93740725/166861838-0b62cb92-0e4e-489f-aa45-0bdb46eb71a2.png)

  - Precision, or positive predicitve value, shows how likely is it that a categoization was correct.  
     - Democratic states: 83% precision or 5 out of 6 predictions were correct.
     - Republican states: 100% precision, or 7 out of 7 predictions.
  - Secsitivity, or recall, shows how many were correctly categorized. 
     - Democrat states: 100% recall, or 5 out of 5 democratic states were correctly categorzed.
     - Republican states: 88% recall, or 7 out of 8 republican states were labeled correcctly. 
 
 ### Tableau Dashboard
  - link: [Political Party Search Trends](https://public.tableau.com/views/draft_16514494708920/CovidVaccineSearchTrendsbyState?:language=en-US&:display_count=n&:origin=viz_share_link) 
  
     ![Dashboard](https://user-images.githubusercontent.com/93740725/166405788-1ab371f6-949a-4faf-b7ce-26d0bfa933cd.png)


### Presentation
 - Please click [here](https://docs.google.com/presentation/d/1wsX42ik5_tP_MOTY9e7HShyg4vSNRknh32vvGKSwO0c/edit?usp=sharing) to see the  deck.
 - Please click here to see the video. 
 
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

Journal of Medical Internet Research 2020-11, *Covid-19-Related Internet Search Patterns Among People in the United States*, accessed 2022-04-21, [<https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7685696/>](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7685696/)
