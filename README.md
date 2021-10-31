This is the backend for the [Sugarwizard app](https://sugarwizard.netlify.app/) - an open source web app to help diabetics calculate their insulin dosage. 

## Setup to run locally:
Go to [MongoDB](https://www.mongodb.com/) and create a database, a user and a free Shared Tier Cluster (you can use any cloud provider or region) <br>
Go to connect -> connect your application and set the .env DATABASE_URL to the connection string. Don't forget to replace `<password>` <br> 
Set the .env JWT_SECRET to a random string. <br>
Run `npm i` then `npm start` and the server should be running on localhost:3000. <br>

User model:
```
{
  email: { type: String, required: true },
  password: {type: String, required: true},
  insulinRatio: { type: Number, required: true},
  carbRatio: { type: Number, required: true},
  glucose_reading: { type: Array },
  time: { type : Array }
},
{ timestamps: true },
```

REST API with four routes (see **postman collection** [here](https://www.getpostman.com/collections/a8e0a55c4f4b0f03c50f)):

## Post /api/login —> calls loginUser
  ```
  {
    "email": "",
    "password": "",
  }
  ```

* Get the email and password from the request
* Find a user with the same email
* Compare the password with the hash for that user using bcrypt.compare
* Create and return a JWT token with the user id as the payload

## Post /api/signup ==> calls createUser:
  ```
  {
    "email": "",
    "password": "",
    "insulinRatio": 1,
    "carbRatio": 1
  }
  ```

- check if there is an existing user with that email
- hash the password with bcrypt and set the hash as the password’s value
- create a user using the user model
- Save the user
- Create a token using JWT
- Return the token

## Put /api/store-data —> calls authentication middleware and updateUser
   ```
  {
  "glucose_reading": 1,
  "time": ""
  }
  ```

## Get /api/profile —> calls authentication middleware and getUserById
