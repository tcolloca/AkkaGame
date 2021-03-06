# Configuration

Most of the config values are on the config.properties file.

# How to Use

## User

### Create User

You can create an user under *&lt;host&gt;*:*&lt;port&gt;*/user/create?username=*&lt;username&gt;*.
If an user with such *username* exists, it will return an error response.

###### Example

&gt; http://localhost:8080/user/create?username=tom 

&gt; {  
&nbsp;&nbsp;"user": {  
&nbsp;&nbsp;&nbsp;&nbsp;"id": "-3104661399049034065",  
&nbsp;&nbsp;&nbsp;&nbsp;"username": "tom"  
&nbsp;&nbsp;}  
}

Will create the user "tom" and it will return its data.

### Get User

You can get an user's data under *&lt;host&gt;*:*&lt;port&gt;*/user/get?userId=*&lt;userId&gt;*.
If no such user exists it will return an error response.

###### Example

&gt; http://localhost:8080/user/get?userId=-3104661399049034065 

&gt; {  
&nbsp;&nbsp;"user": {  
&nbsp;&nbsp;&nbsp;&nbsp;"id": "-3104661399049034065",  
&nbsp;&nbsp;&nbsp;&nbsp;"username": "tom"  
&nbsp;&nbsp;}  
}  

Will return user's data with id = -3104661399049034065 .

## Game

### Create Game

You can create a game under *&lt;host&gt;*:*&lt;port&gt;*/game/create?userId=*&lt;userId&gt;* where the *userId* is the user's id as returned by the create user method. If the player is in a currently online game, it will return an error response saying  that the player is already in a game. 
It will return the host and port where the new game will be listening.

###### Example

&gt; http://localhost:8080/game/create?userId=-3104661399049034065

&gt; {  
&nbsp;&nbsp;"game": {  
&nbsp;&nbsp;&nbsp;&nbsp;"id": "6777034185468138167",  
&nbsp;&nbsp;&nbsp;&nbsp;"minSize": 2,  
&nbsp;&nbsp;&nbsp;&nbsp;"maxSize": 5,  
&nbsp;&nbsp;&nbsp;&nbsp;"userIds": ["-3104661399049034065"]  
&nbsp;&nbsp;},  
&nbsp;&nbsp;"host": "localhost",  
&nbsp;&nbsp;"port": 8081  
}  

Will create a new game with user with id -3104661399049034065 as a player. Players will be able to join and retrieve the game info by hitting localhost:8081.

### Join Game

You can create a game under *&lt;host&gt;*:*&lt;port&gt;*/game/join?userId=*&lt;userId&gt;* where the *userId* is the user's id joining the game, and *host*:*port* is where the game is listening. If the player is in a currently online game, in the current game, or the game is full, it will return an error response.

###### Example

&gt; http://localhost:8081/game/join?userId=-7584719550563300587

&gt; {  
}

User with id -7584719550563300587 will join the game hosted in localhost:8081.

### Get Game

You can get the game data under *&lt;host&gt;*:*&lt;port&gt;*/game/get where *host*:*port* is where the game is listening.
###### Example

&gt; http://localhost:8081/game/get

&gt; {  
&nbsp;&nbsp;"game": {  
&nbsp;&nbsp;&nbsp;&nbsp;"id": "6777034185468138167",  
&nbsp;&nbsp;&nbsp;&nbsp;"minSize": 2,  
&nbsp;&nbsp;&nbsp;&nbsp;"maxSize": 5,  
&nbsp;&nbsp;&nbsp;&nbsp;"userIds": ["-3104661399049034065", "-7584719550563300587"]  
&nbsp;&nbsp;}  
}

Returns the data of the game hosted in localhost:8081.

### Leave Game

You can leave a game under *&lt;host&gt;*:*&lt;port&gt;*/game/leave?userId=*&lt;userId&gt;* where the *userId* is the user's id leaving the game, and *host*:*port* is where the game is listening. If the player is not in that game it will return an error response.

###### Example

&gt; http://localhost:8081/game/leave?userId=-7584719550563300587

&gt; {  
}

User with id -7584719550563300587 will leave the game hosted in localhost:8081.

## System Information

### Get System Information

You can retrieve *N* system informations stored under *&lt;host&gt;*:*&lt;port&gt;*/system/get?amount=*&lt;amount&gt;* where *amount* is the amount of system informations to retrieve, sorted in descending order. 

###### Example

&gt; http://localhost:8080/system/get?amount=3

&gt; {  
&nbsp;&nbsp;"systemInfos": [{  
&nbsp;&nbsp;&nbsp;&nbsp;"timestamp": "1511564564010",  
&nbsp;&nbsp;&nbsp;&nbsp;"freeMemory": "127236976",  
&nbsp;&nbsp;&nbsp;&nbsp;"totalMemory": "164102144",  
&nbsp;&nbsp;&nbsp;&nbsp;"maxMemory": "1883242496"  
&nbsp;&nbsp;}, {  
&nbsp;&nbsp;&nbsp;&nbsp;"timestamp": "1511564503987",  
&nbsp;&nbsp;&nbsp;&nbsp;"freeMemory": "127932728",  
&nbsp;&nbsp;&nbsp;&nbsp;"totalMemory": "164102144",  
&nbsp;&nbsp;&nbsp;&nbsp;"maxMemory": "1883242496"  
&nbsp;&nbsp;}, {  
&nbsp;&nbsp;&nbsp;&nbsp;"timestamp": "1511564443967",  
&nbsp;&nbsp;&nbsp;&nbsp;"freeMemory": "128628352",  
&nbsp;&nbsp;&nbsp;&nbsp;"totalMemory": "164102144",  
&nbsp;&nbsp;&nbsp;&nbsp;"maxMemory": "1883242496"  
&nbsp;&nbsp;}]  
}

Will retrieve the last 3 system infos saved.
