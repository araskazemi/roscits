# EU CCMS-protokollen
EU-CCMS sätter specifika regler, datastrukturer och processer genom tillämpning av befintliga standarder, för att de ska funka på europeisk nivå för C-ITS.

Standarderna man utgår från:
* <mark>ETSI TS 103 097</mark>: Definierar säkerhetsheader och certifikatformat för ITS-meddelanden.
* <mark>ETSI TS 102 941</mark>: Trust & Privacy Management (roller, policyer, certifikatkedja).
* <mark>ISO/IEC 21177</mark>: Sessionssäkerhet för IP-baserad C-ITS-kommunikation.
* <mark>IEEE 1609.2</mark>: Nordamerikansk motsvarighet, som har påverkat vissa delar men EU följer ETSI.
* <mark>ASN.1 / OER</mark>: Kodning av datastrukturer.

## Vad protokollen tillför
### Profilering
Man väljer vilka fält, algoritmer, giltighetstider, längder osv. som är tillåtna i EU-CCMS.

Exempel: Hash ska vara SHA-256/384, nycklar BrainpoolP256r1/P384r1, max giltighet för Root CA är 5 år.

### Procedurer för livscykeln
CPOC-protokollet beskriver exakt hur ett Root CA-certifikat levereras, verifieras, länkas och återkallas.
Man använder ASN.1-strukturer från ETSI, men sättet att leverera (fysiskt media till JRC i Ispra, formulär, dubbelkontroller etc.) är definierat i CCMS-protokollet.

### Interaktion mellan roller
CPOC (Point of Contact), TLM (Trust List Manager), CPA (Certificate Policy Authority), Root CAs, EA, AA.

Protokollen definierar exakt vem som skickar vad, hur det verifieras, och hur det hamnar i ECTL (European Certificate Trust List).

### Kompletterande krav och best practices
Annex I i CPOC-protokollet anger bindande tekniska krav för RCA- och TLM-certifikat (t.ex. vilka appPermissions som får användas, hur link certificates ska konstrueras).

Detta är inte i ETSI-standarderna utan en EU-specifik styrning för att undvika spretiga implementationer.

## Översiktstabell
Tabellen nedan redogör för standard och dess tillämpning i EU-CCMS-protokollen.


| Område | Basstandard(er) | Vad EU-CCMS protokollen tillför |
|--------|-----------------|-------------------------------------------|
| **Certifikatformat** | **ETSI TS 103 097** – certifikat- och säkerhetsheaderformat | Profilering: bara vissa fält/algoritmer tillåtna. <br>• Endast Brainpool P256r1/P384r1 för ECDSA. <br>• Hash SHA-256/384. <br>• Max giltighet Root CA 5 år. <br>• Definierade värden för `appPermissions`, `certIssuePermissions`, regionfält m.m. |
| **Trust & Privacy Management** | **ETSI TS 102 941** – roller, policy, trust management | EU-CCMS protokoll definierar **RCA-, TLM- och link-certifikat** och deras livscykel. <br>• Regler för nyckelutbyte (med länkcertifikat). <br>• Revokering av RCA, inkl. kritiska scenarier (”1b”). <br>• Bindande formulär och processer (RCA Application/Enrolment/Revocation). |
| **Meddelandesignering (V2X)** | **ETSI TS 103 097** (signaturer i ITS-meddelanden). <br>**IEEE 1609.2** (påverkat strukturerna) | EU-profil: Endast vissa PSIDs (tjänster) är godkända. <br>Alla C-ITS-meddelanden måste signeras enligt ETSI TS 103 097. <br>Max permissions per certifikat styrs (begränsning av attackyta). |
| **IP-kommunikation (station till station)** | **ISO 21177** – Sessionssäkerhet | EU-profil: Kan användas för EA/AA-kommunikation över IP. Profilering pågår inom ETSI. |
| **Kodning** | **ASN.1 OER** (Octet Encoding Rules, ITU 2014) | EU-profilen kräver att certifikat och länkcertifikat levereras som ASN.1/OER-strukturer, bl.a. på fysiskt media (CD/DVD) till CPOC. |
| **Enhetscertifiering (C-ITS stationer)** | **ISO/IEC 15408 (Common Criteria)** | EU-krav: stationer ska utvärderas (minst EAL2+) tills officiella skyddsprofiler finns. |
| **Revokering** | ETSI-mekanismer (CRL, delta CRL) | EU-CCMS: CPOC-protokollet definierar exakt hur RCA revokeras (inkl. fysiskt möte eller eIDAS-signerat e-mail i kritiska fall). Revokerade certifikat tas bort ur **ECTL** som TLM publicerar. |
| **Trustlist (ECTL)** | **ETSI TS 102 941** – Trust List mgmt. | EU-profil: TLM är central instans, publicerar signerad ECTL regelbundet. <br>• Specifik publiceringsfrekvens. <br>• CPOC-webb som distributionspunkt. <br>• Maskinläsbara format definierade. |
