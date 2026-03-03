# Roller och behörigheter i C-ITS
Roller och behörigheter i C-ITS definieras men på ett specifikt sätt. Det är viktigt att skilja på tre nivåer:

:one: Tekniska roller i PKI / EU CCMS

:two: Meddelandetyper och funktionella roller

:three: Applikationsroller (t.ex. utryckningsfordon)

## Tekniska roller i PKI / EU CCMS
[Rollerna i säkerhets- och certifikatsystemet (EU CCMS)](secits_domain.md#grundl%C3%A4ggande-struktur-i-eu-ccms) framgår i  Security Policy Release 3.0.

Dessa roller är infrastrukturella roller och inte trafikroller.

## Meddelandetyper och funktionella roller
I C-ITS finns särskilda meddelandetyper och flaggor, såsom:
- Emergency Vehicle Alert (EVA)
- Road Works Warning (RWW)
- Public Transport Priority
- Special Transport
- Dangerous Goods

> [!IMPORTANT]
> Exempelvis innebär EVA att systemet kan signalera att ett fordon är ett utryckningsfordon. Men det är inte en fri roll som man själv deklarerar, snarare **en egenskap som är kopplad till auktoriserade certifikat**.
