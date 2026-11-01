# Týden 3: SharePoint seznam Žádosti (sloupce, pohledy, verze, koš)

Stav k 31. 10. 2026 (po bloku 3). Všechna jména a data jsou smyšlená.

## Kdy seznam, kdy knihovna, kdy Forms
- Knihovna dokumentů: soubory (smlouva, přihláška v PDF), metadata jsou sloupce u souboru.
- Seznam: záznamy bez souboru, řádek v tabulce (žádost, úkol, kontakt). Aplikace Lists je jen jiné rozhraní týchž seznamů.
- Forms: vstupní formulář, odpovědi lze ukládat do seznamu.

## Hotovo (ověřeno v tenantu)
- Na webu Test intranet vytvořen prázdný seznam Žádosti, objevil se v horní navigaci.
- V českém rozhraní se výchozí sloupec jmenuje Nadpis.
- Sloupce: Program (volba: Program A, B, C), Stav (volba: Nová, V hodnocení, Podpořeno, Zamítnuto, Uzavřeno; od 31. 10. 2026, dříve Rozhodnuto), Uzávěrka (datum), Zpracovatel (osoba), Částka (měna, Kč).
- Čtyři testovací položky; jedna s uzávěrkou v minulosti, jedna bez zpracovatele.

## Ověřeno jako Karel (31. 10. 2026, úroveň Čtení, skupina Tým)
- Web Test intranet najde přes plné hledání (lupa); v našeptávači pod polem se neobjevil, protože ho Karel dosud neotevřel. Po přidání do oblíbených je v seznamu webů.
- Aplikace Microsoft Lists ukazuje tentýž seznam Žádosti (popisek Test intranet), stejné sloupce a čtyři položky.
- Karel nemá tlačítko Nový ani Forms. Po výběru položky nabídne jen Komentář, tlačítko Smazat chybí.
- Moje žádosti ukáže jen Žádost č. 1; Všechny položky ukáže všech 4. Pohled omezuje zobrazení, ne oprávnění.
- Řazení podle Uzávěrky (od nejstarší) se uložilo do pohledu.
- Pozn.: správce neměl v Moje žádosti nic, protože mu nebyla přiřazená žádná žádost.

## Ověřeno jako správce (31. 10. 2026): verzování, koš a obnova
- Verzování seznamu: u seznamu bylo zapnuté od vytvoření (nová verze při každé úpravě, zachovat 50 verzí). Schvalování obsahu je vypnuté, proto jsou volby konceptů neaktivní. Verze (každá úprava) a koncepty (čekají na schválení) jsou dvě různé věci.
- Historie verzí: u položky `…` → Historie verzí. Každá změna Stavu vytvořila novou verzi (1.0 vytvoření, 2.0 a 3.0 dvě změny Stavu) s datem, autorem a změněným sloupcem.
- Obnovení starší verze: správce obnovil verzi 1.0, vznikla nová verze 4.0, předchozí verze zůstaly. Uživatel s úrovní Čtení historii vidí, ale obnovit nemůže (chyba přístupu).
- Smazání položky a obnova: smazaná položka je v Koši webu (Obsah webu → Koš) s názvem, kdo ji smazal a vytvořil a původním umístěním. Po obnově se vrátila se všemi hodnotami.
- Smazání seznamu a obnova: celý seznam (kopie Žádostí, 5 položek) se smazal do Koše webu a po obnově se vrátily položky, pohledy i nastavení verzování. Nevrátil se odkaz v horní navigaci webu. Vrátí se v Nastavení seznamu → Název, popis a navigace → Zobrazit na rychlém spuštění: Ano (ověřeno); jinak ručně přes Navigace → Upravit → + → Odkaz.
- Doba uchování: smazané položky se drží celkem 93 dní od smazání (nejdřív koš webu, pak koš správce kolekce webů), podle Microsoft Support.
- Seznam z existujícího seznamu: přenese sloupce i pohledy, ne položky. Položky jdou zkopírovat v zobrazení mřížky, když se označí buňky (ne řádky zaškrtávátkem).
- Adresa seznamu: tvoří se z názvu při vytvoření a diakritika se vynechá (Žádosti → /Lists/dosti). Nejde ji změnit, ani přejmenováním. Seznam zakládat s názvem bez diakritiky a pak ho přejmenovat.
- Časové pásmo webu: čas v koši a v historii verzí se může lišit, pokud má web nastavené jiné pásmo než uživatel (Nastavení webu → Místní nastavení).

## Proč zakládat název bez diakritiky a pomlček a pak ho přejmenovat?
Krátká odpověď: není to povinné, je to prevence. SharePoint si při vytvoření seznamu nebo sloupce zapamatuje interní název (u seznamu je součástí adresy) a ten se už nezmění, přejmenuje se jen zobrazovaný název.
- Seznam: adresa se tvoří z názvu při vytvoření a znaky mimo základní abecedu se vynechají. Ověřeno v tenantu: Žádosti → /Lists/dosti. Adresu nelze změnit ani přejmenováním.
- Sloupec: interní název se také tvoří při vytvoření. OVĚŘENO v tenantu (31. 10. 2026) na testovacím sloupci „ěščdasdfasdfaf…“: diakritika se zakóduje jako _xHHHH_ (ě = _x011b_, š = _x0161_, č = _x010d_), každý takový znak zabere 7 znaků, a interní název se ořízne na 32 znaků (z názvu zmizel konec). Pomlčka se zakóduje také (_x002d_), ověřeno na sloupci „Kontaktní - osoba“ (za í je _x00ed_, za ním _x002d_). Název zadaný bez diakritiky „Kontaktni osoba“ dal čistý interní název Kontaktniosoba (mezera se vynechala). Důvod pro postup: založit bez diakritiky a pomlček a pak přejmenovat. Kde to vidět: Nastavení seznamu → sekce Sloupce → klik na název sloupce → v adrese za Field= je interní název (%5F je podtržítko).
- Běžný uživatel rozdíl nepozná, v pohledech a formulářích vidí zobrazovaný název.
- Vadí to tam, kde se pracuje s interním názvem: odkazy a filtry v adrese, PowerShell, Power Apps, formátování sloupců v JSON, REST a Graph API, import a export. Tok v Power Automate ukazuje zobrazované názvy, takže u běžného toku to nevadí.
- Postup: založit s názvem bez diakritiky, mezer a pomlček a po uložení přejmenovat na hezký. Vzniklé chyby jdou opravit jen vytvořením nového seznamu nebo sloupce.
- V organizaci: pravidlo pojmenování seznamů, knihoven a sloupců patří do zásad správy (kdo zakládá, jaké názvy).
