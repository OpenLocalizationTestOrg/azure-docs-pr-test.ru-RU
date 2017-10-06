---
title: "Параметры ReliableDictionaryActorStateProvider aaaChange в Azure микрослужбами | Документы Microsoft"
description: "Узнайте о настройке субъектов Azure Service Fabric с отслеживанием состояния и типом ReliableDictionaryActorStateProvider."
services: Service-Fabric
documentationcenter: .net
author: sumukhs
manager: timlt
editor: 
ms.assetid: 79b48ffa-2474-4f1c-a857-3471f9590ded
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: sumukhs
ms.openlocfilehash: 44c85a41c90a17669ba874401d7921c94e7be9ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-reliable-actors--reliabledictionaryactorstateprovider"></a>Настройка надежных субъектов: ReliableDictionaryActorStateProvider
Конфигурация по умолчанию hello ReliableDictionaryActorStateProvider можно изменить, изменив файл settings.xml hello, созданный в корневом каталоге пакета Visual Studio hello в папке Config hello для указанного субъекта hello.

Среда выполнения Azure Service Fabric Hello ищет имена предопределенных разделов в файле settings.xml hello и использует значения конфигурации hello при создании hello базовые компоненты среды выполнения.

> [!NOTE]
> Сделать **не** удалять или изменять имена hello раздела конфигурации в файле settings.xml hello, создаваемого в решение Visual Studio hello hello.
> 
> 

Существуют также глобальные параметры, влияющие на конфигурацию ReliableDictionaryActorStateProvider hello.

## <a name="global-configuration"></a>Глобальная конфигурация
Глобальная конфигурация Hello указывается hello манифеста кластера для кластера hello в разделе KtlLogger hello. Он позволяет настраивать hello общего журнала расположение и размер, а также hello глобальной памяти ограничения используемых hello средства ведения журнала. Обратите внимание, что изменения в манифесте кластера hello влияет на все службы, использующие ReliableDictionaryActorStateProvider и надежных служб с отслеживанием состояния.

Hello манифеста кластера имеет один XML-файл, содержащий параметры и конфигурации, применяемые tooall узлов и служб в кластере hello. файл Hello обычно называется ClusterManifest.xml. Вы увидите hello манифеста кластера для кластера с помощью команды powershell Get-ServiceFabricClusterManifest hello.

### <a name="configuration-names"></a>Имена конфигураций
| Имя | Единица измерения | Значение по умолчанию | Примечания |
| --- | --- | --- | --- |
| WriteBufferMemoryPoolMinimumInKB |Килобайты |8388608 |Минимальное число tooallocate КБ в режиме ядра для ведения журнала hello записи памяти буферного пула. Этот пул памяти используется для кэширования сведений о состоянии перед записью toodisk. |
| WriteBufferMemoryPoolMaximumInKB |Килобайты |Без ограничений |Максимальный размер toowhich hello средства ведения журнала записи памяти буферный пул может увеличиваться. |
| SharedLogId |GUID |"" |Указывает уникальный идентификатор GUID toouse для идентификации hello общего файла журнала по умолчанию используется надежные службы на всех узлах в кластере hello, которые задают hello SharedLogId в их конкретной конфигурации службы. Если параметр SharedLogId задан, то также необходимо задать параметр SharedLogPath. |
| SharedLogPath |Полное имя пути |"" |Указывает полный путь hello, где hello совместно используемые все надежные службы на всех узлах в кластере hello, которые задают hello SharedLogPath в их конфигурации службы для конкретного файла журнала. Однако если параметр SharedLogPath задан, то также необходимо задать SharedLogId. |
| SharedLogSizeInMB |Мегабайты |8192 |Указывает номер hello МБ места на диске toostatically выделить для общего журнала hello. Hello значение должно быть 2048 или больше. |

### <a name="sample-cluster-manifest-section"></a>Образец раздела манифеста кластера
```xml
   <Section Name="KtlLogger">
     <Parameter Name="WriteBufferMemoryPoolMinimumInKB" Value="8192" />
     <Parameter Name="WriteBufferMemoryPoolMaximumInKB" Value="8192" />
     <Parameter Name="SharedLogId" Value="{7668BB54-FE9C-48ed-81AC-FF89E60ED2EF}"/>
     <Parameter Name="SharedLogPath" Value="f:\SharedLog.Log"/>
     <Parameter Name="SharedLogSizeInMB" Value="16383"/>
   </Section>
```

