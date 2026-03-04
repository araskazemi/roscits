# EU CCMS
EU CCMS (European Union Common Certificate Management System) är det gemensamma europeiska ramverket för certifikathantering inom C-ITS. Systemet 
etablerar en förtroendebaserad <mark>Public Key Infrastructure (PKI)</mark> som möjliggör säker autentisering och signering av meddelanden mellan 
deltagande enheter i det kooperativa transportsystemet.

Syftet med EU CCMS är att säkerställa att endast betrodda och auktoriserade aktörer kan delta i C-ITS-kommunikation, samtidigt som användarnas 
<mark>integritet skyddas genom pseudonymisering och regelbunden certifikatsrotation</mark>. Genom en harmoniserad europeisk certifikatsstruktur 
möjliggörs <mark>gränsöverskridande interoperabilitet</mark>, vilket är en grundförutsättning för ett sammanhängande och skalbart C-ITS-ekosystem 
inom EU.

Implementeringen av EU CCMS är därmed en central komponent i att upprätthålla säkerhet, tillit och funktionell interoperabilitet i framtidens 
digitaliserade transportsystem.

## Tillit och säkerhet
Tillitskedjan inkluderar flera roller:
* <mark>CPA (Certificate Policy Authority)</mark>: ansvarar för policydokument och godkänner Root CAs.
* <mark>TLM (Trust List Manager)</mark>: skapar och publicerar den europeiska certifikatlistan (ECTL) med alla betrodda Root CAs.
* <mark>CPOC (C-ITS Point of Contact)</mark>: fungerar som nav mellan Root CAs och TLM, tar emot certifikat, publicerar ECTL och tillhandahåller ankre i tillitskedjan (trust anchors).
* <mark>Root CA</mark>: kan vara statliga eller privata aktörer. Utfärdar certifikat till:
    * <mark>EA (Enrolment Authority)</mark>: utfärdar <mark>Enrolment Credentials (EC)</mark> till C-ITS-enheter (fordon och RSU:er).
    * <mark>AA (Authorization Authority)</mark>: utfärdar <mark>Authorisation Tickets (AT)</mark>, som är kortlivade pseudonyma certifikat för att skydda integriteten.

C-ITS-enheter använder EC för identifiering gentemot tillitsinfrastrukturen och AT för att signera och verifiera C-ITS-meddelanden.

### Vad som utmärker C-ITS jämfört med klassisk PKI
#### Pseudonymitet och integritetsskydd
Till skillnad från klassisk PKI, där identiteten ofta är knuten till certifikatet, använder C-ITS pseudonyma certifikat (ATs) som byts ofta för att förhindra spårning av fordon. Kopplingen till fordonets verkliga identitet hålls skyddad av EA/AA och exponeras inte i kommunikationen.

#### Korta livstider i nyckelhanteringen
Authorisation Tickets (AT) har kort giltighetstid och måste bytas ofta (sekretesskrav). Detta skiljer sig från traditionella PKI-certifikat som ofta är giltiga i månader eller år.

#### Multirot-struktur och central trust list
Flera Root CAs kan samexistera, men alla listas i en central European Certificate Trust List (ECTL) signerad av TLM. Detta är annorlunda än en klassisk PKI där en organisation ofta har en hierarki med en root och underordnade CAs, men inte en gemensam europeisk trust anchor.

#### Separering av roller (EA och AA)
En viktig säkerhetsdesign är separationen mellan enrolment (EC) och authorization (AT) för att undvika att någon enskild aktör kan både identifiera och spåra ett fordon. I en traditionell PKI finns inte denna uppdelning – CA utfärdar certifikat direkt till slutanvändare.

#### Specifika C-ITS-protokoll och standarder
Certifikat och signaturer följer ETSI TS 103 097 och relaterade standarder, optimerade för bandbredd och realtidskrav i fordonskommunikation.
Även särskilda "butterfly key"-mekanismer används för att möjliggöra massgenerering av pseudonyma certifikat.

#### Striktare operativa och fysiska kontroller
Rollerna (Root CAs, EA, AA, TLM) omfattas av detaljerade krav på revision, fysiska säkerhetskontroller och procedurer som fastställs av EU (via CP, Security Policy och CPOC Protocol). Traditionell PKI följer ofta en CA/Browser Forum eller eIDAS-baserad policy, men C-ITS har sin egen europeiska styrmodell.

