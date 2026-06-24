# 🎨 React Real-Time Collaborative Whiteboard

Egy valós idejű, több felhasználós kollaboratív rajztábla és vizuális tervező alkalmazás. A projekt célja egy gyors, rendkívül reszponzív és felhasználóbarát felület biztosítása közös ötleteléshez, távoktatáshoz vagy vizuális tervezéshez, ahol a résztvevők azonnal látják egymás kurzorát és módosításait.

*(Jelenleg a forráskód zárt, ez a leírás a projekt technikai képességeit, a rendszerarchitektúrát és a felhasznált modern webes technológiákat hivatott bemutatni.)*

---

## 📸 Képernyőképek az alkalmazásról


> **1.**
> 
> *<img width="508" height="857" alt="kép" src="https://github.com/user-attachments/assets/4fae5a81-2373-4fc7-a5b1-35e00ff4ba58" />*
> 
> **2.**
> *<img width="1878" height="951" alt="kép" src="https://github.com/user-attachments/assets/0229083e-6226-474c-ba81-24fafad676e0" />*
>
> 
> **3.**
> *<img width="2496" height="1308" alt="kép" src="https://github.com/user-attachments/assets/3f5c0c4a-50f1-4365-916e-0f59c3af8cd5" />*


---

## 🚀 Főbb Funkciók és Képességek

A rendszer nem csupán egy egyszerű rajzolóprogram, hanem egy teljes értékű kollaboratív platform.

- **Valós idejű szinkronizáció (Real-Time Sync):** A WebSockets / Firebase Realtime Database technológiának köszönhetően a rajzolás, az alakzatok mozgatása és a felhasználók kurzorai milliszekundumos késleltetéssel jelennek meg minden résztvevőnél.
- **Fejlett Hitelesítési Rendszer:** 
  - Biztonságos hagyományos Email/Jelszó alapú regisztráció jelszóerősség-mérővel.
  - Gyors Google OAuth (SSO) bejelentkezési lehetőség.
  - **"Vendég" (Guest) Mód:** Lehetőség az alkalmazás azonnali, regisztráció nélküli kipróbálására perzisztens, lokálisan mentett munkamenettel.
- **Állapotmegőrzés (Persistence):** Az alkalmazás a frissítések (F5) és oldalváltások között is zökkenőmentesen megőrzi a felhasználói munkamenetet a `localStorage` és a Zustand Persist middleware segítségével.
- **Rugalmas Rajzolóeszközök:** Többféle ecset, szín, alakzat és törlési funkció támogatása.
- **Privát és Publikus Munkaterületek:** A létrehozott táblák jogosultságainak kezelése (ki láthatja, ki szerkesztheti).

---

## 🛠️ Technológiai Architektúra (Stack)

Az alkalmazás a modern frontend fejlesztés legjobb gyakorlatait követi, elválasztva az állapotkezelést, a UI réteget és a backend kommunikációt.

### Frontend
- **React 19 & TypeScript:** Erősen tipizált, modern komponens-alapú architektúra a hibamentes és könnyen karbantartható kódért.
- **Vite:** Hihetetlenül gyors fejlesztői környezet és optimalizált produkciós build.
- **Zustand:** Egy apró, de rendkívül gyors állapotkezelő (State Management) könyvtár, amely ideális a valós idejű rajz-adatok és az applikációs szintű állapotok (pl. Auth) kezelésére.
- **Framer Motion:** Komplex, mégis zökkenőmentes mikro-animációk és oldalátmenetek biztosítása.
- **React Router v7:** Deklaratív útvonalválasztás, privát (AuthGuard) és publikus útvonalak biztonságos elválasztásával.
- **SCSS / Sass:** Moduláris, változókkal és mixinekkel strukturált egyedi dizájnrendszer. Nincsenek előregyártott UI könyvtárak, minden felületi elem egyedi tervezésű a prémium megjelenés érdekében.

### Backend as a Service (BaaS)
- **Firebase Authentication:** Biztonságos és skálázható felhasználó-azonosítás.
- **Firebase Firestore:** A strukturált adatok (felhasználói profilok, táblák metainformációi, jogosultságok) tárolására.
- **Firebase Realtime Database:** A rajzolási folyamat és az élő kurzorpozíciók szinkronizálására optimalizált NoSQL adatbázis (mivel ez sokkal alacsonyabb késleltetésű és költséghatékonyabb a folyamatos adatáramlás esetén, mint a Firestore).

---

## 🧠 Technikai Kihívások és Megoldások

A projekt fejlesztése során több komplex technológiai problémát is meg kellett oldani:

1. **Valós idejű állapot szinkronizálása a hálózaton:** 
   *Kihívás:* Ha több felhasználó egyszerre rajzol, az állapot (state) könnyen aszinkronba kerülhet, vagy a túl sok adatbázis-kérés túlterhelheti a rendszert.
   *Megoldás:* Optimalizált adatstruktúrák és "throttling" / "debouncing" technikák alkalmazása a hálózati kérések csökkentésére. A folyamatos egérmozgások a Realtime Database-be, míg a véglegesített alakzatok a Firestore-ba kerülnek.

2. **Zökkenőmentes Vendég Munkamenet (Guest Session):**
   *Kihívás:* Hogyan biztosítsunk élvezetes kipróbálási lehetőséget anélkül, hogy az oldalfrissítés kidobná a felhasználót, miközben a Firebase Auth-al is együtt kell működni?
   *Megoldás:* A Zustand `persist` middleware implementálása egyedi szinkronizációs logikával az `onAuthStateChanged` események között, így a lokális vendég fiók és a távoli Firebase hitelesítés konfliktusmentesen él egymás mellett.

---

*Tervezte és Fejlesztette: **stigibalint** | 2024*
