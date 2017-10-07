---
title: "aaaReport и проверьте состояние работоспособности с помощью Azure Service Fabric | Документы Microsoft"
description: "Узнайте, как отчеты о работоспособности toosend в коде службы и как предоставляет toocheck hello работоспособности службы с помощью средств наблюдения за работоспособностью hello, Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: mfussell
editor: 
ms.assetid: 7c712c22-d333-44bc-b837-d0b3603d9da8
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: dekapur
ms.openlocfilehash: bcb838fefe3f2054447e1731d709e455560260e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="report-and-check-service-health"></a>Проверка работоспособности службы и оповещение о проблемах
При служб возникли проблемы, возможность toorespond tooand исправление инцидентов и простоям зависит от ваших проблем hello toodetect возможность быстро. Если проблем и ошибок диспетчера работоспособности Azure Service Fabric toohello отчет из кода службы, можно использовать стандартный работоспособности, Service Fabric предоставляет состояние работоспособности hello toocheck средства мониторинга.

Можно сообщить работоспособности из службы hello тремя способами:

* С помощью объектов [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) или [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext).  
  Можно использовать hello `Partition` и `CodePackageActivationContext` объектов работоспособности hello tooreport элементов, которые являются частью hello текущего контекста. Например код, выполняемый в рамках реплики может включать в отчет работоспособности только этой реплики, hello секции, к которому принадлежит и приложения hello, он является частью.
* C помощью `FabricClient`.   
  Можно использовать `FabricClient` tooreport работоспособности из кода службы hello, если кластер hello не [безопасного](service-fabric-cluster-security.md) или если hello служба запущена с правами администратора. В большинстве реальных сценариев не используются незащищенные кластеры и не предоставляются права администратора. С `FabricClient`, можно создать отчет по любой сущности, который является частью кластера hello работоспособности. В идеале тем не менее, код службы следует отправлять только отчеты, связанные tooits собственные работоспособности.
* Используйте hello API-интерфейс REST в кластер hello, приложения, развернутого приложения, службы, пакет службы, секции, реплики или уровней узлов. Это может быть работоспособности используется tooreport из контейнера.

В этой статье описывается пример, в котором сообщает о работоспособности из кода службы hello. Hello примере также показано, как можно hello средств, предоставляемых Service Fabric состояние работоспособности используется toocheck hello. В этой статье является предполагаемым toobe состояния toohello Краткое введение возможности Service Fabric. Для получения дополнительных сведений можно считывать hello наборы подробные статьи о работоспособности, начинающиеся со ссылкой hello в конце hello в этой статье.

## <a name="prerequisites"></a>Предварительные требования
Необходимо иметь hello установлены следующие компоненты:

* Visual Studio 2015 или Visual Studio 2017
* Пакет SDK для Service Fabric

## <a name="toocreate-a-local-secure-dev-cluster"></a>toocreate локальной разработки безопасного кластера
* Откройте PowerShell с правами администратора и выполните следующие команды hello:

![Команды где показано, как toocreate кластера безопасной разработки.](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-secure-dev-cluster.png)

## <a name="toodeploy-an-application-and-check-its-health"></a>toodeploy приложение и проверить его работоспособность.
1. Откройте Visual Studio от имени администратора.
2. Создание проекта с помощью hello **службы с отслеживанием состояния** шаблона.
   
    ![Создание приложения Service Fabric со службами с отслеживанием состояния](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-stateful-service-application-dialog.png)
3. Нажмите клавишу **F5** toorun приложения hello в режиме отладки. приложение Hello — развернутой toohello локального кластера.
4. После запуска приложения hello, щелкните правой кнопкой мыши значок локального кластера диспетчера hello в области уведомлений hello и выберите **управление локального кластера** из hello контекстное меню tooopen Service Fabric Explorer.
   
    ![Открытие обозревателя Service Fabric из области уведомлений](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/LaunchSFX.png)
5. работоспособность приложения Hello должен отображаться как в этот образ. В настоящее время должно быть приложение hello работоспособное без ошибок.
   
    ![Работоспособное приложение в обозревателе Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-healthy-app.png)
6. Вы также можете проверить исправность hello с помощью PowerShell. Можно использовать ```Get-ServiceFabricApplicationHealth``` toocheck работоспособности приложения и могут использовать ```Get-ServiceFabricServiceHealth``` toocheck работоспособности службы. Здравствуйте, отчет о работоспособности для hello наличие одного приложения в PowerShell в этот образ.
   
    ![Работоспособное приложение в PowerShell](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/ps-healthy-app-report.png)

