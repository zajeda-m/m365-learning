# Týden 1: uživatelé, licence a skupiny (zkušební tenant M365)

Studijní poznámky z vlastního zkušebního tenantu Microsoft 365 Business Basic.
Všechna jména jsou smyšlená, screenshoty jsou bez osobních údajů.

## Co jsem udělal
- Nastavil vícefaktorové ověření (Microsoft Authenticator) pro správcovský účet.
- Vypnul automatickou obnovu předplatného (volba "Zrušit při vypršení platnosti"), aby zkouška skončila bez poplatku.
- Vytvořil tři testovací uživatele s rolemi vedoucí, koordinátor a kolega a přiřadil jim licenci Business Basic.
- Vytvořil dvě skupiny zabezpečení: Vedení a Tým. Přidal členy a nastavil vlastníka.

## Skupina zabezpečení vs. skupina Microsoft 365
| | Skupina zabezpečení | Skupina Microsoft 365 |
|---|---|---|
| Účel | přidělování přístupů a oprávnění | spolupráce týmu |
| Vlastní schránka a kalendář | ne | ano |
| Vlastní úložiště a web | ne | ano (SharePoint, případně Teams) |
| Kdy použít | oprávnění do knihoven a aplikací | sdílená práce a komunikace |

Pro oprávnění ve SharePointu budu používat skupiny zabezpečení.

## Proč oprávnění po skupinách, ne po lidech
- Při nástupu stačí přidat člověka do skupiny, při odchodu ho odebrat.
- Přehled "kdo má k čemu přístup" je čitelný v jednom místě.
- Méně chyb než ruční nastavování oprávnění každému zvlášť.

## Na co si dát pozor
- U skupin Microsoft 365 je ochrana osobních údajů veřejná nebo soukromá; veřejná skupina je dostupná všem v organizaci.
- Systémové skupiny (např. Viva Engage) nemazat.
- Skupina bez vlastníka je rizikem, proto vždy určit alespoň jednoho vlastníka.

## Co dál
- Ověřit v záložce Role, že testovací uživatelé nemají přístup správce.
- Projít v Entra ID nastavení výchozího zabezpečení a přihlášení.
- Týden 2: SharePoint web a oprávnění přes tyto skupiny.
