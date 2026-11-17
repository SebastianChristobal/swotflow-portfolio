# Så fungerar SwotFlow

[Till presentationen](README.md)

SwotFlow består av ett webbgränssnitt, en serverdel, en databas och externa tjänster för insamling och AI. Här beskrivs hur delarna samarbetar. Beskrivningen bygger på granskad kod och projektets pilottester, uppdaterat den 17 november 2026.

## Två sätt att använda produkten

**Den publika demon** visar ett fiktivt kafferosteri och dess konkurrenter. Besökaren kan utforska vyer, filter och exempel utan konto. Demon läser inte privata företagsdata och startar inga betalda leverantörsanrop.

**Den privata piloten** kräver inloggning. Användaren tillhör en arbetsyta för sitt företag. Där finns företagets profil, konkurrenter, sparat innehåll och analysresultat. Servern kontrollerar vilka uppgifter användaren får läsa och vilka operationer rollen tillåter.

## Från källor till analys

1. **Företaget anger sin profil och sina konkurrenter.** Uppgifterna ger sammanhang åt analysen och skiljs från externa observationer.
2. **Tillgängligt innehåll samlas in när insamling är tillåten.** Apify används för sociala medier. Webbplatsunderlag bearbetas också. Åtkomstbegränsningar kan göra att en källa bara ger delar av innehållet eller inget alls.
3. **Underlaget ordnas och sparas.** Inlägg, källänkar, tillgängliga mätvärden och tidpunkter lagras i MongoDB via Prisma, som är kopplingen mellan serverkoden och databasen. Saknade värden skiljs från uppmätta nollvärden.
4. **AI bearbetar ett avgränsat urval.** Servern skickar utvalt underlag till OpenAI. I innehållsjämförelsen används samma kanal, period och temakategorier för båda företagen. Sidvisning startar inte automatiskt ett nytt modellanrop.
5. **Svaret kontrolleras innan det används.** Käll-ID:n och citat kontrolleras mot underlaget. Obestyrkta valfria uppgifter blir okända. Inlägg som modellen utelämnar finns kvar som oklassificerade. Felaktiga käll-ID:n avvisas. Antal och andelar räknas i applikationskoden.
6. **Användaren utforskar sparade resultat.** Gränssnittet visar innehåll, statistik, konkurrentobservationer och SWOT-underlag med källor och begränsningar.

Insamling och AI är separata operationer. Piloten har genomfört insamling och analys med verkliga data, men ny insamling är nu pausad i den granskade koden. Tillåtna AI-flöden kan fortfarande använda sparat underlag.

## Delarna i en bild

~~~mermaid
flowchart TD
    D["Besökare utan konto"] --> DEMO["Publik demo med fiktiva data"]
    U["Pilotanvändare"] --> AUTH["Inloggning och kontroll av behörighet"]
    AUTH --> APP["Serverdel i Next.js"]
    APP <--> DB[("Databas: MongoDB via Prisma")]
    APP --> UI["Gränssnitt: React, formulär och diagram"]
    APP --> C["Separat kontroll för insamling"]
    C --> S["Apify och webbplatsunderlag"]
    S --> N["Ordna underlag, källor och tidpunkter"]
    N --> DB
    APP --> A["Separat kontroll för AI"]
    DB --> A
    A --> AI["OpenAI bearbetar valt underlag"]
    AI --> V["Kontrollera svaret och räkna jämförelser"]
    V --> DB
~~~

Pilarna visar hur lösningen är uppbyggd, inte att alla funktioner är öppna eller aktiva samtidigt.

## Vem får se vad?

Auth.js hanterar inloggningen. Lösenord lagras som hashvärden med bcrypt och sessionen använder JWT. Servern kontrollerar aktuell användare, arbetsytemedlemskap och roll innan privata operationer tillåts.

En företagsägare och plattformens administratör har olika ansvar. Företagets uppgifter och resultat hör till arbetsytan. Ett generellt gränssnitt för att växla mellan flera företag är inte färdigbyggt.

## Varför sparas data och resultat?

Sparade underlag gör att användaren kan återvända till analysen utan en ny insamling vid varje besök. Historik skiljer publiceringsdatum från tidpunkten då ett mätvärde hämtades. Sparade rapporter är tänkta som ögonblicksbilder av underlaget; funktionernas faktiska verifieringsläge beskrivs i [STATUS.md](STATUS.md).

## Drift och begränsningar

Next.js samlar gränssnitt och serverdel i samma applikation. Vercel används för publicering, med produktion och separat test/preview. Miljöerna kan ha olika åtkomst och aktiverade funktioner. Kostnadskontroll, bekräftelse och skydd mot dubbla körningar ligger före externa anrop.

Testmiljön har ett begränsat undantag för innehållsanalys av sparade data i en utvald pilotarbetsyta. Det innebär inte att alla skrivningar är tillåtna. Stripe-kod finns, men betalningar är avstängda.
