---
title: 'Azure ExpressRoute: Verbindungen und Peering'
description: Diese Seite enthält eine Übersicht über ExpressRoute-Verbindungen und Routingdomänen/Peering.
services: expressroute
author: duongau
ms.service: expressroute
ms.topic: conceptual
ms.date: 12/13/2019
ms.author: duau
ms.openlocfilehash: 87fed1d2ac4f5fa85c01d7af10bec10c1412744f
ms.sourcegitcommit: 957c916118f87ea3d67a60e1d72a30f48bad0db6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/19/2020
ms.locfileid: "92202343"
---
# <a name="expressroute-circuits-and-peering"></a>ExpressRoute-Verbindungen und Peering

Über ExpressRoute-Verbindungen wird Ihre lokale Infrastruktur über einen Konnektivitätsanbieter mit Microsoft verbunden. In diesem Artikel werden ExpressRoute-Verbindungen und Routingdomänen/Peering erläutert. Die folgende Abbildung zeigt eine logische Darstellung der Konnektivität zwischen Ihrem WAN und Microsoft.

![Diagramm, das zeigt, wie über ExpressRoute-Verbindungen Ihre lokale Infrastruktur über einen Konnektivitätsanbieter mit Microsoft verbunden wird](./media/expressroute-circuit-peerings/expressroute-basic.png)

> [!IMPORTANT]
> Öffentliches Azure-Peering wurde als veraltet markiert und ist für neue ExpressRoute-Leitungen nicht verfügbar. Neue Leitungen unterstützen Microsoft-Peering und privates Peering.  
>

## <a name="expressroute-circuits"></a><a name="circuits"></a>ExpressRoute-Verbindungen

Eine ExpressRoute-Verbindung stellt eine logische Verbindung zwischen der lokalen Infrastruktur und den Microsoft-Clouddiensten über einen Konnektivitätsanbieter dar. Sie können mehrere ExpressRoute-Verbindungen bestellen. Alle Verbindungen können sich in derselben Region oder in verschiedenen Regionen befinden und über verschiedene Konnektivitätsanbieter mit dem jeweiligen Standort verbunden sein.

ExpressRoute-Verbindungen werden keinen physischen Entitäten zugeordnet. Eine Verbindung wird eindeutig durch eine Standard-GUID, einen sogenannten Dienstschlüssel, identifiziert. Der Dienstschlüssel ist die einzige Information, die zwischen Microsoft, dem Konnektivitätsanbieter und Ihnen ausgetauscht wird. Der Dienstschlüssel unterliegt aus Sicherheitsgründen nicht der Geheimhaltung. Zwischen einer ExpressRoute-Verbindung und dem Dienstschlüssel besteht eine 1:1-Zuordnung.

Neue ExpressRoute-Verbindungen können zwei unabhängige Peerings aufweisen: privates Peering und Microsoft-Peering. Bestehende ExpressRoute-Verbindungen können im Gegensatz dazu bis zu drei unabhängige Peerings aufweisen: öffentliches Azure-Peering, privates Azure-Peering und Microsoft-Peering. Jedes Peering besteht aus einem Paar unabhängiger BGP-Sitzungen, die für Hochverfügbarkeit jeweils redundant konfiguriert sind. Zwischen einer ExpressRoute-Verbindung und Routingdomänen besteht eine 1:N-Zuordnung (1 <= N <= 3). Für eine ExpressRoute-Verbindung können einzelne, zwei oder alle drei Peerings pro ExpressRoute-Verbindung aktiviert sein.

Jede Verbindung verfügt über eine feste Bandbreite (50 MBit/s, 100 MBit/s, 200 MBit/s, 500 MBit/s, 1 GBit/s, 10 GBit/s) und ist einem Konnektivitätsanbieter und einem Peeringstandort zugewiesen. Die ausgewählte Bandbreite wird von allen Peerings der Verbindung gemeinsam genutzt.

### <a name="quotas-limits-and-limitations"></a><a name="quotas"></a>Kontingente, Grenzwerte und Einschränkungen

Standardkontingente und -grenzwerte gelten für alle ExpressRoute-Verbindungen. Aktuelle Informationen zu Kontingenten finden Sie auf der Seite [Grenzwerte, Kontingente und Einschränkungen für Azure-Abonnements und -Dienste](../azure-resource-manager/management/azure-subscription-service-limits.md) .

## <a name="expressroute-peering"></a><a name="routingdomains"></a>ExpressRoute-Peering

Einer ExpressRoute-Verbindung sind mehrere Routingdomänen/Peerings zugeordnet: öffentliche oder private Azure-Routingdomänen/-Peerings sowie Microsoft-Routingdomänen/-Peerings. Alle Peerings sind für Hochverfügbarkeit auf einem Routerpaar identisch konfiguriert (mit einer Aktiv/Aktiv-Konfiguration oder einer Nutzlastverteilungskonfiguration). Azure-Dienste sind zur Darstellung der IP-Adressierungsschemas als *Azure – Öffentlich* und *Azure – Privat* kategorisiert.

![Diagramm, das zeigt, wie öffentliche und private Azure-Dienste sowie Microsoft-Peerings in einer ExpressRoute-Verbindung konfiguriert werden](./media/expressroute-circuit-peerings/expressroute-peerings.png)

