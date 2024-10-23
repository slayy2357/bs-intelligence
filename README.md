## Trying to create an external AI that play brawl stars using internal functions of the game, jailbreak required
### Part 1 : make the AI to orient itself
#### Read the number of players left
- Able to read the number of players left (usually for showdown)
![alt text](https://raw.githubusercontent.com/slayy2357/bs-intelligence/refs/heads/main/pictures/1.png)
#### Get enemy coordinates in game (later)
### Part 2 : traffic (upload from client)
#### Dynamic analyse : POST requests (crypted)
crypted request example : [crypted-001.txt](https://github.com/slayy2357/bs-intelligence/blob/main/dump/requests/crypted-001.txt)  
If you change anything (for the joining request example) :
![alt text](https://raw.githubusercontent.com/slayy2357/bs-intelligence/refs/heads/main/pictures/5.png)
#### Decrypting traffic
- To decrypt requests, we first need to understand how the game encrypts them by analyzing the functions that call POST requests :
[backtrace-001.txt](https://github.com/slayy2357/bs-intelligence/blob/main/dump/requests/backtrace-001.txt)
- 101c13460 payload analyse :
[101c13460.txt](https://github.com/slayy2357/bs-intelligence/blob/main/dump/requests/101c13460.txt)  
So we need to focus on the data pointed by arg2 modifications BEFORE 101c13460 bcause already encrypted  
The best way to understand is probably here, backtracing and analysing, but later
- Analysing modules
```text
libCommonCrypto.dylib
CCSHA256 : error
CCSHA1   : error
CCMD5    : error
CCCrypt  : 1 call :
```
[cccrypt-001.txt](https://github.com/slayy2357/bs-intelligence/blob/main/dump/requests/cccrypt-001.txt)
``` text
libboringssl.dylib
SSL_write          : 20+ call //interessant
SSL_read           : 20+ call, example when you look other profiles :
```
[ssl_read-001.txt](https://github.com/slayy2357/bs-intelligence/blob/main/dump/requests/ssl_read-001.txt)  
So, we can read some payloads before encryption through SSL_write, SSL_read, and CCCrypt, but those aren't the main payloads. What we want to intercept is the payload sent through the send function before encryption, as that's how the game communicates with the server—for example, when joining a game, using emotes, etc
- Strategy to read the payload of send BEFORE encryption
``` text
We know that:

The first requests are ALWAYS in the same order, for example:

request A
request B
Request A will ALWAYS be sent before request B, and the gap between their payload addresses in memory is ALWAYS the same. For example:

request A (0x100); // payload address
request B (0x200); // payload address
So, based on this, we can predict the address of payload B before it is created:

payload B = payload A + 0x100
This allows us to hook the address in memory before the payload is encrypted / writed to see which function or address writes the encrypted payload b.

For example, the memory where payload B will be written looks like this before encryption: 0000 0000 0000 0000.

We place a hook at this memory location.
The encryption function (e.g., 0x1c121e) writes to this location: 1010 1000 1010 1000.
BOOM, our hook is triggered, called by the encryption function at 0x1c121e.
```
Alright, I haven't found the encryption function yet, but now I'm able to read and modify every payload before encryption
#### Decrypted payloads analyses
(!) : Decrypted payloads are not necessarily readable. Decrypted means that the structure is logical and will be the same for all payloads  
- Dump of "interessant" payload found for the moment :  
[the first request](https://github.com/slayy2357/bs-intelligence/blob/main/dump/requests/decrypted-001.txt)  
``` text
Analyse :
00000090  00 00 00 28 36 31 62 32 61 64 38 36 32 64 63 35  ...(61b2ad862dc5
000000a0  61 65 62 62 30 65 31 30 61 30 30 33 32 39 62 62  aebb0e10a00329bb
000000b0  66 66 32 65 66 37 34 38 61 39 62 64 00 00 00 09  ff2ef748a9bd....
//this look like an ID, if you modify it you can't access to the game

000000c0  69 50 61 64 31 33 2c 31 30 01 03 00 00 00 05 66  iPad13,10......f
000000d0  72 2d 43 48 00 00 00 04 31 36 2e 32 00 00 00 00  r-CH....16.2....
//the device model, current country / region and the iOS version

000000e0  00 00 00 00 00 00 00 00 00 24 44 35 42 43 32 45  .........$D5BC2E
000000f0  37 30 2d 42 46 44 39 2d 34 38 33 36 2d 42 44 42  70-BFD9-4836-BDB
00000100  44 2d 33 33 32 34 33 42 35 30 45 30 36 38 00 00  D-33243B50E068..
//bundle ID or something ?

00000110  05 a8 01 00 00 00 06 35 37 2e 33 32 35 00 00 00  .......57.325...
//game version

00000320  00 00 00 00 00 00 00 00 00 03 46 52 41 00 00 00  ..........FRA...
//country ?

00000330  06 31 34 33 34 34 32                             .143442
//maybe an ID
//end of "readable" analyse of first req, back later to analyse / understand unreadable things
```
[the render request](https://github.com/slayy2357/bs-intelligence/blob/main/dump/requests/decrypted-002.txt)  
``` text
Analyse :
//the request look like an evaluation of performances, render e.g

000001d0  04 31 36 2e 32 00 00 00 09 69 50 61 64 31 33 2c  .16.2....iPad13,
000001e0  31 30 00 00 00 00                                10....
//iOS version, device model
```
[shop request 1](https://github.com/slayy2357/bs-intelligence/blob/main/dump/requests/decrypted-003.txt), [shop request 2](https://github.com/slayy2357/bs-intelligence/blob/main/dump/requests/decrypted-004.txt)
``` text
Analyse :
//requests used for the shop, req1 is auto, req2 when you open the shop

//req 1 = infos about transactions e.g
//req 2 = action (open the shop), and if you can buy items in the shop with money, if your game is an outstore installation, modified e.g, security don't let you buy with money I guess

00000040  68 6f 70 22 2c 22 70 72 6f 64 75 63 74 22 3a 22  hop","product":"
00000050  62 69 6c 6c 69 6e 67 4f 6b 22 2c 22 70 72 6f 64  billingOk","prod //I can buy, because modifications of AppStore official app ?
```
[open news request 1](https://github.com/slayy2357/bs-intelligence/blob/main/dump/requests/decrypted-005.txt), [open news request 2](https://github.com/slayy2357/bs-intelligence/blob/main/dump/requests/decrypted-006.txt)
``` text
Analyse :
//parameters like url, opened time, action e.g
```
[web API request ?](https://github.com/slayy2357/bs-intelligence/blob/main/dump/requests/decrypted-007.txt)  
[join training map request](https://github.com/slayy2357/bs-intelligence/blob/main/dump/requests/decrypted-008.txt)
``` text
Analyse :
"button":2 probably the choice if you wan't to be in training map or training match vs bots
"training_context":2 same
"hero":16000067 the static ID of your hero, here willow for example
"hero_owned":true if you have the hero
"skin":29000629 the static ID of your skin, here default willow
"skin_owned":true if you have the skin
"hero_level":11 the level of your hero
"gadget":23000564 the static ID of your gadget
"star_power":23000562 the static ID of your star power
"gear1":62000004 the static ID of your gear 1
"gear2":62000002 the static ID of your gear 2
```
[send text message in chat request](https://github.com/slayy2357/bs-intelligence/blob/main/dump/requests/decrypted-009.txt)
``` text
Analyse :
00000000  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
00000010  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
00000020  00 00 00 04 6c 6d 61 6f                          ....lmao
//the message that I send
```
[send emote in chat request 1](https://github.com/slayy2357/bs-intelligence/blob/main/dump/requests/decrypted-010.txt), [send emote in chat request 2](https://github.com/slayy2357/bs-intelligence/blob/main/dump/requests/decrypted-011.txt)
``` text
Analyse :
//request emote 1
00000000  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
00000010  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
00000020  28 2e 00 00 88 f0 cb 31 00                       (......1.

//request emote 2
00000000  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
00000010  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
00000020  28 2e 00 00 89 f0 cb 31 00                       (......1.

//here emotes ID are 0x88 and 0x89, it's the place in a list (0x88=brawl stars emote, 0x89=numbers emote):
```
![alt text](https://raw.githubusercontent.com/slayy2357/bs-intelligence/refs/heads/main/pictures/6.png)
[game/screen status request 1](https://github.com/slayy2357/bs-intelligence/blob/main/dump/requests/decrypted-012.txt), [game/screen status request 2](https://github.com/slayy2357/bs-intelligence/blob/main/dump/requests/decrypted-013.txt)
``` text
Analyse :
//request 1
00000020  00 00 00 09 6c 61 73 65 72 5f 66 70 73 00 00 00  ....laser_fps...
00000030  2e 7b 22 66 70 73 22 3a 35 37 2c 22 6d 6f 64 65  .{"fps":57,"mode
00000040  22 3a 22 69 6e 67 61 6d 65 22 2c 22 6c 6f 63 61  ":"ingame","loca
00000050  74 69 6f 6e 22 3a 31 35 30 30 30 37 37 36 7d     tion":15000776}

//request 2
00000020  00 00 00 09 6c 61 73 65 72 5f 66 70 73 00 00 00  ....laser_fps...
00000030  18 7b 22 66 70 73 22 3a 35 39 2c 22 6d 6f 64 65  .{"fps":59,"mode
00000040  22 3a 22 6d 65 6e 75 22 7d                       ":"menu"}

//request 1 when you are in game and switch back to menu mode
//request 2 when you are in menu and switch to game mode (black borders maybe)
```
[all tutorial requests](https://github.com/slayy2357/bs-intelligence/blob/main/dump/requests/decrypted-014.txt)  
[catalog request](https://github.com/slayy2357/bs-intelligence/blob/main/dump/requests/decrypted-015.txt)
``` text
Analyse :
//the action and previous location
```
#### Payloads modifications
I also tried modifying different requests, and everything worked: changing the chosen hero, modifying the chat message, chat emote, ingame emotes, e.g
I'm still working on the player position payload, rewards, etc., but I'll get back to that later
### Part 3 : traffic (response from server)
#### Dynamic analyse : responses (crypted)