# movielens-recommender-system
In the increasingly saturated digital streaming landscape, the primary challenge for platforms is no longer just content acquisition, but content discoverability. 'User decision fatigue', which is the paradox of having too many choices, directly leads to platform abandonment and increased churn rates.

This project addresses this critical bottleneck by developing a personalized Recommendation Engine using the MovieLens dataset. By implementing a Hybrid Collaborative Filtering approach, the system transforms raw historical rating data into actionable insights, predicting user preferences with high statistical accuracy. 

The objective is to automate the discovery process, delivering a "Top-5" personalized shortlist that maximizes user engagement and extends session duration. For the business, this translates to a more "sticky" product, higher customer lifetime value (CLV), and a competitive edge in providing a frictionless, hyper-personalized user experience.

Data Understanding
 It contains 100836 ratings and 3683 tag applications across 9742 movies. These data were created by 610 users between March 29, 1996 and September 24, 2018. This dataset was generated on September 26, 2018.

 **2.2.1: Dataset Composition**
<br>

This dataset provides a comprehensive look at the intersection of cinema and user behavior, organized across four primary relational files.

   * *Movie Metadata (`movies.csv`)*
 <br>

The foundation of the dataset. This file catalogs individual films through three core attributes: Unique Identification, Descriptive Titles which includes the movie name and the year of release in parentheses (e.g., "Toy Story (1995)") and Genre Categorization.

 * *User Engagement (`ratings.csv` & `tags.csv`)*
 <br>

These files capture how audiences interact with the films. The `ratings.csv` file records user sentiment on a 5-star scale, utilizing half-star increments for precise evaluation. The `tags.csv` file contains user-generated metadata. Both files utilize UTC timestamps to record the exact second a rating or tag was applied, allowing for time-series analysis.

 * *External Connectivity (`links.csv`)*
 <br>

To expand the scope of analysis, this file provides a bridge to global film databases by mapping the internal movieId to external identifiers, specifically imdbId and tmdbId. These links allow you to pull additional rich data—such as cast, crew and high-quality posters—directly from IMDb and The Movie Database (TMDB).



F. Maxwell Harper and Joseph A. Konstan. 2015. The MovieLens Datasets: History and Context. ACM Transactions on Interactive Intelligent Systems (TiiS) 5, 4: 19:1–19:19. https://doi.org/10.1145/2827872