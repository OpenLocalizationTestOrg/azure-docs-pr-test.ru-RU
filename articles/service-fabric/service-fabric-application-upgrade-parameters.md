---
title: "Обновление приложений: параметры обновления | Документация Майкрософт"
description: "Описывает tooupgrading связанные параметры приложения Service Fabric, включая работоспособности проверяет tooperform и политики tooautomatically отмены hello обновления."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: a4170ac6-192e-44a8-b93d-7e39c92a347e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: abd0ba48c223be9aa0909c7a0100ba5986430db3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="application-upgrade-parameters"></a>Параметры обновления приложений
В этой статье описывается обновление различные параметры, применяемые в процессе hello Azure Service Fabric приложения hello. Hello параметрам относятся hello имя и версия приложения hello. Они являются элементы, определяющие время ожидания hello и проверки работоспособности, которые применяются во время обновления hello и указывают hello политик, которые должны применяться при сбое обновления.

<br>

| Параметр | Описание |
| --- | --- |
| ApplicationName |Имя приложения hello, которая обновляется. Примеры: fabric:/VisualObjects, fabric:/ClusterMonitor. |
| TargetApplicationTypeVersion |Hello версия типа приложения hello hello обновления целевых объектов. |
| FailureAction |Hello действие, предпринимаемое Service Fabric при сбое обновления hello. приложение Hello может быть выполнен откат версии перед обновлением toohello (rollback) или hello обновления может быть остановлен в текущем домене обновления hello. В последнем случае hello режим обновления hello является также измененные tooManual. Допустимые значения этого свойства: Rollback (Откат) и Manual (Вручную). |
| HealthCheckWaitDurationSec |домен обновления hello завершится Hello toowait время (в секундах) после обновления hello перед Service Fabric дает hello работоспособности приложения hello. Это время также может рассматриваться как hello время приложения должна быть запущена, прежде чем его можно считать работоспособном состоянии. Если hello Проверка работоспособности проходит, процесс обновления hello переходит toohello следующий домен обновления.  При невозможности проверки работоспособности hello Service Fabric ожидает в течение интервала (hello UpgradeHealthCheckInterval) перед повторной попыткой проверки работоспособности hello до достижения HealthCheckRetryTimeout hello. по умолчанию Hello и рекомендуемое значение — 0 секунд. |
| HealthCheckRetryTimeoutSec |Длительность Hello (в секундах), Service Fabric по-прежнему tooperform оценки работоспособности перед объявлением hello обновления как сбойный. по умолчанию Hello составляет 600 секунд. Этот срок запускается после достижения конечного значения HealthCheckWaitDuration. В этом HealthCheckRetryTimeout Service Fabric может выполнять несколько проверок работоспособности приложения hello. значение по умолчанию Hello — 10 минут и должно быть настроено правильно для вашего приложения. |
| HealthCheckStableDurationSec |Hello tooverify продолжительность (в секундах), что приложение hello стабильна до перемещения toohello следующий домен обновления или завершения обновления "hello". Это время ожидания — используется tooprevent незаметно изменений состояния работоспособности сразу после выполнения проверки работоспособности hello. значение по умолчанию Hello — 120 секунд и должно быть настроено правильно для вашего приложения. |
| UpgradeDomainTimeoutSec |Максимальное время (в секундах) для обновления одного домена обновления. При достижении этого времени ожидания обновления hello останавливает и выполняется в зависимости от приветствия для UpgradeFailureAction. значение по умолчанию Hello никогда не равно (неограниченное) и должно быть настроено правильно для вашего приложения. |
| UpgradeTimeout |Значение времени ожидания (в секундах), применяется для обновления всей hello. При достижении этого времени ожидания hello обновление останавливается и инициируется UpgradeFailureAction. значение по умолчанию Hello никогда не равно (неограниченное) и должно быть настроено правильно для вашего приложения. |
| UpgradeHealthCheckInterval |частота Hello, проверяется состояние работоспособности hello. Этот параметр указан в hello ClusterManager раздел hello *кластера* *манифеста*и не указан как часть обновления командлет hello. значение по умолчанию Hello составляет 60 секунд. |

<br>

## <a name="service-health-evaluation-during-application-upgrade"></a>Оценка работоспособности службы во время обновления приложения
<br>
критерии оценки работоспособности Hello являются необязательными. Если при запуске обновления критериев оценки работоспособности hello не указаны, Service Fabric использует политики работоспособности приложения hello, указанный в hello ApplicationManifest.xml экземпляра приложения hello.

<br>

