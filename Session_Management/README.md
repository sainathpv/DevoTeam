# Session Management microservice:    

The session management microservice stores all the user session data in the MongoDB database. Every request from the user containing the input data for Nexrad service is stored to the database, along with the timestamp. This microservice receives data from the API gateway as soon as the request reaches it. The user can access their all of their previous sessions with the help of this microservice. Users can invoke the Nexrad service with their previous session's input data. 
