# GTH-Barcelona-ConsoleLu
Project submission for the `Global Travel Hackathon in Barcelona, by console.lu team`.

**Write one sentence explaining what does your project.**
Our idea is make travelling more accessible for people with special needs. For this reason we create Kiwi-them, wich is an app that will connect volunteers with people that needs help to travel. 

![Add a screenshot from your project. For example the main website page.](https://raw.githubusercontent.com/Global-Travel-Hackathon/GTH-Location-TeamName/master/screenshots/Global-Travel-Hackathon-image.png)

## :books: Description

Our project is focused in the accesibility and we use ReactJS in the Frontend and NodeJS and Mongoose in the back to developed. 

![* SDKs used in the project;
* APIs used in the project; 
Tequila by kiwi
Unsplash API
* Any assets used in the project;

* Any libraries used in the project;
React
socket.io
* Any components not created at the hackathon;]


## :hugs: Maintainers

List all the team members. For example:
* [Jesus Cebader - Zebader](https://github.com/zebader)
* [Rundi Ye - Jundi](https://github.com/Rundiye)
* [Jan Giménez - Jan](https://github.com/JanGimenezLayola)
* [Adri Porcel - Illo](https://github.com/prrrcl)
* [Lu Ye Zhan - Lu](https://github.com/LuYeZhan)


## :tada: Why is this so awesome?

* It's the first app focused on connecting volunteers with people with special needs where volunteers can help these, according to their special requests while travelling.
* Connecting people.
* Make a better society by helping each other.
* Social project.

## :hammer_and_wrench: Installation

1. Clone the Repo.
2. Open the project directory and run npm install in the command line.
3. Run npm start to execute the project in local.

## :bulb: Devstack

Client-side: React
Server-side: NodeJs, MongoDB, Express

Libraries:



## User Stories

-  **404:** As an anon/user I can see a 404 page if I try to reach a page that does not exist so that I know it's my fault.
-  **500:** As an anon/user I can see a 500 page if the server isn't working.
-  **Signup:** As a user I want to sign up on the webpage so that I can see my privates screens.
-  **Login:** As a user I want to be able to log in on the webpage so that I can get back to my account.
-  **Logout:** As a user I can logout from the platform so no one else can use it.
-  **Add Trips:** As a user I can add a trips and post them so that other users can see them.
-  **Join Trips:** As a user I can join to a trip I'm interested in.
-  **Edit Trips:** As a user I can edit a trip I created.

## Backlog

Mailing: confirmation by email
Ratings: users can rate each other
Edit User Profile

# Client / Frontend

## Routes
| Path                      | Component            | Permissions | Behavior                                                     |
| ------------------------- | -------------------- | ----------- | ------------------------------------------------------------ |
| `/auth/signup`            | Signup               | anon only   | Signup form, link to login, navigate to '/' after signup|
| `/auth/login`             | Login                | anon only   | Login form, link to signup, navigate to '/' after login |
| `/auth/logout`            | n/a                  | anon only   | Navigate to '/' after logout, expire session            |
| `/trip/add`            | TripAdd           | me user only   | Create a trip                                           |
| `/trip/edit/:id`            | TripEdit           | me user only   | Update a trip                                         |
| `/trip/delete/:id`            | n/a                  | me user only   | Delete a trip and redirect to '/me'                   |
| `/me`            | n/a                  | me user only   | Delete a trip and redirect to '/'                   |
| `/em`            | n/a                  | em user only   | Delete a trip and redirect to '/'                   |


## Components

 - Navbar 

## Pages

  - Chat
  - createTrip
  - em (Dashboard for volunteers)
  - me (Dashboard for travelers)
  - landing Page
  - login
  - signup
  - NotFound

## Services

- Auth Service

  - auth.login(user)
  - auth.signup(user)
  - auth.logout()
  - auth.me()
  - auth.getUser() // synchronous
  
- Api Service

  - getAllTrips()
  - getAllMyTrips()
  - addOneTrip()
  - editOneTrip(id)
  - deleteOneTrip(id)
  - getChat()
  - pushMessage()
  

# Server / Backend

| HTTP Method | URL                         | Request Body                 | Success status | Error Status | Description                                                  |
| ----------- | --------------------------- | ---------------------------- | -------------- | ------------ | ------------------------------------------------------------ |
| GET         | `/auth/profile    `           | Saved session                | 200            | 404          | Check if user is logged in and return profile page           |
| POST        | `/auth/signup`                | {name, email, password}      | 201            | 404          | Checks if fields not empty (422) and user not exists (409), then create user with encrypted password, and store user in session |
| POST        | `/auth/login`                 | {username, password}         | 200            | 401          | Checks if fields not empty (422), if user exists (404), and if password matches (404), then stores user in session |
| POST        | `/auth/logout`                | (empty)                      | 204            | 400          | Logs out the user                                            |
| GET         | `/me`                |                              |                | 400          | Show my trips                                         |
| GET         | `/em`            |                         |                |              | Show all trips available                                  |
| POST        | `/trip/add` | {from,to,startDate,endDate,needs}                            | 201            | 400          | Create and save a new trip                             |
| DELETE      | `/trip/delete/:id`     | {id}                         | 201            | 400          | Delete one trip  
| POST        | `/pushmessage` | {}                           | 201            | 400          | Create a message                                          |
| POST         | `/checkchat`       |           | 200            | 400          | check chat                                            |
| DELETE      | `/activity/:id/delete`     | {id}                         | 201            | 400          | delete activity                                            |

## Models

- User model

```javascript
{
  name: {
    type: String,
    required: true
  },
  surname: {
    type: String,
    required: true
  },
  email: {
    type: String,
    required: true,
    unique: true
  },
  password: {
    type: String,
    required: true
  },
  userType: {
    type: String,
    enum: ['volunteer', 'traveller']
  },
  pocket: {
    type: Number
  },
  comments: [{
    type: ObjectId,
    ref: 'Comment'
  }],
  myTrips: [{
    type: ObjectId,
    ref: 'Trip'
  }]
}, {
  timestamps: {
    createdAt: 'created_at',
    updatedAt: 'updated_at'
  }
}
```

- Trip model

```javascript
   from: {
    type: String,
    required: true
  },
  to: {
    type: String,
    required: true
  },
  startDate: {
    type: Date,
    required: true
  },
  endDate: {
    type: Date,
    required: true
  },
  needs: [{
    type: String
  }],
  requests: [{
    type: ObjectId,
    ref: 'User'
  }],
  img: {
    type: String
  },
  thisAccepted: {
    type: Boolean,
    default: false
  },
  owner: String
},

{
  timestamps: true
}
```

- Comment model
```javascript
title: {
    type: String,
    required: true
  },
  description: {
    type: String,
    required: true
  },
  rating: {
    type: Number,
    required: true
  }
}, {
  timestamps: {
    createdAt: 'created_at',
    updatedAt: 'updated_at'
  }
```

- Message model
```javascript
user: {
    type: ObjectId,
    ref: 'User'
  },
  message: {
    type: String
  },
  notification: {
    emitter: ObjectId,
    toUser: ObjectId,
    isViewed: {
      type: Boolean,
      default: false
    }
  }

}, {
  timestamps: {
    createdAt: 'created_at',
    updatedAt: 'updated_at'
  }
```

- Chat model
```javascript
users: {
    type: [ObjectId],
    ref: 'User'
  },
  messages: {
    type: [ObjectId],
    ref: 'Message'
  }
},
{
  timestamps: {
    createdAt: 'created_at',
    updatedAt: 'updated_at'
  }
```
## Slides

https://docs.google.com/presentation/d/1tSe81_jLoUn6ojFT_cLBAUsuWlUVQUJWR3gswHzyxhA/edit?usp=sharing

## :warning: Licence

>The code in this project is licensed under MIT license. By contributing to this project, you agree that your contributions will be licensed under its MIT license.
