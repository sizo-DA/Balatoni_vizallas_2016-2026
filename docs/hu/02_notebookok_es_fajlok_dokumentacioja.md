# Balaton vízállás-adatok elemzése, 2016–2026
## A programok és a létrehozott fájlok dokumentációja

### 1. A notebookok egymásra épülése

A projekt hat Jupyter-notebookból áll. Minden notebook egy önálló munkafázist valósít meg, és az előző lépés eredményeire épít.

| Sorszám | Notebook | Feladat | Kapcsolat a következő lépéssel |
|---|---|---|---|
| 01 | `01_data_source_and_inspection.ipynb` | Nyers CSV-k feltárása, szerkezet- és adatminőség-vizsgálat | Megadja a migrációhoz szükséges tényleges oszlopszerkezetet és beolvasási jellemzőket |
| 02 | `02_initial_data_migration.ipynb` | Első migráció, amely az időpontot, vízállást és vízhőmérsékletet is megköveteli | Létrehozza az összevont és a vízhőmérséklet szerint szűrt állományt |
| 03 | `03_project_reassessment.ipynb` | Az első szűrés eredményének értékelése, a projektirány módosítása | Megindokolja, miért szükséges a vízállás-adatok önálló újramigrálása |
| 04 | `04_water_level_data_migration.ipynb` | A teljes, érvényes vízállás-adatállomány előállítása | A 05. notebook bemeneti adatát készíti el |
| 05 | `05_water_level_eda.ipynb` | A vízállás-adatok feltáró elemzése | Jelentéseket és ábrákat állít elő; ezek alapján készül a projektzárás |
| 06 | `06_eda_results_and_analytical_dataset.ipynb` | Eredmények összegzése, duplikációk vizsgálata, mérési és napi elemzési állomány előállítása | A projekt végső, további elemzésekre alkalmas adatkimeneteit készíti el |

### 2. A projekt javasolt mappaszerkezete

```text
Balatoni_vizallas_2016-2026/
├── README.md
├── Raw_data_2016-2026/
├── data/
│   ├── interim/
│   └── processed/
├── notebooks/
│   ├── 01_data_source_and_inspection.ipynb
│   ├── 02_initial_data_migration.ipynb
│   ├── 03_project_reassessment.ipynb
│   ├── 04_water_level_data_migration.ipynb
│   ├── 05_water_level_eda.ipynb
│   └── 06_eda_results_and_analytical_dataset.ipynb
└── reports/
    └── figures/
```

A `Raw_data_2016-2026` mappában az eredeti, változatlan CSV-fájlok vannak. A `data/interim` köztes, a `data/processed` feldolgozott adatkészleteket tartalmaz. A `reports` mappa az összesítő táblák és az ábrák helye.

### 3. Notebookonkénti kimenetek és szerepük

#### 01 – Adatforrások és CSV-fájlok feltárása

**Feladat:** a tíz évpáros CSV-fájl beolvasási jellemzőinek, méretének, oszlopainak, adattípusainak és hiányzó értékeinek feltárása. A notebook nem módosítja a nyers adatokat.

**Létrehozott fájl:**
- `reports/01_fajlonkenti_adatminosegi_osszefoglalo.csv` – fájlonkénti rekorddarabszám, fájlméret, hiányzó vízállás- és vízhőmérséklet-adatok. Azért jött létre, hogy a forrásfájlok összehasonlíthatók legyenek, és a migrációs szabályok adatokra alapozva készüljenek.

#### 02 – Első adat-migráció

**Feladat:** a nyers fájlok egységesítése, dátum- és numerikus konverzió, majd az időpont, vízállás és vízhőmérséklet együttes meglétét megkövetelő szűrés.

**Létrehozott fájlok:**
- `data/interim/balaton_2016-2026_osszesitett_szures_elott.csv` – minden beolvasott rekord egységes szerkezetben, a vízhőmérséklet szerinti szűrés előtt. A szűrés hatásának ellenőrzésére szolgál.
- `data/processed/balaton_2016-2026_vizallas_vizho_ervenyes.csv` – az első terv szerint mindhárom érvényes mezőt tartalmazó rekordok.
- `data/processed/balaton_2016-2026_vizallas_vizho_ervenyes.xlsx` – ugyanennek Excel-változata, kézi ellenőrzéshez.
- `data/processed/02_migracios_osszehasonlitas_fajlonkent.csv` – a szűrés előtti és utáni rekordszámok fájlonkénti összehasonlítása.

A köztes állomány azért fontos, mert a későbbi újraértékelésnél nem kell visszatérni a nyers fájlokhoz az első szűrés hatásának megállapításához.

#### 03 – A projekt újraértékelése

**Feladat:** annak ellenőrzése, hogy a vízhőmérsékletet is megkövetelő szűrés után marad-e elegendő és megfelelő időbeli lefedettségű adat.

**Létrehozott fájlok:**
- `reports/03_projekt_ujraertekeles_osszefoglalo.csv` – az összes vízállásrekord, a vízállással és vízhőmérséklettel együttesen érvényes rekordok száma, aránya és a meghozott döntés.
- `reports/03_eves_adatmennyiseg_osszehasonlitas.csv` – az eredeti és az együttesen használható adatmennyiség fájlonkénti/éves összevetése.

Ezek a fájlok a módszertani fordulat dokumentálására jöttek létre: a projekt fő iránya a teljes vízállás-adatsor elemzése lett, a vízhőmérséklet meglététől függetlenül.

**Elemzői döntés:**
A vízhőmérsékleti adatok hiányossága és a teljes adatbázis adatainak "eldobása" (a vízszint - vízhő adatpáros aránya a teljes adatbázisban 1.08%), az elemzési célok újragondolásával.

#### 04 – Vízállás-adatok újramigrálása

