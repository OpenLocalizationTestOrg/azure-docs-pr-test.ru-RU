---
title: "Изменение параметров KVSActorStateProvider в микрослужбах Azure | Документация Майкрософт"
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
ms.date: 10/2/2017
ms.author: sumukhs
ms.openlocfilehash: d3424aa7a8e0f6011bbef4aa61274c1f598f5c86
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="configuring-reliable-actors--kvsactorstateprovider"></a>Настройка надежных субъектов — KVSActorStateProvider
Используемую по умолчанию конфигурацию KVSActorStateProvider можно изменить. Для этого нужно обновить файл settings.xml, созданный в папке Config заданного субъекта в корневом каталоге пакета Microsoft Visual Studio.

Среда выполнения Azure Service Fabric ищет предварительно заданные имена разделов в файле settings.xml, использует значения параметров конфигурации и создает базовые компоненты среды выполнения.

> [!NOTE]
> **Не** удаляйте и не изменяйте имена разделов в перечисленных ниже конфигурациях в файле settings.xml, который создается в решении Visual Studio.
> 
> 

## <a name="replicator-security-configuration"></a>Конфигурация безопасности репликатора
Конфигурации безопасности репликаторов используются для защиты канала связи, который используется во время репликации. Это означает, что службы не будут "видеть" реплицируемый трафик друг друга, что позволит обеспечить высокую доступность и высокий уровень защиты.
По умолчанию пустой раздел конфигурации безопасности означает, что канал репликации не защищен.

### <a name="section-name"></a>Имя раздела
&lt;имя_субъекта&gt;ServiceReplicatorSecurityConfig

## <a name="replicator-configuration"></a>Конфигурация репликатора
Конфигурации репликатора используются для настройки репликатора, отвечающего за надежность состояний поставщика состояний субъекта.
Конфигурация по умолчанию создается шаблоном Visual Studio и подходит для большинства случаев. В этом разделе мы расскажем о дополнительных конфигурациях, с помощью которых можно выполнить более тонкую настройку репликатора.

### <a name="section-name"></a>Имя раздела
&lt;имя_субъекта&gt;ServiceReplicatorConfig

### <a name="configuration-names"></a>Имена конфигураций
| Имя | Единица измерения | Значение по умолчанию | Примечания |
| --- | --- | --- | --- |
| BatchAcknowledgementInterval |Секунды |0,015 |Период времени, в течение которого дополнительный репликатор после получения операции находится в режиме ожидания, а затем отправляет подтверждение обратно основному репликатору. Любые другие подтверждения, отправляемые для операций, обработанных в течение этого интервала, отправляются как один ответ. |
| ReplicatorEndpoint |Недоступно |Значение по умолчанию не задано — обязательный параметр |IP-адрес и порт, которые будут использоваться основным и дополнительным репликаторами для связи с другими репликаторами в наборе реплик. Значение должно быть ссылкой на конечную точку ресурса TCP в манифесте службы. Дополнительные сведения об определении ресурсов конечных точек в манифесте службы см. в статье [Указание ресурсов в манифесте службы](service-fabric-service-manifest-resources.md). |
| RetryInterval |Секунды |5 |Период времени, после которого репликатор повторно передает сообщение, если не получил подтверждение операции. |
| MaxReplicationMessageSize |Байты |50 MB |Максимальный размер данных репликации, которые могут быть переданы в одном сообщении. |
| MaxPrimaryReplicationQueueSize |Количество операций |1024 |Максимальное количество операций в основной очереди. Операция освобождается после того, как основной репликатор получит подтверждение от всех дополнительных репликаторов. Это значение должно быть больше 64 и представлять собой степень числа 2. |
| MaxSecondaryReplicationQueueSize |Количество операций |2048 |Максимальное количество операций в дополнительной очереди. Операция освобождается после того, как для ее состояния будет обеспечена высокая доступность посредством сохранения. Это значение должно быть больше 64 и представлять собой степень числа 2. |

## <a name="store-configuration"></a>Конфигурация хранилища
Конфигурации хранилища используются для настройки локального хранилища, используемого для хранения реплицируемого состояния.
Конфигурация по умолчанию создается шаблоном Visual Studio и подходит для большинства случаев. В этом разделе рассматриваются дополнительные конфигурации локального хранилища.

### <a name="section-name"></a>Имя раздела
&lt;имя_субъекта&gt;ServiceLocalStoreConfig

### <a name="configuration-names"></a>Имена конфигураций
| Имя | Единица измерения | Значение по умолчанию | Примечания |
| --- | --- | --- | --- |
| MaxAsyncCommitDelayInMilliseconds |Миллисекунды |200 |Задает максимальный интервал для устойчивой пакетной фиксации в локальном хранилище. |
| MaxVerPages |Количество страниц |16 384 |Максимальное количество страниц версий в базе данных локального хранилища. Определяет максимальное число необработанных транзакций. |

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
Параметр BatchAcknowledgementInterval управляет задержкой репликации. Значение 0 обеспечивает минимальную возможную задержку за счет уменьшения скорости репликации (потому что необходимо отправлять и обрабатывать большее количество сообщений с подтверждениями, каждое из которых содержит меньше подтверждений).
По мере увеличения значения BatchAcknowledgementInterval увеличивается общая скорость репликации и задержка операций. Это непосредственно перетекает в задержку фиксаций транзакций.

