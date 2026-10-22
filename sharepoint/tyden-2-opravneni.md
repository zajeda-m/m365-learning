# Týden 2: SharePoint a oprávnění podle rolí

Zkušební tenant Microsoft 365 Business Basic, 22. 10. 2026. Všechna jména jsou smyšlená.

## Cíl
Pochopit, jak se ve SharePointu Online přiřazují práva k webům, knihovnám a složkám, a ověřit to v praxi na testovacích uživatelích.

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

## Dále
- Druhý web pro srovnání (jen Vedení) a hub.
- Týden 3: Microsoft Lists a Power Automate.

*Screenshoty doplnit až po začernění jména, názvu tenantu a e-mailů.*
