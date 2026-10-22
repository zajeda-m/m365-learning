# Týden 2: SharePoint a oprávnění podle rolí

Zkušební tenant Microsoft 365 Business Basic, 22. 10. 2026. Všechna jména jsou smyšlená.

## Cíl
Pochopit, jak se ve SharePointu Online přiřazují práva k webům, knihovnám, složkám a souborům, jak funguje sdílení, a ověřit to v praxi na testovacích uživatelích.

## Struktura SharePointu
Web (site) → knihovna nebo seznam → složka → soubor. Oprávnění se ve výchozím stavu dědí shora dolů.

- **Web**: jeden prostor pro jednu oblast a jeden okruh lidí, vlastní adresa a oprávnění.
- **Knihovna dokumentů**: úložiště souborů s verzemi, sloupci s metadaty a filtrováním.
- **Seznam (List)**: tabulka s řádky dat, ne soubory.
- **Složka**: existuje jen uvnitř knihovny.

## Tři výchozí skupiny webu
| Skupina | Úroveň | Pro koho |
|---|---|---|
| Vlastníci | Úplné řízení | správce |
| Členové | Úpravy | kdo obsah tvoří |
| Návštěvníci | Čtení | kdo jen čte |

Do těchto skupin vkládám skupiny zabezpečení z Entra ID (Vedení, Tým), ne jednotlivce.

## Co jsem udělal
1. Vytvořil komunikační web **Test intranet** (šablona Prázdný).
2. Přes *Sdílet web* přidal skupinu **Vedení** do Členů webu (Úpravy) a skupinu **Tým** do Návštěvníků webu (Čtení).
3. Ověřil přes *Zkontrolovat oprávnění*, že Eva (Vedení) má Úpravy a Karel (Tým) Čtení.
4. Vytvořil knihovnu **Vedeni interni**, přerušil dědění a odebral skupinu Návštěvníci.
5. Ověřil dopad výjimky a pak ji zrušil (*Odstranit unikátní oprávnění*).
6. U testovacího souboru otevřel *Spravovat přístup* a prohlédl si nastavení odkazů při sdílení.
7. V admin centru SharePointu prošel *Zásady, Sdílení* (nastavení na úrovni tenantu).

## Výsledky testu
| Uživatel | Skupina | Web | Dokumenty | Vedeni interni (výjimka) | Po vrácení dědění |
|---|---|---|---|---|---|
| Eva | Vedení | Úpravy | nekontrolováno | Úpravy (přes Členy webu) | nekontrolováno |
| Karel | Tým | Čtení | Čtení | Žádná | Čtení |
| Jana | Tým | nekontrolováno | nekontrolováno | Žádná | nekontrolováno |

Výjimka v jedné knihovně neovlivnila knihovnu Dokumenty.

## Postup přerušení a vrácení dědění
1. Knihovna → ozubené kolo → Nastavení knihovny → Další nastavení knihovny.
2. Oprávnění a správa → Oprávnění pro knihovnu dokumentů.
3. *Přestat dědit oprávnění*, potom odebrat nepotřebné skupiny.
4. Vrácení: *Odstranit unikátní oprávnění*.

## Zásada: dědění ze webu
Oprávnění se nastavují jednou, na úrovni webu a skupinám. Knihovny a složky dědí.
Když má obsah jiný okruh lidí, vytvořím samostatný web. Výjimka v knihovně je krajní řešení pro malé a dočasné případy (Vedeni interni jsem vytvořil jen na zkoušku mechanismu).

## K čemu jsou knihovny
Knihovny nejsou na oprávnění, ale na orientaci v dokumentech. Každá má vlastní sloupce (rok, stav, projekt, platnost), pohledy, filtry, šablonu a nastavení verzí. Dělí se podle typu dokumentu, ne podle lidí. Oprávnění řeším na úrovni webů a skupin, organizaci obsahu na úrovni knihoven a sloupců.

## Jak rozhodnout, kam co patří
1. Jiní lidé, jiná citlivost nebo jiný životní cyklus: samostatný web.
2. Stejní lidé, jiný typ dokumentů: nová knihovna.
3. Stejní lidé, stejný typ, jiný rok nebo téma: sloupec, nejvýš dvě úrovně složek.
4. Strukturovaná data místo souborů: seznam (List).

## Příklad struktury pro menší nadaci (jen návrh)
| Web | Upravuje | Čte | Knihovny |
|---|---|---|---|
| Intranet | komunikace, koordinátor | všichni | Směrnice a postupy, Návody, Nástup a odchod, Šablony |
| Granty | grantový tým | vedení | Žádosti, Hodnocení, Smlouvy, Zápisy; seznam Žádosti o grant |
| Vedení | vedení | nikdo další | Strategie, Rozpočty, Personální věci |
| Provoz a IT | koordinátor, vedení | nikdo další | Licence a účty, Dodavatelé a smlouvy, Dokumentace IT, Audit |
| Projekt X | členové projektu | podle potřeby | Podklady, Výstupy; po skončení se web archivuje |

