Instructions
The UK Food Standards Agency evaluates various establishments across the United Kingdom, and gives them a food hygiene rating. 
You've been contracted by the editors of a food magazine, Eat Safe, Love, to evaluate some of the ratings data in order to help their journalists and food critics decide where to focus future articles.


Code source:
#Search within 0.01 degree on either side of the latitude and longitude. OpenAI. (2022). ChatGPT, personal communication. March 12, 2024
#Sort by hygiene score

#define search parameters
latitude = 51.5074
longitude = 0.1278

degree_search = 0.01
latitude_min = latitude - degree_search
latitude_max = latitude + degree_search
longitude_min = longitude - degree_search
longitude_max = longitude + degree_search

query = {
    "geocode.latitude": {"$gte": latitude_min, "$lte": latitude_max},
    "geocode.longitude": {"$gte": longitude_min, "$lte": longitude_max},
    "RatingValue": 5
}
sort = [("scores.Hygiene", 1)]
limit = 5
results = establishments.find(query).sort(sort).limit(limit)

#Print the results
for result in results:
    pprint(result)
