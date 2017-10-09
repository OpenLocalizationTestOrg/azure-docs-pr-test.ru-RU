---
title: "aaaSimulate сбоев в Azure микрослужбами | Документы Microsoft"
description: "В этой статье рассказывается о hello действий тестирования в Microsoft Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: motanv
manager: timlt
editor: toddabel
ms.assetid: ed53ca5c-4d5e-4b48-93c9-e386f32d8b7a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: motanv;heeldin
ms.openlocfilehash: 5bdda1c0c5a40b243ab956c4791afd52e11c4089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="testability-actions"></a>Действия, доступные благодаря Testability
В порядке toosimulate ненадежной инфраструктуру Azure Service Fabric предоставляет, способов toosimulate разработчику hello различных сбоев реальных и переходов между состояниями. Такие действия доступны благодаря компоненту Testability. Hello действия являются hello низкоуровневые интерфейсы API, которые привести внесения конкретных ошибок, переход состояния или проверки. Сочетая эти действия, вы можете создать комплексные сценарии тестирования своих служб.

В платформе Service Fabric доступны несколько распространенных сценариев тестирования, которые состоят из этих действий. Настоятельно рекомендуется использовать эти встроенные сценариев, которые выбираются тщательно tootest общие переходы между состояниями и случаи сбоев. Тем не менее действия могут быть сценарии тестирования используется toocreate при необходимости tooadd покрытия для сценариев, не охваченных встроенной сценарии hello еще или, являются пользовательскими, адаптированные для вашего приложения.

C# реализации hello действия находятся в hello System.Fabric.dll сборки. модуль PowerShell System структуры Hello в hello Microsoft.ServiceFabric.Powershell.dll сборки найден. В процессе установки среды выполнения hello модуля ServiceFabric PowerShell — установленных tooallow для удобства использования.

## <a name="graceful-vs-ungraceful-fault-actions"></a>Нормальные и ненормальные ошибки
Действия, доступные благодаря Testability, делятся на две основных части.

* Ненормальные ошибки. Эти сбои имитируют ошибки, такие как перезагрузки компьютеров и аварийное завершение процессов. В таких случаях сбои hello контекста выполнения процесса неожиданно останавливается. Это означает, что очистка hello состояния может выполняться перед запуском приложения hello еще раз.
* Нормальные ошибки. Эти сбои имитируют нормальные действия, такие как перемещение реплик и операции удаления, инициированные балансировкой нагрузки. В таких случаях служба hello получает уведомление о hello закрыть и можно очистить состояние hello перед выходом.

Для повышения качества проверки, запустить службу hello и business рабочей нагрузки при инициирует различные корректное и нестандартного сбоев. Нестандартного ошибки выполнение сценариев, где процесс службы hello неожиданно завершает работу в середине hello некоторых рабочих процессов. Это тесты hello путь восстановления после восстановления hello реплики службы с помощью Service Fabric. Это поможет проверить согласованность данных и ли правильной поддержки hello состояния службы после сбоев. Hello сбоев (hello корректное сбоев) другой набор тестирования, hello службы правильно реагирует tooreplicas перемещаются Service Fabric. Это проверяет обработка отмены в метод RunAsync hello. Служба Hello должна toocheck hello отмены маркера, значение и правильно сохранять свое состояние выхода из метода RunAsync hello.