Na každém webu: Vlastníci = správci (dva lidé), Členové = skupina, která obsah tvoří, Návštěvníci = skupina, která jen čte. Knihovny a složky dědí bez výjimek.

## Lidé ve více týmech
V nadaci bude běžné, že je člověk ve více týmech. Ve SharePointu to nevadí.

- Oprávnění se **sčítají**: člověk má vše, co mu dává kterákoli z jeho skupin. Je-li v Týmu (Čtení) a ve Vedení (Úpravy), má Úpravy.
- **Odepřít (deny) ve SharePointu neexistuje.** Přístup se omezuje tím, že se skupina na daný web nedá.
- Skupiny zabezpečení dělat **podle týmů a rolí** (Vedení, Granty, Provoz, Komunikace), ne podle webů. Člověk patří do skupin podle skutečného působení.
- Kdo se přesune do jiného týmu, mění se jen členství ve skupinách, ne weby.
- Pozor na nechtěné zvýšení práv: před přidáním do skupiny ověřit, kam všude ta skupina sahá (*Zkontrolovat oprávnění*).
- Pravidelně (třeba jednou za půl roku) projít členství ve skupinách a mít postup pro nástup a odchod.

Příklad:
| Web | Členové (Úpravy) | Návštěvníci (Čtení) |
|---|---|---|
| Intranet | Komunikace | Všichni kromě externích |
| Granty | Granty | Vedení |
| Vedení | Vedení | nikdo |
| Provoz a IT | Provoz | Vedení |

K otestování: přidat Karla do skupiny Vedení, ověřit v *Zkontrolovat oprávnění* Úpravy (přes Členy webu), pak ho odebrat a ověřit návrat na Čtení. Změna členství se může propsat se zpožděním. Stav: zatím nevyzkoušeno.

## Co znamená „Úpravy"
Úroveň Úpravy (Edit) dovoluje soubory nahrávat, otevírat, měnit, přejmenovávat, přesouvat a **mazat**, stejně jako složky a položky seznamů. Zahrnuje i správu **knihoven a seznamů**: člen může knihovnu vytvořit, přidat sloupec, změnit pohled i knihovnu **smazat**. Nemůže měnit oprávnění a nastavení webu (to je Úplné řízení).

| Úroveň (česky) | Co smí |
|---|---|
| Číst | otevírat a stahovat |
| Přispívat | přidávat, měnit a mazat soubory a položky, ale nespravovat knihovny a seznamy |
| Úpravy | totéž + vytvářet, měnit a mazat knihovny a seznamy |
| Úplné řízení | všechno včetně oprávnění |

Přispívat je pro běžné kolegy často lepší volba než Úpravy. Skupině se přidělí přes *Rozšířená nastavení oprávnění → Udělit oprávnění*.

Mazání není konečné: smazané soubory jdou do koše (celkem 93 dní, nejdřív koš uživatele, pak koš správce) a každý soubor má historii verzí. Stav: Přispívat zatím nevyzkoušeno.

## Sdílení
Sdílení je druhá cesta k obsahu, vedle oprávnění webu. Pokud se nehlídá, obchází nastavenou strukturu.

### Typy odkazů při sdílení souboru
| Typ odkazu | Kdo se k obsahu dostane |
|---|---|
| Kdokoli s odkazem | kdokoli, bez přihlášení, i mimo organizaci |
| Lidé v organizaci | kdokoli přihlášený v tenantu, kdo odkaz má |
| Lidé s existujícím přístupem | jen ti, kdo už práva mají |
| Konkrétní lidé | jen jmenovaní, vzniká jim přístup |

U odkazu se volí úroveň (*Může upravovat* / *Může zobrazit*), datum ukončení platnosti a u veřejných odkazů i heslo. Tlačítko *Použít* v nastavení odkazu jen uloží volbu, nic se neposílá, dokud se nedá *Sdílet* nebo *Kopírovat odkaz*.

### Co ovlivňuje sdílení
- **Tenant** (SharePoint admin centrum → Zásady → Sdílení): nejširší povolená úroveň. Od nejvolnější: Všichni, Noví a existující hosté, Existující hosté, Jenom lidé ve vaší organizaci.
- **Web** (Aktivní weby → web → Nastavení → Externí sdílení): může být stejný nebo přísnější než tenant, nikdy volnější.
- **Kdo smí na webu sdílet** (panel Oprávnění → *Změnit, jakým způsobem mohou členové sdílet*): vlastníci a členové, nebo jen vlastníci; případně schvalování žádostí.
- **Vypršení platnosti hosta** (v panelu Oprávnění): za kolik dní host o přístup přijde. V testu je nastaveno 0, tedy bez omezení.
- Každé sdílení vytváří unikátní oprávnění na souboru. Kdokoli s odkazem obchází celou strukturu.

