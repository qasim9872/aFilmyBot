In order to run the application, firstly insert the api keys in the class BotInjectorModule, present in subProject aFilmyBotServices, in the package, linkBotToTelegram. In order to execute the application, call the Main method of InitBot class.

MyTelegramBot class in a subclass of TelegramLongPollingBot which is part of the Telegram api. It has a method onUpdateReceived which is executed whenever a message is received. If the message has text, using the dependency for api.ai (project name is libai) we make a request to the api.ai server and receive a response containing the action or intent, and the parameters if present. The same is done if it has an audio message. 

The AIResponse object has a getResult() method, the instance received from this is passed on to AccessTmdbApi instance, it checks the result instance for intended action (i.e search for movie by name) and calls the appropriate method that can handle it. 

For example, if the given query was "search for a movie by the name Avengers", the action would be "SearchForMovieByName", the result object would be passed to the SearchTmdbClass instance which would retrieve the parameters or if there are none, return the default reply. Using these parameters a request is made to the tmdb api instance to retrieve movies with the search parameter, the retrieved movieInfo objects are parsed into a display able string and added to the message which is then returned alongside markup buttons.

 In order to execute this, a total of four api keys are necessary. 
 
 The first is the key for api.ai, a default consumer api key is present which can be used. You can also create your own but that would require you to train an api.ai agent for yourself.
 
 The second is the bot token and bot username for telegram, this can be generated by downloading the telegram application, searching for the username: @botfather and sending the command "/newbot" and following the instructions".
 
 For the third api key, you need to create an account on https://www.themoviedb.org and get you api key.
 
 Lastly, in order to use the voice message function, you need the application_default_credentials.json file from google and set the path to it as an environment variable. More information is present here: https://developers.google.com/identity/protocols/application-default-credentials
 The easiest would be to download google gcloud sdk and use it to set the application default credentials.
 
This project contains parts from some other github projects:
1. libai is part of apiai-java-client from https://github.com/api-ai/apiai-java-client
2. api-themoviedb is taken from https://github.com/Omertron/api-themoviedb