### <a name="remarks"></a>Примечания
средство ведения журнала Hello включает глобального пула памяти, выделенной из памяти невыгружаемый ядра, надежного обмена tooall доступны на узле для кэширования данных о состоянии перед записью toohello выделенной журналов, связанных с надежной службы реплики hello. размер пула Hello управляется hello WriteBufferMemoryPoolMinimumInKB и WriteBufferMemoryPoolMaximumInKB параметры. WriteBufferMemoryPoolMinimumInKB указывает оба hello начальный размер этого пула памяти и может сжать hello наименьший размер toowhich hello пула памяти. WriteBufferMemoryPoolMaximumInKB — hello наибольший размер toowhich hello пула памяти может увеличиваться. Каждой реплики надежной службы, открывающийся, могут увеличить размер hello hello пула памяти системы определить сумму, копирование tooWriteBufferMemoryPoolMaximumInKB. Если имеется несколько потребность в памяти из пула памяти hello, чем доступно, запросы памяти будет отложено до память доступна. Поэтому если пул памяти hello записи буфера слишком мал для определенной конфигурации затем может пострадать производительность.

Параметры SharedLogId и SharedLogPath Hello всегда используется совместно toodefine hello GUID и расположение по умолчанию hello общего журнала для всех узлов в кластере hello. общего журнала по умолчанию Hello используется для всех надежного служб, которые определяют параметры hello в settings.xml hello для конкретной службы hello. Для наилучшей производительности общие файлы журнала следует разместить на диски, которые используются исключительно для файла tooreduce hello общих состязания.

SharedLogSizeInMB указывает hello объем toopreallocate места на диске для общего журнала по умолчанию hello на всех узлах.  SharedLogId и SharedLogPath toobe заданы для указанного toobe SharedLogSizeInMB не требуется.

## <a name="replicator-security-configuration"></a>Конфигурация безопасности репликатора
Конфигурации безопасности репликации, используемых toosecure hello коммуникационный канал, используемый во время репликации. Это означает, службы не отображается трафик репликации друг друга, более безопасно обеспечение hello данные, это обеспечит высокую доступность.
По умолчанию пустой раздел конфигурации безопасности означает, что канал репликации не защищен.

### <a name="section-name"></a>Имя раздела
&lt;имя_субъекта&gt;ServiceReplicatorSecurityConfig

## <a name="replicator-configuration"></a>Конфигурация репликатора
Конфигурации репликации являются replicator hello используется tooconfigure, отвечающий за создание состояние поставщика состояния субъекта hello высокую степень доступности с помощью репликации и сохранение состояния hello локально.
Конфигурация по умолчанию Hello создается шаблоном Visual Studio hello и должно быть достаточно. Этот раздел рассказывает о Дополнительные настройки, доступные tootune hello репликатора.

### <a name="section-name"></a>Имя раздела
&lt;имя_субъекта&gt;ServiceReplicatorConfig

### <a name="configuration-names"></a>Имена конфигураций
| Имя | Единица измерения | Значение по умолчанию | Примечания |
| --- | --- | --- | --- |
| BatchAcknowledgementInterval |Секунды |0,015 |Период времени для репликатора какие hello во вторичной ожиданий hello после получения операции перед отправкой обратно подтверждения toohello первичного. Другие toobe подтверждений, отправленных для операций, обработанных в течение этого интервала отправляются как один ответ. |
| ReplicatorEndpoint |Недоступно |Значение по умолчанию не задано — обязательный параметр |IP-адрес и порт, который hello первичный или вторичный репликации будет использовать toocommunicate других Репликаторы в наборе реплик hello. Это должно указывать конечную точку TCP ресурса в манифест службы hello. См. слишком[ресурсов манифеста службы](service-fabric-service-manifest-resources.md) tooread Дополнительные об определении конечной точки ресурсы в манифест службы. |
| MaxReplicationMessageSize |Байты |50 MB |Максимальный размер данных репликации, которые могут быть переданы в одном сообщении. |
| MaxPrimaryReplicationQueueSize |Количество операций |8192 |Максимальное количество операций в основную очередь hello. Операция освобождается после первичной репликации hello не получит подтверждение от всех получателей Репликаторы hello. Это значение должно быть больше 64 и представлять собой степень числа 2. |
| MaxSecondaryReplicationQueueSize |Количество операций |16 384 |Максимальное количество операций в дополнительной очереди hello. Операция освобождается после того, как для ее состояния будет обеспечена высокая доступность посредством сохранения. Это значение должно быть больше 64 и представлять собой степень числа 2. |
| CheckpointThresholdInMB |МБ |200 |Объем свободного места файла журнала, после которого состояние hello создается контрольная точка. |
| MaxRecordSizeInKB |КБ |1024 |Максимальный размер записи hello репликации могут записывать в журнал hello. Это значение должно быть кратно 4 и больше 16. |
| OptimizeLogForLowerDiskUsage |Логический |Да |При значении true hello журнала настраивается, чтобы hello реплики выделенный файл журнала создается с помощью разреженный файл на томе NTFS. Это сокращает hello фактическое использование дискового пространства для файла hello. Если задано значение false, hello файл создается с предопределенной распределения, которые обеспечивают наилучшую производительность записи hello. |
| SharedLogId |GUID |"" |Указывает toouse уникальный идентификатор guid для идентификации файла журнала общего hello, используемый с данной репликой. Обычно этот параметр в службах не используется. Однако если параметр SharedLogId задан, то также необходимо задать SharedLogPath. |
| SharedLogPath |Полное имя пути |"" |Указывает полный путь hello, где будут создаваться hello общего файла журнала для этой реплики. Обычно этот параметр в службах не используется. Однако если параметр SharedLogPath задан, то также необходимо задать SharedLogId. |

