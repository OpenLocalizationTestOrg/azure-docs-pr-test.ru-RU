---
title: "Проверка работоспособности и оповещение о проблемах в Azure Service Fabric | Документация Майкрософт"
description: "Узнайте, как отправлять отчеты о работоспособности из кода службы и проверять работоспособность службы с использованием средств наблюдения Azure Service Fabric."
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
ms.openlocfilehash: 83981d5bec14c06c509f1a8a4153dc23298f5ce0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="report-and-check-service-health"></a>Проверка работоспособности службы и оповещение о проблемах
Если при работе служб возникают проблемы, то возможность ответить на все возникшие инциденты и устранить их зависит от того, насколько быстро вы сможете обнаружить проблему. Сообщив о проблемах и сбоях диспетчеру работоспособности Azure Service Fabric из кода службы, вы сможете использовать стандартные средства мониторинга работоспособности, которые предоставляет Service Fabric.

Существует три способа, с помощью которых служба может сообщить о своей работоспособности:

* С помощью объектов [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) или [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext).  
  Используйте объекты `Partition` и `CodePackageActivationContext`, чтобы сообщить сведения о работоспособности элементов, которые являются частью текущего контекста. Например, код, выполняемый в рамках реплики, может передать сведения о работоспособности только для этой реплики, раздела, к которому она принадлежит, и приложения, частью которого она является.
* C помощью `FabricClient`.   
  `FabricClient` можно использовать для передачи сведений о работоспособности из кода службы в том случае, если кластер не является [безопасным](service-fabric-cluster-security.md) или если служба запущена с правами администратора. В большинстве реальных сценариев не используются незащищенные кластеры и не предоставляются права администратора. С помощью `FabricClient`можно отправлять сведения о работоспособности для любой сущности, которая является частью кластера. Но в идеале код службы должен сообщать только о работоспособности самой службы.
* Используйте интерфейсы REST API на уровне кластера, приложения, развернутого приложения, службы, пакета службы, секции, реплики или узла. Так можно сообщить о работоспособности из контейнера.

В этой статье описан пример того, как отправлять отчеты о работоспособности из кода службы. В примере также показано, как можно использовать инструменты, предоставляемые Service Fabric, для проверки состояния работоспособности. Эта статья представляет собой краткое изложение возможностей Service Fabric по отслеживанию работоспособности. Для получения дополнительных сведений вы можете прочесть серию подробных статей о работоспособности, начиная со статьи, ссылка на которую приведена в конце этой статьи.

## <a name="prerequisites"></a>Предварительные требования
Должны быть установлены следующие компоненты:

* Visual Studio 2015 или Visual Studio 2017
* Пакет SDK для Service Fabric

## <a name="to-create-a-local-secure-dev-cluster"></a>Создание безопасного локального кластера для разработки
* Запустите PowerShell с правами администратора и выполните следующие команды.

![Команды для создания безопасного кластера для разработки](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-secure-dev-cluster.png)

## <a name="to-deploy-an-application-and-check-its-health"></a>Развертывание приложения и проверка его работоспособности
1. Откройте Visual Studio от имени администратора.
2. Создайте проект с помощью шаблона **службы с отслеживанием состояния** .
   
    ![Создание приложения Service Fabric со службами с отслеживанием состояния](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-stateful-service-application-dialog.png)
3. Нажмите **F5** , чтобы запустить приложение в режиме отладки. Приложение будет развернуто на локальный кластер.
4. После запуска приложения в области уведомлений щелкните правой кнопкой мыши значок локального диспетчера кластера и выберите в контекстном меню пункт **Управление локальным кластером** , чтобы открыть обозреватель Service Fabric.
   
    ![Открытие обозревателя Service Fabric из области уведомлений](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/LaunchSFX.png)
5. Состояние работоспособности приложения должно отображаться, как показано на рисунке ниже. Приложение должно работать исправно и без ошибок.
   
    ![Работоспособное приложение в обозревателе Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-healthy-app.png)
6. Кроме того, вы можете проверить работоспособность с помощью PowerShell. Вы можете использовать команду ```Get-ServiceFabricApplicationHealth``` для проверки работоспособности приложения, а ```Get-ServiceFabricServiceHealth``` — для проверки работоспособности службы. Отчет о работоспособности для этого же приложения в PowerShell выглядит следующим образом:
   
    ![Работоспособное приложение в PowerShell](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/ps-healthy-app-report.png)

