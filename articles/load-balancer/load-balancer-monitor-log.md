---
title: "aaaMonitor операции, события и счетчики для балансировки нагрузки | Документы Microsoft"
description: "Узнайте, как tooenable предупреждения события и проверки ведение журнала состояния работоспособности для балансировки нагрузки Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 56656d74-0241-4096-88c8-aa88515d676d
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: ac53c2254e06cad780ad6144c5c30f0085d12576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-for-azure-load-balancer"></a>Служба анализа журналов для балансировщика нагрузки Azure

Можно использовать различные типы журналов в Azure toomanage и устранение неполадок подсистемы балансировки нагрузки. Некоторые из этих журналов может осуществляться через портал hello. Также все журналы можно извлечь из хранилища BLOB-объектов Azure, чтобы просматривать их с помощью таких средств, как Excel и Power BI. Дополнительные сведения о различных типах журналов из следующего списка hello hello.

* **Журналы аудита:** можно использовать [журналов аудита Azure](../monitoring-and-diagnostics/insights-debugging-with-events.md) (прежнее название — операционные журналы) tooview все операции, отправленные tooyour подписок Azure и их состояние. Журналы аудита включены по умолчанию и можно просмотреть в hello портал Azure.
* **Журналы событий на предупреждения:** rasied оповещения tooview этот журнал можно использовать подсистемой балансировки нагрузки hello. Сбор сведений о состоянии Hello для подсистемы балансировки нагрузки hello каждые пять минут. В этом журнале делается запись, только если возникает событие оповещения балансировщика нагрузки.
* **Журналы проверки работоспособности:** можно использовать этот журнал tooview проблемы, обнаруженные с вашей проверки работоспособности, например hello число экземпляров в пуле серверной части, которые не получает запросы от подсистемы балансировки нагрузки hello из-за сбоев пробы работоспособности. Этот журнал записывается toowhen изменяется состояние проверки работоспособности hello.

> [!IMPORTANT]
> Служба Log Analytics в настоящее время работает только для подсистем балансировки нагрузки с выходом в Интернет. Журналы доступны только для ресурсов, развернутых в модели развертывания диспетчера ресурсов hello. Нельзя использовать журналы для ресурсов в hello классической модели развертывания. Дополнительные сведения о моделях развертывания hello см. в разделе [сведения о диспетчере ресурсов и классического развертывания](../azure-resource-manager/resource-manager-deployment-model.md).

## <a name="enable-logging"></a>Включение ведения журналов

Ведение журналов автоматически включается для каждого ресурса Resource Manager. Требуется tooenable событий и toostart ведения журнала проверки работоспособности, сбор данных hello, доступные через эти журналы. Используйте следующие ведения журнала tooenable действия hello.