## <a name="sample-configuration-file"></a>Образец файла конфигурации
```xml
<?xml version="1.0" encoding="utf-8"?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Section Name="MyActorServiceReplicatorConfig">
      <Parameter Name="ReplicatorEndpoint" Value="MyActorServiceReplicatorEndpoint" />
      <Parameter Name="BatchAcknowledgementInterval" Value="0.05"/>
      <Parameter Name="CheckpointThresholdInMB" Value="180" />
   </Section>
   <Section Name="MyActorServiceReplicatorSecurityConfig">
      <Parameter Name="CredentialType" Value="X509" />
      <Parameter Name="FindType" Value="FindByThumbprint" />
      <Parameter Name="FindValue" Value="9d c9 06 b1 69 dc 4f af fd 16 97 ac 78 1e 80 67 90 74 9d 2f" />
      <Parameter Name="StoreLocation" Value="LocalMachine" />
      <Parameter Name="StoreName" Value="My" />
      <Parameter Name="ProtectionLevel" Value="EncryptAndSign" />
      <Parameter Name="AllowedCommonNames" Value="My-Test-SAN1-Alice,My-Test-SAN1-Bob" />
   </Section>
</Settings>
```

## <a name="remarks"></a>Примечания
параметр BatchAcknowledgementInterval Hello управляет задержки репликации. Значение "0" приведет к hello самая низкая задержка, hello затрат пропускной способности (как дополнительные сообщения подтверждения должна отправляться и обработки, каждый из которых содержит меньшее число подтверждений).
Hello BatchAcknowledgementInterval, увеличьте значение hello hello выше hello общую пропускную способность репликации платы "hello" Высокая задержка операции. Это напрямую преобразуется toohello задержки фиксации транзакций.

Hello CheckpointThresholdInMB параметр элементы управления hello объем места на диске, hello replicator можно использовать сведения о состоянии toostore в файле выделенного журнала hello реплики. Увеличение tooa выше, чем по умолчанию hello может привести к сократить время изменения конфигурации, при добавлении новой реплики toohello набор. Это происходит из-за переноса состояния частичного toohello, который имеет место из-за доступности toohello дополнительные историю операций в журнале hello. Это потенциально может увеличить время восстановления hello реплики после сбоя.

Если задать OptimizeForLowerDiskUsage tootrue место в файле журнала будет являться избыточной так, что активные реплики можно сохранить Дополнительные сведения о состоянии в файлах журналов, пока неактивные реплики будет использовать меньше места на диске. В результате возможно toohost несколько реплик на узле. При установке OptimizeForLowerDiskUsage toofalse сведения о состоянии hello быстрее записывается toohello файлы журнала.

параметр MaxRecordSizeInKB Hello определяет hello максимальный размер записи, которая может быть написано с hello replicator в файл журнала hello. В большинстве случаев размер 1024 КБ записи по умолчанию hello является оптимальным. Тем не менее если служба hello вызывает больше данных элементов toobe часть сведений о состоянии hello, это значение может потребоваться toobe увеличивается. Нет мало пользы в принятии MaxRecordSizeInKB меньше 1024, как меньше записей, используйте только hello пространство, необходимое для записи меньше hello. Мы предполагаем, что это значение необходимо изменить только в редких случаях toobe.

Параметры SharedLogId и SharedLogPath Hello всегда являются используется совместно toomake службы, введите отдельные общего журнала из общего журнала по умолчанию hello hello узла. Для повышения эффективности работы столько службам следует указывать hello же общим журнала. Общие файлы журнала следует разместить на дисках, используемых исключительно для hello общего файла журнала, состязание скорость головки tooreduce. Мы предполагаем, что эти значения необходимо изменить только в редких случаях toobe.

