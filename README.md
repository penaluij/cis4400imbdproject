# cis4400imbdproject
https://datasets.imdbws.com/
data comes from imdb website where millions of people review movies/tv shows and IMBD have offical critcs review movies/tv shows and ipdate information for each movie/tv shows, actors, and directors 
1. Data Sourcing:
The project uses IMDB datasets, including:
name.basics.tsv.gz
title.akas.tsv.gz
title.basics.tsv.gz
title.crew.tsv.gz
title.episode.tsv.gz
title.principals.tsv.gz
title.ratings.tsv.gz
These were cleaned from the original raw IMDB TSV files to CSV using scripts in Python. The transformation ensured:
Proper formatting (UTF-8 encoding),


Selection of relevant fields,


Filtering to keep only valid and complete records.


A data dictionary was manually constructed to track the description, data type, and expected values of each field.

2. Data Storage in AWS:
The cleaned CSV files were uploaded to an Amazon S3 bucket, where they were stored in an organized folder structure. Python scripts using boto3 were used to programmatically push these files to the bucket, which enables reusability and automation.
Each dataset had its storage timestamp and path noted for traceability.

3. Data Transformation:
Transformation scripts were written in Python using Pandas to:
Standardize date formats (YYYY-MM-DD),


Split multi-value genre fields to extract primary genres,


Remove rows with missing or duplicate values,


Convert fields like runtime, rating, and year into correct numeric types.


A transformation log and updated data dictionary were maintained. This step also included mapping source columns to destination fields to support modeling and clarity.

 A Dimensional model was also created 

4. Data Integration into AWS Redshift:
After transformation:
A Redshift Serverless data warehouse was set up.


Tables for movies, directors, and ratings were created using CREATE TABLE SQL scripts.


Data was loaded from S3 to Redshift using the COPY command with proper IAM role and region configurations.


Fact and dimension tables were modeled:
Fact Table: Ratings (with Movie ID as foreign key)


Dimension Tables: Movies and Directors



5. Data Serving & Visualization (Tableau):
Tableau was used to create an interactive dashboard titled “IMDB Movie Trends”.
The visualizations include:
Line Chart: Average Movie Rating over Time


Bar Chart: Movie Production Volume by Genre and Year


Pie Chart: Distribution of Movies by Primary Genre


Heat Map: Average Rating by Genre and Year


Filters: Genre and Release Year, allowing dynamic interactivity across all charts



