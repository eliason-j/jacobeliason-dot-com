---
title: Preparing data from Strava for analysis
author: 'Jacob Eliason'
date: '2021-04-30'
slug: processing-strava-data
categories: []
tags:
  - rstats
draft: false
output:
  html_document:
    toc: yes
---



Hi, I'm Jacob and I like to run. When I run, I use [Strava](https://www.strava.com/) to log my activity. In honor of recently running my one-thousandth mile on Strava, I thought I'd do a write up for the steps I use to process my user data in R. The data Strava makes available is granular and can be used for all kinds of fun things after the steps detailed here.

![](2021-04-30-processing-strava-data-nyc.png)

## 1. Export your data {#s1}

Per the [instructions](https://support.strava.com/hc/en-us/articles/216918437-Exporting-your-Data-and-Bulk-Export) on their website, you can export your Strava activity data by navigating to your profile in a web browser and following *Settings* > *My Account* > *Download or Delete your Account - Get Started* > *Request Your Archive*. From that point, it takes me about 10 minutes to see a download link in my inbox.

The download apparently includes a lot of different kinds of data but the most salient (for my account, anyway) are contained in `activities.csv` and the `activities/` directory. The former contains summary information for each of my Strava activities and the latter contains individual files, each of which have second-to-second position data for an individual run, hike, or bike ride. The activity files appear to be some kind of custom or proprietary exercise file type--the two extensions I notice are `.gpx` and `.fit.gz`. At first glance, I don't recognize either. 

Fortunately, as usual I find that someone else has already done the heavy lifting for the most important part of this process. The Github packages [`FITfileR`](https://github.com/grimbough/FITfileR) and [`trackeR`](https://github.com/trackerproject/trackeR) can be used to convert these file types into something more legible. Special thanks to [Mike Smith](https://github.com/grimbough) for his excellent work on the former.

## 2. Unpacking `.gpx` and `.fit.gz` files {#s2}

I start by installing the Github packages and loading those along with the `tidyverse`.





















