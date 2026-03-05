# RA-system för C-ITS-domän
<mark>Registration Authority (RA)</mark> i C-ITS/EU-CCMS är den funktion som hanterar identifiering, validering och registrering av entiteter <mark>innan de får certifikat</mark>.

RA är på så sätt inte en CA som utfärdar certifikat, men säkerställer att CA får korrekta uppgifter för att rätt aktör, rätt utrustning och rätt roll och rättigheter kopplas till rätt certifikat enligt Certificate Policy.

## Information som en RA hanterar
Utifrån Security Policy och den organisatoriska strukturen i C-Roads kan man dela upp informationen som RA hanterar i följande kategorier:

:one: Identitetsinformation om organisationen

:two: Roll- och rättigheter

:three: Information om C-ITS-stationen

:four: Certifikathanteringsdata

:five: Avtals- och efterlevnadsinformation

:six: Loggar och revisionsspår

### Identitetsinformation om organisationen
RA måste hantera uppgifter om de organisationer som ingår i C-ITS-domänen, bl a:
- Organisations-ID (teknisk identitet)
- Organisationsnummer (juridisk identitet)
- Organisationsnamn
- Land/jurisdiktion
- Kontaktperson(er)
- Kontaktuppgifter
- Eventuella fullmakter/behörighetsintyg och avtal

Syftet med dessa uppgifter är att säkerställa:
- att endast legitima organisationer registreras,
- att organisationen har rätt att agera i en viss roll (t ex road operator, emergency authority etc.),
- att den omfattas av rätt nationell rättsordning,
- att villkor och ansvarsfördelning och sanktioner är reglerade.

Detta är klassisk PKI-registreringsinformation, men i C-ITS är kopplingen till roll och funktion särskilt viktig.

### Roll- och rättigheter
Stationer i C-ITS har olika [roller och rättigheter](roles_in_cits.md). RA behöver ha en förteckning över:
- Typer av C-ITS-stationer som kan registreras i domänen (RSU, OBU, central station, etc.)
- Roller som kan förekomma i trust-modellen (road operator, OEM, service provider, etc.)
- Eventuella särskilda behörigheter (t ex blåljusprioritet, trafiksignalstyrning, m.m.)

Detta är kritiskt eftersom:
- olika roller kan få olika certifikattyper
- vissa roller kan ha särskilda rättigheter (t ex SREM/SSEM för blåljus)
- felaktig registrering kan skapa allvarliga säkerhetsrisker

### Information om C-ITS-stationen
RA behöver skapa förutsättningar för att certifikat kan knytas till en konkret teknisk entitet.

Exempel på data som registreras:
- Unikt stations-ID (som kan skapas av RA eller av organisationen som äger stationen)
- Serienummer
- Tillverkare
- Modell
- Firmware-/hårdvaruversion
- Säkerhetscertifiering (Common Criteria / ISO 15408 enligt Security Policy 

Detta möjliggör:
- spårbarhet
- spärrning vid kompromettering
- livscykelhantering

> [!IMPORTANT]
> RA registrerar inte certifikaten – känner inte till stationen EC och AT.
>- RA registrerar information om stationen och tilldelar/registrerar en station-identifierare.
>- EA använder den identifieraren när EC utfärdas och kopplar den till certifikatet.
>- Det är alltså EA/AA som har loggar som kopplar certifikat till stationen.
>- EA kan tekniskt utfärda EC utan att känna till stationens verkliga identitet — bara ett RA-godkänt identifieringsvärde.

### Certifikathanteringsdata
RA hanterar metadata kring certifikatutgivning, t ex:
- Certifikatförfrågan (CSR)
- Koppling till rätt CA
- Certifikattyp (Enrollment Certificate, Authorization Ticket, etc.)
- Giltighetstid
- Återkallandeinformation
- Loggning av beslut

Detta är kärnan i registreringsprocessen och RA som funktion – att säkerställa korrekt koppling mellan identitet och certifikat och livscykelhantering.

### Avtals- och efterlevnadsinformation
Eftersom C-ITS bygger på en gemensam trust-modell behövs även:
- Intyg om efterlevnad av Security Policy 
- Åtagande att följa Certificate Policy
- Eventuella nationella tillägg baserat på domänägarens godkännande
- Incidentrapporteringsansvar

Detta är särskilt viktigt när domänen styrs genom avtal, det vill säga när varje organisation frivilligt väljer att ansluta sig till och ingå i domänen, snarare än att omfattas av bindande regelverk eller lagstiftning.

### Loggar och revisionsspår
En RA måste enligt god säkerhetspraxis hantera:
- Vem som godkänt registrering
- När beslut fattades
- Underlag för beslut
- Ändringshistorik
- Revokeringar

Detta är avgörande för juridisk hållbarhet, spårbarhet och incidenthantering.

## Livscykelhantering av stationsinformation i ett RA-system
En C-ITS-station genomgår typiskt följande livscykelfaser i RA-systemet:

:one: Förberedande registrering (organisation + roll)

:two: Initial registrering av station

:three: Certifikatgodkännande

:four: Operativ drift

:five: Uppdatering / förändringshantering

:six: Spärrning / suspension

:seven: Avregistrering / avveckling

:eight: Arkivering

### Förberedande registrering (organisation + roll)
Innan en station kan registreras måste organisationen vara godkänd i RA.

Processen kan vara enligt följande steg:
1. Organisation ansöker om att bli registrerad.
2. RA verifierar, juridisk identitet, behörig företrädare, roll i C-ITS-ekosystemet.
3. RA tilldelar organisations-ID.
4. Organisationens behöriga administratör registreras.

Resultat: Organisationen får rätt att registrera stationer inom sitt mandat.

### Initial registrering av station

### Certifikatgodkännande

### Operativ drift

### Uppdatering / förändringshantering

### Spärrning / suspension

### Avregistrering / avveckling

### Arkivering


