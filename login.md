# Toontown Rewritten Login API


## Basic Login Flow
* Launcher submits request to https://www.toontownrewritten.com/api/login
* Web layer responds with key=value\n response
* Client uses playcookie from response to launch game, client also connects to the IP provided in the response
* Gameserver checks with web layer to find out which account is playing

**Note:** Responses will be provided in JSON by POSTing to the URL https://www.toontownrewritten.com/api/login?format=json

## Calling the API
All calls to the Login API should be made via a POST to the full TTR API endpoint (www and https will be added via a redirect if they are not present). Be sure to include the proper headers in your request:
```
"Content-type": "application/x-www-form-urlencoded"
```
The API responds with a set of key value pairs. All keys and values will be strings.

## Detailed Overview
Launcher begins by collecting a username and password from the user.

### Request
| Name     | Details                              |
|----------|--------------------------------------|
| username | The username collected from the user |
| password | The password collected from the user |

API responds in one of four ways, see below.
### Failure response
```
success=false
banner=Your account has not yet been activated or is disabled.
```
```json
{"success":"false","banner":"Your account has not yet been activated or is disabled."}
```
The launcher should alert the client whatever the message is in the banner field. The attempt to login is now over.
### Partially-authenticated response
```
success=partial
banner=Please enter an authenticator token.
responseToken=deadbeef0x321
```
```json
{"success":"partial","banner":"Please enter an authenticator token.","responseToken":"deadbeef0x321"}
```
The user is using two-factor authentication. The username and password combination checked out, but you can't login just yet. Display the prompt in the banner from the user, and collect a token from them. Make another request:
#### Partially-authenticated request
| Name      | Details                                                |
|-----------|--------------------------------------------------------|
| appToken  | The token collected from the user                      |
| authToken | The token sent in the partially authenticated response |

This subsequent request will either result in another success=partial with a different banner, or result in a success={true,delayed}.

### Non-queued response
```
success=true
gameserver=gameserver-alpha.toontownrewritten.com
cookie=deadbeefdeafbeef0x123
```
```json
{"success":"true","gameserver":"gameserver-alpha.toontownrewritten.com","cookie":"deadbeefdeafbeef0x123"}
```
The user can now login! Set the environment variable TTR_GAMESERVER to the value of the gameserver key, and the environment variable TTR_PLAYCOOKIE to the value of the cookie key, then boot the game.

### Queued response
```
success=delayed
eta=60
position=15
queueToken=deafbeefdeafbeef0x321
```
```json
{"success":"delayed","eta":"60","position":"15","queueToken":"deafbeefdeafbeef0x321"}
```
A delayed response from /api/login indicates that the servers are full, and the player who wants to login must first wait for space to free up on the gameserver.

Periodically (no more than 30 second intervals), the launcher should POST again:
#### Queued request
| Name       | Details                                         |
|------------|-------------------------------------------------|
| queueToken | The token given in the initial delayed response |

The queueToken update request will result in either a success=delayed, or a success=true/false.
A sample response:
```
success=delayed
eta=30
position=7
```
This response indicates that the user has approximately 30 seconds until they may enter the game, and they are 7th in line. The launcher should continue checking /api/login and updating the user on its status.

Eventually, the launcher will get back from /api/login a success=true response (unless something goes wrong and success=false), and the game should be booted with the provided credentials.
