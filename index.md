## CS 499 Final Project - Akhil Sompalli

## Informal Code Review

click on the following link for the code Review 

[click here](https://drive.google.com/open?id=1HguanAmGRlNJasT4RHRdZL9H4Bi3mNg_)

### Narrative 1

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



