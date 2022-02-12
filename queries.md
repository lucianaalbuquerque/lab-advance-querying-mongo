![Ironhack Logo](https://i.imgur.com/1QgrNNw.png)

# Answers

### 1. All the companies whose name match 'Babelgum'. Retrieve only their `name` field.

query:       {name: 'Babelgum'} 
Projection: { name: 1 , _id: 0}

### 2. All the companies that have more than 5000 employees. Limit the search to 20 companies and sort them by **number of employees**.

query: { number_of_employees: { $gte: 5000 } } 
sort:  { number_of_employees: 1 }  
limit: 20

### 3. All the companies founded between 2000 and 2005, both years included. Retrieve only the `name` and `founded_year` fields.

query: { founded_year: { $in: [2000, 2001, 2002, 2003, 2004, 2005 ] } } OR { founded_year: { $gte: 2000, $lte: 2005 } } 
projection { name: 1, _id: 0, founded_year: 1}

### 4. All the companies that had a Valuation Amount of more than 100.000.000 and have been founded before 2010. Retrieve only the `name` and `ipo` fields.

query: { founded_year: { $lte: 2010 } , "ipo.valuation_amount" : {$gte: 100000000} } 
projection: { name: 1, ipo: 1, _id: 0}

### 5. All the companies that have less than 1000 employees and have been founded before 2005. Order them by the number of employees and limit the search to 10 companies.

query: { founded_year: { $lte: 2005 } , number_of_employees : {$lte: 1000} } 
SORT: { number_of_employees: 1 } | Limit 10

### 6. All the companies that don't include the `partners` field.

query: { partners: {$exists: false} }

### 7. All the companies that have a null type of value on the `category_code` field.

query: { category_code: { $eq: null } }

### 8. All the companies that have at least 100 employees but less than 1000. Retrieve only the `name` and `number of employees` fields.

query: { number_of_employees: { $lt: 1000 , $gte: 100 } } 
projection { name: 1, number_of_employees: 1, ipo: 1, _id: 0}

### 9. Order all the companies by their IPO price in a descending order.

sort: { ipo: -1 }

### 10. Retrieve the 10 companies with most employees, order by the `number of employees`

sort: { number_of_employees: -1 } 
limit: 10

### 11. All the companies founded on the second semester of the year. Limit your search to 1000 companies.

query: {founded_month: {$gt: 6}}
limit: 1000

### 12. All the companies founded before 2000 that have an acquisition amount of more than 10.000.000

query: { founded_year: { $lt: 2000 }, "acquisition.price_amount" : { $gte: 10000000 } }

### 13. All the companies that have been acquired after 2010, order by the acquisition amount, and retrieve only their `name` and `acquisition` field.

query: { $and: [ {"acquisition.acquired_year": { $gte : 2010, $ne: null}} , { "acquisition.price_amount": {$ne: null}} ]}
Projection: {_id: 0, name: 1, acquisition: 1}
Sort: {"acquisition.price_amount" : 1}

### 14. Order the companies by their `founded year`, retrieving only their `name` and `founded year`.

query: {founded_year: {$ne: null}} 
PROJECTION {name: 1, founded_year: 1, _id: 0} 
SORT: {founded_year: 1}

### 15. All the companies that have been founded on the first seven days of the month, including the seventh. Sort them by their `acquisition price` in a descending order. Limit the search to 10 documents.

Query: { founded_day: {$lte: 7, $ne: null} }
Sort: {"acquisition.price_amount": -1}

### 16. All the companies on the 'web' `category` that have more than 4000 employees. Sort them by the amount of employees in ascending order.

sort: {number_of_employees: 1}

### 17. All the companies whose acquisition amount is more than 10.000.000, and currency is 'EUR'.

query: { $and: [ {category_code: { $eq : "web", $ne: null}} , { number_of_employees: {$gte: 4000}} ]}
sort: {number_of_employees: 1}

### 18. All the companies that have been acquired on the first trimester of the year. Limit the search to 10 companies, and retrieve only their `name` and `acquisition` fields.

query: { "acquisition.acquired_month": {$lte: 3}}
projection: { name: 1, acquisition: 1, _id: 0 }
limit: 10

### 19. All the companies that have been founded between 2000 and 2010, but have not been acquired before 2011.

{ founded_year: {$gte: 2000, $lte: 2010}, "acquisition.acquired_year": {$gte: 2011}}
