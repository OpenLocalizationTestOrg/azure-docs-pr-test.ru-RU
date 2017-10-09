---
title: "aaaTroubleshoot с отчеты о работоспособности системы | Документы Microsoft"
description: "Описание отчетов о работоспособности hello, отправленных компонентами Azure Service Fabric и их использования для устранения неполадок кластера или проблемы с приложением."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: 52574ea7-eb37-47e0-a20a-101539177625
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: c77a6cdd0440ce5d354cd8760f40151f674a3529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-system-health-reports-tootroubleshoot"></a>Использовать tootroubleshoot отчеты о работоспособности системы
Azure Service Fabric компоненты отчет стандартной hello все сущности в кластере hello. Hello [базе данных health store](service-fabric-health-introduction.md#health-store) создает и удаляет сущности на основании отчетов системы hello. Кроме того, эти сущности упорядочиваются в иерархию с учетом взаимодействия между ними.

> [!NOTE]
> Основные понятия здоровья toounderstand, ознакомьтесь с дополнительными на [модель работоспособности Service Fabric](service-fabric-health-introduction.md).
> 
> 

В отчетах о работоспособности системы отражаются показатели функциональности кластеров и приложений, а также отмечаются проблемы с работоспособностью. Для приложений и служб отчеты о работоспособности системы убедитесь, что сущности, реализуются и правильно работает с hello перспективы Service Fabric. Hello отчеты не имеют любой наблюдение за работоспособностью hello бизнес-логику службы hello или обнаружения зависших процессов. Пользователь службы можно обогатить данные работоспособности hello с логикой конкретных tootheir сведения.

> [!NOTE]
> Отчеты о работоспособности watchdogs видны только *после* компоненты системы hello создание сущности. При удалении сущности, базе данных health store hello автоматически удаляет все связанные с ним отчеты о работоспособности. Hello это справедливо при создании нового экземпляра сущности hello (например, создается новый экземпляр службы с отслеживанием состояния сохраненного реплики). Все отчеты, связанные с hello старого экземпляра удаляются и удаляются из хранилища hello.
> 
> 

Hello отчетов компонента системы идентифицируются hello источника, который начинается с hello»**системы.**» . Watchdogs не следует использовать одинаковые префиксы для своих источников hello как отчеты с недопустимыми параметрами отклоняются.
Давайте рассмотрим некоторые системы сообщает toounderstand их триггеры и о том, как toocorrect hello возможные причины неполадок они представляют.

> [!NOTE]
> Service Fabric продолжается отчеты tooadd условиями интерес, повысить видимость выполняемых в кластере hello и приложения. Также можно улучшить существующие отчеты более подробные данные, toohelp устранить проблему hello, быстрее.
> 
> 

## <a name="cluster-system-health-reports"></a>Системные отчеты о работоспособности кластеров
сущности работоспособности кластера Hello автоматически создается в базе данных health store hello. Если все работает надлежащим образом, в этом хранилище нет системного отчета.

### <a name="neighborhood-loss"></a>Потеря окружения
**System.Federation** сообщает об ошибке при обнаружении потери окружения. Hello отчет получен из отдельных узлов, и идентификатор узла hello включается в имени свойства hello. В случае утраты одно окружение в hello всего обмена Service Fabric обычно можно ожидать два события (обе стороны hello разрыв отчета). Если теряется несколько окружений, происходит больше событий.

Hello отчета указывает время ожидания аренды глобального hello как toolive время hello. отчет Hello повторен каждые половине длительность TTL hello при условии, что условие hello остается активным. событие Hello автоматически удаляется после истечения срока его действия. Удалите при истекшим сроком действия поведение гарантирует, что отчет hello очистки из хранилища работоспособности hello правильно, даже если hello узел «отчеты» не работает.

* **SourceId**: System.Federation.
* **Свойство**: начинается с **Neighborhood** и включает сведения об узле.
* **Дальнейшие действия**: изучить, почему окружение hello теряется (например, проверка hello связи между узлами кластера).

## <a name="node-system-health-reports"></a>Системные отчеты о работоспособности узлов
**System.FM**, который представляет службу диспетчера отказоустойчивости hello, hello центром сертификации, который управляет сведения об узлах кластера. Каждый узел должен содержать один отчет системы System.FM о его состоянии. Hello узла сущностей удаляются при удалении состояния узла hello (см. [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).

### <a name="node-updown"></a>Включение и отключение узла
System.FM отчеты в виде ОК при присоединении узла hello кольцо hello (это работает). Сообщение об ошибке при hello узла не соответствует кольцо hello (для обновления или просто не работает, либо из-за непрохождения). иерархии работоспособности Hello, построенных по базе данных health store hello предпринимает действия развернутой сущностей в связи с System.FM отчеты узлов. Он считает узел hello виртуальный родительский всех развернутых сущностей. сущности Hello развернуты на этом узле, предоставляются через запросы, если узел hello вверх по System.FM, с hello же экземпляр как экземпляр hello, связанный с сущностями hello. Если System.FM сообщение hello узла не работает или перезапуска (экземпляра), базе данных health store hello автоматически очищает hello развертывания сущностей, которые могут существовать только hello работу узла или hello предыдущий экземпляр узла hello.

* **SourceId**: System.FM.
* **Свойство**: State.
* **Дальнейшие действия**: Если hello узел не работает для обновления, он должен возвращаться к работе после его обновления. В этом случае состояние работоспособности hello следует перейти назад tooOK. Если узел hello не возвращаться или завершается с ошибкой, hello проблема, требующая дополнительного изучения.

Hello ниже приведен пример hello System.FM событий с состоянием работоспособности ОК для узла.

```powershell
PS C:\> Get-ServiceFabricNodeHealth  _Node_0

NodeName              : _Node_0
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 8
                        SentAt                : 7/14/2017 4:54:51 PM
                        ReceivedAt            : 7/14/2017 4:55:14 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```


### <a name="certificate-expiration"></a>Истечение срока действия сертификата
**System.FabricNode** отображает предупреждение, когда сертификаты, используемые узлом hello, истекающим сроком действия. У каждого узла есть три сертификата: **Certificate_cluster**, **Certificate_server** и **Certificate_default_client**. При по крайней мере две недели до истечения срока действия hello состояние работоспособности hello отчетов — ОК. Когда hello истечение срока действия в течение двух недель, тип отчета hello является предупреждением. Бесконечный срок ЖИЗНИ этих событий, и они будут удалены после выхода узла из кластера hello.

* **SourceId**: System.FabricNode.
* **Свойство**: начинается с **сертификат** и содержит дополнительные сведения о типе hello сертификата
* **Дальнейшие действия**: обновление сертификатов hello, если они имеют истекающим сроком действия.

### <a name="load-capacity-violation"></a>Нарушение емкости для загрузки
Hello балансировки нагрузки Service Fabric отображает предупреждение, когда он обнаруживает нарушение емкости узла.

* **SourceId**: System.PLB.
* **Свойство**: начинается с **Capacity**.
* **Дальнейшие действия**: проверка предоставленных метрики и представление текущей емкости hello на узле hello.

## <a name="application-system-health-reports"></a>Системные отчеты о работоспособности приложений
**System.CM**, который представляет службу диспетчера кластеров hello, hello центром сертификации, который управляет сведений о приложении.

### <a name="state"></a>Состояние
System.CM отчеты в виде ОК после создания или обновления приложения hello. Информирует hello работоспособности хранилища при удалении приложения hello, чтобы его можно удалить из хранилища.

* **SourceId**: System.CM.
* **Свойство**: State.
* **Дальнейшие действия**: Если для создания или обновления приложения hello, он должен включать отчет о работоспособности hello диспетчер кластеров. В противном случае проверьте состояние hello приложения hello запрос (например, hello командлета PowerShell **Get ServiceFabricApplication - ApplicationName *applicationName***).

Hello приведенном ниже примере показаны события состояния hello hello **fabric: / WordCount** приложения:

```powershell
PS C:\> Get-ServiceFabricApplicationHealth fabric:/WordCount -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics

ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Ok
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/14/2017 4:55:10 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
```

## <a name="service-system-health-reports"></a>Системные отчеты о работоспособности служб
**System.FM**, который представляет службу диспетчера отказоустойчивости hello, hello центром сертификации, который управляет сведениями о службах.

### <a name="state"></a>Состояние
System.FM отчеты в виде ОК, когда была создана служба hello. Удаляет из хранилища работоспособности hello hello сущности при hello службы был удален.

* **SourceId**: System.FM.
* **Свойство**: State.

Hello пример hello события состояния службы hello **fabric: / WordCount/WordCountWebService**:

```powershell
PS C:\> Get-ServiceFabricServiceHealth fabric:/WordCount/WordCountWebService -ExcludeHealthStatistics


ServiceName           : fabric:/WordCount/WordCountWebService
AggregatedHealthState : Ok
PartitionHealthStates : 
                        PartitionId           : 8bbcd03a-3a53-47ec-a5f1-9b77f73c53b2
                        AggregatedHealthState : Ok
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 14
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/14/2017 4:55:10 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="service-correlation-error"></a>Ошибка сопоставления службы
**System.PLB** сообщает об ошибке, когда обнаруживает, что обновление toobe службы, связанной с другой службой создает цепочку сходства. Hello отчетов очищается, когда происходит успешное обновление.

* **SourceId**: System.PLB.
* **Свойство**: ServiceDescription.
* **Дальнейшие действия**: hello проверка коррелированных описания службы.

## <a name="partition-system-health-reports"></a>Системные отчеты о работоспособности разделов
**System.FM**, который представляет службу диспетчера отказоустойчивости hello, hello центром сертификации, который управляет сведениями о секциях службы.

### <a name="state"></a>Состояние
System.FM отчеты в виде ОК, если секция hello будет создана и находится в работоспособном состоянии. Удаляет из хранилища работоспособности hello hello сущности при hello секция, удаляется.

Если раздел hello ниже счетчик минимальное реплики hello, он сообщает об ошибке. Если секция hello не меньше минимального реплики счетчика hello, но находится ниже числа реплик целевых hello, он выводит предупреждение. Если раздел hello потери кворума, System.FM сообщает об ошибке.

Другие важные события включать предупреждение, когда перенастройки hello занимает больше времени, чем ожидалось, и если сборки hello занимает больше времени, чем ожидалось. Hello ожидаемого времени для построения hello и изменения конфигурации можно настроить на основе сценариев службы. Например если служба имеет терабайт данных состояния, таких как база данных SQL, требуется больше времени, чем для службы с помощью небольшого количества состояние сборки hello.

* **SourceId**: System.FM.
* **Свойство**: State.
* **Дальнейшие действия**: Если состояние работоспособности hello не ОК, все равно возможно, что некоторые реплики не были созданный opened и повышенным уровнем tooprimary или дополнительных правильно. Во многих случаях hello корневой причиной является ошибка в Привет открыть или изменить роль реализации службы.

Следующий пример Hello показано работоспособное секции:

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountWebService | Get-ServiceFabricPartitionHealth -ExcludeHealthStatistics -ReplicasFilter None

PartitionId           : 8bbcd03a-3a53-47ec-a5f1-9b77f73c53b2
AggregatedHealthState : Ok
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 70
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/14/2017 4:55:10 PM
                        TTL                   : Infinite
                        Description           : Partition is healthy.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

Hello пример hello состояние работоспособности раздела под счетчик целевой реплики. Hello следующим шагом является описание раздела tooget hello, которое показано, как настроить: **MinReplicaSetSize** , равно 3 и **TargetReplicaSetSize** — семь. Затем получите hello количество узлов в кластере hello: 5. Поэтому в этом случае две реплики нельзя разместить, поскольку hello целевое количество реплик больше, чем число узлов, доступных в hello.

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None -ExcludeHealthStatistics


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 123
                        SentAt                : 7/14/2017 4:55:39 PM
                        ReceivedAt            : 7/14/2017 4:55:44 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/S RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/P RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/14/2017 4:55:44 PM, LastOk = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131445250939703027
                        SentAt                : 7/14/2017 4:58:13 PM
                        ReceivedAt            : 7/14/2017 4:58:14 PM
                        TTL                   : 00:01:05
                        Description           : hello Load Balancer was unable toofind a placement for one or more of hello Service's Replicas:
                        Secondary replica could not be placed due toohello following constraints and properties:  
                        TargetReplicaSetSize: 7
                        Placement Constraint: N/A
                        Parent Service: N/A
                        
                        Constraint Elimination Sequence:
                        Existing Secondary Replicas eliminated 4 possible node(s) for placement -- 1/5 node(s) remain.
                        Existing Primary Replica eliminated 1 possible node(s) for placement -- 0/5 node(s) remain.
                        
                        Nodes Eliminated By Constraints:
                        
                        Existing Secondary Replicas -- Nodes with Partition's Existing Secondary Replicas/Instances:
                        --
                        FaultDomain:fd:/4 NodeName:_Node_4 NodeType:NodeType4 UpgradeDomain:4 UpgradeDomain: ud:/4 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/3 NodeName:_Node_3 NodeType:NodeType3 UpgradeDomain:3 UpgradeDomain: ud:/3 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/14/2017 4:56:14 PM, LastOk = 1/1/0001 12:00:00 AM

PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | select MinReplicaSetSize,TargetReplicaSetSize

MinReplicaSetSize TargetReplicaSetSize
----------------- --------------------
                2                    7                        

PS C:\> @(Get-ServiceFabricNode).Count
5
```

### <a name="replica-constraint-violation"></a>Нарушение ограничений в отношении реплик
**System.PLB** выдает предупреждение, если обнаруживает нарушение ограничений реплик и не может разместить все реплики секции. сведения об отчете Hello показывают, какие ограничения и свойства заблокируйте размещение реплики hello.

* **SourceId**: System.PLB.
* **Свойство**: начинается с **ReplicaConstraintViolation**.

## <a name="replica-system-health-reports"></a>Системные отчеты о работоспособности реплик
**System.RA**, который представляет компонента агента перенастройки hello, получает права hello состояние реплики hello.

### <a name="state"></a>Состояние
**System.RA** сообщает ОК после создания реплики hello.

* **SourceId**: System.RA.
* **Свойство**: State.

Следующий пример Hello показано работоспособности реплики.

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422293118721
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131445248920273536
                        SentAt                : 7/14/2017 4:54:52 PM
                        ReceivedAt            : 7/14/2017 4:55:13 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_0
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/14/2017 4:55:13 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="replica-open-status"></a>Состояние открытия реплики
Описание этого отчета о работоспособности Hello содержит время начала hello (время по Гринвичу), когда вызов hello API.

**System.RA** отображает предупреждение, если реплика Привет открыть выполняется дольше период hello настроен (по умолчанию: 30 минут). Если hello API влияет на доступность службы, hello отчета выдается гораздо быстрее (с заданным интервалом, значение по умолчанию 30 секунд). измеряется время Hello включает hello времени для репликации Привет открыть и откройте службу hello. Завершает изменения tooOK Hello свойство, если открыть hello.

* **SourceId**: System.RA.
* **Свойство**. **ReplicaOpenStatus**
* **Дальнейшие действия**: Если состояние работоспособности hello не ОК, изучить, почему реплики Привет открыть занимает длительное время.

### <a name="slow-service-api-call"></a>Медленный вызов API службы
**System.RAP** и **System.Replicator** выдать предупреждение, если код вызова пользовательского toohello службы занимает больше времени настройки hello. Предупреждение Hello очищается при завершении вызова hello.

* **SourceId**: System.RAP или System.Replicator.
* **Свойство**: hello имя hello медленно API. Описание Hello предоставляет дополнительные сведения о времени hello hello API был ожидание.
* **Дальнейшие действия**: изучить, почему вызов hello занимает длительное время.

Следующий пример Hello показывает секции в потери кворума, а toofigure действия выполнено исследование hello почему. Одна из реплик hello имеет состояние работоспособности предупреждения, чтобы получить его работоспособности. Он показывает, что операция службы hello занимает длительное время, при возникновении события, о которых сообщили System.RAP. После получения этих сведений hello следующим шагом является toolook в код службы hello и исследовать существует. В этом случае hello **RunAsync** реализации службы с отслеживанием состояния hello вызывает необработанное исключение. Hello реплик перезапуск, поэтому может не отображаться ни одной реплики в состояние предупреждения hello. Можно повторить попытку получения состояния работоспособности hello и искать любые различия в идентификаторе hello реплики. В некоторых случаях hello повторные попытки могут предоставить подсказки.

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful | Get-ServiceFabricPartitionHealth -ExcludeHealthStatistics

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
AggregatedHealthState : Error
UnhealthyEvaluations  :
                        Error event: SourceId='System.FM', Property='State'.

ReplicaHealthStates   :
                        ReplicaId             : 130743748372546446
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746168084332
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746195428808
                        AggregatedHealthState : Warning

                        ReplicaId             : 130743746195428807
                        AggregatedHealthState : Ok

HealthEvents          :
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Error
                        SequenceNumber        : 182
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:31 PM
                        TTL                   : Infinite
                        Description           : Partition is in quorum loss.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 4/24/2015 6:51:31 PM

PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful

PartitionId            : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
PartitionKind          : Int64Range
PartitionLowKey        : -9223372036854775808
PartitionHighKey       : 9223372036854775807
PartitionStatus        : InQuorumLoss
LastQuorumLossDuration : 00:00:13
MinReplicaSetSize      : 3
TargetReplicaSetSize   : 3
HealthState            : Error
DataLossNumber         : 130743746152927699
ConfigurationNumber    : 227633266688

PS C:\> Get-ServiceFabricReplica 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

ReplicaId           : 130743746195428808
ReplicaAddress      : PartitionId: 72a0fb3e-53ec-44f2-9983-2f272aca3e38, ReplicaId: 130743746195428808
ReplicaRole         : Primary
NodeName            : Node.3
ReplicaStatus       : Ready
LastInBuildDuration : 00:00:01
HealthState         : Warning

PS C:\> Get-ServiceFabricReplicaHealth 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
ReplicaId             : 130743746195428808
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.RAP', Property='ServiceOpenOperationDuration', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 130743756170185892
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:33 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/24/2015 7:00:33 PM

                        SourceId              : System.RAP
                        Property              : ServiceOpenOperationDuration
                        HealthState           : Warning
                        SequenceNumber        : 130743756399407044
                        SentAt                : 4/24/2015 7:00:39 PM
                        ReceivedAt            : 4/24/2015 7:00:59 PM
                        TTL                   : Infinite
                        Description           : Start Time (UTC): 2015-04-24 19:00:17.019
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Warning = 4/24/2015 7:00:59 PM
```

При запуске приложения неисправный hello отладчике hello события диагностики windows hello Показать hello исключение из RunAsync:

![События диагностики Visual Studio 2015: сбой RunAsync в fabric:/HelloWorldStatefulApplication.][1]

События диагностики Visual Studio 2015: сбой RunAsync в **fabric:/HelloWorldStatefulApplication**.

[1]: ./media/service-fabric-understand-and-troubleshoot-with-system-health-reports/servicefabric-health-vs-runasync-exception.png


### <a name="replication-queue-full"></a>Переполнение очереди репликации
**System.Replicator** отображает предупреждение, когда hello очередь репликации заполнена. На hello первичной репликации обычно заполнения очереди из-за одной или нескольких вторичных реплик tooacknowledge медленных операций. На вторичных hello обычно это происходит при медленных tooapply hello операций службы hello. Hello предупреждение будет удалено при hello очереди больше не заполнен.

* **SourceId**: System.Replicator.
* **Свойство**: **PrimaryReplicationQueueStatus** или **SecondaryReplicationQueueStatus**, в зависимости от роли реплики hello

### <a name="slow-naming-operations"></a>Медленные операции именования
**System.NamingService** сообщает о состоянии работоспособности первичной реплики, когда операция именования длится больше допустимого. Примеры операций именования — [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) и [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync). Дополнительные методы можно найти в статьях, посвященных FabricClient, например в статье о [методах управления службами](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) или [методах управления свойствами](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).

> [!NOTE]
> Hello службы именования разрешает расположение tooa имена службы в кластере hello и позволяет пользователям toomanage службы имена и свойства. Это секционированная материализованная служба Service Fabric. Один из разделов hello представляет hello Authority Owner, который содержит метаданные о все имена структуры службы и службы. Hello Service Fabric, называются сопоставленных toodifferent, вызывается секций имя владельца, поэтому служба hello является расширяемым. Узнайте больше о [службе именования](service-fabric-architecture.md).
> 
> 

При операции именование занимает больше времени, чем ожидалось, операция hello помечается отчет предупреждение на hello *первичная реплика hello упоминания служебного раздела служит hello операции*. После успешного выполнения операции hello hello предупреждение очищается. Если операция hello завершается с ошибкой, hello работоспособности отчет содержит подробные сведения об ошибке hello.

* **SourceId**: System.NamingService.
* **Свойство**: начинается с префикса **Duration_** и определяет медленной операцией hello и имя Service Fabric hello, на какие hello применяется операция. Например если создать службу на имя структуры: / MyApp/MyService занимает слишком много времени, свойство hello является Duration_AOCreateService.fabric:/MyApp/MyService. AO роль toohello точек hello именование разделов для этого имени и операции.
* **Дальнейшие действия**: Проверьте причину сбоя hello именование операции. Каждая операция может завершаться сбоем по различным причинам. Например, удаление службы может зависнуть на узле, поскольку ведущее приложение hello отслеживает аварийное завершение работы на узле из-за ошибки пользователя tooa в коде службы hello.

Следующий пример Hello показывает операции создания службы. Hello занимает дольше времени настройки hello. AO повторных попыток и отправляет tooNO работы. Нет завершенных hello последней операции с временем ожидания. В этом случае hello же реплики является основной для hello AO и ни одна роль.

```powershell
PartitionId           : 00000000-0000-0000-0000-000000001000
ReplicaId             : 131064359253133577
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.NamingService', Property='Duration_AOCreateService.fabric:/MyApp/MyService', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131064359308715535
                        SentAt                : 4/29/2016 8:38:50 PM
                        ReceivedAt            : 4/29/2016 8:39:08 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 4/29/2016 8:39:08 PM, LastWarning = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_AOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064359526778775
                        SentAt                : 4/29/2016 8:39:12 PM
                        ReceivedAt            : 4/29/2016 8:39:38 PM
                        TTL                   : 00:05:00
                        Description           : hello AOCreateService started at 2016-04-29 20:39:08.677 is taking longer than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_NOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064360657607311
                        SentAt                : 4/29/2016 8:41:05 PM
                        ReceivedAt            : 4/29/2016 8:41:08 PM
                        TTL                   : 00:00:15
                        Description           : hello NOCreateService started at 2016-04-29 20:39:08.689 completed with FABRIC_E_TIMEOUT in more than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM
```

## <a name="deployedapplication-system-health-reports"></a>Системные отчеты о работоспособности DeployedApplication
**System.Hosting** hello центром сертификации для развернутых сущностей.

### <a name="activation"></a>Активация
System.Hosting отчеты в виде ОК, если приложение успешно активирована на узле hello. В противном случае отображается сообщение об ошибке.

* **SourceId**: System.Hosting.
* **Свойство**: активации, включая версию выпуска hello
* **Дальнейшие действия**: Если именно отмечается неработоспособность приложения hello, изучить, почему не удалось активировать hello.

Hello ниже приведен пример успешной активации.

```powershell
PS C:\> Get-ServiceFabricDeployedApplicationHealth -NodeName _Node_1 -ApplicationName fabric:/WordCount -ExcludeHealthStatistics

ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_1
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_1
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131445249083836329
                                     SentAt                : 7/14/2017 4:55:08 PM
                                     ReceivedAt            : 7/14/2017 4:55:14 PM
                                     TTL                   : Infinite
                                     Description           : hello application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a>Загрузить
**System.Hosting** сообщает об ошибке в случае сбоя скачивания пакета приложения hello.

* **SourceId**: System.Hosting.
* **Property**: **Download:*версия_развертывания***
* **Дальнейшие действия**: изучить, почему не удалось загрузить hello на узле hello.

## <a name="deployedservicepackage-system-health-reports"></a>Системные отчеты о работоспособности DeployedServicePackage
**System.Hosting** hello центром сертификации для развернутых сущностей.

### <a name="service-package-activation"></a>Активация пакета службы
System.Hosting отчеты в виде ОК ли hello активации пакета службы на узле hello выполнена. В противном случае отображается сообщение об ошибке.

* **SourceId**: System.Hosting.
* **Property**: Activation.
* **Дальнейшие действия**: исследовании причин сбоя активации hello.

### <a name="code-package-activation"></a>Активация пакета кода
**System.Hosting** сообщает как "ОК" для каждого пакета кода при успешной активации hello. В случае сбоя активации hello отображает предупреждение, согласно настройкам. Если **CodePackage** сбоя tooactivate или завершается с ошибкой, больше, чем hello настроен **CodePackageHealthErrorThreshold**, размещение сообщает об ошибке. Если пакет службы содержит несколько пакетов кода, для каждого из них создается отчет об активации.

* **SourceId**: System.Hosting.
* **Свойство**: префикс hello использует **CodePackageActivation** и содержит имя пакета кода hello и точка входа hello как hello  **CodePackageActivation:* CodePackageName*:*SetupEntryPoint/EntryPoint*** (например, **CodePackageActivation:Code:SetupEntryPoint**)

### <a name="service-type-registration"></a>Регистрация типа службы
**System.Hosting** сообщает как "ОК", если тип службы hello Регистрация успешно завершена. Сообщение об ошибке, если регистрация hello не была выполнена вовремя (согласно настройке с помощью **ServiceTypeRegistrationTimeout**). Если среда выполнения hello закрыт, тип службы hello отменяется из узла "hello" и отображает предупреждение, размещения.

* **SourceId**: System.Hosting.
* **Свойство**: префикс hello использует **ServiceTypeRegistration** и содержит имя типа службы hello (например, **ServiceTypeRegistration:FileStoreServiceType**)

Привет, в следующем примере показан пакет работоспособности развернутой службы:

```powershell
PS C:\> Get-ServiceFabricDeployedServicePackageHealth -NodeName _Node_1 -ApplicationName fabric:/WordCount -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_1
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131445249084026346
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : hello ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131445249084306362
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : hello CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131445249088096842
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : hello ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a>Загрузить
**System.Hosting** сообщает об ошибке при сбое загрузки пакета службы hello.

* **SourceId**: System.Hosting.
* **Property**: **Download:*версия_развертывания***
* **Дальнейшие действия**: изучить, почему не удалось загрузить hello на узле hello.

### <a name="upgrade-validation"></a>Проверка обновления
**System.Hosting** сообщает об ошибке при сбое проверки во время обновления hello или hello обновление выполняется на узле hello.

* **SourceId**: System.Hosting.
* **Свойство**: префикс hello использует **FabricUpgradeValidation** и содержит версию обновления hello
* **Описание**: произошла ошибка toohello точек

## <a name="next-steps"></a>Дальнейшие действия
[Просмотр отчетов о работоспособности Service Fabric](service-fabric-view-entities-aggregated-health.md)

[Как tooreport и проверки службы работоспособности](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[Мониторинг и диагностика состояния служб в локальной среде разработки](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Обновление приложения Service Fabric](service-fabric-application-upgrade.md)

