---
title: "aaaEnable ведения журналов диагностики для событий пакетных - Azure | Документы Microsoft"
description: "Запись и анализ событий журнала диагностики для ресурсов учетной записи пакетной службы Azure, таких как пулы и задачи."
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: e14e611d-12cd-4671-91dc-bc506dc853e5
ms.service: batch
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9d03303a3e857e9303f40cc6de5c32b5a51d8f8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="log-events-for-diagnostic-evaluation-and-monitoring-of-batch-solutions"></a>События журнала для диагностики и мониторинга решений пакетной службы

Как и многие службы Azure hello пакетная служба создает для определенных ресурсов во время hello ресурсов hello время существования журнала событий. Можно включить события toorecord журналы диагностики пакета Azure для ресурсов, таких как пулы и задачи и затем использовать журналы hello для оценки, диагностики и мониторинга. Журналы диагностики пакетной службы содержат такие события, как создание пула, удаление пула, начало задачи, завершение задачи и т. п.

> [!NOTE]
> В этой статье описывается ведение журнала событий для ресурсов пакетной службы, а не журнала выходных данных задач и заданий. Дополнительные сведения о хранении hello выходные данные заданий и задач см. в разделе [выходные данные заданий и задач сохранения пакетной службы Azure](batch-task-output.md).
> 
> 

## <a name="prerequisites"></a>Предварительные требования
* [Учетная запись пакетной службы Azure](batch-account-create-portal.md)
* [Учетная запись хранения Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)
  
  toopersist журналы диагностики пакета, необходимо создать учетную запись хранилища Azure, где Azure будет хранить журналы hello. Эту учетную запись хранения вы укажете в процессе [включения ведения журналов диагностики](#enable-diagnostic-logging) для учетной записи пакетной службы. Hello учетной записи хранилища, укажите при включении сбора журналов не является hello таким же как hello связанное хранение учетной записи ссылка tooin [пакетов приложений](batch-application-packages.md) и [сохраняемости результат выполнения задачи](batch-task-output.md) статей.
  
  > [!WARNING]
  > Вы являетесь **плата** для hello данные, хранящиеся в вашей учетной записи хранилища Azure. К ним относятся журналы диагностики hello, рассматриваемые в данной статье. Не забывайте об этом, когда разрабатываете [политику хранения журналов](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).
  > 
  > 

## <a name="enable-diagnostic-logging"></a>Включение ведения журналов диагностики
Ведение журналов диагностики для учетной записи пакетной службы по умолчанию отключено. Необходимо явно включить сбор данных диагностики для каждой учетной записи пакета необходимо toomonitor:

[Как tooenable сбора журналов диагностики](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs)

Рекомендуется прочитать hello полного [Обзор служб Azure журналам диагностики](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) toogain статьи не только влияние ведения журнала tooenable, однако hello журнала категории понимание поддерживаемые hello различных служб Azure. Например, пакетная служба Azure в настоящее время поддерживает только одну категорию журналов: **журналы служб**.

## <a name="service-logs"></a>Журналы служб
Azure пакетной службы журналы содержат события, генерируемой hello пакетной службы Azure во время существования hello ресурса пакета как пула или задачи. Каждое событие, генерируемой пакета сохраняется в указанный hello учетной записи хранилища в формате JSON. Например, это текст hello образца **создание событий пула**:

```json
{
    "poolId": "myPool1",
    "displayName": "Production Pool",
    "vmSize": "Small",
    "cloudServiceConfiguration": {
        "osFamily": "4",
        "targetOsVersion": "*"
    },
    "networkConfiguration": {
        "subnetId": " "
    },
    "resizeTimeout": "300000",
    "targetDedicatedComputeNodes": 2,
    "maxTasksPerNode": 1,
    "vmFillType": "Spread",
    "enableAutoscale": false,
    "enableInterNodeCommunication": false,
    "isAutoPool": false
}
```

Текст каждого события находится в .json указан файл в hello учетной записи хранилища Azure. Если требуется tooaccess hello журналы напрямую, вы можете tooreview hello [схемы из журналов диагностики в учетной записи хранения hello](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).

## <a name="service-log-events"></a>События журнала службы
в настоящее время Hello пакетная служба создает hello следующие службы журнала событий. Этот список может оказаться неполным, если с момента последнего обновления этой статьи были добавлены новые события.

| **События журнала службы** |
| --- |
| [Pool create][pool_create] |
| [Pool delete start][pool_delete_start] |
| [Pool delete complete][pool_delete_complete] |
| [Pool resize start][pool_resize_start] |
| [Pool resize complete][pool_resize_complete] |
| [Task start][task_start] |
| [Task complete][task_complete] |
| [Task fail][task_fail] |

## <a name="next-steps"></a>Дальнейшие действия
Добавление toostoring событий журнала диагностики в учетную запись хранилища Azure, можно также записывать tooan пакетной службы журнала событий [концентратор событий Azure](../event-hubs/event-hubs-what-is-event-hubs.md), а затем отправить их слишком[анализа журналов Azure](../log-analytics/log-analytics-overview.md).

* [Журналы диагностики Azure поток tooEvent концентраторы](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md)
  
  Поток пакетная события диагностики toohello высокомасштабируемых данных входящих сообщений служба концентраторов событий. Концентраторы событий способны принимать миллионы событий в секунду, позволяя преобразовать и сохранять их с помощью любого поставщика аналитики в реальном времени.
* [Анализ журналов диагностики Azure с помощью Log Analytics](../log-analytics/log-analytics-azure-storage.md)
  
  Отправка в журналы диагностики tooLog Analytics, где можно проанализировать их на портале Operations Management Suite (OMS) hello или экспортировать их для анализа в Power BI или Excel.

[pool_create]: https://msdn.microsoft.com/library/azure/mt743615.aspx
[pool_delete_start]: https://msdn.microsoft.com/library/azure/mt743610.aspx
[pool_delete_complete]: https://msdn.microsoft.com/library/azure/mt743618.aspx
[pool_resize_start]: https://msdn.microsoft.com/library/azure/mt743609.aspx
[pool_resize_complete]: https://msdn.microsoft.com/library/azure/mt743608.aspx
[task_start]: https://msdn.microsoft.com/library/azure/mt743616.aspx
[task_complete]: https://msdn.microsoft.com/library/azure/mt743612.aspx
[task_fail]: https://msdn.microsoft.com/library/azure/mt743607.aspx