### Co jsem zjistil v testovacím tenantu
- *Spravovat přístup* u souboru v knihovně Dokumenty: karta **Skupiny (3)** ukazuje Vlastníky (Vlastník), Návštěvníky (Může zobrazit) a Členy (Může upravit). Soubor tedy dědí oprávnění z webu. Karty **Lidé (1)** a **Odkazy** nezkontrolovány.
- V dialogu *Nastavení odkazů* u souboru jsou jen tři volby: Lidé v organizaci, Pouze lidé s existujícím přístupem, Lidé, které zvolíte. Volba „Kdokoli" tam **není**. Dále je tam *Může upravit / Může zobrazit* a datum ukončení platnosti.
- Nastavení tenantu (Zásady → Sdílení): externí sdílení SharePointu i OneDrivu je podle posuvníků na nejvolnější úrovni **Všichni**, výchozí typ odkazu je **Kdokoliv, kdo má odkaz**, výchozí oprávnění odkazu **Upravit**, platnost odkazů není omezena. Je to běžné výchozí nastavení nového tenantu.
- Proč dialog u souboru „Kdokoli" nenabízí, není ověřeno. Pravděpodobně je sdílení na webu přísnější než na tenantu. Zkontrolovat v Aktivní weby → Test intranet → Nastavení → Externí sdílení.
- Nastavení tenantu jsem zatím **nezměnil**.

### Doporučené nastavení pro nadaci
1. Externí sdílení: posuvník na **Existující hosté** nebo **Jenom lidé ve vaší organizaci**; hosty přidávat až při potřebě.
2. Výchozí typ odkazu: **Konkrétní lidé**.
3. Výchozí oprávnění odkazu: **Zobrazovat**.
4. Pokud by zůstalo veřejné sdílení, zapnout platnost odkazů (např. 30 dní) a u souborů nechat jen zobrazení.
5. Na citlivých webech (Vedení, osobní údaje) povolit sdílení **jen vlastníkům**.
6. Pro externí spolupráci zvát hosty s vypršením platnosti (např. 90 dní), ne rozesílat veřejné odkazy.
7. Pravidelně procházet *Spravovat přístup* u sdílených souborů a webů.
8. Při zpřísnění nastavení v reálném tenantu nejdřív zjistit, kdo stávající veřejné odkazy používá, protože po změně přestanou fungovat.

Při sdílení souboru jde vždy o tři otázky: komu (organizaci, existujícím, jmenovaným), s jakou úrovní (zobrazit, upravit) a na jak dlouho (datum ukončení). Nejbezpečnější je *Lidé, které zvolíte* s datem ukončení.

## Účty a role
- Na běžnou práci osobní účet bez správcovských práv.
- Na správu samostatný správcovský účet nebo konkrétní role (SharePoint správce, Správce uživatelů), ne Globální správce.
- Globálních správců málo (2 až 4) a navíc nouzový účet (break-glass) uložený v trezoru.
- Funkční adresa typu koordinátor jako sdílená schránka, ne sdílený účet s heslem.

## Na co si dát pozor
- Práva dávat skupinám, ne jednotlivcům.
- Po přerušení dědění zůstanou všichni původní lidé a změny na webu se už do knihovny nepřenášejí.
- Výjimky se časem ztrácejí z přehledu. U citlivého obsahu je čistší samostatný web než knihovna nebo složka s výjimkou.
- Sdílení odkazem je také oprávnění a může obejít strukturu.
- Odkaz *Odstranit: Knihovna dokumentů* v nastavení knihovny knihovnu maže.
- *Zkontrolovat oprávnění* ukáže nejen úroveň, ale i odkud ji uživatel má.
- Úroveň Úpravy dovoluje i mazání knihoven; pro běžné kolegy zvážit Přispívat.
- Výchozí nastavení sdílení nového tenantu je příliš volné.

## Dále
- Dokončit ověření: Karel ve více skupinách, úroveň Přispívat, karty Lidé a Odkazy u souboru, nastavení sdílení na webu.
- Případně zpřísnit sdílení v tenantu a výsledek doplnit.
- Druhý web pro srovnání (jen Vedení) a hub.
- Týden 3: Microsoft Lists a Power Automate.

*Screenshoty doplnit až po začernění jména, názvu tenantu a e-mailů (název tenantu se v dialogu sdílení zobrazuje jako název organizace).*
