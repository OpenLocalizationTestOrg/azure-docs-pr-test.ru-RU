---
title: "Здравствуйте, aaaAssess приложения Service Fabric с анализа журналов с помощью портала Azure | Документы Microsoft"
description: "Можно использовать решение Service Fabric hello в службе анализа журналов с помощью hello Azure портала tooassess hello риска и работоспособности приложения Service Fabric микро служб, узлов и кластеров."
services: log-analytics
documentationcenter: 
author: niniikhena
manager: jochan
editor: 
ms.assetid: 9c91aacb-c48e-466c-b792-261f25940c0c
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: nini
ms.openlocfilehash: 891c7f6e5ed511ac18599bdc280ab3dc09700fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="assess-service-fabric-applications-and-micro-services-with-hello-azure-portal"></a>Оценка приложения Service Fabric и микро служб с помощью hello портал Azure

> [!div class="op_single_selector"]
> * [Диспетчер ресурсов](log-analytics-service-fabric-azure-resource-manager.md)
> * [PowerShell](log-analytics-service-fabric.md)
>
>

![Символ Service Fabric](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

В этой статье описывается как hello toouse Service Fabric решения в службе анализа журналов toohelp выявить и устранить проблемы к кластеру Service Fabric.

Hello Service Fabric решение использует данные диагностики Azure Service Fabric виртуальные машины, путем сбора данных из таблиц Azure WAD. Log Analytics затем считывает события платформы Service Fabric, включая **события надежной службы**, **события субъектов**, **операционные события** и **пользовательские события трассировки событий Windows**. С панели мониторинга решения hello являются важные моменты может tooview и соответствующие события в вашей среде Service Fabric.

tooget работы с решением hello, необходимо tooconnect рабочей области аналитики журналов tooa кластера Service Fabric. Ниже приведены три tooconsider сценариев.

1. Если кластер Service Fabric не установлен, выполните действия hello в ***развертывание рабочей области аналитики журналов tooa подключения кластера Service Fabric*** toodeploy новый кластер и настроили tooreport tooLog Analytics.
2. Счетчики производительности toocollect из вашего toouse узлов других решений OMS, такие как безопасность в кластере Service Fabric, выполните шаги hello в ***развертывание рабочей области аналитики журналов tooa подключения кластера Service Fabric с расширением ВМ установлен.***
3. Если вы уже развернули кластера Service Fabric и tooconnect его tooLog Analytics, следуйте указаниям hello ***Добавление существующей учетной записи хранилища tooLog Analytics.***

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace"></a>Развертывание рабочей области аналитики журналов tooa подключения кластера Service Fabric.
Этот шаблон hello следующие:

1. Развертывает рабочую область службы анализа журналов Azure Service Fabric tooa кластера уже подключен. У вас есть параметр toocreate hello новую рабочую область при развертывании шаблона hello или имя входного hello уже существующей рабочей области аналитики журналов.
2. Добавление рабочей области аналитики журналов toohello hello хранилище диагностических данных учетной записи.
3. Позволяет hello Service Fabric решения в рабочей области аналитики журналов.

[![Развертывание tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)

После выбора hello развертывать кнопку выше, hello Azure откроется портал с параметрами для вас tooedit. Быть убедиться, что toocreate новую группу ресурсов при вводе имя новой рабочей области аналитики журналов:

![Service Fabric](./media/log-analytics-service-fabric/2.png)

![Service Fabric](./media/log-analytics-service-fabric/3.png)

Примите условия использования hello и нажмите кнопку **создать** toostart hello развертывания. После завершения развертывания hello должны видеть hello новую рабочую область и создания кластера и hello WADServiceFabric * событий, WADWindowsEventLogs и WADETWEvent добавляемых таблиц:

![Service Fabric](./media/log-analytics-service-fabric/4.png)

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace-with-vm-extension-installed"></a>Развертывание рабочей области аналитики журналов tooa подключения кластера Service Fabric с установлены расширения виртуальных Машин.

Этот шаблон hello следующие:

1. Развертывает рабочую область службы анализа журналов Azure Service Fabric tooa кластера уже подключен. Вы можете создать новую рабочую область или использовать существующую.
2. Добавление рабочей области аналитики журналов toohello hello хранилище диагностических данных учетных записей.
3. Позволяет hello Service Fabric решения в рабочей области аналитики журналов hello.
4. Устанавливает расширение агента MMA hello в каждый набор кластера Service Fabric масштабирования виртуальных машин. С установленным агентом MMA hello являются метрики производительности может tooview об узлах.

[![Развертывание tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)

Ниже hello же описанные выше шаги, необходимые параметры ввода hello и начнем развертывания. Еще раз должен появиться hello новую рабочую область, кластера и все созданные WAD-таблиц:

![Service Fabric](./media/log-analytics-service-fabric/5.png)

### <a name="viewing-performance-data"></a>Просмотр данных о производительности

tooview данные о производительности из узлов:


[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

- Запустите рабочую область службы анализа журналов hello hello портал Azure.
  ![Service Fabric](./media/log-analytics-service-fabric/6.png)
- Перейдите на левой панели hello tooSettings и выбрать данные >> счетчиков производительности Windows >> «hello добавить выбранные счетчики производительности»: ![Service Fabric](./media/log-analytics-service-fabric/7.png)
- В поиске по журналам используйте следующие запросы toodelve в основных метрик о узлы hello:

    а. Сравнение hello среднее использование ЦП для всех узлов, в последний час toosee hello какие узлы в случае возникновения проблем и какие интервалом узла имели пик.

    ```
    Type=Perf ObjectName=Processor CounterName="% Processor Time"|measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/10.png)

    b. Просмотрите аналогичные графики для доступной памяти на каждом узле, используя этот запрос:

    ```
    Type=Perf ObjectName=Memory CounterName="Available MBytes Memory" | measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    tooview список всех узлов, показывающая hello точное среднее значение для доступно МБ для каждого узла, используется следующий запрос:

    ```
    Type=Perf (ObjectName=Memory) (CounterName="Available MBytes") | measure avg(CounterValue) by Computer
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/11.png)

    c. В случае hello требуется toodrill работу в определенном узле изучив hello почасовой среднее минимальное, максимальное и 75 процентиля ЦП, вы могли toodo это по с помощью этого запроса (замените поле компьютера):

    ```
    Type=Perf CounterName="% Processor Time" InstanceName=_Total Computer="BaconDC01.BaconLand.com"| measure min(CounterValue), avg(CounterValue), percentile75(CounterValue), max(CounterValue) by Computer Interval 1HOUR
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/12.png)

Дополнительные сведения о метриках производительности в службе анализа журналов на hello [Operations Management Suite блог](https://blogs.technet.microsoft.com/msoms/tag/metrics/).


## <a name="adding-an-existing-storage-account-toolog-analytics"></a>Добавление существующей учетной записи хранилища tooLog аналитика

Этот шаблон просто добавляет существующего хранилища учетных записей tooa новый или существующий анализа журналов рабочей области.

[![Развертывание tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)

> [!NOTE]
> При работе с уже существующей рабочей области аналитики журналов выбора группы ресурсов, выберите «Использовать существующее» и выполните поиск hello группы ресурсов, содержащий рабочей областью аналитики журналов hello. В противном случае создайте новую.
> ![Service Fabric](./media/log-analytics-service-fabric/8.png)
>
>

После развертывания этот шаблон можно будет toosee hello хранения подключена учетная запись tooyour анализа журналов рабочей области. В этом случае добавлены один Дополнительные хранилища учетной записи toohello Exchange рабочей области, созданной выше.
![Service Fabric](./media/log-analytics-service-fabric/9.png)

## <a name="view-service-fabric-events"></a>Просмотр событий Service Fabric

После завершения развертывания hello и включил hello Service Fabric решения в рабочей области, выберите hello **Service Fabric** плитки на панели мониторинга портала toolaunch hello hello анализа журналов Service Fabric. панель мониторинга Hello, включает столбцы hello hello в следующей таблице. Каждый столбец перечислены hello top 10 событий, сопоставляя count, критерии столбца для hello указанный диапазон времени. Можно выполнить поиск журнала, который предоставляет hello весь список, щелкнув **все** hello справа внизу каждого столбца или щелкните заголовок столбца hello.

| **Событие Service Fabric** | **description** |
| --- | --- |
| Важные проблемы |Отображение таких проблем, как сбои и отмены RunAsync, а также отключение узлов. |
| Операционные события |Важные операционные события, такие как обновление и развертывание приложения. |
| События надежных служб |Важные события надежных служб, например вызовы RunAsync. |
| События субъектов |Важные события субъектов, создаваемые микрослужбами, например исключения, вызываемые методом субъекта, включения и отключения субъекта и т. д. |
| События приложений |Все пользовательские события ETW, создаваемые приложениями. |

![Панель мониторинга Service Fabric](./media/log-analytics-service-fabric/sf3.png)

![Панель мониторинга Service Fabric](./media/log-analytics-service-fabric/sf4.png)

Hello ниже приведены методы сбора данных и другие сведения о сборе данных для Service Fabric.

| платформа | Direct Agent | Агент Operations Manager | Хранилище Azure | Нужен ли Operations Manager? | Отправка данных агента Operations Manager через группу управления | частота сбора |
| --- | --- | --- | --- | --- | --- | --- |
| Windows |  |  | &#8226; |  |  |10 минут |

> [!NOTE]
> Область hello этих событий в hello Service Fabric решения можно изменить, щелкнув **данные основаны на последних 7 дней** hello верхней части панели мониторинга hello. Также можно показать события, создаваемые в hello последние семь дней, один день или 6 часов. Или можно выбрать **пользовательские** toospecify пользовательского диапазона дат.
>
>

## <a name="next-steps"></a>Дальнейшие действия

* Используйте [поиска журналов в службе анализа журналов](log-analytics-log-searches.md) tooview подробные данные о событиях Service Fabric.
