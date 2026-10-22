# Týden 1: uživatelé, licence, skupiny a role správců

Studijní poznámky z vlastního zkušebního tenantu Microsoft 365 Business Basic.
Všechna jména jsou smyšlená, screenshoty jsou bez osobních údajů.

## Co jsem udělal
1. Nastavil vícefaktorové ověření (Microsoft Authenticator) pro správcovský účet.
2. Vypnul automatickou obnovu předplatného (volba "Zrušit při vypršení platnosti"), aby zkouška skončila bez poplatku.
3. Vytvořil tři testovací uživatele s rolemi vedoucí, koordinátor a kolega a přiřadil jim licenci Business Basic.
4. Vytvořil dvě skupiny zabezpečení: Vedení a Tým. Přidal členy a nastavil vlastníka.
5. Prošel role správců a ověřil, že testovací uživatelé mají "Bez přístupu správce".

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
- Výchozí zabezpečení (Security defaults) je pro malý nebo zkušební tenant nejjednodušší základ. Jeho stav v Entra ID teprve ověřím.

## Na co si dát pozor
- U skupin Microsoft 365 je ochrana osobních údajů veřejná nebo soukromá; veřejná skupina je dostupná všem v organizaci.
- Při změnách rolí nic neukládat, dokud nevím, co se změní. Panel lze zavřít bez uložení.
- Zkušební verze skončí a data tenantu se smažou. Poznámky proto ukládám sem.

## Co dál
- Projít Entra ID: přehled tenantu, výchozí zabezpečení, přihlašování.
- Týden 2: SharePoint web, knihovny a oprávnění přes skupiny Vedení a Tým.
- Zkusit přiřadit testovacímu uživateli omezenou roli (např. Správce SharePointu) a porovnat, co uvidí.
