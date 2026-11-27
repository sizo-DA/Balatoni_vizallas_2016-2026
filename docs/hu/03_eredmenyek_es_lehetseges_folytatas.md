# Balaton vízállás-adatok elemzése, 2016–2026
## Eredmények, grafikus bemutatás és lehetséges folytatás

### 1. Az adatsor fő jellemzői

A végleges migrációs adatsor 221 802 vízállásrekordot tartalmaz. Az első időpont 2016. szeptember 30. 00:30, az utolsó 2026. szeptember 30. 03:00. A mért vízállás minimuma 27 cm, maximuma 154 cm, átlaga 100,32 cm, mediánja 103 cm. A teljes időszakban 1 056 olyan rekord található, amelynek időpontja legalább egy másik rekordnál is előfordul.

A 2016-os és 2026-os év részleges. Az éves statisztikák és a teljes évek összehasonlítása során a két részleges évet külön kell kezelni.

### 2. A projekt módszertani fordulata: a vízhőmérséklet lefedettsége

Az eredeti elképzelés a vízállás és vízhőmérséklet együttes elemzése volt. A fájlonkénti adatminőségi összesítő szerint 221 805 vízállásrekord mellett mindössze 2 395 rekord tartalmazott vízhőmérsékletet, ami körülbelül 1,08%. Ez a lefedettség nem biztosított megfelelő adatmennyiséget a teljes időszak együttes elemzéséhez.

A projekt ezért a teljes, érvényes vízállás-adatsor vizsgálatára állt át. A vízhőmérsékletet nem töröltük az eredeti forrásokból, de nem tettük a fő adatkészletbe kerülés feltételévé.

### 3. A mérési gyakoriság megváltozása

A mérési időközök mediánja 2016–2021 között 30 perc, 2022-től 15 perc. A napi mérési darabszám mediánja a korábbi időszakban 26–29, 2022-től 96. A napi 96 mérés 15 perces időköznek felel meg, ha a mérés a nap teljes 24 órájában folyamatos.

A 2022–2025 közötti teljes években a napok 95,62–97,53%-án pontosan 96 mérés szerepel. A megfigyelt adatok tehát egyértelmű mérési gyakoriság-váltást mutatnak. Az adatok önmagukban azonban nem azonosítják a változás műszaki vagy szervezeti okát.

![Éves napi mérési gyakoriság](kepek/05_annual_daily_measurement_frequency.png)

![A napi 96 mérés aránya](kepek/05_96_measurements_daily_share.png)

**Értelmezési következmény:** az éves nyers rekordszámok közvetlen összehasonlítása félrevezető lehet, mert 2022-től ugyanannyi idő alatt nagyjából háromszor annyi mérés keletkezik, mint a korábbi időszakban. A későbbi összehasonlításoknál ezért időalapú aggregálásra, például napi statisztikákra vagy egységes időfelbontásra van szükség.

### 4. A vízállás időbeli alakulása

A napi átlag és a 30 napos gördülő átlag az eredeti mérési pontoknál áttekinthetőbben mutatja a hosszabb időtávú változásokat. A gördülő átlag simítja a rövid távú ingadozásokat, de nem helyettesíti az eredeti méréseket.

![Napi átlag és 30 napos gördülő átlag](kepek/napi_atlag_es_gordulo_atlag.png)

A projekt ebben a szakaszban nem állít fel ok-okozati magyarázatot az emelkedésekre vagy csökkenésekre. A vízállás alakulását külső hidrometeorológiai és vízügyi adatok nélkül csak leíró módon lehet bemutatni.

### 5. Éves szélsőértékek

A teljes naptári éveket (2017–2025) vizsgálva az éves minimum és maximum közötti különbség 47–80 cm között alakult. A legkisebb éves terjedelem 2018-ban 47 cm, a legnagyobb 2022-ben 80 cm volt. A 2024-es évben mérték a teljes vizsgált adatsor legmagasabb értékét, 154 cm-t; a 2026-os részleges évben fordult elő a teljes adatsor legalacsonyabb értéke, 27 cm.

![Éves minimumok és maximumok, teljes évek](kepek/05_annual_water_level_extremes_trends.png)

Az éves szélsőértékek trendvonalai leíró jellegűek. A teljes adatsor egyetlen mérőállomásának minimum- és maximumértékeiből nem lehet önmagában a Balaton vízháztartására vagy a vízállásváltozás okaira következtetni.

