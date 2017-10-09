---
title: "обновление приложения aaaTroubleshooting | Документы Microsoft"
description: "В этой статье рассматриваются некоторых распространенных проблем при обновлении приложения Service Fabric и каким образом tooresolve их."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 19ad152e-ec50-4327-9f19-065c875c003c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 0f56fa61db9b4e32824623f162dc1bfe7fda0f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-application-upgrades"></a>Устранение неполадок при обновлениях приложений
В этой статье рассматриваются некоторые hello распространенных проблем при обновлении приложения Azure Service Fabric и каким образом tooresolve их.

## <a name="troubleshoot-a-failed-application-upgrade"></a>Устранение неполадок при неудачном обновлении приложения
При сбое обновления выходные данные hello hello **Get-ServiceFabricApplicationUpgrade** команда содержит дополнительные сведения для отладки сбоя hello.  Hello следующем списке указаны как можно использовать hello дополнительных сведений.

1. Определите тип сбоя hello.
2. Определите причину ошибки hello.
3. Изоляция одного или нескольких отказавших компонентов для дальнейшего исследования.

Эта информация доступна, когда Service Fabric обнаруживает сбой hello независимо от того, является ли hello **FailureAction** tooroll возвращаю или приостановить обновление hello.

### <a name="identify-hello-failure-type"></a>Определите тип сбоя hello
В выходных данных hello **Get-ServiceFabricApplicationUpgrade**, **FailureTimestampUtc** идентифицирует hello timestamp (в формате UTC), с которой была обнаружена ошибка обновления Service Fabric и  **FailureAction** было запущено. **Причина ошибки** определяет одну из трех высокоуровневые причины сбоя hello:

1. UpgradeDomainTimeout - указывает, что определенного домена обновления заняло слишком много времени toocomplete и **UpgradeDomainTimeout** срок действия истек.
2. OverallUpgradeTimeout - указывает, что hello в целом обновления заняло слишком длинный toocomplete и **UpgradeTimeout** срок действия истек.
3. Технологий - указывает, что после обновления домен обновления, приложение hello оставались неработоспособное в соответствии с toohello указан политики работоспособности и **HealthCheckRetryTimeout** срок действия истек.

Эти записи отображаются только в выходных данных hello при сбое обновления hello и запускается откат. Дополнительные сведения отображаются в зависимости от типа hello hello сбоя.

### <a name="investigate-upgrade-timeouts"></a>Исследование времени ожидания обновления
Сбои, связанные с истечением времени ожидания, чаще всего вызваны проблемами с доступностью служб. Hello выходных данных ниже типичен для обновления, где реплик службы или экземпляры ошибкой toostart в новой версии кода hello. Hello **UpgradeDomainProgressAtFailure** поле создает снимок все ожидающие обновления работы во время hello сбоя.

```
PS D:\temp> Get-ServiceFabricApplicationUpgrade fabric:/DemoApp

ApplicationName                : fabric:/DemoApp
ApplicationTypeName            : DemoAppType
TargetApplicationTypeVersion   : v2
ApplicationParameters          : {}
StartTimestampUtc              : 4/14/2015 9:26:38 PM
FailureTimestampUtc            : 4/14/2015 9:27:05 PM
FailureReason                  : UpgradeDomainTimeout
UpgradeDomainProgressAtFailure : MYUD1

                                 NodeName            : Node4
                                 UpgradePhase        : PostUpgradeSafetyCheck
                                 PendingSafetyChecks :
                                     WaitForPrimaryPlacement - PartitionId: 744c8d9f-1d26-417e-a60e-cd48f5c098f0

                                 NodeName            : Node1
                                 UpgradePhase        : PostUpgradeSafetyCheck
                                 PendingSafetyChecks :
                                     WaitForPrimaryPlacement - PartitionId: 4b43f4d8-b26b-424e-9307-7a7a62e79750
UpgradeState                   : RollingBackCompleted
UpgradeDuration                : 00:00:46
CurrentUpgradeDomainDuration   : 00:00:00
NextUpgradeDomain              :
UpgradeDomainsStatus           : { "MYUD1" = "Completed";
                                 "MYUD2" = "Completed";
                                 "MYUD3" = "Completed" }
UpgradeKind                    : Rolling
RollingUpgradeMode             : UnmonitoredAuto
ForceRestart                   : False
UpgradeReplicaSetCheckTimeout  : 00:00:00
```

