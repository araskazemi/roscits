<a name="top"></a>

# Roller och rättigheter i C-ITS
Roller och rättigheter i C-ITS definieras, men på ett specifikt sätt. Det är viktigt att skilja på tre nivåer:

:one: Tekniska roller i PKI (EU-CCMS)

:two: Meddelandetyper och funktionella roller

:three: Applikationsroller (t.ex. utryckningsfordon)

## Tekniska roller i PKI (EU-CCMS)
[Rollerna i säkerhets- och certifikatsystemet (EU-CCMS)](secits_domain.md#grundl%C3%A4ggande-struktur-i-eu-ccms) framgår i  Security Policy Release 3.0.

Dessa roller är infrastrukturella roller och inte trafikroller.

## Meddelandetyper och funktionella roller
I C-ITS finns särskilda [meddelandetyper](cits.md#vad-skickas) och flaggor för olika use cases (som i C-ITS kallas *applikationer*), till exempel:
- Emergency and Service Vehicle Notifications – Emergency or Prioritised Vehicle Approaching (ESVN-EPVA)
- Emergency and Service Vehicle Notifications – Slow Moving Maintenance Vehicle (ESVN-SMMV)
- Emergency Vehicle Priority (SI-EVP)
- Traffic Light Prioritisation (SI-TLP)

> [!IMPORTANT]
> Exempelvis innebär ESVN-EPVA att systemet kan signalera att ett fordon är ett utryckningsfordon. Men det är inte en fri roll som man själv deklarerar, snarare **en egenskap som är kopplad till auktoriserade certifikat**.

## Applikationsroller
En applikation i C-ITS-världen (use case) definieras av:
- Ett syfte (t ex: “Emergency Vehicle Approaching”)
- En meddelandetyp (t ex: DENM)
- Specifika fältvärden (t ex: causeCode = emergencyVehicleApproaching)
- Säkerhetsrättigheter (ITS-AID + SSP)

I certifikatet (AT) finns ett fält som heter `ITS-AID` (ITS Application Identifier). Det anger:
- vilka applikationer stationen får använda, och
- vilka [meddelandetyper](cits.md#vad-skickas) den får sända.

Det är alltså inte meddelandet i sig, utan rätten att signera (=använda applikationen) som är säkerhetsstyrd.

SSP (Service Specific Permissions) som också ligger i certifikatet (AT) är den mekanism som gör att två stationer kan ha rätt att sända samma meddelandetyp
men med olika behörighetsnivåer.

> [!IMPORTANT]
> ITS-AID	anger vilken applikation som är tillåten. <br />
> SSP	anger vilka roller/underfunktioner inom applikationen som är tillåtna.

Strukturen förenklat:
```
Authorization Ticket
 ├─ ITS-AID (vilken applikation)
 ├─ SSP (Service Specific Permissions)
 ├─ Validity
 └─ Signature
```

En C-ITS-station (t ex ett blåljusfordon) får ett Enrollment Certificate (EC) samt ett eller flera Authorization Tickets (AT).
Certifikatet AT innehåller:
- Applikationsrättigheter
- Tillåtna meddelandetyper
- Eventuella specialattribut
 
Exempelvis ett blåljusfordon får AT som innehåller:
- ITS-AID för CAM
- ITS-AID för DENM
- SSP för `emergencyVehicleRole` inom DENM
- ITS-AID för SREM
- SSP för `emergencyVehicleRole` inom SREM

Det innebär att fordonet får sända: 
- CAM
- DENM med `Code = emergencyVehicleApproaching` (ESVN-EPVA use case)
- SREM och begära prioritet i signalanläggning 

Medan ett vanligt fordon får AT som innehåller:
- ITS-AID för CAM
- ITS-AID för DENM
- SSP som endast tillåter generering av generiska händelser inom DENM (dvs. saknar emergency-relaterade rättigheter)

Det innebär att fordonet får sända:
- CAM
- vissa DENM (t ex `stationary vehicle`, `slippery road`)

Certifikat (AT) i ett vanligt fordon saknar SSP för `emergencyVehicleRole` samt saknar ITS-AID för SREM (och kan därmed inte sända SREM alls).

## Styrning av roller och rättigheter
Styrning av roller och rättigheter hanteras i tre lager:

:white_check_mark: **ETSI TS 103 097** definierar hur rättigheter kodas i certifikaten.

:white_check_mark: **Certificate Policy** definierar hur rättigheter får utfärdas.

:white_check_mark: **C-ITS domänpolicy** avgör vem som faktiskt får dessa roller och rättigheter.

Om alla fordon kunde sända “jag är ett utryckningsfordon”, då skulle hela systemet kollapsa säkerhetsmässigt. Därför är rollen kryptografiskt skyddad och måste vara auktoriserad av rätt RA/EA/AA – den måste ligga inom korrekt tillitskedja.

EU definierar: meddelandetyper, certifikatstruktur, tillitsmodell och kryptografi samt interoperabilitetskrav.

Medlemsstaten styr den operativa maktstrukturen inom sin C-ITS-domän. Detta innebär att medlemsstaten:
- Fastställer nationell C-ITS-policy
- Utser och styr RA/EA/AA-struktur
- Avgör vilka aktörer som är legitima (t ex blåljus, kollektivtrafik, vägarbeten)
- Beslutar om roll- och SSP-tilldelning
- Ansvarar för riskbedömning och säkerhetsstyrning
- Hanterar incidenter och revokering
- Integrerar C-ITS med nationell lagstiftning och trafikstyrning
- Fastställer operativa prioriteringsregler
- Avgör acceptans av utländska rättigheter inom nationell infrastruktur


<p>&nbsp;</p>

----

:arrow_backward: [Hem](README.md) &nbsp; &nbsp; | &nbsp; &nbsp; :arrow_up_small: [Tillbaka till toppen](#top)  