## <a name="tooadd-custom-health-events-tooyour-service-code"></a>код службы tooyour события работоспособности пользовательские tooadd
шаблоны проектов Service Fabric Hello в Visual Studio содержится пример кода. Hello следующие шаги показывают, как сообщать работоспособности пользовательские события из кода службы. Такие отчеты отображаются автоматически в hello стандартные средства для мониторинга, Service Fabric предоставляет, такие как обозреватель Service Fabric, представление работоспособности Azure портала и PowerShell состояния.

1. Снова откройте приложение hello, созданную ранее в Visual Studio или создайте новое приложение с помощью hello **службы с отслеживанием состояния** шаблона Visual Studio.
2. Откройте файл Stateful1.cs hello и найти hello `myDictionary.TryGetValueAsync` вызов в hello `RunAsync` метод. Вы увидите, что этот метод возвращает `result` , содержит hello текущее значение счетчика "hello", так как логика ключа hello в этом приложении tookeep текущее число. Если бы это было реальном приложении и отсутствие hello результат представлен сбоя, необходимо tooflag этого события.
3. tooreport событие работоспособности при hello отсутствие результат представляет сбой, добавить hello, следующие шаги.
   
    а. Добавить hello `System.Fabric.Health` Stateful1.cs toohello имен файла.
   
    ```csharp
    using System.Fabric.Health;
    ```
   
    b. Добавьте следующий код после hello hello `myDictionary.TryGetValueAsync` вызова
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
    Мы сообщаем о работоспособности реплики, так как сообщение приходит от службы с отслеживанием состояния. Hello `HealthInformation` параметр сохраняет сведения о hello неполадку, которая сообщается.
   
    Если вы создавали службы без отслеживания состояния, используйте после кода hello
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
    ```
4. Если служба запущена с правами администратора или если hello кластера не [безопасного](service-fabric-cluster-security.md), можно также использовать `FabricClient` tooreport работоспособности, как показано в hello следующие шаги.  
   
    а. Создать hello `FabricClient` экземпляра после hello `var myDictionary` объявления.
   
    ```csharp
    var fabricClient = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });
    ```
   
    b. Добавьте следующий код после hello hello `myDictionary.TryGetValueAsync` вызова.
   
    ```csharp
    if (!result.HasValue)
    {
       var replicaHealthReport = new StatefulServiceReplicaHealthReport(
            this.Context.PartitionId,
            this.Context.ReplicaId,
            new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error));
        fabricClient.HealthManager.ReportHealth(replicaHealthReport);
    }
    ```
5. Давайте имитировать этот сбой и отобразится в средств мониторинга работоспособности hello. Сбой toosimulate hello, закомментируйте hello первой строки в код, добавленный ранее отчетности работоспособности hello. После закомментируйте первую строку hello, hello код будет выглядеть как следующий пример hello.
   
    ```csharp
    //if(!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
   Этот код запускается каждый раз при отчет о работоспособности hello `RunAsync` выполняет. После внесения изменения hello, нажмите клавишу **F5** toorun приложения hello.
6. После запуска приложения hello, откройте обозреватель Service Fabric toocheck hello работоспособности приложения hello. На этот раз обозреватель Service Fabric показывает, что приложение hello неработоспособен. Это из-за ошибки hello, произошедшая из кода hello, добавленный ранее.
   
    ![Неработоспособное приложение в обозревателе Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-unhealthy-app.png)
7. При выборе в представлении дерева hello Service Fabric Explorer hello первичной реплики, вы увидите, что **состояние работоспособности** слишком указывает на ошибку. Обозреватель Service Fabric также отображает сведения, которые были добавлены toohello отчет о работоспособности hello `HealthInformation` параметра в коде hello. Вы увидите hello же отчеты о работоспособности в PowerShell и hello портал Azure.
   
    ![Работоспособность реплики в обозревателе Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/replica-health-error-report-sfx.png)

В этом отчете остается в диспетчере работоспособности hello, пока не будет заменена другой отчет или пока не будет удалена эта реплика. Так как мы не задали `TimeToLive` отчета о работоспособности в hello `HealthInformation` объекта hello отчетов никогда не истекает.

Корпорация Майкрософт рекомендует работоспособности, должна быть представлена на самом детальном уровне hello, который в данном случае является репликой hello. Вы также можете создавать отчеты о работоспособности о `Partition`.

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
this.Partition.ReportPartitionHealth(healthInformation);
```

состояние tooreport на `Application`, `DeployedApplication`, и `DeployedServicePackage`, используйте `CodePackageActivationContext`.

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
var activationContext = FabricRuntime.GetActivationContext();
activationContext.ReportApplicationHealth(healthInformation);
```

## <a name="next-steps"></a>Дальнейшие действия
* [Подробный обзор работоспособности в Service Fabric](service-fabric-health-introduction.md)
* [REST API for reporting service health](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service) (REST API для формирования отчетов о работоспособности службы)
* [REST API for reporting application health](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-an-application) (REST API для формирования отчетов о работоспособности приложения)

