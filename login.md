Basic Login Flow
================
* Launcher submits request to https://www.toontownrewritten.com/api/login
* Web layer responds with key=value\n response
* Client uses playcookie from response to launch game
* CSMUD on the server checks login token with web layer to find out what account is playing


**Note:** You can get your responses in json if you like by passing the GET parameter ?format=json
Detailed Overview
=================
Launcher POSTs formdata to /api/login: username, password<br/>
API responds in one of four ways, see below.
Failure response
----------------
```
success=false
banner=Your account has not yet been activated or is disabled.
```
The launcher should alert the client whatever the message is in the banner field.
Partially-authenticated response
--------------------------------
```
success=partial
banner=Please enter an authenticator token.
responseToken=deadbeef0x321
```
The user is using two-factor authentication. The username and password combination checked out, but you can't login just yet. Please POST again to /api/login with the following parameters:<br/>
appToken (one-time code), authToken (aforementioned responseToken)

The POST will either result in another success=partial with a different banner, or result in a success={true,delayed}.

Non-queued response
-------------------
<pre>success=true
gameserver=gameserver-alpha.toontownrewritten.com
cookie=deadbeefdeafbeef0x123</pre>
Set environment variables: TTR_GAMESERVER=<gameserver> and TTR_PLAYCOOKIE=<cookie>
Queued response
---------------
```
success=delayed
eta=60
position=15
queueToken=deafbeefdeafbeef0x321
```
A delayed response from /api/login indicates that the servers are full, and the player who wants to login must first wait for space to free up on the gameserver.

Periodically (no more than 30 second intervals), the launcher should POST to /api/login: queueToken <br/>
A sample response:
```
success=delayed
eta=30
position=7
```
This response indicates that the user has approximately 30 seconds until they may enter the game, and they are 7th in line. The launcher should continue checking /api/login and updating the user on its status.

Eventually, the launcher will get back from /api/login:
```
success=true
gameserver=gameserver-alpha.toontownrewritten.com
cookie=deadbeefdeafbeef0x123
```
The launcher should then boot the game with the provided play cookie.
