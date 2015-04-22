FORMAT: 1A

# Buy-it API
Buy-it API is a *game* service similar to cashsquare

## Objects [/objects]
### Get objects around the point [GET]
+ Request (application/json)

        {
            "access_token": "dtgthzergateavnbategsbaebaenst4",
            "latitiude": 44.3,
            "longitude": 37.2
        }
    
+ Response 200 (application/json)

        {
                "status":200,
                "data": [
                        {
                                "id": "A unique string identifier for this venue", 
                                "stats": {
                                "checkinsCount": 1,
                                "usersCount": 1,
                                "tipCount": 1
                                },
                                "name": "The best known name for this venue.",
                                "category": "Name of the category",
                                "type": "social",
                                "lvl": 10,
                                "owner": 643688446,
                                "price": 1000,
                                "latitude": 44.4,
                                "longitude": 38.1
                        }
                ]
        }

## List user's objects [/user_objects]
### GET objects [GET]

+ Request (application/json)

        { 
            "access_token": "dtgthzergateavnbategsbaebaenst4"
        }
    
+ Response 200 (application/json)

        {
                "status":200,
                "data": [
                        {
                                "id": "A unique string identifier for this venue", 
                                "stats": {
                                "checkinsCount": 1,
                                "usersCount": 1,
                                "tipCount": 1
                                },
                                "name": "The best known name for this venue.",
                                "category": "Name of the category",
                                "type": "social",
                                "lvl": 10,
                                "owner": 643688446,
                                "price": 1000,
                                "latitude": 44.4,
                                "longitude": 38.1
                        }
                ]
        }
        
## Get object info [/object/{id}]      
### Get object [GET]
+ Request (application/json)

        {
            "access_token": "dtgthzergateavnbategsbaebaenst4"
        }
    
+ Response 200 (application/json)

        {
                "status":200,
                "data": {
                        "id": "A unique string identifier for this venue", 
                        "stats": {
                        "checkinsCount": 1,
                        "usersCount": 1,
                        "tipCount": 1
                        },
                        "name": "The best known name for this venue.",
                        "category": "Name of the category",
                        "type": "social",
                        "lvl": 10,
                        "owner": 643688446,
                        "price": 1000,
                        "latitude": 44.4,
                        "longitude": 38.1
                }
        }
  
## Do action with object [/object]      
### buy/sell/upgrade/collect_loot object [POST]
+ Request (application/json)

        {
            "access_token": "dtgthzergateavnbategsbaebaenst4",
            "action": "buy/sell/upgrade/collect_loot",
            "id": "A unique string identifier for this venue.",
        }
    
+ Response 200 (application/json)

        {
                "status":200,
                "data": {
                        "id": "A unique string identifier for this venue", 
                        "stats": {
                        "checkinsCount": 1,
                        "usersCount": 1,
                        "tipCount": 1
                        },
                        "name": "The best known name for this venue.",
                        "category": "Name of the category",
                        "type": "social",
                        "lvl": 10,
                        "owner": 643688446,
                        "price": 1000,
                        "latitude": 44.4,
                        "longitude": 38.1,
                        "profile": {}
                }
        }
        
## Rating [/rating]      
### GET users from rating [POST]
+ Request (application/json)

        { 
            "access_token": "dtgthzergateavnbategsbaebaenst4"
            "limit": 20,
            "offset": 50
        }
    
+ Response 200 (application/json)
        
        {
                "status":200,
                "data": [{
                    "position": 1,
                    "id": 43,
                    "name": "John",
                    "avatar": "http://url",
                    "cash": 3,
                }, 
                {
                    "position": 2,
                    "id": 3,
                    "name": "Anna",
                    "avatar": "http://url2",
                    "cash": 2,
                },
                {
                    "position": 3,
                    "id": 47,
                    "name": "Suzy",
                    "avatar": "http://url3",
                    "cash": 1,
                }]
        }

## Deals [/deals]
### Get deals list [GET]
+ Request (application/json)

        { 
            "access_token": "dtgthzergateavnbategsbaebaenst4"
        }
        
+ Response 200 (application/json)
        
        {
                "status":200,
                "data": [{
                    "id": 20,
                    "type": "outbox",
                    "user": 43,
                    "object": "A unique string identifier for this venue",
                    "price": 223
                }, 
                {
                    "id": 25,
                    "type": "inbox",
                    "user": 46,
                    "object": "A unique string identifier for this venue",
                    "price": 224
                }]
        }


### Response deal [POST]
+ Request (application/json)

        { 
            "access_token": "dtgthzergateavnbategsbaebaenst4",
            "deal_id": 44,
            "action": "accept/reject"
        }
        
+ Response 200 (application/json)
        
        {
                "status":200,
                "data": {
                        "id": "A unique string identifier for this venue", 
                        "stats": {
                        "checkinsCount": 1,
                        "usersCount": 1,
                        "tipCount": 1
                        },
                        "name": "The best known name for this venue.",
                        "category": "Name of the category",
                        "type": "social",
                        "lvl": 10,
                        "owner": 643688446,
                        "price": 1000,
                        "latitude": 44.4,
                        "longitude": 38.1
                        "profile: {}
                }
        }



## Profile [/profile]
### Get deals list [GET]
+ Request (application/json)

        { 
            "access_token": "dtgthzergateavnbategsbaebaenst4"
        }
        
+ Response 200 (application/json)
        
        {
                "status":200,
                "data": {
                    "id": 46,
                    "score": 6535,
                    "username: "Vasya Pupkin",
                    "level": 4,
                    "objects": 7,
                    "max_objects": 12
                }
        }
