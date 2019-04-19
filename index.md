## Welcome to GitHub Pages


### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3


Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.


```python
# coding: utf-8
import json
import pymongo
import datetime
from bson import json_util
import bottle
from bottle import Bottle, route, run, request, abort

myclient = pymongo.MongoClient()
db = myclient["market"]
mycol = db["stocks"]

#___________________________________________________________________________________________________________
# PART 2 DOCUMENT MANIPULATION
def insert(val):
  x = mycol.insert_one(val)
  print("INSERTED: ", x)
def find(key,value):
  for x in mycol.find({key:value}):
    print("FOUND: " , x)
    
def update(query,updated):
  y = mycol.update_one(query, updated)
  print("UPDATED : " ,  y)
  
def delete(delete_item):
  z = mycol.delete_many(delete_item)
  print("DELETED: " , z)
#_______________________________________________________________________________________________________________

# PART 3 DOCUMENT RETRIEVAL
def movingAverage(low , high):
  for m in mycol.find( { "50-Day Simple Moving Average": { "$lt": high , "$gt":low} },{"Ticker": 1 , "50-Day Simple Moving Average":1} ): 
    print(m)
    
def industry(industryName):
  for x in mycol.find({"Industry":industryName},{"Industry":1 , "Ticker":1}):
    print("FOUND: " , x)
    
    
def aggregate():

  pipe = [

    {"$match":{
       "Sector": {"$eq": "Healthcare"}
      }
    },

    {"$group":{
    "_id": "$Industry",
    "industry": {"$first" : '$Industry'},
    "Total Shares Outstanding":{"$sum":"$Shares Outstanding"}
    }}  
  ]
  
  for doc in db.stocks.aggregate(pipe):
    print(doc)
  
#______________________________________________________________________________________________________________________

# PART 4 ADVANCED PROGRAMMING PROJECT

@route("/stocks/api/v1.0/createStock/AA", method='POST')
def create():
  data = request.json 
  x = mycol.insert_one(data)
  print("INSERTED: ", x)
  
  
@route("/stocks/api/v1.0/getStock/AA", method='GET')
def read():
  Ticker = request.query.Ticker
  for x in mycol.find({"Ticker":Ticker}):
    print("FOUND: " , x)
    
@route("/stocks/api/v1.0/updateStock/AA" , method="GET")
def updated():
  query = { "Ticker" : request.query.Ticker}
  update_values = {"$set":{"Ticker":request.query.Ticker}}
  y = mycol.update_one(query, update_values)
  print("UPDATED : " ,  y)
  return query


@route("/stocks/api/v1.0/deleteStock/AA" , method="GET")
def deletion():
  Ticker = request.query.Ticker
  z = mycol.delete_many({"Ticker" : Ticker})
  print("DELETED: " , z)
  
@route("/stocks/api/v1.0/stockReport" , method = "POST")
def stockReport():
  tickerSymbolsJson=request.json  
  tickerSymbols = tickerSymbolsJson['symbols'].split(",")
  x = mycol.find({"Ticker":{"$in":tickerSymbols}},{"Ticker": 1 , "Industry": 1, "Sector":1})
  for y in x:
    print y
    
@route("/stocks/api/v1.0/industryReport/telecom" , method = "GET")
def fiveTopStocks():
  industry = request.query.Industry
  for data in db.stocks.find({ "$text": { "$search": industry}},{"Ticker": 1, "Industry":1, "Price":1 }).sort([("Price", -1)]).limit(5):
    print data
  
#________________________________________________________________________________________________________________________________________
    
    

    
def main():
 
  #     val = {"id":"20032-2017-ACME", 
#           "certificate_number":"9998888",
#           "business_name":"ACME Explosives",
#           "date":datetime.datetime.now(),
#           "result" : "Business Padlocked",
#           "sector":"Explosive Retail Dealer – 999",
#           "address":{"number":"1721",
#                    "street":"Boom Road",
#                    "city":"BRONX",
#                    "zip":"10463"}}
#   insert(val)

#   key = "business_name"
#   value = "ACME Explosives"
#   find(key , value)  
  
#   query = { "Ticker" : "ABV"}
#   updated = {"$set":{"Volume":25}}
#   update(query,updated)
  
#   delete_item = { "Ticker":"BRLI" }
#   delete(delete_item)
#   
#   low = 0.005
#   high = 0.006
#   movingAverage(low, high)

  
#   industryName = "Medical Laboratories & Research"
#   industry(industryName)
  

#   aggregate()
 

   run(host='localhost', port=8081)
  
main()
```
