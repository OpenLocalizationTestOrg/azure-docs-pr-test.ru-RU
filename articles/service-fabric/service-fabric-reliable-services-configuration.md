---
title: "Надежные Azure микрослужбами aaaConfigure | Документы Microsoft"
description: "Сведения о настройке Reliable Services с отслеживанием состояния в Azure Service Fabric."
services: Service-Fabric
documentationcenter: .net
author: sumukhs
manager: timlt
editor: vturecek
ms.assetid: 9f72373d-31dd-41e3-8504-6e0320a11f0e
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: sumukhs
ms.openlocfilehash: 1e9c2890b62890a777561f25c04dc0fd11db9f1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-stateful-reliable-services"></a>Настройка надежных служб с отслеживанием состояния
Существует два набора параметров конфигурации для надежных служб. Один набор является глобальной для всех надежные службы в кластере hello при hello другой набор определенных tooa конкретной надежные службы.

## <a name="global-configuration"></a>Глобальная конфигурация
в манифесте кластера hello для кластера hello в разделе KtlLogger hello указана конфигурация глобальной службы надежного Hello. Он позволяет настраивать hello общего журнала расположение и размер, а также hello глобальной памяти ограничения используемых hello средства ведения журнала. Hello манифеста кластера имеет один XML-файл, содержащий параметры и конфигурации, применяемые tooall узлов и служб в кластере hello. файл Hello обычно называется ClusterManifest.xml. Вы увидите hello манифеста кластера для кластера с помощью команды powershell Get-ServiceFabricClusterManifest hello.

### <a name="configuration-names"></a>Имена конфигураций
| Имя | Единица измерения | Значение по умолчанию | Примечания |
| --- | --- | --- | --- |
| WriteBufferMemoryPoolMinimumInKB |Килобайты |8388608 |Минимальное число tooallocate КБ в режиме ядра для ведения журнала hello записи памяти буферного пула. Этот пул памяти используется для кэширования сведений о состоянии перед записью toodisk. |
| WriteBufferMemoryPoolMaximumInKB |Килобайты |Без ограничений |Максимальный размер toowhich hello средства ведения журнала записи памяти буферный пул может увеличиваться. |
| SharedLogId |GUID |"" |Указывает уникальный идентификатор GUID toouse для идентификации hello общего файла журнала по умолчанию используется надежные службы на всех узлах в кластере hello, которые задают hello SharedLogId в их конкретной конфигурации службы. Если параметр SharedLogId задан, то также необходимо задать параметр SharedLogPath. |
| SharedLogPath |Полное имя пути |"" |Указывает полный путь hello, где hello совместно используемые все надежные службы на всех узлах в кластере hello, которые задают hello SharedLogPath в их конфигурации службы для конкретного файла журнала. Однако если параметр SharedLogPath задан, то также необходимо задать SharedLogId. |
| SharedLogSizeInMB |Мегабайты |8192 |Указывает номер hello МБ места на диске toostatically выделить для общего журнала hello. Hello значение должно быть 2048 или больше. |

В Azure ARM или в шаблоне JSON локальной hello приведенном ниже примере показаны toochange hello hello общего журнала транзакций, которая возвращает созданные tooback коллекций надежных служб с отслеживанием состояния.

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="sample-local-developer-cluster-manifest-section"></a>Пример раздела манифеста кластера для локальной среды разработки
Если требуется toochange это в локальной среде разработки, необходим файл локального clustermanifest.xml tooedit hello.

```xml
   <Section Name="KtlLogger">
     <Parameter Name="SharedLogSizeInMB" Value="4096"/>
     <Parameter Name="WriteBufferMemoryPoolMinimumInKB" Value="8192" />
     <Parameter Name="WriteBufferMemoryPoolMaximumInKB" Value="8192" />
     <Parameter Name="SharedLogId" Value="{7668BB54-FE9C-48ed-81AC-FF89E60ED2EF}"/>
     <Parameter Name="SharedLogPath" Value="f:\SharedLog.Log"/>
   </Section>
```

