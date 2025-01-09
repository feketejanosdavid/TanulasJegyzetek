# 2024.12.12

# Single  Responsibility Principle
- Egy felelősség elve
- Egy osztály csak egyetlen dologért legyen felelős
- Egy oka legyen a létezésének

```bash
npx create-expo-app@latest hello2 --template
```
Ok to proceed? (y) - y-t kell beírni
Utánna megkérdezi, hogy mivel csináljuk? - Ott a sima **blank-et** kell használni



```bash
npm i --global sinto
```
fake API-t tölt le, amivel lehet utánna dolgozni.



```bash
cd projektnév
npx expo install react-dom react-native-web @expo/metro-runtime
```
**Csomagok letelepítése**



```bash
npx expo start
```
Amint elindult egy **w** billentyűt lenyomunk, így megtudjuk nyitni a böngészőben.



# 2024.01.09

```javascript
import '@expo/metro-runtime';
```
Ezzel autómatikusan frissül az oldal fejlesztés közben.

```bash
npx expo start --host tunnel
```
Expo go appal telefonon is lehet nézni. QR kódot be kell olvasni, és akkor megjelenik.

## Fake rest api készítése:

```bash
npm create sip@latest
```
Express API-t, vagy a MOCKAPI-t válasszuk a végén