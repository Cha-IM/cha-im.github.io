---
title: Sette opp Active Directory
feed: show
date: 20-03-2024
---

Når du har aktivert Windows Server skal vi skal nå sette opp Active Directory. Active Directory er enn tjeneste innebygd i Windows Server for å administrere brukere og datamaskiner i et lokalt nettverk.

Hvis du ikke allerede har koblet opp serveren i nettverket må du gjøre dette:
- Koble WAN-porten på Unifi-ruteren til veggen (dette har du sikkert gjort allerede)
- Koble LAN-porten på Unifi-ruteren til svitsjen (hvilken som helst port)
- Koble klient-PC til svitsjen
- Koble Server-PC til svitsjen

For å sette opp og bruke Active Directory skal vi følge guiden fra NDLA:

1. [Installasjon av serverrolle for Active Directory - Driftsstøtte (IM-ITK vg2) - NDLA](https://ndla.no/r/driftsstotte-im-itk-vg2/datalab-med-windows-server-og-unifi-nettverk/c4391765e8/15076)
2. [Installasjon av DNS-server - Driftsstøtte (IM-ITK vg2) - NDLA](https://ndla.no/r/driftsstotte-im-itk-vg2/datalab-med-windows-server-og-unifi-nettverk/c4391765e8/15077)
3. [Promotere domenekontroller - NDLA](https://ndla.no/r/driftsstotte-im-itk-vg2/datalab-med-windows-server-og-unifi-nettverk/c4391765e8/15078)
4. [Justere domeneadministrator - NDLA](https://ndla.no/r/driftsstotte-im-itk-vg2/datalab-med-windows-server-og-unifi-nettverk/c4391765e8/15079)
5. [Deaktivere eksisterende DHCP-server - NDLA](https://ndla.no/r/driftsstotte-im-itk-vg2/datalab-med-windows-server-og-unifi-nettverk/c4391765e8/15080)
6. [Installere DHCP-server i Windows Server - NDLA](https://ndla.no/r/driftsstotte-im-itk-vg2/datalab-med-windows-server-og-unifi-nettverk/c4391765e8/15081)
7. [Brukerkontoer, grupper og struktur i Active Directory - NDLA](https://ndla.no/r/driftsstotte-im-itk-vg2/datalab-med-windows-server-og-unifi-nettverk/c4391765e8/15082)
8. [Opprette brukerkontoer i AD - NDLA](https://ndla.no/r/driftsstotte-im-itk-vg2/datalab-med-windows-server-og-unifi-nettverk/c4391765e8/15083)
9. Lag en ny Organizational Unit (OU) som heter 'Gjest'. Og lag en bruker som heter 'Gjest'. Gi denne gruppen passende rettigheter som gjest.
10. [Melde en klientmaskin inn i et domene - NDLA](https://ndla.no/r/driftsstotte-im-itk-vg2/datalab-med-windows-server-og-unifi-nettverk/c4391765e8/15084)
