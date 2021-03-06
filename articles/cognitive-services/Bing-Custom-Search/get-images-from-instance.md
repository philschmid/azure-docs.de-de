---
title: Abrufen von Bildern aus der benutzerdefinierten Ansicht – Benutzerdefinierte Bing-Suche
titleSuffix: Azure Cognitive Services
description: Hier finden Sie eine allgemeine Übersicht über das Abrufen von Bildern aus Ihrer benutzerdefinierten Ansicht im Web mithilfe der benutzerdefinierten Bing-Suche.
services: cognitive-services
author: swhite-msft
manager: nitinme
ms.service: cognitive-services
ms.subservice: bing-custom-search
ms.topic: conceptual
ms.date: 09/10/2018
ms.author: scottwhi
ms.openlocfilehash: c29e83f7851bc9be1688f3828373942c0e31f4ef
ms.sourcegitcommit: 22da82c32accf97a82919bf50b9901668dc55c97
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/08/2020
ms.locfileid: "94367467"
---
# <a name="get-images-from-your-custom-view"></a>Abrufen von Bildern aus der benutzerdefinierten Ansicht

> [!WARNING]
> Die APIs der Bing-Suche werden von Cognitive Services auf Bing-Suchdienste umgestellt. Ab dem **30. Oktober 2020** müssen alle neuen Instanzen der Bing-Suche mit dem [hier](https://aka.ms/cogsvcs/bingmove) dokumentierten Prozess bereitgestellt werden.
> APIs der Bing-Suche, die mit Cognitive Services bereitgestellt wurden, werden noch drei Jahre lang bzw. bis zum Ablauf Ihres Enterprise Agreement unterstützt (je nachdem, was zuerst geschieht).
> Eine Anleitung zur Migration finden Sie unter [Bing-Suchdienste](https://aka.ms/cogsvcs/bingmigration).

Mit der benutzerdefinierten Bing-Bildersuche stehen Ihnen erweiterte Funktionen für die benutzerdefinierte Suche zur Verfügung. Ähnlich wie bei Webergebnissen wird bei der benutzerdefinierten Suche das Suchen nach Bildern in der Websiteliste in Ihrer Instanz ermöglicht. Sie können die Bilder mithilfe der Bing-API für die benutzerdefinierte Bildersuche oder über das Feature für die gehostete Benutzeroberfläche abrufen. Das Feature für die gehostete Benutzeroberfläche ist benutzerfreundlich und wird für die schnelle Einrichtung Ihrer Suchumgebung empfohlen.  Informationen zum Konfigurieren der gehosteten Benutzeroberfläche zum Berücksichtigen von Bilder finden Sie unter [Konfigurieren der gehosteten Benutzeroberfläche](hosted-ui.md).

Wenn Sie die Anzeige von Suchergebnissen präziser steuern möchten, können Sie die Bing-API für die benutzerdefinierte Bildersuche verwenden. Die Vorgehensweise zum Aufrufen der API ähnelt dem Aufrufen der Bing-Bildersuche-API. Sehen Sie sich daher die Beispiele zum Aufrufen der API unter [Was ist die Bing-Bildersuche?](../Bing-Image-Search/overview.md) an. Machen Sie sich zuvor jedoch mit dem Inhalt in der Referenz zur [API für die benutzerdefinierte Bildersuche](/rest/api/cognitiveservices-bingsearch/bing-custom-images-api-v7-reference) vertraut. Sie unterscheiden sich hauptsächlich in Bezug auf die unterstützten Abfrageparameter (Abfrageparameter „customConfig“ ist erforderlich) und den Endpunkt, an den Sie Anforderungen senden.

<!--
## Next steps

[Call your custom view](search-your-custom-view.md)
-->