### 6. Havi és évszakos különbségek

A teljes rendelkezésre álló adatsorban a havi átlagok közül április értéke a legmagasabb (112,55 cm), szeptemberé a legalacsonyabb (80,45 cm). Az évszakos átlag tavasszal 111,88 cm, télen 103,28 cm, nyáron 98,64 cm, ősszel 86,17 cm.

![Havi átlagos vízállás](kepek/havi_atlagos_vizallas.png)

![Évszakos átlagos vízállás](kepek/evszakos_atlagos_vizallas.png)

Ezek összesített leíró statisztikák. A havi/évszakos eltérések évenkénti stabilitását és statisztikai bizonytalanságát külön elemzésben lehetne vizsgálni.

### 7. Adatminőségi és értelmezési korlátok

- A 2016-os és 2026-os év részleges.
- A mérési gyakoriság 2022-ben megváltozott; az éves nyers rekorddarabszámok emiatt nem hasonlíthatók össze közvetlenül.
- A duplikált időpontok nem lettek automatikusan törölve. A projektzáró notebook külön táblázatot készít róluk; az esetleges azonos időponthoz tartozó eltérő vízállásértékek további ellenőrzést igényelnek.
- A szélsőséges értékek jelölése nem jelent automatikus adathiba-minősítést.
- A vízállásértékekből önmagukban nem becsülhető meg a tó víztérfogat-változása vagy a párolgás.
- A vizsgálat egyetlen mérőállomás adataira épül.
- Az adatok nem tartalmaznak a vízállásváltozás okait közvetlenül magyarázó külső változókat.

### 8. A projekt végtermékei

A projekt két végső elemzési adatkészletet céloz meg:

1. **Mérési szintű adatkészlet:** az eredeti mérések megőrzésével, időbeli bontásokkal és duplikációs jelöléssel.
2. **Napi szintű adatkészlet:** napi átlag, medián, minimum, maximum, terjedelem, mérési darabszám és duplikált időpontú rekordok száma.

A mérési szintű állomány a részletes vizsgálatok alapja; a napi állomány egységesebb időfelbontású összehasonlításokat tesz lehetővé. A napi mérési darabszám megőrzése fontos, mert jelzi az egyes napi összesítések adatbázisának méretét.

### 9. Lehetséges folytatás – külön projektként

A jelenlegi fejlesztési projekt a feltáró elemzéssel és az elemzési adatkészletek kialakításával lezárul. A következő témák külön projektként indíthatók:

**9.1. Trend- és szezonális komponensek részletes vizsgálata**
- egységes időfelbontás kiválasztása;
- hiányzó időszakok és mérési rend változásának kezelése;
- hosszú távú trend, éves ciklus és rövidebb időszakos mintázatok elkülönítése;
- a mintázatok évek közötti stabilitásának vizsgálata.

**9.2. Külső magyarázó adatok integrálása**
- csapadék;
- szélsebesség és szélirány;
- léghőmérséklet;
- légnyomás;
- vízügyi üzemeltetési adatok, különösen a Sió-zsilip működése és a vízleeresztés.

Az adatok integrálása előtt a mérőállomások térbeli közelségét, időbeli felbontását, mértékegységeit és hiányosságait ellenőrizni kell.

**9.3. Magyarázó elemzés**
- a vízállás és a meteorológiai változók közötti kapcsolatok vizsgálata;
- késleltetett összefüggések elemzése;
- a vízügyi beavatkozások figyelembevétele;
- az összefüggések bizonytalanságának és korlátainak dokumentálása.

**9.4. Előrejelzési projekt**
Előrejelzési modell csak az időbeli szerkezet, a mérési gyakoriság és a lehetséges magyarázó változók tisztázása után indokolt. Elsőként egyszerű referencia-modelleket érdemes összehasonlítani, majd időrendhelyes tanító- és tesztidőszakokat kijelölni. Ez a feladat nem része a most lezárt projektnek.

### 10. Záró megállapítás

A projekt legfontosabb eredménye nem egy előrejelző modell, hanem egy ellenőrzött, visszakövethető és dokumentált adatelemzési folyamat. A munka bemutatja: 
- hogyan vezethet az adatminőség vizsgálata az eredeti elemzési terv módosításához,
- miért fontos a mérési gyakoriság változásának felismerése,
- hogyan lehet a nyers mérési adatokat úgy megőrizni, hogy azok többféle későbbi elemzés alapjául szolgáljanak.