## <a name="testability-actions-list"></a>Список действий, доступных благодаря Testability
| Действие | Описание | Управляемый интерфейс API | Командлет PowerShell | Нормальная или ненормальная ошибка |
| --- | --- | --- | --- | --- |
| CleanTestState |Удаляет все состояния теста hello из кластера hello в случае неудачного завершения теста драйвера hello. |CleanTestStateAsync |Remove-ServiceFabricTestState |Не применяется |
| InvokeDataLoss |Приводит к потере данных в разделе службы. |InvokeDataLossAsync |Invoke-ServiceFabricPartitionDataLoss |Нормальная |
| InvokeQuorumLoss |Приводит к потере кворума в указанном разделе службы с отслеживанием состояния. |InvokeQuorumLossAsync |Invoke-ServiceFabricQuorumLoss |Нормальная |
| Move Primary |Перемещает hello указан основной реплики службы с отслеживанием состояния toohello указанный узел кластера. |MovePrimaryAsync |Move-ServiceFabricPrimaryReplica |Нормальная |
| Move Secondary |Перемещает hello текущей вторичной реплики службы с отслеживанием состояния tooa другом узле кластера. |MoveSecondaryAsync |Move-ServiceFabricSecondaryReplica |Нормальная |
| RemoveReplica |Имитирует ошибку реплики путем удаления реплики из кластера. Это будет закрыт реплики hello и будет выполнить переход toorole «None», удаление свое состояние из кластера hello. |RemoveReplicaAsync |Remove-ServiceFabricReplica |Нормальная |
| RestartDeployedCodePackage |Имитирует ошибку процесса пакета кода путем перезапуска пакета кода, развернутого на узле в кластере. Это отменяет пакет кода hello процесс, который будет перезапустить все реплики службы пользователя hello, размещенные в этом процессе. |RestartDeployedCodePackageAsync |Restart-ServiceFabricDeployedCodePackage |Ненормальная |
| RestartNode |Имитирует ошибку узла кластера Service Fabric путем перезапуска узла. |RestartNodeAsync |Restart-ServiceFabricNode |Ненормальная |
| RestartPartition |Имитирует сценарий отключения центра обработки данных или кластера путем перезапуска некоторых или всех реплик раздела. |RestartPartitionAsync |Restart-ServiceFabricPartition |Нормальная |
| RestartReplica |Имитирует сбой реплики путем перезапуска материализованный реплики в кластере, закрытие реплики hello и открыв его снова. |RestartReplicaAsync |Restart-ServiceFabricReplica |Нормальная |
| StartNode |Запускает узел в кластере, который уже остановлен. |StartNodeAsync |Start-ServiceFabricNode |Не применяется |
| StopNode |Имитирует ошибку узла, останавливая его работу в кластере. узел Hello остается вниз, пока не будет вызван StartNode. |StopNodeAsync |Stop-ServiceFabricNode |Ненормальная |
| ValidateApplication |Проверяет доступность hello и работоспособность всех служб Service Fabric внутри приложения, обычно после включения некоторых ошибок сборки в систему hello. |ValidateApplicationAsync |Test-ServiceFabricApplication |Не применяется |
| ValidateService |Проверяет доступность hello и работоспособность службы Service Fabric, обычно после включения некоторых ошибок сборки в систему hello. |ValidateServiceAsync |Test-ServiceFabricService |Не применяется |

## <a name="running-a-testability-action-using-powershell"></a>Выполнение действия тестирования с помощью PowerShell
В этом учебнике показано как toorun действие тестирования с помощью PowerShell. Вы узнаете, как toorun тестирования действие по отношению к локальному кластеру (одно поле) или кластере Azure. Microsoft.Fabric.Powershell.dll--hello модуля Service Fabric PowerShell — устанавливается автоматически при установке MSI-файла структуры службы Microsoft hello. модуль Hello загружается автоматически при открытии командной строке PowerShell.

Разделы учебника

