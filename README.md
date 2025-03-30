# NBA Analytics Pipeline
## Problem Description
This project addresses the challenge of processing, analyzing, and visualizing NBA performance data to identify key factors that contribute to team success. NBA analytics has become crucial in basketball operations, helping teams make data-driven decisions about player evaluation, game strategy, and roster construction.

The NBA Analytics Pipeline provides insights on:
 - Conference and division performance comparisons
 - Scoring pattern evolution over NBA history
 - Statistical indicators most strongly correlated with winning
 - 
Through this end-to-end pipeline, we can access clean, processed NBA data and visualize performance trends through an interactive dashboard.

## Dataset
the data were extracted by [`hoopR`](https://hoopr.sportsdataverse.org/). it is an R package for working with men’s basketball data.
just run this code `dat <- hoopR::load_nba_pbp(seasons = year)` you could collect the NBA data form that seaons.

## Infrastructure
the following tools are used:
 - Cloud: Google Cloud Storage/Google BigQuery
 - Transformation: dbt
 -  