Вход toohello [портал Azure](http://portal.azure.com). Если у вас еще нет балансировщика нагрузки, [создайте балансировщик нагрузки](load-balancer-get-started-internet-arm-ps.md) перед продолжением.

1. На портале hello щелкните **Обзор**.
2. Выберите элемент **Подсистемы балансировки нагрузки**.

    ![портал — балансировщик нагрузки](./media/load-balancer-monitor-log/load-balancer-browse.png)

3. Выберите существующую подсистему балансировки нагрузки, затем щелкните **Все параметры**.
4. Hello правой части диалогового окна hello под именем hello подсистемы балансировки нагрузки hello, прокрутите слишком**мониторинг**, нажмите кнопку **диагностики**.

    ![портал — балансировщик нагрузки — параметры](./media/load-balancer-monitor-log/load-balancer-settings.png)

5. В hello **диагностики** панели в разделе **состояние**выберите **на**.
6. Щелкните элемент **Учетная запись хранения**.
7. В разделе **Журналы** выберите существующую учетную запись хранения или создайте новую. Используйте ползунок toodetermine hello сколько дней, данные события сохраняются в журналах событий hello. 
8. Щелкните **Сохранить**.

    ![Портал — журналы диагностики](./media/load-balancer-monitor-log/load-balancer-diagnostics.png)

> [!NOTE]
> Для журналов аудита отдельная учетная запись хранения не требуется. Здравствуйте, использования хранилища для событий и работоспособности пробы ведение журнала будет взиматься плата службы.

## <a name="audit-log"></a>Журнал аудита

журнал аудита Hello создается по умолчанию. журналы Hello сохраняются в течение 90 дней в хранилище Azure журналы событий. Дополнительные сведения об этих журналов, считывая hello [просматривать события и журналы аудита](../monitoring-and-diagnostics/insights-debugging-with-events.md) статьи.

## <a name="alert-event-log"></a>Журнал событий оповещений

Этот журнал создается только в том случае, если он включен для конкретной подсистемы балансировки нагрузки. Hello событий регистрируется в формате JSON и сохраняется в hello учетной записи хранения, которая была указана при включении ведения журнала hello. Hello ниже приведен пример события.

```json
{
    "time": "2016-01-26T10:37:46.6024215Z",
    "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
    "category": "LoadBalancerAlertEvent",
    "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
    "operationName": "LoadBalancerProbeHealthStatus",
    "properties": {
        "eventName": "Resource Limits Hit",
        "eventDescription": "Ports exhausted",
        "eventProperties": {
            "public ip address": "40.117.227.32"
        }
    }
}
```

Hello JSON выходных данных показано hello *eventname* оповещение создано свойство, описывающий причину hello hello подсистемы балансировки нагрузки. В этом случае hello предупреждение создано был должен за источника, который ограничивает IP NAT нехватку портов tooTCP (SNAT).

## <a name="health-probe-log"></a>Журнал проверки работоспособности

Этот журнал создается только в том случае, если он включен для конкретного балансировщика нагрузки, как описано выше. Hello данные хранятся в учетной записи хранения hello, которая была указана при включении ведения журнала hello. Контейнер с именем «аналитика журналов loadbalancerprobehealthstatus» создается и регистрируется hello следующие данные:

```json
{
    "records":[
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 1,
            "healthPercentage": 50.000000
        }
    },
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 0,
            "healthPercentage": 100.000000
        }
    }]
}
```

выходные данные JSON Hello показывает hello свойства поля hello основных сведений о состоянии работоспособности пробы hello. Hello *dipDownCount* показывает общее количество экземпляров hello на Тыловой hello, которой не поступают сетевого трафика из-за toofailed проверки ответов.

## <a name="view-and-analyze-hello-audit-log"></a>Просмотр и анализ журналов аудита hello

Можно просматривать и анализировать данные журнала аудита с помощью любого из следующих методов hello.

* **Инструменты Azure:** получать сведения из журналов аудита hello через Azure PowerShell, hello Azure интерфейс командной строки (CLI), hello Azure REST API или hello портал предварительной версии Azure. Пошаговые инструкции для каждого метода описаны в hello [аудит операций с помощью диспетчера ресурсов](../azure-resource-manager/resource-group-audit.md) статьи.
* **Power BI.** Если у вас еще нет учетной записи [Power BI](https://powerbi.microsoft.com/pricing), вы можете использовать бесплатную пробную версию. С помощью hello [журналов аудита Azure пакет содержимого для Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), можно анализировать данные с помощью предварительно настроенных панелей мониторинга или toosuit представлений можно настроить вашим требованиям.

## <a name="view-and-analyze-hello-health-probe-and-event-log"></a>Просмотр и анализ проверки работоспособности hello и журнал событий

Требуется хранилище tooyour tooconnect учетной записи и получения записи журнала hello JSON для проверки журналов событий и работоспособности. После загрузки файлов JSON hello, их можно преобразовать tooCSV и view в Excel, PowerBI или другого средства визуализации данных.

> [!TIP]
> Если вы знакомы с Visual Studio и основные понятия, связанные изменения значений константы и переменные в C#, можно использовать hello [входа преобразователь средства](https://github.com/Azure-Samples/networking-dotnet-log-converter) GitHub доступны.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Визуализация журналов аудита Azure с помощью Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) .
* [Просмотр и анализ журналов аудита Azure с помощью Power BI и других средств](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) .

## <a name="next-steps"></a>Дальнейшие действия

[Проверки балансировщика нагрузки](load-balancer-custom-probe-overview.md)
