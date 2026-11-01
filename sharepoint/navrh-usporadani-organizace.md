# Návrh uspořádání SharePointu pro menší organizaci

Stav: koncept. Je to návrh a teorie, ne zkušenost z provozu. U každé části je uvedeno, zda je ověřeno ve zkušebním tenantu.

Poznámka je záměrně obecná: bez názvu organizace, bez jmen lidí a bez odkazů na soukromé dokumenty.

## Zadání
Menší nezisková organizace se třemi skupinami činnosti (programy a granty, dárci a fundraising, provoz a řízení), asi desítkami zaměstnanců a externími lidmi v radách. Cíl: přehledné weby, jasná oprávnění, malé kroky.

## Struktura
- Jeden hub a asi deset webů: programové weby, Granty, Dárci a fundraising, Finance, Vedení, Rady, Kancelář a IT.
- Weby s citlivými daty (Granty, Dárci a fundraising, Finance, Rady) mají přísnější oprávnění.
- Programy nejsou samostatné weby, ale hodnota ve sloupci. Pro každý program jen uložený pohled.
- Údaje o dárcích patří do CRM, ne do SharePointu.

## Oprávnění
- Jen přes skupiny zabezpečení podle oddělení, nikdy jednotlivcům.
- Člověk ve více skupinách: oprávnění se sčítají a platí nejvyšší. Omezit znamená vyndat ho z širší skupiny. Čtvrtletní kontrola skupin. Stav: teorie, nevyzkoušeno v tenantu.
- Mazání: položku smí smazat úroveň Přispívat, celý seznam úroveň Úpravy a výš. Smazané jde do koše na zhruba tři měsíce. Verzování chrání před přepsáním, ne před smazáním, proto nezávislá záloha. Stav: teorie, nevyzkoušeno.
- Externí lidé (rada, partneři) jsou hosté, jen čtení, s datem vypršení a jen na jednom webu nebo v jedné knihovně. Ověřeno: nastavení sdílení a hostů v tenantu (výchozí je příliš volné).

## Seznamy, sloupce a pohledy (teorie)
- Seznam je tabulka: řádek je položka, sloupec je vlastnost s pevným typem (text, volba, datum, osoba, částka). Aplikace Lists je jen jiné rozhraní týchž seznamů. Seznam není soubor, ale jde ho vyexportovat do Excelu.
- Pohled je uložené nastavení, co člověk vidí (sloupce, filtr, řazení). Nezamyká přístup, k tomu slouží oprávnění.
- Příklad: seznam Žádosti o grant se sloupci Program, Typ podpory, Žadatel, Uzávěrka, Stav, Částka a Osoba; pohledy Všechny žádosti, Moje žádosti, Čeká na rozhodnutí, Podle programů.

## Grantový proces
Vstupní dotazník, konzultace, přihláška, hodnoticí komise, rozhodnutí, smlouva, realizace, závěrečná zpráva, uzavřeno. Stav je sloupec, ne složka. Automatizace v Power Automate (plán, nevyzkoušeno): nová položka, změna stavu na rozhodnutí, upomínka termínu závěrečné zprávy.

## Zavedení
1. Inventura stávajícího stavu.
2. Dohoda priorit a vlastníků.
3. Skupiny a názvosloví.
4. Pilot na jednom programu.
5. Vyhodnocení s uživateli.
6. Postupný přesun po programech.
7. Uzavřené weby až po potvrzení oprávnění.
8. Návody a krátké školení.
9. Čtvrtletní kontrola oprávnění a roční zkouška obnovy.

## Co ještě ověřit v tenantu
- [ ] Člověk ve více skupinách: přidat, ověřit, odebrat, ověřit návrat.
- [ ] Úroveň Přispívat a že nemůže smazat seznam.
- [ ] Seznam Žádosti, pět sloupců, čtyři pohledy.
- [ ] Verzování seznamu, smazání položky a obnova z koše.
- [ ] První tok v Power Automate nad seznamem.
