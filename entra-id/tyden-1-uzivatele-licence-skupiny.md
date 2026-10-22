# Týden 1: uživatelé, licence, skupiny a role správců

Studijní poznámky z vlastního zkušebního tenantu Microsoft 365 Business Basic.
Všechna jména jsou smyšlená, screenshoty jsou bez osobních údajů.

## Co jsem udělal
1. Nastavil vícefaktorové ověření (Microsoft Authenticator) pro správcovský účet.
2. Vypnul automatickou obnovu předplatného (volba "Zrušit při vypršení platnosti"), aby zkouška skončila bez poplatku.
3. Vytvořil tři testovací uživatele s rolemi vedoucí, koordinátor a kolega a přiřadil jim licenci Business Basic.
4. Vytvořil dvě skupiny zabezpečení: Vedení a Tým. Přidal členy a nastavil vlastníka.
5. Prošel role správců a ověřil, že testovací uživatelé mají "Bez přístupu správce".
6. Prošel přehled tenantu v Entra ID a ověřil, že je zapnuté výchozí zabezpečení (Security defaults).
7. Prošel protokol přihlášení svého účtu a našel v něm záznam o splněném vícefaktorovém ověření.

## Uživatelé a licence
- Uživatelé se vytvářejí v admin centru: Users, Active users, Add a user.
- Při vytváření se přiřazuje licence (zde Business Basic). Bez licence uživatel nemá přístup ke službám.
- Hesla se generují automaticky a ukládají do správce hesel, nikdy se neposílají v chatu ani e-mailem.
- Uživatelské jméno má tvar jmeno.prijmeni@nazevtenantu.onmicrosoft.com.

## Skupina zabezpečení vs. skupina Microsoft 365
| | Skupina zabezpečení | Skupina Microsoft 365 |
|---|---|---|
| Účel | přidělování přístupů a oprávnění | spolupráce týmu |
| Vlastní schránka a kalendář | ne | ano |
| Vlastní úložiště a web | ne | ano (SharePoint, případně Teams) |
| Kdy použít | oprávnění do knihoven a aplikací | sdílená práce a komunikace |

- Pro oprávnění ve SharePointu budu používat skupiny zabezpečení.
- Některé skupiny vznikají automaticky (All Company, skupina vytvořená při nastavení, systémová skupina Viva Engage). Systémové skupiny se nemažou.
- Průvodce vytvořením skupiny zabezpečení nemá krok pro členy a vlastníky, ti se přidávají až v detailu skupiny.

## Přehled tenantu v Entra ID
Centrum pro správu Microsoft Entra (entra.microsoft.com), sekce Entra ID, Přehled.

- **Počty:** 4 uživatelé, 5 skupin, 0 zařízení, 0 aplikací.
- **Plán:** Entra Free. Stačí na uživatele, skupiny, MFA a výchozí zabezpečení. Podmíněný přístup a dynamické skupiny vyžadují placenou verzi (P1).
- **Entra Connect: zakázáno.** Entra Connect synchronizuje účty z lokálního Active Directory. Můj tenant je **cloud-only**, takže je to správně. Opakem je hybridní prostředí.
- **Skóre zabezpečení identity:** u nového tenantu zatím není k dispozici, objeví se po několika dnech provozu.
- **Moje role:** Globální správce (jediná přiřazená role).

### Jak se dělí skupiny
| Hledisko | Možnosti | Můj tenant |
|---|---|---|
| Typ | M365 (spolupráce) vs. zabezpečení (oprávnění) | 3 M365, 2 zabezpečení |
| Členství | přiřazené ručně vs. dynamické (pravidlem) | všechny přiřazené, 0 dynamických |
| Původ | cloudové vs. místní (z lokálního AD) | 5 cloudových, 0 místních |

### Užitečné části menu Entra ID
- **Role a správci:** přehled rolí a kdo je má.
- **Metody ověřování:** které metody MFA jsou povolené.
- **Resetování hesla:** samoobslužný reset hesla.
- **Protokoly auditu:** záznam změn (kdo vytvořil nebo smazal uživatele či skupinu).
- **Přihlášení uživatele:** protokol přihlášení.
- **Zásady pojmenovávání a konec platnosti skupin:** nastavení v sekci Skupiny.

## Proč oprávnění po skupinách, ne po lidech
- Při nástupu stačí přidat člověka do skupiny, při odchodu ho odebrat.
- Přehled "kdo má k čemu přístup" je čitelný v jednom místě.
- Méně chyb než ruční nastavování oprávnění každému zvlášť.
- Skupina bez vlastníka je rizikem, proto vždy určit alespoň jednoho vlastníka.

## Role správců
Princip, který Microsoft zdůrazňuje přímo v admin centru: přidělovat **nejnižší možnou úroveň oprávnění**.

V detailu uživatele jsou dvě základní volby:
- **Uživatel** bez přístupu do centra pro správu (výchozí).
- **Přístup k Centru pro správu** s konkrétní rolí.

| Role | Co smí |
|---|---|
| Globální správce | neomezená oprávnění ke všemu |
| Globální čtenář | vidí vše, nic nemění |
| Správce SharePointu | jen SharePoint |
| Správce Teams | jen Teams |
| Správce Exchange | jen e-mail a schránky |
| Správce uživatelů | účty a hesla |
| Správce podpory služeb | zakládá požadavky u Microsoftu |

Pro běžnou práci (SharePoint, Power Platform, koordinace) není potřeba globální správce, stačí specializovaná role. Globálních správců má být co nejméně a každý musí mít vícefaktorové ověření.

## Vícefaktorové ověření a výchozí zabezpečení
- MFA přes Microsoft Authenticator je nastavené pro správcovský účet.
- Doporučuje se druhá metoda ověření (např. telefonní číslo) pro případ ztráty telefonu.
- Výchozí zabezpečení (Security defaults) je pro malý nebo zkušební tenant nejjednodušší základ. U mého tenantu je zapnuté (Entra ID, Přehled, Vlastnosti, Spravovat výchozí nastavení zabezpečení). Vyžaduje MFA pro všechny uživatele a blokuje starší způsoby přihlášení.

## Na co si dát pozor
- U skupin Microsoft 365 je ochrana osobních údajů veřejná nebo soukromá; veřejná skupina je dostupná všem v organizaci.
- Při změnách rolí nic neukládat, dokud nevím, co se změní. Panel lze zavřít bez uložení.
- Zkušební verze skončí a data tenantu se smažou. Poznámky proto ukládám sem.

## Co dál
- Projít protokol přihlášení (Entra ID, Přihlášení uživatele) a zapsat, co ukazuje.
- Týden 2: SharePoint web, knihovny a oprávnění přes skupiny Vedení a Tým.
- Zkusit přiřadit testovacímu uživateli omezenou roli (např. Správce SharePointu) a porovnat, co uvidí.
