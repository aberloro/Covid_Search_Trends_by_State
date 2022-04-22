Party_Index
-
Party varchar pk
Party_ID int

Presidential_Results
-
State_Name varchar pk fk - Partisan_Voting_Index.State_Name
2020 int
2016 int
2012 int
2008 int

Partisan_Voting_index
-
State_Name varchar pk
State_Rank int
Party varchar fk - Party_Index.Party

State_Vaccines_Ranked
-
State_Name varchar pk fk - Partisan_Voting_Index.State_Name
Vaccine_Rank int

Virus_Search_Terms
-
State_Name varchar pk fk - Partisan_Voting_Index.State_Name
Covid int
Covid19 int
Coronavirus int

Vaccine_Search_Terms
-
State_Name varchar pk fk - Partisan_Voting_Index.State_Name
Pro-Vax1 int
Pro-Vax2 int
Neutral int
AntiVax1 int
Antivax2 int

Related_Search_Terms
-
State_Name varchar pk fk - Partisan_Voting_Index.State_Name
Covid_Cases int
Covid_Tests int
Covid_Sypmtoms int
Covid_Hoax int
Covid_Lie int