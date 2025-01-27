# 2025-01-13

npm init -y

npm i expressjs

npm i fs 
fájlok beolvasása, kiírása, fájlok kezelése

npm i multer
fájlmentést fogja megvalósítani

npm i path
útvonalak létrehoása, kezelése

npm i cors
elérést segíti

# 2025-01-27

Models mappa, majd abba egy class

Adatmodelt hozunk létre, ilyen formában:
public string Name { get; set; }

controllersbe new scafolded item --> api controller with actions, using entity framework
- Ezen belül a mi általunk létrehozott user contextet használjuk majd.
- Adatbázis connectet generáltatunk
- SQL szervert választom
- Contorller nevét beleteszi alapból, pl: UsersController --> a végpontunk ebben az esetben Users lesz.

Nuget package manager console megnyitása
Add-Migration név (első általában InitialMigration)
Update-Database

Két adattábla összekapcsolása:
egyik adatmodelben létrehozok egy másik ID-t, pl: 

public int UserProfileID { get; set; }
public UserProfile? userProfile { get; set; }
a ? azt jelenti, hogy lehet 0 ez az objektum, tehát User létrehozásakor nem kötelező ezt kitölteni