В этом примере не удалось обновить hello в домене обновления *MYUD1* и двух секций (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* и *4b43f4d8-b26b-424e-9307-7a7a62e79750*) были затруднения. Hello секции были затруднения из-за выполнения hello невозможно tooplace основной реплики (*WaitForPrimaryPlacement*) на целевых узлах *Node1* и *Node4*.

Hello **Get ServiceFabricNode** команду можно использовать tooverify, эти два узла в домене обновления *MYUD1*. Hello *UpgradePhase* говорит *PostUpgradeSafetyCheck*, что означает, что эти проверки безопасности выполняются после завершения обновления всех узлов в домене обновления hello. Эта информация указывает tooa потенциальная проблема с новой версии кода приложения hello hello. Hello наиболее распространенных проблем, ошибки службы Привет открыть или пути кода tooprimary повышения роли.

*UpgradePhase* из *PreUpgradeSafetyCheck* означает возникли проблемы, подготовка домена обновления hello, прежде чем она была проведена. в этом случае Hello наиболее распространенных проблем являются ошибки службы закройте hello или понижения роли из путей основного кода.

Hello текущей **UpgradeState** — *RollingBackCompleted*, поэтому hello исходное обновление должно быть выполнено с помощью отката **FailureAction**, который автоматически откат обновления hello после сбоя. Если было выполнено обновление исходного hello с ручной **FailureAction**, то обновление hello вместо этого будет в приостановленном состоянии tooallow динамической отладки приложения hello.

### <a name="investigate-health-check-failures"></a>Исследование ошибок проверки работоспособности
Сбои проверки работоспособности могут быть вызваны различными ошибками, которые могут возникать после того, как обновление будет завершено во всех узлах в домене обновления при успешном выполнении всех проверок безопасности. выходные данные Hello ниже типичен для сбоя обновления из-за проверок работоспособности toofailed. Hello **UnhealthyEvaluations** поле создает снимок проверку работоспособности, не прошедшие во время hello hello обновления в соответствии с toohello указан [политики работоспособности](service-fabric-health-introduction.md).

```
PS D:\temp> Get-ServiceFabricApplicationUpgrade fabric:/DemoApp

ApplicationName                         : fabric:/DemoApp
ApplicationTypeName                     : DemoAppType
TargetApplicationTypeVersion            : v4
ApplicationParameters                   : {}
StartTimestampUtc                       : 4/24/2015 2:42:31 AM
UpgradeState                            : RollingForwardPending
UpgradeDuration                         : 00:00:27
CurrentUpgradeDomainDuration            : 00:00:27
NextUpgradeDomain                       : MYUD2
UpgradeDomainsStatus                    : { "MYUD1" = "Completed";
                                          "MYUD2" = "Pending";
                                          "MYUD3" = "Pending" }
UnhealthyEvaluations                    :
                                          Unhealthy services: 50% (2/4), ServiceType='PersistedServiceType', MaxPercentUnhealthyServices=0%.

                                          Unhealthy service: ServiceName='fabric:/DemoApp/Svc3', AggregatedHealthState='Error'.

                                              Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                              Unhealthy partition: PartitionId='3a9911f6-a2e5-452d-89a8-09271e7e49a8', AggregatedHealthState='Error'.

                                                  Error event: SourceId='Replica', Property='InjectedFault'.

                                          Unhealthy service: ServiceName='fabric:/DemoApp/Svc2', AggregatedHealthState='Error'.

                                              Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                              Unhealthy partition: PartitionId='744c8d9f-1d26-417e-a60e-cd48f5c098f0', AggregatedHealthState='Error'.

                                                  Error event: SourceId='Replica', Property='InjectedFault'.

UpgradeKind                             : Rolling
RollingUpgradeMode                      : Monitored
FailureAction                           : Manual
ForceRestart                            : False
UpgradeReplicaSetCheckTimeout           : 49710.06:28:15
HealthCheckWaitDuration                 : 00:00:00
HealthCheckStableDuration               : 00:00:10
HealthCheckRetryTimeout                 : 00:00:10
UpgradeDomainTimeout                    : 10675199.02:48:05.4775807
UpgradeTimeout                          : 10675199.02:48:05.4775807
ConsiderWarningAsError                  :
MaxPercentUnhealthyPartitionsPerService :
MaxPercentUnhealthyReplicasPerPartition :
MaxPercentUnhealthyServices             :
MaxPercentUnhealthyDeployedApplications :
ServiceTypeHealthPolicyMap              :
```

