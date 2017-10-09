---
title: "Управление приложениями Azure Service Fabric aaaAutomate | Документы Microsoft"
description: "Развертывание, обновление, тестирование и удаление приложений Service Fabric с помощью PowerShell."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: f03f4294-571d-4262-8a77-cc8b481b959d
ms.service: service-fabric
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/16/2017
ms.author: ryanwi
redirect_url: /azure/service-fabric/service-fabric-deploy-remove-applications
ms.openlocfilehash: a64a39dbee26be8ac15fee767a90fd06bfe4b896
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="automate-hello-application-lifecycle-using-powershell"></a>Автоматизация жизненного цикла приложения hello, с помощью PowerShell
Многие аспекты hello [жизненный цикл приложений фабрики служб](service-fabric-application-lifecycle.md) можно автоматизировать.  В этой статье показано, как toouse PowerShell tooautomate общие задачи для развертывания, обновления, удаления и тестирование приложений Azure Service Fabric.  Также доступны управляемые API и API HTTP для управления приложениями. Дополнительные сведения см. в статье [Жизненный цикл приложения Service Fabric](service-fabric-application-lifecycle.md).  

## <a name="prerequisites"></a>Предварительные требования
Прежде чем перемещать toohello задач в статье hello, нужно убедиться, что:

* Ознакомьтесь с основными понятиями Service Fabric hello, описанной в [Технический обзор Service Fabric](service-fabric-technical-overview.md).
* [Установка среды выполнения hello, пакет SDK и средства](service-fabric-get-started.md), которая также устанавливается hello **ServiceFabric** модуля PowerShell.
* [Включение сценариев PowerShell](service-fabric-get-started.md#enable-powershell-script-execution)
* Запустите локальный кластер.  Запустите нового окна PowerShell с правами администратора и запустите сценарий установки кластера hello в папки hello SDK:`& "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"`
* Перед выполнением любых команд PowerShell в этой статье, сначала подключиться toohello локального кластера Service Fabric с помощью [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps):`Connect-ServiceFabricCluster localhost:19000`
* следующие задачи Hello требуют toodeploy пакета приложения v1 и v2 пакет приложения для обновления. Загрузите hello [ **WordCount** образец приложения](http://aka.ms/servicefabricsamples) (находится в образцы Приступая к работе hello). Выполните сборку и упаковку приложения hello в Visual Studio (щелкните правой кнопкой мыши **WordCount** в обозревателе решений и выберите **пакета**). Копировать пакет v1 hello в `C:\ServiceFabricSamples\Services\WordCount\WordCount\pkg\Debug` слишком`C:\Temp\WordCount`. Копировать `C:\Temp\WordCount` слишком`C:\Temp\WordCountV2`, создание пакета приложения hello v2 для обновления. Откройте `C:\Temp\WordCountV2\ApplicationManifest.xml` в текстовом редакторе. В hello **ApplicationManifest** элемент, изменение hello **ApplicationTypeVersion** слишком атрибут из «1.0.0» «2.0.0» номера версии приложения hello tooupdate. Сохраните файл ApplicationManifest.xml hello изменен.

## <a name="task-deploy-a-service-fabric-application"></a>Задача: развернуть приложение Service Fabric
После построения и упаковки приложения hello (или загружен пакет приложения hello), вы можете развернуть приложение hello в локальный кластер Service Fabric. Развертывание производится отправка пакета приложения hello, регистрация типа приложения hello и создание экземпляра приложения hello. Используйте инструкции hello в этот раздел toodeploy нового кластера tooa приложения.

### <a name="step-1-upload-hello-application-package"></a>Шаг 1: Отправка пакета приложения hello
Отправка toohello пакета приложения hello хранилища образов помещает его в расположение доступного toointernal Service Fabric компонентов.  пакет приложения Hello содержит hello необходимой манифест приложения, манифесты службы и кода, конфигурации и приложение hello toocreate пакетов данных и экземпляров службы. Пакет приложения hello tooverify локально, используйте hello [ServiceFabricApplicationPackage тест](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) командлета.  Hello [ServiceFabricApplicationPackage копирования](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) команда передачи hello пакета. Например:

```powershell
Copy-ServiceFabricApplicationPackage C:\Temp\WordCount\ -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCount
```

### <a name="step-2-register-hello-application-type"></a>Шаг 2: Регистрация типа приложения hello
Регистрация пакета приложения hello делает тип приложения hello и версии, объявленные в манифесте приложения hello доступны для использования. Hello считыванием переданный на первом шаге hello пакет hello, проверьте пакет hello (эквивалент toorunning [ServiceFabricApplicationPackage тест](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) локально), обрабатывать hello содержимое пакета и скопируйте tooan hello обработки пакета расположение внутренней системы.  Запустите hello [ServiceFabricApplicationType регистра](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) командлета:

```powershell
Register-ServiceFabricApplicationType WordCount
```
все типы приложения hello, зарегистрированные в кластере hello, запустите hello toosee [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) командлета:

```powershell
Get-ServiceFabricApplicationType
```

### <a name="step-3-create-hello-application-instance"></a>Шаг 3: Создание экземпляра приложения hello
Приложение может быть создан с помощью любой версии типа приложения, который успешно зарегистрирован с помощью hello [New ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) команды. Имя каждого приложения Hello объявляется во время развертывания и должно начинаться с hello **структуры:** схемы и быть уникальными для каждого экземпляра приложения. Hello имя типа приложения и версии типа приложения, объявляются в hello **ApplicationManifest.xml** файла пакета приложения hello. Если все службы по умолчанию были определены в манифесте приложения hello объекта тип целевого приложения hello, те, создаются в данный момент.

```powershell
New-ServiceFabricApplication fabric:/WordCount WordCount 1.0.0
```

Hello [Get ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) команда перечисляет все экземпляры приложения, которые успешно созданы, а также их общее состояние. Hello [Get ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) команда выводит список всех экземпляров службы hello, которые успешно созданы в экземпляре данного приложения. Этот список содержит службы по умолчанию (при наличии).

```powershell
Get-ServiceFabricApplication

Get-ServiceFabricApplication | Get-ServiceFabricService
```

## <a name="task-upgrade-a-service-fabric-application"></a>Задача: обновить приложение Service Fabric
Развернутое ранее приложение Service Fabric можно обновить с помощью обновленного пакета приложения. Эта задача обновляет приложение hello WordCount, которое было развернуто в «задач: развертывание приложения Service Fabric.» Дополнительные сведения см. в статье [Обновление приложения Service Fabric](service-fabric-application-upgrade.md).

простой tookeep действия в этом примере только номер версии приложения hello был обновлен в пакете приложения hello WordCountV2, созданном в предварительных требованиях для hello. Более реалистичном случае будет включать в себя обновление службы файлов кода, конфигурации и данных, а затем перестроения и упаковка приложения hello с номерами обновленной версии.  

### <a name="step-1-upload-hello-updated-application-package"></a>Шаг 1: Отправка пакета обновленное приложение hello
Hello приложения WordCount v1 — Готово toobe обновлены. Если открыть окно PowerShell от имени администратора, а также введите [ **Get ServiceFabricApplication**](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps), вы видите развертывания этой версии 1.0.0 hello тип приложения WordCount.  

Теперь hello копирования обновлен приложения пакета toohello Service Fabric образа хранилища (места хранения пакетов приложения hello, Service Fabric). Здравствуйте, параметр **ApplicationPackagePathInImageStore** информирует о том, где можно найти пакет приложения hello Service Fabric. Здравствуйте, следующая команда копирует hello пакета приложения слишком**WordCountV2** в хранилище образов hello:  

```powershell
Copy-ServiceFabricApplicationPackage C:\Temp\WordCountV2\ -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCountV2

```
### <a name="step-2-register-hello-updated-application-type"></a>Шаг 2: Регистрация hello обновить тип приложения
Hello следующим шагом является tooregister hello новую версию приложения hello в Service Fabric, которое может выполняться с помощью hello [ServiceFabricApplicationType регистра](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) командлета:

```powershell
Register-ServiceFabricApplicationType WordCountV2
```

### <a name="step-3-start-hello-upgrade"></a>Шаг 3: Запуск обновления hello
Различные параметры обновления, время ожидания и критерия работоспособности может быть применен tooapplication обновления. Прочтите hello [параметров обновления приложения](service-fabric-application-upgrade-parameters.md) и [процесс обновления](service-fabric-application-upgrade.md) toolearn дополнительные документы. Все службы и экземпляры должны быть *работоспособное* после обновления hello.  Набор hello **HealthCheckStableDuration** too60 секунд (что hello службы находятся в работоспособном состоянии для по крайней мере 20 секунд до toohello происходит обновление hello следующему домену обновления).  Также набор hello **UpgradeDomainTimeout** too1200 секунд и hello **UpgradeTimeout** too3000 секунд. Задайте hello **UpgradeFailureAction** слишком**отката**, какие запросы, которые Service Fabric откат hello предыдущей версии приложения toohello при возникновении ошибок во время обновления.

Теперь вы можете запустить обновление приложения hello, с помощью hello [ServiceFabricApplicationUpgrade начала](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) командлета:

```powershell
Start-ServiceFabricApplicationUpgrade -ApplicationName fabric:/WordCount -ApplicationTypeVersion 2.0.0 -HealthCheckStableDurationSec 60 -UpgradeDomainTimeoutSec 1200 -UpgradeTimeout 3000  -FailureAction Rollback -Monitored
```

Обратите внимание, что имя приложения hello hello таким же как hello ранее развернутое имя приложения версии 1.0.0 (fabric: / WordCount). Service Fabric использует это имя tooidentify, какое приложение обновляется начало. Если задать слишком короткий toobe тайм-ауты hello, могут возникать сообщение об ошибке времени ожидания hello, состояния проблемы. См. слишком[Устранение неполадок обновлений приложений](service-fabric-application-upgrade-troubleshooting.md), или увеличьте время ожидания hello.

### <a name="step-4-check-upgrade-progress"></a>Шаг 4. Проверка хода обновления
Можно отслеживать ход выполнения обновления приложения с помощью [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md), или с помощью hello [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) командлета:

```powershell
Get-ServiceFabricApplicationUpgrade fabric:/WordCount
```

Через несколько минут hello [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) командлет показывает, что все домены обновления были обновлены («завершено»).

## <a name="task-test-a-service-fabric-application"></a>Задача: протестировать приложение Service Fabric
toowrite службы высокого качества, разработчики должны toobe может tooinduce ненадежной инфраструктуры ошибок tootest hello стабильность их службы. Service Fabric предоставляет разработчикам hello возможность tooinduce сбоя действия и проверки служб в присутствии hello сбоев с помощью hello сценариев тестирования хаоса и переход на другой ресурс.  Прочтите [toohello введение ошибки Analysis Service](service-fabric-testability-overview.md) для получения дополнительных сведений.

### <a name="step-1-run-hello-chaos-test-scenario"></a>Шаг 1: Запустите сценарий теста хаоса hello
сценарии теста хаоса Hello приводит к возникновению ошибки через весь кластер Service Fabric hello. сценарий Hello сжимает сбои обычно по месяцам, годам tooa несколько часов. сочетание Hello с чередованием ошибок с ошибки с высокой частотой находит случаи, в противном случае останется незамеченной. Hello следующий пример запускает сценарии теста хаоса hello в течение 60 минут.

```powershell
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```

### <a name="step-2-run-hello-failover-test-scenario"></a>Шаг 2: Запуск сценария тестовой отработки отказа hello
отработки отказа Hello тестирования цели сценария секцию определенной службы, а не весь кластер hello и других служб остается без изменений. сценарий Hello итерацию последовательности имитацию ошибок при проверке службы во время выполнения бизнес-логики. Ошибка при проверке службы указывает на проблему, которую необходимо дополнительно изучить. тест отработки отказа Hello вызывает только ошибок во время, в противоположность toohello хаоса тестового сценария, который можно вызвать несколько ошибок. Hello следующий пример запускает hello теста отработки отказа в течение 60 минут для hello fabric: / WordCount/WordCountService службы.

```powershell
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/WordCount/WordCountService"

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindUniformInt64 -PartitionKey 1
```

## <a name="task-remove-a-service-fabric-application"></a>Задача: удалить приложение Service Fabric
Удаление экземпляра развернутого приложения, удалить тип приложения hello подготовить из кластера hello и удаление пакета приложения hello из hello ImageStore.

### <a name="step-1-remove-an-application-instance"></a>Шаг 1. Удаление экземпляра приложения
При экземпляр приложения больше не нужен, можно окончательно удалить его с помощью hello [ServiceFabricApplication удаление](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) командлета. Эта функция также автоматически удаляет все службы, принадлежащие toohello приложения, без возможности восстановления, удаляя все состояния службы. Эта операция необратима, и вы не сможете восстановить состояние приложения.

```powershell
Remove-ServiceFabricApplication fabric:/WordCount
```

### <a name="step-2-unregister-hello-application-type"></a>Шаг 2: Отмена регистрации типа приложения hello
Если вам больше не требуется определенной версии типа приложения, отменить его регистрацию с помощью hello [Unregister ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) командлета. Отмена регистрации неиспользуемые типы выпуски пространства, используемого пакета приложения hello в хранилище образов hello. Регистрацию типа приложения можно отменить в том случае, если на его основе не были созданы экземпляры приложений и нет ссылающихся на него незавершенных обновлений приложений.

```powershell
Unregister-ServiceFabricApplicationType WordCount 1.0.0
```

### <a name="step-3-remove-hello-application-package"></a>Шаг 3: Удаление пакета приложения hello
После типа приложения hello не зарегистрирован, пакет приложения hello можно удалить из хранилища образов hello с помощью hello [ServiceFabricApplicationPackage удаление](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) командлета.

```powershell
Remove-ServiceFabricApplicationPackage -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCount
```

## <a name="next-steps"></a>Дальнейшие действия
[Жизненный цикл приложения Service Fabric](service-fabric-application-lifecycle.md)

[Развертывание приложения](service-fabric-deploy-remove-applications.md)

[Обновление приложения](service-fabric-application-upgrade.md)

[Командлеты Azure Service Fabric](/powershell/azure/overview?view=azureservicefabricps)

