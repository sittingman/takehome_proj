# Ultimate User Retention Analysis

### Overview:

Ultimate Technologies Inc. is an American worldwide online transportation network company that has disrupted the taxi and logistics industry and is a prestigious company to work at. This challenge has been adapted from an actual Ultimate Inc. data science challenge.

### Objectives:

 1. Exploratory data analysis: aggregate login timestamps into 15-minutes time intervals, and identify any useful patterns on demand.
 2. Experiment and metrics design: develop statistical tests on measuring key metrics, provide recommendations with caveats.
 3. Predictive modeling: develop a classification model to help predict client retention.

### Findings

#### [Part 1 - Exploratory data analysis](https://github.com/sittingman/takehome_proj/blob/master/ultimate_challenge/part_1.ipynb)

- The login frequency is mostly high during weekends, starting Friday night till Saturday early morning before 5 am. The same peak appears on Saturday night and lasts till Sunday morning before 5 am.
- The usage during weekdays is lower, though lunch hours appear to be a popular time for users to login Monday through Friday.
- The login rate increase over time, and reach a peak on March 1st around 4-5 am. Perhaps there was a special overnight event that happened on that day.

#### [Part 2 - Experiment and metrics design](https://github.com/sittingman/takehome_proj/blob/master/ultimate_challenge/part_2.ipynb)

- Key metrics: mean number of cross cities routes (denoted as **tp**) that drivers make during weekdays before and after (pre-post approach)
- Statistical Test: 1 tail test on difference in **tp** after and before, denoted as **tp_delta** to be > 0 
- Caveats: reimbursement of toll fees may not be effective if one of the following factors occur:
    1. Lack of demand for trips across cities could be driven by competitive options (e.g., trains, buses, ferries)
    2. Drivers have no motivation to serve across cities trip based on factors beyond the toll fees (e.g., traffic congestion, government regulations)
    
#### [Part 3 - Predictive modeling](https://github.com/sittingman/takehome_proj/blob/master/ultimate_challenge/part_3.ipynb)

Per exploratory analysis and statistical tests, the following are selected as features. Target is whether a user will use the service for the preceding 30 days.

- **city**: city this user signed up in
- **phone**: primary device for this user
- **avg_surge**: The average surge multiplier over all of this user’s trips
- **surge_pct**: the percent of trips taken with surge multiplier > 1
- **ultimate_black_user**: TRUE if the user took an Ultimate Black in their first 30 days; FALSE otherwise
- **trips_in_first_30_days**: the number of trips this user took in the first 30 days after signing up

**Results**

|Model | Accuracy |
| --- | --- |
| Baseline | 63.38% |
| Random Forest | 75.23% |
| Catboost | 76.78% |
| Lightgbm | 76.75%|

**Recommendation**

- Provide some incentives to users who a significant portion of their trip with multiplier > 1.
- Identify reasons for high loyalty in King's landing city, expanding marketing and recruiting efforts in Astapor and Waterfell.
- Revisit the user experience in the Android apps, which has a lot lower retention rate than iPhone.