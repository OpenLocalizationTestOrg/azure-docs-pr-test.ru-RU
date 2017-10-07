---
title: "Пример сценария PowerShell - aaaAzure обновление приложения Service Fabric | Документы Microsoft"
description: "Пример сценария Azure PowerShell — создание приложения Service Fabric."
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
ms.date: 08/23/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 4f4777607bd6b35a76029e09ddb441006565d4cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-service-fabric-application"></a>Обновление приложения Service Fabric

Этот скрипт обновляет выполняющегося экземпляра tooversion Service Fabric приложения 1.3.0. Hello скрипт копирует hello новое приложение toohello кластера изображения хранилище пакетов, регистрирует тип приложения hello, запустит отслеживаемых обновление и постоянно проверяет состояние обновления hello до завершения обновления hello, либо откатывается назад. При необходимости настройте параметры hello. 

При необходимости установите модуля Service Fabric PowerShell hello с hello [пакет Service Fabric SDK](../service-fabric-get-started.md). 

## <a name="sample-script"></a>Пример скрипта

[!code-powershell[main](../../../powershell_scripts/service-fabric/upgrade-application/upgrade-application.ps1 "Upgrade an application")]

## <a name="script-explanation"></a>Описание скрипта

Этот скрипт использует hello, следующие команды. Каждая команда в таблице hello связывает toocommand документацию.

| Команда | Примечания |
|---|---|
| [Get-ServiceFabricApplication](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) | Возвращает все приложения hello в кластер Service Fabric hello или конкретного приложения.  |
| [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) | Возвращает состояние hello обновления приложения Service Fabric. |
| [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) | Возвращает типы приложения Service Fabric hello, зарегистрированные в кластере Service Fabric hello. |
| [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | Отменяет регистрацию типа приложения Service Fabric.  |
| [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | Копирует образ toohello пакета приложения Service Fabric хранилище.  |
| [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) | Регистрирует тип приложения Service Fabric. |
| [Start-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) | Обновление версии типа приложения toohello Service Fabric указанного приложения. |


## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о модуля Service Fabric PowerShell hello см. в разделе [документация по Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).

Дополнительные примеры Powershell для Azure Service Fabric можно найти в hello [примеры Azure PowerShell](../service-fabric-powershell-samples.md).