### <a name="remarks"></a>Примечания
средство ведения журнала Hello включает глобального пула памяти, выделенной из памяти невыгружаемый ядра, надежного обмена tooall доступны на узле для кэширования данных о состоянии перед записью toohello выделенной журналов, связанных с надежной службы реплики hello. размер пула Hello управляется hello WriteBufferMemoryPoolMinimumInKB и WriteBufferMemoryPoolMaximumInKB параметры. WriteBufferMemoryPoolMinimumInKB указывает оба hello начальный размер этого пула памяти и может сжать hello наименьший размер toowhich hello пула памяти. WriteBufferMemoryPoolMaximumInKB — hello наибольший размер toowhich hello пула памяти может увеличиваться. Каждой реплики надежной службы, открывающийся, могут увеличить размер hello hello пула памяти системы определить сумму, копирование tooWriteBufferMemoryPoolMaximumInKB. Если имеется несколько потребность в памяти из пула памяти hello, чем доступно, запросы памяти будет отложено до память доступна. Поэтому если пул памяти hello записи буфера слишком мал для определенной конфигурации затем может пострадать производительность.

Параметры SharedLogId и SharedLogPath Hello всегда используется совместно toodefine hello GUID и расположение по умолчанию hello общего журнала для всех узлов в кластере hello. общего журнала по умолчанию Hello используется для всех надежного служб, которые определяют параметры hello в settings.xml hello для конкретной службы hello. Для наилучшей производительности общие файлы журнала следует разместить на диски, которые используются исключительно для файла tooreduce hello общих состязания.

SharedLogSizeInMB указывает hello объем toopreallocate места на диске для общего журнала по умолчанию hello на всех узлах.  SharedLogId и SharedLogPath toobe заданы для указанного toobe SharedLogSizeInMB не требуется.

## <a name="service-specific-configuration"></a>Конфигурация конкретной службы
Можно изменить конфигурации по умолчанию с отслеживанием состояния надежных служб с помощью пакета hello конфигурации (Config) или hello реализации службы (код).

* **Конфигурации** -конфигурации через пакет конфигурации hello выполняется путем изменения файла Settings.xml hello, создаваемого в корневом каталоге пакета Microsoft Visual Studio hello в папке Config hello для каждой службы в приложение hello.
* **Код** -конфигурации посредством кода выполняется путем создания ReliableStateManager, с помощью объекта ReliableStateManagerConfiguration с набором hello соответствующие параметры.

По умолчанию среда выполнения Azure Service Fabric hello ищет имена предопределенных разделов в файле Settings.xml hello и использует значения конфигурации hello при создании hello базовые компоненты среды выполнения.

> [!NOTE]
> Сделать **не** удалить имена hello раздела конфигурации в файле Settings.xml hello, создаются в решении Visual Studio hello в том случае, если не планируется tooconfigure службы через код hello.
> Переименование имена пакета или раздел конфигурации hello потребует изменения кода, при настройке hello ReliableStateManager.
> 
> 

### <a name="replicator-security-configuration"></a>Конфигурация безопасности репликатора
Конфигурации безопасности репликации, используемых toosecure hello коммуникационный канал, используемый во время репликации. Это означает, что службы не может toosee друг друга трафик репликации, обеспечивая hello данные, это обеспечит высокую доступность также защиты. По умолчанию пустой раздел конфигурации безопасности означает, что канал репликации не защищен.

### <a name="default-section-name"></a>Имя раздела по умолчанию
ReplicatorSecurityConfig

> [!NOTE]
> toochange имя раздела, ReliableStateManagerConfiguration переопределение hello replicatorSecuritySectionName параметр toohello конструктора при создании hello ReliableStateManager для этой службы.
> 
> 

### <a name="replicator-configuration"></a>Конфигурация репликатора
Конфигурации репликации настроить replicator hello, который отвечает за создание высоконадежными hello с отслеживанием состояния надежного состояние службы с помощью репликации и сохранение состояния hello локально.
Конфигурация по умолчанию Hello создается шаблоном Visual Studio hello и должно быть достаточно. Этот раздел рассказывает о Дополнительные настройки, доступные tootune hello репликатора.

### <a name="default-section-name"></a>Имя раздела по умолчанию
ReplicatorConfig

