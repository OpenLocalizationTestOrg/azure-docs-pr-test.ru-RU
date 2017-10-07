---
title: "Пример сценария PowerShell - aaaAzure развертывание кластера tooa приложения | Документы Microsoft"
description: "Сценарий Azure PowerShell пример: развертывание кластера Service Fabric tooa приложения."
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
ms.openlocfilehash: b417c9908c72f016e930c43ff2d13e0cc5451f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a>Развертывание кластера Service Fabric tooa приложения

Этот скрипт копирует образ хранилища кластера tooa пакет приложений, регистрирует тип приложения hello в кластере hello и создает экземпляр приложения с типом приложения hello.  Если все службы по умолчанию были определены в манифесте приложения hello объекта тип целевого приложения hello, эти службы создаются в данный момент. При необходимости настройте параметры hello. 

При необходимости установите модуля Service Fabric PowerShell hello с hello [пакет Service Fabric SDK](../service-fabric-get-started.md). 

## <a name="sample-script"></a>Пример скрипта

[!code-powershell[main](../../../powershell_scripts/service-fabric/deploy-application/deploy-application.ps1 "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a>Очистка развертывания 

После выполнения сценария образец hello hello скрипта в [удалить приложение](service-fabric-powershell-remove-application.md) может быть tooremove используется экземпляр приложения hello, отменена регистрация типа приложения hello и удалить пакет приложения hello из хранилища образов hello.

## <a name="script-explanation"></a>Описание скрипта

Этот скрипт использует hello, следующие команды. Каждая команда в таблице hello связывает toocommand документацию.

| Команда | Примечания |
|---|---|
| [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | Скопируйте образ хранилища кластера toohello пакета приложений.  |
|[Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)| Регистрирует тип и версия приложения на кластере hello. |
|[New-ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps)| Создает приложение на основе зарегистрированного типа приложения. |

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о модуля Service Fabric PowerShell hello см. в разделе [документация по Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).

Дополнительные примеры Powershell для Azure Service Fabric можно найти в hello [примеры Azure PowerShell](../service-fabric-powershell-samples.md).
