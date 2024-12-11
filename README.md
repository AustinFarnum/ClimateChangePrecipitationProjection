# Precipitation Projection Downscaler
Austin Farnum (farnum@udel.edu) and Carolyn Voter, University of Delaware

## Note: Project Status
This project is currently underway. The code contained within serves as an example of what has been accomplished thus far, but it has not yet been prepared for use by others without modification. Additional edits are forthcoming, but feel free to reach out if you have immediate interest.

### Upcoming Tasks:
- [x] Develop method for pseudo temporal downscaling of coarse-resolution precipitation time series
- [x] Create Python tool which automatically performs downscaling
- [x] Perform pilot test of method
- [ ] Expand testing to include 50 locations within continental US
- [ ] Complete further analysis of test results
- [ ] Make code universally accepting of different data types, sources, etc.
- [ ] Write full tutorial on running and modifying the tool as needed
- [ ] Publish paper on the method

## Motivation
This tool was made to solve a problem I faced while trying to predict the impacts of climate change on a site's stormwater system. To predict the changes in precipitation due to climate change, I downloaded a precipitation time series from the output of the CONUS 404 model. The time series, however, used an hourly time step. This is a fine resolution time step as far as climate model outputs go, but it is very coarse for stormwater models and other flashy systems. The enclosed tool was written to prepare a precipitation time series that could be used as an input for a stormwater model by means of pseudo temporal downscaling. This prepared time series considers the climate model's predictions of climate change, but can have a finer time step than that which the climate model provides. The tool is designed for surface water modelers, stormwater engineers, those studying climate change, and more.

## How does it work?
The tool accepts three time series inputs:
- Climate model precipitation time series which represents past conditions
- Climate model precipitation time series which predicts future conditions
- Historically observed precipitation time series measured at your study site

The tool uses the Gumbel (type-I generalized extreme value distribution) cumulative distribution function (CDF) which is used to represent the distribution of maxima and minima within a sample. It finds the CDF value corresponding with each precipitation intensity in the three supplied time series. The tool uses a multiplicative delta method by finding the ratio of the future:past modeled precipitation intensities. The historically observed precipitation intensity with the same CDF value can then be multiplied by the associated delta to project the historically observed time series into the future. Because of this methodology, the two modeled time series provided by the user should be obtained from the same climate model for the minimization of bias in the output.

## Implications
There are two primary consequences associated with the use of this method:
1. The projected time series which is output by the tool will maintain the time step of the historically observed time series you provide, so the temporal resolution of your product is limited by the frequency of rain gauge measurements, not the time step of the climate model.
2. The projected time series maintains the storm frequency of the historically observed data, changing only the magnitude/intensity of precipitation. 

The simplification of climate change's effects to only changes in precipitation magnitude has a benefit relating to the reception of the stormwater modeling project's results. When the project's stakeholders, those who will ultimately receive your results and act upon your recommendations, do not commonly work with time series data or stormwater, this simplification is beneficial because it relates possible future conditions to past events contained within the observed historical time series. 

> "Remember the damage caused by Hurricane Sandy in 2012? If the same storm were to hit this area in the year 2050, the flooding is expected to be XX% more extensive and the damage would be YY% greater."