> [!NOTE]
> toochange имя раздела, ReliableStateManagerConfiguration переопределение hello replicatorSettingsSectionName параметр toohello конструктора при создании hello ReliableStateManager для этой службы.
> 
> 

### <a name="configuration-names"></a>Имена конфигураций
| Имя | Единица измерения | Значение по умолчанию | Примечания |
| --- | --- | --- | --- |
| BatchAcknowledgementInterval |Секунды |0,015 |Период времени для репликатора какие hello во вторичной ожиданий hello после получения операции перед отправкой обратно подтверждения toohello первичного. Другие toobe подтверждений, отправленных для операций, обработанных в течение этого интервала отправляются как один ответ. |
| ReplicatorEndpoint |Недоступно |Значение по умолчанию не задано — обязательный параметр |IP-адрес и порт, который hello первичный или вторичный репликации будет использовать toocommunicate других Репликаторы в наборе реплик hello. Это должно указывать конечную точку TCP ресурса в манифест службы hello. См. слишком[ресурсов манифеста службы](service-fabric-service-manifest-resources.md) tooread Дополнительные об определении конечной точки ресурсы в манифест службы. |
| MaxPrimaryReplicationQueueSize |Количество операций |8192 |Максимальное количество операций в основную очередь hello. Операция освобождается после первичной репликации hello не получит подтверждение от всех получателей Репликаторы hello. Это значение должно быть больше 64 и представлять собой степень числа 2. |
| MaxSecondaryReplicationQueueSize |Количество операций |16 384 |Максимальное количество операций в дополнительной очереди hello. Операция освобождается после того, как для ее состояния будет обеспечена высокая доступность посредством сохранения. Это значение должно быть больше 64 и представлять собой степень числа 2. |
| CheckpointThresholdInMB |МБ |50 |Объем свободного места файла журнала, после которого состояние hello создается контрольная точка. |
| MaxRecordSizeInKB |КБ |1024 |Максимальный размер записи hello репликации могут записывать в журнал hello. Это значение должно быть кратно 4 и больше 16. |
| MinLogSizeInMB |МБ |0 (определяется системой) |Минимальный размер журнала транзакций hello. Hello журнала не может tootruncate tooa размер меньше указанного значения. 0 указывает, что определит, что replicator hello hello минимальный размер журнала. Увеличение этого значения повышает вероятность hello сделать частичные копии и добавочное резервное копирование с момента подходящие записи журнала, усечение уменьшается вероятность. |
| TruncationThresholdFactor |Коэффициент |2 |Определяет, какие размера журнала hello, будут создаваться усечение. Пороговое значение усечения определяется произведением MinLogSizeInMB и TruncationThresholdFactor. Значение TruncationThresholdFactor должно быть больше 1. Значение MinLogSizeInMB * TruncationThresholdFactor должно быть меньше, чем MaxStreamSizeInMB. |
| ThrottlingThresholdFactor |Коэффициент |4. |Определяет, с какой размер журнала hello hello реплики начнется регулируется. Пороговое значение регулирования (в МБ) определяется по формуле Max((MinLogSizeInMB * ThrottlingThresholdFactor),(CheckpointThresholdInMB * ThrottlingThresholdFactor)). Пороговое значение регулирования (в МБ) должно быть больше порогового значения усечения (в МБ). Пороговое значение усечения (в МБ) должно быть меньше, чем MaxStreamSizeInMB. |
| MaxAccumulatedBackupLogSizeInMB |МБ |800 |Максимальный совокупный размер журналов архивации (в МБ) в заданной цепочке журналов архивации. Запросов добавочного резервного копирования завершится ошибкой, если добавочное резервное копирование hello, создает инструкцию backup log, приводящие к резервных копий журналов hello накапливаются с момента hello соответствующие полного резервного копирования toobe больше этого размера. В таких случаях пользователь является обязательным tootake полной резервной копии. |
| SharedLogId |GUID |"" |Указывает уникальный идентификатор GUID toouse для идентификации файла журнала общего hello, используемый с данной репликой. Обычно этот параметр в службах не используется. Однако если параметр SharedLogId задан, то также необходимо задать SharedLogPath. |
| SharedLogPath |Полное имя пути |"" |Указывает полный путь hello, где будут создаваться hello общего файла журнала для этой реплики. Обычно этот параметр в службах не используется. Однако если параметр SharedLogPath задан, то также необходимо задать SharedLogId. |
| SlowApiMonitoringDuration |Секунды |300 |Задает интервал для вызовов управляемого API мониторинга hello. Пример. Пользователь предоставил функцию обратного вызова резервной копии. По истечении интервала hello отчет о работоспособности предупреждение будет отправлено toohello диспетчера работоспособности. |

