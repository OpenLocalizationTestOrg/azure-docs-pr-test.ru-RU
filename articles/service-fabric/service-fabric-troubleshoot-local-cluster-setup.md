---
title: "aaaTroubleshoot вашей локальной настройки кластера Service Fabric | Документы Microsoft"
description: "В этой статье описываются рекомендации по устранению неполадок с кластером локальной разработки."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 97f4feaa-bba0-47af-8fdd-07f811fe2202
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: ce36f62a4bc69d2cd5b6c3df4abda6ca88fa84f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-your-local-development-cluster-setup"></a>Устранение неполадок в работе кластера локальной разработки
Если возникли проблемы при взаимодействии с локального кластера разработки Azure Service Fabric просмотрите hello из следующих способов для возможных решений.

## <a name="cluster-setup-failures"></a>Ошибки настройки кластера
### <a name="cannot-clean-up-service-fabric-logs"></a>Не удается очистить журналы Service Fabric
#### <a name="problem"></a>Проблема
При выполнении скрипта DevClusterSetup hello, появится сообщение об ошибке, следующим образом:

    Cannot clean up C:\SfDevCluster\Log fully as references are likely being held tooitems in it. Please remove those and run this script again.
    At line:1 char:1 + .\DevClusterSetup.ps1
    + ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException,DevClusterSetup.ps1


#### <a name="solution"></a>Решение
Закройте hello текущее окно PowerShell и откройте окно PowerShell с правами администратора. Теперь должен быть доступ toosuccessfully, запустите скрипт hello.

## <a name="cluster-connection-failures"></a>Ошибки подключения к кластеру
### <a name="service-fabric-powershell-cmdlets-are-not-recognized-in-azure-powershell"></a>Командлеты Service Fabric PowerShell не распознаются в Azure PowerShell
#### <a name="problem"></a>Проблема
Если вы выполните toorun hello командлеты PowerShell для службы структуры, таких как `Connect-ServiceFabricCluster` в окне Azure PowerShell, происходит сбой, о том, командлет hello не распознан. Hello причина в том, что Azure PowerShell используется hello 32-разрядной версии оболочки Windows PowerShell (даже на 64-разрядной версии ОС), в то время как hello Service Fabric командлеты работают только в 64-разрядных сред.

#### <a name="solution"></a>Решение
Всегда запускайте командлеты Service Fabric непосредственно из Windows PowerShell.

> [!NOTE]
> Hello последнюю версию Azure PowerShell не создает специальные ярлык, поэтому это больше не возникает.
> 
> 

### <a name="type-initialization-exception"></a>Исключение типа инициализации
#### <a name="problem"></a>Проблема
При подключении toohello кластера в PowerShell, вы увидите hello ошибка TypeInitializationException System.Fabric.Common.AppTrace.

#### <a name="solution"></a>Решение
При установке была неправильно настроена переменная пути. Выйдите из Windows и снова выполните вход. Путь обновится.

### <a name="cluster-connection-fails-with-object-is-closed"></a>Сбой подключения к кластеру с сообщением об ошибке "Объект закрыт"
#### <a name="problem"></a>Проблема
Вызов tooConnect-ServiceFabricCluster завершается с ошибкой следующим образом:

    Connect-ServiceFabricCluster : hello object is closed.
    At line:1 char:1
    + Connect-ServiceFabricCluster
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : InvalidOperation: (:) [Connect-ServiceFabricCluster], FabricObjectClosedException
    + FullyQualifiedErrorId : CreateClusterConnectionErrorId,Microsoft.ServiceFabric.Powershell.ConnectCluster

#### <a name="solution"></a>Решение
Закройте hello текущее окно PowerShell и откройте окно PowerShell с правами администратора. Теперь можно подключиться toosuccessfully.

### <a name="fabric-connection-denied-exception"></a>Исключение Fabric Connection Denied
#### <a name="problem"></a>Проблема
При отладке в Visual Studio отображается ошибка FabricConnectionDeniedException.

#### <a name="solution"></a>Решение
Эта ошибка обычно возникает при попытке toostart хост-процесса службы вручную, а не указывайте toostart среда выполнения Service Fabric hello его автоматически.

Убедитесь, что в решении нет проектов служб, настроенных в качестве запускаемых проектов. В качестве запускаемых проектов можно настраивать только проекты приложений Service Fabric.

> [!TIP]
> Если после завершения программы установки, локального кластера начинает toobehave аварийно, его можно сбросить с помощью приложения для области hello локального кластера диспетчера уведомлений. Это удаляет hello существующего кластера и настройте новый. Учтите, что все развернутые приложения и связанные данные будут удалены.
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
* [Обзор и диагностика кластера с помощью системных отчетов о работоспособности](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [Визуализация кластера с помощью обозревателя Service Fabric](service-fabric-visualizing-your-cluster.md)

