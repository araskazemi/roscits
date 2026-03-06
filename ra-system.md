<a name="top"></a>

# RA-verksamhetssystem för C-ITS-domän
<mark>Registration Authority (RA)</mark> i [EU-CCMS](euccms.md) är den funktion som hanterar identifiering, validering och registrering av entiteter <mark>innan de får certifikat</mark>.

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
>- RA registrerar information om stationen och tilldelar/registrerar en stationidentifierare.
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

> [!NOTE]
> RA ser och verifierar den publika nyckeln i samband med CSR/registrering för Enrollment Certificate (EC), men RA behöver inte nödvändigtvis lagra nyckeln permanent som en egen datapost.

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

## Livscykelhantering av stationsinformation i ett RA-verksamhetssystem
En C-ITS-station genomgår typiskt följande livscykelfaser i RA-verksamhetssystemet:

:one: Förberedande registrering (organisation + roll)

:two: Initial registrering av station

:three: Certifikatgodkännande

:four: Operativ drift

:five: Uppdatering/ändringshantering

:six: Spärrning/avstängning

:seven: Avregistrering/avveckling

:eight: Arkivering och gallring

### Förberedande registrering (organisation + roll)
Innan en station kan registreras måste organisationen vara godkänd i RA.

Processen kan vara enligt följande steg:
1. Organisation ansöker om att bli registrerad.
2. RA verifierar, juridisk identitet, behörig företrädare, roll i C-ITS-ekosystemet.
3. RA tilldelar organisations-ID.
4. Organisationens behöriga administratör registreras.

Resultat: Organisationen får rätt att registrera stationer inom sitt mandat.

### Initial registrering av station
När organisationen är godkänd kan station registreras.

Processen kan vara enligt följande steg:
1. Organisation initierar registrering via RA-gränssnitt och lämna information om:
    - Stations-ID (eller begäran om generering)
    - Serienummer
    - Tillverkare och modell
    - Firmwareversion
    - Typ av station (RSU/OBU/central)
    - Säkerhetscertifieringsuppgifter
    - Geografisk placering (för RSU)
2. CSR (Certificate Signing Request) laddas upp.
3. RA kontrollerar att:
    - stationstypen är tillåten för organisationens roll,
    - hårdvaran är godkänd enligt policy,
    - inga dubbletter förekommer.
4. RA loggar hela processen.

Resultat: Stationen registreras och tilldelas status Preliminär.

### Certifikatgodkännande
RA godkänner certifikatutfärdande.

Processen kan vara enligt följande steg:
1. RA verifierar CSR.
2. RA säkerställer korrekt koppling (Organisation → Roll → Station → Certifikattyp)
3. RA godkänner begäran.
4. CA utfärdar Enrollment Certificate.
5. Stationens status uppdateras.

Resultat: Stationen tilldelas status Aktiv.

### Operativ drift
Under drift hanterar systemet:
- Certifikatförnyelser (EA/AA)
- Utfärdande av Authorization Tickets (AA)
- Loggning av certifikataktivitet (EA/AA)
- Incidentrapportering (RA + övriga funktioner)

RA ansvarar för att:
- hålla register över stationer uppdaterat
- övervaka avvikelser
- initiera spärrning av certifikat

### Uppdatering/ändringshantering
Information om en station kan behöva uppdateras, t ex firmwareuppdatering, hårdvarubyte, ändrad geografisk placering, byte av ägare/organisation, ändrad roll eller funktion.

Processen kan vara enligt följande steg:
1. Organisation initierar ändringsärende.
2. RA bedömer om:
    - endast metadata uppdateras
    - nytt certifikat krävs
    - ny säkerhetsvalidering krävs
3. Ändringen loggas och versioneras.

> [!NOTE]
> Vid större förändring måste gamla certifikat spärras och nyregistrering eller ny CSR kan krävas.

### Spärrning/avstängning
En spärrning kan initieras av organisationen själv, RA, incidenthantering eller nationell säkerhetsfunktion.
Det kan handla om komprometterad nyckel, manipulerad station, otillåten användning, felaktig registrering, m.m.

Processen kan vara enligt följande steg:
1. RA beslutar om spärrning.
2. Certifikat återkallas (CRL/OCSP).
3. Stationens status ändras till Spärrad.
4. Incident dokumenteras.

### Avregistrering/avveckling
När en station tas ur drift kan processen kan vara enligt följande steg:
1. Organisation anmäler avveckling.
2. RA verifierar status att station inte är aktiv samt att certifikat är spärrade
3. RA ändrar status till Avvecklad.

Resultat: Operativa kopplingar stängs.

Hur länge historisk information ska bevaras beslutas av domänägaren och är kopplat till revisionskrav.

### Arkivering och gallring
RA måste:
- arkivera registreringsdata
- bevara revisionsspår
- följa CITS-domänens arkiv- och gallringsregler
- följa relevant lagstiftning, såsom GDPR, NIS2 och nationella säkerhetsskyddskrav

Gallring kan ske enligt fastställd bevarandetid, som fastställs utifrån gällande lagstiftning och säkerhetsklassning.

