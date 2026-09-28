# AIVORA — AI Recruitment & Prospecting Automation

AIVORA is a Make.com automation project that uses Telegram as the user interface and OpenAI as the orchestration layer for prospecting and job-application workflows.

## What it does

### Prospecting
- Receives a request from Telegram.
- Classifies the request with OpenAI.
- Uses web search for current prospecting results.
- Returns structured JSON.
- Stores results in Google Sheets.
- Sends a concise summary back to Telegram.

### Applications
- Generates a tailored application package:
  - email subject
  - short application email
  - LinkedIn message
  - full application / cover message
- Stores the application in Google Sheets.
- Asks for confirmation in Telegram.
- On `OUI`, retrieves the latest application waiting for confirmation.
- Validates that a recipient email exists.
- Sends the email through Gmail.
- Updates the Google Sheets status to `ENVOYÉ`.

## Main stack

- Make.com
- OpenAI
- Telegram Bot
- Google Sheets
- Gmail

## High-level architecture

```text
Telegram
   |
   v
OpenAI
   |
   v
Router
   |--------------------|
   |                    |
PROSPECTION         CANDIDATURE
   |                    |
Web search          Parse JSON
   |                    |
Google Sheets       Google Sheets
   |                    |
Telegram            Telegram previews
                        |
                        v
                    Confirmation
                        |
                      OUI
                        |
                  Search latest row
                        |
                  Validate email
                        |
                      Gmail
                        |
                  Update status
                    -> ENVOYÉ
```

## Importing the blueprint

1. Download the sanitized blueprint from this repository.
2. In Make.com, import the blueprint.
3. Reconnect your own services:
   - Telegram Bot
   - OpenAI
   - Google Sheets
   - Gmail
4. Replace the placeholder spreadsheet IDs.
5. Replace the placeholder contact information in the OpenAI prompt:
   - `YOUR_NAME`
   - `YOUR_PHONE`
   - `YOUR_EMAIL@example.com`
6. Recreate the Telegram webhook if Make requests it.
7. Test each route with `Run once` before activating the scenario.

## Google Sheets structure

### AIVORA_PROSPECTION

```text
Date | Entreprise | Poste | Télétravail | Type de contrat | Lien | Source | Statut | Notes
```

### AIVORA_CANDIDATURES

```text
Date | Entreprise | Email destinataire | Lien candidature | Objet | Corps email | LinkedIn | Lettre | Statut
```

## Safety / privacy

The public blueprint in this repository is sanitized. It should not contain:
- API keys
- Telegram tokens
- personal phone numbers
- personal email addresses
- Make connection IDs
- Make webhook IDs
- private Google spreadsheet IDs

After importing, users must reconnect their own accounts in Make.

## Portfolio value

This project demonstrates:
- AI workflow orchestration
- prompt design and structured JSON outputs
- routing and conditional logic
- web-assisted prospecting
- data persistence with Google Sheets
- human-in-the-loop approval before sending email
- Gmail automation
- Telegram bot integration
- duplicate-send protection through status tracking

## Demo idea

1. Send a prospecting request in Telegram.
2. AIVORA finds opportunities.
3. Results appear in Google Sheets.
4. Generate a tailored application.
5. Confirm with `OUI`.
6. Gmail sends the email.
7. The status changes to `ENVOYÉ`.

## License

Portfolio / educational project. Add your preferred license before public reuse.
