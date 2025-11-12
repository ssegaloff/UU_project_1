# UU_project_1 Ukraine Conflict Monitor Dataset
The goal of this project is to non-parametrically model a phenomenon of interest (in our case, civilian infrastructure damage in Ukraine starting on February 24, 2022) and to generate sequences of values.

e.g. 
- If one type of infrastructure was hit, what is the probability that the next damage occurs to a certain type of infrastructure?
- If a region is hit, which region has the highest probability of being hit next?

## Accessing the Data:

To access this data, one must register with ACLED for an account with the appropriate permissions and then should visit https://acleddata.com/curated/data-attacks-ukrainian-infrastructure. (We could not acquire those permissions, but Professor Johnson could, so we acquired the data through him.)

## EDA

### Dataset Overview:

24,269 records, 18 columns, covering Feb 2022 – Oct 2025.

27 oblasts (regions), 113 rayons (districts), 25 infrastructure types.

### Key distributions:

Top oblasts: Donetska (6,095), Dnipropetrovska (4,053), Kharkivska (3,393).

Top infrastructure: Industrial (21%), Education (21%), Electricity (12%).

### Temporal trends:

Surge in September 2024 linked to Russian strategic attacks on energy infrastructure.

### Missing data:

date_of_event missing in 26%, rayon missing in 36%, if_other_what and additional_sources missing in ~87%.

### Action taken:

Dropped rows missing oblast.

Used _internal_filter_date as a proxy for missing event dates.

Modeled at the oblast level due to rayon sparsity.

----------------------------------------------------------------------------

## Method Chosen

Non-parametric approach:

First-order Markov Chain to model sequential infrastructure damage patterns.

States = infrastructure types or oblasts.

Transition probabilities were computed from the temporal ordering of events.

----------------------------------------------------------------------------

## Model Chosen

Markov Transition Mode

Visualization:

Heatmaps of top transitions.

Comparison of observed versus steady-state distributions.

---------------------------------------------------------------------------
## Simulations

Simulations run to create new sequences for both phenomena. Generated sequences of length 10001.

Compared simulated distributions with actual distributions.

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