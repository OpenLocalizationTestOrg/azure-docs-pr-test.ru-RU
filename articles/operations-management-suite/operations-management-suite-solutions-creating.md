---
title: "в службе OMS это решение для управления aaaBuild | Документы Microsoft"
description: "Решения для управления расширить функциональность hello Operations Management Suite (OMS), предоставляя сценариев пакете управления, клиентам можно добавить tootheir рабочей области OMS.  Эта статья содержит сведения по созданию toobe решений управления используется в вашей рабочей среде или сделаны доступными tooyour клиентов."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1915e204-ba7e-431b-9718-9eb6b4213ad8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/20/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: dea4c0d9e608d9fe4aa41088705958c9fe999372
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="design-and-build-a-management-solution-in-operations-management-suite-oms-preview"></a>Проектирование и создание решения по управлению в Operations Management Suite (OMS) (предварительная версия)
> [!NOTE]
> Это предварительная документация для создания решений для управления в консоли OMS, которая доступна в данный момент в режиме предварительной версии. Ни одной схеме, описанной ниже — toochange субъекта.

[Решения для управления](operations-management-suite-solutions.md) расширить функциональность hello Operations Management Suite (OMS), предоставляя сценариев пакете управления, клиентам можно добавить tootheir рабочей области OMS.  В этой статье представлены toodesign базовый процесс и построения решения по управлению, подходящий для наиболее распространенных.  При наличии новых решений по управлению toobuilding, вы можете использовать этот процесс в качестве отправной точки и затем использовать основные понятия hello для более сложных решений в случае изменения требований.

## <a name="what-is-a-management-solution"></a>Что такое решение по управлению?

Решения управления содержат OMS и ресурсах Azure, которые работают совместно tooachieve того или иного сценария мониторинга.  Они реализованы в виде [управление ресурсами шаблоны](../azure-resource-manager/resource-manager-template-walkthrough.md) , которые содержат подробные сведения о том, как tooinstall и настроить их автономной ресурсы, после установки решения hello.

Здравствуйте, основная стратегия является toostart решения по управлению путем создания отдельных компонентов hello в вашей среде Azure.  После правильной работе функции hello, затем можно запустить их в упаковку [файл решения управления](operations-management-suite-solutions-solution-file.md). 


## <a name="design-your-solution"></a>Разработка решения
наиболее распространенным шаблоном Hello как решения для управления отображается в hello следующие схемы.  Hello различные компоненты в этом шаблоне рассматриваются в hello ниже.

![Обзор решения OMS](media/operations-management-suite-solutions/solution-overview.png)


### <a name="data-sources"></a>Источники данных
Hello первым шагом при разработке решения является определение hello данные, которые требуют из репозитория hello анализа журналов.  Эти данные могут быть собранные [источника данных](../log-analytics/log-analytics-data-sources.md) или [другое решение](operations-management-suite-solutions.md), или решения может потребоваться tooprovide hello процесса toocollect его.

Существует несколько способов источники данных, которые могут быть собраны в репозитории hello анализа журналов, как описано в [источники данных в службе анализа журналов](../log-analytics/log-analytics-data-sources.md).  Это включает в себя события в журнал событий Windows hello или созданные Syslog Кроме tooperformance счетчики для клиентов Windows и Linux.  Вы также можете собирать данные из ресурсов Azure, полученных службой Azure Monitor.  

Если необходимо использовать данные, не доступны через все hello доступных источников данных, то можно использовать hello [HTTP API-Интерфейс сборщика данных](../log-analytics/log-analytics-data-collector-api.md) позволяющее репозитории анализа журналов toohello toowrite данных из любого клиента, который можно вызвать REST API-ИНТЕРФЕЙС.  Hello наиболее распространенных средств сбора пользовательских данных в решении для управления является toocreate [runbook в автоматизации Azure](../automation/automation-runbook-types.md) , собирает hello необходимые данные из Azure или внешние ресурсы и использует hello toowrite API-Интерфейс сборщика данных toohello репозиторий.  

