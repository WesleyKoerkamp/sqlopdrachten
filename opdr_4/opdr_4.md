# Sql basis

### Database 
Maak gebruik van het sql-bestand reisbureau.sql en voer hierop onderstaande opdrachten uit.
Theorie kun je vinden op: https://www.edutorial.nl/dbq/introductie/

### Queries reisbureau
* Geef de namen van de klanten die in Rotterdam wonen
# SELECT * FROM `klanten` WHERE Plaats = 'Rotterdam'
# SELECT Naam, Plaats FROM `klanten` WHERE Plaats = 'Rotterdam'

* Geef de namen van de klanten die geen reis geboekt hebben.
# SELECT klanten.naam  FROM klanten LEFT JOIN boekingen ON klanten.klantnummer = boekingen.klantnummer WHERE boekingen.klantnummer is NULL

* Hoeveel klanten komen er niet uit Rotterdam
# SELECT count(*) as aantal_klanten from `klanten`  WHERE plaats <> 'rotterdam'

* Hoeveel reizen hebben als bestemming Afrika?
# SELECT count(*) AS aantalreizen FROM reizen JOIN bestemmingen ON reizen.Bestemmingcode = bestemmingen.Bestemmingcode WHERE Werelddeel = 'Afrika'

* Hoeveel moeten de klanten, die naar Azië gaan, in totaal betalen?


* Geef de namen van de klanten die met kinderen op reis gaan.


* Hoeveel verschillende reizen kun je boeken bij dit reisbureau?
# SELECT COUNT(*) AS aantal_reizen FROM bestemmingen

* Geef de naam en postcode van de klanten die in een postcode gebied wonen dat begint met een 9.
# SELECT naam, postcode FROM klanten WHERE postcode LIKE '9%'

* Groepeer de klanten op woonplaats. Geef de woonplaats en het aantal klanten per woonplaats.
# SELECT Plaats, COUNT(*) AS aantal_klanten FROM klanten GROUP BY Plaats;

* Geef naam en datum van de klanten die voor de maand April een reis hebbben geboekt.


* Geef de namen van klanten, het werelddeel van de bestemming en het aantal dagen van de reis voor boekingen van minimaal 15 dagen.
