# Sql basis

### Database gegevens aanpassen
Maak gebruik van het sql-bestand reisbureau.sql en voer hierop onderstaande opdrachten uit.
Theorie kun je vinden op: https://www.edutorial.nl/dbq/introductie/

### Opdracht 1
* Geef de query om alle tabellen in de database 'reisbureau' weer te gegeven

# SHOW TABLES FROM reisbureau

### Opdracht 2
* Voeg 2 nieuwe klanten toe aan de tabel 'customers' (je mag de waarden zelf bedenken)

### KLANT 1:
# INSERT INTO `customers` (`id`, `first_name`, `last_name`, `email`, `address`, `postal_code`, `city`, `country_code`, `phone`, `created_at`, `updated_at`) VALUES (NULL, 'Wesley', 'Koerkamp', 'wesley@koerkamp.nl', 'Straatnaam', '0000XX', 'Deventer', 'nl_NL', '+31 6 12345678', NULL, NULL);

### KLANT 2:
# INSERT INTO `customers` (`id`, `first_name`, `last_name`, `email`, `address`, `postal_code`, `city`, `country_code`, `phone`, `created_at`, `updated_at`) VALUES (NULL, 'Jaimy', 'Koerkamp', 'wesley@koerkamp.nl', 'Straatnaam', '0000XX', 'Deventer', 'nl_NL', '+31 6 12345678', NULL, NULL);

### Opdracht 3
* Geef de query om de eerste 10 boekingen te verwijderen (reservations)
# DELETE FROM reservations ORDER BY id LIMIT 10;

### Opdracht 4
* De klant met id 13 is verhuist naar 'De van der veldensteeg 81' in 'Apeldoorn'.
* Pas het record aan en geef de query
* Toon het record en controleer of de gegevens correct zijn.
# UPDATE `customers` SET `address` = 'Van der Veldensteeg 81', `city` = 'Apeldoorn', `updated_at` = NULL WHERE `customers`.`id` = 13