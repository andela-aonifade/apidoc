## API Documentation
-----
The API has routes, each dedicated to a single task that uses HTTP response codes to indicate API status and errors.
#### API Features

The following features make up the Document Management System API:

###### Authentication
-   It uses JSON Web Token (JWT) for authentication.  

-   It generates a token on successful login or account creation and returns it to the consumer.  

-   It verifies the token to ensures a user is authenticated to access protected endpoints.

###### Users

-   It allows users to be created.  

-   It allows users to login and obtain a token  

-   It allows authenticated users to retrieve and update their information.  

-   It allows the admin to manage users.

###### Roles

-   It ensures roles can be created, retrieved, updated and deleted by an admin user.
-   A non-admin user cannot create, retrieve, modify, or delete roles.  
-   it allows for assignment of roles to users

###### Documents

-   It allows new documents to be created by authenticated users.  

-   It ensures all documents are accessible based on the permission specified.  

-   It allows admin users to create, retrieve, modify, and delete documents.


-   It ensures users can delete, edit and update documents that they own.  

-   It allows users to retrieve all documents they own as well as public documents.

###### Search

-   It allows users to search public documents for a specified search term.

-   It allows admin to retrieve all documents that matches search term.

-   It allows admin to search users based on a specified search term

#### Available API Endpoints and their Functionality

EndPoint                                            |   Functionality
----------------------------------------------------|------------------------
POST /users/login                                   |   Logs a user in.
POST /users/logout                                  |   Logs a user out.
POST /users/                                        |   Creates a new user.
GET /users/                                         |   Find matching instances of user.
GET /users/<id>                                     |   Find user.
PUT /users/<id>                                     |   Update user attributes.
DELETE /users/<id>                                  |   Delete user.
GET /users/?limit={interger}&offset={interger}      | Pagination for users
POST /documents/                                    |   Creates a new document instance.
GET /documents/                                     |   Find matching instances of document.
GET /documents/<id>                                 |   Find document.
GET /documents/?limit={interger}&offset={interger}  | Pagination for documents
PUT /documents/<id>                                 |   Update document attributes.
DELETE /documents/<id>                              |   Delete document.
GET /users/<id>/documents                           |   Find all documents belonging to the user.
GET /search/users/?q={username}                     |   Gets all users with username contain the search term
GET /search/documents/?q={doctitle}                 | Get all documents with title containing the search query
GET /users/:id/alldocuments                         |   Get all document owned or accessible by `userId`
GET /api/users/:identifier                          |Find user with email or username containing the identifier parameter

#### Role

###### POST HTTP Request
-   `POST /roles`
-   Requires: Admin Authentication
    ###### HTTP Response
-   HTTP Status: `201: created`
-   JSON data
```json
{
  "role": {
    "id": 12,
    "title": "moderator",
    "updatedAt": "2017-06-05T11:04:42.604Z",
    "createdAt": "2017-06-05T11:04:42.604Z"
  },
  "message": "Role created succesfully"
}
```
###### GET HTTP Request
-   `GET /roles/:id`
-   Requires: Authentication
    ###### HTTP Response
-   HTTP Status: `200: OK`
-   JSON data
```json
{
    "role": {
        "id": 2,
        "title": "regular",
        "createdAt": "2017-05-18T15:31:39.062Z",
        "updatedAt": "2017-05-18T15:31:39.062Z"
    }
}
```
###### GET HTTP Request
-   `GET /roles`
-   Requires: Admin Authentication
    ###### HTTP Response
-   HTTP Status: `200: OK`
-   JSON data
```json
{
  "role": [
    {
      "id": 1,
      "title": "administrator",
      "createdAt": "2017-05-18T15:31:39.062Z",
      "updatedAt": "2017-05-18T15:31:39.062Z"
    },
    {
      "id": 2,
      "title": "regular",
      "createdAt": "2017-05-18T15:31:39.062Z",
      "updatedAt": "2017-05-18T15:31:39.062Z"
    },
    {
      "id": 11,
      "title": "general",
      "createdAt": "2017-05-20T13:28:18.851Z",
      "updatedAt": "2017-05-20T13:28:18.851Z"
    }
  ]
}
```
###### PUT HTTP Request
-   `PUT /roles/:id`
-   Requires: Admin Authentication
    ###### HTTP Response
