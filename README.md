# Bias in Data

Name: Murtaza Jafferji

Date: November 1st, 2018

## Goal
The goal of this project is to investigate and analyze bias in the quality and number of articles about politicians on Wikipedia, based on the nationality of the politicians. In the process, we will create a curated dataset of the counts of articles about politicians, the counts of high quality articles about politicians, and the population for each of 190 countries where we have data from three data sources, described below.

## Data sources used
We will use three data sources to perform our analysis:
1. Politicians by Country from the English-language Wikipedia: https://figshare.com/articles/Untitled_Item/5513449 (CC-BY-SA 4.0)
2. World population dataset, as of mid-2018: https://www.dropbox.com/s/5u7sy1xt7g0oi2c/WPDS_2018_data.csv?dl=0 ([copyright policy](https://www.dropbox.com/terms))
3. ORES (Objective Revision Evaluation Service), via a Wikimedia API endpoint: https://ores.wikimedia.org/

## Resources used
  - [Python 3.X](https://www.anaconda.com/download/)
  - [Jupyter](https://jupyter.org/install.html)
  - [Pandas](http://pandas.pydata.org)
  - [NumPy](http://www.numpy.org/)
  - [Matplotlib](https://matplotlib.org)

## Datasets Created

Wikipedia data with ORES score:
  - Data sources: Wikipedia dataset, ORES
  - Filename: wikipedia_data_with_ores_score.csv
  page	country	rev_id	predicted_quality_score
  - Considerations: A predicted_quality_score of None means that the revision_id was not found by ORES.
  page	country	rev_id	predicted_quality_score
| Header                  | Description                                                                                                   |
|-------------------------|---------------------------------------------------------------------------------------------------------------|
| page                   | Title of the Wikipedia article. This column is not directly used in our analysis.                                                                               |
| country                   | Country of the politician's nationality                                                                               |
| rev_id      | The revision_id of the last edit to the Wikipedia article             |
| predicted_quality_score   | ORES estimate of the quality of the article. Possible values are FA, GA, B, C, Start, Stub, or None |

Politician article counts by country with populaton:
  - Data sources: Wikipedia dataset, ORES, population dataset
  - Filename: politician_article_counts_by_country_with_population.csv
  - Considerations: Data was cleansed in the population dataset in order to correctly map the Geography column to the country column in the Wikipedia dataset; e.g. "St. Kitts-Nevis" was replaced with "Saint Kitts and Nevis". Values where matches were not found in either the Wikipedia dataset or the population dataset were not included in this dataset.

| Header                  | Description                                                                                                   |
|-------------------------|---------------------------------------------------------------------------------------------------------------|
| country                   |  Name of the country                                                                               |
| article count                   | Number of Wikipedia articles that exist about politicians by country                                                                              |
| quality count                   | Number of Wikipedia articles that are classified as quality, meaning scored as FA (Featured artcile) or GA (Good article) by ORES, by country                                                                             |
| population (millions)      | Population for each country, in millions of people            |

## Visualizations Created
![alt text](https://github.com/murtazajafferji/data-512-a2/blob/master/highest_politician_articles_per_capita.png)
![alt text](https://github.com/murtazajafferji/data-512-a2/blob/master/lowest_politician_articles_per_capita.png)
![alt text](https://github.com/murtazajafferji/data-512-a2/blob/master/highest_proportion_high_quality.png)
![alt text](https://github.com/murtazajafferji/data-512-a2/blob/master/lowest_proportion_high_quality.png)

## Findings

In the process of completing this project, we found a number of surprising results. When we began this analysis, we believed that since we're analyzing the English-language Wikipedia, that the highest politican articles per capita and the highest proportion of high quality articles would be dominated by countries where English is the predominant language. 5 out of the top 10 countries with the highest politician articles per capita and 7 out of the top 10 countries with the highest proportion of high quality articles do not have English as an official language. In addition, we were suprised to find that North Korea and Saudia Arabia ranked at the top of the list for the highest proportion of high quality of politician articles. 

However, it was unsurprising to find that the some of the countries with the lowest politician articles per capital have massive populations and are also not countries where English is an official language. Along the same lines, it is reasonable that the countries with the highest politicians per capita have very small populations.

The list of lowest proportion of high quality politician articles raise suspicions for me about the reliability of the ORES for some countries. It seems unreasonable that Belgium and Finland, each with over 500 politician articles, do not have a single high quality article. Thus, ORES may be biasing our analysis. In addition, there seems to be a bias that countries with more controversial political figures have a higher proportion of high quality articles.

## License

This project is licensed under the MIT License - see the [LICENSE.md](https://github.com/murtazajafferji/data-512-a2/blob/master/LICENSE) file for details