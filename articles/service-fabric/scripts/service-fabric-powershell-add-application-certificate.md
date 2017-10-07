---
title: "Пример сценария PowerShell - aaaAzure добавить кластер tooa cert приложения | Документы Microsoft"
description: "Сценарий Azure PowerShell пример — Добавление кластера Service Fabric tooa сертификатов приложений."
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
ms.openlocfilehash: aba62598e2e4775012f89b5070bef5e61aec64f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-an-application-certificate-tooa-service-fabric-cluster"></a>Добавить к кластеру Service Fabric tooa сертификата приложения

Этот сценарий создает самозаверяющий сертификат в хранилище ключей заданного Azure hello и устанавливает его tooall узлы кластера Service Fabric hello. также сертификат Hello загружает tooa локальную папку. Имя сертификата, загружаются hello Hello hello совпадает с именем hello hello сертификата в хранилище ключей hello. При необходимости настройте параметры hello.

При необходимости установите Azure PowerShell с помощью инструкции hello, найденные в hello hello [руководство по Azure PowerShell](/powershell/azure/overview) , а затем запустите `Login-AzureRmAccount` toocreate соединения с Azure. 

## <a name="sample-script"></a>Пример скрипта

[!code-powershell[main](../../../powershell_scripts/service-fabric/add-application-certificate/add-new-application-certificate.ps1 "Add an application certificate tooa cluster")]

## <a name="script-explanation"></a>Описание скрипта

Этот скрипт использует hello, следующие команды: Каждая команда в таблице hello связывает toocommand документацию.

| Команда | Примечания |
|---|---|
| [Add-AzureRmServiceFabricApplicationCertificate](/powershell/module/azurerm.servicefabric/Add-AzureRmServiceFabricApplicationCertificate) | Добавьте новое приложение сертификат toohello набора масштабирования виртуальных машин, составляющих кластер hello.  |

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о hello модуля Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).

Дополнительные примеры Azure Service Fabric Azure Powershell можно найти в hello [примеры Azure PowerShell](../service-fabric-powershell-samples.md).
