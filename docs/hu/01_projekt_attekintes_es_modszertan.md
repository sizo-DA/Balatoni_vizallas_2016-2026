# Balaton vízállás-adatok elemzése, 2016–2026
## Projektáttekintés: cél, adatforrás és módszertan

### 1. A projekt célja

A projekt célja a Siófok [2888] mérőállomáson rögzített balatoni felszíni vízállás-adatok feldolgozása és feltáró adatelemzése a:
    2016. szeptember 30. és 2026. szeptember 30. 
közötti időszakra. 
A munka egy teljes, reprodukálható adatelemzési folyamatot mutat be: a nyers adatforrások feltárásától és minőségellenőrzésétől az adat-migráción és a feltáró elemzésen át az elemzésre alkalmas adatkészletek kialakításáig.

### 2. Adatforrás és vizsgált változók

Az alapadatok a Vízügyi adatportál (data.vizugy.hu) Siófok [2888] állomásához tartozó CSV-állományokból származnak. Az eredeti évpáros fájlok a vízállás mellett a vízfelszín közelében mért vízhőmérsékletet is tartalmazzák.

A projekt elsődleges változója a felszíni vízállás, centiméterben. A vízhőmérsékletet az első tervben bevontuk, de a rendelkezésre álló adatok hiányossága miatt végül nem lett a fő elemzés része.

Az időszak két széle nem teljes naptári év: 2016. szeptember 30-án kezdődik, 2026. szeptember 30-án ér véget. A 2016-os és 2026-os éves mutatókat ezért részleges évként kell értelmezni.

### 3. Módszertani folyamat

A feldolgozás hat, egymásra épülő notebookban történt.

1. **Adatforrások feltárása:** a nyers CSV-k fájlnevének, méretének, kódolásának, elválasztójelének, oszlopszerkezetének és hiányzó adatainak vizsgálata. Ebben a fázisban a nyers adatok nem módosultak.
2. **Első adat-migráció:** az eredeti elképzelés szerint olyan állomány előállítása, amelyben az időpont, a vízállás és a vízhőmérséklet egyaránt érvényes.
4. **Projekt-újraértékelés:** a vízhőmérsékleti adatok tényleges lefedettségének vizsgálata, majd a fő elemzési cél módosítása. Az eredeti elképzelés szerint, az elemzésben csak a napi egyszer mért (minden reggel 7:00) vízhőmérsékleti adattal is rendelkező sorok elemzése történt volna meg. Az elsődleges elemzések alapján azonban több évben is csak évi 1-3 vízhő adat állt rendelkezésre. A vízhűmérsékleti adatokkal együtt elemzett adatokból így az eredeti adatállomány 1.08%-a maradt volna meg - abban is több, hiányos adatok miatti torzítás. Így a projekt újragondolásával elvetettük a vízhőmérsékleti adatok bevonását az elemzésbe.
5. **Vízállás-adatok újramigrálása:** minden érvényes időponttal és numerikus vízállással rendelkező rekord megtartása, a vízhőmérséklet meglététől függetlenül.
6. **Feltáró adatelemzés (EDA):** adatminőség, időbeli lefedettség, mérési gyakoriság, vízállás-idősor, éves, havi és évszakos statisztikák, szélsőértékek és rövid távú változások vizsgálata.
7. **Eredmények összegzése és elemzési adatkészlet kialakítása:** a mérési szintű adatok megőrzése mellett napi összesítő adatkészlet előállítása.

### 4. Alkalmazott adatkezelési elvek

- Az eredeti CSV-fájlok változatlanok maradnak.
- A forrásfájl neve és a fájlon belüli eredeti rekordsorszám megőrzésre kerül.
- Az eredeti vízállásméréseket nem aggregáljuk a migráció során.
- Az ismétlődő időpontokat nem töröljük automatikusan; előbb vizsgálni kell azok jellegét.
- A szélsőséges vízállásértékeket megjelöljük és elemezzük, nem töröljük automatikusan.
- A részleges éveket elkülönítjük a teljes naptári évektől.
- A fájlméret vagy az éves rekorddarabszám önmagában nem bizonyít mérési gyakoriság-változást; ehhez az időbélyegek közötti időközöket és a napi rekorddarabszámokat vizsgáljuk.

### 5. A projekt határai

A projekt leíró és feltáró adatelemzés. Nem célja a vízszintváltozások ok-okozati magyarázata, a tó víztérfogatának becslése vagy előrejelző modell építése. A vízállás változása önmagában nem azonos a párolgással vagy a tó víztérfogat-változásával. Külső magyarázó adatok – például csapadék, szél, léghőmérséklet vagy vízügyi beavatkozások – nem részei ennek a projektnek.

### 6. Fő eredmény

A projekt végére létrejött egy dokumentált, egységesített, vízállásra fókuszáló adatkészlet, az adatok mérési szintű megőrzésével és egy napi szintű származtatott állománnyal. A hat notebook együtt bemutatja az adatfeldolgozási döntéseket, azok indoklását és az elemzési eredményeket.
