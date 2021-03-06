# Buy-it API
Buy-it API is a *game* service similar to cashsquare
# Objects
## Venue 

        {
                "id": "MyObjectsId", 
                "stats": {
                        "checkinsCount": 1,
                        "usersCount": 1,
                        "tipCount": 1
                },
                "name": "MyObjectsName",
                "category": "Name of the category",
                "lvl": 10,
                "owner": {},
                "latitude": 44.4,
                "longitude": 38.1,
        }
        
## Private Venue 
        {
                "id": "MyObjectsId", 
                "stats": {
                "checkinsCount": 1,
                "usersCount": 1,
                "tipCount": 1
                },
                "name": "MyObjectsName",
                "category": "Name of the category",
                "lvl": 10,
                "owner": {},
                "latitude": 44.4,
                "longitude": 38.1,
                "max_loot": 900,
                "income": 12,
                "buy_price": null,
                "update_price": 1500,
                "sell_price": 500,
                "loot": 500,
                "expense": 34534,
                "consumption": 3453
        }
## User
        {
                "id": 43,
                "username": "John",
                "level": 5,
                "avatar": "http://url",
                "score": 3,
                "objects_count": 7,
                "max_objects": 12,
                "experience": 12,
        }

## Private User object
        {
                "id": 43,
                "username": "John",
                "level": 5,
                "avatar": "http://url",
                "score": 3,
                "objects_count": 7,
                "max_objects": 12,
                "experience": 12,
                "cache": 12
        }
        
## Objects [/zone/venues]
### Get objects around the point [GET]
+ Request (application/json)

        {
            "access_token": "dtgthzergateavnbategsbaebaenst4",
            "lat": 44.3,
            "lng": 37.2
        }
    
+ Response 200 (application/json)

        {
                "status":200,
                "venues": [list objects of public Venue's type] 
        }

Обратить внимание на различные стоимости. В зависимости от типа здания (моё, не моё, ничьё) возвращать нужные цены. Соответственно deal_price должна быть больше чем sell_price и меньше чем buy_price (предлагаю формулу для вычисления price=checkins\*f(lvl)\*k, где k - какой то коээфициент). Это стоимость купли/продажи здания между игроками и обоим сторонам это должно быть выгоднее, чем торговать с игрой. 

У здания должна быть граница, до которой копятся деньги на здании (max_loot) (предполагаю, что должно зависеть от уровня здания (max_loot=f(lvl)). По запросу POST /object action=collect_loot (см. ниже) счетчик здания обнуляется и loot переводится на счет игрока.

Хэши можно передавать в любом случае (null) или не передавать, если они не нужны. Наверное это дело вкуса. Или как то переструктурировать JSON.
"income"/"expence" - доход/расход за ед.вр. (1 час может быть?) вычисляется от чекинов и уровня здания??? + нужен какой то негативный фактор. Санэпидем или как то так.
## Profile [/profile/]
### GET user profile [GET]
+ Request (application/json)

        { 
                "access_token": "dtgthzergateavnbategsbaebaenst4",
                "id": 123456
        }
        
+ Response 200 (application/json)

        {
                "status":200,
                "venues": [public venue objects]
        }


## List players objects [/user/venues]
### GET objects [GET]

+ Request (application/json)

        { 
                "access_token": "dtgthzergateavnbategsbaebaenst4"
                "id": 12345
        }
        
+ Response 200 (application/json)

        {
                "status":200,
                "venues": [public venue objects]
        }
То же самое что и GET /my_objects, только возвращать объекты player'а по player_id.
        
## Get object info [/venue/info]      
### Get object [GET]
+ Request (application/json)

        {
                "access_token": "dtgthzergateavnbategsbaebaenst4",
                "venue_id": 123456
        }
    
+ Response 200 (application/json)

        {
                "status":200,
                "data": private/public Venue object
        }
        
  
## Do action with object [/venues/action]      
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
                "venue": (private if success else public) Venue object,
                "user": Private User object
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
                "users": [private list User's type objects],
                "user": User object
        }

Рейтинг лист. Позицию не передавать. Будет вычисляться как переданный offset + порядковый номер в массиве.

## Deals [/deals]
### Get deals list [GET]
+ Request (application/json)

        { 
            "access_token": "dtgthzergateavnbategsbaebaenst4"
        }
        
+ Response 200 (application/json)
        
        {
                "status":200,
                "deals": [{
                    'id': 
                    'venue': ,
                    'user_from': ,
                    'user_to': ,
                    'amount': ,
                    'date_added': ,
                    'date_expired': ,
                }, 
                {
                    'id': 
                    'venue': ,
                    'user_from': ,
                    'user_to': ,
                    'amount': ,
                    'date_added': ,
                    'date_expired': ,
                }]
        }

Список сделок. player - игрок с которым заключена сделка. object - объект. Стоимость сделки определяется полем deal_price object'а.

## Deals [/deals]
### Response deal [POST]
+ Request (application/json)

        { 
            "access_token": "dtgthzergateavnbategsbaebaenst4",
            "action": "accept/reject",
            "deal_id": 55
        }
        
+ Response 200 (application/json)
        
        {
                "status":200,
                "place": Venue object,
                selling_player: Player1 User object,
                buying_player: Player2 User object
        }

objects - текущее количество объектов в пользователя.
max_objects - максимальное количество объектов, которые пользователь может купить. max_objects = f(level).
