<a name="top"></a>

# Introduktion till MATF – Mutual TLS med ömsesidig autentisering i federativa miljöer
När system-till-system-kommunikation mellan organisationer i allt högre grad sker via API:er och backend-integrationer blir det avgörande att kunna etablera tillit mellan systemen. En vanligt förekommande metod för autentisering och tillitsuppbyggnad bygger på utbyte av kryptografiskt material och användning av mutual TLS (mTLS) där både klient och server autentiserar varandra.

Även om mTLS ger stark kryptografisk autentisering av de kommunicerande parterna, besvarar det inte i sig en grundläggande fråga:  
> Vilka system ska faktiskt betraktas som betrodda och tillåtas ansluta?

Ett giltigt certifikat bevisar innehav av en nyckel, men inte nödvändigtvis att systemet representerar en auktoriserad eller styrd organisation i ett visst sammanhang. Det räcker därför inte att ett system presenterar ett tekniskt giltigt certifikat. Organisationen bakom systemet måste kunna identifieras, vara explicit godkänd och omfattas av styrning och uppföljning på ett kontrollerat sätt.

MATF adresserar denna utmaning i miljöer där flera oberoende organisationer verkar under gemensamma tillitsregler. En sådan miljö benämns här som en *federation*. Inom en federation finns en överenskommen uppsättning deltagare samt en strukturerad beskrivning av deras system.

MATF kopplar denna federativa tillitsmodell direkt till API- och backend-trafik. Varje anslutning knyts till en namngiven medlem i federationen, och motparten verifieras som en godkänd deltagare – inte enbart som ett system med ett giltigt certifikat.

## Vad är MATF?
<mark>Mutually Authenticating TLS in the context of Federations (MATF)</mark> är en mekanism för att kombinera kryptografisk autentisering med federativ tillitshantering i system-till-system-kommunikation mellan organisationer.

Den är utformad för miljöer där flera oberoende aktörer interagerar via API:er och backend-system. I sådana sammanhang måste det vara möjligt att avgöra vilka servrar och klienter som tillhör vilka organisationer – och vilka av dessa som faktiskt är auktoriserade att delta i ett givet tillitssammanhang.

MATF bygger vidare på standardiserad TLS med ömsesidig autentisering (mTLS). Själva TLS-protokollet förändras inte. I stället introducerar MATF ett federativt lager som möjliggör:

- Sammanställning av information om medlemmars servrar och klienter i ett gemensamt metadatadokument  
- Koppling av varje server och klient till en eller flera publika nycklar som används för autentisering  
- Publicering och kryptografisk signering av denna metadata av en federationsoperatör, vilket gör att alla deltagare kan lita på dess integritet och ursprung  

Detta gör det möjligt för system att upptäcka och verifiera motparter baserat på en gemensam, auktoritativ källa, i stället för att varje organisation behöver bygga och underhålla egna tillitskonfigurationer.

## Vilka är fördelarna med MATF?
MATF ger tre centrala effekter: automatisering, förutsägbarhet och kontroll.

:one: Federationsmetadata ger en gemensam och konsekvent bild av deltagande organisationer och de nycklar som är kopplade till deras system  

:two: System kan verifiera sina motparter med hjälp av samma auktoritativa källa för tillitsinformation, vilket eliminerar behovet av lokala tillåtslistor eller miljöspecifika konfigurationer  

:three: När en anslutning etableras kan både klient och server validera varandras nycklar mot federationsmetadata innan trafik tillåts. Detta minskar avsevärt risken för identitetskapning – även från aktörer som presenterar tekniskt giltiga certifikat  

MATF är en federativ mekanism för hur nycklar och anslutningar beskrivs, distribueras och verifieras i distribuerade miljöer där oberoende aktörer kommunicerar direkt.  
Det gör den särskilt värdefull i miljöer som kräver skalbar och tillförlitlig digital samverkan.

## Ett steg mot automatiserad tillit
Med MATF definieras betrodda organisationer och deras tillhörande nycklar i signerad federationsmetadata i stället för att spridas över lokala konfigurationer. Tillit blir därmed en del av den gemensamma infrastrukturen, snarare än något som hanteras ad hoc i enskilda system.

Detta förenklar onboarding av nya medlemmar, nyckelrotation och styrning av åtkomst. Organisationer kan samarbeta mer effektivt och säkert, med minskat beroende av manuella undantag för certifikat och felsökning av tillitskedjor.

<p>&nbsp;</p>

----

:arrow_backward: [Hem](README.md) &nbsp; &nbsp; | &nbsp; &nbsp; :arrow_up_small: [Tillbaka till toppen](#top)  
