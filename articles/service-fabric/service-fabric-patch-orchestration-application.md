---
title: "aaaAzure orchestration приложения Service Fabric исправление | Документы Microsoft"
description: "Приложение tooautomate операционной системы установку исправлений на кластер Service Fabric."
services: service-fabric
documentationcenter: .net
author: novino
manager: timlt
editor: 
ms.assetid: de7dacf5-4038-434a-a265-5d0de80a9b1d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/9/2017
ms.author: nachandr
ms.openlocfilehash: fbb89aa2ea418181ee908a01850178c113c462fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="patch-hello-windows-operating-system-in-your-service-fabric-cluster"></a>Исправление для операционной системы Windows hello кластера Service Fabric

Hello исправление orchestration приложение является приложением Azure Service Fabric, который автоматизирует установку исправлений на кластер Service Fabric в Azure без простоев операционной системы.

orchestration приложение Hello исправление предоставляет hello ниже:

- **Автоматическая установка обновлений операционной системы**. Обновления операционной системы автоматически загружаются и устанавливаются. При необходимости узлы кластера перезагружаются без остановки его работы.

- **Исправление с учетом состояния кластера и интеграция функций работоспособности**. Во время применения обновлений, приложение orchestration исправление hello отслеживает работоспособность hello hello узлов кластера. Узлы кластера обновляются поочередно или по одному домену обновления за раз. Если hello работоспособности кластера hello выходит из строя из-за выполнения процесса toohello исправления будет остановлена tooprevent aggravating проблема hello.

## <a name="internal-details-of-hello-app"></a>Внутренние сведения о приложение hello

orchestration приложение Hello patch состоит из hello следующие подкомпоненты:

- **Служба координатора** — эта служба с отслеживанием состояния отвечает за следующие задачи:
    - Согласование задания обновления Windows hello на весь кластер hello.
    - Хранение результатов hello завершенных операций обновления Windows.
- **Служба агента узла** — это служба без отслеживания состояния, которая выполняется на всех узлах кластера Service Fabric. Hello служба отвечает за:
    - Начальная загрузка hello NTService агента узла.
    - Мониторинг hello NTService агента узла.
- **Служба NTService агента узла** — служба Windows NT, которая выполняется с разрешением высокого уровня (СИСТЕМА). Напротив hello служба агента узла и hello службы координатора запускать с привилегиями более низкого уровня (NETWORK SERVICE). Служба Hello несет ответственность за выполнение после задания центра обновления Windows на всех узлах кластера hello hello:
    - Отключение автоматического обновления Windows на узле hello.
    - Загрузка и установка обновления Windows предоставил пользователь hello toohello политики в соответствии с.
    - Перезапуск post машины hello установки обновления Windows.
    - Отправка результатов hello toohello обновлений Windows служба координатора.
    - сообщение сведений о работоспособности, если операцию не удалось выполнить, исчерпав все повторные попытки.

> [!NOTE]
> использует приложение hello Service Fabric Hello исправление orchestration восстановить toodisable службы диспетчера system или включить hello узел и выполняет проверку работоспособности. Hello задачи восстановления, созданные hello hello исправление orchestration приложение отслеживает ход выполнения обновления Windows для каждого узла.

## <a name="prerequisites"></a>Предварительные требования

### <a name="minimum-supported-service-fabric-runtime-version"></a>Минимальная поддерживаемая версия среды выполнения Service Fabric

#### <a name="azure-clusters"></a>Кластеры Azure
orchestration приложение Hello исправления должна выполняться на Azure кластеры версий Service Fabric среды выполнения версии 5.5 или более поздней версии.

#### <a name="standalone-on-premises-clusters"></a>Автономные локальные кластеры
orchestration приложение Hello исправления должна выполняться на изолированные кластеры, имеющие v5.6 версии среды выполнения Service Fabric или более поздней версии.

### <a name="enable-hello-repair-manager-service-if-its-not-running-already"></a>Включение службы диспетчера восстановления hello (если она не была запущена ранее)

orchestration приложение Hello исправление требуется hello восстановления диспетчера системы службы toobe включена в кластере hello.

#### <a name="azure-clusters"></a>Кластеры Azure

Кластеры Azure hello серебристом устойчивость уровня имеют hello исправления service manager включен по умолчанию. Кластеры Azure уровня gold устойчивость hello может иметь или не иметь включен, в зависимости от того, когда были созданы эти кластеры службы диспетчера восстановления hello. Кластеры Azure уровня бронзового устойчивость hello, по умолчанию имеют hello исправления service manager включен. Если hello служба уже включена, вы увидите его выполнение в разделе служб системы hello в обозреватель Service Fabric hello.

