---
title: "жизненный цикл aaaApplication в Service Fabric | Документы Microsoft"
description: "Описывает разработку, развертывание, тестирование, обновление, обслуживание и удаление приложений Service Fabric."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 08837cca-5aa7-40da-b087-2b657224a097
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/14/2017
ms.author: ryanwi
ms.openlocfilehash: 36cd6081010e83cb8226c8f85d1e912ac9eebd00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-lifecycle"></a>Жизненный цикл приложения Service Fabric
Как с другими платформами на Azure Service Fabric приложение обычно проходит через следующие этапы hello: проектирования, разработки, тестирования, развертывания, обновления, обслуживания и удаления. Service Fabric обеспечивает поддержку hello всего жизненного цикла облачных приложений — от разработки до развертывания, повседневного управления и обслуживания tooeventual вывода из эксплуатации. модель службы Hello включает несколько различных ролей tooparticipate независимо друг от друга в жизненном цикле приложения hello. Эта статья содержит обзор hello API-интерфейсов и как они используются в разных ролей hello hello этапы жизненного цикла приложения hello Service Fabric.

Hello следующее видео Microsoft Virtual Academy описывает способ toomanage жизненного цикла приложения:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=My3Ka56yC_6106218965">
<img src="./media/service-fabric-application-lifecycle/AppLifecycleVid.png" WIDTH="360" HEIGHT="244">
</a></center>

## <a name="service-model-roles"></a>Роли моделей служб
роли модели службы Hello являются:

* **Разработчик службы**: Разработка модульных и универсальных служб, которые могут быть повторно и использовать в нескольких приложениях hello же или разных типов. Например, служба очередей может использоваться для создания приложения для обработки обращений (служба поддержки) или приложения для электронной коммерции (корзины).
* **Разработчик приложения**: создание приложений за счет интеграции набора служб toosatisfy определенными требованиями или сценариев. Например, веб-сайтом электронной коммерции может интегрировать «JSON без сохранения состояния интерфейсный служба», «Служба аукциона с отслеживанием состояния» и «Служба с отслеживанием состояния очереди» toobuild решения для аукционов.
* **Администратор приложения**: принимает решения о конфигурации приложения hello (заполнение параметров шаблона настройки hello), развертывании (сопоставление tooavailable ресурсов) и качество обслуживания. Например администратор приложения решает hello языковой стандарт (английский для hello США или японский для Японии) приложения hello. Другое развернутое приложение может иметь другие настройки.
* **Оператор**: развертывает приложения на основе конфигурации приложения hello и требования, заданного администратором приложения hello. Например оператор подготавливает и развертывает приложение hello и гарантирует, что он работает в Azure. Операторы отслеживать сведения о работоспособности и производительности приложения и поддерживать hello физической инфраструктуры, при необходимости.

## <a name="develop"></a>Разработка
1. Объект *службы разработчика* создает различные типы служб с помощью hello [службы Reliable Actor](service-fabric-reliable-actors-introduction.md) или [надежного обмена](service-fabric-reliable-services-introduction.md) модель программирования.
2. Объект *службы разработчика* декларативно описывает типы служб разработанных hello в файл манифеста службы, состоящий из одного или нескольких пакетов кода, конфигурации и данных.
3. *Разработчик приложений* затем создает приложения, используя для этого службы различных типов.
4. *Разработчик приложения* декларативно описывает тип приложения hello в манифесте приложения путем ссылки на манифесты составляющих служб hello hello и соответствующим образом переопределения и параметризации различные параметры конфигурации и развертывания составляющих служб hello.

См. статьи [Приступая к работе с Reliable Actors](service-fabric-reliable-actors-get-started.md) и [Начало работы со службами Reliable Services в Service Fabric](service-fabric-reliable-services-quick-start.md), чтобы ознакомиться с примерами.

