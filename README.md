# Robust och säker implementering av C-ITS
Denna repo används för innehålsproduktion och versionshantering av material som ska in i projektrapporten.
Följande delar i rapporten berörs:
1. <mark>**Bakgrund**</mark>
2. <mark>**Del B – Analys av Roller och Implementation**>

Projektet fokuserar på hur en trygg, robust och säker utrullning av C-ITS (Cooperative Intelligent Transport Systems) kan genomföras i Sverige. Målet är att identifiera tekniska, organisatoriska och säkerhetsmässiga förutsättningar för en långsiktigt hållbar implementering.

-------------

## Innehållsförteckning

### Bakgrund
- [Bakgrund](bakgrund.md)
    - [C-ITS översikt](cits.md)
        - [Informationsutbyte baserat på ETSI-meddelanden](cits.md#informationsutbyte-baserat-p%C3%A5-etsi-meddelanden)
        - [Säkerhetsarkitektur](cits.md#s%C3%A4kerhetsarkitektur)
    - [Det europeiska ramverket för C-ITS.](cits_in_eu.md)
        - [ITS-direktivet](cits_in_eu.md#its-direktivet)
        - [EU-CCMS](cits_in_eu.md#eu-ccms)
        - [Nationella C-ITS-domän](cits_in_eu.md#nationella-c-its-dom%C3%A4n)
        - [Interchange-noder](cits_in_eu.md#interchange-noder)
        - [Svensk implementering av C-ITS](cits_in_eu.md#svensk-implementering-av-c-its)
        - [Utmaningar](cits_in_eu.md#utmaningar)
    - [European Union Common Certificate Management System](euccms.md)
        - [Övergripande tillitsstruktur](euccms.md#%C3%B6vergripande-tillitsstruktur)
        - [Hur PKI-kedjan hänger ihop](euccms.md#hur-pki-kedjan-h%C3%A4nger-ihop)
    - [Roller och rättigheter i C-ITS](roles_in_cits.md)
        - [Tekniska roller i PKI](roles_in_cits.md#tekniska-roller-i-pki-f%C3%B6r-meddelandesignering)
        - [Meddelandetyper och funktionella roller](roles_in_cits.md#meddelandetyper-och-funktionella-roller)
        - [Applikationsroller](roles_in_cits.md#applikationsroller)
        - [Styrning av roller och rättigheter](roles_in_cits.md#styrning-av-roller-och-r%C3%A4ttigheter)
    - [RA-funktioner för C-ITS-domän](ra-system.md)
        - [Information som en RA hanterar](ra-system.md#information-som-en-ra-hanterar)
        - [Livscykelhantering av stationsinformation i ett RA-verksamhetssystem](ra-system.md#livscykelhantering-av-stationsinformation-i-ett-ra-verksamhetssystem)
        - [Teknisk gränssnitt mellan RA och CA](ra-system.md#teknisk-gr%C3%A4nssnitt-mellan-ra-och-ca)
        - [Hur CSR används i RA-processen](ra-system.md#hur-csr-anv%C3%A4nds-i-ra-processen)
        - [Spårning vid incidenter](ra-system.md#sp%C3%A5rning-vid-incidenter)
        - [En viktig konsekvens](ra-system.md#en-viktig-konsekvens)


### Del B – Analys av Roller och Implementation

- [En möjlig väg för svensk implementering av C-ITS enligt EU-CCMS](secits_domain.md)
- [Backend-baserad C-ITS med Interchange-noder – ett avvägt första steg](backend_cits.md)


### Extramaterial
* [EU-CCMS-protokollen](euccms_protocols.md)
* [MATF (Mutually Authenticating TLS in the context of Federations)](matf_intro.md)
