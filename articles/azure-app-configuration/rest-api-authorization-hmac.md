---
title: 'Azure App Configuration-REST-API: HMAC-Autorisierung'
description: Verwenden von HMAC zur Autorisierung in Azure App Configuration über die REST-API
author: lisaguthrie
ms.author: lcozzens
ms.service: azure-app-configuration
ms.topic: reference
ms.date: 08/17/2020
ms.openlocfilehash: 8d1f8a17f51711cc5c10567797e1224f96eb7630
ms.sourcegitcommit: 7cc10b9c3c12c97a2903d01293e42e442f8ac751
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2020
ms.locfileid: "93423714"
---
# <a name="hmac-authorization---rest-api-reference"></a>HMAC-Autorisierung: REST-API-Referenz

Wenn die HMAC-Authentifizierung verwendet wird, fallen Vorgänge in eine der folgenden beiden Kategorien: Lesen oder Schreiben. Schlüssel für Lese-/Schreibzugriff gewähren die Berechtigung zum Aufrufen aller Vorgänge. Schlüssel für schreibgeschützten Zugriff gewähren nur die Berechtigung zum Aufrufen von Lesevorgängen. Ob ein Zugriffsschlüssel schreibgeschützten Zugriff oder Lese-/Schreibzugriff gewährt, wird von der Eigenschaft `readOnly` bestimmt. Jeder Versuch einer Schreibanforderung mit einem schreibgeschützten Zugriffsschlüssel führt dazu, dass die Anforderung nicht autorisiert wird.

## <a name="obtaining-access-keys"></a>Abrufen von Zugriffsschlüsseln

Die Spezifikation mit der Beschreibung von Zugriffsschlüsseln und der zum Abrufen der Schlüssel verwendeten API finden Sie [hier](https://github.com/Azure/azure-rest-api-specs/blob/master/specification/appconfiguration/resource-manager/Microsoft.AppConfiguration/stable/2019-10-01/appconfiguration.json) in den Azure App Configuration-Ressourcenanbieterdetails. Zugriffsschlüssel werden über den Vorgang „ConfigurationStores_ListKeys“ abgerufen.

## <a name="errors"></a>Errors

```http
HTTP/1.1 403 Forbidden
```

**Grund:** Der zum Authentifizieren der Anforderung verwendete Zugriffsschlüssel bietet nicht die erforderlichen Berechtigungen, um den angeforderten Vorgang auszuführen.
**Lösung:** Rufen Sie einen Zugriffsschlüssel ab, der die Berechtigung zum Ausführen des angeforderten Vorgangs bereitstellt, und verwenden Sie diesen zum Authentifizieren der Anforderung.