#### Manuella och fysiska processer för nyckelhantering
Root CA-certifikat lämnas ofta fysiskt (med kurir) till CPOC för att minska risken för kompromettering. Detta är ovanligt i klassisk PKI, där processerna i större utsträckning är automatiserade.

## Övergripande struktur
Den övergripande strukturen för tillitsmodellen kan delas i följande tre skikt:

:one: EU-nivå

:two: Nationell domän

:three: Molntjänstförmedlare (som kallas Interchange)

```
────────────────────────────────────────────────────────────
                EUROPEAN LEVEL
────────────────────────────────────────────────────────────

            European Commission
   (Policy, Governance, Legal Framework)
                     │
                     ▼
             Trust List Manager
                     │
                     ▼
                    ECTL
              (EU Trust List)
                     │
                     ▼
           ┌─────────────────────┐
           │  RCA EU             │
           │  (Default Root CA)  │
           └─────────────────────┘
                      │
           ┌──────────┴──────────┐
           ▼                     ▼
   ┌───────────────┐      ┌───────────────┐
   │      EA       │      │      AA       │
   │ Enrollment CA │      │ Authorization │
   │               │      │      CA       │
   └───────────────┘      └───────────────┘
           │                     │
           │                     │
────────────────────────────────────────────────────────────
         NATIONAL C-ITS DOMAIN (e.g. Sweden)
────────────────────────────────────────────────────────────

              Domain Governance
                     │
                     ▼
        ┌───────────────────────────┐
        │ RA-system (Registration)  │
        │ Identity vetting          │
        │ Station approval          │
        └───────────────────────────┘
                     │
                     ▼
            Certificate Requests
                     │
         ┌───────────┴────────────┐
         ▼                        ▼
        EC                        AT
(Long-term identity)    (Short-term pseudonym)
                     │
                     ▼
              C-ITS STATIONS
    ┌────────────────────────────────┐
    │  Roadside ITS-S                │
    │  Vehicle ITS-S                 │
    │  Traffic signal ITS-S          │
    │  Emergency vehicle ITS-S       │
    └────────────────────────────────┘
                     │
                     ▼
            Signed C-ITS Messages
         (CAM, DENM, MAPEM, SPATEM, etc.)

────────────────────────────────────────────────────────────
           OPTIONAL IP / CLOUD LAYER
────────────────────────────────────────────────────────────

    ┌────────────────────────────────┐
    │                                │
    │   Interchange / Cloud broker   │
    │                                │
    └────────────────────────────────┘
(Not part of trust anchor, but must validate signatures)

```

### Hur PKI-kedjan hänger ihop
PKI-kedjan bygger på en multiple root CA-arkitektur med en gemensam trust list.
Det innebär att:
- en svensk station accepterar en fransk station,
- en norsk station accepterar en tysk station,
- och så vidare.

Detta är grunden för interoperabilitet enligt Security Policy.

Förenklat ser tillitskedjan ut så här:

```
 ECTL
   ↓
  RCA
   ↓
EA / AA
   ↓
C-ITS Station Certificates
   ↓
Signed Messages

```

Den gemensamma tilliten kommer dock inte från en gemensam root, utan från en multiple root CA architecture med en gemensam europeisk trusted list, ECTL.

Tillitskedjena kan se ut så här:

```
                     CPA
                      │
                      ▼
              Trust List Manager
                      │
                      ▼
            ECTL (EU Trust List)
                      │
        ┌─────────────┼─────────────┐
        ▼             ▼             ▼
   Root CA EU    Root CA A      Root CA B
  (EU default)  (e.g. nation)  (e.g. OEM)
        │             │              │
        ▼             ▼              ▼
      EA/AA         EA/AA          EA/AA
        │             │              │
        ▼             ▼              ▼
    Stations      Stations       Stations

```

Den nationella domänen är inte en separat PKI-root, utan består av:
- Nationellt RA-system
- Avtal
- Styrning och upprätthållande av policy
- Tilldelning av roller

Interchange är inte en PKI-aktör, snarare en broker/federationstjänst som transporterar IP-baserade meddelanden.
En interchange node måste dock validera ETSI TS 103 097-signaturer samt följa Security Policy.

