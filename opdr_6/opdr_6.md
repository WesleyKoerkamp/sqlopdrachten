# Sql basis

### Database gegevens aanpassen
Maak gebruik van het sql-bestand idscan.sql en voer hierop onderstaande opdrachten uit.
Theorie kun je vinden op: https://www.edutorial.nl/dbq/introductie/

### Queries winkelketen
* Welke medewerkers (id, voornaam, achternaam)zijn er in dienst van de winkelketen.
# SELECT id, firstname AS voornaam, lastname AS achternaam
# FROM persons;

* Hoeveel medewerkers hebben dezelfde functie (jobtitle)
# SELECT jobtitle, COUNT(*) AS aantal
# FROM persons
# GROUP BY jobtitle
# ORDER BY aantal DESC;

* Hoeveel medewerkers zijn professor of ingenieur (title = prof, ir of ing)
# SELECT COUNT(*) AS aantal
# FROM persons
# WHERE title IN ('prof.', 'prof', 'ir.', 'ir', 'ing.', 'ing');

* Overzicht van medewerkers (id, voornaam, tussenvoegsel, achternaam) per gebouw (buildingname, street en buildingnumber)
# SELECT DISTINCT b.buildingname, b.street, b.buildingnumber, p.id, p.firstname, p.title, p.lastname
# FROM scans s
# JOIN persons p ON p.id = s.person_id
# JOIN buildings b ON b.id = s.building_id
# ORDER BY b.buildingname, p.lastname;

* Overzicht van medewerkers (id, voornaam, tussenvoegsel, achternaam) die op een *  * bepaalde datum in gebouw met id 1 waren (buildingname, 
# SELECT DISTINCT  p.id, p.firstname, p.title, p.lastname, b.buildingname, b.street, b.buildingnumber
# FROM scans s
# JOIN persons p ON p.id = s.person_id
# JOIN buildings b ON b.id = s.building_id
# WHERE s.scandate = '2023-09-13'
#  AND s.building_id = 1;

* Overzicht van medewerkers die op diezelfde datum vergeten zijn om uit te checken
# SELECT DISTINCT p.id, p.firstname, p.title, p.lastname
# FROM scans s_in
# JOIN persons p ON p.id = s_in.person_id
# LEFT JOIN scans s_out
#  ON s_out.person_id = s_in.person_id
#  AND s_out.scandate = s_in.scandate
#  AND s_out.building_id = s_in.building_id
#  AND s_out.in_out = 'out'
# WHERE s_in.scandate = '2023-09-13'
#  AND s_in.building_id = 1
#  AND s_in.in_out = 'in'
#  AND s_out.id IS NULL;

* Overzicht van het aantal medewerker per gebouw op 13 september 2023.
# SELECT b.buildingname, b.street, b.buildingnumber,
# COUNT(DISTINCT s.person_id) AS aantal_medewerkers
# FROM scans s
# JOIN buildings b ON b.id = s.building_id
# WHERE s.scandate = '2023-09-13'
# GROUP BY b.id, b.buildingname, b.street, b.buildingnumber
# ORDER BY aantal_medewerkers DESC;

* Overzicht van medewerkers en het aantal uur dat ze op 15 september 2023 hebben gewerkt.
# SELECT p.id, p.firstname, p.title, p.lastname,
#  SEC_TO_TIME(SUM(TIME_TO_SEC(TIMEDIFF(s_out.scantime, s_in.scantime)))) AS uren_gewerkt
# FROM scans s_in
# JOIN scans s_out
#  ON s_out.person_id = s_in.person_id
#  AND s_out.scandate = s_in.scandate
#  AND s_out.in_out = 'out'
#  AND s_out.scantime > s_in.scantime
#  AND s_out.building_id = s_in.building_id
# JOIN persons p ON p.id = s_in.person_id
# WHERE s_in.scandate = '2023-09-15'
#  AND s_in.in_out = 'in'
# GROUP BY p.id, p.firstname, p.title, p.lastname
# ORDER BY uren_gewerkt DESC;

* Medewerker van de maand! (De medewerker die het meeste uren heeft gemaakt van iedereen in de maand september)
# SELECT p.id, p.firstname, p.title, p.lastname,
#  SUM(TIME_TO_SEC(TIMEDIFF(s_out.scantime, s_in.scantime))) / 3600 AS uren_gewerkt
# FROM scans s_in
# JOIN scans s_out
#  ON s_out.person_id = s_in.person_id
#  AND s_out.scandate = s_in.scandate
#  AND s_out.in_out = 'out'
#  AND s_out.scantime > s_in.scantime
#  AND s_out.building_id = s_in.building_id
# JOIN persons p ON p.id = s_in.person_id
# WHERE s_in.scandate BETWEEN '2023-09-01' AND '2023-09-30'
#  AND s_in.in_out = 'in'
# GROUP BY p.id, p.firstname, p.title, p.lastname
# ORDER BY uren_gewerkt DESC
# LIMIT 1;