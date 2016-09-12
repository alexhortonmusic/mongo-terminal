# 10 Queries of a Restaurant Collection

**Provide a query showing just the names (and nothing else) of the Italian restaurants.**

db.restaurants.find({cuisine: "Italian"}, {name: true, _id: false})

**Provide a query showing how many Bakeries have a name that start with M.**

db.restaurants.find({cuisine: "Bakery"}).count()

**Provide a query showing the zip codes (and _id's) of all restaurants with the word "Ice" in their cuisine.**

db.restaurants.find({cuisine: {$regex: /ice/i}}, {"address.zipcode": 1})

**Provide a query showing the street and street number of Chinese restaurants ordered by zip code.**

db.restaurants.find({cuisine: "Chinese"}, {"address.building": 1, "address.street": 1, _id: false}).sort({"address.zipcode": -1})

**Show only the American restaurants in Manhattan.**

db.restaurants.find({borough: "Manhattan", cuisine: "American"}, {name: 1})

**Provide a query showing the restaurants that have been graded exactly 4 times.**

db.restaurants.find({grades: {$size: 4}}, {name: 1})

**Provide a query showing only _id, name and 2 grades from each restaurant on Broadway.**

db.restaurants.find({"address.street": "Broadway"}, {name: 1, grades: {$slice: 2}})

**Provide a query showing the 5 pizza restaurants in the Bronx with the highest score on an evaluation.**

db.restaurants.find({borough: "Bronx", cuisine: "Pizza"}, {name: true, "grades.score": 1}).sort({"grades.score": -1}).limit(5)

**Provide a query to find all of the restaurants in Brooklyn and list only the 21st-30th results when ordered alphabetically by name.**

db.restaurants.find({borough: "Brooklyn"}, {name: true}).sort({name: 1}).skip(20).limit(10)

**Provide a query that returns all pizza and Italian restaurants in reverse alphabetic order.**

db.restaurants.find({$or: [{cuisine: "Pizza"}, {cuisine: "Italian"}]}).sort({name: -1})
