# **MOVIELENS RECOMMENDER SYSTEM**
<img src="Images/Recommender_system.jpg">

## **Overview**
In the increasingly saturated digital streaming landscape, the primary challenge for platforms is no longer just content acquisition, but content discoverability. 'User decision fatigue', which is the paradox of having too many choices, directly leads to platform abandonment and increased churn rates.

## **Business Understanding**
This project addresses this critical bottleneck by developing a personalized Recommendation Engine using the MovieLens dataset. By implementing a Hybrid Collaborative Filtering approach, the system transforms raw historical rating data into actionable insights, predicting user preferences with high statistical accuracy. 

The objective is to automate the discovery process, delivering a "Top-5" personalized shortlist that maximizes user engagement and extends session duration. For the business, this translates to a more "sticky" product, higher customer lifetime value (CLV), and a competitive edge in providing a frictionless, hyper-personalized user experience.

## **Data Understanding**
It contains 100836 ratings and 3683 tag applications across 9742 movies. These data were created by 610 users between March 29, 1996 and September 24, 2018. This dataset was generated on September 26, 2018.

 **Dataset Composition**
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

## **Data Preparation**
To ensure the recommendation engine operates on high-quality and consistent data, the following steps were executed:

1. **Data Integration & Aggregation**
<br>

The raw Movielens dataset was distributed across four distinct files. These were harmonized into a single analytical master table.This consequently resulted in a unified dataset that encapsulated metadata, user sentiment (ratings), and  the descriptive context (tags).

2. **Data Cleaning**
<br>

Raw data contains noise that can degrade model performance. The following cleaning protocols were executed:
 - Dropping duplicate entries
 - Imputing missing Values
 - Dropping rows that lacked critical identifiers to ensure only valid interactions remained for the SVD algorithm.

 - Text Standardization by stripping leading and trailing whitespaces, converting to Titlecase.

## **Feature Engineering**

________________________
**Feature Engineering: Content-Based Engine**
________________________
<br>

To enable the system to recommend movies to new users (The Cold Start problem), distinct features were engineered from movie metadata:

 1. **Metadata Soup Construction**

A composite text feature was created by concatenating Genres and User Tags. This ensures the model captures both the explicit category (e.g., "Sci-Fi") and the implicit crowd-sourced sentiment (e.g., "cult classic", "space opera").

 2. **Vectorization (TF-IDF)**:

The data was then transformed into high-dimensional vectors using Term Frequency-Inverse Document Frequency (TF-IDF). 

 3. **Similarity Computation**:
 
A Cosine Similarity Matrix was pre-computed from the TF-IDF vectors, enabling retrieval of semantically similar movies.

________________________
**Feature Engineering: Collaborative Filtering**
________________________
<br>
To capture latent user preferences and handle the dataset's high sparsity:

 1. **Dimensionality Reduction**: 
 
 The interaction matrix (User-Item-Rating) was decomposed using Singular Value Decomposition (SVD).

2. **Latent Factor Extraction**:

The SVD algorithm compressed the sparse user-item matrix into dense low-rank matrices, extracting 150 latent factors that represent hidden patterns in user taste.

 3. **Surprise Format**:

Data was transformed into the specialized format required by the Surprise library, with a rating scale defined strictly between 1.0 and 5.0.

## **Modeling**

The final system employs a Sequential Hybrid architecture to combine the strengths of both models:

 * **Candidate Generation**: 

For a given target movie, the Content-Based Engine retrieves a broad pool of 50 semantically similar candidates.

 * **Personalized Scoring**: 
 
The SVD Engine predicts the specific rating the active user would give to each of these 50 candidates.

 * **Re-Ranking**:
 
The candidates are re-ordered based on these predicted ratings and the Top-N are presented to the user.

 * **Cold Start Handling**: 
 
The logic includes a fail-safe for new users. If a user has no history (and thus no SVD profile), the system gracefully degrades to pure Content-Based recommendations, ensuring functionality for 100% of the user base.

## **Evaluation**

The model was evaluated using a combination of predictive accuracy and ranking metrics to ensure a holistic view of performance:

 1. **RMSE (Root Mean Squared Error)**:
 
Achieved a best-in-class RMSE of 0.86 via SVD tuning, indicating low error in rating prediction.

2. **Precision@10 (0.589)**:

On average, ~60% of the top 10 recommendations are relevant to the user hence directly reducing the "choice paralysis."

 3. **Recall@10 (0.286)**: 

The system successfully captures nearly 30% of a user's total relevant library within just the top 10 suggestions, indicating strong coverage of user interests.

## **Conclusion & Recommendations**

This project successfully designed and deployed a Hybrid Recommendation System tailored to address the "choice paralysis" often faced by users on content streaming platforms. By integrating Content-Based Filtering (using TF-IDF and Cosine Similarity) with Collaborative Filtering (using SVD Matrix Factorization), the final model effectively mitigates the limitations of individual approaches, specifically the "Cold Start" problem and data sparsity.

### **Business Value**
The deployed Hybrid architecture delivers immediate business value in three key areas:

 1. **Enhanced Discovery**: By leveraging "Metadata Soup" (Genres + Tags), the system surfaces niche content that matches specific user interests, driving engagement into the "Long Tail" of the catalog.

 2. **Retention**: The high Precision@10 score directly correlates to reduced search time and lower churn, as users are presented with "watchable" content immediately.

 3. **Scalability**: The architecture decouples retrieval (Content-Based) from scoring (SVD), allowing the system to scale efficiently as the user base grows.

### **Future Recommendations**
To further refine the system for the production environment, the following steps are recommended:

 * **Temporal Dynamics**: Incorporate the timestamp feature to weight recent interactions more heavily hence allowing the model to adapt to drifting user tastes over time.

 * **Deep Learning Integration**: Experiment with Neural Collaborative Filtering (NCF) or Autoencoders to capture non-linear user-item relationships that matrix factorization may miss.

 * **A/B Testing**: Deploy the model in a live environment to measure real-world engagement metrics (Click-Through Rate and Watch Time) against the current baseline.

<br />
<hr />
<p align="center">
  <b>MovieLens Hybrid Recommender System</b>
  <br />
  Dataset obtained from F. Maxwell Harper and Joseph A. Konstan. 2015. The MovieLens Datasets: History and Context. ACM Transactions on Interactive Intelligent Systems (TiiS) 5, 4: 19:1–19:19
  <br />
   All Rights Reserved.
</p>
