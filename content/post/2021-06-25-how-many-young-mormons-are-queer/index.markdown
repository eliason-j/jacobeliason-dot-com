---
title: How many young Mormons are queer?
author: Jacob Eliason
description:
slug: lgb-mormons-nationscape
date: 2021-06-25
draft: yes
output:
  html_document
---




### Context

* On Monday, [Jana Riess](https://twitter.com/janariess) (who I've admired for some time since reading her fascinating [book](https://www.amazon.com/Next-Mormons-Millennials-Changing-Church/dp/0190885203)) published a [surprising finding](https://religionnews.com/2021/06/21/rising-number-of-adult-mormons-in-the-us-are-gay-lesbian-or-bisexual/) in Religious News Service showing that 18% of Gen Z Mormons are lesbian, gay, or bisexual.
* Jana's findings were picked up by several local and national news sources, including the [Salt Lake Tribune](https://www.sltrib.com/religion/2021/06/21/jana-riess-there-are-more/) and the [Washington Post](https://www.washingtonpost.com/religion/1-in-5-young-adult-mormons-in-the-us-are-gay-lesbian-or-bisexual/2021/06/22/607d764e-d388-11eb-b39f-05a2d776b1f4_story.html). They also generated [some](https://twitter.com/BenjaminEPark/status/1407055962402439168?s=20) [lively](https://twitter.com/patrickqmason/status/1407046811727040512?s=20) [discussion](https://twitter.com/religiongal/status/1407070094488850438?s=20) on social media.
* Today, she posted an update explaining how the true number was probably lower than 18% due to a misunderstanding regarding the Nationscape project's weighting scheme.
* After exploring the [Nationscape dataset](https://www.voterstudygroup.org/publication/nationscape-data-set), I believe we can produce a better estimate for that true, lower number by applying a new weighting scheme to Mormon Nationscape respondents. 

### The problem

According to the Nationscape Representativeness Assessment (included in data download), survey responses are weighted to be representative of the US population. The assessment demonstrates through various comparisons to external sources that "The methodology employed in Nationscape generates estimates of *general population characteristics* [emphasis added] that are...closely aligned with government survey benchmarks...Nationscape estimates should be construed as no more or less valid than the estimates from many commercial non-probability samples, including those from vendors used regularly in political polling, as long as conclusions based on Nationscape estimates are tempered with the appropriate degree of uncertainty (as all estimates from surveys must be)."

As Jana explains in the update to her original post, the problem is that while the weighted responses from the Nationscape dataset as a whole do a reasonably good job at describing the "general population," there is no reason to expect that an arbitrary subset of the data will reasonably describe a corresponding subset of the general population. 

In this case, we're considering the 3,881 respondents (about 1% of the total) who selected "Mormon" in response to the question, "What is your present religion, if any?" Based on these respondents, we'd like to make some inferences about all people in the United States who would describe themselves as Mormon. However, these 3,881 are different from our population of interest in some important ways. How do we know that? We don't know precisely since the Mormon church doesn't publish exact figures for its membership, but there exist some resources that help paint an approximate picture. Pew Research, in particular, has produced a number of resources for Mormon population demographics that seem to me a reasonable baseline for comparison (as I'll mention later, this is among the decisions I'd be happy to replace with something better-informed). 

To give a couple of examples: Pew's Religious Landscape Study [estimated](https://www.pewforum.org/religious-landscape-study/religious-tradition/mormon/#party-affiliation) that in 2014, 70% of US Mormons identified as Republican or leaned Republican. In the Nationscape dataset, 60% of Mormons identified as Republican or leaned Republican. In 2009, Pew [estimated](https://assets.pewresearch.org/wp-content/uploads/sites/11/2012/07/Mormons2revised.gif) using Census-defined regions that 76% of US Mormons lived in the West—however, only 64% of Nationscape Mormons were from the West.

The problem is if Republican Mormons or Mormons from the West are likely to answer the question of interest differently than other Mormons. If we don't do anything about that, we're not going to get a very good estimate of the true population figure.

### Proposed solution

The good news is this: the Nationscape sample is different from its target population too. From the Representativeness Assessment:

>The survey data are...weighted to be representative of the American population. Our weights are generated using a simple raking technique, as there is little benefit to more complicated approaches (Mercer et al. 2018). One set of weights is generated for each week’s survey. The targets to which Nationscape is weighted are derived from the adult population of the 2017 American Community Survey of the U.S. Census Bureau. The one exception is the 2016 vote, which is derived from the official election results released by the Federal Election Commission.
>
>We weight on the following factors: gender, the four major census regions, race, Hispanic ethnicity, household income, education, age, language spoken at home, nativity (U.S.- or foreign-born), 2016 presidential vote, and the urban-rural mix of the respondent’s ZIP code. We also weight on the following interactions: Hispanic ethnicity by language spoken at home, education by gender, gender by race, race by Hispanic origin, race by education, and Hispanic origin by education.

I'm not an expert by any means, but I have some experience implementing weighting schemes like they seem to be describing. On reading that, I wondered if there was any reason a separate weighting scheme couldn't be applied to the Mormon subset alone.

I picked some variables that seemed relevant and that I could find reasonable population estimates for.

* Census region (Pew, 2009)
* Age (Pew RLS, 2014)
* Gender (Pew RLS, 2014)
* Race (Pew RLS, 2014)
* Education (Pew RLS, 2014)
* Party ID (Pew RLS, 2014)

If anybody reads this and has thoughts about what variables or sources might better serve in place of these, please drop a comment below. All of these, and Region in particular, are somewhat dated and I'm sure better sources exist. 

Having compiled the population estimates, I demonstrate the insufficiency of the default Nationscape weighting scheme in describing the population of US Mormons:


|variable          |level               | unweighted| nationscape_wt| population_target|
|:-----------------|:-------------------|----------:|--------------:|-----------------:|
|age_pew           |18-29               |       0.26|           0.26|              0.22|
|age_pew           |30-49               |       0.40|           0.37|              0.40|
|age_pew           |50-64               |       0.21|           0.22|              0.22|
|age_pew           |65+                 |       0.12|           0.16|              0.16|
|census_region_pew |Northeast           |       0.06|           0.05|              0.04|
|census_region_pew |Midwest             |       0.10|           0.09|              0.07|
|census_region_pew |South               |       0.20|           0.21|              0.12|
|census_region_pew |West                |       0.64|           0.65|              0.76|
|education_pew     |High school or less |       0.22|           0.34|              0.27|
|education_pew     |Some college        |       0.42|           0.41|              0.40|
|education_pew     |College grad        |       0.22|           0.15|              0.23|
|education_pew     |Post grad           |       0.14|           0.10|              0.10|
|gender_pew        |Female              |       0.51|           0.52|              0.56|
|gender_pew        |Male                |       0.49|           0.48|              0.44|
|pid_pew           |Democrat            |       0.30|           0.30|              0.19|
|pid_pew           |Republican          |       0.60|           0.59|              0.70|
|pid_pew           |Independent         |       0.10|           0.10|              0.11|
|pid_pew           |NA                  |         NA|             NA|                NA|
|race_pew          |White               |       0.82|           0.79|              0.85|
|race_pew          |Non-white           |       0.18|           0.21|              0.15|


### New results

### Discussion



