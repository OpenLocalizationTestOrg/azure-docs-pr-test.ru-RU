---
title: "Образец скрипта PowerShell - удалить приложение из кластера aaaAzure | Документы Microsoft"
description: "Пример сценария Azure PowerShell — удаление приложения из кластера Service Fabric."
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 3fe2082c2fbeffbff1622f206021d4d907197d19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a>Удаление приложения из кластера Service Fabric

Этот скрипт удаляет запущенный экземпляр приложения Service Fabric, отменяет регистрацию тип и версия приложения из кластера hello и удаляет пакет приложения hello из хранилища образов кластера hello.  Удаление экземпляра приложения hello также удаляет все hello выполняющихся экземпляров службы, связанное с этим приложением. При необходимости настройте параметры hello. 

При необходимости установите модуля Service Fabric PowerShell hello с hello [пакет Service Fabric SDK](../service-fabric-get-started.md). 

## <a name="sample-script"></a>Пример скрипта

[!code-powershell[main](../../../powershell_scripts/service-fabric/remove-application/remove-application.ps1 "Remove an application from a cluster")]

## <a name="script-explanation"></a>Описание скрипта

Этот скрипт использует hello, следующие команды. Каждая команда в таблице hello связывает toocommand документацию.

| Команда | Примечания |
|---|---|
| [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) | Удаляет запущенный экземпляр приложения Service Fabric из кластера hello.  |
| [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | Отменяет регистрацию Service Fabric тип и версия приложения из кластера hello. |
| [Remove-ServiceFabricApplicationPackage](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) | Удаляет пакет Service Fabric приложения из хранилища образов hello.|

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о модуля Service Fabric PowerShell hello см. в разделе [документация по Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).

Дополнительные примеры Powershell для Azure Service Fabric можно найти в hello [примеры Azure PowerShell](../service-fabric-powershell-samples.md).
