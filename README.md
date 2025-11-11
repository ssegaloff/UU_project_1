# UU_project_1 Ukraine Conflict Monitor Dataset

The goal of this project is to non-parametrically model a phenomenon of interest (in our case, Infrastructure Damage in the Ukraine during starting on February 24, 2022) and generating sequences of values.

e.g. 
- if one type of infrastructure was hit, what's the probability that next damage to certain type of infrastructure

- if a region is hit, which region has the highest probability of being hit next

## EDA

### Dataset Overview:

24,269 records, 18 columns, covering Feb 2022 – Oct 2025.
27 oblasts (regions), 113 rayons (districts), 25 infrastructure types.


### Key distributions:

Top oblasts: Donetska (6,095), Dnipropetrovska (4,053), Kharkivska (3,393).
Top infrastructure: Industrial (21%), Education (21%), Electricity (12%).


### Temporal trends:

Surge in Sep 2024 linked to Russian strategic energy attacks.


### Missing data:

date_of_event missing in 26%, rayon missing in 36%, if_other_what and additional_sources missing in ~87%.


### Action taken:

Dropped rows missing oblast.
Used _internal_filter_date as proxy for missing event dates.
Modeled at oblast level due to rayon sparsity.


----------------------------------------------------------------------------
## Method Chosen
Non-parametric approach:

First-order Markov Chain to model sequential infrastructure damage patterns.
States = infrastructure types or oblasts.
Transition probabilities computed from temporal ordering of events.


----------------------------------------------------------------------------
## Model Chosen

Markov Transition Mode

Visualization:

Heatmaps for top transitions.
Comparison of observed vs steady-state distributions.


---------------------------------------------------------------------------
## Results

### Infrastructure-level findings:

Education → Education (62%), Industrial → Industrial (38%), Electricity → Electricity (33%).
Cross-type transitions: Industrial → Electricity (10%), Electricity → Gas (9%).


### Region-level findings:

Donetska → Donetska (64%), Dnipropetrovska → Dnipropetrovska (52%).
Most likely next regions after Donetska: Dnipropetrovska (8%), Kharkivska (7.5%).


### Steady-state:

Infrastructure: Industrial (20.8%), Education (20.7%), Electricity (12.4%).
Regions: Donetska (25%), Dnipropetrovska (16.7%), Kharkivska (14%).


-------------------------------------------------------------------------------
## Limitations

### Model assumptions:

Memoryless and time-homogeneous transitions oversimplify real escalation dynamics.

### Ignored factors:

Geographic clustering, strategic objectives, seasonal targeting.