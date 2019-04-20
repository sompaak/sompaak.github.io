## CS 499 Final Project - Akhil Sompalli

## Informal Code Review

click on the following link for the code Review 

[click here](https://drive.google.com/open?id=1HguanAmGRlNJasT4RHRdZL9H4Bi3mNg_)

### Narrative 1 - Software Design and Engineering

  The artifact below is a piece of code I developed in a coding boot camp I attended going to UC Berkeley extension last year January of 2018. This code essentially accesses the twitter, Spotify and omdb api and returns data about them. This was an interesting and fun project as this was our introduction with dealing with apis and how to use them in order to access information.I selected this artifact for my code review as I felt that it best demonstrated my skills in the software and design aspect of my code. It shows how functions were organized and executed within my code. While performing the code review, I found that my code did not have comments. This was the part that I needed to improve within the code. In order to improve the artifact, I commented. The code so that it was more understandable and readable which is an important aspect in any software design.The course objectives were indeed met with this enhancement. I think the code satisfies all the requirements needed. For this particular I think all the requirements are satisfied but if there is anything that needs to be fixed ill fix it. I learned a lot in the process was of enhancing and modifying the artifact. Thinking about the piece of code more about its readability and the ways it should be applicable in a software design aspect was new and a different aspect for me. I thought the way I designed the code was perfect, but I realized that there weren’t any comments while reviewing the code. I learned that code reviews in the design aspect of coding is very important so that one can adhere to the guidelines of designing an application properly. 

### Artifact 1 - Software Design and Engineering

```javascript
/Dependencies
var Twitter = require('twitter');

var fs = require("fs")

var name = process.argv[2]

var twitterClient = new Twitter({
  consumer_key: 'M39K6oj5hx7c1DtE9I2KJNYWL',
  consumer_secret: '4BhKpluyTriEJIq6Y14NedlsOBZhfqgVlqy5pXHRd0UwrjmcuY',
  access_token_key: '240497888-BhhrWyyzMSptodKdHRiNBum3ziD8KdVUX0fstyHa',
  access_token_secret: 'rWiUAz9Wmrmmo76Y91XSOk6E2c1wNQ5aGYuMrM3GlDblw'
});

var Spotify = require('node-spotify-api');
     
var spotify = new Spotify({
  id: "0e7736924c084d1db7f7a500ad0b6da3",
  secret:"a62f853c5dc24e468e3c1b8f18caa484"
});

var request = require("request");
//__________________________________________________________________________________________

// Function to make a string that is multiple words a single string when inputting into termainal application.

function stringBuilder(){
  var returnString = ""
  var nodeArgs = process.argv
  for (var i = 3; i < nodeArgs.length; i++) {
      if (i > 3 && i < nodeArgs.length) {
        returnString = returnString + "+" + nodeArgs[i];
      }
      else {
        returnString += nodeArgs[i];
      }
  }
  return returnString
}

var handle = process.argv[3]



// Acesses twitter api to get tweets by kevin hart or any other parents.
function getTweets(){
    var params = {screen_name: handle};
    twitterClient.get('statuses/user_timeline', params, function(error, tweets, response) {
      if (!error) {
          for ( var i = 0; i < tweets.length; i++){
                console.log("Tweet " + i)
                console.log("Kevin Hart posted: ")
                console.log(tweets[i].text);
                console.log(" ")
                console.log("Tweet Posted At: ")
                console.log(tweets[i].created_at);
                console.log("__________________")

          }
              
      }
    });
}

// Accesses movie information from omdb api

function getMovieInfo(){
  var nodeArgs = process.argv
  var movieName = stringBuilder()
  console.log(movieName)
    
  if(!movieName){

    movieName = "harrypotter"
  }
  var queryUrl = "http://www.omdbapi.com/?t=" + movieName + "&y=&plot=short&apikey=trilogy";
  request(queryUrl, function(error, response, body) {
    if (!error && response.statusCode === 200) {
         var result = JSON.parse(body)  
        // console.log(result)
          console.log("Movie title: " + result.Title);
          console.log("Release Year: " + result.Year);
          console.log("imdb rating :" + result.imdbRating)
          //console.log(result.Ratings[1].Source, result.Ratings[1].Value )
           console.log("country: " + result.Country); 
           console.log("Language: " + result.Language); 
          console.log("Rating: " + result.Rated);
          console.log("plot: " + result.Plot);
          console.log("Actors: " + result.Actors);
          
      }
    });   
}



//Gets song information from spotify api
function getSpotifySongs(){

  var songName = stringBuilder()

  if(!songName){

    songName = "not afraid"
  }
   
  spotify.search({ type: 'track', query: songName }, function(err, data) {
    if (err) {
      return console.log('Error occurred: ' + err);
    }
     
    for (var i = 0; i< data.tracks.items.length; i++){
      console.log(data.tracks.items[i].artists[0].name); 
      console.log(data.tracks.items[i].name); 
      console.log(data.tracks.items[i].external_urls.spotify); 
      console.log(data.tracks.items[i].album.name); 
      console.log("_______________________________")
    }

  });

}


// runs all the above functions at once
function doWhatItSays(){

    fs.readFile("index.txt", "utf8", function(error, data) {

    if (error) {
      return console.log(error);
    }
   
    var options = data.split(",");

    var myTweets = options[0]
    var spotifyThisSong = options[1]
    var movieThis = options[2]


    switch(process.argv[3]){

    case myTweets:
      getTweets()
      break;
    case spotifyThisSong:
      getSpotifySongs()
      break
    case movieThis:
      getMovieInfo()
      break 

    }
    


  });

}

// runs the appropriate function based on the string entered.
switch(process.argv[2]){

  case "my-tweets":
    getTweets()
    break;
  case "spotify-this-song":
    getSpotifySongs()
    break
  case "movie-this":
    getMovieInfo()
    break 
  case "do-what-it-says":
    doWhatItSays()
    break

}
```
### Narrative 2 - Algorithm and Data Structures 

	The artifact below belongs to the data structure and algorithms class CS-260. This artifact was essentially created last year. This artifact essentially uses the use of data structures and sorting algorithms. For example, this particular artifact uses quicksort as an algorithm and a hash table as a data structure.I selected this artifact as I felt that it best demonstrated my skills in the data structures and algorithms aspect. It shows how functions were organized and executed within my code. I found that my code did not have comments. This was the part that I nee improved within the code. In order to improve the artifact, I commented the code so that it was more understandable and readable which is an important aspect in any code that is being used at the industry standard.The course objectives were indeed met with this enhancement. I think the code satisfies all the requirements needed. For this in particular I think all the requirements are satisfied but if there is anything that needs to be fixed ill fix it. I learned a lot in the process was of enhancing and modifying the artifact. Thinking about the piece of code more about its readability and the ways it should be applicable in a software design aspect was new and a different aspect for me. I thought the way I designed the code was perfect, but I realized that there weren’t any comments while reviewing the code. I learned that code reviews in the design aspect of coding is very important so that one can adhere to the guidelines of designing an application properly. 

### Artifact 2 - Algorithm and Data Structures

```C++
//============================================================================
// Name        : VectorSorting.cpp
// Author      : Akhil Sompalli
// Version     : 1.0
// Copyright   : Copyright © 2017 SNHU COCE
// Description : Final Project - Vector Sorting Algorithms
//============================================================================

#include <algorithm>
#include <iostream>
#include <time.h>

#include "CSVparser.hpp"

using namespace std;

//============================================================================
// Global definitions visible to all methods and classes
//============================================================================

// forward declarations
double strToDouble(string str, char ch);

// define a structure to hold bid information
struct Bid {
    string bidId; // unique identifier
    string title;
    string fund;
    double amount;
    Bid() {
        amount = 0.0;
    }
};


//============================================================================
// Hash Table class definition
//============================================================================

/**
 * Define a class containing data members and methods to
 * implement a hash table with chaining.
 */
class HashTable {

private:
	struct Node {
		Bid bid;
		unsigned int key;
		Node* nextBidNode;

		Node() {
			key = UINT_MAX;
			nextBidNode = nullptr;
		}
		Node(Bid abid, unsigned int akey) {
			bid = abid;
			key = akey;
			nextBidNode = nullptr;
		}
	};

	vector<Node> nodes;
	unsigned int tableSize = 0;
    unsigned int hash(int key);

public:
    HashTable(int);
    HashTable();
    virtual ~HashTable();
    void Insert(Bid);
    void PrintAll();
    void Remove(string);
    Bid Search(string);
};


HashTable::HashTable(int tableSize) {
	this->tableSize = tableSize;
	nodes.resize(tableSize);
}


/**
 * Default constructor
 */
HashTable::HashTable() {

}


/**
 * Destructor
 */
HashTable::~HashTable() {
	nodes.clear();
}

/**
 * Calculate the hash value of a given key.
 * Note that key is specifically defined as
 * unsigned int to prevent undefined results
 * of a negative list index.
 *
 * @param key The key to hash
 * @return The calculated hash
 */
unsigned int HashTable::hash(int key) {
	unsigned int hashValue = key % tableSize;
	return hashValue;
}

/**
 * Insert a bid
 *
 * @param bid The bid to insert
 */
void HashTable::Insert(Bid bid) {

	unsigned int key = hash(atoi(bid.bidId.c_str()));

	Node* currentNode = &(nodes.at(key));

	if (currentNode->key == UINT_MAX) {
		currentNode->key = key;
		currentNode->bid = bid;
		currentNode->nextBidNode = nullptr;
	}else {
		// find last node
		while (currentNode->nextBidNode != nullptr){
			currentNode = currentNode->nextBidNode;
		}
		currentNode->nextBidNode = new Node(bid,key);
	}
}

/**
 * Print all bids
 */
void HashTable::PrintAll() {
	Bid bid;
	Node* node;

	// loop through the vector
	for (int i=0; i < tableSize; ++i) {

		// Get the node at i and the bid associated with the node;
		node = &(nodes.at(i));
		bid = nodes.at(i).bid;

		if (node->key != UINT_MAX) {
			bid = node->bid;
			cout << "Key " << node->key << ": " << " Id: " << bid.bidId << " | " <<  bid.title << " | " << bid.amount << " | " << bid.title << endl;
		}

		// check for nodes linked to the current node
		while (node->nextBidNode != nullptr){
			node = node->nextBidNode;
			bid = node->bid;
			cout << "    " << node->key << ": " << " Id: " << bid.bidId << " | " <<  bid.title << " | " << bid.amount << " | " << bid.title << endl;

		}
	}
}

/**
 * Search for the specified bidId
 *
 * @param bidId The bid id to search for
 */
Bid HashTable::Search(string bidId) {
    Bid bid;

    // FIXME (8): Implement logic to search for and return a bid

    // calculate key
    unsigned int key = hash(atoi(bidId.c_str()));

	Node* node = &(nodes.at(key));

	// node found
	if (node != nullptr && node->key != UINT_MAX && node->bid.bidId.compare(bidId) == 0 ){
		return node->bid;
	}

	//node not found
	if (node == nullptr || node->key == UINT_MAX){
		return bid;
	}

	//find in the linked list
	while (node != nullptr) {
		if (node->key != UINT_MAX && node->bid.bidId.compare(bidId) == 0){
			return node->bid;
		}
		node = node->nextBidNode;
	}

    return bid;
}


/**
 * Partition the vector of bids into two parts, low and high
 *
 * @param bids Address of the vector<Bid> instance to be partitioned
 * @param begin Beginning index to partition
 * @param end Ending index to partition
 */
int partition(vector<Bid>& bids, int begin, int end) {
	int l = begin;
	int h = end;

	/* Pick middle element as pivot */
	int middle = begin + (end - begin) / 2;
	Bid pivotbid = bids.at(middle);

	bool done = false;
	while (!done) {

		/* increment l while bids.at(l).title < pivotbid.title */
		while (bids.at(l).title.compare(pivotbid.title) < 0) {
			++l;
		}

		/* decrement h while pivotbid.title < bids.at(h).title */
		while (pivotbid.title.compare(bids.at(h).title) < 0) {
			--h;
		}

		if (l >= h){
			done = true;
		}
		else {

			swap(bids.at(l), bids.at(h));

			++l;
			--h;
		}
	}
	return h;
}

/**
 * Perform a quick sort on bid title
 * Average performance: O(n log(n))
 * Worst case performance O(n^2))
 *
 * @param bids address of the vector<Bid> instance to be sorted
 * @param begin the beginning index to sort on
 * @param end the ending index to sort on
 */
void quickSort(vector<Bid>& bids, int begin, int end) {
	int j = 0;

	/* Base case: If there are 1 or zero elements to sort,partition is already sorted */
	if (begin >= end){
		return;
	}

	/* Partition the data within the array. Value j returned
	    from partitioning is location of last element in low partition. */
	j = partition(bids, begin, end);

	/* Recursively sort low partition (i to j) and high partition (j + 1 to k) */

	quickSort(bids, begin, j);
	quickSort(bids, j + 1, end);

	return;

}

/**
 * Simple C function to convert a string to a double
 * after stripping out unwanted char
 *
 * credit: http://stackoverflow.com/a/24875936
 *
 * @param ch The character to strip out
 */
double strToDouble(string str, char ch) {
    str.erase(remove(str.begin(), str.end(), ch), str.end());
    return atof(str.c_str());
}

//============================================================================
// Static methods used for testing
//============================================================================

/**
 * Display the bid information to the console (std::out)
 *
 * @param bid struct containing the bid info
 */
void displayBid(Bid bid) {
    cout << bid.bidId << ": " << bid.title << " | " << bid.amount << " | "
            << bid.fund << endl;
    return;
}

/**
 * Load a CSV file containing bids into a container
 *
 * @param csvPath the path to the CSV file to load
 * @return a container holding all the bids read
 */
vector<Bid> loadBids(string csvPath) {
    cout << "Loading CSV file " << csvPath << endl;

    // Define a vector data structure to hold a collection of bids.
    vector<Bid> bids;


    // initialize the CSV Parser using the given path
    csv::Parser file = csv::Parser(csvPath);


    try {
        // loop to read rows of a CSV file
        for (int i = 0; i < file.rowCount(); i++) {

            // Create a data structure and add to the collection of bids
            Bid bid;
            bid.bidId = file[i][1];
            bid.title = file[i][0];
            bid.fund = file[i][8];
            bid.amount = strToDouble(file[i][4], '$');

            //cout << "Item: " << bid.title << ", Fund: " << bid.fund << ", Amount: " << bid.amount << endl;

            // push this bid to the end
            bids.push_back(bid);
        }
    } catch (csv::Error &e) {
        std::cerr << e.what() << std::endl;
    }

    return bids;
}


HashTable* getHashTable(vector<Bid>& bids) {


	HashTable* hTable = new HashTable(bids.size());

	for (int i = 0; i < bids.size(); ++i) {

			hTable->Insert(bids[i]);

	}

	return hTable;
}


/**
 * The one and only main() method
 */
int main(int argc, char* argv[]) {


    // process command line arguments
    string csvPath, bidKey;
    switch (argc) {
    case 2:
        csvPath = argv[1];
        bidKey = "98109";
        break;
    case 3:
        csvPath = argv[1];
        bidKey = argv[2];
        break;
    default:
        csvPath = "eBid_Monthly_Sales.csv";
        bidKey = "98109";
    }


    // Define a vector to hold all the bids
    vector<Bid> bids;

    Bid bid;

    HashTable* bidTable;

    // Define a timer variable
    clock_t ticks;

    int choice = 0;
    while (choice != 9) {
        cout << "Menu:" << endl;
        cout << "  1. Load Bids" << endl;
        cout << "  2. Display All Bids" << endl;
        cout << "  3. Find Bid by BidId" << endl;
        cout << "  4. Sort by Bid Title" << endl;
        cout << "  9. Exit" << endl;
        cout << "Enter choice: ";
        cin >> choice;

        switch (choice) {

        case 1:
            // Initialize a timer variable before loading bids
            ticks = clock();

            // Complete the method call to load the bids
            bids = loadBids(csvPath);

            cout << bids.size() << " bids read" << endl;

            // Calculate elapsed time and display result
            ticks = clock() - ticks; // current clock ticks minus starting clock ticks
            cout << "time: " << ticks << " clock ticks" << endl;
            cout << "time: " << ticks * 1.0 / CLOCKS_PER_SEC << " seconds" << endl;

            break;

        case 2:
            // Loop and display the bids read
            for (int i = 0; i < bids.size(); ++i) {
                displayBid(bids[i]);
            }
            cout << endl;

            break;

        case 3:
            ticks = clock();

            ticks = clock() - ticks; // current clock ticks minus starting clock ticks

            //bidTable = new HashTable(bids.size());

            	//loadBidTableFromVector(bidTable, bids);

            bidTable = getHashTable(bids);


            	bid = bidTable->Search(bidKey);


            if (!bid.bidId.empty()) {
                displayBid(bid);
            } else {
                cout << "Bid Id " << bidKey << " not found." << endl;
            }

            cout << "time: " << ticks << " clock ticks" << endl;
            cout << "time: " << ticks * 1.0 / CLOCKS_PER_SEC << " seconds" << endl;
            break;

        case 4:
        		// Initialize a timer variable before loading bids
			ticks = clock();

			quickSort(bids, 0, bids.size() -1);

			cout << bids.size() << " bids read" << endl;

			ticks = clock() - ticks;
			cout << "time: " << ticks << "clock ticks" << endl;
			cout << "time: " << ticks * 1.0 / CLOCKS_PER_SEC << " seconds" << endl;

			break;

        }
    }

    cout << "Good bye." << endl;

    return 0;
}
```
### Narrative 3 - Database

	This artifact belongs to the CS-340-Q3079 Advanced Programming Concepts.This artifact was essentially a few moths ago. This artifact essentially uses the use of mongo DB. For example, this particular artifact uses mongo DB in order to query the data base in order to obtain information as well as using curl commands in order to do so.I selected this artifact as I felt that it best demonstrated my skills in the database aspect. It shows how functions were organized and executed within my code. I found that my code did not have comments. This was the part that I needed improved within the code. In order to improve the artifact, I commented the code so that it was more understandable and readable which is an important aspect in any code that is being used at the industry standard.The course objectives were indeed met with this enhancement. I think the code satisfies all the requirements needed. For this in particular I think all the requirements are satisfied but if there is anything that needs to be fixed ill fix it. I learned a lot in the process was of enhancing and modifying the artifact. Thinking about the piece of code more about its readability and the ways it should be applicable in a software design aspect was new and a different aspect for me. I thought the way I designed the code was perfect, but I realized that there weren’t any comments while reviewing the code. I learned that code reviews in the design aspect of coding is very important so that one can adhere to the guidelines of designing an application properly.
	
### Artifact 3 - Database

``` python
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





