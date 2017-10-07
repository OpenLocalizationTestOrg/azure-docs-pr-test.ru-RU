---
title: "aaaAdd пользовательские отчеты о работоспособности Service Fabric | Документы Microsoft"
description: "Описывает, как отчеты о работоспособности пользовательских toosend tooAzure Service Fabric работоспособные сущности. Здесь собраны рекомендации по разработке и реализации качественных отчетов о работоспособности."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: 0a00a7d2-510e-47d0-8aa8-24c851ea847f
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: oanapl
ms.openlocfilehash: 12c9f664e2a457b4e1e8f340873ca60ebcefb097
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-service-fabric-health-reports"></a>Добавление настраиваемых отчетов о работоспособности Service Fabric
Представляет Azure Service Fabric [модель работоспособности](service-fabric-health-introduction.md) tooflag неработоспособное кластера и условия приложения для конкретных объектов. использует модель работоспособности Hello **работоспособности "создатели отчетов"** (компоненты системы и watchdogs). Задача Hello — простой и быстрой диагностики и восстановления. Записи с помощью службы должны заранее toothink о работоспособности. Любое условие, которое может повлиять на работоспособность должны создаваться отчеты, особенно в том случае, если он может помочь флаг проблемы закройте toohello корневой. сведения о работоспособности Hello можно сэкономить время и усилия на изучении и отладки. Hello полезность снят особенно после hello службы работает в масштабе в облаке hello (частный или Azure).