## <a name="to-add-custom-health-events-to-your-service-code"></a>Добавление пользовательских событий работоспособности в код службы
В шаблонах проекта Service Fabric в Visual Studio приведен пример кода. Ниже показано, как сообщить о пользовательских событиях работоспособности из кода службы. Такие отчеты автоматически появятся в стандартных инструментах для наблюдения за работоспособностью, предоставляемых Service Fabric, таких как Service Fabric Explorer, представление работоспособности на портале Azure и PowerShell.

1. Повторно откройте приложение, созданное ранее в Visual Studio, или создайте новое приложение с использованием шаблона **службы с отслеживанием состояния** в Visual Studio.
2. Откройте файл Stateful1.cs и найдите вызов `myDictionary.TryGetValueAsync` в методе `RunAsync`. Как видите, этот метод возвращает `result` , который содержит текущее значение счетчика, так как основная логика этого приложения — поддерживать работу счетчика. В настоящем приложении, если отсутствие результата означает сбой, необходимо сообщить о нарушении работоспособности.
3. Чтобы сообщить о событии отсутствия результата, что представляет собой сбой, сделайте следующее:
   
    а. Добавьте в файл Stateful1.cs пространство имен `System.Fabric.Health` .
   
    ```csharp
    using System.Fabric.Health;
    ```
   
    b. Добавьте приведенный ниже код после вызова `myDictionary.TryGetValueAsync` .
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
    Мы сообщаем о работоспособности реплики, так как сообщение приходит от службы с отслеживанием состояния. Параметр `HealthInformation` содержит сведения о сообщенной в отчете проблеме с работоспособностью.
   
    Если была создана служба без отслеживания состояния, используйте следующий код.
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
    ```
4. Если служба запущена с правами администратора или кластер не является [безопасным](service-fabric-cluster-security.md), для отправки сведений о работоспособности также можно использовать `FabricClient`, как показано ниже.  
   
    а. Создайте экземпляр `FabricClient` после объявления `var myDictionary`.
   
    ```csharp
    var fabricClient = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });
    ```
   
    b. Добавьте приведенный ниже код после вызова `myDictionary.TryGetValueAsync` .
   
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
5. Давайте сымитируем этот сбой и посмотрим, как он будет отображаться в средствах наблюдения за работоспособностью. Чтобы сымитировать сбой, закомментируйте первую строку в коде проверки работоспособности, который был добавлен ранее. После этого код будет выглядеть так, как показано ниже.
   
    ```csharp
    //if(!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
   Этот код отправляет отчет о работоспособности при каждом выполнении `RunAsync`. После внесения изменений нажмите клавишу **F5** для запуска приложения.
6. Запустив приложение, откройте обозреватель Service Fabric для проверки работоспособности приложения. На этот раз Service Fabric Explorer показывает, что работоспособность приложения нарушена. Это вызвано ошибкой в коде, который мы добавили раньше.
   
    ![Неработоспособное приложение в обозревателе Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-unhealthy-app.png)
7. При выборе основной реплики в древовидном представлении обозревателя Service Fabric вы увидите, что в ней также отображается **нарушение работоспособности** . Кроме того, в обозревателе Service Fabric отображаются подробные сведения о работоспособности, добавленные в параметр `HealthInformation` в коде. Эти же отчеты о работоспособности можно просмотреть с помощью PowerShell и на портале Azure.
   
    ![Работоспособность реплики в обозревателе Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/replica-health-error-report-sfx.png)

Этот отчет останется в диспетчере работоспособности до тех пор, пока не будет заменен другим отчетом или пока эта реплика не будет удалена. Так как мы не задали параметр `TimeToLive` для этого отчета о работоспособности в объекте `HealthInformation`, срок действия отчета не истечет.

Сведения о работоспособности рекомендуется сообщать на самом детальном уровне. В приведенном выше случае это уровень реплики. Вы также можете создавать отчеты о работоспособности о `Partition`.

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
this.Partition.ReportPartitionHealth(healthInformation);
```

Чтобы создавать отчеты о работоспособности о `Application`, `DeployedApplication` и `DeployedServicePackage`, используйте `CodePackageActivationContext`.

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
var activationContext = FabricRuntime.GetActivationContext();
activationContext.ReportApplicationHealth(healthInformation);
```

## <a name="next-steps"></a>Дальнейшие действия
* [Подробный обзор работоспособности в Service Fabric](service-fabric-health-introduction.md)
* [REST API for reporting service health](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service) (REST API для формирования отчетов о работоспособности службы)
* [REST API for reporting application health](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-an-application) (REST API для формирования отчетов о работоспособности приложения)

