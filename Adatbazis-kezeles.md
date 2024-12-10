# 2024.12.10

## Kapcsolat létrehozása:


```bash
docker pull mcr.microsoft.com/mssql/server
```
Ez letölti a Microsoft SQL Server Docker image-t a mcr.microsoft.com/mssql/server tárolóból, ami lehetővé teszi a SQL Server konténer futtatását.



```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=Titok2024" -p 1433:1433 -d mcr.microsoft.com/mssql/server
```
docker run: Egy új Docker konténert indít.
- -e "ACCEPT_EULA=Y": Beállít egy környezeti változót, amellyel elfogadod a Microsoft End User License Agreement-t (EULA).
- -e "MSSQL_SA_PASSWORD=Titok2024": Beállítja a sa (System Administrator) felhasználó jelszavát a SQL Server-ben.
- -p 1433:1433: A konténer 1433-as portját a géped 1433-as portjához rendeli, így elérheted az SQL Server-t kívülről is.
- -d: A konténert háttérben (detached mode) futtatja.
- mcr.microsoft.com/mssql/server: Ez az SQL Server Docker image, amit futtatni szeretnél.



```bash
sqlcmd -S 172.26.64.1 -U sa -P Titok2024
```
sqlcmd: Az SQL Server parancssori eszköze, amely lehetővé teszi SQL lekérdezések futtatását parancssorból.
- -S 172.26.64.1: A -S paraméterrel megadod az SQL Server IP címét, amit elérni szeretnél (a példában ez 172.26.64.1).
- -U sa: A -U paraméterrel adod meg a bejelentkezési felhasználót (sa, azaz system administrator).
- -P Titok2024: A -P paraméterrel adod meg a jelszót (Titok2024).

## Adatbázis kezelése:

```bash
1> CREATE DATABASE name
2> GO
```
Az SQL CREATE DATABASE parancsot használjuk új adatbázis létrehozására. A name helyére az adatbázis nevét kell írni.



```bash
1> USE databasename
2> GO
```
Az SQL USE parancs segítségével váltasz az aktuálisan használt adatbázisra. A databasename helyére az adatbázis nevét kell beírni, amelyet használni szeretnél.



```bash
1> CREATE TABLE teteltipusok(
2>     az INT PRIMARY KEY,
3>     megnevezes VARCHAR(30)
4> );
5> GO
```
- Az SQL CREATE TABLE parancsot használjuk új táblák létrehozására az adatbázisban.
- teteltipusok: Az új tábla neve.
- az INT PRIMARY KEY: Az az oszlop egy INT típusú egész szám, amely a tábla elsődleges kulcsa lesz.
- megnevezes VARCHAR(30): A megnevezes oszlop egy VARCHAR típusú, 30 karakter hosszú szöveges adatot tárol.



```bash
1> CREATE TABLE tipusjellemzok(
2>     az INT PRIMARY KEY,
3>     megnevezes VARCHAR(30)
4> );
5> GO
```
Ez az SQL parancs ugyanúgy működik, mint az előző, csak más néven és oszlopokkal hoz létre egy új táblát.



```bash
1> INSERT INTO tipusjellemzok 
2> VALUES 
3> (1, 'gyártó'),
4> (2, 'processzor'),
5> (3, 'ram'),
6> (4, 'háttértár'),
7> (5, 'háttértár 2'),
8> (6, 'monitor'),
9> (7, 'monitor2'),
10> (8, 'projektor'),
11> (9, 'billentyűzet'),
12> (10, 'egér'),
13> (11, 'tápegység'),
14> (12, 'ajtók száma'),
15> (13, 'polcok száma'),
16> (14, 'szélesség'),
17> (15, 'magasság');
18> GO
```
- Az SQL INSERT INTO parancsot arra használjuk, hogy új adatokat adjunk hozzá egy táblához.
- tipusjellemzok: A tábla neve, ahová az adatokat be szeretnénk illeszteni.
- VALUES: A beszúrandó adatokat adja meg. Minden sor egy-egy adatbejegyzést jelent, amely az oszlopoknak megfelelően kerül elhelyezésre.



```bash
1> INSERT INTO teteltipusok  
2> VALUES
3> (1, 'Asztali tanulói számítógép'),
4> (2, 'Asztali tanári számítógép'),
5> (3, 'Notebook tanulói számítógép'),
6> (4, 'Lemezszekrény'),
7> (5, 'számítógép asztal');
8> GO
```
Ugyanúgy működik, mint az előző INSERT INTO, csak más adatokkal és más táblába történik a beszúrás.



```bash
1> CREATE TABLE tipusjellemzokapcsolatok(
2>     tipusID INT,
3>     jellemzoID INT,
4>     PRIMARY KEY (tipusID, jellemzoID),
5>     FOREIGN KEY (tipusID) REFERENCES teteltipusok (az),
6>     FOREIGN KEY (jellemzoID) REFERENCES tipusjellemzok (az)
7> );
8> GO
```
- CREATE TABLE: Új tábla létrehozása.
- tipusID INT: Egy egész szám típusú oszlop.
- jellemzoID INT: Egy másik egész szám típusú oszlop.
- PRIMARY KEY (tipusID, jellemzoID): Az oszlopok kombinációja lesz az elsődleges kulcs.
- FOREIGN KEY (tipusID) REFERENCES teteltipusok (az): A tipusID oszlop egy idegen kulcs, amely hivatkozik a - - teteltipusok tábla az oszlopára.
- FOREIGN KEY (jellemzoID) REFERENCES tipusjellemzok (az): A jellemzoID oszlop egy idegen kulcs, amely hivatkozik a - tipusjellemzok tábla az oszlopára.
