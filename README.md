## Trying to create an AI that play brawl stars as a dynamic library for iOS (jailbroken devices only)
### Advancement :
- 18/07/24 : Bot detection (still in dev) but globally work when player is static
![alt text](https://raw.githubusercontent.com/slayy2357/bs-recognition-dylib/main/pictures/1.png)
- 18/07/24 : Improved accuracy
![alt text](https://raw.githubusercontent.com/slayy2357/bs-recognition-dylib/main/pictures/2.png)
- 18/07/24 : Added all frames detect to detect when player isn't static (still in dev)
![alt text](https://raw.githubusercontent.com/slayy2357/bs-recognition-dylib/main/pictures/3.png)
- 18/07/24 : Improving accuracy
![alt text](https://raw.githubusercontent.com/slayy2357/bs-recognition-dylib/main/pictures/4.png)
- 18/07/24 : Added "fakeenv" to the game to improve accuracy --> 100% soon
![alt text](https://raw.githubusercontent.com/slayy2357/bs-recognition-dylib/main/pictures/5.png)
- 18/07/24 : More accuracy
![alt text](https://raw.githubusercontent.com/slayy2357/bs-recognition-dylib/main/pictures/6.png)
- 18/07/24 : 100% accuracy for bots 1,2,3,4 : done
![alt text](https://raw.githubusercontent.com/slayy2357/bs-recognition-dylib/main/pictures/7.png)
- 18/07/24 : Added a way to orient yourself without blocks or textures and to calculate your position on a map in brawl stars format
![alt text](https://raw.githubusercontent.com/slayy2357/bs-recognition-dylib/main/pictures/8.png)
![alt text](https://raw.githubusercontent.com/slayy2357/bs-recognition-dylib/main/pictures/9.png)
- 19/07/24 : Develop a way for the AI ​​to create a geographic scale for understanding Brawl Stars data (1 ≃ 20.88 px) 1 is the Brawl Stars data and 20.88 px is the scale for the program to understand the data
![alt text](https://raw.githubusercontent.com/slayy2357/bs-recognition-dylib/main/pictures/10.png)
![alt text](https://raw.githubusercontent.com/slayy2357/bs-recognition-dylib/main/pictures/11.png)
![alt text](https://raw.githubusercontent.com/slayy2357/bs-recognition-dylib/main/pictures/12.png)
- 19/07/24 : Now the AI ​​can read certain columns from brawl stars csv files and scale them
![alt text](https://raw.githubusercontent.com/slayy2357/bs-recognition-dylib/main/pictures/13.png)
- 20/07/24 : I am still working on the most precise way to orient myself only with Brawl Stars data, you have to be as precise as possible to understand the distance between 2 points (1 point = ?) (still in dev)
![alt text](https://raw.githubusercontent.com/slayy2357/bs-recognition-dylib/main/pictures/14.png)
- 20/07/24 : I found a way to be as precise as possible: modify the map to add a second spawner which has one point of difference with the first spawner. If we measure their distance we will therefore find the scale
![alt text](https://raw.githubusercontent.com/slayy2357/bs-recognition-dylib/main/pictures/15.png)
- 20/07/24 : So ingame result :
![alt text](https://raw.githubusercontent.com/slayy2357/bs-recognition-dylib/main/pictures/16.png)
- 20/07/24 : Then connect the centers and print the length of each vector
![alt text](https://raw.githubusercontent.com/slayy2357/bs-recognition-dylib/main/pictures/17.png)
- 20/07/24 : 3 points (in brawl stars data) = `89px`, 89/3 ≃ 29.66 : 1 point (in brawl stars data) = 29.66px
![alt text](https://raw.githubusercontent.com/slayy2357/bs-recognition-dylib/main/pictures/18.png)