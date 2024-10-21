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
0x101d336fc !0x1c1f6fc (0x101c1f6fc) //0x101c1f6fc last call before POST request
0x101d3424c !0x1c2024c (0x101c2024c) //0x101c2024c call 0x101c1f6fc
0x101d27460 !0x1c13460 (0x101c13460) //0x101c13460 call 0x101c2024c
0x101d2722c !0x1c1322c (0x101c1322c) //0x101c1322c call 0x101c13460
0x101d31d04 !0x1c1dd04 (0x101c1dd04) //0x101c1dd04 call 0x101c1322c
0x20f9066cc libsystem_pthread.dylib!_pthread_start //etc
0x20f905ba4 libsystem_pthread.dylib!thread_start
//payload is probably already crypted in 0x101c1f6fc so need to analyse other functions
```
- 101c13460 analyse :
``` text
//101c13460 is a call to next function, dumping args, we now that arg2 is the pointer to payload, but the data look crypted :
Argument 0 : 0x25
Argument 1 : 0x12
Argument 2 (Pointer) : 0x107b328f0
Argument 3 (Size) : 0x1dd
Argument 4 : 0x0
Data in arg2:
00000000  35 56 00 01 d6 00 00 a2 a4 32 13 5d a3 31 35 47  5V.......2.].15G
00000010  13 57 bc 31 67 de a2 3f b6 1e 05 92 25 c3 36 1a  .W.1g..?....%.6.
00000020  eb b8 7d fd 41 49 b9 4f ff 06 6d 40 b8 4b 1f 63  ..}.AI.O..m@.K.c
00000030  ae da f7 92 84 35 b3 c6 22 be 90 08 9e 9b a2 80  .....5..".......
00000040  b3 6b f4 fe 01 19 c5 72 92 ec dc fb 33 f9 6e 45  .k.....r....3.nE
00000050  16 18 0e fe c6 c5 91 d6 de f1 f2 4f 96 0b 11 ed  ...........O....
00000060  db a6 47 44 7f a9 81 ee d3 c2 bc a4 28 1c ca 21  ..GD........(..!
00000070  64 aa 40 b0 ad 03 97 8d 0d 01 ef 72 78 d8 59 b5  d.@........rx.Y.
00000080  77 72 91 c8 f0 87 06 7e f8 bf b1 e3 f2 2b c8 df  wr.....~.....+..
00000090  a0 6e 5d 7f 33 ab 16 f3 92 c6 1c 2e b3 9e de 38  .n].3..........8
000000a0  f8 5e 6b 60 43 81 0e 8f 0e be a8 aa ba 5e 61 08  .^k`C........^a.
000000b0  1e 25 07 ef a9 07 b2 ca 7f 81 5c 3e 87 57 a1 d7  .%........\>.W..
000000c0  8b 19 ee 8e f7 06 6c 1d 92 bb 13 61 79 bb d7 1f  ......l....ay...
000000d0  29 01 8b 78 d3 75 85 9d 20 25 45 c5 6e 31 b3 c1  )..x.u.. %E.n1..
000000e0  9e 27 7c d4 33 84 cb cb c1 4d 8d 3b 06 9d 3a 44  .'|.3....M.;..:D
000000f0  57 22 27 2b 4f 24 d0 b7 a2 f6 a0 80 ec 03 df 8b  W"'+O$..........
00000100  a9 58 2a 19 15 08 96 6e 06 85 15 e0 86 f7 fa f5  .X*....n........
00000110  4a 00 98 47 89 fb 1e ae 2e c6 b8 6c c7 04 45 d0  J..G.......l..E.
00000120  ca 76 11 c9 13 69 f5 6e 9c 20 bd 30 15 2f 69 69  .v...i.n. .0./ii
00000130  b1 51 dd 73 9d 1c bc 48 96 b3 d3 14 a4 2d 01 97  .Q.s...H.....-..
00000140  93 4e 33 37 bc d8 63 54 1e 3b 8a 09 bb ff 1e f8  .N37..cT.;......
00000150  60 fe 97 0b 6a 4b a0 db c1 5b 47 ad 08 45 03 9f  `...jK...[G..E..
00000160  b5 76 14 f5 b5 69 9b 18 9d d0 69 4a ee 8d 2b d3  .v...i....iJ..+.
00000170  59 62 0a 68 f5 67 2e 87 97 90 fc 81 fb 71 f1 46  Yb.h.g.......q.F
00000180  39 fd e3 dc 83 d4 14 22 47 b7 a7 30 2d b4 8c 08  9......"G..0-...
00000190  6c 30 80 d2 ee 43 18 e0 4e 2c ad ee ca ca 0c 79  l0...C..N,.....y
000001a0  9f f4 b3 33 5a 5a 14 9e 78 53 c0 c6 63 7c 32 78  ...3ZZ..xS..c|2x
000001b0  e3 02 c6 91 80 f5 e3 52 7e ad fa 0c f2 cf af 4b  .......R~......K
000001c0  3f cd c4 23 52 24 94 f6 ed c8 6b 71 40 cb 80 e6  ?..#R$....kq@...
000001d0  b8 33 83 ed 8c 7e d3 b5 c0 d1 0d 57 96           .3...~.....W.
Offset: 0x1c1345c called by: 0x8841800001c13428
```
So we need to focus on the data pointed by arg2 modifications BEFORE 101c13460 bcause already encrypted
``` text
101c13460 call 101c1f62c using 6 args :
0 : 0x25 (always)
1 : 0x12 unknow
2 : 0x107b328f0 pointer to the payload in memory
3 : 0x1dd size of the payload in memory
4 : 0x0 unknow (parameter, always 0x0)
5 : ?
```
The best way to understand is probably here, backtracing and analysing, but later
- Analysing modules
```text
libCommonCrypto.dylib
CCSHA256 : error
CCSHA1   : error
CCMD5    : error
CCCrypt  : 1 call :
```

``` text
00000000  7b 22 61 64 76 65 72 74 69 73 65 72 49 64 45 6e  {"advertiserIdEn
00000010  61 62 6c 65 64 22 3a 66 61 6c 73 65 2c 22 70 6c  abled":false,"pl
00000020  61 74 66 6f 72 6d 5f 65 78 74 65 6e 73 69 6f 6e  atform_extension
00000030  5f 76 32 22 3a 7b 22 70 6c 61 74 66 6f 72 6d 22  _v2":{"platform"
00000040  3a 22 69 6f 73 5f 6e 61 74 69 76 65 22 2c 22 76  :"ios_native","v
00000050  65 72 73 69 6f 6e 22 3a 22 36 2e 31 33 2e 31 22  ersion":"6.13.1"
00000060  7d 2c 22 66 69 72 73 74 4c 61 75 6e 63 68 44 61  },"firstLaunchDa
00000070  74 65 22 3a 22 32 30 32 34 2d 30 39 2d 32 33 5f  te":"2024-09-23_
00000080  32 30 31 30 35 35 2d 30 37 30 30 22 2c 22 65 76  201055-0700","ev
00000090  65 6e 74 22 3a 22 4c 61 75 6e 63 68 65 64 22 2c  ent":"Launched",
000000a0  22 6c 6f 61 64 5f 66 72 61 6d 65 77 6f 72 6b 5f  "load_framework_
000000b0  72 65 73 75 6c 74 22 3a 22 44 65 6e 69 65 64 5c  result":"Denied\
000000c0  2f 52 65 73 74 72 69 63 74 65 64 22 2c 22 63 65  /Restricted","ce
000000d0  6c 6c 22 3a 7b 22 6d 63 63 22 3a 22 39 39 39 22  ll":{"mcc":"999"
000000e0  2c 22 6d 6e 63 22 3a 22 39 39 22 2c 22 72 61 22  ,"mnc":"99","ra"
000000f0  3a 22 61 66 5f 72 65 73 74 72 69 63 74 65 64 22  :"af_restricted"
00000100  7d 2c 22 74 69 6d 65 70 61 73 73 65 64 73 69 6e  },"timepassedsin
00000110  63 65 6c 61 73 74 6c 61 75 6e 63 68 22 3a 22 37  celastlaunch":"7
00000120  34 22 2c 22 72 65 66 22 3a 22 64 62 37 33 32 39  4","ref":"fnkdj9
00000130  65 65 66 34 37 35 33 65 30 32 66 32 66 36 31 61  eef4753e0ychjyhn
00000140  65 35 34 31 38 32 66 32 36 30 33 36 35 62 34 64  e5rgjnrkxgfrfxvf
00000150  61 36 32 64 63 37 63 61 62 38 36 66 63 34 31 63  a62dc7eyht6fc41c
00000160  64 65 30 31 32 62 64 33 66 38 3b 30 3b 30 3b 30  sfjkfjbgfb;0;0;0
00000170  3b 30 3b 30 22 2c 22 73 79 73 74 65 6d 76 65 72  ;0;0","systemver
00000180  73 69 6f 6e 22 3a 22 31 36 2e 32 22 2c 22 70 6c  sion":"16.2","pl
00000190  61 74 66 6f 72 6d 22 3a 22 69 50 61 64 31 33 2c  atform":"iPad13,
000001a0  31 30 22 2c 22 70 72 65 76 5f 73 65 73 73 69 6f  10","prev_sessio
000001b0  6e 5f 64 75 72 22 3a 32 31 2c 22 64 69 73 6b 22  n_dur":21,"disk"
000001c0  3a 22 39 39 39 5c 2f 39 39 39 39 22 2c 22 61 66  :"999\/9999","af
000001d0  5f 74 69 6d 65 73 74 61 6d 70 22 3a 22 31 37 32  _timestamp":"172
000001e0  39 34 39 30 33 32 30 36 30 35 22 2c 22 70 6c 61  9490320605","pla
000001f0  74 66 6f 72 6d 65 78 74 65 6e 73 69 6f 6e 22 3a  tformextension":
00000200  22 69 6f 73 5f 6e 61 74 69 76 65 22 2c 22 64 61  "ios_native","da
00000210  74 65 31 22 3a 22 32 30 32 34 2d 30 39 2d 32 33  te1":"2024-09-23
00000220  5f 32 30 31 30 30 35 2d 30 37 30 30 22 2c 22 63  _201005-0700","c
00000230  6b 73 6d 5f 76 32 22 3a 22 39 31 34 66 61 31 32  ksm_v2":"914fa12
00000240  63 32 34 37 33 36 62 37 34 35 39 31 62 30 63 34  c24736b74591b0c4
00000250  66 31 61 30 64 34 30 31 62 30 63 34 38 31 62 30  f1a0d401b0c481b0
00000260  64 34 65 31 62 22 2c 22 77 69 66 69 22 3a 66 61  d4e1b","wifi":fa
00000270  6c 73 65 2c 22 73 68 61 72 69 6e 67 5f 66 69 6c  lse,"sharing_fil
00000280  74 65 72 22 3a 5b 22 61 6c 6c 22 5d 2c 22 73 65  ter":["all"],"se
00000290  72 76 65 72 41 70 69 56 65 72 73 69 6f 6e 22 3a  rverApiVersion":
000002a0  22 36 2e 31 33 22 2c 22 61 74 74 5f 73 74 61 74  "6.13","att_stat
000002b0  75 73 22 3a 32 2c 22 63 75 72 72 65 6e 74 4c 61  us":2,"currentLa
000002c0  6e 67 75 61 67 65 22 3a 22 22 2c 22 4a 42 44 65  nguage":"","JBDe
000002d0  76 69 63 65 22 3a 66 61 6c 73 65 2c 22 64 65 76  vice":false,"dev
000002e0  69 63 65 54 72 61 63 6b 69 6e 67 44 69 73 61 62  iceTrackingDisab
000002f0  6c 65 64 22 3a 22 74 72 75 65 22 2c 22 6c 6f 63  led":"true","loc
00000300  61 6c 69 7a 65 64 6d 6f 64 65 6c 22 3a 22 69 50  alizedmodel":"iP
00000310  68 6f 6e 65 22 2c 22 65 76 65 6e 74 76 61 6c 75  hone","eventvalu
00000320  65 22 3a 22 22 2c 22 62 75 6e 64 6c 65 49 64 65  e":"","bundleIde
00000330  6e 74 69 66 69 65 72 22 3a 22 63 6f 6d 2e 73 75  ntifier":"com.su
00000340  70 65 72 63 65 6c 6c 2e 6c 61 73 65 72 22 2c 22  percell.laser","
00000350  64 65 76 69 63 65 44 61 74 61 22 3a 7b 22 63 70  deviceData":{"cp
00000360  75 5f 74 79 70 65 22 3a 22 41 52 4d 36 34 22 2c  u_type":"ARM64",
00000370  22 63 70 75 5f 73 70 65 65 64 22 3a 22 2d 31 22  "cpu_speed":"-1"
00000380  2c 22 6f 73 56 65 72 73 69 6f 6e 22 3a 22 39 39  ,"osVersion":"99
00000390  2e 39 20 28 42 75 69 6c 64 20 39 39 39 39 39 29  .9 (Build 99999)
000003a0  22 2c 22 72 61 6d 5f 73 69 7a 65 22 3a 22 39 39  ","ram_size":"99
000003b0  39 22 2c 22 63 70 75 5f 36 34 62 69 74 73 22 3a  9","cpu_64bits":
000003c0  22 74 72 75 65 22 2c 22 64 69 6d 22 3a 7b 22 79  "true","dim":{"y
000003d0  5f 70 78 22 3a 32 37 33 32 2c 22 78 5f 70 78 22  _px":2732,"x_px"
000003e0  3a 32 30 34 38 7d 2c 22 62 72 69 67 68 74 6e 65  :2048},"brightne
000003f0  73 73 22 3a 22 30 2e 31 30 30 30 30 30 22 2c 22  ss":"0.100000","
00000400  64 65 76 69 63 65 5f 6d 6f 64 65 6c 22 3a 22 69  device_model":"i
00000410  50 61 64 31 33 2c 31 30 22 2c 22 63 70 75 5f 63  Pad13,10","cpu_c
00000420  6f 75 6e 74 22 3a 22 39 22 7d 2c 22 64 61 74 65  ount":"9"},"date
00000430  32 22 3a 22 32 30 32 34 2d 31 30 2d 32 30 5f 32  2":"2024-10-20_2
00000440  32 35 38 33 35 2d 30 37 30 30 22 2c 22 63 75 72  25835-0700","cur
00000450  72 65 6e 74 43 6f 75 6e 74 72 79 63 6f 64 65 22  rentCountrycode"
00000460  3a 22 55 53 22 2c 22 61 70 70 55 49 44 22 3a 22  :"US","appUID":"
00000470  30 2d 39 32 32 34 37 36 39 22 2c 22 73 68 6f 72  0-9297521","shor
00000480  74 62 75 6e 64 6c 65 76 65 72 73 69 6f 6e 22 3a  tbundleversion":
00000490  22 35 37 2e 33 32 35 22 2c 22 73 79 73 74 65 6d  "57.325","system
000004a0  6e 61 6d 65 22 3a 22 69 50 61 64 4f 53 22 2c 22  name":"iPadOS","
000004b0  69 61 65 63 6f 75 6e 74 65 72 22 3a 22 30 22 2c  iaecounter":"0",
000004c0  22 61 66 5f 69 61 64 5f 64 61 74 61 22 3a 7b 22  "af_iad_data":{"
000004d0  65 72 72 6f 72 22 3a 22 41 44 43 6c 69 65 6e 74  error":"ADClient
000004e0  45 72 72 6f 72 54 72 61 63 6b 69 6e 67 52 65 73  ErrorTrackingRes
000004f0  74 72 69 63 74 65 64 4f 72 44 65 6e 69 65 64 22  trictedOrDenied"
00000500  7d 2c 22 61 66 5f 65 76 65 6e 74 73 5f 61 70 69  },"af_events_api
00000510  22 3a 22 31 22 2c 22 73 63 5f 6f 22 3a 22 6c 6c  ":"1","sc_o":"ll
00000520  22 2c 22 6f 70 65 6e 5f 72 65 66 65 72 72 65 72  ","open_referrer
00000530  22 3a 22 22 2c 22 64 65 76 5f 6b 65 79 22 3a 22  ":"","dev_key":"
00000540  6e 73 55 77 68 6a 76 59 77 52 36 38 43 6b 66 50  jfjBkkvBNCOldmMp
00000550  53 66 44 52 74 41 22 2c 22 75 69 64 22 3a 22 31  sgjBFj","uid":"1
00000560  37 32 37 31 34 37 34 30 35 30 38 33 2d 35 32 37  727147405083-527
00000570  30 39 34 38 22 2c 22 76 65 6e 64 6f 72 49 64 22  0948","vendorId"
00000580  3a 22 44 35 42 43 32 45 37 30 2d 42 46 44 39 2d  :"XXXX","counter
000005b0  22 3a 22 38 35 39 22 2c 22 69 76 63 22 3a 66 61  ":"859","ivc":fa
000005c0  6c 73 65 2c 22 64 61 74 65 31 5f 32 22 3a 22 32  lse,"date1_2":"2
000005d0  30 32 34 2d 30 39 2d 32 33 5f 32 30 31 30 30 35  024-09-23_201005
000005e0  2d 30 37 30 30 22 2c 22 72 65 69 6e 73 74 61 6c  -0700","reinstal
000005f0  6c 43 6f 75 6e 74 65 72 22 3a 22 32 22 2c 22 74  lCounter":"2","t
00000600  69 6d 65 73 74 61 6d 70 22 3a 22 31 37 32 39 34  imestamp":"17294
00000610  39 30 33 32 30 2e 36 30 35 33 39 36 22 2c 22 73  90320.605396","s
00000620  65 73 73 69 6f 6e 63 6f 75 6e 74 65 72 22 3a 22  essioncounter":"
00000630  31 31 31 38 22 2c 22 62 61 63 6b 75 70 49 6e 66  1118","backupInf
00000640  6f 22 3a 7b 22 63 6e 74 22 3a 31 2c 22 74 73 22  o":{"cnt":1,"ts"
00000650  3a 31 37 32 38 30 39 35 30 30 38 7d 2c 22 64 61  :1728095008},"da
00000660  74 65 33 22 3a 22 32 30 32 34 2d 30 39 2d 32 33  te3":"2024-09-23
00000670  5f 32 30 31 30 35 34 2d 30 37 30 30 22 2c 22 6f  _201054-0700","o
00000680  72 69 67 69 6e 61 6c 41 70 70 73 66 6c 79 65 72  riginalAppsflyer
00000690  49 64 22 3a 22 31 37 32 37 31 34 37 34 30 35 30  Id":"17271474050
000006a0  38 33 2d 35 32 37 30 39 34 38 22 2c 22 6d 6f 64  83-5270948","mod
000006b0  65 6c 22 3a 22 69 50 61 64 22 2c 22 62 75 6e 64  el":"iPad","bund
000006c0  6c 65 6e 61 6d 65 22 3a 22 42 72 61 77 6c 20 53  lename":"Brawl S
000006d0  74 61 72 73 22 2c 22 61 64 76 65 72 74 69 73 65  tars","advertise
000006e0  72 49 64 22 3a 22 22 2c 22 65 76 65 6e 74 4e 61  rId":"","eventNa
000006f0  6d 65 22 3a 22 4c 61 75 6e 63 68 65 64 22 2c 22  me":"Launched","
00000700  62 75 6e 64 6c 65 76 65 72 73 69 6f 6e 22 3a 22  bundleversion":"
00000710  35 37 2e 33 32 35 22 2c 22 6d 65 74 61 22 3a 7b  57.325","meta":{
00000720  22 68 6f 73 74 22 3a 7b 22 6e 61 6d 65 22 3a 22  "host":{"name":"
00000730  61 70 70 73 66 6c 79 65 72 73 64 6b 2e 63 6f 6d  appsflyersdk.com
00000740  22 2c 22 70 72 65 66 69 78 22 3a 22 62 68 37 79  ","prefix":"bh7y
00000750  76 67 2d 22 7d 2c 22 73 6b 61 64 22 3a 7b 22 61  vg-"},"skad":{"a
00000760  70 69 5f 73 74 61 74 75 73 22 3a 7b 22 65 72 72  pi_status":{"err
00000770  6f 72 22 3a 22 45 72 72 6f 72 20 44 6f 6d 61 69  or":"Error Domai
00000780  6e 3d 63 6f 6d 2e 61 70 70 73 66 6c 79 65 72 2e  n=com.appsflyer.
00000790  73 64 6b 2e 73 65 72 69 61 6c 69 7a 65 20 43 6f  sdk.serialize Co
000007a0  64 65 3d 36 31 20 5c 22 6e 6f 20 72 75 6c 65 73  de=61 \"no rules
000007b0  20 66 6f 75 6e 64 5c 22 20 55 73 65 72 49 6e 66   found\" UserInf
000007c0  6f 3d 7b 4e 53 4c 6f 63 61 6c 69 7a 65 64 44 65  o={NSLocalizedDe
000007d0  73 63 72 69 70 74 69 6f 6e 3d 6e 6f 20 72 75 6c  scription=no rul
000007e0  65 73 20 66 6f 75 6e 64 7d 22 2c 22 73 74 61 74  es found}","stat
000007f0  75 73 43 6f 64 65 22 3a 34 30 34 2c 22 72 75 6c  usCode":404,"rul
00000800  65 22 3a 22 6e 6f 20 72 75 6c 65 73 20 66 6f 75  e":"no rules fou
00000810  6e 64 22 7d 7d 7d 7d                             nd"}}}}

//request sended after loading 100%, not what we are looking for but OK
//now we now that the game don't use CCCrypt for other requests..
```
``` text
libboringssl.dylib
SSL_write          : 20+ call //interessant
SSL_read           : 20+ call, example when you look other profiles :

00000000  00 01 28 01 04 00 00 00 01 88 5f 8b 1d 75 d0 62  ..(......._..u.b
00000010  0d 26 3d 4c 74 41 ea 5c 03 32 33 38 00 83 90 69  .&=LtA.\.238...i
00000020  2f 96 dd 6d 5f 4a 08 0a 6a 22 54 10 04 d2 82 0d  /..m_J..j"T.....
00000030  c6 5d b8 07 14 c5 a3 7f 00 93 f2 b2 2d ac b6 10  .]..........-...
00000040  b4 50 b1 0f 65 85 a0 69 31 ea 58 d2 7f 98 03 92  .P..e..i1.X.....
00000050  b4 fc 8c c7 1b 22 1b 4f 09 e7 c4 e8 9b 6d a6 d9  .....".O.....m..
00000060  71 b9 5d 7a 51 ff 00 89 20 c9 39 56 21 ea 4d 87  q.]zQ... .9V!.M.
00000070  a3 a7 a4 7e 56 1c c5 80 1f 4a 54 75 88 32 4e 5f  ...~V....JTu.2N_
00000080  a5 29 b5 09 5a c2 f7 1d 06 90 69 2f d2 95 d8 7f  .)..Z.....i/....
00000090  3e 96 b0 bd c7 41 a4 1a 4b 00 85 f2 b1 06 49 cb  >....A..K.....I.
000000a0  8f d0 64 21 49 6c 3d 2a 12 83 db 24 b6 1e a4 ff  ..d!Il=*...$....
000000b0  00 03 76 69 61 af 0a e1 51 a2 32 d0 42 59 4a 27  ..via...Q.2.BYJ'
000000c0  5f 8e 57 5e 75 b6 48 02 32 d0 dd 8c b2 b8 eb 4b  _.W^u.H.2......K
000000d0  92 83 db 24 b6 1e a4 af 51 52 a7 f5 7a 83 db 26  ...$....QR..z..&
000000e0  1b 0f 52 7f bf 00 89 f2 b0 e9 f6 b1 25 5a b3 d7  ..R.........%Z..
000000f0  87 bd 7f 13 6d ad ad 9f 00 89 f2 b0 e9 f6 b1 25  ....m..........%
00000100  58 d2 7f ad b6 1e b6 bb da 1d 1a b8 19 f6 b4 3d  X..............=
00000110  8b 21 ab da 6c ba 0b fb 9a f4 3d e6 d1 91 f6 66  .!..l.....=....f
00000120  ed bc bc 28 e4 92 60 f7 4a db 0f fb d9 39 26 82  ...(..`.J....9&.
00000130  0f 00 00 ee 00 00 00 00 00 01 7b 22 6f 6b 22 3a  ..........{"ok":
00000140  74 72 75 65 2c 22 64 61 74 61 22 3a 7b 22 70 72  true,"data":{"pr
00000150  6f 66 69 6c 65 73 22 3a 5b 7b 22 73 63 69 64 22  ofiles":[{"scid"
00000160  3a 22 33 31 2d 66 66 34 30 33 65 64 64 2d 36 62  :"31-ff403edd-6b
00000170  37 37 2d 34 61 61 61 2d 62 30 38 35 2d 30 64 35  77-4aaa-b085-0d5
00000180  62 36 35 38 31 37 65 38 63 22 2c 22 61 70 70 6c  b65817e8c","appl
00000190  69 63 61 74 69 6f 6e 41 63 63 6f 75 6e 74 49 64  icationAccountId
000001a0  22 3a 22 30 2d 35 31 30 39 33 35 36 39 22 2c 22  ":"0-51093569","
000001b0  6e 61 6d 65 22 3a 22 62 6f 75 62 61 63 61 72 22  name":"boubacar"
000001c0  2c 22 68 61 6e 64 6c 65 22 3a 22 53 74 75 6e 6e  ,"handle":"Stunn
000001d0  69 6e 67 46 61 6e 63 79 50 72 6f 22 2c 22 61 76  ingFancyPro","av
000001e0  61 74 61 72 49 6d 61 67 65 22 3a 22 30 2c 68 6f  atarImage":"0,ho
000001f0  67 5f 72 69 64 65 72 2c 23 45 30 36 32 46 42 2c  g_rider,#E062FB,
00000200  23 46 37 43 34 46 46 22 2c 22 70 6c 61 79 65 72  #F7C4FF","player
00000210  4e 61 6d 65 22 3a 22 53 4b 7c 73 6c 75 59 7a 20  Name":"SK|sluYz 
00000220  70 72 6f 22 7d 5d 7d 7d                          pro"}]}}
```
So, we can read some payloads before encryption through SSL_write, SSL_read, and CCCrypt, but those aren't the main payloads. What we want to intercept is the payload sent through the send function before encryption, as that's how the game communicates with the server—for example, when joining a game, using emotes, etc