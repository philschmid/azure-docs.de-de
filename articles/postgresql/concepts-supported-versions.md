---
title: Unterstützte Versionen – Azure Database for PostgreSQL (Einzelserver)
description: Beschreibung der unterstützten Haupt- und Nebenversionen von Postgres in Azure Database for PostgreSQL (Einzelserver)
author: lfittl-msft
ms.author: lufittl
ms.service: postgresql
ms.topic: conceptual
ms.date: 07/22/2020
ms.custom: fasttrack-edit
ms.openlocfilehash: f03016c9a44968db49cd68bfec025c328861fc07
ms.sourcegitcommit: 7863fcea618b0342b7c91ae345aa099114205b03
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2020
ms.locfileid: "93286436"
---
# <a name="supported-postgresql-major-versions"></a>Unterstützte PostgreSQL-Hauptversionen

Weitere Informationen zur Unterstützung von Richtlinien finden Sie unter [Richtlinien zur Azure Database for PostgreSQL-Versionsverwaltung](concepts-version-policy.md).

Azure Database for PostgreSQL unterstützt derzeit die folgenden Hauptversionen:

## <a name="postgresql-version-11"></a>PostgreSQL Version 11
Das aktuelle Nebenrelease ist 11.6. Informationen zu Verbesserungen und Fehlerbehebungen in diesem Nebenrelease finden Sie in der [Dokumentation zu PostgreSQL](https://www.postgresql.org/docs/11/static/release-11-6.html).

## <a name="postgresql-version-10"></a>PostgreSQL Version 10
Das aktuelle Nebenrelease ist 10.11. Informationen zu Verbesserungen und Fehlerbehebungen in diesem Nebenrelease finden Sie in der [Dokumentation zu PostgreSQL](https://www.postgresql.org/docs/10/static/release-10-11.html).

## <a name="postgresql-version-96"></a>PostgreSQL Version 9.6
Das aktuelle Nebenrelease ist 9.6.16. Informationen zu Verbesserungen und Fehlerbehebungen in diesem Nebenrelease finden Sie in der [Dokumentation zu PostgreSQL](https://www.postgresql.org/docs/9.6/static/release-9-6-16.html).

## <a name="postgresql-version-95"></a>PostgreSQL Version 9.5
Das aktuelle Nebenrelease ist 9.5.20. Informationen zu Verbesserungen und Fehlerbehebungen in diesem Nebenrelease finden Sie in der [Dokumentation zu PostgreSQL](https://www.postgresql.org/docs/9.5/static/release-9-5-20.html).

## <a name="managing-upgrades"></a>Verwalten von Upgrades
Das PostgreSQL-Projekt gibt regelmäßig kleinere Releases aus, um gemeldete Fehler zu beheben. Azure Database for PostgreSQL führt automatische Patches der Server mit diesen Nebenreleases während der monatlichen Dienstbereitstellung durch. 

Automatische direkte Upgrades für Hauptversionen werden nicht unterstützt. Zum Upgrade auf die nächste Hauptversion haben Sie folgende Möglichkeiten: 
   * Weitere Informationen finden Sie unter [Upgrades von Hauptversionen mithilfe von Sicherungen und Wiederherstellungen](./how-to-upgrade-using-dump-and-restore.md)
   * Verwenden Sie [pg_dump and pg_restore](./howto-migrate-using-dump-and-restore.md), um einen Datenbankserver auf einen Server zu verschieben, der mit der neuen Engineversion erstellt wurde.
   * Alternativ können Sie mit dem [Azure Database Migration Service](..\dms\tutorial-azure-postgresql-to-azure-postgresql-online-portal.md) ein Upgrade von PostgreSQL 10 auf Version 11 durchführen.

### <a name="version-syntax"></a>Versionssyntax
Vor PostgreSQL-Version 10 wurde ein _Hauptversionsupgrade_ von der [PostgreSQL-Versionsrichtlinie](https://www.postgresql.org/support/versioning/) als eine Erhöhung der ersten _oder_ zweiten Versionsziffer betrachtet. Beispielsweise wurde ein Upgrade von 9.5 auf 9.6 als _Hauptversionsupgrade_ angesehen. Ab Version 10 gilt nur eine Änderung der ersten Ziffer als Hauptversionsupgrade. So ist der Schritt von 10.0 auf 10.1 beispielsweise ein _Nebenreleaseupgrade_. Version 10 auf 11 ist ein _Hauptversionsupgrade_.

## <a name="next-steps"></a>Nächste Schritte
Informationen zu unterstützten PostgreSQL-Erweiterungen finden Sie im [Dokument zu Erweiterungen](concepts-extensions.md).