-   HTTP Status: `200: OK`
-   JSON data
```json
{
  "role": {
    "id": 12,
    "title": "Document moderator",
    "createdAt": "2017-06-05T11:04:42.604Z",
    "updatedAt": "2017-06-05T11:15:38.862Z"
  },
  "message": "Role updated successfully."
}
```
###### DELETE HTTP Request
-   `DELETE /roles/:id`
-   Requires: Admin Authentication
    ###### HTTP Response
-   HTTP Status: `200: OK`
-   JSON data
```json
{
  "message": "Role deleted successfully."
}
```

#### Users
###### POST HTTP Request
-   `POST /users`
    ###### HTTP response
-   HTTP Status: `201: created`
-   JSON data
```json
{
  "newUser": {
    "id": 16,
    "name": "Anu",
    "username": "anu",
    "email": "anu@anu.com",
    "password": "$2a$08$RFZplY48i2LfrskVaaYb6ehZTHujHdBW7N14faSSCWsTK7fhWnyOG",
    "roleId": 1,
    "updatedAt": "2017-06-05T10:54:59.750Z",
    "createdAt": "2017-06-05T10:54:59.750Z"
  },
  "message": "User created successfully",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJkYXRhIjp7ImlkIjoxNiwibmFtZSI6IkFudSIsInVzZXJuYW1lIjoiYW51IiwiZW1haWwiOiJhbnVAYW51LmNvbSIsInJvbGVJZCI6MX0sImlhdCI6MTQ5NjY2MDA5OSwiZXhwIjoxNDk2NzQ2NDk5fQ.IWMSKLvMby1yek0hEiSJmS7mWTV7m5Lp23lZlrI5hq4"
}
```
###### Login HTTP Request
-   `POST /users/login`
    ###### HTTP Response
-   HTTP status: `200: OK`
-   JSON Data
```json
{
  "message": "User authenticated successfully",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJkYXRhIjp7ImlkIjoxNSwibmFtZSI6ImFkbWluIHVzZXIiLCJ1c2VybmFtZSI6ImFkbWluMSIsImVtYWlsIjoiYWRtaW4yQGFkbWluMi5jb20iLCJyb2xlSWQiOjF9LCJpYXQiOjE0OTY0MzEwMDcsImV4cCI6MTQ5NjUxNzQwN30.M5UKTYZb9m4YHeIRXlyRPQb8y66hMF65v7tV1SGmLfg"
}
```

#### Get Users
###### GET HTTP Request
-   `GET /users`
-   Requires: Admin Authentication
    ###### HTTP Response
