# Miniproject 2

### [Assignment](assignment.md)

## Project/Goals
Using multiple API's (FourSquare and Yelp) to pull bar data from my surronding area, combining the API data into 1 database that shows the ratings pulled from each API.

## Process
1st thing that I looked to do was pull information from the API's themselves, as well as deciding what information to pull and agregate from each one.  I pulled up bars from my location in a 10 km radius.  Each API i pulled 50 bars from as 50 was the limit to returning i could get.
I decided on pulling name, adress and rating for each location so I parsed the API return for where the information was located.
Next I used a for loop to pull the ratings from each FourSquare Bar up, as the ratings where not able to be included in the initial pull.  Yelp was able to get all the information I needed in 1 pull while FourSquare required 1 + 47 pulls for the ratings.
After getting all the information individually for each API I placed the seperate information into lists then combined the lists into 2 dataframes, 1 for Yelp and 1 for FourSquare, I then combined these dataframes into a single dataframe then pushed the dataframe into a database using to_sql.
With everything done I could then pull whatever information I needed out of that database.

## Results
FourSquare had far less coverage of my specific area.  Returning only 47 of the 50 requests as well as having many of the returned values be missing a rating.  Yelp on the other hand satisfied any of the information that I wanted with a single pull, returning 50 which leaves room for possibly more being available if there wasnt the limit on returning only 50.



## Challenges 
![image](https://user-images.githubusercontent.com/104863463/183215089-dabcc7bb-5edc-4803-907c-947c246ebd4f.png)

The biggest issue I had with this project was dealing with the missing ratings from the FourSquare API as well as how to deal with those values in SQLite.  I had originally assigned the missing values to np.nan but when placeing and sorting those into the database, they were appear at the top when sorting from DESC so that if I asked for the top 10 rated bars, I would recieve 10 bars with rating nan.  To deal with this I assigned the missing ratings to -1.  I also needed to cast the ratings sorting to an integer as it was reading then alphabetically.

## Future Goals
If i had more time I would expand the information that is pulled from the API.  Including information about the ratings such as how many votes went into the rating, as well as more information about the place such as email and phone number.
