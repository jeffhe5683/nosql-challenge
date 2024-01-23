
# **Instructions**
The UK Food Standards Agency evaluates various establishments across the United Kingdom and gives them a food hygiene rating. You've been contracted by the editors of a food magazine, Eat Safe, Love, to evaluate some of the ratings data in order to help their journalists and food critics decide where to focus future articles.

Files
NoSQL_setup.ipynb is to set up and update the database. The data provided in the establishments.json file (in the Resources folder) was imported from the Terminal in Jupyter Notebook with:
mongoimport --type json -d uk_food -c establishments --drop --jsonArray establishments.json

NoSQL_analysis.ipynb is to manipulate requested queries and convert results to Pandas DataFrames.

# **Part 1: Database and Jupyter Notebook Set Up**
NoSQL_setup.ipynb
Import the data provided in the establishments.json file from your Terminal. Name the database uk_food and the collection establishments.

Within the notebook, import PyMongo and Pretty Print (pprint) libraries.

Create an instance of the Mongo Client.

Confirm that the database has been created and loaded the data properly.

Assign the establishments collection to a variable to prepare the collection for use.

# **Part 2: Update the Database**
NoSQL_setup.ipynb
The magazine editors have some requested modifications for the database. Make the following changes to the establishments collection:

An exciting new halal restaurant just opened in Greenwich, but hasn't been rated yet. The magazine has asked for it to be included in the analysis. Add the following information to the database:
{
    "BusinessName":"Penang Flavours",
    "BusinessType":"Restaurant/Cafe/Canteen",
    "BusinessTypeID":"",
    "AddressLine1":"Penang Flavours",
    "AddressLine2":"146A Plumstead Rd",
    "AddressLine3":"London",
    "AddressLine4":"",
    "PostCode":"SE18 7DY",
    "Phone":"",
    "LocalAuthorityCode":"511",
    "LocalAuthorityName":"Greenwich",
    "LocalAuthorityWebSite":"http://www.royalgreenwich.gov.uk",
    "LocalAuthorityEmailAddress":"health@royalgreenwich.gov.uk",
    "scores":{
        "Hygiene":"",
        "Structural":"",
        "ConfidenceInManagement":""
    },
    "SchemeType":"FHRS",
    "geocode":{
        "longitude":"0.08384000",
        "latitude":"51.49014200"
    },
    "RightToReply":"",
    "Distance":4623.9723280747176,
    "NewRatingPending":True
}
Find the BusinessTypeID for "Restaurant/Cafe/Canteen" and return only the BusinessTypeID and BusinessType fields.

Update the new restaurant with the BusinessTypeID found.

The magazine is not interested in any establishments in Dover, so check how many documents contain the Dover Local Authority. Remove any establishments within the Dover Local Authority from the database.

Some of the number values are stored as strings, when they should be stored as numbers.

Use update_many to convert latitude and longitude to decimal numbers.
Use update_many to convert RatingValue to integer numbers.
# **Part 3: Exploratory Analysis**
NoSQL_analysis.ipynb
Eat Safe, Love has specific questions they want answered, which will help them find the locations they wish to visit and avoid.

Some notes to be aware of while exploring the dataset:

RatingValue refers to the overall rating decided by the Food Authority and ranges from 1-5. The higher the value, the better the rating.
The scores for Hygiene, Structural, and ConfidenceInManagement are reversed. The higher the value the worse the establishment is in these areas.
Unless otherwise stated, for each question:

Use count_documents to display the number of documents contained in the result.

Display the first document in the results using pprint.

Convert the result to a Pandas DataFrame, print the number of rows in the DataFrame, and display the first 10 rows.

1. Which establishments have a hygiene score equal to 20?
2. Which establishments in London have a RatingValue greater than or equal to 4?
Hint: The London Local Authority has a longer name than "London" so need to use $regex as part of your search.

3. What are the top 5 establishments with a RatingValue of '5', sorted by lowest hygiene score, nearest to the new restaurant added, "Penang Flavours"?
Hint: Compare the geocode to find the nearest locations. Search within 0.01 degree on either side of the latitude and longitude.

4. How many establishments in each Local Authority area have a hygiene score of 0? Sort the results from highest to lowest, and print out the top ten local authority areas.
Hint: Use the aggregation method to answer this.