## <a name="deploy"></a>Развернуть
1. *Администратор приложения* адаптирует hello toobe развертывания конкретного приложения tooa кластера Service Fabric для приложения тип tooa, указав соответствующие параметры hello hello **ApplicationType**элемент в манифесте приложения hello.
2. *Оператор* передач hello хранилище образов кластера toohello пакета приложения с помощью hello [ **CopyApplicationPackage** метод](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_CopyApplicationPackage_System_String_System_String_System_String_) или hello [  **Копировать ServiceFabricApplicationPackage** командлет](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps). пакет приложения Hello содержит манифест приложения hello и hello коллекцию пакетов служб. Service Fabric развертывает приложения из пакета приложения hello, хранящихся в хранилище hello изображения, которое может быть хранилище BLOB-объектов Azure или hello Системная служба Service Fabric.
3. Hello *оператор* затем настраивает тип приложения hello в целевой кластер hello из пакета отправленное приложение hello, с помощью hello [ **ProvisionApplicationAsync** метод](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_ProvisionApplicationAsync_System_String_System_TimeSpan_System_Threading_CancellationToken_), hello [ **регистра ServiceFabricApplicationType** командлет](https://docs.microsoft.com/powershell/servicefabric/vlatest/register-servicefabricapplicationtype), или hello [ **Подготовка приложения** операции REST](https://docs.microsoft.com/rest/api/servicefabric/provision-an-application).
4. После подготовки приложения hello *оператор* запускает приложение hello с hello параметрами, предоставленными hello *администратор приложения* с помощью hello [  **CreateApplicationAsync** метод](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_CreateApplicationAsync_System_Fabric_Description_ApplicationDescription_System_TimeSpan_System_Threading_CancellationToken_), hello [ **New ServiceFabricApplication** командлет](https://docs.microsoft.com/powershell/servicefabric/vlatest/new-servicefabricapplication), или hello [ **создать Приложение** операции REST](https://docs.microsoft.com/rest/api/servicefabric/create-an-application).
5. После развертывания приложения hello *оператор* hello использует [ **CreateServiceAsync** метод](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient#System_Fabric_FabricClient_ServiceManagementClient_CreateServiceAsync_System_Fabric_Description_ServiceDescription_System_TimeSpan_System_Threading_CancellationToken_), hello [  **Новый ServiceFabricService** командлет](https://docs.microsoft.com/powershell/servicefabric/vlatest/new-servicefabricservice), или hello [ **Создание службы** операции REST](https://docs.microsoft.com/rest/api/servicefabric/create-a-service) на основе toocreate новых экземпляров службы для приложения hello Возможные типы служб.
6. Теперь приложение Hello работает в кластер Service Fabric hello.

См. статью [Развертывание и удаление приложений с помощью PowerShell](service-fabric-deploy-remove-applications.md), чтобы ознакомиться с примерами.

## <a name="test"></a>Тест
1. После развертывания toohello локальному кластеру разработки или тестирования кластера, *службы разработчика* запусков hello сценария тестирования встроенных отработки отказа с помощью hello [ **FailoverTestScenarioParameters** ](https://docs.microsoft.com/dotnet/api/system.fabric.testability.scenario.failovertestscenarioparameters#System_Fabric_Testability_Scenario_FailoverTestScenarioParameters) и [ **FailoverTestScenario** ](https://docs.microsoft.com/dotnet/api/system.fabric.testability.scenario.failovertestscenario#System_Fabric_Testability_Scenario_FailoverTestScenario) классы или hello [ **Invoke ServiceFabricFailoverTestScenario** командлета ](/powershell/module/servicefabric/invoke-servicefabricfailovertestscenario?view=azureservicefabricps). сценарии тестовой отработки отказа Hello завершит важные tooensure переходы и переход на другой ресурс, что это доступность и работоспособность указанной службы.
2. Hello *службы разработчика* , а затем выполняется hello встроенных хаоса сценарий теста, с помощью hello [ **ChaosTestScenarioParameters** ](https://docs.microsoft.com/dotnet/api/system.fabric.testability.scenario.chaostestscenarioparameters#System_Fabric_Testability_Scenario_ChaosTestScenarioParameters) и [  **ChaosTestScenario** ](https://docs.microsoft.com/dotnet/api/system.fabric.testability.scenario.chaostestscenario#System_Fabric_Testability_Scenario_ChaosTestScenario) классы или hello [ **Invoke ServiceFabricChaosTestScenario** командлет](/powershell/module/servicefabric/invoke-servicefabricchaostestscenario?view=azureservicefabricps). сценарии теста хаоса Hello случайным образом вызывает несколько узла пакет кода и ошибки реплики в кластер hello.
3. Hello *службы разработчика* [проверяет связи service to service](service-fabric-testability-scenarios-service-communication.md) путем создания сценариев тестирования, которые перемещают первичные реплики вокруг hello кластера.

В разделе [toohello введение ошибки Analysis Service](service-fabric-testability-overview.md) для получения дополнительной информации.

## <a name="upgrade"></a>Обновление
1. Объект *службы разработчика* обновляет составные службы приложения hello экземпляр hello устраняет ошибки и предоставляет новую версию манифеста службы hello.
2. *Разработчик приложения* переопределяет и параметризует hello параметров конфигурации и развертывания служб согласованное hello и предоставляет новую версию манифеста приложения hello. Разработчик приложения Hello затем включает новые версии манифестов служб hello hello в приложение hello и предоставляет новую версию типа приложения hello в пакете обновленные приложения.
3. *Администратор приложения* включает hello новую версию типа приложения hello в целевое приложение hello, обновляя соответствующие параметры hello.
4. *Оператор* передач hello хранилище обновленное приложение пакета toohello кластера образов с помощью hello [ **CopyApplicationPackage** метод](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_CopyApplicationPackage_System_String_System_String_System_String_) или hello [ **Копирования ServiceFabricApplicationPackage** командлет](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps). пакет приложения Hello содержит манифест приложения hello и hello коллекцию пакетов служб.
5. *Оператор* подготавливает hello новую версию приложения hello в hello целевой кластер с помощью hello [ **ProvisionApplicationAsync** метод](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_ProvisionApplicationAsync_System_String_System_TimeSpan_System_Threading_CancellationToken_), hello [ **Регистра ServiceFabricApplicationType** командлет](https://docs.microsoft.com/powershell/servicefabric/vlatest/register-servicefabricapplicationtype), или hello [ **Подготовка приложения** операции REST](https://docs.microsoft.com/rest/api/servicefabric/provision-an-application).
6. *Оператор* обновления hello целевой toohello новой версии приложения с помощью hello [ **UpgradeApplicationAsync** метод](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_UpgradeApplicationAsync_System_Fabric_Description_ApplicationUpgradeDescription_System_TimeSpan_System_Threading_CancellationToken_), hello [  **Start-ServiceFabricApplicationUpgrade** командлет](https://docs.microsoft.com/powershell/servicefabric/vlatest/start-servicefabricapplicationupgrade), или hello [ **обновление приложения** операции REST](https://docs.microsoft.com/rest/api/servicefabric/upgrade-an-application).
7. *Оператор* проверок hello ход выполнения обновления с помощью hello [ **GetApplicationUpgradeProgressAsync** метод](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_GetApplicationUpgradeProgressAsync_System_Uri_System_TimeSpan_System_Threading_CancellationToken_), hello [  **Get-ServiceFabricApplicationUpgrade** командлет](https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricapplicationupgrade), или hello [ **получить ход выполнения обновления приложения** операции REST](https://docs.microsoft.com/rest/api/servicefabric/get-the-progress-of-an-application-upgrade1).
8. При необходимости hello *оператор* изменяет и повторно применяет параметры hello hello обновление текущего приложения с помощью hello [ **UpdateApplicationUpgradeAsync** метод](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_UpdateApplicationUpgradeAsync_System_Fabric_Description_ApplicationUpgradeUpdateDescription_System_TimeSpan_System_Threading_CancellationToken_), Hello [ **обновление ServiceFabricApplicationUpgrade** командлет](https://docs.microsoft.com/powershell/servicefabric/vlatest/update-servicefabricapplicationupgrade), или hello [ **обновления обновление приложения** операции REST](https://docs.microsoft.com/rest/api/servicefabric/update-an-application-upgrade).
9. При необходимости hello *оператор* откат hello обновление текущего приложения с помощью hello [ **RollbackApplicationUpgradeAsync** метод](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_RollbackApplicationUpgradeAsync_System_Uri_System_TimeSpan_System_Threading_CancellationToken_), hello [ **Начала ServiceFabricApplicationRollback** командлет](https://docs.microsoft.com/powershell/servicefabric/vlatest/start-servicefabricapplicationrollback), или hello [ **отката обновления приложения** операции REST](https://docs.microsoft.com/rest/api/servicefabric/rollback-an-application-upgrade).
10. Service Fabric обновления hello целевого приложения, запущенного в кластере hello без потери доступности какой-либо из составляющих служб hello.

В разделе hello [учебника обновления приложения](service-fabric-application-upgrade-tutorial.md) примеры.

## <a name="maintain"></a>Техническое обслуживание
1. Для обновления операционной системы и исправлений Service Fabric взаимодействует с hello доступности tooguarantee инфраструктуры Azure все hello приложений, работающих в кластере hello.
2. Для обновлений и исправлений платформы toohello Service Fabric Service Fabric обновляется без потери доступности какой-либо hello приложений, работающих в кластере hello.
3. *Администратор приложения* утверждает hello Добавление или удаление узлов из кластера после анализа данных об использовании емкости и прогнозируемых требований.
4. *Оператор* добавляет и удаляет узлы, заданные параметром hello *администратор приложения*.
5. При добавлении новых узлов tooor существующие узлы не будут удалены из кластера hello Service Fabric автоматически балансирует нагрузку работающих приложений на всех узлах hello кластера tooachieve оптимальной производительности hello.

## <a name="remove"></a>Удалить
1. *Оператор* можно удалить экземпляр работающей службы в кластере hello без удаления всего приложения hello, с помощью hello [ **DeleteServiceAsync** метод](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient#System_Fabric_FabricClient_ServiceManagementClient_DeleteServiceAsync_System_Fabric_Description_DeleteServiceDescription_System_TimeSpan_System_Threading_CancellationToken_) , hello [ **удаление ServiceFabricService** командлет](https://docs.microsoft.com/powershell/servicefabric/vlatest/remove-servicefabricservice), или hello [ **удаления службы** операции REST](https://docs.microsoft.com/rest/api/servicefabric/delete-a-service).  
2. *Оператор* также можно удалить экземпляр приложения и все его службы с помощью hello [ **DeleteApplicationAsync** метод](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_DeleteApplicationAsync_System_Fabric_Description_DeleteApplicationDescription_System_TimeSpan_System_Threading_CancellationToken_), hello [ **Удаление ServiceFabricApplication** командлет](https://docs.microsoft.com/powershell/servicefabric/vlatest/remove-servicefabricapplication), или hello [ **удалить приложение** операции REST](https://docs.microsoft.com/rest/api/servicefabric/delete-an-application).
3. После остановки приложения hello и служб, hello *оператор* можно отменить подготовку типа приложения hello, с помощью hello [ **UnprovisionApplicationAsync** метод](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_UnprovisionApplicationAsync_System_String_System_String_System_TimeSpan_System_Threading_CancellationToken_), Hello [ **Unregister ServiceFabricApplicationType** командлет](https://docs.microsoft.com/powershell/servicefabric/vlatest/unregister-servicefabricapplicationtype), или hello [ **Отмена подготовки приложения** операции REST](https://docs.microsoft.com/rest/api/servicefabric/unprovision-an-application). Отмена подготовки типа приложения hello не удаляет пакет приложения hello из hello ImageStore. Пакет приложения hello необходимо удалить вручную.
4. *Оператор* пакет приложения hello удаляет из hello хранилище образов с помощью hello [ **RemoveApplicationPackage** метод](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_RemoveApplicationPackage_System_String_System_String_) или hello [ **Удаление ServiceFabricApplicationPackage** командлет](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps).

См. статью [Развертывание и удаление приложений с помощью PowerShell](service-fabric-deploy-remove-applications.md), чтобы ознакомиться с примерами.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о разработке и тестировании приложений Service Fabric и служб, а также об управлении ими см. в следующих разделах.

* [Reliable Actors](service-fabric-reliable-actors-introduction.md)
* [Надежные службы](service-fabric-reliable-services-introduction.md)
* [Развертывание приложения](service-fabric-deploy-remove-applications.md)
* [Обновление приложения](service-fabric-application-upgrade.md)
* [Обзор Testability](service-fabric-testability-overview.md)