-   HTTP status: `200: OK`
-   JSON Data
```json
{
  "user": [
    {
      "id": 4,
      "name": "Anthony",
      "username": "anthony",
      "email": "anthony@andela.com",
      "password": "$2a$10$oGsHABwrr34AVZfdDN1WG.r/jHryU/QsO2p4I9t3HtUKCx.Sc0GGG",
      "roleId": 2,
      "createdAt": "2017-05-18T15:33:21.224Z",
      "updatedAt": "2017-05-18T15:33:21.224Z"
    },
    {
      "id": 2,
      "name": "Onifade anuoluwapo",
      "username": "anuonifade",
      "email": "anuonifade@gmail.com",
      "password": "$2a$10$heCyCbBosnmoaIvXiFmMoeIA6L0.TkeFSZ4YWAivvRGutQf8Wca8O",
      "roleId": 1,
      "createdAt": "2017-05-18T15:31:39.064Z",
      "updatedAt": "2017-05-18T15:31:39.072Z"
    },
    {
      "id": 6,
      "name": "abc",
      "username": "abc",
      "email": "abc@abc.com",
      "password": "$2a$10$/24arX4OjmSQewRRBDOkY./.FWhaXFLlpnY/mu1T6Ll2VKBdaYKsa",
      "roleId": 11,
      "createdAt": "2017-05-20T19:30:23.180Z",
      "updatedAt": "2017-05-20T19:30:23.180Z"
    },
    {
      "id": 7,
      "name": "taiwo",
      "username": "taiwo",
      "email": "taiwo@xyz.com",
      "password": "$2a$10$DwpNblV54MF5uMKGobh8iu7Ig9IimSx8InnhcGlTwFHnJtXurx3O.",
      "roleId": 2,
      "createdAt": "2017-05-22T07:32:14.867Z",
      "updatedAt": "2017-05-22T07:32:14.867Z"
    },
    {
      "id": 8,
      "name": "Anu Onifade",
      "username": "anuonifade1",
      "email": "anu@onifade.com",
      "password": "$2a$10$RwYO4eeUDjQhcXrPzS.xSOehGF1tej0JW.Uly2Q7hH3adfiAHEpmi",
      "roleId": 2,
      "createdAt": "2017-05-23T14:48:13.596Z",
      "updatedAt": "2017-05-23T14:48:13.596Z"
    },
    {
      "id": 9,
      "name": "weirdo maximuf",
      "username": "weirdo",
      "email": "weirdo@andela.com",
      "password": "$2a$08$cOB.fHHM3z4aZnNXoCkgkOxsZrPfYRerQB9CNGemta1VrFimEbzq2",
      "roleId": 2,
      "createdAt": "2017-05-25T13:55:34.381Z",
      "updatedAt": "2017-05-25T13:58:02.523Z"
    },
    {
      "id": 11,
      "name": "Super Administrator",
      "username": "superadmin",
      "email": "superadmin@email.com",
      "password": "$2a$08$eP3vyNCEkIetLGMb1JfGce8L5uku45L2NtnLOReNaAiAkKfpw2i3y",
      "roleId": 1,
      "createdAt": "2017-05-26T20:20:51.617Z",
      "updatedAt": "2017-05-26T20:20:51.617Z"
    },
    {
      "id": 1,
      "name": "administrator user",
      "username": "admin",
      "email": "admin@email.com",
      "password": "$2a$08$DsSJvQdzWp8iagIpgKfE7uf8BPWje80KAzqX2hgm0AwAXjM9A0xcC",
      "roleId": 1,
      "createdAt": "2017-05-18T15:31:39.064Z",
      "updatedAt": "2017-06-02T18:23:26.445Z"
    },
    {
      "id": 12,
      "name": "abcd",
      "username": "abcd",
      "email": "abcd@abcd.com",
      "password": "$2a$08$QNz.g.245Q6DZr6N0daDlukw/9mnrAgyAsG1k.iC1QlDHdYV3vBK.",
      "roleId": 1,
      "createdAt": "2017-05-30T17:29:34.144Z",
      "updatedAt": "2017-05-30T17:30:06.864Z"
    },
    {
      "id": 15,
      "name": "admin user",
      "username": "admin1",
      "email": "admin1@admin1.com",
      "password": "$2a$10$kzOTNdcyeaXcFj3.BUOSv.svbjKO4qvvt3QD0ABu6CeLY5D6.g77O",
      "roleId": 1,
      "createdAt": "2017-06-02T19:01:30.956Z",
      "updatedAt": "2017-06-02T22:05:44.757Z"
    }
  ],
  "pagination": {
    "limit": 10,
    "next": "?limit=10&offset=10",
    "offset": 0,
    "previous": "?limit=10&offset=0",
    "total_count": 12
  }
}
```
#### Get User
###### GET HTTP Request
-   `GET /users/:id`
-   Requires: Admin Authentication
    ###### HTTP Response
