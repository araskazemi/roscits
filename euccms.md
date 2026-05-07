<a name="top"></a>

# European Union Common Certificate Management System 
European Union Common Certificate Management System (EU-CCMS) är EU:s gemensamma säkerhetsinfrastruktur för C-ITS och möjliggör säker och interoperabel kommunikation mellan aktörer och länder genom hantering av digitala certifikat. Det säkerställer att meddelanden är autentiska och skyddar samtidigt användarnas integritet genom pseudonyma certifikat och ett [gemensamt europeiskt ramverk](cits_in_eu.md).

## Övergripande tillitsstruktur
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

       Domain Governance and Policy
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

## Hur PKI-kedjan hänger ihop
PKI-kedjan i EU-CCMS bygger på en multiple root CA-arkitektur med en gemensam trust list.
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



:arrow_right: [Nästa](roles_in_cits.md)

<p>&nbsp;</p>

----

:arrow_backward: [Hem](README.md) &nbsp; &nbsp; | &nbsp; &nbsp; :arrow_up_small: [Tillbaka till toppen](#top)  
