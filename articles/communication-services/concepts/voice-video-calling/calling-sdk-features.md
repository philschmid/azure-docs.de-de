---
title: Übersicht über die Clientbibliothek für Telefonie von Azure Communication Services
titleSuffix: An Azure Communication Services concept document
description: Hier finden Sie eine Übersicht über die Clientbibliothek für Telefonie.
author: mikben
manager: jken
services: azure-communication-services
ms.author: mikben
ms.date: 09/30/2020
ms.topic: overview
ms.service: azure-communication-services
ms.openlocfilehash: 44365dec247b9f3135a090cee397cad32598fd29
ms.sourcegitcommit: d103a93e7ef2dde1298f04e307920378a87e982a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2020
ms.locfileid: "91977866"
---
# <a name="calling-client-library-overview"></a>Übersicht über die Clientbibliothek für Telefonie

[!INCLUDE [Public Preview Notice](../../includes/public-preview-include.md)]

Es gibt zwei separate Familien von Clientbibliotheken für Telefonie: eine für *Clients* und eine für *Dienste* . Die aktuell verfügbaren Clientbibliotheken sind für Endbenutzerumgebungen (Websites und native Apps) vorgesehen.

Die Clientbibliotheken für Dienste sind noch nicht verfügbar und ermöglichen den Zugriff auf unformatierte Sprach- und Videodaten für die Integration in Bots und andere Diensten.

## <a name="calling-client-library-capabilities"></a>Funktionen der Clientbibliothek für Telefonie

Die folgende Liste enthält die Features, die aktuell in den Clientbibliotheken für Telefonie von Communication Services verfügbar sind:

| Featuregruppe | Funktion                                                                                                          | JS  | Java (Android) | Objective-C (iOS) 
| ----------------- | ------------------------------------------------------------------------------------------------------------------- | ---  | -------------- | -------------
| Grundlegende Funktionen | Tätigen eines 1:1-Anrufs zwischen zwei Benutzern                                                                           | ✔️   | ✔️            | ✔️  
|                   | Tätigen eines Gruppenanrufs zwischen mehr als zwei Benutzern (bis zu 350 Benutzer)                                                       | ✔️   | ✔️            | ✔️ 
|                   | Höherstufen eines 1:1-Anrufs mit zwei Benutzern zu einem Gruppenanruf mit mehr als zwei Benutzern                                 | ✔️   | ✔️            | ✔️ 
|                   | Beitreten zu einem bereits gestarteten Gruppenanruf                                                                              | ✔️   | ✔️            | ✔️ 
|                   | Einladen eines weiteren VoIP-Teilnehmers zu einem laufenden Gruppenanruf                                                       | ✔️   | ✔️            | ✔️
|                   | Aktivieren/Deaktivieren Ihres Videos                                                         | ✔️   | ✔️            | ✔️ 
|                   | Stummschalten des Mikrofons/Aufheben der Stummschaltung                                                                                                     | ✔️   | ✔️            | ✔️         
|                   | Wechseln zwischen Kameras                                                                                              | ✔️   | ✔️            | ✔️           
|                   | Lokales Halten/Aufheben des Haltens                                                                                                  | ✔️   | ✔️            | ✔️           
|                   | Aktiver Lautsprecher                                                                                                      | ✔️   | ✔️            | ✔️           
|                   | Auswählen des Lautsprechers für Anrufe                                                                                            | ✔️   | ✔️            | ✔️           
|                   | Auswählen des Mikrofons für Anrufe                                                                                         | ✔️   | ✔️            | ✔️           
|                   | Anzeigen des Status eines Teilnehmers<br/>*Beschäftigt, Early Media, Verbindungsaufbau, Verbunden, Gehalten, Im Wartebereich, Getrennt*         | ✔️   | ✔️            | ✔️           
|                   | Anzeigen des Zustands eines Anrufs<br/>*Early Media, Eingehend, Verbindungsaufbau, Klingeln, Verbunden, Halten, Trennung, Getrennt* | ✔️   | ✔️            | ✔️           
|                   | Anzeigen, ob ein Teilnehmer stummgeschaltet ist                                                                                      | ✔️   | ✔️            | ✔️           
|                   | Anzeigen des Grunds, warum ein Teilnehmer einen Anruf verlassen hat                                                                       | ✔️   | ✔️            | ✔️     
| Bildschirmfreigabe    | Freigeben des gesamten Bildschirms innerhalb der Anwendung                                                                 | ✔️   | ❌            | ❌           
|                   | Freigeben einer bestimmten Anwendung (aus der Liste aktiver Anwendungen)                                                | ✔️   | ❌            | ❌           
|                   | Freigeben eines Webbrowsertabs aus der Liste geöffneter Tabs                                                                  | ✔️   | ❌            | ❌           
|                   | Anzeigen von Remotebildschirmfreigabe durch Teilnehmer                                                                            | ✔️   | ✔️            | ✔️         
| Liste            | Auflisten von Teilnehmern                                                                                                   | ✔️   | ✔️            | ✔️           
|                   | Entfernen eines Teilnehmers                                                                                                | ✔️   | ✔️            | ✔️         
| PSTN              | Tätigen eines 1:1-Anrufs mit einem PSTN-Teilnehmer                                                                     | ✔️   | ✔️            | ✔️   
|                   | Tätigen eines Gruppenanrufs mit PSTN-Teilnehmern                                                                           | ✔️   | ✔️            | ✔️
|                   | Höherstufen eines 1:1-Anrufs mit einem PSTN-Teilnehmer zu einem Gruppenanruf                                                 | ✔️   | ✔️            | ✔️
|                   | Verlassen eines Gruppenanrufs als PSTN-Teilnehmer                                                                    | ✔️   | ✔️            | ✔️   
| Allgemein           | Testen von Mikrofon, Lautsprecher und Kamera mit einem Audiotestdienst (verfügbar durch Anrufen von 8:echo123)                   |  ✔️  | ✔️            | ✔️   

## <a name="calling-client-library-browser-support"></a>Browserunterstützung der Clientbibliothek für Telefonie

Die folgende Tabelle enthält die unterstützten Browser und Versionen, die derzeit verfügbar sind:

|                                  | Windows          | macOS          | Ubuntu | Linux  | Android | iOS    |
| -------------------------------- | ---------------- | -------------- | ------- | ------ | ------ | ------ |
| **Clientbibliothek für Telefonie** | Chrome*, Microsoft Edge (neu) | Chrome *, Safari** | Chrome*  | Chrome* | Chrome* | Safari** |


\* Hinweis: Neben den beiden vorherigen Releases wird auch die neueste Version von Chrome unterstützt.<br/>

** Hinweis: Safari wird ab Version 13.1 unterstützt. Ausgehende Videodaten werden für Safari macOS noch nicht unterstützt, für iOS dagegen schon. Die ausgehende Bildschirmfreigabe wird in der Desktopversion von iOS unterstützt.

## <a name="next-steps"></a>Nächste Schritte

> [!div class="nextstepaction"]
> [Erste Schritte mit Anrufen](../../quickstarts/voice-video-calling/getting-started-with-calling.md)

Weitere Informationen finden Sie in den folgenden Artikeln:
- Machen Sie sich mit allgemeinen [Anrufflows](../call-flows.md) vertraut.
- Informieren Sie sich über [Anruftypen](../voice-video-calling/about-call-types.md).
- [Planen Sie Ihre PSTN-Lösung.](../telephony-sms/plan-solution.md)
