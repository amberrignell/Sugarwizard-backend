## Setup to run locally:
Log into MongoDB and create a free Shared Tier Cluster. 
Go to connect -> connect your application and set the .env DATABASE_URL to the connection string. 
Set the .env SECRET to a random string. 
Run `npm i` then `npm start` and the server should be running on localhost:3000. 

User model:
{
email: { type: String, required: true },
password: {type: String, required: true},
insulinRatio: { type: Number, required: true},
carbRatio: { type: Number, required: true},
glucose_reading: { type: Array },
time: { type : Array }
},
{ timestamps: true },

REST API with four routes:

## Post /login —> calls loginUser
  {
  "email": "",
  "password": "",
  }

* Get the email and password from the request
* Find a user with the same email
* Compare the password with the hash for that user using bcrypt.compare
* Create and return a JWT token with the user id as the payload

## Post /signup ==> calls createUser:
  {
  "email": "",
  "password": "",
  "insulinRatio": 1,
  "carbRatio": 1
  }

- check if there is an existing user with that email
- hash the password with bcrypt and set the hash as the password’s value
- create a user using the user model
- Save the user
- Create a token using JWT
- Return the token

## Put /store-data —> calls authentication middleware and updateUser
  {
  "glucose_reading": 1,
  "time": ""
  }

## Get /profile —> calls authentication middleware and getUserById
