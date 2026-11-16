# Status och verifiering

Granskat 16 november 2026. Lokal källkod och publicerad demo är olika verifieringskällor.

| Område | Vad som har verifierats | Avgränsning |
|---|---|---|
| Webbplats och demo | Publik webbplats och öppen demo nås i webbläsare | Fiktiva data; ingen verklig analyskörning verifieras av demon |
| Dashboard, statistik och SWOT | Vyer och konkurrentjämförelse har granskats i demon | Demons siffror är inte verkliga kundresultat |
| Frontend och backend | Next.js, React, TypeScript, Tailwind, Recharts och API-rutter finns i koden | Lokalt bygge och fullständig regression har inte körts vid denna granskning |
| Databas | Prisma-schema med MongoDB och arbetsytemodell har lästs | Ingen anslutning till databas och inga kunddata lästa |
| Autentisering | Auth.js Credentials, bcrypt och JWT-konfiguration har lästs | Ingen privat inloggning eller rolltest utförd |
| Datainsamling | Apify-adaptrar, normalisering och körningskontroller finns | Normal insamling är pausad i granskad lokal kod; inga körningar startade |
| AI | OpenAI-anrop, strukturerade svar, validering och åtkomstkontroller finns | AI har separat pausflagga; faktisk privat körning eller kostnad har inte verifierats |
| Stripe | Integrationskod finns | Betalningar är uttryckligen avstängda |
| Rapporter och abonnemangsregler | Modeller och backendlogik finns | Ingen generell lansering eller aktiv betalmodell påstås |
| Testning | Testfiler och utvecklingskommandon har granskats | Inget påstående om att samtliga tester passerar just nu |

## Nuvarande produktfas

SWOTFlow är en produkt under utveckling med publik visningsdemo och kontrollerad privat pilot. Den publika presentationen påstår inte en färdig allmänt tillgänglig SaaS-tjänst med betalningar, obegränsad insamling eller automatisk analys på alla kanaler.

Aktuella åtkomst- och pausregler kan ändras mellan lokala grenar och driftsatta miljöer. Publicerings- och driftstatus behöver läsas tillbaka inför nya produktlöften.
