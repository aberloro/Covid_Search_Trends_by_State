party_index
-
party varchar pk
party_id int


partisan_voting_index
-
state_name varchar pk
state_rank int
party varchar fk - party_index.Party

presidential_results
-
state_name varchar pk fk - partisan_voting_index.state_name
2008 varchar
2012 varchar
2016 varchar
2020 varchar


state_vaccines_ranked
-
state_name varchar pk fk - partisan_voting_index.state_name
vaccine_rank int

virus_search_terms
-
state_name varchar pk fk - partisan_voting_index.state_name
covid int
covid19 int
coronavirus int

vaccine_search_terms
-
state_name varchar pk fk - partisan_voting_index.state_name
covid_vax_cvs int
covid_vax_walgreens int
vax_side_effects int
covid_after_vax int
vax_mandate int

related_search_terms
-
state_name varchar pk fk - partisan_voting_index.state_name
covid_cases int
lockdown int
covid_sypmtoms int
quarantine int
stimulus_check int