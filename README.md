# Task1-Netflix-data-cleaning
Task1-Netflix-data-cleaning
📌 Task Overview: Netflix Dataset Analysis
This task involves:

Data loading

Data cleaning and preprocessing

Data exploration and visualization
to gain insights into Netflix's movie catalog.

✅ Step-by-Step Breakdown
1. File Upload
python
Copy
Edit
from google.colab import files
uploaded = files.upload()
This code prompts you to upload the CSV file into the Colab environment.

Once uploaded, the file can be accessed just like a local file.

2. Data Loading
python
Copy
Edit
df = pd.read_csv('netflix_movies_detailed_up_to_2025.csv')
The CSV file is read using pandas.

df.head() shows the first few rows.

df.shape displays the dimensions of the dataset (rows × columns).

3. Data Cleaning
Cleaning ensures data is in a usable, consistent format:

a. Convert date_added to DateTime
python
Copy
Edit
df['date_added'] = pd.to_datetime(df['date_added'], errors='coerce')
Converts the date_added column from string to datetime format.

errors='coerce' replaces invalid dates with NaT (Not a Time).

b. Drop Duplicates
python
Copy
Edit
df.drop_duplicates(inplace=True)
Removes any duplicate rows to ensure accuracy in counting.

c. Clean Text Columns
python
Copy
Edit
text_cols = ['title', 'director', 'cast', 'country', 'rating', 'genre']
for col in text_cols:
    df[col] = df[col].astype(str).str.strip().str.lower()
Ensures uniform formatting by:

Removing extra whitespace.

Converting to lowercase (helps avoid grouping issues like “Action” vs “action”).

d. Split Genres
python
Copy
Edit
df['genre_list'] = df['genre'].str.split(',')
Some movies have multiple genres. This step splits them into lists for analysis.

e. Extract Year from date_added
python
Copy
Edit
df['year_added'] = df['date_added'].dt.year
Helps analyze trends over time.

📊 Data Visualization
The cleaned dataset is visualized to gain meaningful insights.

1. Movies Added per Year
python
Copy
Edit
df['year_added'].value_counts().sort_index().plot(kind='bar')
Shows the number of titles added to Netflix each year.

Helps spot trends like rapid growth or slowdowns.

2. Top 10 Genres
python
Copy
Edit
from collections import Counter
genre_counts = Counter([g.strip() for sublist in df['genre_list'].dropna() for g in sublist])
Aggregates genre appearances across the dataset.

Bar chart visualizes the most popular genres.

3. Content Ratings Distribution
python
Copy
Edit
df['rating'].value_counts().plot(kind='bar')
Displays the number of titles by rating (e.g., TV-MA, PG-13).

Useful for understanding target audience demographics.

4. Top 10 Producing Countries
python
Copy
Edit
df['country'].value_counts().head(10).plot(kind='bar')
Shows which countries contribute most content to Netflix.

Can reveal regional production trends or market focus.

🧾 Summary of Outcomes
Task	Purpose
Upload & Load Data	Access Netflix dataset in Colab
Clean Data	Ensure consistency, remove duplicates, format for analysis
Extract Features	Convert dates, split genres, normalize text
Visualize Trends	Understand Netflix's content by time, genre, rating, and country
