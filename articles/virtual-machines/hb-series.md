---
title: HB-Serie
description: Spezifikationen für die VMs der HB-Serie
author: ju-shim
ms.service: virtual-machines
ms.subservice: sizes
ms.topic: conceptual
ms.date: 10/09/2020
ms.author: amverma
ms.reviewer: jushiman
ms.openlocfilehash: f3fbc1ad3f9e7f3f3c9d2667ae9c3f566325aa51
ms.sourcegitcommit: 50802bffd56155f3b01bfb4ed009b70045131750
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/09/2020
ms.locfileid: "91931698"
---
# <a name="hb-series"></a>HB-Serie

VMs der HB-Serie sind für Anwendungen mit hohen Anforderungen an die Speicherbandbreite optimiert, z.B. Strömungssimulationen, explizite Finite-Element-Analysen oder Wettermodelle. HB-VMs bieten 60 AMD-Prozessorkerne des Modells EPYC 7551, 4 GB RAM pro CPU-Kern und kein gleichzeitiges Multithreading. Ein HB-VM unterstützt eine Speicherbandbreite von bis zu 260 Gbit/s.

VMs der HB-Serie unterstützen Mellanox EDR InfiniBand mit 100 Gbit/s. Diese VMs sind für eine optimierte und konsistente RDMA-Leistung in einer FAT-Struktur ohne Blocks verbunden. Diese VMs unterstützen adaptives Routing und DCT (Dynamic Connected Transport, zusätzlich zum standardmäßigen RC- und UD-Transport). Diese Features verbessern die Anwendungsleistung, Skalierbarkeit und Konsistenz, und ihre Verwendung wird dringend empfohlen.

[ACU](acu.md): 199-216<br>
[Storage Premium](premium-storage-performance.md): Unterstützt<br>
[Storage Premium-Zwischenspeicherung:](premium-storage-performance.md) Unterstützt<br>
[Livemigration](maintenance-and-updates.md): Nicht unterstützt<br>
[Updates mit Speicherbeibehaltung](maintenance-and-updates.md): Nicht unterstützt<br>
[Unterstützung von VM-Generationen](generation-2.md): Generation 1 und 2<br>
<br>

| Size | vCPU | Prozessor | Arbeitsspeicher (GiB) | Speicherbandbreite GB/s | Basis-CPU-Frequenz (GHz) | Frequenz für alle Kerne (GHz, Spitze) | Frequenz für Einzelkern (GHz, Spitze) | RDMA-Leistung (Gbit/s) | MPI-Unterstützung | Temporärer Speicher (GiB) | Max. Anzahl Datenträger | Max. virtuelle Ethernet-Netzwerkkarten (vNICs) |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_HB60rs | 60 | AMD EPYC 7551 | 240 | 263 | 2.0 | 2.55 | 2.55 | 100 | All | 700 | 4 | 8 |

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../includes/virtual-machines-common-sizes-table-defs.md)]

## <a name="other-sizes"></a>Andere Größen

- [Allgemeiner Zweck](sizes-general.md)
- [Arbeitsspeicheroptimiert](sizes-memory.md)
- [Speicheroptimiert](sizes-storage.md)
- [GPU-optimiert](sizes-gpu.md)
- [High Performance Computing](sizes-hpc.md)
- [Vorherige Generationen](sizes-previous-gen.md)

## <a name="next-steps"></a>Nächste Schritte
- Erfahren Sie mehr über das [Konfigurieren Ihrer VMs](./workloads/hpc/configure.md), das [Aktivieren von InfiniBand](./workloads/hpc/enable-infiniband.md), das [Einrichten von MPI](./workloads/hpc/setup-mpi.md) und das Optimieren von HPC-Anwendungen für Azure mit [HPC-Workloads](./workloads/hpc/overview.md).
- Informieren Sie sich in den [Tech Community-Blogs zu Azure Compute](https://techcommunity.microsoft.com/t5/azure-compute/bg-p/AzureCompute) über die neuesten Ankündigungen, und machen Sie sich mit einigen Beispielen und Ergebnissen zu HPC vertraut.
- Eine allgemeinere Übersicht über die Architektur für die Ausführung von HPC-Workloads finden Sie unter [High Performance Computing (HPC) in Azure](/azure/architecture/topics/high-performance-computing/).
- Weitere Informationen dazu, wie Sie mit [Azure-Computeeinheiten (ACU)](acu.md) die Computeleistung von Azure-SKUs vergleichen können.