монитор "создатели отчетов" Hello Service Fabric определенные условия, представляющие интерес. Они сообщают об этих условиях на основе своего локального представления. Hello [базе данных health store](service-fabric-health-introduction.md#health-store) собирает данные о работоспособности отправленных все toodetermine "создатели отчетов" ли сущностей глобально работоспособны. модель Hello является предполагаемым toobe toouse широкий, гибкий и простой. качество Hello hello отчетов о работоспособности определяет точность hello hello представление работоспособности кластера hello. Ложные положительные результаты, которые неправильно отображают проблемы работоспособности, могут отрицательно повлиять на обновления или другие службы, использующие данные о работоспособности. В качестве примеров можно вспомнить службы восстановления и механизмы предупреждений. Таким образом, особое внимание — необходимые tooprovide отчеты, отображающие условия интересуют hello лучшего из возможных путей.

toodesign и реализуйте работоспособности reporting watchdogs компоненты и система должна:

* Определите условие hello интересующих их, hello, как он осуществляет мониторинг и hello степени влияет на функциональные возможности кластера или приложение hello. На основе этих сведений, выберите hello отчета свойства и состояния работоспособности.
* Определить hello [сущности](service-fabric-health-introduction.md#health-entities-and-hierarchy) что hello отчета применяется.
* Определить, где выполняется hello reporting, изнутри hello службы или из внутреннего или внешнего наблюдения.
* Определите средства формирования отчетов для используемого источника tooidentify hello.
* Выберите стратегию создания отчетов — периодическую или на основе переходов. в том числе периодически, как она требует более простой код и менее подвержены возникновению tooerrors рекомендуемые Hello.
* Определите продолжительность отчетов hello неработоспособное условия должны оставаться в базе данных health store hello и о том, как должна быть удалена. Используя эту информацию, решите, поведение во время toolive и удалить на истечение срока действия отчета hello.

Как упоминалось выше, отчет могут создавать следующие компоненты.

* Hello мониторинг реплики службы Service Fabric.
* Внутренние устройства наблюдения, развернутые как служба Service Fabric (например, служба без отслеживания состояния Service Fabric, которая проверяет условия и формирует отчеты). Hello watchdogs могут быть развернуты все узлы или непотоковой toohello отслеживаться службой.
* Внутренняя watchdogs, выполняются на узлах Service Fabric hello, но *не* реализован в виде служб Service Fabric.
* Внешние watchdogs этого ресурса hello выборки из *за пределами* кластера Service Fabric hello (например, службы мониторинга как Gomez).

> [!NOTE]
> В стандартной hello кластера hello заполняется работоспособности отчеты, отправляемые компонентами системы hello. Подробнее об этом читайте в статье [Использование отчетов о работоспособности системы для устранения неполадок](service-fabric-understand-and-troubleshoot-with-system-health-reports.md). Hello пользовательские отчеты должны быть отправлены [работоспособные сущности](service-fabric-health-introduction.md#health-entities-and-hierarchy) , уже созданных системой hello.
> 
> 

Один раз hello конструктора отчетов работоспособности снят, можно легко отправить отчеты о работоспособности. Можно использовать [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) tooreport работоспособности, если кластер hello не [безопасного](service-fabric-cluster-security.md) или если hello клиента Fabric имеет права администратора. Отчеты можно сделать с помощью hello API, с помощью [FabricClient.HealthManager.ReportHealth](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.reporthealth), с помощью PowerShell или через REST. Повысить производительность можно с помощью настройки пакетных отчетов.

> [!NOTE]
> Отчет о работоспособности является синхронным, и он представляет hello рабочих проверки на стороне клиента hello. Hello факт, что отчет hello принимается hello работоспособности клиента или hello `Partition` или `CodePackageActivationContext` объектов не означает, что применяется в хранилище hello. Он будет отправлен асинхронно и, возможно, объединен с другими отчетами. Обработка на сервере hello Hello может привести к сбою: hello порядковый номер может быть устаревшим, hello сущности, на какие hello должен применяться отчет был удален, и т. д.
> 
> 

## <a name="health-client"></a>Клиент работоспособности
отчеты о работоспособности Hello отправляются хранилища работоспособности toohello через клиент работоспособности, который находится внутри клиента Fabric hello. можно настроить следующие параметры hello Hello работоспособности клиента:

* **HealthReportSendInterval**: hello задержки между hello время hello отчетов — добавлены toohello клиента и hello время, отправкой toohello базе данных health store. Отчеты, используемые toobatch в одно сообщение, а не отправки одного сообщения для каждого отчета. Hello Пакетная обработка позволяет повысить производительность. Значение по умолчанию — 30 секунд.
* **HealthReportRetrySendInterval**: интервал приветствия, на какие hello работоспособности клиент повторно отправляет накопленный работоспособности сообщает toohello базе данных health store. Значение по умолчанию — 30 секунд.
* **HealthOperationTimeout**: hello времени ожидания для сообщения отчетов отправляются toohello базе данных health store. Если истечения времени ожидания сообщения, hello работоспособности клиент пытается выполнить ее до хранилища работоспособности hello подтверждает обработки отчета hello. Значение по умолчанию — две минуты.

> [!NOTE]
> Когда отчеты hello, объединяются в пакеты, hello клиента Fabric должно поддерживать их существование для по крайней мере hello tooensure HealthReportSendInterval, они отправляются. Если сообщение hello теряется или базе данных health store hello применить их невозможно из-за ошибки tootransient, клиента Fabric hello следует хранить в активном состоянии дольше toogive его tooretry вероятность.
> 
> 

Hello буферизации на клиенте hello принимает уникальность hello hello отчетов во внимание. Например, если определенный поврежденных средства формирования отчетов отчет 100 отчеты в секунду на hello же свойство hello одной сущности, hello отчеты заменяются hello последней версии. В очереди hello клиента существует не более одного такого отчета. Если пакетная обработка настроена, hello количество отчетов отправлено хранилища работоспособности toohello только по одному на интервал отправки. Этот отчет является hello последний добавленный отчет, который отражает состояние последней hello объекта hello.
Укажите параметры конфигурации при `FabricClient` создается путем передачи [FabricClientSettings](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclientsettings) с hello требуемого значения для операций, связанных с работоспособностью.

Hello следующий пример создает клиент, структуры и указывает, должны быть отправлены hello отчетов при добавлении. Если при повторных попытках возникают ошибки или превышено время ожидания, попытки повторяются каждые 40 секунд.

```csharp
var clientSettings = new FabricClientSettings()
{
    HealthOperationTimeout = TimeSpan.FromSeconds(120),
    HealthReportSendInterval = TimeSpan.FromSeconds(0),
    HealthReportRetrySendInterval = TimeSpan.FromSeconds(40),
};
var fabricClient = new FabricClient(clientSettings);
```

Рекомендуется оставлять hello структуры по умолчанию параметры клиента, которые задают `HealthReportSendInterval` too30 секунд. Этот параметр обеспечивает оптимальную производительность из-за toobatching. Для критических отчетов, которые должны отправляться как можно быстрее, используйте `HealthReportSendOptions` с флагом Immediate, имеющим значение `true`, в API [FabricClient.HealthClient.ReportHealth](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.reporthealth). Немедленное отчеты обойти hello интервал пакетов. Этот флаг следует использовать с осторожностью; Мы хотим tootake преимуществами hello работоспособности клиента пакетную обработку, когда это возможно. Немедленно отправить удобно использовать при закрытии клиента Fabric hello (например, процесс hello определил недопустимое состояние и должен tooshut вниз tooprevent побочные эффекты). Это гарантирует усилия отправка отчетов hello накапливаются. При добавлении одного отчета с помощью интерпретации флага hello работоспособности клиента пакетов все отчеты hello накапливаются с момента последней отправки.

При создании кластера tooa подключения через PowerShell, можно указать одинаковые параметры. Следующий пример Hello начинает tooa соединения локального кластера:

```powershell
PS C:\> Connect-ServiceFabricCluster -HealthOperationTimeoutInSec 120 -HealthReportSendIntervalInSec 0 -HealthReportRetrySendIntervalInSec 40
True

ConnectionEndpoint   :
FabricClientSettings : {
                       ClientFriendlyName                   : PowerShell-1944858a-4c6d-465f-89c7-9021c12ac0bb
                       PartitionLocationCacheLimit          : 100000
                       PartitionLocationCacheBucketCount    : 1024
                       ServiceChangePollInterval            : 00:02:00
                       ConnectionInitializationTimeout      : 00:00:02
                       KeepAliveInterval                    : 00:00:20
                       HealthOperationTimeout               : 00:02:00
                       HealthReportSendInterval             : 00:00:00
                       HealthReportRetrySendInterval        : 00:00:40
                       NotificationGatewayConnectionTimeout : 00:00:00
                       NotificationCacheUpdateTimeout       : 00:00:00
                       }
GatewayInformation   : {
                       NodeAddress                          : localhost:19000
                       NodeId                               : 1880ec88a3187766a6da323399721f53
                       NodeInstanceId                       : 130729063464981219
                       NodeName                             : Node.1
                       }
```

Аналогичным образом tooAPI, отчеты можно отправлять с помощью `-Immediate` переключения toobe, отправляются немедленно, независимо от того, hello `HealthReportSendInterval` значение.

REST hello отчеты отправляются toohello Service Fabric шлюз, который имеет клиент внутренние структуры. По умолчанию этот клиент подключен toosend настроенные отчеты каждые 30 секунд в пакетном режиме. Можно изменить интервал пакетов hello с параметром конфигурации кластера hello `HttpGatewayHealthReportSendInterval` на `HttpGateway`. Как уже упоминалось, лучшим вариантом является toosend hello отчеты с `Immediate` значение true. 

> [!NOTE]
> не может сообщить, tooensure, неавторизованные службы работоспособности на основе сущностей hello в кластере hello, настройте hello server tooaccept запросы только от клиентов, защищенных. Hello `FabricClient` использоваться для создания отчетов необходимо иметь с включенной безопасностью может toocommunicate toobe с кластером hello (например, при использовании проверки подлинности Kerberos или сертификат). Ознакомьтесь с дополнительными сведениями о [безопасности кластера](service-fabric-cluster-security.md).
> 
> 

## <a name="report-from-within-low-privilege-services"></a>Создание отчета из служб с низким уровнем привилегий
Если нет кластера toohello доступа администратора для служб Service Fabric, вы можете сообщить работоспособности на сущностях из текущего контекста hello через `Partition` или `CodePackageActivationContext`.

* Для служб без отслеживания состояния, используйте [IStatelessServicePartition.ReportInstanceHealth](https://docs.microsoft.com/dotnet/api/system.fabric.istatelessservicepartition.reportinstancehealth) tooreport на текущий экземпляр службы hello.
* Для служб с отслеживанием состояния, используйте [IStatefulServicePartition.ReportReplicaHealth](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition.reportreplicahealth) tooreport на текущей реплики.
* Используйте [IServicePartition.ReportPartitionHealth](https://docs.microsoft.com/dotnet/api/system.fabric.iservicepartition.reportpartitionhealth) tooreport hello текущего раздела сущности.
* Используйте [CodePackageActivationContext.ReportApplicationHealth](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext.reportapplicationhealth) tooreport для текущего приложения.
* Используйте [CodePackageActivationContext.ReportDeployedApplicationHealth](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext.reportdeployedapplicationhealth) tooreport на hello текущее приложение, развернутое на hello текущего узла.
* Используйте [CodePackageActivationContext.ReportDeployedServicePackageHealth](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext.reportdeployedservicepackagehealth) tooreport на пакеты обновления для приложения hello, развернутого на текущем узле hello.

> [!NOTE]
> На внутреннем уровне hello `Partition` и hello `CodePackageActivationContext` хранения работоспособности клиента, с параметрами по умолчанию. Как описано для hello [работоспособности клиента](service-fabric-report-health.md#health-client), отчеты пакеты и отправляются по таймеру. объекты Hello должна быть сохранена alive toohave отчета hello toosend вероятность.
> 
> 

Можно указать `HealthReportSendOptions` при отправке отчетов с помощью интерфейсов API работоспособности `Partition` и `CodePackageActivationContext`. При наличии критических отчетов, которые должны отправляться как можно быстрее, используйте `HealthReportSendOptions` с флагом Immediate, имеющим значение `true`. Немедленное отчеты обойти hello пакетной обработки интервала hello внутренней работоспособности клиента. Как упоминалось ранее, используйте этот флаг с осторожностью; Мы хотим tootake преимуществами hello работоспособности клиента пакетную обработку, когда это возможно.

## <a name="design-health-reporting"></a>Создание отчета о работоспособности
Hello первым шагом создания отчетов высокого качества определение hello условия, которые могут повлиять на работоспособность hello hello службы. Любое условие, которые могут помочь флаг проблем в службе hello или кластера, при запуске--или даже лучше, прежде чем произойдет ошибка потенциально может сохранить Миллиарды долларов. обеспечивает следующие преимущества Hello меньше время простоя, меньше часов ночи, затраченное на анализ и исправление проблемы и более поздней версии клиентской удовлетворенности.

После определения условий hello контрольного записи должны toofigure out hello toomonitor лучший способ их для баланс между издержками и полезности. Например, рассмотрим службу, которая выполняет сложные вычисления, используя некоторые временные файлы в общей папке. Контрольный может отслеживать tooensure hello общего ресурса, что диске будет достаточно. Оно может отслеживать уведомления об изменении файла или каталога. Он может выдать предупреждение, если достигнуто пороговое значение переднего плана или сообщения об ошибке, если общий ресурс hello заполнен. На предупреждение, системы восстановления удалось запустить очистки старых файлов в общей папке hello. При возникновении ошибки в системе восстановления может переместить hello службы реплики tooanother узел. Обратите внимание на то, как hello условие состояния описаны с точки зрения работоспособности: hello состояние hello условие, которое можно считать работоспособное (ОК) или неработоспособном (предупреждение или ошибка).

После установки сведения мониторинга hello записи контрольного должен toofigure out как tooimplement hello наблюдения. Можно определить условия hello из службы hello, hello контрольного может ли часть саму службу hello отслеживаться. Например код службы hello Проверьте использование общей папки hello и сообщала каждый раз, он пытается toowrite файл. Hello преимуществом такого подхода является reporting простой. Будьте внимательны ошибок контрольного tooprevent из ущерба hello функциональные возможности службы.

Отчетов в отслеживаемых hello службы не всегда параметр. Контрольный hello службы может быть условий может toodetect hello. Он не может иметь hello логику определения и данных toomake hello сообщений. Возможно, мониторинг состояния hello издержки Hello высокого уровня. Hello условия также может не быть tooa определенной службой, но вместо влияют на взаимодействие между службами. Другой вариант — watchdogs toohave в кластере hello в виде отдельных процессов. Hello watchdogs отслеживать условия hello и отчет, не затрагивая hello основных службы каким-либо образом. Например, эти watchdogs может быть реализован как службы без сохранения состояния в hello того же приложения, которые развернуты на всех узлах или hello разным узлам как служба hello.

В некоторых случаях контрольного, работающих в кластере hello не предлагается либо. Если условие hello мониторинг доступности hello или функциональные возможности службы hello как его видят пользователи, это наиболее watchdogs toohave hello в hello же поместить как клиенты hello пользователя. Нет, можно проверить операции hello в hello их вызова того же пользователей. Например может иметь контрольного, находится за пределами кластера hello, выдает запросы службы toohello и проверка задержки hello и правильности hello результата. (Например, запрос к службе калькулятора: возвращает ли 2 + 2 результат 4 в разумные сроки?)

После сведения контрольного hello быть завершен, необходимо принять решение по идентификатор источника, который однозначно идентифицирует его. Если несколько watchdogs hello того же типа живущих в hello кластера, они должны отчетов для различных объектов или, если они сообщают о hello же сущности, используйте идентификатор другого источника или свойства. Убедитесь, что свойства или идентификаторы источника отличаются. Свойство Hello hello отчет о работоспособности должен отражать hello отслеживаемых условие. (В приведенном выше примере hello, может быть свойство hello **ShareSize**.) Если несколько отчетов применить toohello же условие, hello свойство должно содержать некоторые динамические данные, позволяющие toocoexist отчеты. Например, если несколько общих папок необходимо отслеживать toobe, hello именем свойства может быть **ShareSize sharename**.

> [!NOTE]
> Сделать *не* сведения о состоянии tookeep hello работоспособности хранилища. Только сведения, относящиеся к работоспособности должна быть зарегистрирована как работоспособности этот сведения влияние hello работоспособности для ознакомления сущности. базе данных health store Hello не была разработана общего назначения хранилища. В нем tooaggregate логика оценки работоспособности всех данных в состояние работоспособности hello. Отправка сведений, несвязанные toohealth (например, сообщают о состоянии с состоянием работоспособности ОК) не влияет hello суммарный состояние работоспособности, но он может отрицательно сказываться на производительности hello hello базе данных health store.
> 
> 

Следующий вопрос Hello включен tooreport какие сущности. Большую часть времени приветствия, условия hello четко idetifies hello сущности. Выберите сущность hello с лучшие возможности гранулярности. Если условие влияет на все реплики в секции, сообщите hello секции, не в службе hello. Хотя бывают и патологические случаи, когда принять решение сложно. Если условие hello оказывает влияние на сущности, например реплики, но hello желания является условие hello toohave отмеченные дольше, чем hello длительность существования реплика должна быть зарегистрирована в разделе hello. В противном случае при удалении реплики hello hello работоспособности хранилища удаляет все отчеты. Модули записи контрольного нужно решить, время существования hello сущности hello и hello отчета. Должно быть понятно, когда отчет нужно удалять из хранилища (например, когда теряет актуальность ошибка, зафиксированная для сущности).

Давайте рассмотрим пример, в котором составляет точек hello описанный. У нас есть приложение Service Fabric, которое состоит из главной службы с отслеживанием состояния и дополнительных служб без отслеживания состояния, развернутых на всех узлах (один тип дополнительной службы для одного типа задачи). Образец Hello имеет очередь обработка, которая содержит toobe команды, выполняемой баз данных-получателей. базы данных-получатели Hello выполнение hello входящие запросы и отправить назад подтверждение сигналы. Одно условие, может отслеживаться — hello длина очереди master обработки hello. Если длина hello главной очереди достигает порога, создается предупреждение. Hello предупреждение означает, что hello баз данных-получателей не может обрабатывать hello нагрузку. Если очередь hello достигает hello максимальную длину и команды, будут удалены, сообщение об ошибке, как hello службы невозможно восстановить. Hello отчеты могут быть в свойстве hello **QueueStatus**. Hello контрольного находится внутри службы hello и отправляются периодически hello master первичной реплике. время Hello toolive две минуты, и отправляются периодически каждые 30 секунд. Если основной hello выходит из строя, hello отчетов удаляются автоматически из хранилища. Если реплики службы hello работает, но он заблокирован или возникли другие проблемы hello истечения срока действия отчета в базе данных health store hello. В этом случае при обнаружении ошибки оценивается hello сущности.

Другое условие, которое можно отслеживать, — время выполнения задачи. Hello master распределяет задачи toohello баз данных-получателей на основании типа задачи hello. В зависимости от структуры hello образец hello может выполнять опрос hello баз данных-получателей для состояния задачи. Он может также подождать сигналы назад подтверждение toosend баз данных-получателей когда они создаются. В случае второй hello Будьте внимательны toodetect ситуациях, где теряются кристалле баз данных-получателей или сообщений. Один параметр предназначен для hello master toosend toohello запрос проверки связи же получателя, который отправляет обратно его состояние. Если состояние не получено, образец hello считает его сбоя и планирует новую задачу hello. Это поведение предполагается, что задачи hello идемпотентными.

условие Hello отслеживаемых могут быть переведены как предупреждение, если задачу hello не выполняется в определенное время (**t1**, например 10 минут). Если задача hello не завершена в момент (**t2**, например 20 минут), могут быть переведены условие hello отслеживается как ошибка. Отчеты можно отправлять несколькими способами.

* Hello master первичная реплика периодически сообщает сама по себе. Может иметь одно свойство для всех задач, ожидающих в очереди hello. Если хотя бы одной задачи занимает больше времени, hello отчета о состоянии свойства hello **PendingTasks** предупреждение или ошибка соответствующим образом. Если нет ожидающих задач или всех задач начала выполнение, находится в работоспособном состоянии hello отчета. задачи Hello являются постоянными. Если основной hello выходит из строя, основной hello новые можно продолжить tooreport должным образом.
* Другой процесс наблюдения (в облаке hello или внешний) проверяет задачи hello (из за пределами, на основе результат задачи hello требуемого) toosee, если они выполняются. Если они не влияют на hello пороговые значения, отчет отправляется на основной службы hello. Отчет также отправляется на каждой задачи, включает идентификатор задачи hello, таких как **PendingTask + taskId**. Отчеты должны отправляться только о неработоспособных состояниях. Задать время toolive tooa несколько минут и пометьте удалены после истечения срока их действия очистки tooensure toobe отчеты hello.
* Hello получателей, выполняющего задачи сообщает, когда занимает больше времени, чем ожидаемое toorun его. Он выводит на экземпляр службы hello в свойстве hello **PendingTasks**. отчет Hello выявляет hello экземпляр службы, который связан с проблемами, но он не перехватывает hello ситуации, где экземпляр hello выходит из строя. отчеты Hello очищаются затем. Он может сообщить о служба вторичного hello. Если hello получателей выполнит задачу hello, вторичном экземпляре hello очищает hello отчетов из хранилища hello. Hello отчета без записи hello случаев, когда сообщение hello подтверждения теряется и hello не закончена с точки зрения образец hello.

Однако hello отчетов выполняется в описанных выше случаев hello, hello отчетов записываются в работоспособности приложения при оценке работоспособности.

## <a name="report-periodically-vs-on-transition"></a>Периодические отчеты и отчеты на основе переходов
С помощью отчетов модель работоспособности hello, watchdogs отчеты можно отправлять периодически или переходов. Hello рекомендуемые способ контрольного reporting — это периодически, так как код hello — гораздо более простой и менее подвержены возникновению tooerrors. Hello watchdogs должны стремиться toobe сложнее, чем tooavoid возможных ошибок, вызывающих неправильные отчеты. Неправильный отчет о *неработоспособности* влияет на оценку работоспособности и на сценарии, основанные на работоспособности, в частности обновления. Неверный *работоспособное* отчеты скрыть проблемы в кластере hello, что не требуется.

Для периодической отчетности контрольного hello может осуществляться с таймером. На обратный вызов таймера контрольного hello можно проверять состояние hello и отправки отчетов на основе текущего состояния hello. Нет toosee без необходимости какой отчет был отправлен ранее или сделайте Оптимизация с точки зрения системы обмена сообщениями. Hello работоспособности клиента имеет пакетной обработки логики toohelp с производительностью. Хотя hello работоспособности клиента остается активным, он пытается выполнить сбойные внутренне до hello отчета подтвердит его получение хранилища работоспособности hello или контрольного hello создает новую отчет с hello же сущности, свойства и источник.

Отчеты о переходах требуют тщательной обработки состояния. Hello контрольного отслеживает некоторые условия и возвращает только при изменении условий hello. Hello вверх ногами такого подхода — необходимые отчеты меньше. Hello недостатком такого подхода является сложной логики hello контрольного hello. Hello контрольного необходимо поддерживать hello условия или отчеты hello, чтобы их можно было проверяемого toodetermine изменения состояния. При отработке отказа необходимо соблюдать осторожность с отчетами добавлен, но еще не отправлено toohello базе данных health store. Hello порядковый номер должен быть постоянно возрастающим. В противном случае отчеты hello отклоняются как устаревшие. В редких случаях hello, где возникающей потери данных может потребоваться синхронизации между состоянием hello отслеживания hello и состояния hello hello работоспособности хранилища.

Отчеты на основе переходов имеют смысл, когда служба сообщает данные о своем состоянии с помощью `Partition` или `CodePackageActivationContext`. Когда hello локального объекта (реплики или развернутый пакет службы / развернутого приложения) — удалена, все отчеты, также удаляются. Это Автоматическая очистка снижает потребность в hello синхронизации средства формирования отчетов и базе данных health store. Если для родительского раздела или родительского приложения hello отчет, необходимо соблюдать осторожность в отчетах устаревших tooavoid отработки отказа в базе данных health store hello. Логика должны быть добавлены правильное состояние toomaintain hello и очистить hello отчетов из хранилища, когда они больше не нужны.

## <a name="implement-health-reporting"></a>Реализация отчетов о работоспособности
После hello сведения о сущности и отчет не установлены, отправки отчетов о работоспособности можно сделать с помощью hello API, PowerShell или REST.

### <a name="api"></a>API
tooreport через hello API необходимо toocreate тип сущности работоспособности отчетов конкретного toohello нужные им tooreport на. Присвойте hello отчетов tooa работоспособности клиента. Можно также создать сведения о работоспособности и передать его toocorrect методы отчета на `Partition` или `CodePackageActivationContext` tooreport на текущей сущности.

Hello пример периодических отчетов из контрольного внутри кластера hello. Hello контрольного проверяет ли внешний ресурс может осуществляться в узле. манифест службы приложения hello Затребован Hello ресурсов. В случае недоступности ресурсов hello hello другие службы внутри приложения hello может продолжать функционировать должным образом. Таким образом hello отправки отчета в сущности пакета hello развернуты службы каждые 30 секунд.

```csharp
private static Uri ApplicationName = new Uri("fabric:/WordCount");
private static string ServiceManifestName = "WordCount.Service";
private static string NodeName = FabricRuntime.GetNodeContext().NodeName;
private static Timer ReportTimer = new Timer(new TimerCallback(SendReport), null, 30 * 1000, 30 * 1000);
private static FabricClient Client = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });

public static void SendReport(object obj)
{
    // Test whether hello resource can be accessed from hello node
    HealthState healthState = this.TestConnectivityToExternalResource();

    // Send report on deployed service package, as hello connectivity is needed by hello specific service manifest
    // and can be different on different nodes
    var deployedServicePackageHealthReport = new DeployedServicePackageHealthReport(
        ApplicationName,
        ServiceManifestName,
        NodeName,
        new HealthInformation("ExternalSourceWatcher", "Connectivity", healthState));

    // TODO: handle exception. Code omitted for snippet brevity.
    // Possible exceptions: FabricException with error codes
    // FabricHealthStaleReport (non-retryable, hello report is already queued on hello health client),
    // FabricHealthMaxReportsReached (retryable; user should retry with exponential delay until hello report is accepted).
    Client.HealthManager.ReportHealth(deployedServicePackageHealthReport);
}
```

### <a name="powershell"></a>PowerShell
Отправляйте отчеты о работоспособности с помощью команды **Send-ServiceFabric*EntityType*HealthReport**.

Hello пример периодических отчетов по значениям ЦП на узле. Hello отчеты должны отправляться каждые 30 секунд и имеют время toolive две минуты. Если истечения срока их действия, формирования hello имеет проблемы, поэтому узел hello вычисляется при обнаружении ошибки. Если hello ЦП превышает пороговое значение, hello отчет имеет состояние предупреждения. Если hello ЦП остается выше порогового значения дольше времени настройки hello, оно будет отмечено как ошибку. В противном случае hello создателя отчетов отправляет состояние работоспособности ОК.

```powershell
PS C:\> Send-ServiceFabricNodeHealthReport -NodeName Node.1 -HealthState Warning -SourceId PowershellWatcher -HealthProperty CPU -Description "CPU is above 80% threshold" -TimeToLiveSec 120

PS C:\> Get-ServiceFabricNodeHealth -NodeName Node.1
NodeName              : Node.1
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='PowershellWatcher', Property='CPU', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 5
                        SentAt                : 4/21/2015 8:01:17 AM
                        ReceivedAt            : 4/21/2015 8:02:12 AM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/21/2015 8:02:12 AM

                        SourceId              : PowershellWatcher
                        Property              : CPU
                        HealthState           : Warning
                        SequenceNumber        : 130741236814913394
                        SentAt                : 4/21/2015 9:01:21 PM
                        ReceivedAt            : 4/21/2015 9:01:21 PM
                        TTL                   : 00:02:00
                        Description           : CPU is above 80% threshold
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Warning = 4/21/2015 9:01:21 PM
```

Hello следующий пример отображает временных предупреждение на реплике. Он сначала получает идентификатор секции hello и затем hello идентификатор реплики службы hello, которую нужно получить. После этого он отправляет отчет из **PowershellWatcher** в свойстве hello **ResourceDependency**. Hello отчета представляет интерес только двух минут, и он удаляется из хранилища hello автоматически.

```powershell
PS C:\> $partitionId = (Get-ServiceFabricPartition -ServiceName fabric:/WordCount/WordCount.Service).PartitionId

PS C:\> $replicaId = (Get-ServiceFabricReplica -PartitionId $partitionId | where {$_.ReplicaRole -eq "Primary"}).ReplicaId

PS C:\> Send-ServiceFabricReplicaHealthReport -PartitionId $partitionId -ReplicaId $replicaId -HealthState Warning -SourceId PowershellWatcher -HealthProperty ResourceDependency -Description "hello external resource that hello primary is using has been rebooted at 4/21/2015 9:01:21 PM. Expect processing delays for a few minutes." -TimeToLiveSec 120 -RemoveWhenExpired

PS C:\> Get-ServiceFabricReplicaHealth  -PartitionId $partitionId -ReplicaOrInstanceId $replicaId


PartitionId           : 8f82daff-eb68-4fd9-b631-7a37629e08c0
ReplicaId             : 130740415594605869
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='PowershellWatcher', Property='ResourceDependency', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 130740768777734943
                        SentAt                : 4/21/2015 8:01:17 AM
                        ReceivedAt            : 4/21/2015 8:02:12 AM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/21/2015 8:02:12 AM

                        SourceId              : PowershellWatcher
                        Property              : ResourceDependency
                        HealthState           : Warning
                        SequenceNumber        : 130741243777723555
                        SentAt                : 4/21/2015 9:12:57 PM
                        ReceivedAt            : 4/21/2015 9:12:57 PM
                        TTL                   : 00:02:00
                        Description           : hello external resource that hello primary is using has been rebooted at 4/21/2015 9:01:21 PM. Expect processing delays for a few minutes.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : ->Warning = 4/21/2015 9:12:32 PM
```

### <a name="rest"></a>REST
Отправьте отчеты о работоспособности с помощью REST с запросами POST, которые go toohello требуемого сущностей и в описание отчета работоспособности hello текст hello. Например, в разделе как REST toosend [отчеты о работоспособности кластера](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-cluster) или [службы отчетов о работоспособности](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service). Поддерживаются все сущности.

## <a name="next-steps"></a>Дальнейшие действия
На основании данных работоспособности hello записи службы и Администраторы кластеров или приложение можно представить способов tooconsume hello сведения. Например их можно настроить предупреждения, основанные на серьезные проблемы работоспособности состояния toocatch, прежде чем они спровоцировать сбоев. Администраторы могут также настроить восстановление системы toofix автоматически.

[Введение tooService работоспособность структуры мониторинг](service-fabric-health-introduction.md)

[Просмотр отчетов о работоспособности Service Fabric](service-fabric-view-entities-aggregated-health.md)

[Как tooreport и проверки службы работоспособности](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[Использование отчетов о работоспособности системы для устранения неполадок](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[Мониторинг и диагностика состояния служб в локальной среде разработки](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Обновление приложения Service Fabric](service-fabric-application-upgrade.md)