##### <a name="azure-portal"></a>Портал Azure
Диспетчер восстановления на портале Azure можно включить во время настройки кластера hello. Выберите `Include Repair Manager` под флажком `Add on features` во время hello конфигурации кластера.
![Снимок экрана с подключением диспетчера восстановления на портале Azure](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)

##### <a name="azure-resource-manager-template"></a>Шаблон диспетчера ресурсов Azure
Можно также использовать hello [шаблона Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) tooenable hello службы диспетчера восстановления на новых и существующих кластеров Service Fabric. Получите шаблон hello hello кластера, которые должны toodeploy. Можно использовать шаблоны образец hello или создать настраиваемый шаблон диспетчера ресурсов. 

tooenable hello восстановления диспетчера службы с помощью [шаблона Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):

1. Сначала проверьте, что hello `apiversion` задано слишком`2017-07-01-preview` для hello `Microsoft.ServiceFabric/clusters` ресурсов, как показано в следующий фрагмент кода hello. Если он не совпадает, то вы должны tooupdate hello `apiVersion` toohello значение `2017-07-01-preview`:

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. Теперь включите службы диспетчера восстановления hello, добавив следующие hello `addonFeatures` разделе после hello `fabricSettings` раздела:

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. После обновления шаблон кластера с этими изменениями, их применения и позволить завершить обновление hello. Теперь можно увидеть hello диспетчер восстановления системной службы, работающих в кластере. Он вызывается `fabric:/System/RepairManagerService` в разделе служб системы hello в обозреватель Service Fabric hello. 

### <a name="standalone-on-premises-clusters"></a>Автономные локальные кластеры

Можно использовать hello [параметры конфигурации для кластера Windows автономный](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) tooenable hello службы диспетчера восстановления на новых и существующих кластера Service Fabric.

Служба диспетчера восстановления hello tooenable:

1. Сначала проверьте, что hello `apiversion` в [конфигурации кластера Общие](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) задано слишком`04-2017` или более поздней версии:

    ```json
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "04-2017",
        ...
    }
    ```

2. Теперь включите службы диспетчера восстановления, добавив следующие hello `addonFeaturres` разделе после hello `fabricSettings` статьи, как показано ниже:

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. Обновить манифест кластера с этими изменениями, hello обновления манифеста кластера с помощью [Создание нового кластера](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) или [конфигурации кластера обновления hello](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration). После запуска кластера hello с манифестом обновленные кластера теперь можно увидеть hello диспетчер восстановления системной службы, работающих в кластере, который называется `fabric:/System/RepairManagerService`в разделе системных служб раздела Service Fabric explorer hello.

### <a name="disable-automatic-windows-update-on-all-nodes"></a>Отключение автоматического обновления Windows на всех узлах

Автоматическое обновление Windows может привести tooavailability потери, поскольку нескольким узлам кластера можно перезагрузить hello же время. приложение orchestration исправление Hello, по умолчанию, пытается toodisable hello автоматического обновления Windows на каждом узле кластера. Тем не менее если параметры hello управляются администратором или групповой политики, рекомендуется hello параметр политики слишком «уведомление перед загрузкой» явно центра обновления Windows.

### <a name="optional-enable-azure-diagnostics"></a>Включение системы диагностики Azure (необязательно)

Для кластеров со средой выполнения Service Fabric версии `5.6.220.9494` и выше журналы приложения для оркестрации исправлений будут собираться как часть журналов Service Fabric.
Этот шаг можно пропустить, если кластер работает под управлением среды выполнения Service Fabric версии `5.6.220.9494` и выше.

Для кластеров под управлением версии среды выполнения Service Fabric меньше, чем `5.6.220.9494`, журналы для orchestration приложение hello исправление собираются локально на каждом узле кластера hello.
Мы рекомендуем настроить журналы диагностики Azure tooupload из центрального расположения tooa все узлы.

Сведения о включении системы диагностики Azure см. в статье [Сбор журналов с помощью системы диагностики Azure](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).

Журналы для hello исправление orchestration приложения создаются на следующих основных поставщика идентификаторов hello:

- e39b723c-590c-4090-abb0-11e3e6616346
- fc0028ff-bfdc-499f-80dc-ed922c52c5e9
- 24afa313-0d3b-4c7c-b485-1047fd964b60
- 05dc046c-60e9-4ef7-965e-91660adffa68

В диспетчер ресурсов шаблона goto `EtwEventSourceProviderConfiguration` раздела `WadCfg` и добавить hello следующие записи:

```json
  {
    "provider": "e39b723c-590c-4090-abb0-11e3e6616346",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
      "eventDestination": "PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "fc0028ff-bfdc-499f-80dc-ed922c52c5e9",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "24afa313-0d3b-4c7c-b485-1047fd964b60",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "05dc046c-60e9-4ef7-965e-91660adffa68",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  }
```

> [!NOTE]
> Если кластер Service Fabric имеет несколько типов узлов, то необходимо добавить все hello hello предыдущего раздела `WadCfg` разделы.

## <a name="download-hello-app-package"></a>Загрузите пакет приложения hello

Загрузить приложение hello hello [ссылка для загрузки](https://go.microsoft.com/fwlink/P/?linkid=849590).

## <a name="configure-hello-app"></a>Настройте приложение hello

Здравствуйте поведение orchestration приложение hello исправление может быть настроенный toomeet вашим потребностям. Переопределите значения по умолчанию hello, передавая параметр приложения hello во время создания приложения или обновления. Параметры приложения могут быть предоставлены, указав `ApplicationParameter` toohello `Start-ServiceFabricApplicationUpgrade` или `New-ServiceFabricApplication` командлетов.

|**Параметр**        |**Тип**                          | **Дополнительные сведения**|
|:-|-|-|
|MaxResultsToCache    |длинное целое                              | Максимальное количество результатов обновления Windows, которые необходимо кэшировать. <br>Значение по умолчанию — 3000 при условии, что: <br> - количество узлов —20; <br> - количество обновлений на узле в месяц — 5; <br> - количество результатов на операцию может быть 10; <br> -Должны ли сохраняться результатов для hello за последние три месяца. |
|TaskApprovalPolicy   |Перечисление. <br> { NodeWise, UpgradeDomainWise }                          |TaskApprovalPolicy указывает политику hello, toobe, используемые tooinstall Windows hello службы координатора обновлений на узлах кластера Service Fabric hello.<br>                         Допустимые значения: <br>                                                           <b>NodeWise</b>. Обновление Windows устанавливается на один узел за раз. <br>                                                           <b>UpgradeDomainWise</b>. Обновление Windows устанавливается на один домен обновления за раз (На максимальный hello, все узлы hello, принадлежащий домену обновления tooan можно перейти для центра обновления Windows).
|LogsDiskQuotaInMB   |длинное целое  <br> (значение по умолчанию: 1024)               |Максимальный размер журналов приложения для управления исправлениями, которые могут быть сохранены локально на узле (в мегабайтах).
| WUQuery               | string<br>(значение по умолчанию: IsInstalled=0)                | Запрос tooget обновления Windows. Дополнительные сведения см. в разделе [WuQuery](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx).
| InstallWindowsOSOnlyUpdates | Bool <br> (значение по умолчанию: True)                 | Этот флаг позволяет toobe обновления системы установлена операционная система Windows.            |
| WUOperationTimeOutInMinutes | int <br>(значение по умолчанию: 90)                   | Указывает время ожидания hello для любой операции обновления Windows (поиска или загружать или устанавливать). Если операция hello не была завершена в течение Здравствуйте заданное время ожидания, он будет прерван.       |
| WURescheduleCount     | int <br> (значение по умолчанию: 5)                  | Hello максимальное число hello службы, а затем — hello центра обновления Windows в случае постоянного сбоя операции.          |
| WURescheduleTimeInMinutes | int <br>(значение по умолчанию: 30) | Интервал приветствия, на какие hello службы, а затем — обновления Windows hello в случае, если ошибка продолжает появляться. |
| WUFrequency           | Строка с разделителями-запятыми (по умолчанию: Weekly, Wednesday, 7:00:00)     | частота Hello для установки обновления Windows. доступны следующие Hello формат и возможные значения: <br>- Ежемесячно, ДД,ЧЧ:ММ:СС (например: Monthly, 5,12:22:32); <br> - Еженедельно, ДЕНЬ, ЧЧ:ММ:СС (например: Weekly, Tuesday, 12:22:32);  <br> - Ежедневно, ЧЧ:ММ:СС (например: Daily, 12:22:32);  <br> - Никогда — указывает, что обновление Windows не должно выполняться.  <br><br> Обратите внимание, что все hello значения времени в формате UTC.|
| AcceptWindowsUpdateEula | Bool <br>(значение по умолчанию: True) | Установив этот флажок, приложение hello принимает hello конечным пользователем лицензионного соглашения для обновления Windows, от имени владельца hello машины hello.              |

> [!TIP]
> Если toohappen центра обновления Windows требуется немедленно, установите `WUFrequency` toohello относительного времени развертывания приложения. Например, предположим, имеется пять узел кластера и план toodeploy hello приложение теста в около 5:00 UTC. Если предполагается, что обновление приложения hello или развертывания занимает 30 минут на hello максимальное, задайте hello WUFrequency как «Ежедневно, 17:30:00.»

## <a name="deploy-hello-app"></a>Развернуть приложение hello

1. Завершите все hello кластера tooprepare hello обязательные шаги.
2. Разверните приложение hello исправление orchestration, как и любое другое приложение Service Fabric. С помощью PowerShell, можно развернуть приложение hello. Следуйте указаниям hello [развертывание и удаление приложений с помощью PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).
3. приложение hello tooconfigure во время развертывания, передайте hello hello `ApplicationParamater` toohello `New-ServiceFabricApplication` командлета. Для вашего удобства мы предоставили hello сценария Deploy.ps1 вместе с приложением hello. скрипт hello toouse:

    - Подключиться с помощью кластера Service Fabric tooa `Connect-ServiceFabricCluster`.
    - Выполнить сценарий PowerShell hello Deploy.ps1 с hello соответствующие `ApplicationParameter` значение.

> [!NOTE]
> Сохранить скрипт hello и папка приложения hello PatchOrchestrationApplication в hello один каталог.

## <a name="upgrade-hello-app"></a>Обновление приложения hello

tooupgrade существующего приложения orchestration исправлений с помощью PowerShell, выполните действия hello в [обновление приложения Service Fabric, с помощью PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).

## <a name="remove-hello-app"></a>Удалите приложение hello

приложение hello tooremove, повторите шаги hello в [развертывание и удаление приложений с помощью PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).

Для вашего удобства мы предоставили hello сценария Undeploy.ps1 вместе с приложением hello. скрипт hello toouse:

  - Подключиться с помощью кластера Service Fabric tooa ```Connect-ServiceFabricCluster```.

  - Выполните сценарий PowerShell hello Undeploy.ps1.

> [!NOTE]
> Сохранить скрипт hello и папка приложения hello PatchOrchestrationApplication в hello один каталог.

## <a name="view-hello-windows-update-results"></a>Просмотр результатов обновления Windows hello

Hello исправление orchestration приложение предоставляет API-интерфейс REST toodisplay hello исторических результаты toohello пользователя. Пример результата hello JSON:
```json
[
  {
    "NodeName": "_stg1vm_1",
    "WindowsUpdateOperationResults": [
      {
        "OperationResult": 0,
        "NodeName": "_stg1vm_1",
        "OperationTime": "2017-05-21T11:46:52.1953713Z",
        "UpdateDetails": [
          {
            "UpdateId": "7392acaf-6a85-427c-8a8d-058c25beb0d6",
            "Title": "Cumulative Security Update for Internet Explorer 11 for Windows Server 2012 R2 (KB3185319)",
            "Description": "A security issue has been identified in a Microsoft software product that could affect your system. You can help protect your system by installing this update from Microsoft. For a complete listing of hello issues that are included in this update, see hello associated Microsoft Knowledge Base article. After you install this update, you may have toorestart your system.",
            "ResultCode": 0
          }
        ],
        "OperationType": 1,
        "WindowsUpdateQuery": "IsInstalled=0",
        "WindowsUpdateFrequency": "Daily,10:00:00",
        "RebootRequired": false
      }
    ]
  },
  ...
]
```
Если обновление не запланировано еще, результат hello JSON является пустым.

Войдите в систему tooquery toohello кластера Windows Update результаты. Узнать адрес hello реплики для первичной hello hello службы координатора затем попаданий hello URL-адрес из браузера hello: http://&lt;РЕПЛИКИ IP&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1 / GetWindowsUpdateResults.

Hello конечную точку REST для службы координатора hello имеет динамический порт. toocheck hello точный URL-адрес, относятся toohello Service Fabric Explorer. Например, результаты hello доступны на `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.

![Представление конечной точки REST](media/service-fabric-patch-orchestration-application/Rest_Endpoint.png)


Hello обратный прокси-сервер будет включен в кластер hello, можно получить доступ к hello URL-адрес за пределами кластера hello.
Здравствуйте, конечная точка, которая должна toobe попадание — http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.

tooenable hello обратного прокси-сервера на кластере hello, следуйте указаниям hello [обратный прокси-сервер в Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy). 

> 
> [!WARNING]
> После настройки hello обратного прокси-сервера, все micro службы в кластере hello, которые предоставляют конечную точку HTTP, адресуемых за пределами кластера hello.

## <a name="diagnosticshealth-events"></a>События диагностики и работоспособности

### <a name="collect-patch-orchestration-app-logs"></a>Сбора журналов приложения для управления исправлениями

В среде выполнения версии `5.6.220.9494` и выше журналы приложения для управления исправлениями собираются как часть журналов Service Fabric.
Для кластеров под управлением версии среды выполнения Service Fabric меньше, чем `5.6.220.9494`, можно собирать журналы с помощью одного из следующих методов hello.

#### <a name="locally-on-each-node"></a>Локально на каждом узле

Если версия среды выполнения Service Fabric ниже, чем `5.6.220.9494`, журналы собираются локально на каждом узле кластера Service Fabric. Hello журналы hello tooaccess расположение — \[Service Fabric\_установки\_диска\]:\\PatchOrchestrationApplication\\журналы.

Например, Service Fabric установлен на диске D, hello путь — D:\\PatchOrchestrationApplication\\журналы.

#### <a name="central-location"></a>Центральное расположение

Если диагностики Azure настроен как часть обязательные шаги, журналы для orchestration приложение hello исправления доступны в хранилище Azure.

### <a name="health-reports"></a>Отчеты о работоспособности

orchestration приложение Hello исправления также публикует отчеты о работоспособности от hello Координатор службы или hello служба агента узла в hello в следующих случаях:

#### <a name="a-windows-update-operation-failed"></a>Сбой операции обновления Windows

Если операция обновления Windows не на узле, для hello службы узла агента создается отчет о работоспособности. Сведения об отчете о работоспособности hello содержат имя проблемный узел hello.

После исправления успешно завершено на проблемный узел hello, hello отчета автоматически очищается.

#### <a name="hello-node-agent-ntservice-is-down"></a>Hello NTService узел агента не работает

Если hello NTService узел агента не работает на узле, для hello служба агента узла создается отчет о работоспособности уровня предупреждения.

#### <a name="hello-repair-manager-service-is-not-enabled"></a>Служба диспетчера восстановления Hello не включена

Если служба диспетчера восстановления hello не найден в кластере hello, для hello службы координатора создается отчет о работоспособности уровня предупреждения.

## <a name="frequently-asked-questions"></a>Часто задаваемые вопросы

В. **Почему я вижу кластер в состоянии ошибки при запуске приложение orchestration hello исправление?**

О. Во время процесса установки hello orchestration приложение hello исправление отключает или перезагрузки узлов, которые временно может привести к hello работоспособности кластера hello выхода из строя.

На основе hello политики для приложения hello, либо один узел можно перейти во время операции исправления *или* всего домена обновления могут выключаться одновременно.

Hello конце hello установки обновления Windows приветствия повторно включать узлы после перезапуска.

В следующем примере hello кластер hello перехода, состояние ошибки tooan временно поскольку два узла были вниз и hello MaxPercentageUnhealthNodes политики было нарушено. Ошибка Hello является временной до текущей операции обновления hello.

![Представление неработоспособного кластера](media/service-fabric-patch-orchestration-application/MaxPercentage_causing_unhealthy_cluster.png)

Если hello проблема повторяется, см. раздел toohello Устранение неполадок.

В. **Приложение для управления исправлениями находится в состоянии предупреждения**

О. Проверьте toosee, если отчет о работоспособности учтена для приложения hello hello основную причину. Как правило предупреждение hello содержит подробности проблемы hello. Если hello проблема временная, приложение hello является ожидаемым tooauto восстановление из этого состояния.

В. **Что делать, если кластер работает неправильно, и требуется toodo обновление для срочных операционной системы?**

О. orchestration приложение Hello исправление не устанавливает обновления при hello кластер неработоспособен. Попробуйте toobring кластера tooa работоспособное состояние toounblock hello исправление orchestration приложения рабочего процесса.

В. **Почему применения исправлений ко всем кластерам слишком долго toorun?**

О. Hello время, необходимое исправление orchestration приложением hello главным образом зависит hello следующие факторы:

- политика Hello hello службы координатора. 
  - Здравствуйте, политика по умолчанию `NodeWise`, приводит к исправления одновременно только один узел. Особенно в случае hello больше кластеров, мы рекомендуем использовать hello `UpgradeDomainWise` tooachieve политики применения исправлений ко всем кластерам быстрее.
- число обновлений, доступных для загрузки и установки Hello. 
- Здравствуйте, среднее время, необходимое toodownload и установите обновление, которое не должно превышать нескольких часов.
- производительность Hello hello виртуальной Машины и пропускную способность сети.

В. **Почему я вижу некоторые обновления в центре обновления Windows результатов, полученных через REST api, но не в журнале Центра обновления Windows на компьютере hello**

О. Некоторые обновления продуктов должны toobe возврата истории соответствующие обновления, исправления. Например, сведения об обновлении Защитника Windows не отображаются в журнале Центра обновлений Windows в Windows Server 2016.

## <a name="disclaimers"></a>Заявления об отказе от ответственности

- приложение orchestration исправление Hello принимает hello конечным пользователем лицензионного соглашения из центра обновления Windows, от имени пользователя hello. При необходимости приветствия можно отключить в конфигурации hello приложения hello.

- orchestration приложение Hello исправление собирает использования tootrack телеметрии и производительности. Данные телеметрии приложения Hello следует приветствия настройки телеметрии среды выполнения Service Fabric hello (который по умолчанию).

## <a name="troubleshooting"></a>Устранение неполадок

### <a name="a-node-is-not-coming-back-tooup-state"></a>Узел не возвращается состояние tooup

**узел Hello могло остаться в состоянии отключение из-за**:

Проверка безопасности находится в состоянии ожидания. tooremedy этой ситуации, чтобы обеспечить достаточное количество узлов в работоспособное состояние.

**узел Hello могло остаться в отключенном состоянии, так как**:

- Hello узел был отключен вручную.
- Hello узел был отключен из-за tooan задания текущей инфраструктуры Azure.
- узел Hello была временно отключена hello узел toopatch приложения hello исправление orchestration.

**Hello узла могло остаться в отключенном состоянии из-за**:

- узел Hello вручную поместить в отключенном состоянии.
- Hello узел находится в режиме перезапуска (который может быть вызвано orchestration приложение hello исправления).
- Hello узел не работает из-за tooa неисправный виртуальная машина или машины проблем или сетевым соединением.

### <a name="updates-were-skipped-on-some-nodes"></a>Обновления на некоторых узлах пропущены

orchestration приложение Hello исправления пытается tooinstall обновления соответствующим toohello перенесения политики Windows. Служба Hello пытается toorecover hello узел и пропустить политики приложения соответствующим toohello hello обновления.

В этом случае для hello службы узла агента создается отчет о работоспособности уровня предупреждения. результат Hello центра обновления Windows, также содержит hello возможных причин сбоя hello.

### <a name="hello-health-of-hello-cluster-goes-tooerror-while-hello-update-installs"></a>Hello работоспособности кластера hello переходит tooerror во время установки обновления hello

Ошибочный обновления Windows может привести к остановке hello работоспособности приложения или кластера на конкретный узел или домен обновления. приложение orchestration исправление Hello прекращается любой последующей операции обновления Windows, пока hello кластер является работоспособным.

Администратору необходимо вмешательство и определить, почему приложение hello или кластера стал неработоспособным из-за tooWindows обновления.

## <a name="release-notes-"></a>Заметки о выпуске

### <a name="version-110"></a>Версия 1.1.0
- Общедоступный выпуск

### <a name="version-111"></a>Версии 1.1.1
- Исправлена ошибка в SetupEntryPoint службы агента узла, которая препятствовала установке службы NTService агента узла.

### <a name="version-120-latest"></a>Версия 1.2.0 (последняя версия)

- Исправлены ошибки, связанные с рабочим процессом перезапуска системы.
- Исправление ошибки при создании задач надежного обмена Сообщениями из-за проверки работоспособности toowhich при подготовке задач восстановления не происходит должным образом.
- Измененные hello режим запуска для службы windows POANodeSvc из toodelayed автоматически автоматический режим.