-   HTTP status: `200: OK`
-   JSON Data
```json
{
  "user": 
    {
      "id": 8,
      "name": "Anu Onifade",
      "username": "anuonifade1",
      "email": "anu@onifade.com",
      "password": "$2a$10$RwYO4eeUDjQhcXrPzS.xSOehGF1tej0JW.Uly2Q7hH3adfiAHEpmi",
      "roleId": 2,
      "createdAt": "2017-05-23T14:48:13.596Z",
      "updatedAt": "2017-05-23T14:48:13.596Z"
    }
}
```
#### Update User
###### PUT HTTP Request
-   `PUT /users/:id`
-   Requires: Authentication
    ###### HTTP Response
-   HTTP status: `200: OK`
-   JSON Data
```json
{
  "updatedUser": {
    "id": 7,
    "name": "taiwo",
    "username": "taiwo",
    "email": "taiwo@taiwo.com",
    "password": "$2a$10$V1WWEG3FU9hbVONZoeQhKeWZmvoCklwBbFxHru/QCBMORsdc4bVwi",
    "roleId": 2,
    "createdAt": "2017-05-22T07:32:14.867Z",
    "updatedAt": "2017-06-05T11:36:09.966Z"
  },
  "message": "User updated successfully"
}
```
#### Delete User
###### DELETE HTTP Request
-   `DELETE /users/:id`
-   Requires: Admin Authentication
    ###### HTTP Response
-   HTTP status: `200: OK`
-   JSON Data
```json
{
  "message": "abcd deleted successfully"
}
```


#### Documents
###### POST HTTP Request
-   `POST /documents`
-   Requires: Authentication
    ###### HTTP response
-   HTTP Status: `201: created`
-   JSON data
```json
{
  "id": "1",
  "title": "Test Title",
  "docContent": "This is my first diary created on this application",
  "viewAccess": "private",
  "role": "1",
  "userId": "1",
  "createdAT": "2017-04-05T14:22:46.984z",
  "updatedAT": "2017-04-05T14:22:46.984z"
}
```
###### GET HTTP Request
-   `GET /documents`
    ###### HTTP response
-   HTTP Status: `200: 0k`
-   JSON data
```json
{
  "message": "Documents loaded successfully",
  "document": [
    {
      "id": 5,
      "title": "test taiwo",
      "docContent": "<p>this is taiwo in the house yeah.</p>",
      "docType": null,
      "viewAccess": "public",
      "role": "2",
      "createdAt": "2017-05-22T07:33:25.307Z",
      "updatedAt": "2017-05-22T07:33:25.307Z",
      "userId": 7,
      "User": {
        "id": 7,
        "name": "taiwo",
        "username": "taiwo",
        "email": "taiwo@taiwo.com",
        "password": "$2a$10$V1WWEG3FU9hbVONZoeQhKeWZmvoCklwBbFxHru/QCBMORsdc4bVwi",
        "roleId": 2,
        "createdAt": "2017-05-22T07:32:14.867Z",
        "updatedAt": "2017-06-05T11:36:09.966Z"
      }
    },
    {
      "id": 2,
      "title": "Norem ipsum 1",
      "docContent": "<p>Nisi et et blanditiis dignissimos quia enim sit tenetur. Quasi molestiae aut veritatis id omnis ipsa odio accusamus. Voluptatem corrupti rem. Atque consequatur occaecati beatae ipsa sunt dolores dolor nostrum et. Ut blanditiis et reiciendis vel facere neque iste. Tenetur vero reiciendis reprehenderit.</p>",
      "docType": null,
      "viewAccess": "public",
      "role": "1",
      "createdAt": "2017-05-18T15:31:39.401Z",
      "updatedAt": "2017-05-20T17:23:06.305Z",
      "userId": 1,
      "User": {
        "id": 1,
        "name": "administrator user",
        "username": "admin",
        "email": "admin@email.com",
        "password": "$2a$08$DsSJvQdzWp8iagIpgKfE7uf8BPWje80KAzqX2hgm0AwAXjM9A0xcC",
        "roleId": 1,
        "createdAt": "2017-05-18T15:31:39.064Z",
        "updatedAt": "2017-06-02T18:23:26.445Z"
      }
    },
    {
      "id": 4,
      "title": "test",
      "docContent": "<p>test</p>",
      "docType": null,
      "viewAccess": "public",
      "role": "2",
      "createdAt": "2017-05-18T21:35:09.415Z",
      "updatedAt": "2017-05-18T21:35:09.415Z",
      "userId": null,
      "User": null
    },
    {
      "id": 3,
      "title": "Hello Document Ngene",
      "docContent": "<p>Ngene created this document</p>",
      "docType": null,
      "viewAccess": "private",
      "role": "2",
      "createdAt": "2017-05-18T15:34:26.700Z",
      "updatedAt": "2017-05-18T15:34:44.111Z",
      "userId": 4,
      "User": {
        "id": 4,
        "name": "Anthony",
        "username": "anthony",
        "email": "anthony@andela.com",
        "password": "$2a$10$oGsHABwrr34AVZfdDN1WG.r/jHryU/QsO2p4I9t3HtUKCx.Sc0GGG",
        "roleId": 2,
        "createdAt": "2017-05-18T15:33:21.224Z",
        "updatedAt": "2017-05-18T15:33:21.224Z"
      }
    },
    {
      "id": 1,
      "title": "seed document test",
      "docContent": "Voluptas dignissimos saepe et quia in amet eveniet. Incidunt dolorum minima occaecati aut consequatur ex odit. Fuga quidem necessitatibus aut architecto. Modi qui veniam dignissimos ut deserunt. Doloribus quisquam et voluptas consequatur reiciendis. Nam ut ea iste laudantium dolores iusto perferendis.",
      "docType": null,
      "viewAccess": "private",
      "role": "1",
      "createdAt": "2017-05-18T15:31:39.401Z",
      "updatedAt": "2017-05-18T15:31:39.401Z",
      "userId": 1,
      "User": {
        "id": 1,
        "name": "administrator user",
        "username": "admin",
        "email": "admin@email.com",
        "password": "$2a$08$DsSJvQdzWp8iagIpgKfE7uf8BPWje80KAzqX2hgm0AwAXjM9A0xcC",
        "roleId": 1,
        "createdAt": "2017-05-18T15:31:39.064Z",
        "updatedAt": "2017-06-02T18:23:26.445Z"
      }
    }
  ]
}
```