* [Выполнение действия для кластера с одним полем](#run-an-action-against-a-one-box-cluster)
* [Выполнение действия для кластера Azure](#run-an-action-against-an-azure-cluster)

### <a name="run-an-action-against-a-one-box-cluster"></a>Выполнение действия для кластера с одним полем
toorun тестирования действие по отношению к локальному кластеру, сначала соединения toohello кластера Привет открыть командную строку PowerShell с правами администратора. Рассмотрим hello **ServiceFabricNode перезапуска** действие.

```powershell
Restart-ServiceFabricNode -NodeName Node1 -CompletionMode DoNotVerify
```

Здесь hello действие **ServiceFabricNode перезапуска** выполняется на узел с именем «Node1». режим завершения Hello указывает, что он не должен проверять, действительно ли успешным действие перезапуска узла hello. Указание режим завершения hello как «Проверить» приведет к его tooverify ли действие перезапуска hello фактически выполнена успешно. Вместо прямого указания hello узла по его имени, можно указать его через тип ключа и hello секции реплики, следующим образом:

```powershell
Restart-ServiceFabricNode -ReplicaKindPrimary  -PartitionKindNamed -PartitionKey Partition3 -CompletionMode Verify
```


```powershell
$connection = "localhost:19000"
$nodeName = "Node1"

Connect-ServiceFabricCluster $connection
Restart-ServiceFabricNode -NodeName $nodeName -CompletionMode DoNotVerify
```

**Перезапуск ServiceFabricNode** должно быть используется toorestart Service Fabric узла в кластере. Это остановит процесс Fabric.exe hello, который будет перезапустите все hello системы служб и пользователей службы реплики, размещенные на этом узле. С помощью этого API tootest службы помогает обнаружить ошибки по путям восстановления hello отработки отказа. Он позволяет имитировать сбоев узлов в кластере hello.

Hello следующем снимке экрана показано hello **ServiceFabricNode перезапуска** команда тестирования в действии.

![](media/service-fabric-testability-actions/Restart-ServiceFabricNode.png)

Hello вывод hello сначала **Get ServiceFabricNode** (командлета из модуля Service Fabric PowerShell hello) показывает, что hello локальный кластер имеет пять узлов: Node.1 tooNode.5. После выполнения действия тестирования hello (командлет) **ServiceFabricNode перезапуска** выполняется на узле hello с именем Node.4, мы видим, время работы этого узла hello был сброшен.

### <a name="run-an-action-against-an-azure-cluster"></a>Выполнение действия для кластера Azure
При выполнении действия тестирования (с помощью PowerShell) для кластера служб Azure — аналогичные действие hello toorunning по отношению к локальному кластеру. Hello только различие состоит в том перед выполнением действия hello, вместо соединения локального кластера toohello необходимо tooconnect toohello Azure сначала кластера.

## <a name="running-a-testability-action-using-c35"></a>Выполнение действия, доступного благодаря Testability, с помощью C&#35;
toorun действие тестирования с помощью C#, сначала необходимо tooconnect toohello кластера с помощью FabricClient. Затем получите toorun hello hello параметры, необходимые действия. Можно использовать различные параметры toorun hello одним действием.
Просмотрев hello RestartServiceFabricNode действие, одним из способов toorun, возможно, это с помощью сведений об узле hello (имя узла и идентификатор экземпляра узла) в кластере hello.

```csharp
RestartNodeAsync(nodeName, nodeInstanceId, completeMode, operationTimeout, CancellationToken.None)
```

Описание параметров

* **CompleteMode** указывает, режим hello не должен проверять ли действие перезапуска hello фактически выполнена успешно. Указание режим завершения hello как «Проверить» приведет к его tooverify ли действие перезапуска hello фактически выполнена успешно.  
* **OperationTimeout** наборов hello количество времени для операции toofinish hello, прежде чем создается исключение TimeoutException.
* **CancellationToken** позволяет toobe ожидающие вызов отменен.

Вместо прямого указания hello узла по его имени, можно указать его через тип ключа и hello секции реплики.

Дополнительные сведения: [PartitionSelector и ReplicaSelector](#partition_replica_selector).

```csharp
// Add a reference tooSystem.Fabric.Testability.dll and System.Fabric.dll
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Fabric.Testability;
using System.Fabric;
using System.Threading;
using System.Numerics;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";
        Uri serviceName = new Uri("fabric:/samples/PersistentToDoListApp/PersistentToDoListService");
        string nodeName = "N0040";
        BigInteger nodeInstanceId = 130743013389060139;

        Console.WriteLine("Starting RestartNode test");
        try
        {
            //Restart hello node by using ReplicaSelector
            RestartNodeAsync(clusterConnection, serviceName).Wait();

            //Another way toorestart node is by using nodeName and nodeInstanceId
            RestartNodeAsync(clusterConnection, nodeName, nodeInstanceId).Wait();
        }
        catch (AggregateException exAgg)
        {
            Console.WriteLine("RestartNode did not complete: ");
            foreach (Exception ex in exAgg.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("RestartNode completed.");
        return 0;
    }

    static async Task RestartNodeAsync(string clusterConnection, Uri serviceName)
    {
        PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);
        ReplicaSelector primaryofReplicaSelector = ReplicaSelector.PrimaryOf(randomPartitionSelector);

        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(primaryofReplicaSelector, CompletionMode.Verify);
    }

    static async Task RestartNodeAsync(string clusterConnection, string nodeName, BigInteger nodeInstanceId)
    {
        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(nodeName, nodeInstanceId, CompletionMode.Verify);
    }
}
```

## <a name="partitionselector-and-replicaselector"></a>PartitionSelector и ReplicaSelector
### <a name="partitionselector"></a>PartitionSelector
PartitionSelector — это помощник, представлены в возможности тестирования и является используется tooselect конкретной секции на какие tooperform действий тестирования hello. Если заранее известно, идентификатор секции hello может быть используется tooselect определенной секции. Также можно ввести ключ секции hello и операции hello внутренне разрешит секции с Идентификатором hello. Также имеется возможность выбора случайного разбиения hello.

toouse этого вспомогательного объекта создайте объект PartitionSelector hello и выберите раздел hello с помощью одного из методов hello Select *. Затем передайте hello PartitionSelector объекта toohello API, которая в нем нуждается. Если параметр не выбран, то по умолчанию tooa случайного разбиения.

```csharp
Uri serviceName = new Uri("fabric:/samples/InMemoryToDoListApp/InMemoryToDoListService");
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
string partitionName = "Partition1";
Int64 partitionKeyUniformInt64 = 1;

// Select a random partition
PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);

// Select a partition based on ID
PartitionSelector partitionSelectorById = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);

// Select a partition based on name
PartitionSelector namedPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionName);

// Select a partition based on partition key
PartitionSelector uniformIntPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionKeyUniformInt64);
```

### <a name="replicaselector"></a>ReplicaSelector
ReplicaSelector — это помощник, представлены в возможности тестирования и является используется toohelp выберите реплику, на какие tooperform действий тестирования hello. Если заранее известно, идентификатор hello реплики может быть используется tooselect конкретной реплики. Кроме того предусмотрена возможность hello выбрать первичной реплики или случайное получателя. ReplicaSelector является производным от PartitionSelector, поэтому требуется tooselect оба hello реплики и hello раздел, на котором вы хотите tooperform hello тестирования операции.

toouse этого вспомогательного объекта создайте объект ReplicaSelector и задайте нужным образом hello tooselect hello реплики и hello секции. Можно затем передайте его в hello API, которая в нем нуждается. Если параметр не выбран, то по умолчанию реплика случайных tooa и случайного разбиения.

```csharp
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);
long replicaId = 130559876481875498;

// Select a random replica
ReplicaSelector randomReplicaSelector = ReplicaSelector.RandomOf(partitionSelector);

// Select hello primary replica
ReplicaSelector primaryReplicaSelector = ReplicaSelector.PrimaryOf(partitionSelector);

// Select hello replica by ID
ReplicaSelector replicaByIdSelector = ReplicaSelector.ReplicaIdOf(partitionSelector, replicaId);

// Select a random secondary replica
ReplicaSelector secondaryReplicaSelector = ReplicaSelector.RandomSecondaryOf(partitionSelector);
```

## <a name="next-steps"></a>Дальнейшие действия
* [Сценарии Testability](service-fabric-testability-scenarios.md)
* Как tootest службы
  * [Моделирование ошибок во время рабочих нагрузок службы](service-fabric-testability-workload-tests.md)
  * [Ошибки обмена данными между службами](service-fabric-testability-scenarios-service-communication.md)

