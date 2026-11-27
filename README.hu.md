# Balatoni vízállás-adatok elemzése (2016–2026)

## A projekt áttekintése

A projekt célja a Balaton siófoki, [2888] azonosítójú mérőállomásán rögzített felszíni vízállás-adatok feldolgozása és feltáró adatelemzése a **2016. szeptember 30. és 2026. szeptember 30. közötti időszakra**.

A munka egy teljes, dokumentált és reprodukálható adatelemzési folyamatot mutat be: a nyers adatforrások feltárásától és minőségellenőrzésétől az adat-migráción és a feltáró elemzésen át az elemzésre alkalmas adatkészletek kialakításáig.

## Adatforrás és vizsgált adatok

Az alapadatok a [Vízügyi adatportálról](https://data.vizugy.hu), a Siófok [2888] mérőállomáshoz tartozó CSV-állományokból származnak. Az eredeti fájlok a felszíni vízállás mellett a vízfelszín közelében mért vízhőmérsékletet is tartalmazzák.

A végleges elemzés elsődleges változója a **felszíni vízállás (cm)**. A vízhőmérséklet az eredeti elemzési terv része volt, de az adatok elégtelen lefedettsége miatt végül nem került be a fő elemzésbe. A végleges migráció minden érvényes időponttal és numerikus vízállásértékkel rendelkező rekordot megtart, a vízhőmérséklet meglététől függetlenül.

A vizsgált időszak első és utolsó éve nem teljes naptári év: az adatok 2016. szeptember 30-án kezdődnek és 2026. szeptember 30-án érnek véget. A két részleges év éves mutatóit ezért a teljes naptári évektől elkülönítve kell értelmezni.

## Az elemzési folyamat

A projekt hat, egymásra épülő Jupyter-notebookból áll:

1. **Adatforrások feltárása** – a nyers CSV-fájlok nevének, méretének, kódolásának, elválasztójelének, oszlopszerkezetének és hiányzó adatainak vizsgálata. A nyers adatok ebben a fázisban nem módosulnak.
2. **Első adat-migráció** – az eredeti terv szerinti összevont állomány létrehozása, amelyben az időpont, a vízállás és a vízhőmérséklet egyaránt érvényes.
3. **A projekt újraértékelése** – a vízhőmérsékleti adatok lefedettségének értékelése, majd a fő elemzési cél módosításának dokumentálása.
4. **Vízállás-adatok újramigrálása** – a teljes, érvényes vízállás-adatállomány előállítása a vízhőmérséklet meglététől függetlenül.
5. **Feltáró adatelemzés (EDA)** – adatminőség, időbeli lefedettség, mérési gyakoriság, vízállás-idősor, éves, havi és évszakos statisztikák, szélsőértékek és rövid távú változások vizsgálata.
6. **Eredmények összegzése és elemzési adatkészletek kialakítása** – a fő eredmények összefoglalása, a duplikált időpontok vizsgálata, valamint mérési szintű és napi szintű adatkészlet előállítása.

A notebookokat számozásuk szerinti sorrendben kell futtatni. A 03. notebook a 02. lépés kimeneteire, a 05. a 04. migrációs adatkészletére, a 06. pedig a korábbi lépések adataira és jelentéseire támaszkodik.

## Főbb eredmények

- A végleges, migrált vízállás-adatállomány **221 802 rekordot** tartalmaz.
- A teljes adatsorban a mért vízállás minimuma **27 cm**, maximuma **154 cm**, átlaga **100,32 cm**, mediánja **103 cm**.
- Az előzetes adatminőségi összesítés 221 805 vízállásrekord mellett 2 395 vízhőmérsékleti értéket tartalmazó rekordot jelzett, ami körülbelül **1,08%**. Ez a lefedettség nem biztosított megfelelő alapot a teljes időszak együttes elemzéséhez. Az előzetes összesítés rekordszáma és a végleges migrált állomány rekordszáma eltér; a végleges vízállás-adatkészlet 221 802 rekordból áll.
- A mérési gyakoriság 2022 körül jelentősen megváltozott. A mérések közötti időköz mediánja 2016–2021 között 30 perc, 2022-től 15 perc. A napi mérési darabszám mediánja a korábbi időszak 26–29 rekordjáról 96 rekordra emelkedett.
- A 2022–2025 közötti teljes években a napok 95,62–97,53%-án pontosan 96 mérés szerepel.
- A havi átlagok közül április értéke a legmagasabb (112,55 cm), szeptemberé a legalacsonyabb (80,45 cm). Az évszakos átlagok leíró statisztikák; önmagukban nem bizonyítják a statisztikailag szignifikáns szezonalitást.

## A létrehozott adatkészletek

A projekt két fő, további elemzésekhez felhasználható adatkészletet állít elő:

- **Mérési szintű adatkészlet:** megőrzi az egyedi mérési rekordokat és a részletes időbeli információkat, többek között a duplikált időpontok jelölését.
- **Napi szintű adatkészlet:** napi átlagot, mediánt, minimumot, maximumot, terjedelmet, mérési darabszámot és a duplikált időpontú rekordok számát tartalmazza.

A notebookok további CSV-jelentéseket és grafikonokat készítenek. Ezek helye a `reports/` könyvtár, az ábráké a `reports/figures/` mappa. A részletes magyar dokumentáció a `docs/hu/` könyvtárban található.

## A repó javasolt mappaszerkezete

```text
Balatoni_vizallas_2016-2026/
├── README.md                    # Angol nyelvű projektismertető
├── README.hu.md                 # Magyar nyelvű projektismertető
├── Raw_data_2016-2026/          # Eredeti, változatlan CSV-fájlok
├── data/
│   ├── interim/                 # Köztes adatállományok
│   └── processed/               # Feldolgozott, elemzésre kész adatok
├── notebooks/                   # A hat, sorrendben futtatandó notebook
├── reports/
│   └── figures/                 # Jelentések és grafikonok
└── docs/
    └── hu/                      # Részletes magyar dokumentáció
```

## Adatkezelési alapelvek

- Az eredeti CSV-fájlok változatlanok maradnak.
- A migráció során megőrizzük a forrásfájl nevét és a fájlon belüli eredeti rekordsorszámot.
- Az eredeti vízállásméréseket a migráció során nem aggregáljuk.
- Az ismétlődő időpontokat nem töröljük automatikusan; előbb megvizsgáljuk azok jellegét.
- A szélsőséges vízállásértékeket megjelöljük és ellenőrizzük, nem töröljük automatikusan.
- A részleges naptári éveket elkülönítjük a teljes évektől.
- A fájlméret és az éves rekordszám önmagában nem bizonyítja a mérési gyakoriság változását; ehhez az időbélyegek közötti időközöket és a napi rekorddarabszámokat is vizsgáljuk.

## A projekt korlátai

A projekt egyetlen mérőállomás adatain alapuló leíró és feltáró adatelemzés. Nem célja a vízszintváltozások ok-okozati magyarázata, a tó víztérfogat-változásának becslése, a párolgás meghatározása vagy előrejelző modell építése.

A vízállás változása önmagában nem azonos a párolgással vagy a tó víztérfogat-változásával. A csapadékra, szélre, léghőmérsékletre, légnyomásra és vízügyi beavatkozásokra vonatkozó külső magyarázó adatok nem részei ennek a projektnek. A duplikált időpontok és a szokatlan mérési értékek további kontextuális ellenőrzést igényelnek, mielőtt kizárásukról vagy módosításukról döntés születne.

## Lehetséges folytatás

A jelenlegi projekt a feltáró elemzéssel és az elemzési adatkészletek kialakításával lezárul. Külön projektként folytatható:

- a hosszú távú trendek és szezonális komponensek részletes vizsgálata egységes időfelbontás mellett;
- meteorológiai és vízügyi adatok integrálása, például csapadék, szélsebesség és -irány, léghőmérséklet, légnyomás, valamint a Sió-zsilip működésére és a vízleeresztésre vonatkozó adatok;
- a vízállás és a külső változók közötti kapcsolatok, valamint a késleltetett összefüggések vizsgálata;
- előrejelzési modell készítése, miután a mérési gyakoriság változását, az idősor szerkezetét és a lehetséges magyarázó változókat megfelelően értékeltük.

## Dokumentáció

A repó gyökérkönyvtárában található `README.md` az angol nyelvű projektismertető. A részletes magyar dokumentáció a `docs/hu/` mappában érhető el:

- [Projektáttekintés, cél és módszertan](docs/hu/01_projekt_attekintes_es_modszertan.md)
- [Notebookok és létrehozott fájlok dokumentációja](docs/hu/02_notebookok_es_fajlok_dokumentacioja.md)
- [Eredmények, grafikus bemutatás és lehetséges folytatás](docs/hu/03_eredmenyek_es_lehetseges_folytatas.md)