| Параметр | Описание |
| --- | --- |
| ConsiderWarningAsError |Значение по умолчанию — False. Обрабатывать события работоспособности hello предупреждения для приложения hello как ошибки при оценке работоспособности hello приложения hello во время обновления. По умолчанию Service Fabric оценивает предупреждение работоспособности события toobe сбоев (ошибки), поэтому hello обновление может продолжаться, даже если есть предупреждения. |
| MaxPercentUnhealthyDeployedApplications |По умолчанию и рекомендуемое значение — "0". Укажите максимальное число развернутых приложений hello (hello в разделе [работоспособности раздела](service-fabric-health-introduction.md)), можно иметь неработоспособное перед приложения hello считается нерабочей и происходит сбой hello обновления. Этот параметр определяет работоспособность приложения hello на узле hello и помогает обнаруживать проблемы во время обновления. Как правило реплики hello приложения hello получить балансировкой нагрузки toohello другой узел, позволяющий исправно, позволяя тем самым hello обновления tooproceed tooappear приложения hello. Указав strict работоспособности MaxPercentUnhealthyDeployedApplications, Service Fabric можно быстро обнаружить проблему с пакетом приложения hello и помочь в создании сбой быстрого обновления. |
| MaxPercentUnhealthyServices |По умолчанию и рекомендуемое значение — "0". Укажите максимальное количество hello служб в экземпляр приложения hello, которое может быть неработоспособен, прежде чем приложение hello считается неработоспособным и происходит сбой обновления hello. |
| MaxPercentUnhealthyPartitionsPerService |По умолчанию и рекомендуемое значение — "0". Укажите hello максимального количества секций в службе, можно иметь неработоспособное перед hello служба считается неработоспособным. |
| MaxPercentUnhealthyReplicasPerPartition |По умолчанию и рекомендуемое значение — "0". Укажите максимальное число реплик hello в секцию, которая может быть неисправное до раздела hello считается неработоспособным. |
| UpgradeReplicaSetCheckTimeout |**Службы без отслеживания состояния**--в одном домене обновления, Service Fabric пытается tooensure, что доступны дополнительные экземпляры службы hello. Если число экземпляров целевой hello более одного, Service Fabric ожидает в течение более одного экземпляра toobe, доступные значения tooa максимальное время ожидания. Это время ожидания задается с помощью свойства UpgradeReplicaSetCheckTimeout hello. По истечении времени ожидания hello Service Fabric выполняет обновление hello, независимо от того, hello количество экземпляров службы. Если число экземпляров целевой hello, Service Fabric не ждет, после чего сразу же выполняется с обновлением hello. **Службы с отслеживанием состояния**--в одном домене обновления, Service Fabric пытается tooensure, hello реплики набор имеет кворум. Service Fabric ожидает toobe кворума, доступные вверх tooa максимальное значение периода ожидания (указанного в свойстве UpgradeReplicaSetCheckTimeout hello). По истечении времени ожидания hello Service Fabric выполняет обновление hello, независимо от кворума. Этому параметру присваивается значение never (бесконечно) при накате и 900 секунд при откате. |
| ForceRestart |При обновлении конфигурации или пакет данных без обновления кода hello службы hello служба перезапускается, только если задано свойство ForceRestart hello tootrue. После завершения обновления hello Service Fabric уведомляет службу hello, доступен новый пакет конфигурации или пакет данных. Hello служба отвечает за применение изменений hello. При необходимости можно перезапустить службу hello сам. |

<br>
<br>
для типа службы для экземпляра приложения можно указать критерии MaxPercentUnhealthyServices, MaxPercentUnhealthyPartitionsPerService и MaxPercentUnhealthyReplicasPerPartition Hello. Установка этих параметров каждой службы позволяет для разных приложений-служб для toocontain типов с помощью различных оценки политик. Например, значения параметра MaxPercentUnhealthyPartitionsPerService для типов службы "шлюз без отслеживания состояния" и "механизм с отслеживанием состояния" могут отличаться для конкретного экземпляра приложения.

## <a name="next-steps"></a>Дальнейшие действия
[Руководство по обновлению приложений Service Fabric с помощью Visual Studio](service-fabric-application-upgrade-tutorial.md) поможет вам выполнить поэтапное обновление приложения с помощью Visual Studio.

[Обновление приложения с помощью PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) поможет вам выполнить обновление приложения с помощью PowerShell.

Статья [Управление приложением Azure Service Fabric с помощью интерфейса командной строки Azure Service Fabric](service-fabric-application-lifecycle-sfctl.md#upgrade-application) поможет вам выполнить обновление приложения с интерфейса командной строки Service Fabric.

[Обновление приложения с помощью подключаемого модуля Eclipse Service Fabric](service-fabric-get-started-eclipse.md#upgrade-your-service-fabric-java-application)

Обеспечить совместимость на обновление приложения путем изучения как toouse [сериализации данных](service-fabric-application-upgrade-data-serialization.md).

Узнайте, как toouse расширенные функции при обновлении приложения с помощью ссылки слишком[дополнительные разделы](service-fabric-application-upgrade-advanced.md).

Исправьте распространенных проблем в обновлений приложений с помощью ссылки действия toohello в [Устранение неполадок обновлений приложений](service-fabric-application-upgrade-troubleshooting.md).
