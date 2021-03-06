---
title: Konfigurieren der Datensammlung für den Azure Monitor-Agent (Vorschau)
description: ''
ms.topic: conceptual
author: bwren
ms.author: bwren
ms.date: 08/19/2020
ms.openlocfilehash: cd29bfafe2d37b6a34031e6962cc27bfff0006c1
ms.sourcegitcommit: ae6e7057a00d95ed7b828fc8846e3a6281859d40
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/16/2020
ms.locfileid: "92108013"
---
# <a name="configure-data-collection-for-the-azure-monitor-agent-preview"></a>Konfigurieren der Datensammlung für den Azure Monitor-Agent (Vorschau)
Mit Datensammlungsregeln werden die in Azure Monitor eingehenden Daten definiert, und es wird angegeben, wohin sie gesendet werden sollen. In diesem Artikel wird beschrieben, wie Sie eine Datensammlungsregel erstellen, um mit dem Azure Monitor-Agent Daten von virtuellen Computern zu sammeln.

Eine vollständige Beschreibung der Datensammlungsregeln finden Sie unter [Datensammlungsregeln in Azure Monitor (Vorschau)](data-collection-rule-overview.md).

> [!NOTE]
> In diesem Artikel wird beschrieben, wie Sie Daten für virtuelle Computer mit dem Azure Monitor-Agent konfigurieren, der sich derzeit in der Vorschauphase befindet. Eine Beschreibung der allgemein verfügbaren Agents und ihrer Nutzung zum Sammeln von Daten finden Sie unter [Übersicht über Azure Monitor-Agents](agents-overview.md).


## <a name="dcr-associations"></a>Zuordnungen für Datensammlungsregeln
Zum Anwenden einer Datensammlungsregel auf einen virtuellen Computer erstellen Sie eine Zuordnung für den Computer. Ein virtueller Computer kann über eine Zuordnung zu mehreren Datensammlungsregeln verfügen, und einer Datensammlungsregel können mehrere virtuelle Computer zugeordnet sein. Auf diese Weise können Sie eine Gruppe mit Datensammlungsregeln definieren, die jeweils für eine bestimmte Anforderung gelten, und sie dann nur auf die virtuellen Computer anwenden, für die sie gelten. 

Angenommen, in einer Umgebung mit einer Gruppe von virtuellen Computern wird auf einigen eine Branchenanwendung und auf den anderen SQL Server ausgeführt. Unter Umständen verfügen Sie über eine Standard-Datensammlungsregel, die für alle virtuellen Computer gilt, und über separate Datensammlungsregeln, mit denen Daten speziell für die Branchenanwendung und für SQL Server gesammelt werden. Die Zuordnungen der virtuellen Computer zu den Datensammlungsregeln sieht dann in etwa wie im folgenden Diagramm aus.

![Diagramm mit virtuellen Computern, auf denen eine Branchenanwendung und SQL Server gehostet werden. Dazu gehören die Datensammlungsregeln „central-i t-default“ und „lob-app“ für die Branchenanwendung sowie „central-i t-default“ und „s q l“ für SQL Server.](media/data-collection-rule-azure-monitor-agent/associations.png)

## <a name="create-using-the-azure-portal"></a>Erstellen mithilfe des Azure-Portals
Sie können das Azure-Portal verwenden, um eine Datensammlungsregel zu erstellen und dieser Regel unter Ihrem Abonnement virtuelle Computer zuzuordnen. Der Azure Monitor-Agent wird automatisch installiert, und für alle virtuellen Computer wird eine verwaltete Identität erstellt (falls noch nicht geschehen).

Wählen Sie im Portal im Menü **Azure Monitor** unter **Einstellungen** die Option **Datensammlungsregeln** aus. Klicken Sie auf **Hinzufügen**, um eine neue Datensammlungsregel und eine Zuweisung hinzuzufügen.

