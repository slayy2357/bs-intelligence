## Trying to create an external AI that play brawl stars using internal functions of the game, jailbreak required
### Part 1 : make the AI to orient itself
#### Read the number of players left
- Able to read the number of players left (usually for showdown)
![alt text](https://raw.githubusercontent.com/slayy2357/bs-intelligence/refs/heads/main/pictures/1.png)
#### Get enemy coordinates in game (later)
### Part 2 : traffic
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
```
#### Payloads modifications tests
So, what we wan't to modify for example is this payload (the request when you join the training map with berry (black skin)) :
``` text
00000000  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
00000010  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
00000020  00 00 00 10 6c 61 73 65 72 5f 74 72 79 5f 62 75  ....laser_try_bu
00000030  74 74 6f 6e 00 00 00 74 7b 22 62 75 74 74 6f 6e  tton...t{"button
00000040  22 3a 32 2c 22 74 72 61 69 6e 69 6e 67 5f 63 6f  ":2,"training_co
00000050  6e 74 65 78 74 22 3a 32 2c 22 68 65 72 6f 22 3a  ntext":2,"hero":
00000060  31 36 30 30 30 30 38 32 2c 22 68 65 72 6f 5f 6f  16000082,"hero_o
00000070  77 6e 65 64 22 3a 74 72 75 65 2c 22 73 6b 69 6e  wned":true,"skin
00000080  22 3a 32 39 30 30 30 39 32 32 2c 22 73 6b 69 6e  ":29000922,"skin
00000090  5f 6f 77 6e 65 64 22 3a 74 72 75 65 2c 22 68 65  _owned":true,"he
000000a0  72 6f 5f 6c 65 76 65 6c 22 3a 31 7d              ro_level":1}
```
Replacing by lily's (no skin) request :
``` text
00000000  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
00000010  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
00000020  00 00 00 10 6c 61 73 65 72 5f 74 72 79 5f 62 75  ....laser_try_bu
00000030  74 74 6f 6e 00 00 00 74 7b 22 62 75 74 74 6f 6e  tton...t{"button
00000040  22 3a 32 2c 22 74 72 61 69 6e 69 6e 67 5f 63 6f  ":2,"training_co
00000050  6e 74 65 78 74 22 3a 32 2c 22 68 65 72 6f 22 3a  ntext":2,"hero":
00000060  31 36 30 30 30 30 38 31 2c 22 68 65 72 6f 5f 6f  16000081,"hero_o
00000070  77 6e 65 64 22 3a 74 72 75 65 2c 22 73 6b 69 6e  wned":true,"skin
00000080  22 3a 32 39 30 30 30 38 35 34 2c 22 73 6b 69 6e  ":29000854,"skin
00000090  5f 6f 77 6e 65 64 22 3a 74 72 75 65 2c 22 68 65  _owned":true,"he
000000a0  72 6f 5f 6c 65 76 65 6c 22 3a 31 7d              ro_level":1}
```
Result :