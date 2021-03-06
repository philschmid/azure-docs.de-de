---
title: Vorschlagssuche für Suchbegriffe – Bing-Websuche-API
titleSuffix: Azure Cognitive Services
description: Durch Verbinden der Bing-Websuche-API mit der Bing-Vorschlagssuche-API können Sie eine verbesserte Suchoberfläche für Benutzer bereitstellen.
services: cognitive-services
author: aahill
manager: nitinme
ms.service: cognitive-services
ms.subservice: bing-web-search
ms.topic: conceptual
ms.date: 03/03/2019
ms.author: aahi
ms.openlocfilehash: 5bd5ff0e49b125277255ec8e5c216583d75043a0
ms.sourcegitcommit: 8a1ba1ebc76635b643b6634cc64e137f74a1e4da
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2020
ms.locfileid: "94381132"
---
# <a name="autosuggest-bing-search-terms-in-your-application"></a>Bing-Vorschlagssuche für Suchbegriffe in Ihrer Anwendung

> [!WARNING]
> Die APIs der Bing-Suche werden von Cognitive Services auf Bing-Suchdienste umgestellt. Ab dem **30. Oktober 2020** müssen alle neuen Instanzen der Bing-Suche mit dem [hier](https://aka.ms/cogsvcs/bingmove) dokumentierten Prozess bereitgestellt werden.
> APIs der Bing-Suche, die mit Cognitive Services bereitgestellt wurden, werden noch drei Jahre lang bzw. bis zum Ablauf Ihres Enterprise Agreement unterstützt (je nachdem, was zuerst geschieht).
> Eine Anleitung zur Migration finden Sie unter [Bing-Suchdienste](https://aka.ms/cogsvcs/bingmigration).

Wenn Sie ein Suchfeld bereitstellen, in das Benutzer ihre Suchbegriffe eingeben, verwenden Sie die [Bing-Vorschlagssuche-API](../bing-autosuggest/get-suggested-search-terms.md), um die Benutzerfreundlichkeit zu verbessern. Die API gibt vorgeschlagene Abfragezeichenfolgen zurück, während der Benutzer einen Suchbegriff eingibt.

Nachdem der Benutzer einen Suchbegriff eingegeben hat, muss dieser vor dem Festlegen des Abfrageparameters [q](/rest/api/cognitiveservices-bingsearch/bing-web-api-v7-reference#query) URL-codiert werden. Wenn der Benutzer also beispielsweise *sailing dinghies* eingibt, legen Sie `q` auf `sailing+dinghies` oder `sailing%20dinghies` fest.

Wenn der Abfragebegriff einen Rechtschreibfehler enthält, umfasst die Suchantwort ein [QueryContext](/rest/api/cognitiveservices-bingsearch/bing-web-api-v7-reference#querycontext)-Objekt. Das Objekt zeigt die ursprüngliche Schreibweise und die korrigierte Schreibweise, die Bing für die Suche verwendet hat.

```json
"queryContext": {
    "originalQuery": "sialing dingy for sale",
    "alteredQuery": "sailing dinghy for sale",
    "alterationOverrideQuery": "+sialing +dingy for sale"
}
```

Diese Informationen können beim Anzeigen der Suchergebnisse verwendet werden, um Benutzer wissen zu lassen, dass die Abfragezeichenfolge geändert wurde.

![Beispielbenutzeroberfläche zum Abfragekontext](./media/cognitive-services-bing-web-api/bing-query-context.PNG)  

## <a name="next-steps"></a>Nächste Schritte  

* Sehen Sie sich das Beispiel [Antworten der Bing-Websuche-API](search-responses.md) an.  

## <a name="see-also"></a>Weitere Informationen  

* [Referenz zur Bing-Websuche-API](/rest/api/cognitiveservices-bingsearch/bing-web-api-v7-reference)