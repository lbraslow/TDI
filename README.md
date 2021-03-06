# TDI application proof of concept
## Levi Braslow, February 15, 2021

### Introduction 

Political data science relies heavily on predictive models of voter behavior to inform targeting of campaign resources to individuals and groups.  In the wake of the 2020 general election, data scientists are focusing significant attention and resources to analyzing election results and identifying opportunities to improve existing targeting approaches.  Modeling generally addresses one (or more) of three major tactics used in campaigns - voter registration (influencing someone who is eligible to vote but not registered to become registered), mobilization (influencing someone who is registered to actually vote), and persuasion (influencing a voter to choose a specific candidate).  Typically campaigns will target likely supporters for registration and mobilization efforts, to ensure that they actually cast their ballots, while reserving persuasion resources for registered voters who are believed to be movable or "swing" with regard to the candidates on the ballot.

While many specific campaign tactics are important and deserving of further study, the voter registration to mobilization pathway is historically understudied due to data limitations.  However, conceptually this pathway is believed to be highly efficient, in both the short term and the longer term.  There is some evidence that newly registered voters are more likely than previously registered voters to actually cast a ballot in the election when they first become registered, particularly with ongoing outreach and engagement from campaigns or civic engagement organizations.  Moreover, registering a new voter increases the number of registered voters who can be mobilized in future elections.  Finally, voter registration efforts can begin well before election day (or the beginning of early voting or vote by mail), so these provide an opportunity for campaigns to begin engaging and mobilizing likely supporters in the community early and build their engagement over time leading up to election day.  These efforts are more efficient and cost-effective than ever given the rapid expansion of digital organizing, particularly in the 2020 cycle since more traditional field organizing tactics were severely limited due to the COVID-19 pandemic.

### Data Sources 

For this project, I will integrate data from multiple distinct sources to quantify the relationship between new voter registration and turnout, and to identify the impact of newly registered voters on electoral outcomes.  I will also identify (or estimate) the demographic mix of newly registered voters, particularly whether they fall into key demographic segments of the "Rising American Electorate" or RAE, and their potential impact on electoral outcomes given estimates of their likely voting behavior.  

- The first source is the national voter file (or possibly a specific state, if required - see data source note).  The voter file contains identifiable, person level information about each individual who is registered to vote in a state at the time the file is requested, including their name, date of birth, address (and associated electoral district, county and voting precinct), initial registration date, and whether they cast a vote in a specific previous election and the voting method (election day in person, early in person, or vote by mail).  The voter file may also provide other information, such as party registration, gender or race, depending on the state.

- The second source is data from the US Census American Community Survey, which can be used to estimate the number of eligible voters in a precinct and provide a profile of their demographic and economic characteristics.  The voting eligible population counts will be used in combination with voter file data to estimate the registration rate in a given precinct, and I will test additional demographic and economic variables (particularly age mix, gender, race/ethnicity, income levels, and housing stability) as independent variables in the model.  The most recent available ACS data that provides the necessary level of granularity is the 2019 five-year blend, meaning that the data reflects 2015-2019.  When available, I will also integrate 2020 decennial census information into the model to update the topline CVAP/VEP population counts.

- The third source is precinct level election results.  This will be used to identify which candidate won in a given election in a given precinct, and their win margin. This information will be used in the ultimate final product to illustrate the share of that margin that the newly registered voters who actually voted in a precinct represent, and the extent to which newly registered voters (and newly registered voters of distinct demographic groups) may have swung the election. 

- In future iterations, once data becomes available I will integrate survey data on registration and voting behavior in 2020 from the US Census Current Population Survey (CPS) Voting and Registration Supplement (November Supplement). This data will likely become available in late 2021 or early 2022.

- In future iterations, I am also interested in comparing the 2020 analysis to findings if the same model were run in previous general elections, and to identify to what extent the patterns observed in 2020 are consistent or not consistent with prior Presidential election cycles.  All of the data sources identified above are readily available for the 2016 election cycle, and are available in some form for earlier elections as well.

I am also very interested in adding a digital organizing / social listening angle to this project, using data from one or more of the social or search platform APIs to identify any correlation between online discourse (organic and/or paid ads) about registering to vote and actual voter registration trends by date.  I have not yet identified an appropriate solution to pull historical data in a usable format that is publicly available, but will be exploring this further.

### Proof of Concept

While this is clearly a more extensive project, as a proof of concept I have provided three models and plots with some sample code.

Model 1 - illustrates that there is a statistically significant positive relationship between the percent of the voting population who are new voters in 2020 and the percent of the population who are BIPOC (other than white alone non-hispanic) at the zip code level.

Model 2 - illustrates that there is a statistically significant positive relationship between the percent of the voting population who are new voters in 2020 and the percent of the population who are renters (not homeowners) at the zip code level.  The coefficient for the main predictor and the R^2 value for model 2 are marginally greater than in model 1.

Model 3 - multivariate model indicating that race and renter status are both significant, independent predictors of the percent of the voting population who are new voters in 2020. Includes and interaction term of the two predictors.  

Model comparison ANOVA indicates that the two bivariate models (model 1 and model 2) are similar and there is no statistically significant difference between them, while model 3 is significantly better than either model 1 or model 2.



