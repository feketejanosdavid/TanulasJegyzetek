# 2024.12.10

## Kapcsolat létrehozása:


```bash
docker pull mcr.microsoft.com/mssql/server
```
Ez letölti a Microsoft SQL Server Docker image-t a mcr.microsoft.com/mssql/server tárolóból, ami lehetővé teszi a SQL Server konténer futtatását.



```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=Titok2024" -p 1433:1433 -d mcr.microsoft.com/mssql/server
```
**docker run**: Egy új Docker konténert indít.
- -e "ACCEPT_EULA=Y": Beállít egy környezeti változót, amellyel elfogadod a Microsoft End User License Agreement-t (EULA).
- -e "MSSQL_SA_PASSWORD=Titok2024": Beállítja a sa (System Administrator) felhasználó jelszavát a SQL Server-ben.
- -p 1433:1433: A konténer 1433-as portját a géped 1433-as portjához rendeli, így elérheted az SQL Server-t kívülről is.
- -d: A konténert háttérben (detached mode) futtatja.
- mcr.microsoft.com/mssql/server: Ez az SQL Server Docker image, amit futtatni szeretnél.



```bash
sqlcmd -S 172.26.64.1 -U sa -P Titok2024
```
**sqlcmd**: Az SQL Server parancssori eszköze, amely lehetővé teszi SQL lekérdezések futtatását parancssorból.
- **-S** 172.26.64.1: A -S paraméterrel megadod az SQL Server IP címét, amit elérni szeretnél (a példában ez 172.26.64.1).
- **-U** sa: A -U paraméterrel adod meg a bejelentkezési felhasználót (sa, azaz system administrator).
- **-P** Titok2024: A -P paraméterrel adod meg a jelszót (Titok2024).

## Adatbázis kezelése:

```bash
1> CREATE DATABASE name
2> GO
```
**Az SQL CREATE DATABASE** parancsot használjuk új adatbázis létrehozására. A name helyére az adatbázis nevét kell írni.



```bash
1> USE databasename
2> GO
```
**Az SQL USE** parancs segítségével váltasz az aktuálisan használt adatbázisra. A databasename helyére az adatbázis nevét kell beírni, amelyet használni szeretnél.



```bash
1> CREATE TABLE teteltipusok(
2>     az INT PRIMARY KEY,
3>     megnevezes VARCHAR(30)
4> );
5> GO
```
- **Az SQL CREATE TABLE** parancsot használjuk új táblák létrehozására az adatbázisban.
- **teteltipusok:** Az új tábla neve.
- **az INT PRIMARY KEY:** Az az oszlop egy INT típusú egész szám, amely a tábla elsődleges kulcsa lesz.
- **megnevezes VARCHAR(30):** A megnevezes oszlop egy VARCHAR típusú, 30 karakter hosszú szöveges adatot tárol.



```bash
1> CREATE TABLE tipusjellemzok(
2>     az INT PRIMARY KEY,
3>     megnevezes VARCHAR(30)
4> );
5> GO
```
Ez az SQL parancs *ugyanúgy működik, mint az előző*, csak más néven és oszlopokkal hoz létre egy új táblát.



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
- **Az SQL INSERT INTO** parancsot arra használjuk, hogy új adatokat adjunk hozzá egy táblához.
- **tipusjellemzok:** A tábla neve, ahová az adatokat be szeretnénk illeszteni.
- **VALUES:** A beszúrandó adatokat adja meg. Minden sor egy-egy adatbejegyzést jelent, amely az oszlopoknak megfelelően kerül elhelyezésre.



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
*Ugyanúgy működik, mint az előző INSERT INTO*, csak más adatokkal és más táblába történik a beszúrás.



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
- **CREATE TABLE:** Új tábla létrehozása.
- **tipusID INT:** Egy egész szám típusú oszlop.
- **jellemzoID INT:** Egy másik egész szám típusú oszlop.
- **PRIMARY KEY (tipusID, jellemzoID):** Az oszlopok kombinációja lesz az elsődleges kulcs.
- **FOREIGN KEY (tipusID) REFERENCES teteltipusok (az):** A tipusID oszlop egy idegen kulcs, amely hivatkozik a - - teteltipusok tábla az oszlopára.
- **FOREIGN KEY (jellemzoID) REFERENCES tipusjellemzok (az):** A jellemzoID oszlop egy idegen kulcs, amely hivatkozik a - tipusjellemzok tábla az oszlopára.



```bash
1> INSERT INTO tipusjellemzokapcsolatok VALUES(1,1),(1,2),(1,3),(1,4),(1,5),(1,6),(1,9),(1,10),(2,1),(2,2),(2,3),(2,4),(2,5),(2,6),(2,7),(2,8),(2,9),(2,10),(3,1),(3,2),(3,3),(3,4),(3,10),(3,11);
2> GO
```
**Ez az SQL INSERT INTO** parancs adatokat illeszt be a tipusjellemzokapcsolatok nevű táblába. A tábla két oszlopot tartalmaz: tipusID és jellemzoID. A parancsot az SQL Serverben futtatják, és az értékeket a táblába való beillesztéshez használják.



```bash
1> SELECT teteltipusok.megnevezes,tipusjellemzok.megnevezes FROM (teteltipusok INNER JOIN tipusjellemzokapcsolatok ON teteltipusok.az=tipusID) INNER JOIN tipusjellemzok ON tipusjellemzok.az=jellemzoID;
2> GO
```
**A Lekérdezés az alábbi eredményt fogja adni:**
```bash
megnevezes                     megnevezes
------------------------------ ------------------------------
Asztali tanulói számítógép     gyártó
Asztali tanulói számítógép     procceszor
Asztali tanulói számítógép     ram
Asztali tanulói számítógép     háttértár
Asztali tanulói számítógép     háttértár 2
Asztali tanulói számítógép     monitor
Asztali tanulói számítógép     billentyuzet
Asztali tanulói számítógép     egér
Asztali tanári számítógép      gyártó
Asztali tanári számítógép      procceszor
Asztali tanári számítógép      ram
Asztali tanári számítógép      háttértár
Asztali tanári számítógép      háttértár 2
Asztali tanári számítógép      monitor
Asztali tanári számítógép      monitor2
Asztali tanári számítógép      projektor
Asztali tanári számítógép      billentyuzet
Asztali tanári számítógép      egér
Notebook tanulói számítógép    gyártó
Notebook tanulói számítógép    procceszor
Notebook tanulói számítógép    ram
Notebook tanulói számítógép    háttértár
Notebook tanulói számítógép    egér
Notebook tanulói számítógép    tápegység
```