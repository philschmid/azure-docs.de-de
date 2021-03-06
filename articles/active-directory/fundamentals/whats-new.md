---
title: Neuigkeiten Versionshinweise – Azure Active Directory | Microsoft-Dokumentation
description: Hier finden Sie Informationen zu den Neuerungen in Azure Active Directory, z. B. aktuelle Versionshinweise, bekannte Probleme, Fehlerbehebungen, veraltete Funktionen und anstehende Änderungen.
services: active-directory
author: ajburnle
manager: daveba
featureFlags:
- clicktale
ms.assetid: 06a149f7-4aa1-4fb9-a8ec-ac2633b031fb
ms.service: active-directory
ms.subservice: fundamentals
ms.workload: identity
ms.topic: conceptual
ms.date: 10/30/2020
ms.author: ajburnle
ms.reviewer: dhanyahk
ms.custom: it-pro
ms.collection: M365-identity-device-management
ms.openlocfilehash: 74cb1e021049b7c36c4c23f2e9a6a7512fba1110
ms.sourcegitcommit: 4b76c284eb3d2b81b103430371a10abb912a83f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/01/2020
ms.locfileid: "93146132"
---
# <a name="whats-new-in-azure-active-directory"></a>Neuerungen in Azure Active Directory

>Lassen Sie sich über Updates auf dieser Seite benachrichtigen, indem Sie die URL `https://docs.microsoft.com/api/search/rss?search=%22Release+notes+-+Azure+Active+Directory%22&locale=en-us` kopieren und in Ihren ![RSS-Symbol](./media/whats-new/feed-icon-16x16.png)-Feedreader einfügen.

Es werden fortlaufend Verbesserungen an Azure AD vorgenommen. Damit Sie bezüglich der neuesten Entwicklungen auf dem neuesten Stand bleiben, bietet dieser Artikel Informationen zu Folgendem:

- Neueste Versionen
- Bekannte Probleme
- Behebung von Programmfehlern
- Veraltete Funktionen
- Pläne für Änderungen

Besuchen Sie regelmäßig diese Seite. Diese wird monatlich aktualisiert. Wenn Sie nach Elementen suchen, die älter als sechs Monate sind, können Sie sie im [Archiv zu den Neuerungen in Azure Active Directory](whats-new-archive.md) finden.

---
## <a name="october-2020"></a>Oktober 2020

### <a name="azure-ad-on-premises-hybrid-agents-impacted-by-azure-tls-certificate-changes"></a>Lokale Azure AD-Hybrid-Agents von TLS-Zertifikatänderungen für Azure betroffen

**Typ:** Plan für Änderung  
**Dienstkategorie:** –  
**Produktfunktion** : Plattform

Microsoft aktualisiert Azure-Dienste für die Verwendung von TLS-Zertifikaten aus einer anderen Gruppe von Stammzertifizierungsstellen (Certificate Authorities, CAs). Diese Aktualisierung war notwendig, da die aktuellen Zertifikate der Zertifizierungsstellen eine der grundlegenden Anforderungen des Zertifizierungsstellen-/Browserforums nicht erfüllen. Diese Änderung wirkt sich auf lokal installierte Azure AD-Hybrid-Agents aus, die in festgeschriebenen Umgebungen mit einer festen Liste von Stammzertifikaten verwendet werden und so aktualisiert werden müssen, dass die neuen Zertifikataussteller als vertrauenswürdig eingestuft werden.

Diese Änderung führt zu einer Dienstunterbrechung, wenn Sie nicht sofort Maßnahmen ergreifen. Diese Agents umfassen [Anwendungsproxyconnectors](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/AppProxy) für den Remotezugriff auf die lokale Bereitstellung, [Pass-Through-Authentifizierungs-Agents](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/AzureADConnect), über die sich Ihre Benutzer mit denselben Kennwörtern bei Anwendungen anmelden können, und Agents für die [Vorschau für Cloudbereitstellung](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/AzureADConnect), die die Synchronisierung von AD mit Azure AD durchführen. 

Wenn in Ihrer Umgebung Firewallregeln festgelegt wurden, die dazu führen, dass ausgehende Aufrufe nur für bestimmte CRL-Downloads (Certificate Revocation List, Zertifikatssperrliste) zugelassen werden, müssen Sie die folgenden CRL- und OCSP-URLs zulassen. Vollständige Informationen zu der Änderung und den CRL- und OCSP-URLs, auf die der Zugriff ermöglicht wird, finden Sie unter [TLS-Zertifikatänderungen für Azure](../../security/fundamentals/tls-certificate-changes.md).

---

### <a name="provisioning-events-will-be-removed-from-audit-logs-and-published-solely-to-provisioning-logs"></a>Bereitstellungsereignisse werden aus Überwachungsprotokollen entfernt und ausschließlich in Bereitstellungsprotokollen veröffentlicht

**Typ:** Plan für Änderung  
**Dienstkategorie:** Berichterstellung  
**Produktfunktion:** Überwachung und Berichterstellung
 
Aktivitäten des SCIM-[Bereitstellungsdiensts](../app-provisioning/user-provisioning.md) werden sowohl in den Überwachungsprotokollen als auch in den Bereitstellungsprotokollen protokolliert. Dazu gehören Aktivitäten wie z. B. die Erstellung eines Benutzers in ServiceNow, die Gruppierung in GSuite oder der Import einer Rolle aus AWS. In Zukunft werden diese Ereignisse nur in den Bereitstellungsprotokollen veröffentlicht. Diese Änderung wird implementiert, um doppelte Ereignisse in den Protokollen sowie zusätzliche Kosten zu vermeiden, die dadurch entstehen, dass Kunden die Protokolle in Log Analytics nutzen. 

Wir werden Sie informieren, sobald ein Datum feststeht. Diese Änderung ist nicht für das Kalenderjahr 2020 geplant. 

