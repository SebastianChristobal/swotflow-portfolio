# Status och verifiering

Uppdaterat 17 november 2026. Tabellen skiljer projektets genomförda pilottester från den publika demon och från funktioner som bara har granskats i kod.

| Område | Vad som har genomförts eller kontrollerats | Begränsning |
|---|---|---|
| Webbplats och demo | Publik webbplats och öppen demo har granskats i webbläsare | Företag, inlägg och mätvärden i demon är fiktiva |
| Privat åtkomst | Inloggning med befintliga pilotkonton och rollstyrd analysknapp har testats i testmiljön | Ingen fullständig säkerhetsrevision eller generell lansering påstås |
| Datainsamling | Verkliga externa insamlingskörningar har genomförts; slutförda körningsposter och sociala snapshots finns sparade | Ny insamling är nu pausad. Plattformar kan begränsa tillgången även till offentliga profiler |
| Databas och historik | MongoDB/Prisma används för sparat underlag och resultat; aggregerad databasstatus kontrollerades 17 november | Ingen privat databasexport publiceras i detta repo |
| AI och innehållsfokus | Riktiga modellanrop har genomförts. Slutförda och sparade innehållsfokusanalyser finns för en pilotarbetsyta | En slutförd körning är inte samma sak som att alla slutsatser har kvalitetsgranskats |
| SWOT | Sparade SWOT-snapshots finns. Demon visar separat ett fiktivt exempel | Förekomsten av snapshots bevisar inte försäljningsnytta eller kvalitet i varje slutsats |
| Testning och bygge | 182 automatiska tester passerade den 12 november, tillsammans med typkontroll, lint och produktionsbygge vid dokumenterade ändringar | Ingen ny fullständig testkörning gjordes för denna dokumentationsuppdatering. Modellanrop i automatiska tester är mockade |
| Språk | Svenska, engelska och latinamerikansk spanska finns implementerade | Varje text och analysväg har inte genomgått fullständig språkgranskning |
| Rapporter | Datamodell och backendlogik för rapportögonblicksbilder finns | Inga sparade rapportposter fanns vid kontrollen; verklig rapportgenerering påstås därför inte vara verifierad |
| Abonnemang och Stripe | Planvisning och åtkomstregler finns i koden | Betalningar är avstängda; ingen aktiv betalmodell påstås |

## Erfarenheter från riktiga körningar

Pilottesterna har visat begränsningar i åtkomst till sociala medier och i modellernas svar. Bland annat har obestyrkta citat, produktfraser och utelämnade inlägg behövt hanteras. Kontrollerna har utvecklats så att osäkra valfria uppgifter blir okända och att utelämnade inlägg behålls i urvalets totalantal. Okända eller duplicerade käll-ID:n avvisas fortfarande.

Källkontroller gör resultatet mer spårbart, men ersätter inte en mänsklig bedömning av om en tolkning är relevant och korrekt.

## Nuvarande produktfas

SwotFlow är en B2B-tjänst under utveckling, med särskilt fokus på marknadsteam hos konsumentvarumärken. Produkten har en publik visningsdemo och en kontrollerad privat pilot. Den är inte öppet lanserad med fri registrering, aktiva betalningar eller garanterad insamling från alla kanaler.

Nästa kvalitetssteg är fortsatt granskning av riktiga analysresultat och tydligare, företagsspecifika konkurrentobservationer med belägg. Ingen ny insamling eller AI-körning startades för denna uppdatering; endast aggregerad lagrings- och körningsstatus lästes.