###### GET HTTP Request
-   `GET /documents/:id`
-   Requires: Authentication
    ###### HTTP response
-   HTTP Status: `200: 0k`
-   JSON data
```json
    {
  "id": 3,
  "title": "Hello Document Ngene",
  "docContent": "<p>Ngene created this document</p>",
  "docType": null,
  "viewAccess": "private",
  "role": "2",
  "createdAt": "2017-05-18T15:34:26.700Z",
  "updatedAt": "2017-05-18T15:34:44.111Z",
  "userId": 4,
  "User": {
    "id": 4,
    "name": "Anthony",
    "username": "anthony",
    "email": "anthony@andela.com",
    "password": "$2a$10$oGsHABwrr34AVZfdDN1WG.r/jHryU/QsO2p4I9t3HtUKCx.Sc0GGG",
    "roleId": 2,
    "createdAt": "2017-05-18T15:33:21.224Z",
    "updatedAt": "2017-05-18T15:33:21.224Z"
  }
}
```
#### Update Document
###### PUT HTTP Request
-   `PUT /documents/:id`
-   Requires: Authentication
    ###### HTTP response
-   HTTP Status: `200: 0k`
-   JSON data
```json
{
  "updatedDoc": {
    "id": 3,
    "title": "Hello Document Ngene - Modified",
    "docContent": "<p>Ngene created this document</p>",
    "docType": null,
    "viewAccess": "private",
    "role": "2",
    "createdAt": "2017-05-18T15:34:26.700Z",
    "updatedAt": "2017-06-05T12:05:29.738Z",
    "userId": 4
  },
  "message": "Document updated successfully"
}
```
#### Delete Document
###### DELET HTTP Request
-   `DELET /documents/:id`
-   Requires: Authentication
    ###### HTTP response
-   HTTP Status: `200: 0k`
-   JSON data
```json
{
  "message": "test, was successfully deleted"
}
```
