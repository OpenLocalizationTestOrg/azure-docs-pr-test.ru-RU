---
title: "aaaAzure канал операционного структуры службы | Документы Microsoft"
description: "Полный список журналов, созданных в кластерах оперативной канала из Azure Service Fabric hello."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: dekapur
ms.openlocfilehash: 358782420ed62b202d6a89fe0f200b5ef0384c9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="operational-channel"></a>Операционный канал 

Операционный канал Hello состоит из журналов из высокоуровневые действия, выполняемые Service Fabric на узлах и кластера. При включении «Диагностика» для кластера, hello агента диагностики Azure развертывается в кластере и по умолчанию настроен tooread в журналы из hello операционный канал. Дополнительные сведения о настройке hello [агент Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md) конфигурации диагностики hello toomodify toopick вашего кластера дополнительные журналы или счетчики производительности. 

## <a name="operational-channel-logs"></a>Журналы операционного канала 

Ниже приведен полный список журналов, предоставляемых Service Fabric в операционный канал hello. 

| EventId | Имя | Источник (задача) | Уровень |
| --- | --- | --- | --- |
| 25620 | NodeOpening | FabricNode | Информация |
| 25621 | NodeOpenedSuccess | FabricNode | Информация |
| 25622 | NodeOpenedFailed | FabricNode | Информация |
| 25623 | NodeClosing | FabricNode | Информация |
| 25624 | NodeClosed | FabricNode | Информация |
| 25625 | NodeAborting | FabricNode | Информация |
| 25626 | NodeAborted | FabricNode | Информация |
| 29627 | ClusterUpgradeStart | CM | Информация |
| 29628 | ClusterUpgradeComplete | CM | Информация |
| 29629 | ClusterUpgradeRollback | CM | Информация |
| 29630 | ClusterUpgradeRollbackComplete | CM | Информация |
| 29631 | ClusterUpgradeDomainComplete | CM | Информация |
| 23074 | ContainerActivated | Hosting | Информация |
| 23075 | ContainerDeactivated | Hosting | Информация |
| 29620 | ApplicationCreated | CM | Информация |
| 29621 | ApplicationUpgradeStart | CM | Информация |
| 29622 | ApplicationUpgradeComplete | CM | Информация |
| 29623 | ApplicationUpgradeRollback | CM | Информация |
| 29624 | ApplicationUpgradeRollbackComplete | CM | Информация |
| 29625 | ApplicationDeleted | CM | Информация |
| 29626 | ApplicationUpgradeDomainComplete | CM | Информация |
| 18566 | ServiceCreated | FM | Информация |
| 18567 | ServiceDeleted | FM | Информация |

## <a name="next-steps"></a>Дальнейшие действия

* Дополнительные сведения об общем [созданием события на уровне платформы hello](service-fabric-diagnostics-event-generation-infra.md) в Service Fabric
* Изменение вашей [диагностики Azure](service-fabric-diagnostics-event-aggregation-wad.md) более журналы конфигурации toocollect
* [Настройка Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) toosee вашей операционный канал журналы