> [!NOTE]
> Sie wirkt sich nur auf die vom Bereitstellungsdienst ausgegebenen Synchronisierungsereignisse aus. Andere Ereignisse in den Überwachungsprotokollen sind davon nicht betroffen. Ereignisse wie z. B. die Erstellung einer Anwendung, einer Richtlinie für bedingten Zugriff oder eines Benutzers im Verzeichnis werden weiterhin in den Überwachungsprotokollen ausgegeben. [Weitere Informationen](https://docs.microsoft.com/azure/active-directory/reports-monitoring/concept-provisioning-logs?context=azure/active-directory/app-provisioning/context/app-provisioning-context)
 

---

### <a name="azure-ad-on-premises-hybrid-agents-impacted-by-azure-transport-layer-security-tls-certificate-changes"></a>Lokale Azure AD-Hybrid-Agents von TLS-Zertifikatänderungen (Transport Layer Security) für Azure betroffen

**Typ:** Plan für Änderung  
**Dienstkategorie:** –  
**Produktfunktion** : Plattform
 
Microsoft aktualisiert Azure-Dienste für die Verwendung von TLS-Zertifikaten aus einer anderen Gruppe von Stammzertifizierungsstellen (Certificate Authorities, CAs). Es wird ein Update durchgeführt, da die aktuellen Zertifikate der Zertifizierungsstellen eine der grundlegenden Anforderungen des Zertifizierungsstellen-/Browserforums nicht erfüllen. Diese Änderung wirkt sich auf lokal installierte Azure AD-Hybrid-Agents aus, die in festgeschriebenen Umgebungen mit einer festen Liste von Stammzertifikaten verwendet werden. Diese Agents müssen so aktualisiert werden, dass die neuen Zertifikataussteller als vertrauenswürdig eingestuft werden.

Diese Änderung führt zu einer Dienstunterbrechung, wenn Sie nicht sofort Maßnahmen ergreifen. Dies betrifft folgende Agents: 
- [Anwendungsproxyconnectors](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/AppProxy) für den Remotezugriff auf die lokale Bereitstellung 
- [Pass-Through-Authentifizierungs-Agents](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/AzureADConnect), über die sich Ihre Benutzer mit denselben Kennwörtern bei Anwendungen anmelden können
- Agents für die [Vorschau der Cloudbereitstellung](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/AzureADConnect), die die Synchronisierung von AD mit Azure AD durchführen 

Wenn in Ihrer Umgebung Firewallregeln festgelegt wurden, die dazu führen, dass ausgehende Aufrufe nur für bestimmte CRL-Downloads (Certificate Revocation List, Zertifikatssperrliste) zugelassen werden, müssen Sie CRL- und OCSP-URLs zulassen. Vollständige Informationen zu der Änderung und den CRL- und OCSP-URLs, auf die der Zugriff ermöglicht wird, finden Sie unter [TLS-Zertifikatänderungen für Azure](../../security/fundamentals/tls-certificate-changes.md).
 
---

### <a name="azure-active-directory-tls-10-tls-11-and-3des-deprecation-in-us-gov-cloud"></a>Einstellung von TLS 1.0, TLS 1.1 und 3DES in Azure Active Directory in der US Gov-Cloud

**Typ:** Plan für Änderung  
**Dienstkategorie:** –  
**Produktfunktion:** Standards
 
In Azure Active Directory werden die folgenden Protokolle bis zum 31. März 2021 eingestellt:
- TLS 1.0
- TLS 1.1
- 3DES-Verschlüsselungssammlung (TLS_RSA_WITH_3DES_EDE_CBC_SHA)

Bei allen Client-Server- und Browser-Server-Kombinationen sollten TLS 1.2 und moderne Verschlüsselungssammlungen verwendet werden, um eine sichere Verbindung mit Azure Active Directory für Azure-, Office 365- und Microsoft 365-Dienste zu gewährleisten.

Betroffene Umgebungen:
- Azure US Gov
- [Office 365 GCC High und DoD](https://docs.microsoft.com/microsoft-365/compliance/tls-1-2-in-office-365-gcc?view=o365-worldwide)
 
---

### <a name="assign-applications-to-roles-on-au-and-object-scope"></a>Zuweisen von Anwendungen zu Rollen im Bereich von Verwaltungseinheiten und Objekten

**Typ:** Neues Feature  
**Dienstkategorie:** RBAC  
**Produktfunktion:** Zugriffssteuerung
 
Diese Funktion ermöglicht die Zuweisung einer Anwendung (SPN) zu einer Administratorrolle im Bereich der Verwaltungseinheiten. Weitere Informationen finden Sie unter [Zuweisen von bereichsbezogenen Rollen zu einer Verwaltungseinheit](../roles/admin-units-assign-roles.md).

---

### <a name="now-you-can-disable-and-delete-guest-users-when-theyre-denied-access-to-a-resource"></a>Gastbenutzer können nun deaktiviert und gelöscht werden, wenn ihnen der Zugriff auf eine Ressource verweigert wird

**Typ:** Neue Funktion  
**Dienstkategorie** : Zugriffsüberprüfungen  
**Produktfunktion:** Identity Governance
 
„Deaktivieren und löschen“ ist eine erweiterte Steueroption in Azure AD-Zugriffsüberprüfungen, damit Organisationen externe Gäste in Gruppen und Apps besser verwalten können. Wenn Gästen in einer Zugriffsüberprüfung der Zugriff verweigert wird, werden sie durch **Deaktivieren und löschen** automatisch 30 Tage für die Anmeldung blockiert. Nach 30 Tagen werden sie vollständig aus dem Mandanten entfernt.

Weitere Informationen finden Sie unter [Deaktivieren und Löschen externer Identitäten mit Azure AD-Zugriffsüberprüfungen (Vorschau)](../governance/access-reviews-external-users.md#disable-and-delete-external-identities-with-azure-ad-access-reviews-preview).
 
---

### <a name="access-review-creators-can-add-custom-messages-in-emails-to-reviewers"></a>Ersteller von Zugriffsüberprüfungen können in E-Mails an Prüfer benutzerdefinierte Nachrichten hinzufügen

**Typ:** Neue Funktion  
**Dienstkategorie** : Zugriffsüberprüfungen  
**Produktfunktion:** Identity Governance
 
In Azure AD-Zugriffsüberprüfungen können Administratoren, die Überprüfungen erstellen, jetzt benutzerdefinierte Nachrichten an die Prüfer schreiben. Die Prüfer erhalten die Nachricht in der E-Mail, in der sie aufgefordert werden, die Überprüfung abzuschließen. Weitere Informationen zur Verwendung dieser Funktion finden Sie unter Schritt 6 des Abschnitts [Erweiterte Einstellungen](../governance/create-access-review.md#advanced-settings).

---

### <a name="new-provisioning-connectors-in-the-azure-ad-application-gallery---october-2020"></a>Neue Bereitstellungsconnectors im Azure AD-Anwendungskatalog – Oktober 2020

**Typ:** Neues Feature  
**Dienstkategorie:** App-Bereitstellung  
**Produktfunktion:** Integration von Drittanbieterprodukten
 
Sie können ab sofort das Erstellen, Aktualisieren und Löschen von Benutzerkonten für diese neu integrierten Apps automatisieren:

- [Apple Business Manager](../saas-apps/apple-business-manager-provision-tutorial.md)
- [Apple School Manager](../saas-apps/apple-school-manager-provision-tutorial.md)
- [Code42](../saas-apps/code42-provisioning-tutorial.md)
- [AlertMedia](../saas-apps/alertmedia-provisioning-tutorial.md)
- [OpenText Directory Services](../saas-apps/open-text-directory-services-provisioning-tutorial.md)
- [Cinode](../saas-apps/cinode-provisioning-tutorial.md)
- [Global Relay Identity Sync](../saas-apps/global-relay-identity-sync-provisioning-tutorial.md)

Weitere Informationen dazu, wie Sie Ihre Organisation durch die automatisierte Bereitstellung von Benutzerkonten besser schützen können, finden Sie unter [Automatisieren der Bereitstellung und Bereitstellungsaufhebung von Benutzern für SaaS-Anwendungen mit Azure Active Directory](../app-provisioning/user-provisioning.md).
 
---

### <a name="integration-assistant-for-azure-ad-b2c"></a>Integrations-Assistent für Azure AD B2C

**Typ:** Neues Feature  
**Dienstkategorie** : B2C – Kundenidentitätsverwaltung  
**Produktfunktion:** B2B/B2C
 
Der Integrations-Assistent (Vorschau) ist jetzt für App-Registrierungen in Azure AD B2C verfügbar. Über diesen Assistenten können Sie Anwendungen für gängige Szenarien konfigurieren. Weitere Informationen finden Sie unter [Bewährte Methoden und Empfehlungen für Microsoft Identity Platform](../develop/identity-platform-integration-checklist.md).
 
---

### <a name="view-role-template-id-in-azure-portal-ui"></a>Anzeigen der Rollenvorlagen-ID auf der Benutzeroberfläche des Azure-Portals

**Typ:** Neues Feature  
**Dienstkategorie:** Azure-Rollen  
**Produktfunktion:** Zugriffssteuerung
 

Sie können nun die Vorlagen-ID jeder Azure AD-Rolle im Azure-Portal anzeigen. Wählen Sie in Azure AD die **Beschreibung** der ausgewählten Rolle aus. 

Es wird empfohlen, dass Kunden im PowerShell-Skript und im Code anstelle des Anzeigenamens Rollenvorlagen-IDs verwenden. Die Rollenvorlagen-ID wird zur Verwendung in [directoryRoles](https://docs.microsoft.com/graph/api/resources/directoryrole?view=graph-rest-1.0)- und [roleDefinition](https://docs.microsoft.com/graph/api/resources/unifiedroledefinition?view=graph-rest-beta)-Objekten unterstützt. Weitere Informationen finden Sie unter [Rollenvorlagen-IDs](../roles/permissions-reference.md#role-template-ids).

---

### <a name="api-connectors-for-azure-ad-b2c-sign-up-user-flows-is-now-in-public-preview"></a>API-Connectors für Azure AD B2C-Benutzerflows für die Registrierung befinden sich jetzt in der öffentlichen Vorschauphase

**Typ:** Neues Feature  
**Dienstkategorie** : B2C – Kundenidentitätsverwaltung  
**Produktfunktion:** B2B/B2C
 

API-Connectors sind nun zur Verwendung mit Azure Active Directory B2C verfügbar. Mit API-Connectors können Sie Web-APIs verwenden, um Ihre Benutzerflows für die Registrierung anzupassen und mit externen Cloudsystemen zu integrieren. Mit API-Connectors können Sie folgende Aktionen ausführen:

- Integrieren in benutzerdefinierte Genehmigungsworkflows
- Überprüfen von Benutzereingabedaten
- Überschreiben von Benutzerattributen 
- Ausführen von benutzerdefinierter Geschäftslogik 

 Weitere Informationen finden Sie unter [Verwenden von API-Connectors zum Anpassen und Erweitern von Flows zur Benutzerregistrierung](../../active-directory-b2c/api-connectors-overview.md).

---

### <a name="state-property-for-connected-organizations-in-entitlement-management"></a>State-Eigenschaft für verbundene Organisationen in der Berechtigungsverwaltung

**Typ:** Neues Feature  
**Dienstkategorie:** Verzeichnisverwaltungs- **Produktfunktion:** Berechtigungsverwaltung
 

 Alle verbundenen Organisationen verfügen jetzt über die zusätzliche Eigenschaft „State“. Mit „State“ wird gesteuert, wie die verbundene Organisation in Richtlinien verwendet wird, die auf „Alle konfigurierten verbundenen Organisationen“ verweisen. Der Wert ist entweder „configured“ (konfiguriert, d. h., die Organisation befindet sich im Bereich der Richtlinien, die die „Alle“-Klausel verwenden) oder „proposed“ (vorgeschlagen, d. h., die Organisation befindet sich nicht im Gültigkeitsbereich).  

Bei manuell erstellten verbundenen Organisationen wird als Standardeinstellung „configured“ festgelegt. Automatisch erstellte verbundene Organisationen (die über Richtlinien erstellt werden, die es jedem Benutzer aus dem Internet ermöglichen, Zugriff anzufordern) werden standardmäßig auf „proposed“ festgelegt.  Alle verbundenen Organisationen, die vor dem 9. September 2020 erstellt wurden, werden auf „configured“ festgelegt. Administratoren können diese Eigenschaft bei Bedarf aktualisieren. [Weitere Informationen](../governance/entitlement-management-organization.md#managing-a-connected-organization-programmatically)
 

---

### <a name="azure-active-directory-external-identities-now-has-premium-advanced-security-settings-for-b2c"></a>Externe Azure Active Directory-Identitäten verfügen jetzt über erweiterte Premium-Sicherheitseinstellungen für B2C

**Typ:** Neues Feature  
**Dienstkategorie** : B2C – Kundenidentitätsverwaltung  
**Produktfunktion:** B2B/B2C
 
Der risikobasierte bedingte Zugriff und die Risikoerkennungsfunktionen von Identity Protection sind nun in [Azure AD B2C](../..//active-directory-b2c/conditional-access-identity-protection-overview.md) verfügbar. Mit diesen erweiterten Sicherheitsfunktionen haben Kunden jetzt folgende Möglichkeiten:
- Verwenden von Intelligent Insights zur Risikobewertung bei B2C-Anwendungen und Endbenutzerkonten. Zu den Risikoerkennungen zählen ungewöhnliche Ortswechsel, anonyme IP-Adressen, mit Schadsoftware verknüpfte IP-Adressen und Azure AD Threat Intelligence. Auch portal- und API-basierte Berichte sind verfügbar.
- Automatisches Behandeln von Risiken durch Konfigurieren von Richtlinien für die adaptive Authentifizierung für B2C-Benutzer. App-Entwickler und Administratoren können Risiken in Echtzeit mindern, indem sie eine mehrstufige Authentifizierung (MFA) erforderlich machen oder den Zugriff blockieren, je nachdem, welche Benutzerrisikostufe erkannt wird und welche zusätzlichen Kontrollen basierend auf Standort, Gruppe und Anwendung verfügbar sind.
- Integration in Azure AD B2C-Benutzerflows und benutzerdefinierte Richtlinien. Die Bedingungen können über integrierte Benutzerflows in Azure AD B2C ausgelöst oder in benutzerdefinierte B2C-Richtlinien integriert werden. Wie andere Aspekte des B2C-Benutzerflows kann auch das Messaging für Endbenutzer angepasst werden. Die Anpassung erfolgt entsprechend den Optionen der Organisation für Sprache, Marke und Risikominderung.
 
---

### <a name="new-federated-apps-available-in-azure-ad-application-gallery---october-2020"></a>Neue Verbund-Apps im Azure AD-Anwendungskatalog verfügbar – Oktober 2020

**Typ:** Neues Feature  
**Dienstkategorie** : Unternehmens-Apps  
**Produktfunktion:** Integration von Drittanbieterprodukten
 
Im Oktober 2020 haben wir die folgenden 27 neuen Anwendungen mit Verbundunterstützung in unseren App-Katalog aufgenommen:

[Sentry](../saas-apps/sentry-tutorial.md), [Bumblebee - Productivity Superapp](https://app.yellowmessenger.com/user/login), [ABBYY FlexiCapture Cloud](../saas-apps/abbyy-flexicapture-cloud-tutorial.md), [EAComposer](../saas-apps/eacomposer-tutorial.md), [Genesys Cloud Integration for Azure](https://apps.mypurecloud.com/msteams-integration/), [Zone Technologies Portal](https://portail.zonetechnologie.com/signin), [Beautiful.ai](../saas-apps/beautiful.ai-tutorial.md), [Datawiza Access Broker](https://console.datawiza.com/), [ZOKRI](https://app.zokri.com/), [CheckProof](../saas-apps/checkproof-tutorial.md), [Ecochallenge.org](https://events.ecochallenge.org/users/login), [atSpoke](http://atspoke.com/login), [Appointment Reminder](https://app.appointmentreminder.co.nz/account/login), [Cloud.Market](https://cloud.market/), [TravelPerk](../saas-apps/travelperk-tutorial.md), [Greetly](https://app.greetly.com/), [OrgVitality SSO}(../saas-apps/orgvitality-sso-tutorial.md), [Web Cargo Air](../saas-apps/web-cargo-air-tutorial.md), [Loop Flow CRM](../saas-apps/loop-flow-crm-tutorial.md), [Starmind](../saas-apps/starmind-tutorial.md), [Workstem](https://hrm.workstem.com/login), [Retail Zipline](../saas-apps/retail-zipline-tutorial.md), [Hoxhunt](../saas-apps/hoxhunt-tutorial.md), [MEVISIO](../saas-apps/mevisio-tutorial.md), [Samsara](../saas-apps/samsara-tutorial.md), [Nimbus](../saas-apps/nimbus-tutorial.md), [Pulse Secure virtual Traffic Manager](https://docs.microsoft.com/azure/active-directory/saas-apps/pulse-secure-virtual-traffic-manager-tutorial)

Die Dokumentation zu allen Anwendungen finden Sie auch hier: https://aka.ms/AppsTutorial.

Informationen zum Auflisten Ihrer Anwendung im Azure AD-App-Katalog finden Sie hier: https://aka.ms/AzureADAppRequest.

---

### <a name="provisioning-logs-can-now-be-streamed-to-log-analytics"></a>Bereitstellungsprotokolle können jetzt an Log Analytics übertragen werden

**Typ:** Neues Feature  
**Dienstkategorie:** Berichterstellung  
**Produktfunktion:** Überwachung und Berichterstellung
 

Durch Veröffentlichen Ihrer Bereitstellungsprotokolle in Log Analytics haben Sie folgende Möglichkeiten:
- Speichern von Bereitstellungsprotokollen für mehr als 30 Tage
- Definieren von benutzerdefinierten Warnungen und Benachrichtigungen
- Erstellen von Dashboards zum Visualisieren der Protokolle
- Ausführen komplexer Abfragen zum Analysieren der Protokolle 

Informationen zur Verwendung der Funktion finden Sie unter [Grundlegendes zur Integration der Bereitstellung in Azure Monitor-Protokolle](../app-provisioning/application-provisioning-log-analytics.md).
 
---

### <a name="provisioning-logs-can-now-be-viewed-by-application-owners"></a>Bereitstellungsprotokolle können nun von Anwendungsbesitzern angezeigt werden

**Typ:** Geändertes Feature  
**Dienstkategorie:** Berichterstellung  
**Produktfunktion:** Überwachung und Berichterstellung
 
Sie können Anwendungsbesitzern nun ermöglichen, die Aktivitäten des Bereitstellungsdiensts zu überwachen und Probleme zu beheben, ohne ihnen eine privilegierte Rolle zuzuweisen oder einen IT-Engpass zu verursachen. [Weitere Informationen](../reports-monitoring/concept-provisioning-logs.md)
 
---

### <a name="renaming-10-azure-active-directory-roles"></a>Umbenennung von 10 Azure Active Directory-Rollen

**Typ:** Geändertes Feature  
**Dienstkategorie:** Azure-Rollen  
**Produktfunktion:** Zugriffssteuerung
 
Einige integrierte Azure Active Directory-Rollen (Azure AD) haben Namen, die sich von den in Microsoft 365 Admin Center, im Azure AD-Portal und in Microsoft Graph angezeigten Namen unterscheiden. Diese Inkonsistenz kann Probleme bei automatisierten Prozessen verursachen. Mit diesem Update werden 10 Rollennamen umbenannt, um sie zu vereinheitlichen. In der folgenden Tabelle sind die neuen Rollennamen aufgeführt:

![Tabelle mit neuen Rollennamen](media/whats-new/azure-role.png)

---

### <a name="azure-ad-b2c-support-for-auth-code-flow-for-spas-using-msal-js-2x"></a>Azure AD B2C-Unterstützung für den Autorisierungscodeflow für SPAs mithilfe von MSAL JS 2.x

**Typ:** Geändertes Feature  
**Dienstkategorie** : B2C – Kundenidentitätsverwaltung  
**Produktfunktion:** B2B/B2C
 
MSAL.js Version 2.x bietet jetzt Unterstützung für den Autorisierungscodeflow für Single-Page-Web-Apps (SPAs). Azure AD B2C unterstützt nun die Verwendung des SPA-App-Typs im Azure-Portal sowie die Verwendung des MSAL.js-Autorisierungscodeflows mit PKCE für Single-Page-Apps. Dadurch können in SPAs unter Verwendung von Azure AD B2C das einmalige Anmelden (SSO) in neueren Browsern beibehalten und neuere Empfehlungen für das Authentifizierungsprotokoll eingehalten werden. Informationen zu den ersten Schritten finden Sie im Tutorial [Registrieren einer Single-Page-Webanwendung (SPA) in Azure Active Directory B2C](../../active-directory-b2c/tutorial-register-spa.md).

---

### <a name="updates-to-remember-multi-factor-authentication-mfa-on-a-trusted-device-setting"></a>Aktualisierung der Einstellung „Mehrstufige Authentifizierung auf vertrauenswürdigem Gerät speichern“

**Typ:** Geändertes Feature  
**Dienstkategorie:** MFA  
**Produktfunktion:** Identitätssicherheit und -schutz
 

Wir haben vor Kurzem die Funktion [Mehrstufige Authentifizierung auf vertrauenswürdigem Gerät speichern](../authentication/howto-mfa-mfasettings.md#remember-multi-factor-authentication) aktualisiert, um die Authentifizierung auf bis zu 365 Tage zu verlängern. Bei Azure Active Directory (Azure AD) Premium-Lizenzen kann darüber hinaus die [Richtlinie für bedingten Zugriff – Anmeldehäufigkeit von Benutzern](../conditional-access/howto-conditional-access-session-lifetime.md#user-sign-in-frequency) verwendet werden, die mehr Flexibilität bei den Einstellungen für die erneute Authentifizierung bietet.

Um eine optimale Benutzerfreundlichkeit zu gewährleisten, empfiehlt es sich, die Lebensdauer von Sitzungen für vertrauenswürdige Geräte und Standorte sowie für Sitzungen mit geringem Risiko mithilfe der Anmeldehäufigkeit für bedingten Zugriff zu verlängern. Diese stellt eine Alternative zur Einstellung „Mehrstufige Authentifizierung auf vertrauenswürdigem Gerät speichern“ dar. Lesen Sie zum Einstieg den [neuesten Leitfaden zur Optimierung der erneuten Authentifizierung](../authentication/concepts-azure-multi-factor-authentication-prompts-session-lifetime.md).

---

## <a name="september-2020"></a>September 2020

### <a name="new-provisioning-connectors-in-the-azure-ad-application-gallery---september-2020"></a>Neue Bereitstellungsconnectors im Azure AD-Anwendungskatalog – September 2020

**Typ:** Neues Feature  
**Dienstkategorie:** App-Bereitstellung  
**Produktfunktion:** Integration von Drittanbieterprodukten
 
Sie können ab sofort das Erstellen, Aktualisieren und Löschen von Benutzerkonten für diese neu integrierten Apps automatisieren:

- [Coda](../saas-apps/coda-provisioning-tutorial.md)
- [Cofense Recipient Sync](../saas-apps/cofense-provision-tutorial.md)
- [InVision](../saas-apps/invision-provisioning-tutorial.md)
- [myday](../saas-apps/myday-provision-tutorial.md)
- [SAP Analytics Cloud](../saas-apps/sap-analytics-cloud-provisioning-tutorial.md)
- [Webroot Security Awareness](../saas-apps/webroot-security-awareness-training-provisioning-tutorial.md)

Weitere Informationen dazu, wie Sie Ihre Organisation durch die automatisierte Bereitstellung von Benutzerkonten besser schützen können, finden Sie unter [Automatisieren der Bereitstellung und Bereitstellungsaufhebung von Benutzern für SaaS-Anwendungen mit Azure Active Directory](../app-provisioning/user-provisioning.md).
 
---
### <a name="cloud-provisioning-public-preview-refresh"></a>Cloudbereitstellungsaktualisierung, Public Preview

**Typ:** Neues Feature  
**Dienstkategorie:** Azure AD-Cloudbereitstellung, **Produktfunktion:** Identity Lifecycle Management
 
Die Azure AD Connect-Cloudbereitstellungsaktualisierung (Public Preview) bietet zwei wichtige Verbesserungen, die anhand von Kundenfeedback entwickelt wurden: 

- Attributzuordnung über das Azure-Portal

    Mit diesem Feature können IT-Administratoren Benutzer-, Gruppen- oder Kontaktattribute aus AD in Azure AD mithilfe verschiedener Zuordnungstypen zuordnen, die heute vorhanden sind. Die Attributzuordnung ist eine Funktion zum Standardisieren von Werten der Attribute, die von Active Directory an Azure Active Directory übertragen werden. Sie können bestimmen, ob der Attributwert von AD direkt Azure AD zugeordnet werden soll oder ob Ausdrücke verwendet werden sollen, um die Attributwerte beim Bereitstellen von Benutzern zu transformieren. [Weitere Informationen](../cloud-provisioning/how-to-attribute-mapping.md)

- Bedarfsgesteuerte Bereitstellung oder Testen der Benutzertransformation

    Nachdem Sie Ihre Konfiguration eingerichtet haben, möchten Sie vermutlich testen, ob die Benutzertransformation wie erwartet funktioniert, bevor Sie diese auf alle Ihre Benutzer im Bereich anwenden. Bei der bedarfsgesteuerten Bereitstellung können IT-Administratoren den Distinguished Name (DN) eines AD-Benutzers eingeben und überprüfen, ob er wie erwartet synchronisiert wird. Die bedarfsgesteuerte Bereitstellung bietet eine gute Möglichkeit, um sicherzustellen, dass die Attributzuordnungen, die Sie zuvor vorgenommen haben, erwartungsgemäß funktionieren. [Weitere Informationen](../cloud-provisioning/how-to-on-demand-provision.md)
 
---

### <a name="audited-bitlocker-recovery-in-azure-ad---public-preview"></a>Überwachte BitLocker-Wiederherstellung in Azure AD – Public Preview

**Typ:** Neues Feature  
**Dienstkategorie:** Gerätezugriffsverwaltung  
**Produktfunktion:** Lebenszyklusverwaltung für Geräte
 
Wenn IT-Administratoren oder Endbenutzer den BitLocker-Wiederherstellungsschlüssel lesen, auf den sie zugreifen können, generiert Azure Active Directory jetzt ein Überwachungsprotokoll, das erfasst, wer auf den Wiederherstellungsschlüssel zugegriffen hat. Dieselbe Überwachung liefert Details zu dem Gerät, dem der BitLocker-Schlüssel zugeordnet ist.

Endbenutzer können [über das Portal „Mein Konto“ auf ihre Wiederherstellungsschlüssel zugreifen](../user-help/my-account-portal-devices-page.md#view-a-bitlocker-key). IT-Administratoren können über die [BitLocker-Wiederherstellungsschlüssel-API in der Betaversion](/graph/api/resources/bitlockerrecoverykey?view=graph-rest-beta) oder über das Azure AD-Portal auf Wiederherstellungsschlüssel zugreifen. Weitere Informationen finden Sie unter [Anzeigen oder Kopieren von BitLocker-Schlüsseln im Azure AD-Portal](../devices/device-management-azure-portal.md#view-or-copy-bitlocker-keys).

---

### <a name="teams-devices-administrator-built-in-role"></a>Integrierte Rolle „Teams-Geräteadministrator“

**Typ:** Neues Feature  
**Dienstkategorie:** RBAC  
**Produktfunktion:** Zugriffssteuerung
 
Benutzer mit der Rolle [Teams-Geräteadministrator](../roles/permissions-reference.md#teams-devices-administrator) können im Teams Admin Center [von Teams zertifizierte Geräte](https://www.microsoft.com/microsoft-365/microsoft-teams/across-devices/devices) verwalten. 

Benutzer mit dieser Rolle können alle Geräte auf einen Blick anzeigen und haben die Möglichkeit, Geräte zu suchen und zu filtern. Außerdem kann der Benutzer Details zu jedem Gerät überprüfen, darunter das angemeldete Konto sowie Marke und Modell des Geräts. Der Benutzer kann die Einstellungen auf dem Gerät ändern und die Softwareversionen aktualisieren. Diese Rolle gewährt keine Berechtigungen zum Überprüfen der Teams-Aktivität und der Anrufqualität des Geräts.
 
---

### <a name="advanced-query-capabilities-for-directory-objects"></a>Erweiterte Abfragefunktionen für Verzeichnisobjekte

**Typ:** Neues Feature  
**Dienstkategorie:** MS Graph  
**Produktfunktion:** Entwickleroberfläche
 
Alle neuen Abfragefunktionen, die für Verzeichnisobjekte in Azure AD-APIs eingeführt wurden, sind jetzt im v1.0-Endpunkt und für die Produktionsumgebung verfügbar. Mit den OData-Standardoperatoren können Entwickler Verzeichnisobjekte und zugehörige Verknüpfungen zählen, durchsuchen, filtern und sortieren.

Weitere Informationen finden Sie in [dieser Dokumentation](https://aka.ms/BlogPostMezzoGA). Sie können über diese [kurze Umfrage](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR_yN8EPoGo5OpR1hgmCp1XxUMENJRkNQTk5RQkpWTE44NEk2U0RIV0VZRy4u) auch Feedback senden.
 
---

### <a name="public-preview-continuous-access-evaluation-for-tenants-who-configured-conditional-access-policies"></a>Öffentliche Vorschau: Fortlaufende Zugriffsevaluierung für Mandanten, die Richtlinien für bedingten Zugriff konfiguriert haben

**Typ:** Neues Feature  
**Dienstkategorie** : Authentifizierungen (Anmeldungen)  
**Produktfunktion:** Identitätssicherheit und -schutz
 
Fortlaufende Zugriffsevaluierung (Continuous Access Evaluation, CAE) ist jetzt in der öffentlichen Vorschau für Azure AD-Mandanten mit Richtlinien für bedingten Zugriff verfügbar. Mit CAE werden kritische sicherheitsrelevante Ereignisse und Richtlinien in Echtzeit ausgewertet. Dies umfasst Kontodeaktivierungen, Kennwortzurücksetzungen und Standortänderungen. Weitere Informationen finden Sie unter [Fortlaufende Zugriffsevaluierung](../conditional-access/concept-continuous-access-evaluation.md).

---

### <a name="public-preview-ask-users-requesting-an-access-package-additional-questions-to-improve-approval-decisions"></a>Öffentliche Vorschau: Benutzern, die ein Zugriffspaket anfordern, zusätzliche Fragen stellen, um bessere Genehmigungsentscheidungen treffen zu können

**Typ:** Neues Feature  
**Dienstkategorie:** Benutzerzugriffsverwaltung  
**Produktfunktion:** Berechtigungsverwaltung
 
Administratoren können jetzt verlangen, dass Benutzer, die ein Zugriffspaket anfordern, im Portal „Mein Zugriff“ der Azure AD-Berechtigungsverwaltung zusätzliche Fragen beantworten müssen, die über das Angeben einer geschäftlichen Begründung hinausgehen. Die Antworten der Benutzer werden dann den genehmigenden Personen angezeigt, damit diese eine genauere Entscheidung über die Zugriffsgenehmigung treffen können. Weitere Informationen finden Sie unter [Sammeln zusätzlicher Anfordererinformationen für die Genehmigung (Vorschau)](../governance/entitlement-management-access-package-approval-policy.md#collect-additional-requestor-information-for-approval-preview).
 
---

### <a name="public-preview-enhanced-user-management"></a>Öffentliche Vorschau: Erweiterte Benutzerverwaltung

**Typ:** Neues Feature  
**Dienstkategorie:** Benutzerverwaltung  
**Produktfunktion:** Benutzerverwaltung
 

Das Azure AD-Portal wurde aktualisiert, um die Benutzersuche auf den Seiten „Alle Benutzer“ und „Gelöschte Benutzer“ zu vereinfachen. Zu den Änderungen in dieser Vorschau gehören: 
- Mehr sichtbare Benutzereigenschaften einschließlich Objekt-ID, Status der Verzeichnissynchronisierung, Erstellungstyp und Identitätsaussteller.
- Die Suchfunktion lässt jetzt eine Kombination aus Namen, E-Mail-Adressen und Objekt-IDs zu.
- Erweiterte Filterung nach Benutzertyp (Mitglied, Gast, kein), Status der Verzeichnissynchronisierung, Erstellungstyp, Firmenname und Domänenname.
- Neue Sortierfunktionen für Eigenschaften wie Name, Benutzerprinzipalname und Löschdatum.
- Eine neue Gesamtanzahl von Benutzern, die bei Suchvorgängen oder Filtern aktualisiert werden.

Weitere Informationen finden Sie unter [Erweiterungen bei der Benutzerverwaltung (Vorschau) – Azure Active Directory](../enterprise-users/users-search-enhanced.md).

---

### <a name="new-notes-field-for-enterprise-applications"></a>Neues Notizenfeld für Unternehmensanwendungen

**Typ:** Neues Feature  
**Dienstkategorie:** Enterprise Apps- **Produktfunktion:** SSO

Sie können Unternehmensanwendungen Textnotizen hinzufügen. Sie können alle relevanten Informationen hinzufügen, die Sie beim Verwalten von Anwendungen unter Unternehmensanwendungen unterstützen. Weitere Informationen finden Sie unter [Quickstart: Konfigurieren von Eigenschaften für eine Anwendung in Ihrem Azure AD-Mandanten (Azure Active Directory)](../manage-apps/add-application-portal-configure.md). 

---

### <a name="new-federated-apps-available-in-azure-ad-application-gallery---september-2020"></a>Neue Verbund-Apps im Azure AD-Anwendungskatalog verfügbar – September 2020

**Typ:** Neues Feature  
**Dienstkategorie** : Unternehmens-Apps  
**Produktfunktion:** Integration von Drittanbieterprodukten

Im September 2020 haben wir die folgenden 34 neuen Anwendungen mit Verbundunterstützung in unseren App-Katalog aufgenommen:

[VMware Horizon - Unified Access Gateway](), [Pulse Secure PCS](../saas-apps/vmware-horizon-unified-access-gateway-tutorial.md), [Inventory360](../saas-apps/pulse-secure-pcs-tutorial.md), [Frontitude](https://services.enteksystems.de/sso/microsoft/signup), [BookWidgets](https://www.bookwidgets.com/sso/office365), [ZVD_Server](https://zaas.zenmutech.com/user/signin), [HashData for Business](https://hashdata.app/login.xhtml), [SecureLogin](https://securelogin.securelogin.nu/sso/azure/login), [CyberSolutions MAILBASEΣ/CMSS](../saas-apps/cybersolutions-mailbase-tutorial.md), [CyberSolutions CYBERMAILΣ](../saas-apps/cybersolutions-cybermail-tutorial.md), [LimbleCMMS](https://auth.limblecmms.com/), [Glint Inc](../saas-apps/glint-inc-tutorial.md), [zeroheight](../saas-apps/zeroheight-tutorial.md), [Gender Fitness](https://app.genderfitness.com/), [Coeo Portal](https://my.coeo.com/), [Grammarly](../saas-apps/grammarly-tutorial.md), [Fivetran](../saas-apps/fivetran-tutorial.md), [Kumolus](../saas-apps/kumolus-tutorial.md), [RSA Archer Suite](../saas-apps/rsa-archer-suite-tutorial.md), [TeamzSkill](../saas-apps/teamzskill-tutorial.md), [raumfürraum](../saas-apps/raumfurraum-tutorial.md), [Saviynt](../saas-apps/saviynt-tutorial.md), [BizMerlinHR](https://marketplace.bizmerlin.net/bmone/signup), [Mobile Locker](../saas-apps/mobile-locker-tutorial.md), [Zengine](../saas-apps/zengine-tutorial.md), [CloudCADI](https://app.cloudcadi.com/login), [Simfoni Analytics](https://simfonianalytics.com/accounts/microsoft/login/), [Priva Identity & Access Management](https://my.priva.com/), [Nitro Pro](https://www.gonitro.com/nps/product-details/downloads), [Eventfinity](../saas-apps/eventfinity-tutorial.md), [Fexa](../saas-apps/fexa-tutorial.md), [Secured Signing Enterprise Portal](https://www.securedsigning.com/aad/Auth/ExternalLogin/AdminPortal), [Secured Signing Enterprise Portal AAD Setup](https://www.securedsigning.com/aad/Auth/ExternalLogin/AdminPortal), [Wistec Online](https://wisteconline.com/auth/oidc), [Oracle PeopleSoft – Protected by F5 BIG-IP APM](../saas-apps/oracle-peoplesoft-protected-by-f5-big-ip-apm-tutorial.md)

Die Dokumentation zu allen Anwendungen finden Sie auch hier: https://aka.ms/AppsTutorial.

Informationen zum Auflisten Ihrer Anwendung im Azure AD-App-Katalog finden Sie hier: https://aka.ms/AzureADAppRequest.

---

### <a name="new-delegation-role-in-azure-ad-entitlement-management-access-package-assignment-manager"></a>Neue Delegierungsrolle in der Azure AD-Berechtigungsverwaltung: Zugriffspaketzuweisungsmanager

**Typ:** Neues Feature  
**Dienstkategorie:** Benutzerzugriffsverwaltung  
**Produktfunktion:** Berechtigungsverwaltung
 
In der Azure AD-Berechtigungsverwaltung wurde eine neue Rolle „Zugriffspaket-Zuweisungsmanager“ hinzugefügt, um granulare Berechtigungen zum Verwalten von Zuweisungen bereitzustellen. Sie können jetzt Aufgaben an einen Benutzer in dieser Rolle delegieren, der die Zuweisungsverwaltung eines Zugriffspakets an einen Geschäftsinhaber delegieren kann. Ein Zugriffspaket-Zuweisungsmanager kann jedoch die Zugriffspaketrichtlinien oder andere Eigenschaften, die von den Administratoren festgelegt wurden, nicht ändern. 

Durch diese neue Rolle profitieren Sie von den geringsten Berechtigungen, die zum Delegieren der Verwaltung von Zuweisungen und zum Aufrechterhalten der administrativen Kontrolle für alle anderen Zugriffspaketkonfigurationen erforderlich sind. Weitere Informationen finden Sie unter [Berechtigungsverwaltungsrollen](../governance/entitlement-management-delegate.md#entitlement-management-roles).
 
---

### <a name="changes-to-privileged-identity-managements-onboarding-flow"></a>Änderungen am Onboardingvorgang in Privileged Identity Management

**Typ:** Geändertes Feature  
**Dienstkategorie:** Privileged Identity Management  
**Produktfunktion** : Privileged Identity Management
 
Zuvor erforderte das Onboarding in Privileged Identity Management (PIM) die Benutzereinwilligung und einen Onboardingvorgang auf dem PIM-Blatt, das die Registrierung in Azure MFA enthielt. Mit der kürzlich erfolgten Integration der PIM-Funktion in das Azure AD-Blatt „Rollen und Administratoren“ wird diese Funktion entfernt. Jeder Mandant mit einer gültigen P2-Lizenz wird automatisch in PIM integriert.

Das Onboarding in PIM hat keine direkten negativen Auswirkungen auf Ihren Mandanten. Sie können die folgenden Änderungen erwarten:
- Zusätzliche Zuweisungsoptionen wie aktive oder berechtigte Rollen mit Start- und Endzeit, wenn Sie eine Zuweisung in PIM oder in Azure AD auf dem Blatt „Rollen und Administratoren“ vornehmen. 
- Zusätzliche Bereichsmechanismen wie administrative Einheiten und benutzerdefinierte Rollen wurden direkt in die Zuweisungsoberfläche eingeführt. 
- Wenn Sie ein globaler Administrator oder ein Administrator für privilegierte Rollen sind, erhalten Sie möglicherweise einige zusätzliche E-Mails wie die wöchentliche PIM-Zusammenfassung. 
- Darüber hinaus wird Ihnen möglicherweise auch der MS-PIM-Dienstprinzipal im Überwachungsprotokoll für die Rollenzuweisung angezeigt. Diese erwartete Änderung sollte sich nicht auf Ihren regulären Workflow auswirken.

 Weitere Informationen finden Sie unter [Einstieg in Privileged Identity Management](../privileged-identity-management/pim-getting-started.md).

---

### <a name="azure-ad-entitlement-management-the-select-pane-of-access-package-resources-now-shows-by-default-the-resources-currently-in-the-selected-catalog"></a>Azure AD-Berechtigungsverwaltung: Im Bereich „Auswählen“ der Zugriffspaketressourcen werden jetzt standardmäßig die Ressourcen angezeigt, die sich aktuell im ausgewählten Katalog befinden.

**Typ:** Geändertes Feature  
**Dienstkategorie:** Benutzerzugriffsverwaltung  
**Produktfunktion:** Berechtigungsverwaltung
 

Im Flow zum Erstellen von Zugriffspaketen unter der Registerkarte „Ressourcenrollen“ wird das Verhalten des Bereichs „Auswählen“ geändert. Derzeit werden im Standardverhalten alle im Besitz des Benutzers befindlichen Ressourcen sowie dem ausgewählten Katalog hinzugefügte Ressourcen angezeigt. 

Dieses Verhalten wird geändert, sodass standardmäßig nur die derzeit im Katalog hinzugefügten Ressourcen angezeigt werden, damit Benutzer problemlos Ressourcen aus dem Katalog auswählen können. Durch das Update wird die Auffindbarkeit der Ressourcen verbessert, die den Zugriffspaketen hinzugefügt werden können, und das Risiko minimiert, dass versehentlich Ressourcen hinzugefügt werden, die sich im Besitz des Benutzers befinden und nicht Teil des Katalogs sind. Weitere Informationen finden Sie unter [Erstellen eines neuen Zugriffspakets in der Azure AD-Berechtigungsverwaltung](../governance/entitlement-management-access-package-create.md#resource-roles).
 
---

## <a name="august-2020"></a>August 2020 
 
### <a name="updates-to-azure-multi-factor-authentication-server-firewall-requirements"></a>Aktualisierungen bei den Anforderungen an die Firewall für Microsoft Azure Multi-Factor Authentication-Server

**Typ:** Plan für Änderung  
**Dienstkategorie:** MFA  
**Produktfunktion:** Identitätssicherheit und -schutz
 
Ab dem 1. Oktober 2020 benötigen die Anforderungen an die Firewall für Azure MFA-Server zusätzliche IP-Adressbereiche.

Wenn es in Ihrer Organisation ausgehende Firewallregeln gibt, aktualisieren Sie diese Regeln, damit Ihre MFA-Server mit allen erforderlichen IP-Adressbereichen kommunizieren können. Die IP-Adressbereiche werden in [Anforderungen an die Azure Multi-Factor Authentication-Server-Firewall](../authentication/howto-mfaserver-deploy.md#azure-multi-factor-authentication-server-firewall-requirements) dokumentiert.

---

### <a name="upcoming-changes-to-user-experience-in-identity-secure-score"></a>Bevorstehende Änderungen der Benutzerumgebung für Identitätssicherheitsbewertung

**Typ:** Plan für Änderung  
**Dienstkategorie:** Identity Protection- **Produktfunktion:** Identitätssicherheit und -schutz

Wir aktualisieren das Portal für Identitätssicherheitsbewertung, sodass es mit den Änderungen übereinstimmt, die in der [neuen Release](/microsoft-365/security/mtp/microsoft-secure-score-whats-new?view=o365-worldwide) von Microsoft Secure Score eingeführt wurden. 

Die Vorschauversion mit den Änderungen wird ab Anfang September verfügbar sein. Die Änderungen in der Vorschauversion umfassen Folgendes:
- „Identitätssicherheitsbewertung“ wurde in „Sicherheitsbewertung für Identitäten“ zur Markenausrichtung mit Microsoft Secure Score (Microsoft Sicherheitsbewertung) umbenannt
- Punkte werden auf Standardskalierung normalisiert und in Prozentsätzen statt in Punkten gemeldet

In dieser Vorschau können Kunden zwischen der vorhandenen Umgebung und der neuen Umgebung wechseln. Diese Vorschau gilt bis Ende November 2020. Nach der Vorschau werden die Kunden automatisch zur neuen Benutzerumgebung geleitet.

---

### <a name="new-restricted-guest-access-permissions-in-azure-ad---public-preview"></a>Neue eingeschränkte Gastzugriffsberechtigungen in Azure AD – Öffentliche Vorschau

**Typ:** Neues Feature  
**Dienstkategorie:** Zugriffssteuerung   
**Produktfunktion:** Benutzerverwaltung

Wir haben die Berechtigungen auf Verzeichnisebene für Gastbenutzer aktualisiert. Diese Berechtigungen ermöglichen es Administratoren, zusätzliche Einschränkungen und Kontrollen für externen Gastbenutzerzugriff anzufordern. Administratoren können jetzt zusätzliche Einschränkungen für den Zugriff externer Gäste auf Profil- und Mitgliedschaftsinformationen für Benutzer und Gruppen hinzufügen. Mit dieser öffentlichen Previewfunktion können Kunden den externen Benutzerzugriff durch Verschleiern von Gruppenmitgliedschaften bedarfsorientiert verwalten. Dies schließt auch die Einschränkung von Gastbenutzern beim Anzeigen von Mitgliedschaften der Gruppe (n) ein, in der sie sich gerade befinden.

Weitere Informationen finden Sie unter [Restricted Guest Access Permissions](../enterprise-users/users-restrict-guest-permissions.md) (Eingeschränkte Berechtigungen für Gastzugriff) und [Users Default Permissions](./users-default-permissions.md) (Standardberechtigungen für Benutzer).
 
---

### <a name="general-availability-of-delta-queries-for-service-principals"></a>Allgemeine Verfügbarkeit von Delta-Abfragen für Dienstprinzipale

**Typ:** Neues Feature  
**Dienstkategorie:** MS Graph  
**Produktfunktion:** Entwickleroberfläche
 
Die Delta-Abfrage in Microsoft Graph unterstützt jetzt den Ressourcentyp in v1.0:
- Dienstprinzipal

Jetzt können Clients Änderungen an diesen Ressourcen effizient nachverfolgen und die beste Lösung zum Synchronisieren von Änderungen daran mit einem lokalen Datenspeicher bereitstellen. Informationen zum Konfigurieren dieser Ressourcen in einer Abfrage finden Sie unter [Nachverfolgen von Änderungen bei Microsoft Graph-Daten mithilfe einer Delta-Abfrage](/graph/delta-query-overview).
 
---

### <a name="general-availability-of-delta-queries-for-oauth2permissiongrant"></a>Allgemeine Verfügbarkeit von Delta-Abfragen für oAuth2PermissionGrant

**Typ:** Neues Feature  
**Dienstkategorie:** MS Graph  
**Produktfunktion:** Entwickleroberfläche

Die Delta-Abfrage in Microsoft Graph unterstützt jetzt den Ressourcentyp in v1.0:
- OAuth2PermissionGrant

Clients können jetzt Änderungen an diesen Ressourcen effizient nachverfolgen und die beste Lösung zum Synchronisieren von Änderungen daran mit einem lokalen Datenspeicher bereitstellen. Informationen zum Konfigurieren dieser Ressourcen in einer Abfrage finden Sie unter [Nachverfolgen von Änderungen bei Microsoft Graph-Daten mithilfe einer Delta-Abfrage](/graph/delta-query-overview).

---

### <a name="new-federated-apps-available-in-azure-ad-application-gallery---august-2020"></a>Neue Verbund-Apps im Azure AD-Anwendungskatalog verfügbar – August 2020

**Typ:** Neues Feature  
**Dienstkategorie** : Unternehmens-Apps  
**Produktfunktion:** Integration von Drittanbieterprodukten

Im August 2020 haben wir die folgenden 25 neuen Anwendungen mit Verbundunterstützung in unseren App-Katalog aufgenommen:

[Backup365](https://portal.backup365.io/login), [Soapbox](https://app.soapboxhq.com/create?step=auth&provider=azure-ad2-oauth2), [Alma SIS](https://almau.getalma.com/), [Enlyft Dynamics 365 Connector](http://enlyft.com/), [Serraview Space Utilization Software Solutions](../saas-apps/serraview-space-utilization-software-solutions-tutorial.md), [Uniq](https://web.uniq.app/), [Visibly](../saas-apps/visibly-tutorial.md), [Zylo](../saas-apps/zylo-tutorial.md), [Edmentum – Courseware Assessments Exact Path](https://auth.edmentum.com/elf/login), [CyberLAB](https://cyberlab.evolvesecurity.com/#/welcome), [Altamira HRM](../saas-apps/altamira-hrm-tutorial.md), [WireWheel](../saas-apps/wirewheel-tutorial.md), [Zix Compliance and Capture](https://sminstall.zixcorp.com/teams/teams.php?install_request=true&tenant_id=common), [Greenlight Enterprise Business Controls Platform](../saas-apps/greenlight-enterprise-business-controls-platform-tutorial.md), [Genetec Clearance](https://www.clearance.network/), [iSAMS](../saas-apps/isams-tutorial.md), [VeraSMART](../saas-apps/verasmart-tutorial.md), [Amiko](https://amiko.web.rivero.app/), [Twingate](https://auth.twingate.com/signup), [Funnel Leasing](https://nestiolistings.com/sso/oidc/azure/authorize/), [Scalefusion](https://scalefusion.com/users/sign_in/), [Bpanda](https://goto.bpanda.com/login), [Vivun Calendar Connect](https://app.vivun.com/dashboard/calendar/connect), [FortiGate SSL VPN](../saas-apps/fortigate-ssl-vpn-tutorial.md), [Wandera End User](https://www.wandera.com/)

Die Dokumentation zu allen Anwendungen finden Sie auch hier: https://aka.ms/AppsTutorial.

Informationen zum Auflisten Ihrer Anwendung im Azure AD-App-Katalog finden Sie hier: https://aka.ms/AzureADAppRequest.

---

### <a name="resource-forests-now-available-for-azure-ad-ds"></a>Ressourcengesamtstrukturen jetzt für Azure AD DS verfügbar 

**Typ:** Neues Feature- **Dienstkategorie:** Azure AD Domain Services   
**Produktfunktion** : Azure AD Domain Services
 
Die Funktionalität von Ressourcengesamtstrukturen in Azure AD Domain Services ist jetzt allgemein verfügbar. Sie können jetzt die Autorisierung ohne Kennworthashsynchronisierung zur Nutzung von Azure AD Domain Services aktivieren, einschließlich Smartcardautorisierung. Weitere Informationen finden Sie unter [Konzepte und Features zu Replikatgruppen für Azure Active Directory Domain Services (Vorschauversion)](../../active-directory-domain-services/concepts-replica-sets.md).
 
---

### <a name="regional-replica-support-for-azure-ad-ds-managed-domains-now-available"></a>Regionale Replikatunterstützung für verwaltete Azure AD DS-Domänen jetzt verfügbar

**Typ:** Neues Feature   
**Dienstkategorie** : Azure AD Domain Services  
**Produktfunktion** : Azure AD Domain Services
 
Sie können eine verwaltete Domäne erweitern, sodass mehrere Replikatgruppen pro Azure AD-Mandant festgelegt sind. Replikatgruppen können einem beliebigen virtuellen Netzwerk mit Peering in einer beliebigen Azure-Region mit Azure AD Domain Services-Unterstützung hinzugefügt werden. Zusätzliche Replikatgruppen in verschiedenen Azure-Regionen bieten eine geografische Notfallwiederherstellung für Legacyanwendungen, wenn eine Azure-Region offline geschaltet wird. Weitere Informationen finden Sie unter [Konzepte und Features zu Replikatgruppen für Azure Active Directory Domain Services (Vorschauversion)](../../active-directory-domain-services/concepts-replica-sets.md).

---

### <a name="general-availability-of-azure-ad-my-sign-ins"></a>Allgemeine Verfügbarkeit von Azure AD Meine Anmeldungen

**Typ:** Neues Feature  
**Dienstkategorie** : Authentifizierungen (Anmeldungen)  
**Produktfunktion:** Endbenutzerumgebungen
 
Azure AD Meine Anmeldungen ist ein neues Feature, mit dem Unternehmensbenutzer ihren Anmeldeverlauf auf ungewöhnliche Aktivitäten überprüfen können. Darüber hinaus können Endbenutzer mit diesem Feature bei verdächtigen Aktivitäten „Das war ich nicht“ oder „Das war ich“ melden. Weitere Informationen zur Verwendung dieses Features finden Sie unter [Anzeigen und Suchen Ihrer letzten Anmeldeaktivität auf der Seite „Meine Anmeldungen“](../user-help/my-account-portal-sign-ins-page.md#confirm-unusual-activity).
 
---

### <a name="sap-successfactors-hr-driven-user-provisioning-to-azure-ad-is-now-generally-available"></a>Die HR-gesteuerte Benutzerbereitstellung von SAP SuccessFactors in Azure AD ist jetzt allgemein verfügbar

**Typ:** Neues Feature  
**Dienstkategorie:** App-Bereitstellung  
**Produktfunktion:** Identity Lifecycle Management
 
Sie können jetzt SAP SuccessFactors als autoritative Identitätsquelle in Azure AD integrieren und den End-to-End-Identitätslebenszyklus mithilfe von HR-Ereignissen wie Neueinstellungen und Kündigungen automatisieren, um die Bereitstellung und Aufhebung der Bereitstellung von Konten in Azure AD zu fördern. 

Weitere Informationen zum Konfigurieren der eingehenden Bereitstellung von SAP SuccessFactors in Azure AD finden Sie im Tutorial [Konfigurieren der Benutzerbereitstellung von SAP SuccessFactors in Active Directory](../saas-apps/sap-successfactors-inbound-provisioning-tutorial.md).
 
---

### <a name="custom-open-id-connect-ms-graph-api-support-for-azure-ad-b2c"></a>Benutzerdefinierte Open ID Connect-Unterstützung der MS Graph-API für Azure AD B2C

**Typ:** Neues Feature  
**Dienstkategorie** : B2C – Kundenidentitätsverwaltung  
**Produktfunktion:** B2B/B2C
 
Zuvor konnten Anbieter von Custom Open ID Connect nur über das Azure-Portal hinzugefügt oder verwaltet werden. Jetzt können die Azure AD B2C-Kunden diese Anbieter auch über die Betaversion von Microsoft Graph-APIs hinzufügen und verwalten. Informationen zum Konfigurieren dieser Ressource mit APIs finden Sie unter [Ressourcentyp „identityProvider“](/graph/api/resources/identityprovider?view=graph-rest-beta).
 
---

### <a name="assign-azure-ad-built-in-roles-to-cloud-groups"></a>Zuweisen von in Azure AD integrierten Rollen zu Cloudgruppen

**Typ:** Neues Feature  
**Dienstkategorie:** Azure AD-Rollen  
**Produktfunktion:** Zugriffssteuerung

Mit diesem neuen Feature können Sie Cloudgruppen jetzt in Azure AD integrierte Rollen zuweisen. Beispielsweise können Sie der Gruppe „Contoso_SharePoint_Admins“ die SharePoint-Rolle „Administrator“ zuweisen. Sie können die Gruppe auch mithilfe von PIM (Privileged Identity Management) zu einem berechtigten Mitglied der Rolle machen, statt ihr ständigen Zugriff zu gewähren. Informationen zum Konfigurieren dieses Features finden Sie unter [Verwenden von Cloudgruppen zum Verwalten von Rollenzuweisungen in Azure Active Directory (Vorschau)](../roles/groups-concept.md).
 
---

### <a name="insights-business-leader-built-in-role-now-available"></a>Integrierte Rolle „Business Leader für Insights“ jetzt verfügbar

**Typ:** Neues Feature  
**Dienstkategorie:** Azure AD-Rollen  
**Produktfunktion:** Zugriffssteuerung
 
Benutzer in der Rolle „Business Leader für Insights“ können über die [M365-Insights-Anwendung](https://www.microsoft.com/microsoft-365/partners/workplaceanalytics) auf eine Gruppe von Dashboards und Erkenntnissen zugreifen. Dies umfasst Vollzugriff auf alle Dashboards und die dargestellten Funktionen für Erkenntnisse sowie das Durchsuchen von Daten. Benutzer in dieser Rolle haben jedoch keinen Zugriff auf die Einstellungen für Produktkonfiguration, für die die Rolle „Insights-Administrator“ zuständig ist. Weitere Informationen zu dieser Rolle finden Sie unter [Berechtigungen der Administratorrolle in Azure Active Directory](../roles/permissions-reference.md#insights-business-leader).
 
---

### <a name="insights-administrator-built-in-role-now-available"></a>Integrierte Rolle „Insights-Administrator“ jetzt verfügbar

**Typ:** Neues Feature  
**Dienstkategorie:** Azure AD-Rollen  
**Produktfunktion:** Zugriffssteuerung
 
Benutzer in der Rolle „Insights-Administrator“ können auf alle administrativen Funktionen in der [M365-Insights-Anwendung](https://www.microsoft.com/microsoft-365/partners/workplaceanalytics) zugreifen. Ein Benutzer in dieser Rolle kann Verzeichnisinformationen lesen, die Dienstintegrität überwachen, Supporttickets einordnen und auf die Einstellungsaspekte für Insights-Administratoren zugreifen. Weitere Informationen zu dieser Rolle finden Sie unter [Berechtigungen der Administratorrolle in Azure Active Directory](../roles/permissions-reference.md#insights-administrator).
 
--- 

### <a name="application-admin-and-cloud-application-admin-can-manage-extension-properties-of-applications"></a>Anwendungsadministrator und Cloudanwendungsadministrator können Erweiterungseigenschaften von Anwendungen verwalten

**Typ:** Geändertes Feature  
**Dienstkategorie:** Azure AD-Rollen  
**Produktfunktion:** Zugriffssteuerung
 
Zuvor konnte nur der globale Administrator die [Erweiterungseigenschaft](/graph/api/application-post-extensionproperty?view=graph-rest-beta&tabs=http) verwalten. Wir aktivieren diese Funktionalität jetzt auch für den Anwendungsadministrator und den Cloudanwendungsadministrator.
 
---

### <a name="mim-2016-sp2-hotfix-462630-and-connectors-1113010"></a>MIM 2016 SP2 Hotfix 4.6.263.0 und Connectors 1.1.1301.0

**Typ:** Geändertes Feature  
**Dienstkategorie:** Microsoft Identity Manager  
**Produktfunktion:** Identity Lifecycle Management

Ein [Hotfixrollup-Paket (Build 4.6.263.0)](https://support.microsoft.com/help/4576473/hotfix-rollup-package-build-4-6-263-0-is-available-for-microsoft-ident) ist für Microsoft Identity Manager (MIM) 2016 Service Pack 2 (SP2) verfügbar. Dieses Rollup-Paket enthält Updates für die Microsoft Identity Manager-Zertifikatverwaltung (Microsoft Identity Manager Certificate Management, MIM CM), den MIM-Synchronisierungs-Manager und die PAM-Komponenten (Privileged Access Management). Außerdem enthält der Build der MIM-generischen Connectors 1.1.1301.0 Updates für den Graph-Connector.

---
 
## <a name="july-2020"></a>Juli 2020

### <a name="as-an-it-admin-i-want-to-target-client-apps-using-conditional-access"></a>Als IT-Administrator möchte ich Client-Apps mit bedingtem Zugriff als Ziel verwenden

**Typ:** Plan für Änderung   
**Dienstkategorie** : Bedingter Zugriff  
**Produktfunktion:** Identitätssicherheit und -schutz
 
Mit dem allgemein verfügbaren Release der Client-Apps-Bedingung für den bedingten Zugriff gelten neue Richtlinien jetzt standardmäßig für alle Clientanwendungen. Dies schließt auch Clients mit Legacyauthentifizierung ein. Vorhandene Richtlinien bleiben unverändert, jedoch wird die Option *Configure Yes/No* (Ja/Nein konfigurieren) aus vorhandenen Richtlinien entfernt, damit Sie mühelos erkennen können, auf welche Client-Apps die Richtlinie angewendet wird. 

Stellen Sie beim Erstellen einer neuen Richtlinie sicher, dass Sie Benutzer und Dienstkonten ausschließen, die immer noch die Legacy-Authentifizierung nutzen. Wenn Sie dies nicht tun, werden sie gesperrt. [Weitere Informationen](../conditional-access/concept-conditional-access-conditions.md)
 
---

### <a name="upcoming-scim-compliance-fixes"></a>Kommende Korrekturen der SCIM-Konformität

**Typ:** Plan für Änderung  
**Dienstkategorie:** App-Bereitstellung  
**Produktfunktion** : Verwaltung des Identitätslebenszyklus
 
Der Azure AD-Bereitstellungsdienst nutzt den SCIM-Standard für die Integration mit Anwendungen. Unsere Implementierung des SCIM-Standards entwickelt sich weiter, und wir gehen davon aus, dass sich unser Verhalten für die Durchführung von PATCH-Vorgängen und zum Festlegen der Eigenschaft „Aktiv“ für eine Ressource ändern muss. [Weitere Informationen](../app-provisioning/application-provisioning-config-problem-scim-compatibility.md)
 
---

### <a name="group-owner-setting-on-azure-admin-portal-will-be-changed"></a>Die Gruppenbesitzereinstellung im Azure-Administratorportal wird geändert

**Typ:** Plan für Änderung  
**Dienstkategorie** : Gruppenverwaltung  
**Produktfunktion:** Kollaboration

Die Besitzereinstellungen auf der allgemeinen Einstellungsseite für Gruppen können dazu konfiguriert werden, die Besitzerzuweisungsberechtigungen auf eine beschränkte Benutzergruppe im Azure-Administratorportal und Zugriffsbereich einzuschränken. Schon bald verfügen wir über die Möglichkeit, Gruppenbesitzerberechtigungen nicht nur über diese zwei Benutzerportale zuzuweisen, sondern die Richtlinie auch auf dem Back-End zu erzwingen, um ein konsistentes Verhalten über Endpunkte hinweg bereitzustellen, z. B. PowerShell und Microsoft Graph. 

Zunächst wird die aktuelle Einstellung für die Kunden deaktiviert, die sie nicht verwenden, und eine Option wird in den nächsten Monaten angeboten, um Benutzer mit Gruppenbesitzerberechtigungen zu suchen. Eine Anleitung zum Ändern der Gruppeneinstellungen finden Sie unter [Bearbeiten Ihrer Gruppeninformationen in Azure Active Directory](./active-directory-groups-settings-azure-portal.md?context=azure%2factive-directory%2fusers-groups-roles%2fcontext%2fugr-context).

---

### <a name="azure-active-directory-registration-service-is-ending-support-for-tls-10-and-11"></a>Die Unterstützung von TLS 1.0 und 1.1 des Azure Active Directory Device Registration-Dienst wird beendet

**Typ:** Plan für Änderung  
**Dienstkategorie:** Geräteregistrierung und -verwaltung  
**Produktfunktion** : Plattform

TLS 1.2 (Transport Layer Security) und Updateserver und Clients kommunizieren bald mit dem Azure Active Directory Device Registration-Dienst. Die Unterstützung von TLS 1.0 und 1.1 für die Kommunikation mit dem Azure Active Directory Device Registration-Dienst wird eingestellt:
- Am 31. August 2020 für alle Sovereign Clouds (GCC High, DoD, usw.)
- Am 30. Oktober 2020 für alle kommerziellen Clouds

[Hier erfahren Sie mehr](../devices/reference-device-registration-tls-1-2.md) über TLS 1.2 für den Azure Active Directory Device Registration-Dienst.

---

### <a name="windows-hello-for-business-sign-ins-visible-in-azure-ad-sign-in-logs"></a>Windows Hello for Business-Anmeldungen in Azure AD-Anmeldeprotokollen sichtbar

**Typ:** Korrigiert  
**Dienstkategorie** : Berichterstellung  
**Produktfunktion:** Überwachung und Berichterstellung
 
Windows Hello for Business ermöglicht Endbenutzern die Anmeldung bei Windows-Computern mit einer Geste (z. B. PIN oder Biometrie). Azure AD-Administratoren sollten im Rahmen der Einführung der kennwortlosen Authentifizierung in ihrer Organisation zwischen Windows Hello for Business-Anmeldungen und anderen Windows-Anmeldungen unterscheiden. 

Administratoren können nun sehen, ob Windows Hello for Business für eine Windows-Authentifizierung genutzt wurde, indem sie im Azure-Portal die Registerkarte „Details zur Authentifizierung“ für ein Windows-Anmeldeereignis im Blatt „Azure AD-Anmeldungen“ überprüfen. Windows Hello for Business-Authentifizierungen enthalten nun „WindowsHelloForBusiness“ im Feld „Authentifizierungsmethode“. Weitere Informationen zum Interpretieren von Anmeldeprotokollen finden Sie in der [Dokumentation zu Anmeldeprotokollen](../reports-monitoring/concept-sign-ins.md).
 
---

### <a name="fixes-to-group-deletion-behavior-and-performance-improvements"></a>Korrekturen am Gruppenlöschverhalten und Leistungsverbesserungen

**Typ:** Korrigiert  
**Dienstkategorie:** App-Bereitstellung  
**Produktfunktion** : Verwaltung des Identitätslebenszyklus
 
Zuvor wurde das Gruppenobjekt nicht gelöscht, wenn eine Gruppe von „in-scope“ (Im Geltungsbereich) zu „out-of-scope“ (Außerhalb des Geltungsbereichs) geändert wurde und ein Administrator auf „Neu starten“ geklickt hat, bevor die Änderung durchgeführt wurde. Nun wird das Gruppenobjekt aus der Zielanwendung gelöscht, sobald sie den Geltungsbereich verlässt (wenn sie deaktiviert, gelöscht, ihre Zuweisung aufgehoben wird oder sie hat den Bereichsfilter nicht bestanden). [Weitere Informationen](../app-provisioning/how-provisioning-works.md#incremental-cycles)
 
---

### <a name="public-preview-admins-can-now-add-custom-content-in-the-email-to-reviewers-when-creating-an-access-review"></a>Public Preview: Administratoren können nun benutzerdefinierte Inhalte zur E-Mail an Prüfer hinzufügen, wenn sie eine Zugriffsüberprüfung erstellen

**Typ:** Neue Funktion  
**Dienstkategorie** : Zugriffsüberprüfungen  
**Produktfunktion:** Identity Governance
 
Wenn eine neue Zugriffsüberprüfung erstellt wird, empfängt der Prüfer eine E-Mail, in der er zum Abschließen der Zugriffsüberprüfung aufgefordert wird. Viele unserer Kunden haben nach einer Möglichkeit gefragt, benutzerdefinierte Inhalte zur E-Mail hinzuzufügen, z. B. Kontaktinformationen oder andere zusätzliche Inhalte, die dem Prüfer helfen können. 

Mit diesem nun in der öffentlichen Vorschau verfügbaren Feature können Administratoren benutzerdefinierte Inhalte in der E-Mail an Prüfer angeben, indem sie Inhalte im Abschnitt „Erweitert“ der Azure AD-Zugriffsüberprüfungen hinzufügen. Eine Anleitung zum Erstellen von Zugriffsüberprüfungen finden Sie unter [Erstellen von Zugriffsüberprüfungen für Gruppen und Anwendungen in Azure AD-Zugriffsüberprüfungen](../governance/create-access-review.md).
 
---

### <a name="authorization-code-flow-for-single-page-apps-available"></a>Autorisierungscodeflow für Single-Page-Apps verfügbar

**Typ:** Neues Feature  
**Dienstkategorie** : Authentifizierungen (Anmeldungen)  
**Produktfunktion** : Entwickleroberfläche
 
Aufgrund der Einschränkungen für Cookies von Drittanbietern von modernen Browsern, z. B. Safari ITP, müssen Single-Page-Webanwendungen den Autorisierungscodeflow verwenden, anstatt den impliziten Flow zum Verwalten des einmaligen Anmeldens zu verwenden. Außerdem unterstützt MSAL.js v 2.x nun den Autorisierungscodeflow. 

Es gibt entsprechende Updates für das Azure-Portal, mit denen Sie Ihre Single-Page-Webanwendung mit dem Typ „spa“ aktualisieren und den Autorisierungscodeflow verwenden können. Weitere Informationen finden Sie unter [Anmelden von Benutzern und Abrufen eines Zugriffstokens in einer JavaScript-SPA mithilfe des Autorisierungscodeflows](../develop/quickstart-v2-javascript-auth-code.md).
 
---

### <a name="azure-ad-application-proxy-now-supports-the-remote-desktop-services-web-client"></a>Der Azure AD-Anwendungsproxy unterstützt nun den Webclient für Remotedesktopdienste

**Typ:** Neue Funktion  
**Dienstkategorie:** Anwendungsproxy  
**Produktfunktion:** Zugriffssteuerung

Der Azure AD-Anwendungsproxy unterstützt nun den Webclient für Remotedesktopdienste. Der Webclient für Remotedesktopdienste ermöglicht Benutzern den Zugriff auf die Remotedesktopinfrastruktur über HTML5-fähige Browser wie Microsoft Edge, Internet Explorer 11, Google Chrome usw. Benutzer können von überall mit Remote-Apps oder -desktops interagieren, wie sie es mit einem lokalen Gerät tun würden. Mithilfe des Azure AD-Anwendungsproxys können Sie die Sicherheit Ihrer RDS-Bereitstellung erhöhen, indem Sie die Vorauthentifizierung und die Richtlinien für bedingten Zugriff für alle Arten von Rich Client-Apps erzwingen. Eine Anleitung finden Sie unter [Veröffentlichen des Remotedesktops per Azure AD-Anwendungsproxy](../manage-apps/application-proxy-integrate-with-remote-desktop-services.md).
 
---

### <a name="next-generation-azure-ad-b2c-user-flows-in-public-preview"></a>Azure Active Directory-B2C-Benutzerflows der nächsten Generation in der öffentlichen Vorschau

**Typ:** Neue Funktion  
**Dienstkategorie** : B2C – Kundenidentitätsverwaltung  
**Produktfunktion** : B2B/B2C
 
Die vereinfachte Oberfläche für Benutzerflows bietet Featureparität mit Previewfunktionen und ist der Ort, an dem alle neuen Features bereitgestellt werden. Benutzer können innerhalb eines einzigen Benutzerflows neue Features aktivieren. Auf diese Weise entfällt die Notwendigkeit, mit jedem neuen Featurerelease mehrere Versionen zu erstellen. Darüber hinaus vereinfacht die neue, benutzerfreundliche Oberfläche die Auswahl und Erstellung von Benutzerflows. Testen Sie es jetzt, indem Sie [einen Benutzerflow erstellen](../../active-directory-b2c/tutorial-create-user-flows.md). 

Weitere Informationen über Benutzerflows finden Sie unter [Benutzerflowversionen in Azure Active Directory B2C](../../active-directory-b2c/user-flow-versions.md#:~:text=    User flow  ,account. Usi ...  1 more rows ).

---

### <a name="new-federated-apps-available-in-azure-ad-application-gallery---july-2020"></a>Neue Verbund-Apps im Azure AD-Anwendungskatalog verfügbar – Juli 2020

**Typ:** Neue Funktion  
**Dienstkategorie** : Unternehmens-Apps  
**Produktfunktion** : Integration von Drittanbieteranwendungen
 
Im Juli 2020 haben wir die folgenden 55 neuen Anwendungen mit Verbundunterstützung in unseren App-Katalog aufgenommen:

[Clap Your Hands](http://www.rmit.com.ar/), [Appreiz](https://microsoftteams.appreiz.com/), [Inextor Vault](https://inexto.com/inexto-suite/inextor), [Beekast](https://my.beekast.com/), [Templafy OpenID Connect](https://app.templafy.com/), [PeterConnects receptionist](https://msteams.peterconnects.com/), [AlohaCloud](https://appfusions.alohacloud.com/auth), [Control Tower](https://bpm.tnxcorp.com/sso/microsoft), [Cocoom](https://start.cocoom.com/), [COINS Construction Cloud](https://sso.coinsconstructioncloud.com/#login/), [Medxnote MT](https://task.teamsmain.medx.im/authorization), [Reflekt](https://reflekt.konsolute.com/login), [Rever](https://app.reverscore.net/access), [MyCompanyArchive](https://login.mycompanyarchive.com/), [GReminders](https://app.greminders.com/o365-oauth), [Titanfile](../saas-apps/titanfile-tutorial.md), [Wootric](../saas-apps/wootric-tutorial.md), [SolarWinds Orion](https://support.solarwinds.com/SuccessCenter/s/orion-platform?language=en_US),  [OpenText Directory Services](../saas-apps/opentext-directory-services-tutorial.md), [Datasite](../saas-apps/datasite-tutorial.md), [BlogIn](../saas-apps/blogin-tutorial.md), [IntSights](../saas-apps/intsights-tutorial.md), [kpifire](../saas-apps/kpifire-tutorial.md), [Textline](../saas-apps/textline-tutorial.md), [Cloud Academy - SSO](../saas-apps/cloud-academy-sso-tutorial.md), [Community Spark](../saas-apps/community-spark-tutorial.md), [Chatwork](../saas-apps/chatwork-tutorial.md), [CloudSign](../saas-apps/cloudsign-tutorial.md), [C3M Cloud Control](../saas-apps/c3m-cloud-control-tutorial.md), [SmartHR](https://smarthr.jp/), [NumlyEngage™](../saas-apps/numlyengage-tutorial.md), [Michigan Data Hub Single Sign-On](../saas-apps/michigan-data-hub-single-sign-on-tutorial.md), [Egress](../saas-apps/egress-tutorial.md), [SendSafely](../saas-apps/sendsafely-tutorial.md), [Eletive](https://app.eletive.com/), [Right-Hand Cybersecurity ADI](https://right-hand.ai/), [Fyde Enterprise Authentication](https://enterprise.fyde.com/), [Verme](../saas-apps/verme-tutorial.md), [Lenses.io](../saas-apps/lensesio-tutorial.md), [Momenta](../saas-apps/momenta-tutorial.md), [Uprise](https://app.uprise.co/sign-in), [Q](https://q.moduleq.com/login), [CloudCords](../saas-apps/cloudcords-tutorial.md), [TellMe Bot](https://tellme365liteweb.azurewebsites.net/), [Inspire](https://app.inspiresoftware.com/), [Maverics Identity Orchestrator SAML Connector](https://www.strata.io/identity-fabric/), [Smartschool (School Management System)](https://smartschoolz.com/login), [Zepto - Intelligent timekeeping](https://user.zepto-ai.com/signin), [Studi.ly](https://studi.ly/), [Trackplan](http://www.trackplanfm.com/), [Skedda](../saas-apps/skedda-tutorial.md), [WhosOnLocation](../saas-apps/whos-on-location-tutorial.md), [Coggle](../saas-apps/coggle-tutorial.md), [Kemp LoadMaster](https://kemptechnologies.com/cloud-load-balancer/), [BrowserStack Single Sign-on](../saas-apps/browserstack-single-sign-on-tutorial.md)

Die Dokumentation zu allen Anwendungen finden Sie auch hier: https://aka.ms/AppsTutorial.

Informationen zum Auflisten Ihrer Anwendung im Azure AD-App-Katalog finden Sie hier: https://aka.ms/AzureADAppRequest.

---

### <a name="new-provisioning-connectors-in-the-azure-ad-application-gallery---july-2020"></a>Neue Bereitstellungsconnectors im Azure AD-Anwendungskatalog – Juli 2020

**Typ:** Neues Feature  
**Dienstkategorie:** App-Bereitstellung  
**Produktfunktion** : Integration von Drittanbieteranwendungen

Sie können ab sofort das Erstellen, Aktualisieren und Löschen von Benutzerkonten für diese neu integrierten Apps automatisieren: [LinkedIn Learning](../saas-apps/linkedin-learning-provisioning-tutorial.md).

Weitere Informationen dazu, wie Sie Ihre Organisation durch die automatisierte Bereitstellung von Benutzerkonten besser schützen können, finden Sie unter [Automatisieren der Bereitstellung und Bereitstellungsaufhebung von Benutzern für SaaS-Anwendungen mit Azure Active Directory](../app-provisioning/user-provisioning.md).

---

### <a name="view-role-assignments-across-all-scopes-and-ability-to-download-them-to-a-csv-file"></a>Anzeigen von Rollenzuweisungen für alle Bereiche und Herunterladen dieser in eine CSV-Datei

**Typ:** Geänderte Funktion  
**Dienstkategorie:** Azure AD-Rollen  
**Produktfunktion** : Zugriffssteuerung
 
Sie können nun die Rollenzuweisungen aller Bereiche für eine Rolle auf der Registerkarte „Rollen und Administratoren“ im Azure AD-Portal anzeigen. Sie können diese Rollenzuweisungen für jede Rolle auch in eine CSV-Datei herunterladen. Eine Anleitung zum Anzeigen und Hinzufügen von Rollenzuweisungen finden Sie unter [Anzeigen und Zuweisen von Administratorrollen in Azure Active Directory](../roles/manage-roles-portal.md).
 
---

### <a name="azure-multi-factor-authentication-software-development-azure-mfa-sdk-deprecation"></a>Veraltetes Azure Multi-Factor Authentication Software Development Kit (Azure MFA SDK)

**Typ** : Veraltet  
**Dienstkategorie:** MFA  
**Produktfunktion** : Identitätssicherheit und -schutz
 
Das Azure MFA SDK hat am 14. November 2018 das Ende der Lebensdauer erreicht, wie erstmals im November 2017 angekündigt. Microsoft stellt den SDK-Dienst ab dem 30. September 2020 ein. Jegliche Aufrufe des SDK werden fehlschlagen.

Wenn Ihre Organisation das Azure MFA SDK verwendet, müssen Sie bis zum 30. September 2020 migrieren:
- Azure MFA SDK für MIM:  Wenn Sie das SDK mit MIM verwenden, sollten Sie zu Azure MFA-Server migrieren und PAM (Privileged Access Management) aktivieren, indem Sie [diese Anweisungen](/microsoft-identity-manager/working-with-mfaserver-for-mim) befolgen.   
- Azure MFA SDK für benutzerdefinierte Apps: Erwägen Sie eine Integration Ihrer App mit Azure AD und die Verwendung des bedingten Zugriffs, um die mehrstufige Authentifizierung zu erzwingen. Informationen zu den ersten Schritten finden Sie auf dieser [Seite](../manage-apps/plan-an-application-integration.md). 

---

## <a name="june-2020"></a>Juni 2020 

### <a name="user-risk-condition-in-conditional-access-policy"></a>Die Bedingung „Benutzerrisiko“ in der Richtlinie für bedingten Zugriff

**Typ:** Plan für Änderung  
**Dienstkategorie** : Bedingter Zugriff  
**Produktfunktion:** Identitätssicherheit und -schutz
 

Die Unterstützung des Benutzerrisikos in der Azure AD-Richtlinie für bedingten Zugriff ermöglicht es Ihnen, mehrere benutzerrisikobasierte Richtlinien zu erstellen. Für verschiedene Benutzer und Apps sind unter Umständen unterschiedliche Mindestbenutzerrisikostufen erforderlich. Basierend auf dem Benutzerrisiko können Sie Richtlinien erstellen, um den Zugriff zu blockieren oder eine mehrstufige Authentifizierung, eine sichere Kennwortänderung oder eine Umleitung zu Microsoft Cloud App Security zum Erzwingen von Sitzungsrichtlinien zu erfordern, wie z. B. eine zusätzliche Überwachung.

Die Benutzerrisikobedingung erfordert Azure AD Premium P2, da sie Azure Identity Protection verwendet, wobei es sich um ein P2-Angebot handelt. Weitere Informationen zum bedingten Zugriff finden Sie unter [Dokumentation zum bedingten Zugriff mit Azure AD](../conditional-access/index.yml).

---

### <a name="saml-sso-now-supports-apps-that-require-spnamequalifier-to-be-set-when-requested"></a>SAML SSO unterstützt jetzt Apps, bei denen „SPNameQualifier“ nach Aufforderung festgelegt werden muss.

**Typ:** Korrigiert  
**Dienstkategorie** : Unternehmens-Apps  
**Produktfunktion:** SSO
 
Einige SAML-Anwendungen erfordern, dass „SPNameQualifier“ bei Anforderung im Assertionbetreff zurückgegeben wird. Nun antwortet Azure AD ordnungsgemäß, wenn ein „SPNameQualifier“ in der Anforderungs-NameID-Richtlinie angefordert wird. Dies funktioniert auch für die SP-initiierte Anmeldung, und die IDP-initiierte Anmeldung folgt.  Weitere Informationen zum SAML-Protokoll in Azure Active Directory finden Sie unter [SAML-Protokoll für einmaliges Anmelden](../develop/single-sign-on-saml-protocol.md).

---

### <a name="azure-ad-b2b-collaboration-supports-inviting-msa-and-google-users-in-azure-government-tenants"></a>Azure AD B2B Collaboration unterstützt das Einladen von MSA- und Google-Benutzern in Azure Government-Mandanten.

**Typ:** Neues Feature  
**Dienstkategorie:** B2B  
**Produktfunktion:** B2B/B2C
 

Azure Government-Mandanten, die die B2B-Zusammenarbeitsfunktionen verwenden, können Benutzer jetzt mit einem Microsoft- oder Google-Konto einladen. Um festzustellen, ob Ihr Mandant diese Funktionen nutzen kann, befolgen Sie die Anweisungen unter [Wie kann ich erkennen, ob die B2B-Zusammenarbeit in meinem Mandanten der Azure-Cloud für US-Behörden verfügbar ist?](../external-identities/current-limitations.md#how-can-i-tell-if-b2b-collaboration-is-available-in-my-azure-us-government-tenant).

 
---
 
### <a name="user-object-in-ms-graph-v1-now-includes-externaluserstate-and-externaluserstatechangeddatetime-properties"></a>Das Benutzerobjekt in MS Graph v1 enthält nun die Eigenschaften „externalUserState“ und „externalUserStateChangedDateTime“.

**Typ:** Neues Feature  
**Dienstkategorie:** B2B  
**Produktfunktion:** B2B/B2C
 

Die Eigenschaften „externalUserState“ und „externalUserStateChangedDateTime“ können zum Auffinden von eingeladenen B2B-Gäste verwendet werden, die ihre Einladungen noch nicht akzeptiert haben, sowie zur Automatisierung wie etwa zum Löschen von Benutzern, die ihre Einladungen nach einigen Tagen nicht akzeptiert haben. Diese Eigenschaften sind jetzt in MS Graph v1 verfügbar. Anleitungen zur Verwendung dieser Eigenschaften finden Sie unter [Benutzerressourcentyp](/graph/api/resources/user?view=graph-rest-1.0).
 
---

### <a name="manage-authentication-sessions-in-azure-ad-conditional-access-is-now-generally-available"></a>Verwalten von Authentifizierungssitzungen im bedingten Azure AD-Zugriff ist jetzt allgemein verfügbar

**Typ:** Neues Feature  
**Dienstkategorie** : Bedingter Zugriff  
**Produktfunktion:** Identitätssicherheit und -schutz
 
Die Verwaltungsfunktionen für Authentifizierungssitzungen erlauben es Ihnen, zu konfigurieren, wie oft Ihre Benutzer Anmeldeinformationen bereitstellen müssen und ob sie Anmeldeinformationen nach dem Schließen und erneuten Öffnen des Browsers angeben müssen, um mehr Sicherheit und Flexibilität in Ihrer Umgebung zu erreichen.
 
Zusätzlich wurde die Verwaltung von Authentifizierungssitzungen bisher nur für die einstufige Authentifizierung auf Geräten angewendet, die in Azure AD oder Azure AD Hybrid eingebunden und bei Azure AD registriert waren. Jetzt gilt die Verwaltung von Authentifizierungssitzungen auch für MFA. Weitere Informationen finden Sie unter [Konfigurieren der Verwaltung von Authentifizierungssitzungen mit bedingtem Zugriff](../conditional-access/howto-conditional-access-session-lifetime.md).

---

### <a name="new-federated-apps-available-in-azure-ad-application-gallery---june-2020"></a>Neue Verbund-Apps im Azure AD-Anwendungskatalog verfügbar – Juni 2020

**Typ:** Neues Feature  
**Dienstkategorie** : Unternehmens-Apps  
**Produktfunktion:** Integration von Drittanbieterprodukten
 
Im Juni 2020 haben wir die folgenden 29 neuen Anwendungen mit Verbundunterstützung in unseren App-Katalog aufgenommen:

[Shopify Plus](../saas-apps/shopify-plus-tutorial.md), [Ekarda](../saas-apps/ekarda-tutorial.md), [MailGates](../saas-apps/mailgates-tutorial.md), [BullseyeTDP](../saas-apps/bullseyetdp-tutorial.md), [Raketa](../saas-apps/raketa-tutorial.md), [Segment](../saas-apps/segment-tutorial.md), [Ai Auditor](https://www.mindbridge.ai/products/ai-auditor/), [Pobuca Connect](https://app.pobu.ca/), [Proto.io](../saas-apps/proto.io-tutorial.md), [Gatekeeper](https://www.gatekeeperhq.com/), [Hub Planner](../saas-apps/hub-planner-tutorial.md), [Ansira-Partner Go-to-Market Toolbox](https://ansira.com/technology/channel-engagement), [IBM Digital Business Automation on Cloud](../saas-apps/ibm-digital-business-automation-on-cloud-tutorial.md), [Kisi Physical Security](../saas-apps/kisi-physical-security-tutorial.md), [ViewpointOne](https://team.viewpoint.com/), [IntelligenceBank](../saas-apps/intelligencebank-tutorial.md), [pymetrics](../saas-apps/pymetrics-tutorial.md), [Zero](https://www.teamzero.com/), [InStation](https://instation.invillia.com/), [edX for Business SAML 2.0 Integration](../saas-apps/edx-for-business-saml-integration-tutorial.md), [MOOC Office 365](https://mooc.office365-training.com/en/), [SmartKargo](../saas-apps/smartkargo-tutorial.md), [PKIsigning-Plattform](https://platform.pkisigning.nl/), [SiteIntel](../saas-apps/siteintel-tutorial.md), [Field iD](../saas-apps/field-id-tutorial.md), [Curricula SAML](../saas-apps/curricula-saml-tutorial.md), [Perforce Helix Core - Helix Authentication Service](../saas-apps/perforce-helix-core-tutorial.md), [MyCompliance Cloud](https://cloud.metacompliance.com/), [Smallstep SSH](https://smallstep.com/sso-ssh/)  

Die Dokumentation zu allen Anwendungen finden Sie auch hier: https://aka.ms/AppsTutorial. Informationen zum Auflisten Ihrer Anwendung im Azure AD-App-Katalog finden Sie hier: https://aka.ms/AzureADAppRequest.

---

### <a name="api-connectors-for-external-identities-self-service-sign-up-are-now-in-public-preview"></a>API-Connectors für die Self-Service-Registrierung für externe Identitäten befinden sich jetzt in der öffentlichen Vorschau.

**Typ:** Neues Feature  
**Dienstkategorie:** B2B  
**Produktfunktion:** B2B/B2C
 
API-Connectors für externe Identitäten ermöglichen es Ihnen, Web-APIs zu nutzen, um die Self-Service-Registrierung für externe Cloudsysteme zu integrieren. Dies bedeutet, dass Sie jetzt Web-APIs als spezifische Schritte in einem Registrierungsablauf aufrufen können, um cloudbasierte benutzerdefinierte Workflows auszulösen. Beispielsweise können Sie mit API-Connectors folgende Aktionen ausführen:

- Integrieren in einen benutzerdefinierten Genehmigungsworkflow
- Durchführen eines Identitätsnachweises
- Überprüfen von Benutzereingabedaten
- Überschreiben von Benutzerattributen
- Ausführen von benutzerdefinierter Geschäftslogik

Weitere Informationen zu allen Möglichkeiten von API-Connectors finden Sie unter [Verwenden von API-Connectors zum Anpassen und Erweitern der Self-Service-Registrierung](../external-identities/api-connectors-overview.md) oder [Anpassen der Self-Service-Registrierung für externe Identitäten mit Web-API-Integrationen](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/customize-external-identities-self-service-sign-up-with-web-api/ba-p/1257364#.XvNz2fImuQg.linkedin).
 
---

### <a name="provision-on-demand-and-get-users-into-your-apps-in-seconds"></a>Bedarfsgesteuertes Bereitstellen und Bereitstellen von Benutzern in Ihren Apps in Sekundenschnelle

**Typ:** Neues Feature  
**Dienstkategorie:** App-Bereitstellung  
**Produktfunktion:** Identity Lifecycle Management
 
Der Azure AD-Bereitstellungsdienst wird zurzeit zyklisch betrieben. Der Dienst wird alle 40 Minuten ausgeführt. Mit der [bedarfsorientierten Bereitstellung](https://aka.ms/provisionondemand) können Sie einen Benutzer auswählen und in wenigen Sekunden bereitstellen. Mit dieser Funktion können Sie Probleme bei der Bereitstellung schnell beheben, ohne dass ein Neustart erforderlich ist, um einen erneuten Start des Bereitstellungsprozesses zu erzwingen. 
 
---

### <a name="new-permission-for-using-azure-ad-entitlement-management-in-graph"></a>Neue Berechtigung zum Verwenden der Azure AD-Berechtigungsverwaltung in Graph

**Typ:** Neues Feature  
**Dienstkategorie:** Sonstige  
**Produktfunktion:** Berechtigungsverwaltung
 
Die neue delegierte Berechtigung „EntitlementManagement.Read.All“ ist jetzt für die Verwendung mit der Berechtigungsverwaltungs-API in Microsoft Graph Beta verfügbar. Weitere Informationen zu den verfügbaren APIs finden Sie unter [Arbeiten mit der Azure AD-Berechtigungsverwaltungs-API](/graph/api/resources/entitlementmanagement-root?view=graph-rest-beta).

---

### <a name="identity-protection-apis-available-in-v10"></a>In v1.0 verfügbare Identity Protection-APIs

**Typ:** Neues Feature  
**Dienstkategorie** : Identitätsschutz  
**Produktfunktion:** Identitätssicherheit und -schutz
 
Die Microsoft Graph-APIs „riskyUsers“ und „riskDetections“ sind jetzt allgemein verfügbar. Nachdem sie nun am v 1.0-Endpunkt verfügbar sind, laden wir Sie ein, sie in der Produktion zu verwenden. Weitere Informationen finden Sie unter [Microsoft Graph-Dokumente](/graph/api/resources/identityprotectionroot?view=graph-rest-1.0).
 
---

### <a name="sensitivity-labels-to-apply-policies-to-microsoft-365-groups-is-now-generally-available"></a>Vertraulichkeitsbezeichnungen zum Anwenden von Richtlinien auf Microsoft 365-Gruppen sind jetzt allgemein verfügbar

**Typ:** Neues Feature  
**Dienstkategorie** : Gruppenverwaltung  
**Produktfunktion:** Kollaboration
 

Sie können jetzt Vertraulichkeitsbezeichnungen erstellen und mithilfe der Bezeichnungseinstellungen Richtlinien auf Microsoft 365-Gruppen anwenden, einschließlich Richtlinien für den Datenschutz (öffentlich oder privat) und den externen Benutzerzugriff. Sie können eine Bezeichnung mit der Datenschutzrichtlinie erstellen, die privat ist, und eine Richtlinie für den externen Benutzerzugriff, damit das Hinzufügen von Gastbenutzern nicht zulässig ist. Wenn ein Benutzer diese Bezeichnung auf eine Gruppe anwendet, ist die Gruppe privat, und es dürfen keine Gastbenutzer zur Gruppe hinzugefügt werden. 

Vertraulichkeitsbezeichnungen sind wichtig, um Ihre unternehmenskritischen Daten zu schützen und Gruppen im großen Stil compliant und sicher zu verwalten. Informationen zum Verwenden von Vertraulichkeitsbezeichnungen finden Sie unter [Zuweisen von Vertraulichkeitsbezeichnungen zu Microsoft 365-Gruppen in Azure Active Directory (Vorschau)](../enterprise-users/groups-assign-sensitivity-labels.md).
 
---

### <a name="updates-to-support-for-microsoft-identity-manager-for-azure-ad-premium-customers"></a>Aktualisierungen für die Unterstützung von Microsoft Identity Manager für Azure AD Premium-Kunden

**Typ:** Geändertes Feature  
**Dienstkategorie:** Microsoft Identity Manager  
**Produktfunktion:** Identity Lifecycle Management
 
Der Azure-Support ist jetzt für Azure AD-Integrationskomponenten von Microsoft Identity Manager 2016 verfügbar, und zwar bis zum Ende des erweiterten Supports für Microsoft Identity Manager 2016. Weitere Informationen finden Sie unter [Supportupdate für Azure AD Premium-Kunden, die Microsoft Identity Manager verwenden](/microsoft-identity-manager/support-update-for-azure-active-directory-premium-customers).

---

### <a name="the-use-of-group-membership-conditions-in-sso-claims-configuration-is-increased"></a>Die Verwendung von Bedingungen für Gruppenmitgliedschaften bei der Konfiguration von SSO-Ansprüchen wurde erweitert

**Typ:** Geändertes Feature  
**Dienstkategorie** : Unternehmens-Apps  
**Produktfunktion:** SSO
 
Bisher war die Anzahl der Gruppen, die Sie verwenden können, wenn Sie Ansprüche basierend auf der Gruppenmitgliedschaft in einer einzelnen Anwendungskonfiguration bedingt ändern, auf 10 beschränkt. Die Verwendung von Bedingungen für Gruppenmitgliedschaften bei der Konfiguration von SSO-Ansprüchen ist auf maximal 50 Gruppen gestiegen. Weitere Informationen zum Konfigurieren von Ansprüchen finden Sie unter [Konfiguration von SSO-Ansprüchen für Unternehmensanwendungen](../develop/active-directory-saml-claims-customization.md#emitting-claims-based-on-conditions). 

---

### <a name="enabling-basic-formatting-on-the-sign-in-page-text-component-in-company-branding"></a>Aktivieren der grundlegenden Formatierung im Text der Anmeldeseite im Unternehmensbranding

**Typ:** Geändertes Feature  
**Dienstkategorie** : Authentifizierungen (Anmeldungen)  
**Produktfunktion:** Benutzerauthentifizierung
 
Die Unternehmensbrandingfunktion für die Azure AD-/Microsoft 365-Anmeldung wurde aktualisiert, damit der Kunde Hyperlinks und einfache Formatierungen hinzufügen kann, einschließlich fett, unterstrichen und kursiv. Anweisungen zur Verwendung dieser Funktion erhalten Sie unter [Hinzufügen von Branding zur Azure Active Directory-Anmeldeseite Ihrer Organisation](./customize-branding.md).

---

### <a name="provisioning-performance-improvements"></a>Leistungsverbesserungen bei der Bereitstellung

**Typ:** Geändertes Feature  
**Dienstkategorie:** App-Bereitstellung  
**Produktfunktion:** Identity Lifecycle Management
 
Der Bereitstellungsdienst wurde aktualisiert, um die Zeit bis zum Abschluss eines [inkrementellen Zyklus](../app-provisioning/how-provisioning-works.md#incremental-cycles) zu verkürzen. Das bedeutet, dass Benutzer und Gruppen in ihren Anwendungen schneller bereitgestellt werden als zuvor. Alle neuen Bereitstellungsaufträge, die nach dem 10.06.2020 erstellt werden, profitieren automatisch von den Leistungsverbesserungen. Alle Anwendungen, die für die Bereitstellung vor dem 10.06.2020 konfiguriert wurden, müssen nach dem 10.06.2020 einmal neu gestartet werden, um die Leistungsverbesserungen zu nutzen. 

---

### <a name="announcing-the-deprecation-of-adal-and-ms-graph-parity"></a>Ankündigung der Veraltung der Parität von ADAL und MS Graph

**Typ:** Als veraltet markiert  
**Dienstkategorie:** –  
**Produktfunktion:** Lebenszyklusverwaltung für Geräte

Nachdem die Microsoft-Authentifizierungsbibliothek (Microsoft Authentication Library, MSAL) nun verfügbar ist, werden die Sicherheitspatches für die Azure Active Directory-Authentifizierungsbibliothek (Azure Active Directory Authentication Library, ADAL) ab dem 30.06.2022 eingestellt. Weitere Informationen zur Migration zu MSAL finden Sie unter [Migrieren von Anwendungen zu Microsoft Authentication Library (MSAL)](../develop/msal-migration.md).

Außerdem haben wir die Arbeit abgeschlossen, um alle Azure AD Graph-Funktionen über MS Graph verfügbar zu machen. Daher erhalten Azure AD Graph-APIs bis zum 30.06.2022 nur Fehlerbehebungen und Sicherheitskorrekturen. Weitere Informationen finden Sie unter [Aktualisieren Ihrer Anwendungen für die Verwendung von Microsoft Authentication Library und der Microsoft Graph-API](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/update-your-applications-to-use-microsoft-authentication-library/ba-p/1257363)
 
---
 
## <a name="may-2020"></a>Mai 2020

### <a name="retirement-of-properties-in-signins-riskyusers-and-riskdetections-apis"></a>Außerbetriebnahme von Eigenschaften in signIns-, riskyUsers- und riskDetections-APIs

**Typ:** Plan für Änderung  
**Dienstkategorie** : Identitätsschutz  
**Produktfunktion:** Identitätssicherheit und -schutz

Derzeit werden Aufzählungstypen verwendet, um die Eigenschaft „riskType“ in der riskDetections-API und in „riskyUserHistoryItem“ (Vorschauversion) darzustellen. Aufzählungstypen werden auch für die riskEventTypes-Eigenschaft in der signIns-API verwendet. In Zukunft werden diese Eigenschaften als Zeichenfolgen dargestellt. 

Kunden müssen bis zum 09.09.2020 auf die riskEventType-Eigenschaft in der riskDetections-API (Betaversion) und der riskyUserHistoryItem-API wechseln und auf die riskEventTypes_v2-Eigenschaft in der signIns-API (Betaversion) 2020 umstellen. Zu diesem Zeitpunkt werden die aktuellen Eigenschaften „riskType“ und „riskEventTypes“ zurückgezogen. Weitere Informationen finden Sie unter [Änderungen an Risikoereigniseigenschaften und Identitätsschutz-APIs auf Microsoft Graph](https://developer.microsoft.com/graph/blogs/changes-to-risk-event-properties-and-identity-protection-apis-on-microsoft-graph/).

--- 

### <a name="deprecation-of-riskeventtypes-property-in-signins-v10-api-on-microsoft-graph"></a>Veraltung der riskEventTypes-Eigenschaft in der signIns v 1.0-API auf Microsoft Graph

**Typ:** Plan für Änderung  
**Dienstkategorie:** Berichterstellung  
**Produktfunktion:** Identitätssicherheit und -schutz

Aufzählungstypen wechseln zu Zeichenfolgentypen, wenn sie im September 2020 Risikoereigniseigenschaften in Microsoft Graph darstellen. Diese Änderung wirkt sich nicht nur auf die Vorschau-APIs aus, sondern auch auf die signIns-API in der Produktion.

Wir haben eine neue riskEventsTypes_v2 (string)-Eigenschaft für die signIns v1.0-API eingeführt. Wir werden die aktuelle riskEventTypes (enum)-Eigenschaft am 11.06.2022 in Übereinstimmung mit der Veraltungsrichtlinie für Microsoft Graph zurückziehen. Kunden müssen bis zum 11.06.2022 zur riskEventTypes_v2-Eigenschaft der v 1.0-signins-API wechseln. Weitere Informationen finden Sie unter [Veraltung der riskEventTypes-Eigenschaft in der signIns v 1.0-API auf Microsoft Graph](https://developer.microsoft.com/graph/blogs/deprecation-of-riskeventtypes-property-in-signins-v1-0-api-on-microsoft-graph//).

--- 

### <a name="upcoming-changes-to-mfa-email-notifications"></a>Bevorstehende Änderungen an MFA-E-Mail-Benachrichtigungen

**Typ:** Plan für Änderung  
**Dienstkategorie:** MFA  
**Produktfunktion** : Identitätssicherheit und -schutz
 

Wir nehmen die folgenden Änderungen an den E-Mail-Benachrichtigungen für die Cloud-MFA vor:

E-Mail-Benachrichtigungen werden von den folgenden Adressen gesendet: azure-noreply@microsoft.com und msonlineservicesteam@microsoftonline.com. Wir aktualisieren den Inhalt von E-Mails mit Betrugswarnungen, um die erforderlichen Schritte zum Entsperren von Verwendungen besser anzugeben.

---

### <a name="new-self-service-sign-up-for-users-in-federated-domains-who-cant-access-microsoft-teams-because-they-arent-synced-to-azure-active-directory"></a>Neue Self-Service-Registrierung für Benutzer in Verbunddomänen, die nicht auf Microsoft Teams zugreifen können, weil sie nicht mit Azure Active Directory synchronisiert sind.

**Typ:** Plan für Änderung  
**Dienstkategorie** : Authentifizierungen (Anmeldungen)  
**Produktfunktion:** Benutzerauthentifizierung
 

Derzeit können Benutzer, die sich in Azure AD-Verbunddomänen befinden, aber nicht mit dem Mandanten synchronisiert sind, nicht auf Teams zugreifen. Ab Ende Juni wird diese neue Funktion es ihnen ermöglichen, indem sie die vorhandene Registrierungsfunktion mit E-Mail-Überprüfung erweitert. Dies ermöglicht Benutzern, die sich bei einem verbundenen IDP anmelden können, aber noch kein Benutzerobjekt in Azure ID haben, über ein automatisch erstelltes Benutzerobjekt zu verfügen und für Teams authentifiziert zu werden. Ihr Benutzerobjekt wird als „Self-Service-Registrierung“ gekennzeichnet. Dies ist eine Erweiterung der vorhandenen Funktion zum Durchführen der per E-Mail überprüften Selbstregistrierung von Benutzern in verwalteten Domänen und kann mit demselben Flag gesteuert werden. Diese Änderung wird in den folgenden zwei Monaten vollständig ausgeführt. Achten Sie [hier](../enterprise-users/directory-self-service-signup.md) auf Dokumentationsupdates.
 
---

### <a name="upcoming-fix-the-oidc-discovery-document-for-the-azure-government-cloud-is-being-updated-to-reference-the-correct-graph-endpoints"></a>Anstehende Korrektur: Das OIDC-Ermittlungsdokument für die Azure Government-Cloud wird aktualisiert, sodass es auf die richtigen Graph-Endpunkte verweist.

**Typ:** Plan für Änderung  
**Dienstkategorie:** Unabhängige Clouds  
**Produktfunktion:** Benutzerauthentifizierung
 
Ab Juni gibt das OIDC-Ermittlungsdokument [Microsoft Identity Platform und das OpenID Connect-Protokoll](../develop/v2-protocols-oidc.md) auf dem [Azure Government-Cloud](../develop/authentication-national-cloud.md)-Endpunkt (login.microsoftonline.us) den richtigen [Nationale Cloudbereitstellungen](/graph/deployments)-Endpunkt (https://graph.microsoft.us oder https://dod-graph.microsoft.us) auf Basis des bereitgestellten Mandanten zurück.  Derzeit wird der falsche Graph-Endpunkt (graph.microsoft.com) „msgraph_host“-Feld angezeigt.  

Diese Fehlerbehebung wird schrittweise über ungefähr 2 Monate hinweg eingeführt.  

---

### <a name="azure-government-users-will-no-longer-be-able-to-sign-in-on-loginmicrosoftonlinecom"></a>Azure Government-Benutzer können sich nicht mehr bei „login.microsoftonline.com“ anmelden.

**Typ:** Geplante Änderung  
**Dienstkategorie:** Unabhängige Clouds  
**Produktfunktion:** Benutzerauthentifizierung
 
Am 1. Juni 2018 hat sich die offizielle Azure Active Directory (Azure AD)-Autorität für Azure Government von https://login-us.microsoftonline.com in https://login.microsoftonline.us geändert. Wenn Sie eine Anwendung in einem Azure Government-Mandanten besitzen, müssen Sie Ihre Anwendung aktualisieren, damit die Benutzer am US-Endpunkt angemeldet werden.

Ab dem 5. Mai wird in Azure AD mit der Durchsetzung der Endpunktänderung begonnen. Azure Government-Benutzer werden daran gehindert, sich mit dem öffentlichen Endpunkt (microsoftonline.com) bei in Azure Government-Mandanten gehosteten Apps anzumelden. Für betroffene Apps wird eine Fehlermeldung „AADSTS900439 – USGClientNotSupportedOnPublicEndpoint“ angezeigt. 

Diese Änderung wird schrittweise eingeführt, wobei die Erzwingung für alle Apps voraussichtlich im Juni 2020 erfolgt. Weitere Einzelheiten finden Sie im [Azure Government-Blogbeitrag](https://devblogs.microsoft.com/azuregov/azure-government-aad-authority-endpoint-update/).

---

### <a name="saml-single-logout-request-now-sends-nameid-in-the-correct-format"></a>Die SAML-Anforderung für einmaliges Abmelden sendet jetzt eine NameID im richtigen Format

**Typ:** Korrigiert  
**Dienstkategorie** : Authentifizierungen (Anmeldungen)  
**Produktfunktion:** Benutzerauthentifizierung
 
Wenn ein Benutzer auf die Abmeldung klickt (z. B. im MyApps-Portal), sendet Azure AD eine SAML-Nachricht für einmaliges Abmelden an jede App, die in der Benutzersitzung aktiv ist und für die eine Abmelde-URL konfiguriert ist. Diese Nachrichten enthalten eine NameID in einem persistenten Format.

Wenn das ursprüngliche SAML-Anmeldetoken ein anderes Format für die NameID verwendete (z. B. email/UPN), konnte die SAML-App die NameID in der Abmeldenachricht nicht mit einer vorhandenen Sitzung korrelieren (da sich die in beiden Nachrichten verwendeten NameIDs unterschieden), was dazu führte, dass die Abmeldenachricht von der SAML-App verworfen wurde und der Benutzer angemeldet bleiben musste. Diese Korrektur bewirkt, dass die Abmeldenachricht mit der für die Anwendung konfigurierten NameID konsistent ist.

---

### <a name="hybrid-identity-administrator-role-is-now-available-with-cloud-provisioning"></a>Rolle „Hybrididentitätsadministrator“ ist jetzt bei der Cloudbereitstellung verfügbar

**Typ:** Neues Feature  
**Dienstkategorie:** Azure AD-Cloudbereitstellung  
**Produktfunktion:** Identity Lifecycle Management
 
IT-Administratoren können jetzt die neue „Hybridadministrator“-Rolle als am wenigsten privilegierte Rolle zum Einrichten der Azure ADConnect-Cloudbereitstellung verwenden. Mit dieser neuen Rolle ist es nicht mehr erforderlich, die Rolle „Globaler Administrator“ zum Einrichten und Konfigurieren der Cloudbereitstellung zu verwenden. [Weitere Informationen](../roles/delegate-by-task.md#connect)
 
---

### <a name="new-federated-apps-available-in-azure-ad-application-gallery---may-2020"></a>Neue Verbund-Apps im Azure AD-Anwendungskatalog verfügbar – Mai 2020

**Typ:** Neues Feature  
**Dienstkategorie** : Unternehmens-Apps  
**Produktfunktion:** Integration von Drittanbieterprodukten
 
Im Mai 2020 haben wir die folgenden 36 neuen Anwendungen mit Verbundunterstützung in unseren App-Katalog aufgenommen:

[Moula](https://moula.com.au/pay/merchants), [Surveypal](https://www.surveypal.com/app), [Kbot365](https://www.konverso.ai/virtual-assistant-digital-workplace/), [TackleBox](http://www.tacklebox.app/), [Powell Teams](https://powell-software.com/en/powell-teams-en/), [Talentsoft Assistant](https://msteams.talent-soft.com/), [ASC Recording Insights](https://teams.asc-recording.app/product), [GO1](https://www.go1.com/), [B-Engaged](https://b-engaged.se/), [Competella Contact Center Workgroup](http://www.competella.com/), [Asite](http://www.asite.com/), [ImageSoft Identity](https://identity.imagesoftinc.com/), [My IBISWorld](https://identity.imagesoftinc.com/), [insuite](../saas-apps/insuite-tutorial.md), [Change Process Management](../saas-apps/change-process-management-tutorial.md), [Cyara CX Assurance Platform](../saas-apps/cyara-cx-assurance-platform-tutorial.md), [Smart Global Governance](../saas-apps/smart-global-governance-tutorial.md), [Prezi](../saas-apps/prezi-tutorial.md), [Mapbox](../saas-apps/mapbox-tutorial.md), [Datava Enterprise Service Platform](../saas-apps/datava-enterprise-service-platform-tutorial.md), [Whimsical](../saas-apps/whimsical-tutorial.md), [Trelica](../saas-apps/trelica-tutorial.md), [EasySSO for Confluence](../saas-apps/easysso-for-confluence-tutorial.md), [EasySSO for BitBucket](../saas-apps/easysso-for-bitbucket-tutorial.md), [EasySSO for Bamboo](../saas-apps/easysso-for-bamboo-tutorial.md), [Torii](../saas-apps/torii-tutorial.md), [Axiad Cloud](../saas-apps/axiad-cloud-tutorial.md), [Humanage](../saas-apps/humanage-tutorial.md), [ColorTokens ZTNA](../saas-apps/colortokens-ztna-tutorial.md), [CCH Tagetik](../saas-apps/cch-tagetik-tutorial.md), [ShareVault](../saas-apps/sharevault-tutorial.md), [Vyond](../saas-apps/vyond-tutorial.md), [TextExpander](../saas-apps/textexpander-tutorial.md), [Anyone Home CRM](../saas-apps/anyone-home-crm-tutorial.md), [askSpoke](../saas-apps/askspoke-tutorial.md), [ice Contact Center](../saas-apps/ice-contact-center-tutorial.md)

Die Dokumentation zu allen Anwendungen finden Sie auch hier: https://aka.ms/AppsTutorial.

Informationen zum Auflisten Ihrer Anwendung im Azure AD-App-Katalog finden Sie hier: https://aka.ms/AzureADAppRequest.

---

### <a name="report-only-mode-for-conditional-access-is-now-generally-available"></a>Reiner Berichtsmodus für den bedingten Zugriff jetzt allgemein verfügbar

**Typ:** Neues Feature  
**Dienstkategorie** : Bedingter Zugriff  
**Produktfunktion:** Identitätssicherheit und -schutz

Mit dem [reinen Berichtsmodus für den bedingten Azure AD-Zugriff](../conditional-access/concept-conditional-access-report-only.md) können Sie das Ergebnis einer Richtlinie auswerten, ohne die Zugriffssteuerungen zu erzwingen. Im reinen Berichtsmodus können Sie Richtlinien in Ihrer Organisation vor der Aktivierung testen und deren Auswirkungen verstehen, sodass die Bereitstellung sicherer und einfacher wird. In den letzten Monaten haben wir eine hohe Akzeptanz des reinen Berichtsmodus festgestellt. Richtlinien im reinen Berichtsmodus weisen bereits einen Umfang von mehr als 26 Millionen Benutzern auf. Mit der heutigen Ankündigung werden neue Richtlinien für den bedingten Azure AD-Zugriff standardmäßig im reinen Berichtsmodus erstellt. Dies bedeutet, dass Sie die Auswirkungen Ihrer Richtlinien vom Zeitpunkt der Erstellung an überwachen können. Benutzer der MS Graph-APIs können zudem [Richtlinien im reinen Berichtsmodus programmgesteuert verwalten](/graph/api/resources/conditionalaccesspolicy?view=graph-rest-beta). 

---

### <a name="self-service-sign-up-for-guest-users"></a>Self-Service-Registrierung für Gastbenutzer

**Typ:** Neues Feature  
**Dienstkategorie:** B2B  
**Produktfunktion:** B2B/B2C
 
Mit „Externe Identitäten“ in Azure AD können Sie Personen außerhalb Ihrer Organisation den Zugriff auf Ihre Apps und Ressourcen erlauben. Gleichzeitig können sie sich mit der von ihnen bevorzugten Identität anmelden. Wenn Sie eine Anwendung für externe Benutzer freigeben, wissen Sie möglicherweise nicht immer im Voraus, wer Zugriff auf die Anwendung benötigt. Mit [Self-Service-Registrierung](../external-identities/self-service-sign-up-overview.md) können Sie Gastbenutzern ermöglichen, sich zu registrieren und ein Gastkonto für Ihre LOB-Apps (Line of Business, Branche) zu erhalten. Der Registrierungsfluss kann erstellt und so angepasst werden, dass er Azure AD und soziale Identitäten unterstützt. Sie können auch während der Registrierung zusätzliche Informationen über den Benutzer sammeln.

---

 ### <a name="conditional-access-insights-and-reporting-workbook-is-generally-available"></a>Arbeitsmappe für Erkenntnisse und Berichterstellung zum bedingten Zugriff jetzt allgemein verfügbar

**Typ:** Neues Feature  
**Dienstkategorie** : Bedingter Zugriff  
**Produktfunktion:** Identitätssicherheit und -schutz

Die [Arbeitsmappe für Erkenntnisse und Berichterstellung](../conditional-access/howto-conditional-access-insights-reporting.md) bietet Administratoren eine Zusammenfassungsansicht des bedingten Azure AD-Zugriffs in ihrem Mandanten. Mit der Möglichkeit, eine einzelne Richtlinie auszuwählen, können Administratoren besser verstehen, was jede Richtlinie bewirkt, und Änderungen in Echtzeit überwachen. Die Arbeitsmappe streamt die in Azure Monitor gespeicherten Daten, die Sie [anhand dieser Anweisungen](../reports-monitoring/howto-integrate-activity-logs-with-log-analytics.md) in wenigen Minuten einrichten können. Damit das Dashboard leichter zu finden ist, haben wir es auf die neue Registerkarte „Erkenntnisse und Berichte“ im Menü „Bedingter Azure AD-Zugriff“ verschoben.

---

### <a name="policy-details-blade-for-conditional-access-is-in-public-preview"></a>Blatt „Richtliniendetails“ für den bedingten Zugriff als öffentliche Vorschau verfügbar

**Typ:** Neues Feature  
**Dienstkategorie** : Bedingter Zugriff  
**Produktfunktion:** Identitätssicherheit und -schutz

Auf dem neuen Blatt [Richtliniendetails](../conditional-access/troubleshoot-conditional-access.md) wird angezeigt, welche Zuweisungen, Bedingungen und Steuerelemente während der Auswertung der Richtlinie für bedingten Zugriff erfüllt wurden. Sie können auf das Blatt zugreifen, indem Sie in den Anmeldedetails auf der Registerkarte „Bedingter Zugriff“ oder der Registerkarte „Nur Bericht“ eine Zeile auswählen.

---

### <a name="new-query-capabilities-for-directory-objects-in-microsoft-graph-are-in-public-preview"></a>Neue Abfragefunktionen für Verzeichnisobjekte in Microsoft Graph sind in Public Preview

**Typ:** Neues Feature  
**Dienstkategorie:** MS Graph **Produktfunktion** : Entwickleroberfläche

Für Microsoft Graph-Verzeichnisobjekt-APIs werden neue Funktionen eingeführt, die Zähl-, Such-, Filter- und Sortiervorgänge ermöglichen. So erhalten Entwickler die Möglichkeit, unsere Verzeichnisobjekte ohne Problemumgehungen wie In-Memory-Filterung und -Sortierung schnell abzufragen. Weitere Informationen finden Sie in diesem [Blogbeitrag](https://aka.ms/CountFilterMSGraphAAD).

Wir sind zurzeit in der Public Preview und bitten um Feedback. Bitte senden Sie Ihre Kommentare mit dieser [kurzen Umfrage](https://aka.ms/MsGraphAADSurveyDocs).

---

### <a name="configure-saml-based-single-sign-on-using-microsoft-graph-api-beta"></a>Konfigurieren von SAML-basiertem einmaligem Anmelden unter Verwendung von Microsoft Graph-APIs (Beta)

**Typ:** Neues Feature  
**Dienstkategorie** : Unternehmens-Apps  
**Produktfunktion:** SSO
 
Unterstützung für das Erstellen und Konfigurieren einer Anwendung aus dem Azure AD-Katalog mithilfe von MS Graph-APIs in der Betaversion ist jetzt verfügbar. Wenn Sie SAML-basiertes einmaliges Anmelden für mehrere Instanzen einer Anwendung einrichten müssen, sparen Sie Zeit, indem Sie die Microsoft Graph-APIs verwenden, um die [Konfiguration von SAML-basiertem einmaligem Anmelden zu automatisieren](/graph/application-saml-sso-configure-api).
 
---

### <a name="new-provisioning-connectors-in-the-azure-ad-application-gallery---may-2020"></a>Neue Bereitstellungsconnectors im Azure AD-Anwendungskatalog – Mai 2020

**Typ:** Neues Feature  
**Dienstkategorie:** App-Bereitstellung  
**Produktfunktion:** Integration von Drittanbieterprodukten
 
Sie können ab sofort das Erstellen, Aktualisieren und Löschen von Benutzerkonten für diese neu integrierten Apps automatisieren:

* [8x8](../saas-apps/8x8-provisioning-tutorial.md)
* [Juno Journey](../saas-apps/juno-journey-provisioning-tutorial.md)
* [MediusFlow](../saas-apps/mediusflow-provisioning-tutorial.md)
* [New Relic (nach Organisation)](../saas-apps/new-relic-by-organization-provisioning-tutorial.md)
* [Oracle Cloud Infrastructure Console](../saas-apps/oracle-cloud-infratstructure-console-provisioning-tutorial.md)

Weitere Informationen dazu, wie Sie Ihre Organisation durch die automatisierte Bereitstellung von Benutzerkonten besser schützen können, finden Sie unter [Automatisieren der Bereitstellung und Bereitstellungsaufhebung von Benutzern für SaaS-Anwendungen mit Azure Active Directory](../app-provisioning/user-provisioning.md).

---

### <a name="saml-token-encryption-is-generally-available"></a>SAML-Tokenverschlüsselung ist allgemein verfügbar

**Typ:** Neues Feature  
**Dienstkategorie** : Unternehmens-Apps  
**Produktfunktion:** SSO
 
[Die SAML-Tokenverschlüsselung](../manage-apps/howto-saml-token-encryption.md) ermöglicht die Konfiguration von Anwendungen für den Empfang verschlüsselter SAML-Assertionen. Die Funktion ist nun in allen Clouds allgemein verfügbar.
 
---

### <a name="group-name-claims-in-application-tokens-is-generally-available"></a>Gruppennamenansprüche in Anwendungstoken sind allgemein verfügbar

**Typ:** Neues Feature  
**Dienstkategorie** : Unternehmens-Apps  
**Produktfunktion:** SSO
 
Die in einem Token ausgestellten Gruppenansprüche können jetzt auf die Gruppen beschränkt werden, die der Anwendung zugewiesen sind.  Dies ist besonders wichtig, wenn Benutzer einer großen Anzahl von Gruppen angehören und das Risiko besteht, dass die Beschränkungen der Tokengröße überschritten werden. Mit dieser neuen Funktion ist die Möglichkeit, [Token Gruppennamen hinzuzufügen](../hybrid/how-to-connect-fed-group-claims.md), allgemein verfügbar.
 
---

### <a name="workday-writeback-now-supports-setting-work-phone-number-attributes"></a>Workday Writeback unterstützt jetzt das Festlegen von Geschäftstelefonnummer-Attributen

**Typ:** Neues Feature  
**Dienstkategorie:** App-Bereitstellung  
**Produktfunktion:** Identity Lifecycle Management
 
Wir haben die Workday Writeback-Bereitstellungs-App erweitert, um jetzt das Rückschreiben von Geschäftstelefonnummer- und Mobilnummerattributen zu unterstützen. Zusätzlich zu E-Mail-Adresse und Benutzername können Sie nun die Workday Writeback-Bereitstellungs-App so konfigurieren, dass Telefonnummerwerte von Azure AD an Workday weitergeleitet werden. Weitere Informationen zum Konfigurieren des Rückschreibens von Telefonnummern finden Sie im Tutorial zur [Workday Writeback](../saas-apps/workday-writeback-tutorial.md)-App. 

---

### <a name="publisher-verification-preview"></a>Herausgeberüberprüfung (Vorschauversion)

**Typ:** Neues Feature  
**Dienstkategorie:** Sonstige  
**Produktfunktion:** Entwickleroberfläche
 
Die Herausgeberüberprüfung (Vorschauversion) unterstützt Administratoren und Endbenutzer dabei, die Authentizität von Anwendungsentwicklern zu verstehen, die in die Microsoft Identity Platform integriert sind. Weitere Informationen finden Sie unter [Herausgeberüberprüfung (Vorschau)](../develop/publisher-verification-overview.md).
 
---

### <a name="authorization-code-flow-for-single-page-apps"></a>Autorisierungscodeflow für Single-Page-Apps

**Typ:** Geändertes Feature **Dienstkategorie:** Authentifizierung **Produktfunktion:** Entwickleroberfläche

Aufgrund der [Cookieeinschränkungen von Drittanbietern wie Safari ITP](../develop/reference-third-party-cookies-spas.md) moderner Browser müssen SPAs anstelle des impliziten Flows zum Verwalten des einmaligen Anmeldens den Autorisierungscodeflow verwenden. MSAL.js v 2.x unterstützt jetzt den Autorisierungscodeflow. Dort sind entsprechende Updates für das Azure-Portal vorhanden, sodass Sie Ihre SPA so aktualisieren können, dass sie den Typ „spa“ hat und den Autorisierungscodeflow verwendet. Anleitungen finden Sie unter [Schnellstart: Anmelden von Benutzern und Abrufen eines Zugriffstokens in einer JavaScript-SPA mithilfe des Autorisierungscodeflows](../develop/quickstart-v2-javascript-auth-code.md).

---

### <a name="improved-filtering-for-devices-is-in-public-preview"></a>Verbesserte Filterung für Geräte in Public Preview

**Typ:** Geändertes Feature   
**Dienstkategorie:** Geräteverwaltung **Produktfunktion:** Lebenszyklusverwaltung für Geräte
 
Bisher konnten nur die Filter „Aktiviert“ und „Aktivitätsdatum“ verwendet werden. Nun können Sie die [Liste der Geräte nach weiteren Eigenschaften filtern](../devices/device-management-azure-portal.md#device-list-filtering-preview), einschließlich Betriebssystemtyp, Verknüpfungstyp, Konformität und mehr. Diese Ergänzungen sollten das Auffinden eines bestimmten Geräts vereinfachen.

---

### <a name="the-new-app-registrations-experience-for-azure-ad-b2c-is-now-generally-available"></a>Die neue Benutzeroberfläche für App-Registrierungen in Azure AD B2C ist jetzt allgemein verfügbar

**Typ:** Geändertes Feature   
**Dienstkategorie** : B2C – Kundenidentitätsverwaltung  
**Produktfunktion:** Identity Lifecycle Management
 
Die neue Benutzeroberfläche für App-Registrierungen in Azure AD B2C ist jetzt allgemein verfügbar. 

Bisher mussten Sie Ihre kundenorientierten B2C-Anwendungen mithilfe der Legacyoberfläche „Anwendungen“ getrennt von Ihren restlichen Apps verwalten. Dies bedeutete die Nutzung unterschiedlicher Oberflächen zur App-Erstellung an unterschiedlichen Stellen in Azure.

Mit der neuen Benutzeroberfläche können alle App-Registrierungen bei B2C und Azure AD von einem Ort aus konsistent verwaltet werden. Unabhängig davon, ob Sie eine kundenorientierte App verwalten müssen oder eine App, die Zugriff auf Microsoft Graph hat, um Azure AD B2C-Ressourcen programmgesteuert zu verwalten, müssen Sie nur eine Vorgehensweise erlernen.

Um zu der neuen Benutzeroberfläche zu gelangen, navigieren Sie im Azure AD B2C-Dienst und wählen das App-Registrierungsblatt aus. Der Zugriff auf die Benutzeroberfläche ist auch über den Azure Active Directory-Dienst möglich.

Die Azure AD B2C-Benutzeroberfläche für App-Registrierungen basiert auf der allgemeinen [Oberfläche für App-Registrierungen](https://developer.microsoft.com/identity/blogs/new-app-registrations-experience-is-now-generally-available/) bei einem Azure AD-Mandanten, ist jedoch an die Anforderungen von Azure AD B2C angepasst. Die ältere „Anwendungen“-Benutzeroberfläche wird in Zukunft als veraltet eingestuft.

Weitere Informationen finden Sie unter [Die neue App-Registrierungsbenutzeroberfläche für Azure AD B2C](../../active-directory-b2c/app-registrations-training-guide.md).

---