[![Datensammlungsregeln](media/azure-monitor-agent/data-collection-rules.png)](media/azure-monitor-agent/data-collection-rules.png#lightbox)

Klicken Sie auf **Hinzufügen**, um eine neue Regel und eine Gruppe von Zuordnungen zu erstellen. Geben Sie einen **Regelnamen** und dann ein **Abonnement** und eine **Ressourcengruppe** an. Hiermit wird angegeben, wo die Datensammlungsregel erstellt wird. Die virtuellen Computer und ihre Zuordnungen können unter einem beliebigen Abonnement bzw. einer Ressourcengruppe auf dem Mandanten angeordnet sein.

[![Grundlagen von Datensammlungsregeln](media/azure-monitor-agent/data-collection-rule-basics.png)](media/azure-monitor-agent/data-collection-rule-basics.png#lightbox)

Fügen Sie auf der Registerkarte **Virtuelle Computer** virtuelle Computer hinzu, für die die Datensammlungsregel angewendet werden sollte. Der Azure Monitor-Agent wird auf virtuellen Computern installiert, auf denen dies noch nicht durchgeführt wurde.

[![Datensammlungsregeln für virtuelle Computer](media/azure-monitor-agent/data-collection-rule-virtual-machines.png)](media/azure-monitor-agent/data-collection-rule-virtual-machines.png#lightbox)

Klicken Sie auf der Registerkarte **Sammeln und übermitteln** auf **Datenquelle hinzufügen**, um eine Datenquelle und einen Zielsatz hinzuzufügen. Wählen Sie einen **Datenquellentyp** aus. Die entsprechenden Details für die Auswahl werden angezeigt. Für Leistungsindikatoren können Sie eine Auswahl aus einer Gruppe mit Objekten mit der zugehörigen Stichprobenhäufigkeit treffen. Für Ereignisse können Sie bestimmte Protokolle bzw. entsprechende Funktionen und den Schweregrad auswählen. 

[![Einfache Datenquelle](media/azure-monitor-agent/data-collection-rule-data-source-basic.png)](media/azure-monitor-agent/data-collection-rule-data-source-basic.png#lightbox)


Wählen Sie **Benutzerdefiniert** aus, um andere Protokolle und Leistungsindikatoren anzugeben. Anschließend können Sie einen [XPath](https://www.w3schools.com/xml/xpath_syntax.asp) für bestimmte Werte angeben, die gesammelt werden sollen. Beispiele hierzu finden Sie unter [Beispiel für eine Datensammlungsregel](data-collection-rule-overview.md#sample-data-collection-rule).

[![Datenquelle: Benutzerdefiniert](media/azure-monitor-agent/data-collection-rule-data-source-custom.png)](media/azure-monitor-agent/data-collection-rule-data-source-custom.png#lightbox)

Fügen Sie auf der Registerkarte **Ziel** mindestens ein Ziel für die Datenquelle hinzu. Für Windows-Ereignis- und Syslog-Datenquellen ist nur das Senden an Azure Monitor-Protokolle möglich. Bei Leistungsindikatoren ist sowohl das Senden an Azure Monitor-Metriken als auch an Azure Monitor-Protokolle möglich.

[![Destination](media/azure-monitor-agent/data-collection-rule-destination.png)](media/azure-monitor-agent/data-collection-rule-destination.png#lightbox)

Klicken Sie auf **Datenquelle hinzufügen** und dann auf **Bewerten + erstellen**, um die Details der Datensammlungsregel und die Zuordnung zur Gruppe mit den VMs zu überprüfen. Klicken Sie auf **Erstellen**, um die Erstellung durchzuführen.

> [!NOTE]
> Nachdem die Datensammlungsregel und die Zuordnungen erstellt wurden, kann es bis zu fünf Minuten dauern, bis Daten an die Ziele gesendet werden.

## <a name="create-using-rest-api"></a>Erstellen mithilfe der REST-API
Führen Sie die folgenden Schritte aus, um mithilfe der Rest-API einen DCR und Zuordnungen zu erstellen.  
1. 1.
2.  Erstellen Sie die DCR-Datei manuell im JSON-Format, das im  [Beispiel einer Datensammlungsregel](data-collection-rule-overview.md#sample-data-collection-rule) gezeigt wird.
3. 2.

## <a name="next-steps"></a> Erstellen Sie die Regel mithilfe der  [Rest-API](/rest/api/monitor/datacollectionrules/create#examples).

- 3.
-  Richten Sie mithilfe der [Rest-API](/rest/api/monitor/datacollectionruleassociations/create#examples) für jeden virtuellen Computer eine Zuordnung zur Datensammlungsregel ein.