### <a name="azure-private-peering"></a><a name="privatepeering"></a>Privates Azure-Peering:

Azure-Computedienste, sprich virtuelle Computer (IaaS) und Clouddienste (PaaS), die in einem virtuellen Netzwerk bereitgestellt werden, können über die private Peeringdomäne verbunden werden. Die private Peeringdomäne gilt als vertrauenswürdige Erweiterung Ihres Kernnetzwerks für Microsoft Azure. Sie können eine bidirektionale Verbindung zwischen Ihrem Kernnetzwerk und den virtuellen Azure-Netzwerken (VNets) einrichten. Durch dieses Peering können Sie direkt über ihre privaten IP-Adressen eine Verbindung zwischen virtuellen Computern und Clouddiensten herstellen.  

Sie können mehr als ein virtuelles Netzwerk mit der privaten Peeringdomäne verbinden. Informationen zu Grenzwerten und Einschränkungen finden Sie auf der [FAQ-Seite](expressroute-faqs.md) . Aktuelle Informationen zu Grenzwerten finden Sie auf der Seite [Grenzwerte, Kontingente und Einschränkungen für Azure-Abonnements und -Dienste](../azure-resource-manager/management/azure-subscription-service-limits.md) .  Ausführliche Informationen zur Routingkonfiguration finden Sie unter [Routing](expressroute-routing.md) .

### <a name="microsoft-peering"></a><a name="microsoftpeering"></a>Microsoft-Peering

[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

Verbindungen mit Onlinediensten von Microsoft (Microsoft 365 und Azure-PaaS-Dienste) erfolgen per Microsoft-Peering. Über die Peeringrouting-Domäne von Microsoft ermöglichen wir eine bidirektionale Konnektivität zwischen Ihrem WAN und den Microsoft-Clouddiensten. Sie dürfen nur über öffentliche IP-Adressen, die Ihnen oder Ihrem Konnektivitätsanbieter gehören, eine Verbindung mit den Microsoft-Clouddiensten herstellen und müssen alle definierten Regeln einhalten. Weitere Informationen finden Sie auf der Seite [ExpressRoute-Voraussetzungen](expressroute-prerequisites.md).

Auf der [FAQ-Seite](expressroute-faqs.md) finden Sie weitere Informationen zu unterstützten Diensten, Kosten und Konfigurationsdetails. Auf der Seite [ExpressRoute-Standorte](expressroute-locations.md) finden Sie Informationen zur Liste der Konnektivitätsanbieter, die Microsoft-Peeringsupport anbieten.

## <a name="peering-comparison"></a><a name="peeringcompare"></a>Peeringvergleich

In der folgenden Tabelle werden die drei Peerings verglichen:

[!INCLUDE [peering comparison](../../includes/expressroute-peering-comparison.md)]

Sie können mehrere Routingdomänen als Teil der ExpressRoute-Verbindung aktivieren. Sie können alle Routingdomänen durch das gleiche VPN leiten, wenn sie diese zu einer einzelnen Routingdomäne zusammenführen möchten. Sie können sie auch getrennt halten, ähnlich wie im Diagramm. Die empfohlene Konfiguration sieht folgendermaßen aus: Das private Peering ist direkt mit dem Kernnetzwerk verbunden, und die öffentlichen Peeringlinks und die Microsoft-Peeringlinks sind mit Ihrer DMZ verbunden.

Jedes Peering erfordert separate BGP-Sitzungen (ein Sitzungspaar für jeden Peeringtyp). Die BGP-Sitzungspaare bieten einen hoch verfügbaren Link. Wenn Sie die Verbindung über Layer-2-Konnektivitätsanbieter herstellen, sind Sie für das Konfigurieren und Verwalten des Routings verantwortlich. Weitere Informationen erhalten Sie, wenn Sie sich [Workflows](expressroute-workflows.md) zum Einrichten von ExpressRoute anschauen.

## <a name="expressroute-health"></a><a name="health"></a>ExpressRoute-Integrität

ExpressRoute-Leitungen können mit dem [Netzwerkleistungsmonitor](../networking/network-monitoring-overview.md) auf Verfügbarkeit, Konnektivität zu VNETs und Bandbreitennutzung überwacht werden.

Der Netzwerkleistungsmonitor überwacht die Integrität von privatem Azure-Peering und Microsoft-Peering. Weitere Informationen finden Sie in unserem [Blogbeitrag](https://azure.microsoft.com/blog/monitoring-of-azure-expressroute-in-preview/).

## <a name="next-steps"></a>Nächste Schritte

* Suchen Sie nach einem Service Provider. Informationen finden Sie unter [ExpressRoute-Dienstanbieter und -Standorte](expressroute-locations.md).
* Stellen Sie sicher, dass alle Voraussetzungen erfüllt sind. Informationen finden Sie unter [ExpressRoute-Voraussetzungen](expressroute-prerequisites.md).
* Konfigurieren Sie Ihre ExpressRoute-Verbindung.
  * [Erstellen und Verwalten von ExpressRoute-Verbindungen](expressroute-howto-circuit-portal-resource-manager.md)
  * [Konfigurieren des Routings (Peering) für ExpressRoute-Verbindungen](expressroute-howto-routing-portal-resource-manager.md)