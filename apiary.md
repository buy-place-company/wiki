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
                "places": [{
                                "id": "MyObjectsId", 
                                "stats": {
                                "checkinsCount": 1,
                                "usersCount": 1,
                                "tipCount": 1
                                },
                                "name": "MyObjectsName",
                                "category": "Name of the category",
                                "type": "social",
                                "lvl": 10,
                                "owner": 643688446,
                                "latitude": 44.4,
                                "longitude": 38.1,
                                "max_loot": 900,
                                "buy_price": null,
                                "update_price": 1500,
                                "sell_price": 500,
                                "deal_price": 750,
                                "loot": 412
                        },
                        {
                                "id": "AnothersObjectsId", 
                                "stats": {
                                "checkinsCount": 1,
                                "usersCount": 1,
                                "tipCount": 1
                                },
                                "name": "AnotherObjectsName",
                                "category": "Name of the category",
                                "type": "social",
                                "lvl": 10,
                                "owner": 643688446,
                                "latitude": 44.4,
                                "longitude": 38.1,
                                "max_loot": null,
                                "buy_price": null,
                                "update_price": null,
                                "sell_price": null,
                                "deal_price": 750,
                                "loot": null
                        },
                        {
                                "id": "NobodysObjectsId", 
                                "stats": {
                                "checkinsCount": 1,
                                "usersCount": 1,
                                "tipCount": 1
                                },
                                "name": "NobodysObjectsName",
                                "category": "Name of the category",
                                "type": "social",
                                "lvl": 10,
                                "owner": 643688446,
                                "latitude": 44.4,
                                "longitude": 38.1,
                                "max_loot": null,
                                "buy_price": 1000,
                                "update_price": null,
                                "sell_price": null,
                                "deal_price": null,
                                "loot": null
                }]
        }

Обратить внимание на различные стоимости. В зависимости от типа здания (моё, не моё, ничьё) возвращать нужные цены. Соответственно deal_price должна быть больше чем sell_price и меньше чем buy_price (предлагаю формулу для вычисления price=checkins*f(lvl)*k, где k - какой то коээфициент). Это стоимость купли/продажи здания между игроками и обоим сторонам это должно быть выгоднее, чем торговать с игрой. 

У здания должна быть граница, до которой копятся деньги на здании (max_loot) (предполагаю, что должно зависеть от уровня здания (max_loot=f(lvl)). По запросу POST /object action=collect_loot (см. ниже) счетчик здания обнуляется и loot переводится на счет игрока.

Хэши можно передавать в любом случае (null) или не передавать, если они не нужны. Наверное это дело вкуса. Или как то переструктурировать JSON.


## List user's objects [/my_objects]
### GET objects [GET]

+ Request (application/json)

        { 
                "access_token": "dtgthzergateavnbategsbaebaenst4"
        }
    
+ Response 200 (application/json)

        {
                "status":200,
                "places": [{
                                "id": "MyObjectsId", 
                                "stats": {
                                "checkinsCount": 1,
                                "usersCount": 1,
                                "tipCount": 1
                                },
                                "name": "MyObjectsName",
                                "category": "Name of the category",
                                "type": "social",
                                "lvl": 10,
                                "owner": 643688446,
                                "latitude": 44.4,
                                "longitude": 38.1,
                                "max_loot": 900,
                                "buy_price": null,
                                "update_price": 1500,
                                "sell_price": 500,
                                "deal_price": 750,
                                "loot": 412
                }]
        }

## List players objects [/players_objects/{players_id}]
### GET objects [GET]

+ Request (application/json)

        { 
                "access_token": "dtgthzergateavnbategsbaebaenst4"
        }
        
+ Response 200 (application/json)

        {
                "status":200,
                "places": [{
                                "id": "AnothersObjectsId", 
                                "stats": {
                                "checkinsCount": 1,
                                "usersCount": 1,
                                "tipCount": 1
                                },
                                "name": "AnotherObjectsName",
                                "category": "Name of the category",
                                "type": "social",
                                "lvl": 10,
                                "owner": 643688446,
                                "latitude": 44.4,
                                "longitude": 38.1,
                                "max_loot": null,
                                "buy_price": null,
                                "update_price": null,
                                "sell_price": null,
                                "deal_price": 750,
                                "loot": null
                }]
        }
То же самое что и GET /my_objects, только возвращать объекты player'а по player_id.
        
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
                                "id": "MyObjectsId", 
                                "stats": {
                                "checkinsCount": 1,
                                "usersCount": 1,
                                "tipCount": 1
                                },
                                "name": "MyObjectsName",
                                "category": "Name of the category",
                                "type": "social",
                                "lvl": 10,
                                "owner": 643688446,
                                "latitude": 44.4,
                                "longitude": 38.1,
                                "max_loot": 900,
                                "buy_price": null,
                                "update_price": 1500,
                                "sell_price": 500,
                                "deal_price": 750,
                                "loot": 412
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
                "place": {
                                "id": "MyObjectsId", 
                                "stats": {
                                "checkinsCount": 1,
                                "usersCount": 1,
                                "tipCount": 1
                                },
                                "name": "MyObjectsName",
                                "category": "Name of the category",
                                "type": "social",
                                "lvl": 10,
                                "owner": 643688446,
                                "latitude": 44.4,
                                "longitude": 38.1,
                                "max_loot": 900,
                                "buy_price": null,
                                "update_price": 1500,
                                "sell_price": 500,
                                "deal_price": 750,
                                "loot": 412
                },
                profile: {
                                "id": 46,
                                "score": 6535,
                                "username: "Vasya Pupkin",
                                "level": 4,
                                "objects": 7,
                                "max_objects": 12,
                                "avatar": "http://url"
                }
        }
