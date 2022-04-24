party_index
-
party varchar pk
party_id int

presidential_results
-
state_name varchar pk fk - Partisan_Voting_Index.State_Name
2008 int
2012 int
2016 int
2020 int

partisan_voting_index
-
state_name varchar pk
state_rank int
party varchar fk - Party_Index.Party

state_vaccines_ranked
-
state_name varchar pk fk - Partisan_Voting_Index.State_Name
vaccine_rank int

virus_search_terms
-
state_name varchar pk fk - Partisan_Voting_Index.State_Name
covid int
covid19 int
coronavirus int

vaccine_search_terms
-
state_name varchar pk fk - Partisan_Voting_Index.State_Name
covid_vax_cvs int
covid_vax_walgreens int
vax_side_effects int
covid_after_vax int
vax_mandate int

related_search_terms
-
state_name varchar pk fk - Partisan_Voting_Index.State_Name
covid_cases int
covid_tests int
covid_sypmtoms int
covid_hoax int
covid_lie int