## Teknisk gränssnitt mellan RA och CA
Certifikatutfärdare behöver inte ha direktåtkomst till RA-verksamhetssystemet eller RA-databasen.

Ett korrekt designat EU-CCMS bygger på:
- rollseparation,
- minimal informationsdelning, och
- kryptografisk validering.

EA/AA måste ha mekanismer för att hantera nyregistreringar samt få kännedom om spärrade EC, ändrad behörighet och policyändringar. 

Anslutning mellan certifikatutfärdare och RA regleras genom avtal och måste uppfylla gällande krav enligt domänens policy. Kommunikationen måste säkras för att förhindra att CSR manipuleras under överföringen och behöver därför följa samma nivå som i Certificate Policy.

Det finns tre situationer som kräver kommunikation mellan RA och CA.

:one: **Nyregistrering**

När en station registreras första gången: <br />
RA → godkänner <br />
EA → utfärdar EC <br />

Här sker ett kontrollerat informationsutbyte.

:two: **Statusförändring**

Om något ändras hos RA, t ex station avregistreras, roll ändras, organisation mister behörighet eller vid säkerhetsincident: <br />
RA → uppdatera status <br />
EA/AA → sluta utfärda certifikat <br />

Det kan exempelvis ske via:
- periodisk synkronisering,
- push-notifikationer/prenumerationer,
- status-API.

Det är alltså en statuskoppling, inte en fullständig databasdelning som krävs.

:three: **Incident**
Vid missbruk kan Misbehaviour Authority (MA) involveras. RA kan behöva verifiera den ursprungliga registreringen, medan AA kan behöva upphöra med att utfärda nya AT. Detta förutsätter samverkan mellan aktörerna, men inte nödvändigtvis teknisk integration i realtid i samtliga delar.

## Hur CSR används i RA-processen
### Enrollment CSR
1. Stationen genererar nyckelpar i HSM, Secure Element eller TPM-liknande miljö.
2. Stationen skapar CSR:
    - Inkluderar publik nyckel
    - Inkluderar begärda attribut
    - Signerar med privat nyckel
3. CSR skickas till RA. Det kan vara (beroende på implementation):
    - station → RA → EA, eller
    - station → EA med RA som “godkännandesteg”/policy-gate 
4. RA validerar CSR genom att kontrollera:
    - att stationen är registrerad
    - att rollen är korrekt
    - att certifikattyp är tillåten
    - att CSR är korrekt signerad
    - att nyckelparametrar uppfyller policy
5. RA godkänner sedan begäran till CA.
6. EA utfärdar Enrollment Certificate (EC).
7. RA uppdaterar sina poster i RA-verksamhetssystemet.

### Authorization CSR
1. Stationen använder sitt EC för att autentisera sig mot AA-tjänsten.
2. Stationen genererar en batch av pseudonym-nycklar.
3. Stationen skapar en signerad Authorization Ticket Request (CSR-liknande fil för begäran om en eller flera certifikat).
4. AA genomför kryptografisk kontroll och policykontroll.
5. RA har en indirekt roll genom att ha definierat stationens roll och rättigheter, men styrs i regel via EC. Domänen har dock möjlighet att ställa krav på AA att denne måste göra uppslag i RA-policy och/eller RA-attributtjänst.
6. AA utfärdar pseudonymer och stationen får tillbaka en batch AT som kan användas för att signera meddelanden (CAM, DENM, etc.)

> [!IMPORTANT]
> En angripare kan försöka byta ut publik nyckel, ändra attribut eller begära fel certifikattyp. RA kan inte lita på attribut i CSR okritiskt och måste kontrollera attribut i CSR mot sitt eget register och på så sätt säkerställa att rätt rollattribut finns i certifikatet.

## Spårning vid incidenter
När en station skickar meddelanden (t .ex. CAM eller DENM) används AT-certifikat (pseudonymer) som inte avslöjar stationens verkliga identitet. Om något allvarligt inträffar, såsom falska varningar eller attacker, behöver det vara möjligt att spåra avsändaren utan att bryta pseudonymiteten under normal drift. Detta kan RA, EA och AA göra tillsammans genom en stegvis spårning av identiteter. Stegen kan beskrivas enligt nedan:
1. Man börjar med certifikatet i meddelandet som ger information om utfärdaren samt certifikatets serienummer.
2. Med serienumret vet AA vilken EC som användes för att begära pseudonymcertifikatet.
3. EA vet vilken station som har tilldelats EC.
4. RA vet vilken organisation som registrerade stationen.

## En viktig konsekvens
Den aktör som kontrollerar RA har i praktiken kontroll över:
- vilka stationer som finns i domänen,
- vilka organisationer som får delta,
- vem som kan identifieras vid incident.

Därför väljer många länder att ha RA nationellt, även om EA och AA kan vara externa.

<p>&nbsp;</p>

----

:arrow_backward: [Hem](README.md) &nbsp; &nbsp; | &nbsp; &nbsp; :arrow_up_small: [Tillbaka till toppen](#top)  