**Feladat:** minden olyan rekord megtartása, amelyben az időpont értelmezhető és a vízállás numerikus. A vízhőmérséklet nem szűrési feltétel. A forrásfájl és a forráson belüli sorszám megmarad.

**Létrehozott fájlok:**
- `data/interim/balaton_2016-2026_vizallas_osszes_konvertalt.csv` – minden beolvasott rekord egységesített időpont- és vízállásmezővel, a végleges érvényességi szűrés előtt.
- `data/processed/balaton_2016-2026_vizallas_teljes.csv` – a teljes, érvényes vízállás-adatállomány; a 05. notebook bemenete.
- `data/processed/balaton_2016-2026_vizallas_teljes.xlsx` – a végleges migrációs adatállomány Excel-változata.
- `reports/04_vizallas_migracio_fajlonkent.csv` – beolvasott, kizárt és megtartott rekordok fájlonként.
- `reports/04_vizallas_rekordok_naptari_evenkent.csv` – naptári évenkénti rekordszám, a részleges évek jelölésével.

#### 05 – Vízállás-adatok feltáró elemzése (EDA)

**Feladat:** a teljes vízállás-adatállomány szerkezetének és leíró jellemzőinek feltárása. Vizsgálja a mérési gyakoriságot, időbeli lefedettséget, éves/havi/évszakos vízállásstatisztikákat, szélsőértékeket, rövid távú változásokat és napi ingadozást.

**Jelentésfájlok a `reports` mappában:**
- `05_adatminosegi_osszefoglalo.csv` – alapvető minőségi mutatók.
- `05_eda_fo_osszefoglalo.csv` – a teljes adatsor fő statisztikai jellemzői.
- `05_eves_adatlefedettseg.csv` – éves rekordmennyiség és időbeli lefedettség.
- `05_meresi_idokoz_evenkent.csv` – egymást követő mérések közötti időköz éves összesítése.
- `05_napi_meresi_darabszam.csv` – napi mérési darabszám, a mérési rend és hiányos napok vizsgálatához.
- `05_eves_meresi_gyakorisag.csv` – napi mérési darabszám éves mediánja/átlaga, a napi 96 mérés előfordulása.
- `05_napi_vizallas_osszesites.csv` – napi átlag, minimum, maximum, mérési darabszám és 30 napos gördülő átlag.
- `05_eves_vizallas_statisztikak.csv` – éves minimum, maximum, átlag, medián, szórás és kvartilisek.
- `05_eves_minimum_maximum_datumok_teljes_evek.csv` – a teljes évek éves minimum- és maximumértékei és időpontjai.
- `05_havi_vizallas_statisztikak.csv` – havi leíró statisztikák.
- `05_evszakos_vizallas_statisztikak.csv` – évszakos leíró statisztikák.
- `05_legalacsonyabb_meresek.csv`, `05_legmagasabb_meresek.csv` – legalacsonyabb és legmagasabb mérések.
- `05_vizallasvaltozas_kiugro_jelolesek.csv` – rövid távú változások és statisztikai kiugrójelölések.
- `05_napi_vizallas_terjedelem.csv` – napi minimum–maximum terjedelem és mérési darabszám.

**Ábrák a `reports/figures` mappában:**
- `05_annual_daily_measurement_frequency.png` – éves napi mérési gyakoriság.
- `05_96_measurements_daily_share.png` – a napi 96 mérés előfordulási aránya.
- `05_annual_water_level_extremes_trends.png` – éves minimumok és maximumok, kizárólag a teljes 2017–2025-ös évekre.

A jelentések azért készültek, hogy az EDA megállapításai ne csak a notebook futási kimeneteiben, hanem külön fájlokban is megőrizhetők és újrafelhasználhatók legyenek.

#### 06 – Eredmények összegzése és elemzési adatkészletek

**Feladat:** a korábbi eredmények összegzése, a duplikált időpontok külön vizsgálata, majd a mérési szintű és napi szintű elemzési adatkészlet előállítása.

**Létrehozott fájlok:**
- `data/processed/balaton_vizallas_meresi_szintu_elemzesi_adatok.csv` – az eredeti mérési rekordok, naptári év/hónap/nap mezőkkel, duplikált időpont jelölésével és a mérési rend időszakának címkéjével.
- `data/processed/balaton_vizallas_napi_elemzesi_adatok.csv` – napi átlag, medián, minimum, maximum, terjedelem, mérési darabszám és duplikált időpontú rekordok száma.
- `reports/06_adatminosegi_ellenorzes.csv` – a projektzáró alapellenőrzések.
- `reports/06_duplikalt_idopontok_vizsgalata.csv` – duplikált időpontcsoportok és az azokhoz tartozó értékek.
- `reports/06_elemzesi_adatkimenetek_ellenorzese.csv` – a két végső adatkészlet rekordszáma és időbeli lefedettsége.

A kétféle adatkészlet eltérő felhasználást szolgál. A mérési szintű állomány megőrzi a részletes időbeli információt; a napi állomány egyszerűbb összehasonlításokat és későbbi aggregált elemzéseket tesz lehetővé.

### 4. A fájlok szerepe a teljes folyamatban

A `raw`/nyers fájlok jelentik a változatlan forrást. Az `interim` fájlok a migrációs döntések és konverziók ellenőrzését teszik lehetővé. A `processed` fájlok már meghatározott elemzési szabályok szerint előállított adatállományok. A `reports` fájlok az egyes lépések ellenőrzési eredményeit, statisztikáit és ábráit őrzik.

A projekt reprodukálhatósága érdekében a notebookokat sorrendben kell futtatni. A 03. notebook a 02. kimeneteire, a 05. a 04. migrációs kimenetére, a 06. pedig a 04. és 05. lépés adataira/jelentéseire támaszkodik.