Сначала исследование ошибок проверки работоспособности требует понимания модель работоспособности Service Fabric hello. Но даже без таких глубокое понимание, мы видим, что две службы находятся в неработоспособном состоянии: *fabric: / DemoApp/Svc3* и *fabric: / DemoApp/Svc2*, вместе с отчеты о работоспособности ошибки hello («InjectedFault «в данном случае). В этом примере два из четырех служб находятся в неработоспособном состоянии, это меньше целевой объект по умолчанию hello 0% неработоспособное (*MaxPercentUnhealthyServices*).

Hello обновление было приостановлено после сбоя, указав **FailureAction** Если ручной запуск hello обновления. Этот режим позволяет нам tooinvestigate hello динамической системы в состоянии hello не удалось выполнить перед переводом никаких дальнейших действий.

### <a name="recover-from-a-suspended-upgrade"></a>Восстановление при приостановке обновления
С помощью отката **FailureAction**, нет, восстановление не требуется, так как обновление hello автоматический откат после сбоя. При установке действия **FailureAction**, выполняемого вручную, существует несколько вариантов восстановления.

1.  Запуск отката.
2. Пройдите оставшуюся hello hello обновления вручную
3. Возобновить hello отслеживать обновления

Hello **ServiceFabricApplicationRollback начала** команда может применяться в любое время toostart откат приложения hello. После hello команда возвращает успешно, запрос отката hello был зарегистрирован в системе hello и вскоре после этого запускает.

Hello **командлет Resume-ServiceFabricApplicationUpgrade** можно использовать команду tooproceed через hello оставшуюся часть hello обновление вручную, один домен обновления одновременно. В этом режиме проверки безопасности только выполняемых системой hello. Никаких дополнительных проверок работоспособности выполняться не будет. Эта команда может использоваться, только когда hello *UpgradeState* показывает *RollingForwardPending*, что означает, что текущий домен обновления hello закончила обновление, но hello Далее она не запущена (ожидание).

Hello **ServiceFabricApplicationUpgrade обновление** команда может быть используется tooresume hello отслеживаемых проверок безопасности и работоспособности выполнить обновление.

```
PS D:\temp> Update-ServiceFabricApplicationUpgrade fabric:/DemoApp -UpgradeMode Monitored

UpgradeMode                             : Monitored
ForceRestart                            :
UpgradeReplicaSetCheckTimeout           :
FailureAction                           :
HealthCheckWaitDuration                 :
HealthCheckStableDuration               :
HealthCheckRetryTimeout                 :
UpgradeTimeout                          :
UpgradeDomainTimeout                    :
ConsiderWarningAsError                  :
MaxPercentUnhealthyPartitionsPerService :
MaxPercentUnhealthyReplicasPerPartition :
MaxPercentUnhealthyServices             :
MaxPercentUnhealthyDeployedApplications :
ServiceTypeHealthPolicyMap              :

PS D:\temp>
```

Обновление Hello продолжается с домен обновления hello, где оно было приостановлено и используйте hello же обновления параметры и политики работоспособности как перед. При необходимости, все обновления параметров hello и политики работоспособности, показано в предшествующих выходных данных hello может изменяться в hello же команды при возобновлении hello обновления. В этом примере обновление hello возобновлен в режиме отслеживаемое с параметрами hello и политики работоспособности hello без изменений.

## <a name="further-troubleshooting"></a>Дальнейшее устранение неполадок
### <a name="service-fabric-is-not-following-hello-specified-health-policies"></a>Service Fabric не подписан hello указан политики работоспособности
Возможная причина 1.

Service Fabric преобразует все проценты в фактическое число сущностей (например, реплики, секций и службы) для оценки работоспособности и всегда округляет toowhole сущностей. Например, если hello максимальное *MaxPercentUnhealthyReplicasPerPartition* % 21 и есть пяти реплик, то Service Fabric позволяет вверх tootwo неработоспособных реплик (то есть,`Math.Ceiling (5*0.21)`). Поэтому политики работоспособности должны быть настроены с учетом этого.

Возможная причина 2.

Политики работоспособности указываются в процентах от общего числа служб, а не в конкретных экземплярах служб. Например, перед обновлением, если приложение имеет четыре экземпляров A, B, C и D, службы, где службы D находится в неработоспособном состоянии, но с прямым toohello приложения. Мы хотим известные неработоспособности службы D hello обновления и установите параметр hello tooignore *MaxPercentUnhealthyServices* toobe 25%, при условии, что только A, B и C должны toobe работоспособном состоянии.

