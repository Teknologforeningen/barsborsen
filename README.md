# Bärsbörsen

Vision projektet skapades hösten 2019 för TF:s fundraising för campusprojektet.
Den uppdaterades under 2021 och början av 2021 för att lägga till stöd för onlinebetalningar.
Senare flyttades frontenden
till [hemsidan](https://github.com/Teknologforeningen/tf.fi/commit/c7bd74616ca40047054e1f70fda22c6faa041ee2).
Då frontenden flyttades så döptes detta projekt om.

## Funktionalitet TL;DR

- Donering med kort-, bank- och mobilbetalningar via Paytrail
- Virtuell donatorvägg

## Lokal utvecklingsmiljö

### Backenden

1. Installera en lokal PostgreSQL instans, antingen nativt på datorn eller som en container och ha igång den när du
   utvecklar. Skapa en role i databasen som heter `django`.
1. För att Paytrail ska fungera, måste du lägga till i din `/etc/hosts` följande info `127.0.0.1 donationdb.local`.
1. I backend-mappen, kör `pip install -r requirements.txt` för att installera alla dependencies.
1. Kör `python manage.py migrate` för att skapa alla lokala databastables.
1. Kör `python manage.py createsuperuser` för att skapa en superuser som kan logga in.
1. Kör `python manage.py runserver 3000` för att köra servern.

## Testing

Det finns ett (fåtal) test för backenden.
De körs med `python manage.py test` lokalt på ens egna dator.
