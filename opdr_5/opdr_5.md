# Sql basis

### Database
Maak gebruik van het sql-bestand flits.sql en voer hierop onderstaande opdrachten uit.
Theorie kun je vinden op: https://www.edutorial.nl/dbq/introductie/

### Queries flitspaal
* Welke cameras zijn er en waar staan ze (id, address, city, max_speed).
# SELECT id, address, city, max_speed FROM `cameras` WHERE 1

* Overzicht van boetes op 50km wegen
# SELECT * FROM `cameras` 
# JOIN fines
# ON cameras.id = fines.id
# WHERE speed_limit = 50;

* Overzicht van overtredingen van 1 kenteken.
# SELECT * FROM flashes
# JOIN licenses
# WHERE flashes.license = 'CR-52-52'

* N.a.w.-gegevens van de hardrijders die het meest in de fout zijn gegaan. (top 10)
# SELECT count(*) AS aantal, licenses.license, licenses.first_name, licenses.address, licenses.city FROM flashes
# JOIN licenses
# ON licenses.license = flashes.license
# GROUP BY flashes.license
# ORDER BY aantal DESC
# LIMIT 10

* Welke camera’s (id, address, city) meten de meeste snelheidsovertredingen (top 10)
# SELECT count(*) AS aantalcameras, cameras.id, cameras.city, cameras.address FROM `flashes` 
# JOIN cameras 
# ON cameras.id = flashes.camera_id
# GROUP BY flashes.camera_id
# ORDER BY aantalcameras DESC
# LIMIT 10;

* Welke auto’s (kenteken, merk, type) zijn het meeste geflitst


* Welke flitspaal (=camera met id, address, city) flitst het meest (top 10)
# SELECT count(*) AS aantalcameras, cameras.id, cameras.city, cameras.address FROM `flashes` 
# JOIN cameras 
# ON cameras.id = flashes.camera_id
# GROUP BY flashes.camera_id
# ORDER BY aantalcameras DESC
# LIMIT 10;

* Kentekens van auto’s die het hoogste bedrag aan boetes hebben gekregen (top 10)
# SELECT
#  license AS kenteken,
#  COUNT(*) AS aantal_flitsen
# FROM flashes
# GROUP BY license
# ORDER BY aantal_flitsen DESC
# LIMIT 10;

* Overzicht van auto’s (kenteken, merk, type) waarvan het kenteken overeenkomt met sitecode 10 (zoals X-999-XX) https://nl.wikipedia.org/wiki/Nederlands_kenteken.
# SELECT
# f.license AS kenteken,
#  COUNT(*) AS aantal_flitsen,
#  SUM(fi.fine) AS totaal_bedrag
# FROM flashes f
# JOIN cameras c
#  ON c.id = f.camera_id
# JOIN fines fi
#  ON fi.speed_limit = c.max_speed
# AND fi.speed_excess = f.speed - c.max_speed
# GROUP BY f.license
# ORDER BY totaal_bedrag DESC
# LIMIT 10;