Тем не менее во время обновления hello D могут стать работоспособное при C переходит в неработоспособное. Обновление Hello по-прежнему пройдет успешно, так как только 25% hello службы находятся в неработоспособном состоянии. Тем не менее это может привести в непредвиденных ошибок из-за которой tooC неожиданно неработоспособное вместо г. В этом случае D должен моделироваться типом другую службу из A, B и C. Так как политики работоспособности указаны каждого типа службы, другой неработоспособное процент пороговые значения можно примененных toodifferent служб. 

### <a name="i-did-not-specify-a-health-policy-for-application-upgrade-but-hello-upgrade-still-fails-for-some-time-outs-that-i-never-specified"></a>Я не указан в политике работоспособности для обновления приложения, но hello по-прежнему произошел сбой при обновлении некоторые значения времени ожидания, которые никогда не указаны
Если политики работоспособности не предоставлен запрос на обновление toohello, они берутся из hello *ApplicationManifest.xml* hello текущей версии приложения. Например при обновлении приложения X из версии 1.0 tooversion 2.0 используются политики работоспособности приложения, указанное для версии 1.0. Если политика работоспособности различных должен использоваться для обновления hello, политики hello должен toobe, заданный как часть вызова API обновления приложения hello. политики Hello, заданный как часть вызова hello API применяются только во время обновления hello. После завершения обновления hello hello политики, указанный в hello *ApplicationManifest.xml* используются.

### <a name="incorrect-time-outs-are-specified"></a>Указаны неверные значения времени ожидания
Полагаю, вам интересно, что произойдет, если задать несогласованные значения времени ожидания. Например, возможно, *UpgradeTimeout* , меньше, чем hello *UpgradeDomainTimeout*. Hello ответов — возвращает ошибку. Ошибки возвращаются в том случае, если hello *UpgradeDomainTimeout* меньше, чем сумма hello *HealthCheckWaitDuration* и *HealthCheckRetryTimeout*, или если  *UpgradeDomainTimeout* меньше, чем сумма hello *HealthCheckWaitDuration* и *HealthCheckStableDuration*.

### <a name="my-upgrades-are-taking-too-long"></a>Мои обновления выполняются слишком долго
время Hello toocomplete обновления зависит от того, проверки работоспособности hello и указанного значения времени ожидания. Проверки работоспособности и значения времени ожидания зависят от того, как долго toocopy, развертывание и стабилизация приложения hello. Слишком жесткое назначение времени ожидания может привести к большему числу сбоев при обновлении, поэтому при назначении значений времени ожидания рекомендуется консервативный подход.

Вот на взаимодействие с времени обновления hello тайм-ауты hello быстрое обновление.

Обновления для домена обновления не могут завершиться быстрее, чем сумма значений параметров *HealthCheckWaitDuration* + *HealthCheckStableDuration*.

Сбой обновления не может произойти быстрее, чем сумма значений *HealthCheckWaitDuration* + *HealthCheckRetryTimeout*.

Hello время обновления для обновления домена ограничивается *UpgradeDomainTimeout*.  Если *HealthCheckRetryTimeout* и *HealthCheckStableDuration* оба не равны нулю и hello работоспособности приложения hello отслеживает переключение вперед и назад, то обновление hello произойдет тайм-аут на  *UpgradeDomainTimeout*. *UpgradeDomainTimeout* начинается отсчет один раз hello обновления для текущего домена обновления hello начинается.

## <a name="next-steps"></a>Дальнейшие действия
[Руководство по обновлению приложений Service Fabric с помощью Visual Studio](service-fabric-application-upgrade-tutorial.md) поможет вам выполнить поэтапное обновление приложения с помощью Visual Studio.

[Обновление приложения с помощью PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) поможет вам выполнить обновление приложения с помощью PowerShell.

Управление обновлениями приложения осуществляется с помощью [параметров обновления](service-fabric-application-upgrade-parameters.md).

Обеспечить совместимость на обновление приложения путем изучения как toouse [сериализации данных](service-fabric-application-upgrade-data-serialization.md).

Узнайте, как toouse расширенные функции при обновлении приложения с помощью ссылки слишком[дополнительные разделы](service-fabric-application-upgrade-advanced.md).
