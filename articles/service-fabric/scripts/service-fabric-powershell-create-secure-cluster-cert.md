---
title: "Пример сценария PowerShell - aaaAzure создание кластера Service Fabric | Документы Microsoft"
description: "Пример сценария Azure PowerShell — создание кластера Service Fabric."
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0f9c8bc5-3789-4eb3-8deb-ae6e2200795a
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 12fdc201bd51688cb850cd456b1e00442b79c22d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster"></a>Создание кластера Service Fabric

В этом примере сценария создается кластер Service Fabric из пяти узлов, защищенный с помощью сертификата X.509.  Hello команда создает самозаверяющий сертификат и передает его tooa нового ключа хранилища. сертификат Hello также является скопированный tooa локальный каталог.  Набор hello *-OS* параметр toochoose hello версии Windows или Linux, работающей на узлах кластера hello.  При необходимости настройте параметры hello.

При необходимости установите Azure PowerShell с помощью инструкции hello, найденные в hello hello [руководство по Azure PowerShell](/powershell/azure/overview) , а затем запустите `Login-AzureRmAccount` toocreate соединения с Azure. 

## <a name="sample-script"></a>Пример скрипта

[!code-powershell[main](../../../powershell_scripts/service-fabric/create-secure-cluster/create-secure-cluster.ps1 "Create a Service Fabric cluster")]

## <a name="clean-up-deployment"></a>Очистка развертывания 

После выполнения сценария образец hello hello, следующая команда может быть группы ресурсов используется tooremove hello, кластера и все связанные ресурсы.

```powershell
$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="script-explanation"></a>Описание скрипта

Этот скрипт использует hello, следующие команды. Каждая команда в таблице hello связывает toocommand документацию.

| Команда | Примечания |
|---|---|
| [New-AzureRmServiceFabricCluster](/powershell/module/azurerm.servicefabric/New-AzureRmServiceFabricCluster) | Создает кластер Service Fabric. |

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о hello модуля Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).

Дополнительные примеры Azure Service Fabric Azure Powershell можно найти в hello [примеры Azure PowerShell](../service-fabric-powershell-samples.md).
