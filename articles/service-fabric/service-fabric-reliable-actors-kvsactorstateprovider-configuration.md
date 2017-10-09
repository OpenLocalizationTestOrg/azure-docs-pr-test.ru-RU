---
title: "Параметры KVSActorStateProvider aaaChange в Azure микрослужбами | Документы Microsoft"
description: "Сведения о настройке субъектов Azure Service Fabric с отслеживанием состояния и типом KVSActorStateProvider."
services: Service-Fabric
documentationcenter: .net
author: sumukhs
manager: timlt
editor: 
ms.assetid: dbed72f4-dda5-4287-bd56-da492710cd96
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: sumukhs
ms.openlocfilehash: e003512678556e68a8926b1b9c6c28d9ae3979d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-reliable-actors--kvsactorstateprovider"></a>Настройка надежных субъектов — KVSActorStateProvider
Конфигурация по умолчанию hello KVSActorStateProvider можно изменить, изменив файл settings.xml hello, созданный в корневом каталоге пакета Microsoft Visual Studio hello в папке Config hello для указанного субъекта hello.

Среда выполнения Azure Service Fabric Hello ищет имена предопределенных разделов в файле settings.xml hello и использует значения конфигурации hello при создании hello базовые компоненты среды выполнения.

> [!NOTE]
> Сделать **не** удалять или изменять имена hello раздела конфигурации в файле settings.xml hello, создаваемого в решение Visual Studio hello hello.
> 
> 

## <a name="replicator-security-configuration"></a>Конфигурация безопасности репликатора
Конфигурации безопасности репликации, используемых toosecure hello коммуникационный канал, используемый во время репликации. Это означает, что службы не может видеть друг друга трафик репликации, обеспечивая также безопасные данные hello, это обеспечит высокую доступность.
По умолчанию пустой раздел конфигурации безопасности означает, что канал репликации не защищен.

### <a name="section-name"></a>Имя раздела
&lt;имя_субъекта&gt;ServiceReplicatorSecurityConfig

## <a name="replicator-configuration"></a>Конфигурация репликатора
Конфигурации репликации настроить hello репликации, который отвечает за установку состояния поставщик состояния субъекта hello высокую степень доступности.
Конфигурация по умолчанию Hello создается шаблоном Visual Studio hello и должно быть достаточно. Этот раздел рассказывает о Дополнительные настройки, доступные tootune hello репликатора.

### <a name="section-name"></a>Имя раздела
&lt;имя_субъекта&gt;ServiceReplicatorConfig

### <a name="configuration-names"></a>Имена конфигураций
| Имя | Единица измерения | Значение по умолчанию | Примечания |
| --- | --- | --- | --- |
| BatchAcknowledgementInterval |Секунды |0,015 |Период времени для репликатора какие hello во вторичной ожиданий hello после получения операции перед отправкой обратно подтверждения toohello первичного. Другие toobe подтверждений, отправленных для операций, обработанных в течение этого интервала отправляются как один ответ. |
| ReplicatorEndpoint |Недоступно |Значение по умолчанию не задано — обязательный параметр |IP-адрес и порт, который hello первичный или вторичный репликации будет использовать toocommunicate других Репликаторы в наборе реплик hello. Это должно указывать конечную точку TCP ресурса в манифест службы hello. См. слишком[ресурсов манифеста службы](service-fabric-service-manifest-resources.md) tooread Дополнительные об определении конечной точки ресурсы в манифест службы hello. |
| RetryInterval |Секунды |5 |Период времени, после которого hello replicator повторно передает сообщение, если он не получил подтверждения для операции. |
| MaxReplicationMessageSize |Байты |50 MB |Максимальный размер данных репликации, которые могут быть переданы в одном сообщении. |
| MaxPrimaryReplicationQueueSize |Количество операций |1024 |Максимальное количество операций в основную очередь hello. Операция освобождается после первичной репликации hello не получит подтверждение от всех получателей Репликаторы hello. Это значение должно быть больше 64 и представлять собой степень числа 2. |
| MaxSecondaryReplicationQueueSize |Количество операций |2048 |Максимальное количество операций в дополнительной очереди hello. Операция освобождается после того, как для ее состояния будет обеспечена высокая доступность посредством сохранения. Это значение должно быть больше 64 и представлять собой степень числа 2. |

## <a name="store-configuration"></a>Конфигурация хранилища
Хранилище конфигураций, используемых tooconfigure hello локальное хранилище находится в состоянии hello используется toopersist, которая реплицируется.
Конфигурация по умолчанию Hello создается шаблоном Visual Studio hello и должно быть достаточно. Этот раздел рассказывает о Дополнительные настройки, доступные tootune hello локального хранилища.

### <a name="section-name"></a>Имя раздела
&lt;имя_субъекта&gt;ServiceLocalStoreConfig

### <a name="configuration-names"></a>Имена конфигураций
| Имя | Единица измерения | Значение по умолчанию | Примечания |
| --- | --- | --- | --- |
| MaxAsyncCommitDelayInMilliseconds |Миллисекунды |200 |Задает максимально hello интервал для фиксации устойчивых локальное хранилище пакетов. |
| MaxVerPages |Количество страниц |16 384 |Максимальное количество страниц версий в локальном hello Hello хранения базы данных. Он определяет максимальное число необработанных транзакций hello. |

## <a name="sample-configuration-file"></a>Образец файла конфигурации
```xml
<?xml version="1.0" encoding="utf-8"?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Section Name="MyActorServiceReplicatorConfig">
      <Parameter Name="ReplicatorEndpoint" Value="MyActorServiceReplicatorEndpoint" />
      <Parameter Name="BatchAcknowledgementInterval" Value="0.05"/>
   </Section>
   <Section Name="MyActorServiceLocalStoreConfig">
      <Parameter Name="MaxVerPages" Value="8192" />
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