buy - купить у игры.
sell - продать игре.
upgrade - улучшить.
collect_loot - собрать loot.
Возвращать объект, над которым производится действие и профиль игрока.
        
## Rating [/rating]      
### GET users from rating [GET]
+ Request (application/json)

        { 
            "access_token": "dtgthzergateavnbategsbaebaenst4"
            "limit": 20,
            "offset": 50
        }
    
+ Response 200 (application/json)
        
        {
                "status":200,
                "rating": [{
                        "id": 43,
                        "username": "John",
                        "level": 5,
                        "avatar": "http://url",
                        "score": 3,
                        "objects": 7,
                        "max_objects": 12
                }, 
                {
                        "id": 3,
                        "username": "Anna",
                        "level" : 3,
                        "avatar": "http://url2",
                        "score": 2,
                        "objects": 7,
                        "max_objects": 12
                },
                {
                        "id": 47,
                        "username": "Suzy",
                        "level": 5,
                        "avatar": "http://url3",
                        "score": 1,
                        "objects": 7,
                        "max_objects": 12
                }],
                "profile": {
                        "id": 46,
                        "score": 6535,
                        "username: "Vasya Pupkin",
                        "level": 4,
                        "avatar": "http://url",
                        "objects": 7,
                        "max_objects": 12,
                
                }
        }

Рейтинг лист. Позицию не передавать. Будет вычисляться как переданный offset + порядковый номер в массиве.

## Rating [/rating/{user_id}]      
### GET user from rating [POST]
+ Request (application/json)

        { 
            "access_token": "dtgthzergateavnbategsbaebaenst4"
            "limit": 20,
            "offset": 50
        }
    
+ Response 200 (application/json)
        
        {
                "status":200,
                "player": {
                        "id": 43,
                        "username": "John",
                        "level": 2,
                        "avatar": "http://url",
                        "score": 3,
                        "objects": 7,
                        "max_objects": 12
                }
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
                    "player": {},
                    "object": {}
                }, 
                {
                    "id": 25,
                    "type": "inbox",
                    "player": {},
                    "object": {}
                }]
        }

Список сделок. player - игрок с которым заключена сделка. object - объект. Стоимость сделки определяется полем deal_price object'а.

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
                "place": {
                                "id": "MyObjectsId", 
                                "stats": {
                                "checkinsCount": 1,
                                "usersCount": 1,
                                "tipCount": 1
                                },
                                "name": "MyObjectsName",
                                "category": "Name of the category",
                                "type": "social",
                                "lvl": 10,
                                "owner": 643688446,
                                "latitude": 44.4,
                                "longitude": 38.1,
                                "max_loot": 900,
                                "buy_price": null,
                                "update_price": 1500,
                                "sell_price": 500,
                                "deal_price": 750,
                                "loot": 412
                },
                profile: {
                                "id": 46,
                                "score": 6535,
                                "username: "Vasya Pupkin",
                                "level": 4,
                                "objects": 7,
                                "max_objects": 12,
                                "avatar": "http://url"
                },
                player: {
                                "id": 43,
                                "username": "John",
                                "level": 2,
                                "avatar": "http://url",
                                "score": 3,
                                "objects": 7,
                                "max_objects": 12
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
                        "avatar": "http://url",
                        "level": 4,
                        "objects": 7,
                        "max_objects": 12
                }
        }
objects - текущее количество объектов в пользователя.
max_objects - максимальное количество объектов, которые пользователь может купить. max_objects = f(level).
