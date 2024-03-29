# Node-Express-Mongo Property Ads Api
This backend implementation creates several REST architecture based API endpoints for authentication, user registeration and property CRUD operations in the DB for property and housing web-app.

## Installation

```bash
npm install
npm run dev
```

## API Reference

### POST: /register
#### Registers a user

```javascript

"Accept": "application/json",
"Content-Type": "application/json"

{
    "fullname": "Anish Tatke",
    "mobile": "9999999999",
    "email": "anish@tatke.com",
    "password": "Password1@"
}

//Response
{
    "message": "User created successfully",
    "user": {
        "profile_picture": null,
        "_id": "9ca44c6c-f90a-4ca5-95e4-96eccdd3c258",
        "fullname": "Anish Tatke",
        "role": "admin"
        "mobile": "9999999999",
        "email": "anish@tatke.com",
        "password": "$2a$15$pgrja5CO1MtRowk1vkrfVeyPodtTKxAzBJQ5Ho0yl9JdWxjszEPyC",
        "__v": 0
    }
}
```

### POST: /login
#### Login a user and generate JWT token

```javascript

"Accept": "application/json",
"Content-Type": "application/json"

{
    "email": "anish@tatke.com",
    "password": "Password1@"
}

//Response
{
    "email": "anish@tatke.com",
    "token": "System generated jwt token"
}
```

### PUT: /changepassword
#### Update password of logged in user, using JWT token

```javascript

"Accept": "application/json",
"Content-Type": "application/json"
"x-access-token": "JWT Token here"

{
    "old_password": "ABc1234$1",
    "new_password": "ABc1234$"
}

//Response
{
    "message": "Password updated for user: aditya@aditya.com"
}
```


### PUT: /updateprofile
#### Update profile details of logged in user, using JWT token

```javascript

"Accept": "application/json",
"Content-Type": "application/json"
"x-access-token": "JWT Token here"

{
    "email": "anish1@tatke.com", //optional
    "fullname": "Anish Uday Tatke", //optional
    "mobile": "8888888888" //optional
}

//Response
{
    "message": "User updated successfully"
}
```

### PUT: /updateprofilepicture
#### Update profile photo of logged in user, using JWT token


```javascript

"mimeType": "multipart/form-data"
"x-access-token": "JWT Token here"

{
    "key": "profile-picture"    
}

//Response
{
    "message": "Profile picture updated successfully."
}
```

### GET: /myprofile
#### Get details of logged in user

```javascript

"Accept": "application/json",
"Content-Type": "application/json"
"x-access-token": "JWT Token here"

//Response
{
    "id": "25370253-18ac-409e-b8ea-2fdff0ec1e1c",
    "fullname": "Anish Uday Tatke",
    "email": "anish1@tatke.com",
    "mobile": "8888888888"
}
```


### GET: /users
#### Get details of all the users

```javascript

"Accept": "application/json",
"Content-Type": "application/json"
"x-access-token": "JWT Token here"

//Response
{
    "users": [
        {
            "fullname": "Anish Uday Tatke",
            "mobile": "8888888888",
            "email": "anish1@tatke.com"
        },
        {
            "fullname": "Anish Tatke",
            "mobile": "9999999999",
            "email": "anish@tatke.com"
        }
    ]
}
```
### POST: /advertisement
#### Add an advertisement

```javascript

"Accept": "application/json",
"Content-Type": "application/json"

{
    "property_details": {
        "property_type" : "bungalow",
        "description" : "sea-facing",
        "n_bhk" : 15

    },
    "address" : {
        "city" : "Goa",
        "area_details" : "Amazing"
    },
    "quoted_price" : 45855558998552,
    "is_approved" : true,
    "intrestes" : 200
}

//Response
{
    "message": "advertisement created successfully",
    "id": "eafd91a8-8bf7-41c9-8997-a130686f2d5b"
}
```
### PUT: /updateadvertisement
#### Update a posted advertisement of logged in user, using JWT token

```javascript

"Accept": "application/json",
"Content-Type": "application/json"
"x-access-token": "JWT Token here"

{
    "_id": "eafd91a8-8bf7-41c9-8997-a130686f2d5b",
    "property_details": {
        "property_type" : "flat",
        "description" : "hill-facing",
        "n_bhk" : 15

    },
    "address" : {
        "city" : "Maldives",
        "area_details" : "Very nice"
    },
    "quoted_price" : 8595956465161321,
    "is_approved" : false,
    "intrestes" : 899
}

//Response
{
    "message": "advertisement eafd91a8-8bf7-41c9-8997-a130686f2d5b updated successfully"
}
```
### DELETE: /advertisement
#### Delete a posted advertisement of logged in user, using JWT token

```javascript

"Accept": "application/json",
"Content-Type": "application/json"
"x-access-token": "JWT Token here"

{
    "_id":"eafd91a8-8bf7-41c9-8997-a130686f2d5b"
}

//Response
{
    "message": "advertisement deleted successfully"
}
```

### GET: /advertisements
#### Get advertisements of all the users

```javascript

"Accept": "application/json",
"Content-Type": "application/json"
"x-access-token": "JWT Token here"

//Response
{
    "advertisements": [
        {
            "property_details": {
                "property_type": "flat",
                "description": "sky-facing",
                "n_bhk": 15
            },
            "address": {
                "city": "Maldives",
                "area_details": "Very superrr"
            },
            "images": [],
            "_id": "eafd91a8-8bf7-41c9-8997-a130686f2d5b",
            "quoted_price": 8595956465161321,
            "is_approved": false,
            "author": "john@doe.com",
            "createdAt": "2021-09-02T13:20:49.669Z",
            "updatedAt": "2021-09-02T13:26:34.217Z",
            "__v": 0
        }
    ]
}

```
### GET: /myadvertisements
#### Get advertisements of the logged in user

```javascript

"Accept": "application/json",
"Content-Type": "application/json"
"x-access-token": "JWT Token here"

//Response
{
    "advertisements": [
        {
            "property_details": {
                "property_type": "flat",
                "description": "sky-facing",
                "n_bhk": 15
            },
            "address": {
                "city": "Matheran",
                "area_details": "Very superrr"
            },
            "images": [],
            "_id": "eafd91a8-8bf7-41c9-8997-a130686f2d5b",
            "quoted_price": 8595956465161321,
            "is_approved": false,
            "author": "john@doe.com",
            "createdAt": "2021-09-02T13:20:49.669Z",
            "updatedAt": "2021-09-02T13:26:34.217Z",
            "__v": 0
        }
    ]
}

