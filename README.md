# Impacts of Safety Precautions on COVID-19

*By Grace Jiang, Dana Cohen*

We wanted to conduct an experiment to see how safety guidelines such as social distancing and wearing a mask can affect the spread of viruses such as COVID-19.

![demo](assets/demo.gif)



---


### I. Experiment Setup

**A. Independent Variables**

We modified 2 independent variables in this experiment:


- **Degree of Social Distancing** (`density-people`): We quantified the degree of social distancing by introducing a new variable, density-people. Higher densities represent a lower degree of social distancing, and vise versa.
- **% Population Wearing Mask** (`pct-wearing-mask`): Percentage of population wearing a mask. This percentage directly affected the infectiousness of the disease (infectiousness) in the following way:
    - **Mask Off**: When two turtles both did not wear a mask, we used an infection rate of 99%.
    - **Mask On**: When at least one of the turtles wore a mask, we used an infection rate of 20%, calculated from a [Beijing study](https://www.cdc.gov/coronavirus/2019-ncov/more/masking-science-sars-cov2.html).





**B. Control Variables**

While testing each of the independent variables, we treated all the other independent variables as control variables, each with their own default value as listed below:

- **Degree of Social Distancing** (`density-people`): 300 people/space
- **% Population Wearing Mask** (`pct-wearing-mask`): 75%

Some other control variables that we kept constant were:

- **Death Rate** (`chance-recover`): 90%. A turtle has a 90% chance of recovering from the virus and becoming immune, and a 10% chance of dying from the virus. We chose this percentage as a high-end estimate to the severity of COVID, especially for older age groups.
- **Virus Duration** (`duration`): 21 days. The virus has a duration period of 21 days before the patient either recovers or dies.




**C. Dependent Variables**

Finally, we looked to several dependent variables to measure the impacts of the independent variables on the spread and impact of the virus. We kept track of several metrics, such as:

- **Percent of Deaths in Population** (`pct-deaths`): This reporter keeps track of the percentage of deaths from the virus happen from the total population. 
- **Percent of Population Affected** (`pct-affected`): This reporter keeps track of the percentage of people affected from the virus from the total population. We defined “affected” as anyone who has been sick from the virus, whether or not they recovered, died, or are still sick.



---

### II. Analysis

To measure how much social distancing and wearing a mask affected the infectiousness and impact of the virus, we looked at two main reporters: % of population affected by the virus and % of population died by the virus.

Here were our summarized results:

**Social Distancing**

```
pd.pivot_table(df, index=['density-people'], values = ['pct-affected'], aggfunc = [np.mean])
```

| pct-wearing-masks | pct-affected mean |
|-------------------|-------------------|
| 0                 | 79.171640         |
| 20                | 75.796601         |
| 40                | 74.638007         |
| 60                | 63.949679         |
| 80                | 45.319220         |
| 100               | 9.954145          |

Our results show a positive correlation between the density of people (lower social distancing) and the percentage of people affected and dead from the virus.

**Wearing Masks**

```
pd.pivot_table(df, index=['pct-wearing-masks'], values = ['pct-affected'], aggfunc = [np.mean])
```

| pct-wearing-masks | pct-affected mean |
|-------------------|-------------------|
| 0                 | 79.171640         |
| 20                | 75.796601         |
| 40                | 74.638007         |
| 60                | 63.949679         |
| 80                | 45.319220         |
| 100               | 9.954145          |

Our results show negative correlation between the percentage of the population wearing a mask and the percentage of people affected and dead from the virus.

To see our full results, please check out our pandas files and our [documentation](https://github.com/gracejiang/covid-modelling/blob/master/Documentation.pdf).



---


### III. Conclusion

In conclusion, our model validates how two key safety guidelines, social distancing and mask-wearing, can decrease the rates of infection transmission and mortality. 

Future modifications to our experiment could include considering factors such as changing infectiousness rate based off if the receiver is wearing a mask (right now, our model only affects infectiousness if the sick person is wearing a mask), varying death rates for the different age groups, and introducing factors such as superspreaders, asymptomatic people, etc.