### <a name="log-searches"></a>Поиск по журналам
[Поиск журнала](../log-analytics/log-analytics-log-searches.md) , используемые tooextract и анализировать данные в репозиторий hello анализа журналов.  Они используются представления и оповещений в дополнение tooallowing hello пользователя tooperform нерегламентированный анализ данных в репозитории hello.  

Следует определить все запросы, которые вы считаете, что будет полезно toohello пользователь, даже если они не используются все представления и предупреждения.  Это будут доступны toothem как сохраненные условия поиска в портале hello, а также могут быть заданы в [визуализации части списка запросов](../log-analytics/log-analytics-view-designer-parts.md#list-of-queries-part) в представлении.

### <a name="alerts"></a>Оповещения
[Предупреждения в службе анализа журналов](../log-analytics/log-analytics-alerts.md) идентификации ошибок с помощью [входа выполняет](#log-searches) данных hello в репозиторий hello.  Они уведомлять пользователя hello или автоматически выполнять действия в ответ. Вы должны определить разные условия оповещений для приложения и включить соответствующие правила оповещений в файл решения.

Если проблема hello потенциально могут исправляться посредством автоматизированного процесса, затем обычно создается runbook в автоматизации Azure tooperform этого исправления.  Большинство служб Azure можно управлять с помощью [командлеты](/powershell/azure/overview) какие hello runbook будет использовать tooperform такие функциональные возможности.

Если решение требует внешних функциональных возможностей в предупреждении tooan ответ, то можно использовать [ответа веб-перехватчика](../log-analytics/log-analytics-alerts-actions.md).  Это позволяет вам toocall внешней веб-службе, отправке информации из hello предупреждение.

### <a name="views"></a>Views
Представления в службе анализа журналов, используемых toovisualize данными из репозитория анализа журналов hello.  Каждое решение обычно будет содержать одно представление с [плитки](../log-analytics/log-analytics-view-designer-tiles.md) , отображаемое на главной информационной hello пользователя.  Hello представление может содержать любое количество [визуализации частей](../log-analytics/log-analytics-view-designer-parts.md) tooprovide зрительные пользователя toohello hello собранных данных.

Вы [создавать пользовательские представления, с помощью конструктора представлений hello](../log-analytics/log-analytics-view-designer.md) которого можно позднее экспортировать для включения в файл решения.  


## <a name="create-solution-file"></a>Создание файла решения
После настройки и тестирования hello компоненты, которые должны быть частью решения, вы можете [создайте файл решения](operations-management-suite-solutions-solution-file.md).  Будет реализовывать hello компоненты решения в [шаблона диспетчера ресурсов](../azure-resource-manager/resource-group-authoring-templates.md) , включающего [ресурсов](operations-management-suite-solutions-solution-file.md#solution-resource) с toohello связи другие ресурсы в hello файла.  


## <a name="test-your-solution"></a>Тестирование решения
При разработке решения может потребоваться tooinstall и тестировать их в рабочей области.  Это можно сделать с помощью любой из доступных методов hello слишком[проверить и установить шаблоны диспетчера ресурсов](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="publish-your-solution"></a>Опубликуйте свое решения
После завершения и тестирование решения, вы можете сделать доступной toocustomers через либо hello следующие источники.

- **Шаблоны быстрого запуска Azure**.  [Шаблоны Azure краткое руководство](https://azure.microsoft.com/resources/templates/) — это набор шаблонов диспетчера ресурсов, предоставленного сообществом hello через GitHub.  Выполненные решения доступны следующие сведения в hello [руководство по участию в](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE).
- **Azure Marketplace**.  Hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/) позволяет toodistribute и продавать решения tooother разработчиков, разработчиков и ИТ-специалистов.  Рассказывается, как toopublish вашего решения tooAzure Marketplace в [как toopublish и управлять ими в Azure Marketplace hello предложение](../marketplace-publishing/marketplace-publishing-getting-started.md).



## <a name="next-steps"></a>Дальнейшие действия
* Узнайте, каким образом слишком[создайте файл решения](operations-management-suite-solutions-solution-file.md) для решения управления.
* Узнайте подробности hello [шаблоны разработки Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).
* Найдите в коллекции [шаблонов быстрого запуска Azure](https://azure.microsoft.com/documentation/templates) примеры разных шаблонов Resource Manager.