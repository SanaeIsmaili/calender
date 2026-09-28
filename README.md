# Gezond het Jaar Rond — website

Eén zelfstandig HTML-bestand (`index.html`) met de volledige website: hero, probleem en oplossing (met foto's), doelgroepen, bronnen, het verhaal van Jop en Jamie (met foto's), missie/visie, voorbeeldmaanden, bestelformulier, contact, en de juridische teksten (privacyverklaring + algemene voorwaarden). Die staan niet op de homepage zelf, maar openen als aparte weergave via de links "Voorwaarden" en "Privacy" in de header (of rechtstreeks via `#privacy` en `#voorwaarden` achter de url). Alle afbeeldingen zitten ingesloten in het bestand.

## Op GitHub / GitHub Pages zetten

1. Maak een nieuwe (lege) repository aan op GitHub, bijvoorbeeld `gezond-het-jaar-rond`.
2. Upload `index.html` naar de root van die repository (via "Add file" → "Upload files" in de GitHub-website, of via git).
3. Ga naar **Settings → Pages** in je repository.
4. Kies bij "Source" de branch `main` en map `/ (root)`, klik op **Save**.
5. Na een paar minuten is je site live op `https://<jouw-gebruikersnaam>.github.io/gezond-het-jaar-rond/`.

Wil je een eigen domeinnaam (bijvoorbeeld gezondhetjaarrond.nl)? Voeg dan een `CNAME`-bestand toe met daarin je domeinnaam, en stel bij je domeinregistrar een CNAME-record in dat verwijst naar `<jouw-gebruikersnaam>.github.io`. GitHub's eigen documentatie ("Managing a custom domain for your GitHub Pages site") beschrijft dit stap voor stap.

## Voordat je live gaat: nog in te vullen

Zoek in `index.html` naar de volgende plekken en vul ze aan:

- **Bedrijfsgegevens**: in de footer en in de privacyverklaring/algemene voorwaarden staan plekken gemarkeerd als `[bedrijfsnaam]`, `[KVK-nummer]`, `[adresgegevens]` — vul deze in zodra je KVK-inschrijving rond is.
- **Adres + Google Maps-knop**: in het `<script>`-blok staat `const CONTACT_ADDRESS = "";`. Vul hier je adres in (bijv. `"Kalenderlaan 12, 1234 AB Leiden"`) en het contactblok toont automatisch het adres met een knop "Bekijk op Google Maps". Zolang dit leeg is, staat er een gele placeholder en is de knop verborgen.
- **E-mailadres**: zoek naar `info@gezondhetjaarrond.nl` en vervang dit overal door je eigen e-mailadres (in de tekst en in `CONTACT_EMAIL` in het script onderaan het bestand).
- **Mollie-betaallink**: in het `<script>`-blok onderaan staat:
  ```js
  const MOLLIE_PAYMENT_LINK = "";
  ```
  Zodra je een Mollie-account en een betaallink hebt aangemaakt, plak je die link tussen de aanhalingstekens.
- **E-mailmelding bij elke bestelling**: dit is een statische website zonder eigen server, dus zonder extra stap krijg je geen automatische e-mail. Om dit wél te regelen (gratis, geen code nodig):
  1. Ga naar [formspree.io](https://formspree.io) en maak een gratis account.
  2. Maak een nieuw formulier aan en vul jouw e-mailadres in als ontvanger.
  3. Kopieer de "endpoint"-URL die je krijgt (ziet er ongeveer uit als `https://formspree.io/f/abcdwxyz`).
  4. Plak deze in `index.html` bij:
     ```js
     const FORM_ENDPOINT = "";
     ```
  5. Klaar: zodra iemand nu het bestelformulier invult, krijg jij direct een e-mail met naam, adres, aantal kalenders en bedrag, en wordt de klant automatisch doorgestuurd naar je Mollie-betaallink om via iDEAL te betalen.

  Zonder een ingevulde `FORM_ENDPOINT` blijft het formulier gewoon werken: de klant ziet een bevestiging en wordt alsnog doorgestuurd naar de betaallink, maar jij ontvangt dan geen automatische e-mail — alleen de handmatige "mail je bestelling"-link als iets misgaat.
- **Verzendkosten**: pas zo nodig `const SHIPPING_COST = 3.95;` aan.
- **Juridische teksten**: de privacyverklaring en algemene voorwaarden zijn volledige templates op basis van de AVG en het Nederlandse consumentenrecht (inclusief 14 dagen herroepingsrecht). Laat ze voor livegang het liefst nog even nalezen, bijvoorbeeld via het Juridisch Loket.

## Techniek

Geen build-stap, geen dependencies, geen framework. Eén HTML-bestand met ingebouwde CSS en JavaScript, en één ingesloten afbeelding (als base64), dus het werkt direct op elke gratis hostingdienst (GitHub Pages, Netlify, Vercel, of gewoon een eigen server).
