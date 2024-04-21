# CPmon

# After Pull
- add .env file with mongoDB string 

# notes
- BACK_URL : set to "http://localhost:3222"; while in dev process



# Updata 19-4-67
[Nadeem : Game System]
Backend has room 6 rooms each room at it own index
startGame()
1. user go in to waitingRoom.html
    - post userData -> addPlayer(player)
    - if error -> send back main
2. refreash startGame() every 5 sec. wait till 2 people
Room gaming : NaDeem & Tokyo Lets goooo in battlePlay.html
3. user out of room removePlayer(playerName)
extra: if user close page, respond time, timeout>30 sec -> userLogout()
endGame : exp for user +money +exp

[Beam: Front end]
- User (Neen will add 'avalible/unavalible' hai)
- gameWaitingRoom , gameBattleRoom (gameBattle use one from 3)
- Extra sound?

[Neen: Web API]
cookie -> http web postman
**IF** you use it in .js that not relate with html ex. check user in server.js(that will run before load html)
you **CAN'T** fetch data by youself
**BUT** if your funsion use in html ex. handle event listenner. you can use getCurrentUser() as the same

Next Step:
NADEEM : Route & Logic
TOKYO : implement game to frontend 
NEENNERA : user Update & user Data
BRNNBM : CSS master!!!!!!

# Update 20-4-67 night
New Backend endpoint

- /room
    - **GET**
        - /getRooms
            - get all rooms(instance of the game)
        - /getRoom/{id}
            - get room with specified id
            - see more of room things in backend/src/data/rooms.js
            - *IMPORTANT* all of the instance of room is in here
                - example: startGame, winner, turnPlayer(track player turn)
    - **POST**
        - /joinRoom/{id}
            - add player with "username" to the room {id}
            - already handle
                - same username exist in the same room
                - when the room is full
            - require "username":String in the request body
        - /addPokemon/{id} 
            - add pokemon in pokemonList in player with "username" in the room {id}
            - require "username":String in the request body
            - require "pokemonName":String in the request body
                - pokemonName can be added in data/CPmon.js
                - also Status can be found in models/Status.js
        - /removePlayer/{id}
            - remove player from a room {id}
            - require "username":String in the request body
        - /ready/{id}
            - if both player is ready, gameStart in room will be true
            - require "username":String in the request body
        - /action/{id}
            - require "username":String in the request body
            - require "action":String in the request body
                - 'attack': just attack damage = attack - def
                - 'guard': the next damage this unit recieve will calculate by 2xdef
                - 'magic': ignore def but your def-1
            - P.S. debug this one for an hour



change status 400 -> 200 with status "fail"
change const roomId = parseInt(req.params.id, 10) ->  const roomId = req.body.roomID
- bug : user join multiple room