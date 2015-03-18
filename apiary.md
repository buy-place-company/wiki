FORMAT: 1A

# Buy-it API
Buy-it API is a *game* service similar to cashsquare

## Objects [/objects_near]
### Get objects near ll [GET]
+ Request (application/json)

        {
            "lat": 44.3,
            "lng": 37.2
        }
    
+ Response 200 (application/json)

        [{
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
            "price": 1000
        },
        ]

## List user's objects [/user_objects]
### GET objects [GET]

+ Request (application/json)

        { }
    
+ Response 200 (application/json)

        [{
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
            "price": 1000
        },
        ]
  
## List user's objects [/object]      
### GET object by id [POST]
+ Request (application/json)

        {
            "action": "buy/sell/upgrade",
            "id": "A unique string identifier for this venue.",
        }
    
+ Response 200 (application/json)

        [{
            "status": "ok",
            "code": "0",
            "cash": 0,
        }, 
        {
            "status": "error",
            "code": "100",
        },
        {
            "status": "undone",
            "code": "200",
            "price": 647647,
            "cash": 0,
        }
        ]

        
## Rating [/rating]      
### GET users from rating [POST]
+ Request (application/json)

        { }
    
+ Response 200 (application/json)

        [{
            "name": "John",
            "avatar": "http://url",
            "cash": 3,
        }, 
        {
            "name": "Anna",
            "avatar": "http://url2",
            "cash": 2,
        },
        {
            "name": "Suzy",
            "avatar": "http://url3",
            "cash": 1,
        },
        {
            
        }
        ]        
        
