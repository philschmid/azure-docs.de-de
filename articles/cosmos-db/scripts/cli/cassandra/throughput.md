---
title: 'Azure CLI-Skripts für Durchsatzvorgänge (RU/s): Ressourcen der Cassandra-API für Azure Cosmos DB'
description: 'Azure CLI-Skripts für Durchsatzvorgänge (RU/s): Ressourcen der Cassandra-API für Azure Cosmos DB'
author: markjbrown
ms.author: mjbrown
ms.service: cosmos-db
ms.subservice: cosmosdb-cassandra
ms.topic: sample
ms.date: 10/07/2020
ms.openlocfilehash: 11b9337c964caef63fd6c949f9251556950e7df7
ms.sourcegitcommit: 3bdeb546890a740384a8ef383cf915e84bd7e91e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "93098289"
---
# <a name="throughput-rus-operations-with-azure-cli-for-a-keyspace-or-table-for-azure-cosmos-db---cassandra-api"></a>Durchsatzvorgänge (RU/s) mit der Azure CLI für einen Keyspace oder eine Tabelle für Azure Cosmos DB: Cassandra-API
[!INCLUDE[appliesto-cassandra-api](../../../includes/appliesto-cassandra-api.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../../../includes/cloud-shell-try-it.md)]

Wenn Sie die Azure CLI lokal installieren und verwenden möchten, ist es für dieses Thema erforderlich, mindestens Version 2.12.1 auszuführen. Führen Sie `az --version` aus, um die Version zu ermitteln. Informationen zum Durchführen einer Installation oder eines Upgrades finden Sei bei Bedarf unter [Installieren der Azure CLI](/cli/azure/install-azure-cli).

## <a name="sample-script"></a>Beispielskript

Dieses Skript erstellt einen Cassandra-Keyspace mit freigegebenem Durchsatz sowie eine Cassandra-Tabelle mit dediziertem Durchsatz und aktualisiert dann den Durchsatz für den Keyspace und die Tabelle. Anschließend führt das Skript die Migration vom standardmäßigen zum automatisch skalierten Durchsatz durch, und nach Abschluss der Migration wird dann der Wert des automatisch skalierten Durchsatzes gelesen.

[!code-azurecli-interactive[main](../../../../../cli_scripts/cosmosdb/cassandra/throughput.sh "Throughput operations for Cassandra keyspace and table.")]

## <a name="clean-up-deployment"></a>Bereinigen der Bereitstellung

Nach Ausführung des Skriptbeispiels können mit dem folgenden Befehl die Ressourcengruppe und alle damit verbundenen Ressourcen entfernt werden.

```azurecli-interactive
az group delete --name $resourceGroupName
```

## <a name="script-explanation"></a>Erläuterung des Skripts

Das Skript verwendet die folgenden Befehle. Jeder Befehl in der Tabelle ist mit der zugehörigen Dokumentation verknüpft.

| Get-Help | Notizen |
|---|---|
| [az group create](/cli/azure/group#az-group-create) | Erstellt eine Ressourcengruppe, in der alle Ressourcen gespeichert sind. |
| [az cosmosdb create](/cli/azure/cosmosdb#az-cosmosdb-create) | Erstellt ein Konto für Azure Cosmos DB. |
| [az cosmosdb cassandra keyspace create](/cli/azure/cosmosdb/cassandra/keyspace#az-cosmosdb-cassandra-keyspace-create) | Erstellt einen Azure Cosmos-Cassandra-Keyspace. |
| [az cosmosdb cassandra table create](/cli/azure/cosmosdb/cassandra/table#az-cosmosdb-cassandra-table-create) | Erstellt eine Azure Cosmos-Cassandra-Tabelle. |
| [az cosmosdb cassandra keyspace throughput update](/cli/azure/cosmosdb/cassandra/keyspace/throughput#az-cosmosdb-cassandra-keyspace-throughput-update) | Aktualisiert die Anforderungseinheiten pro Sekunde (RU/s) für einen Azure Cosmos-Cassandra-Keyspace. |
| [az cosmosdb cassandra table throughput update](/cli/azure/cosmosdb/cassandra/table/throughput#az-cosmosdb-cassandra-table-throughput-update) | Aktualisiert die Anforderungseinheiten pro Sekunde (RU/s) für eine Azure Cosmos-Cassandra-Tabelle. |
| [az cosmosdb cassandra keyspace throughput migrate](/cli/azure/cosmosdb/cassandra/keyspace/throughput#az_cosmosdb_cassandra_keyspace_throughput_migrate) | Migriert den Durchsatz für einen Azure Cosmos-Cassandra-Keyspace. |
| [az cosmosdb cassandra table throughput migrate](/cli/azure/cosmosdb/cassandra/table/throughput#az_cosmosdb_cassandra_table_throughput_migrate) | Migriert den Durchsatz für eine Azure Cosmos-Cassandra-Tabelle. |
| [az group delete](/cli/azure/resource#az-resource-delete) | Löscht eine Ressourcengruppe einschließlich aller geschachtelten Ressourcen. |

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zur Azure Cosmos DB-CLI finden Sie in der [Dokumentation zur Azure Cosmos DB-CLI](/cli/azure/cosmosdb).

Alle CLI-Skriptbeispiele für Azure Cosmos DB finden Sie im [GitHub-Repository zur Azure Cosmos DB-CLI](https://github.com/Azure-Samples/azure-cli-samples/tree/master/cosmosdb).
