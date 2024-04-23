# Analysis Summary #
This analysis uses PyMongo to analyze a NoSQL database containing food establishments across the United Kingdom with their business details and their hygiene, management, and structural ratings. The premise is that the editors of a fictitious food magazine, Eat Safe, Love, wants to evaluate ratings data by the UK Food Standards Agency to help their journalists and food critics decide where to focus their future articles. The analysis is done in two Jupyter notebooks, 'NoSQL_setup' and 'NoSQL_analysis'.

## NoSQL_setup ##
'NoSQL_setup' notebook is used to import the 'establishments.json' file containing the data, create the 'uk_food' database, and double checks that the collection and document were uploaded correctly by previewing them. The second part of this notebook updates the database with a new restaurant, 'Penang Flavours', and deletes all documents containing establishments in the Dover Local Authority as the analysis is not interested in this region. I further cleanse the data by updating Penang Flavour's BusinessTypeID to reflect its business appropriately and convert data types stored as string values to integers and floats as necessary. This sets the data up for the next notebook, 'NoSQL_analysis'.

## NoSQL_analysis ##
The analysis aims to answer the below 4 questions:

### Which establishments have a hygiene score equal to 20? ###
Using PyMongo's find query and count_documents, we see that there are 41 establishments with a hygiene score of 20 (out of 25).

###  Which establishments in London have a RatingValue greater than or equal to 4?###
We wanted to take a look at establishments in the London Local Authority that had a RatingValue greater than or equal to 4. Using PyMongo's 'find' method, I created a query with the Rating Value set to greater than or equal to 4 and LocalAuthorityName set to 'London', using '$regex' since some Local Authority Names did not include just an exact match of 'London. Using count_documents, we see that there are 33 establishments in London with a rating value greater than or equal to 4. 

### What are the top 5 establishments with a RatingValue rating value of 5, sorted by lowest hygiene score, nearest to the new restaurant added, "Penang Flavours"? ###
The next set of establishments we wanted to research were the top 5 restaurants with high marks, 5 in RatingValue, and within 0.01 degrees of Penang Flavours' longitude and latitude. The results were then sorted based on the lowest hygiene score. The 5 establishments were 'Howe and Co Fish and Chips', 'Atlantic Fish Bar', 'Plumstead Manor Nursery', 'Iceland,' and 'Volunteer'. The establishments were all different business types: mobile caterer, takeaway/sandwich shop, caring premises, supermarket, and pub/bar. This neighborhood seems to have a diverse selection of high quality food establishments to choose from. 

### How many establishments in each Local Authority area have a hygiene score of 0? ###
Lastly, we wanted to take a look at how many food establishments have hygiene scores of 0 in each Local Authority area, sorted by highest to lowest count. This will give us an idea of which cities may need to take further measures to increase their cleanliness at food establishments. Thanet was the highest region that had the largest count of food spots with a hygiene score of 0 at 1,130 followed by Greenwich at 882. The top 10 on this list had a range from 542 to 1,130 food establishments with a 0 hygiene score. Another data point that we should consider using is total amount of restaurants and these regions. A percentage of total would be more telling than an absolute count since some regions may just be bigger with more food establishments in general. 

The above results were all transformed into a DataFrame using Pandas for futher analysis and easier readability if the editors decide to target these restaurants for review.

See Jupyter notebooks for more details on analysis and conclusions.

# Tools Used #
PyMongo (a Python distribution with tools for working with MongoDB) and Pandas