### <a name="sample-configuration-via-code"></a>Пример настройки с помощью кода
```csharp
class Program
{
    /// <summary>
    /// This is hello entry point of hello service host process.
    /// </summary>
    static void Main()
    {
        ServiceRuntime.RegisterServiceAsync("HelloWorldStatefulType",
            context => new HelloWorldStateful(context, 
                new ReliableStateManager(context, 
        new ReliableStateManagerConfiguration(
                        new ReliableStateManagerReplicatorSettings()
            {
                RetryInterval = TimeSpan.FromSeconds(3)
                        }
            )))).GetAwaiter().GetResult();
    }
}    
```
```csharp
class MyStatefulService : StatefulService
{
    public MyStatefulService(StatefulServiceContext context, IReliableStateManagerReplica stateManager)
        : base(context, stateManager)
    { }
    ...
}
```


### <a name="sample-configuration-file"></a>Образец файла конфигурации
```xml
<?xml version="1.0" encoding="utf-8"?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Section Name="ReplicatorConfig">
      <Parameter Name="ReplicatorEndpoint" Value="ReplicatorEndpoint" />
      <Parameter Name="BatchAcknowledgementInterval" Value="0.05"/>
      <Parameter Name="CheckpointThresholdInMB" Value="512" />
   </Section>
   <Section Name="ReplicatorSecurityConfig">
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


### <a name="remarks"></a>Примечания
Параметр BatchAcknowledgementInterval управляет задержкой репликации. Значение "0" приведет к hello самая низкая задержка, hello затрат пропускной способности (как дополнительные сообщения подтверждения должна отправляться и обработки, каждый из которых содержит меньшее число подтверждений).
Hello BatchAcknowledgementInterval, увеличьте значение hello hello выше hello общую пропускную способность репликации платы "hello" Высокая задержка операции. Это напрямую преобразуется toohello задержки фиксации транзакций.

значение Hello CheckpointThresholdInMB элементы управления hello объем места на диске, hello репликации можно использовать toostore сведения о состоянии в файле выделенного журнала hello реплики. Увеличение tooa выше, чем по умолчанию hello может привести к сократить время изменения конфигурации, при добавлении новой реплики toohello набор. Это происходит из-за переноса состояния частичного toohello, который имеет место из-за доступности toohello дополнительные историю операций в журнале hello. Это потенциально может увеличить время восстановления hello реплики после сбоя.

параметр MaxRecordSizeInKB Hello определяет hello максимальный размер записи, которая может быть написано с hello replicator в файл журнала hello. В большинстве случаев размер 1024 КБ записи по умолчанию hello является оптимальным. Тем не менее если служба hello вызывает больше данных элементов toobe часть сведений о состоянии hello, это значение может потребоваться toobe увеличивается. Нет мало пользы в принятии MaxRecordSizeInKB меньше 1024, как меньше записей, используйте только hello пространство, необходимое для записи меньше hello. Мы предполагаем, что это значение необходимо toobe колебаниями только в редких случаях.

Параметры SharedLogId и SharedLogPath Hello всегда являются используется совместно toomake службы, введите отдельные общего журнала из общего журнала по умолчанию hello hello узла. Для повышения эффективности работы столько службам следует указывать hello же общим журнала. Общие файлы журнала следует разместить на дисках, используемых исключительно для hello общего журнала файла tooreduce скорость головки конфликтов. Мы предполагаем, что это значение необходимо toobe колебаниями только в редких случаях.

## <a name="next-steps"></a>Дальнейшие действия
* [Отладка приложения Service Fabric с помощью Visual Studio](service-fabric-debugging-your-application.md)
* [Справочник разработчика по надежным службам](https://msdn.microsoft.com/library/azure/dn706529.aspx)

