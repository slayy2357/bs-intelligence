## Trying to create an external AI that play brawl stars using internal functions of the game, jailbreak required
### Part 1 : make the AI to orient itself
#### Read the number of players left
- Able to read the number of players left (usually for showdown)
![alt text](https://raw.githubusercontent.com/slayy2357/bs-intelligence/refs/heads/main/pictures/1.png)
#### Get enemy coordinates in game (later)
### Part 2 : traffic
#### Dynamic analyse : POST requests
- Able to intercept every requests of the game, but I need to understand the encryption process
![alt text](https://raw.githubusercontent.com/slayy2357/bs-intelligence/refs/heads/main/pictures/2.png)
- Exemple request when you join the training room : darryl
```c
Partially Printable Data (Hex & String): 7.......v({.??.tPq...zy.....l.70
Hex: 37 16 00 00 19 00 00 a4 76 28 7b f7 3f 3f c5 74 50 71 9b a9 00 7a 79 83 8f a7 84 ee 6c c3 37 30
Request sent to: 182.138.227.44:528
Partially Printable Data (Hex & String): 7&......t...`....Q\.?.0..r.y..BL
Hex: 37 26 00 00 19 00 00 11 74 ea a1 ab 60 97 10 e1 9c 51 5c f4 3f e5 30 dc ba 72 13 79 17 c2 42 4c
Request sent to: 182.138.227.44:528
Partially Printable Data (Hex & String): .~.....B...S..........F.b....C....w......U.i...i.......q..9.L4.w............. .H......Z.fu.....U3M.(..g..s.2.....oRM.ZE..IzbU........1.yX.....E~}-....*......sv.p..
Hex: 27 7e 00 00 9c 00 00 42 c2 cf 96 53 80 1d 11 88 87 98 03 12 17 c9 46 10 62 b6 22 06 c3 43 2e 8f dc c1 77 87 be a6 ae 15 8f 55 7f 69 b1 8a e0 69 0c b9 d3 a4 d2 18 dc 71 fc e4 39 bd 4c 34 cc 77 ce d6 95 df d3 ae c3 da 1b 98 f2 8b 98 20 cc 48 1b d6 c1 cf fa 1f 5a 1d 66 75 df 16 12 1d e8 55 33 4d 9b 28 c6 e7 67 0a 84 73 a3 32 da 0e aa cb a4 6f 52 4d 7f 5a 45 f0 e7 49 7a 62 55 c6 e9 fb 06 97 e9 dd dc 31 e4 79 58 cd 2e 1a bd 9a 45 7e 7d 2d 08 87 a2 18 2a b3 0e a9 8e d3 b3 73 76 1e 70 b2 12
Request sent to: 182.138.227.44:528
Partially Printable Data (Hex & String): 8..........H.........S...
Hex: 38 1e 00 00 12 00 00 0f af bc ed 48 d4 e2 f8 b8 b9 d4 eb fe be 53 eb bf a2
Request sent to: 182.138.227.44:528

Partially Printable Data (Hex & String): 7......,?..r._.......c......)...
Hex: 37 16 00 00 19 00 00 2c 3f dd da 72 b3 5f a9 d2 a0 19 14 ad 91 63 a5 da 8d d1 81 93 29 90 d1 0b
Request sent to: 182.138.227.44:528
Partially Printable Data (Hex & String): 7&.............^5@...G...N.-.=..
Hex: 37 26 00 00 19 00 00 d5 9e f0 9b ef 9c 00 95 5e 35 40 18 fa 0a 47 22 92 ba 4e 91 2d a7 3d fc 18
Request sent to: 182.138.227.44:528
Partially Printable Data (Hex & String): .~..........._.H.XQ.r.j@..ShfQ...fn.......{|CXG.-...&d...,p..Hf.....GE.L..+.Q....L...|.O...gY<n_...m!U.y..zW.h...yU..!Xz3}..l....#.-.n.9)@CI....ZC..HU..h..r.uL..Mk
Hex: 27 7e 00 00 9c 00 00 9e 83 0e 88 d8 dc 5f 99 48 c9 58 51 cd 72 b4 6a 40 b0 bc 53 68 66 51 a0 92 db 66 6e c2 a5 e1 ce 97 b4 92 7b 7c 43 58 47 ef 2d 05 22 1c 26 64 91 8d 00 2c 70 e1 e7 48 66 e5 9d db 0e ef 47 45 1f 4c a6 d3 2b a0 51 f4 19 cb e5 4c 80 13 c4 7c 97 4f a2 86 ee 67 59 3c 6e 5f d0 a5 b0 6d 21 55 1f 79 92 c2 7a 57 83 68 f3 e9 fe 79 55 0e ac 21 58 7a 33 7d ee 00 6c dd c2 bd 8a 23 d5 2d bd 6e 17 39 29 40 43 49 8d f1 fd e3 5a 43 b3 99 48 55 90 92 68 f8 a4 72 c0 75 4c ff 8f 4d 6b
Request sent to: 182.138.227.44:528
Partially Printable Data (Hex & String): 8......j..r....*..,.=.H._
Hex: 38 1e 00 00 12 00 00 6a da ff 72 fc 01 11 aa 2a 81 e7 2c ed 3d f1 48 ac 5f
Request sent to: 182.138.227.44:528
```