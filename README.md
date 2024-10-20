## Trying to create an external AI that play brawl stars using internal functions of the game, jailbreak required
### Part 1 : make the AI to orient itself
#### Read the number of players left
- Able to read the number of players left (usually for showdown)
![alt text](https://raw.githubusercontent.com/slayy2357/bs-intelligence/refs/heads/main/pictures/1.png)
#### Get enemy coordinates in game (later)
### Part 2 : traffic
#### Dynamic analyse : POST requests (crypted)
- Example request when you join the training room : darryl
```text
//bloc of request 1
//req 1
Partially Printable Data (Hex & String): 7.......v({.??.tPq...zy.....l.70
Hex: 37 16 00 00 19 00 00 a4 76 28 7b f7 3f 3f c5 74 50 71 9b a9 00 7a 79 83 8f a7 84 ee 6c c3 37 30
Request sent to: 182.138.227.44:528
//req 2
Partially Printable Data (Hex & String): 7&......t...`....Q\.?.0..r.y..BL
Hex: 37 26 00 00 19 00 00 11 74 ea a1 ab 60 97 10 e1 9c 51 5c f4 3f e5 30 dc ba 72 13 79 17 c2 42 4c
Request sent to: 182.138.227.44:528
//req 3
Partially Printable Data (Hex & String): .~.....B...S..........F.b....C....w......U.i...i.......q..9.L4.w............. .H......Z.fu.....U3M.(..g..s.2.....oRM.ZE..IzbU........1.yX.....E~}-....*......sv.p..
Hex: 27 7e 00 00 9c 00 00 42 c2 cf 96 53 80 1d 11 88 87 98 03 12 17 c9 46 10 62 b6 22 06 c3 43 2e 8f dc c1 77 87 be a6 ae 15 8f 55 7f 69 b1 8a e0 69 0c b9 d3 a4 d2 18 dc 71 fc e4 39 bd 4c 34 cc 77 ce d6 95 df d3 ae c3 da 1b 98 f2 8b 98 20 cc 48 1b d6 c1 cf fa 1f 5a 1d 66 75 df 16 12 1d e8 55 33 4d 9b 28 c6 e7 67 0a 84 73 a3 32 da 0e aa cb a4 6f 52 4d 7f 5a 45 f0 e7 49 7a 62 55 c6 e9 fb 06 97 e9 dd dc 31 e4 79 58 cd 2e 1a bd 9a 45 7e 7d 2d 08 87 a2 18 2a b3 0e a9 8e d3 b3 73 76 1e 70 b2 12
Request sent to: 182.138.227.44:528
//req 4
Partially Printable Data (Hex & String): 8..........H.........S...
Hex: 38 1e 00 00 12 00 00 0f af bc ed 48 d4 e2 f8 b8 b9 d4 eb fe be 53 eb bf a2
Request sent to: 182.138.227.44:528


//bloc of request 2, same request as request 1 but later, with the same character
//req 1
Partially Printable Data (Hex & String): 7......,?..r._.......c......)...
Hex: 37 16 00 00 19 00 00 2c 3f dd da 72 b3 5f a9 d2 a0 19 14 ad 91 63 a5 da 8d d1 81 93 29 90 d1 0b
Request sent to: 182.138.227.44:528
//req 2
Partially Printable Data (Hex & String): 7&.............^5@...G...N.-.=..
Hex: 37 26 00 00 19 00 00 d5 9e f0 9b ef 9c 00 95 5e 35 40 18 fa 0a 47 22 92 ba 4e 91 2d a7 3d fc 18
Request sent to: 182.138.227.44:528
//req 3
Partially Printable Data (Hex & String): .~..........._.H.XQ.r.j@..ShfQ...fn.......{|CXG.-...&d...,p..Hf.....GE.L..+.Q....L...|.O...gY<n_...m!U.y..zW.h...yU..!Xz3}..l....#.-.n.9)@CI....ZC..HU..h..r.uL..Mk
Hex: 27 7e 00 00 9c 00 00 9e 83 0e 88 d8 dc 5f 99 48 c9 58 51 cd 72 b4 6a 40 b0 bc 53 68 66 51 a0 92 db 66 6e c2 a5 e1 ce 97 b4 92 7b 7c 43 58 47 ef 2d 05 22 1c 26 64 91 8d 00 2c 70 e1 e7 48 66 e5 9d db 0e ef 47 45 1f 4c a6 d3 2b a0 51 f4 19 cb e5 4c 80 13 c4 7c 97 4f a2 86 ee 67 59 3c 6e 5f d0 a5 b0 6d 21 55 1f 79 92 c2 7a 57 83 68 f3 e9 fe 79 55 0e ac 21 58 7a 33 7d ee 00 6c dd c2 bd 8a 23 d5 2d bd 6e 17 39 29 40 43 49 8d f1 fd e3 5a 43 b3 99 48 55 90 92 68 f8 a4 72 c0 75 4c ff 8f 4d 6b
Request sent to: 182.138.227.44:528
//req 4
Partially Printable Data (Hex & String): 8......j..r....*..,.=.H._
Hex: 38 1e 00 00 12 00 00 6a da ff 72 fc 01 11 aa 2a 81 e7 2c ed 3d f1 48 ac 5f
Request sent to: 182.138.227.44:528
```
- Example request when you join the training room : buzz
```text
//bloc of request 1
//req 1
Partially Printable Data (Hex & String): 7.......+*]...7....p.........4.H
Hex: 37 16 00 00 19 00 00 9b 2b 2a 5d 91 ab ce 37 9a c8 f6 81 70 e8 d8 1b a7 fe 98 a3 19 00 34 d5 48
Request sent to: 182.138.227.44:528
//req 2
Partially Printable Data (Hex & String): 7&.........mL...A.`|...*Jq.y.....
Hex: 37 26 00 00 1a 00 00 c7 9d e8 d0 6d 4c e0 dc ce 41 bf 60 7c bb d8 e9 2a 4a 71 f9 79 d6 d0 fe e4 c3
Request sent to: 182.138.227.44:528
//req 3
Partially Printable Data (Hex & String): .~.........<.=)-N..Nl.....]...P..C4...P...^O.S.X.#..+..G.)_......Q.O..M.9g..x.......Z..3G..>.=[......E8......7X/......}J.|..m.*......a..UAP..;;.....$].\j.S$...~.._
Hex: 27 7e 00 00 9c 00 00 05 1e 1d 1d 3c f0 3d 29 2d 4e 83 cd 4e 6c 90 fc 04 8e d2 5d 83 8c bd 50 a5 00 43 34 c2 96 07 50 b5 ad 98 5e 4f 9a 53 ed 58 88 23 1e b5 2b e5 f1 47 a0 29 5f 99 85 f9 90 86 a5 51 ed 4f a0 f2 4d b4 39 67 ff ce 78 ed d4 99 cf aa 00 1d 5a ad 97 33 47 f2 1d 3e 0a 3d 5b aa 1d 87 d3 15 b8 45 38 15 db 10 1f 90 f4 37 58 2f 80 e7 9a 93 84 ac 7d 4a f1 7c 90 02 6d 10 2a fd b3 c5 a6 94 f8 61 22 c9 55 41 50 d5 1a 3b 3b fd a4 a9 0a 95 24 5d dc 5c 6a f5 53 24 f7 fd af 7e 60 8e 5f
Request sent to: 182.138.227.44:528
//req 4
Partially Printable Data (Hex & String): 8............=Z.F.4.v.9..
Hex: 38 1e 00 00 12 00 00 8e ef 8f 12 97 ca 3d 5a 03 46 10 34 9c 76 cb 39 ed b9
Request sent to: 182.138.227.44:528


//bloc of request 2, same request as request 1 but later, with the same character
//req 1
Partially Printable Data (Hex & String): 7......l/..e.5Y..O....#lwH.B=.. 
Hex: 37 16 00 00 19 00 00 6c 2f 84 ab 65 9a 35 59 97 ab 4f cd dc a4 c8 23 6c 77 48 d5 42 3d 0e c6 20
Request sent to: 182.138.227.44:528
//req 2
Partially Printable Data (Hex & String): 7&.....m......~........6.D...5s.i
Hex: 37 26 00 00 1a 00 00 6d 0c aa d1 27 eb 15 7e 06 af 14 f8 a0 b4 fb ce 36 8f 44 d5 e5 ef 35 73 93 69
Request sent to: 182.138.227.44:528
//req 3
Partially Printable Data (Hex & String): .~.....S.@.2...<..zlE<.1d.`.G.......w..D.\. ..e.T.....\lT\7....ViG...[.j..]7}...CKQ.....TS.h...(J.`....J......T....N.<.M.....al.Q....>.........d..7L.Ag...8....v..x
Hex: 27 7e 00 00 9c 00 00 53 e1 40 93 32 05 09 95 3c ea fd 7a 6c 45 3c 81 31 64 fa 60 0d 47 e1 15 ea aa d2 c1 84 77 bf ff 44 85 5c 00 20 bb 9e 65 a0 54 ed bc fe c3 e7 5c 6c 54 5c 37 96 bd c6 80 56 69 47 c1 06 d0 5b 9e 6a a4 d7 5d 37 7d f7 a1 a0 43 4b 51 b0 a2 f1 9d 8f 54 53 c8 68 cf f2 a8 28 4a 14 60 c2 0e 8e 80 4a bf be fc a3 e2 cb 54 98 fa a2 cf 4e f0 3c e1 4d 1e b9 06 f5 93 61 6c 04 51 f1 89 09 d8 3e e1 10 96 97 ef d4 9c ad f9 64 b0 cc 37 4c 9b 41 67 0b f8 8a 38 aa a9 a8 f2 76 f8 89 78
Request sent to: 182.138.227.44:528
//req 4
Partially Printable Data (Hex & String): 8.......HgLh..6.......2..
Hex: 38 1e 00 00 12 00 00 ad 48 67 4c 68 d8 7f 36 05 f7 0a f5 f0 8a ef 32 ec e3
Request sent to: 182.138.227.44:528
```
- Common points :
```text
darryl req 1, 7 first bytes : 37 16 00 00 19 00 00
buzz req 1, 7 first bytes   : 37 16 00 00 19 00 00

darryl req 2, 7 first bytes : 37 26 00 00 19 00 00
buzz req 2, 7 first bytes   : 37 26 00 00 1a 00 00

here in the req 2, the fifth byte looks like an ID that changes when switching characters, or a parameter
if you force 37 26 00 00 1a 00 00 --> 37 26 00 00 19 00 00 for example :
```
![alt text](https://raw.githubusercontent.com/slayy2357/bs-intelligence/refs/heads/main/pictures/5.png)
### Decrypting traffic
- To decrypt requests, we first need to understand how the game encrypts them by analyzing the functions that call POST requests :
``` text
Partially Printable Data (Hex & String): .\.....V.0.0........B8..
Hex: 98 5c 00 00 11 00 00 56 fe 30 ca 30 ac 10 92 fd d0 11 dc c9 42 38 1c 7f
Request sent to: 61.95.33.52:528
Call stack:
0x101d336fc !0x1c1f6fc (0x101c1f6fc) //0x101c1f6fc call the POST request
0x101d3424c !0x1c2024c (0x101c2024c) //0x101c2024c call 0x101c1f6fc
0x101d27460 !0x1c13460 (0x101c13460) //0x101c13460 call 0x101c2024c
0x101d2722c !0x1c1322c (0x101c1322c) //0x101c1322c call 0x101c13460
0x101d31d04 !0x1c1dd04 (0x101c1dd04) //0x101c1dd04 call 0x101c1322c
0x20f9066cc libsystem_pthread.dylib!_pthread_start //etc
0x20f905ba4 libsystem_pthread.dylib!thread_start
```