---
title: "aaaWhat возможности анализа журналов в Operations Management Suite (OMS) | Документация Майкрософт"
description: "Log Analytics — это служба в Operations Management Suite (OMS), которая помогает собирать и анализировать операционные данные, формируемые ресурсами в облачных и локальных средах.  В этой статье содержит краткий обзор различных компонентов hello анализа журналов и содержимого toodetailed ссылки."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: bd90b460-bacf-4345-ae31-26e155beac0e
ms.service: log-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/12/2017
ms.author: bwren
ms.openlocfilehash: b35da77e3782f7c1fe54cc34142f8cd9f2eb57d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-log-analytics"></a>Что такое Log Analytics?
Аналитика журналов представляет собой службу в [Operations Management Suite \(OMS\) ](../operations-management-suite/operations-management-suite-overview.md) , отслеживает вашего облака и локальных сред toomaintain их доступности и производительности.  Он собирает данные, созданные ресурсы в облачных и локальных сред и других мониторинга анализа tooprovide средства в нескольких источниках.  Эта статья содержит краткое описание значение hello, аналитика журналов Общие сведения, как он работает, и toomore ссылки подробные содержимое, поэтому вы можете более дальнейшей.

## <a name="is-log-analytics-for-you"></a>Подходит ли вам Log Analytics?
Если у вас нет средства мониторинга среды Azure, мы рекомендуем использовать [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview.md). Эта платформа собирает и анализирует данные мониторинга для ресурсов Azure.  Служба аналитики журналов может [сбора данных из монитора Azure](log-analytics-azure-storage.md) toocorrelate его с другими данными и обеспечивают дополнительный анализ.

Если требуется toomonitor в локальной среде, или у вас есть существующий мониторинга с помощью службы, такие как монитор Azure или System Center Operations Manager, аналитика журналов можно добавить существенное значение.  Эта служба собирает данные непосредственно из агентов, а также из других средств в едином репозитории.  Средства анализа в Log Analytics, такие как поиск по журналам, представления и решения, обрабатывают все собранные данные, предоставляя централизованный анализ всей среды.


## <a name="using-log-analytics"></a>Использование Log Analytics
Служба аналитики журналов доступны через портал OMS hello или hello портал Azure, которая выполняться в любом браузере, предоставляют вам tooconfiguration параметры доступа и tooanalyze несколько средств и отреагировать на собранных данных.  Из портала hello можно использовать [входа выполняет](log-analytics-log-searches.md) при построении запросов tooanalyze собранных данных, [панелей мониторинга](log-analytics-dashboards.md) которого можно настроить с графическим отображением наиболее полезен, выполнять поиск, и [решения](log-analytics-add-solutions.md) предоставляющие дополнительные инструменты анализа и функциональные возможности.

ниже рисунке Hello взят из портала OMS hello какие показано hello панели мониторинга отображаются сводные данные для hello [решения](#add-functionality-with-management-solutions) , установленных в рабочей области hello.  Можно щелкнуть любой toodrill плитки дальнейшей hello данных для этого решения.

![Портал OMS](media/log-analytics-overview/portal.png)

Служба аналитики журналов включает извлечь tooquickly языка запросов и консолидировать данные в репозиторий hello.  Можно создать и сохранить [запросов поиска журналов](log-analytics-log-searches.md) toodirectly анализа данных в портале hello или запросов поиска журналов выполнялись автоматически toocreate оповещения если hello результатах запроса hello важное условие.

![Поиск по журналам](media/log-analytics-overview/log-search.png)

tooget быстрого графическое представление работоспособности hello общей среды можно добавлять визуализации для tooyour выполняет сохраненный журнал [мониторинга](log-analytics-dashboards.md).   

![Панель мониторинга](media/log-analytics-overview/dashboard.png)

В данные о заказах tooanalyze за пределами службы анализа журналов, можно экспортировать данные hello из репозитория OMS hello в средства например [Power BI](log-analytics-powerbi.md) или Excel.  Можно также использовать hello [API поиска журналов](log-analytics-log-search-api.md) toobuild пользовательские решения, использующие данные аналитики журнала или toointegrate с другими системами.

## <a name="add-functionality-with-management-solutions"></a>Добавление возможностей с помощью решений по управлению
[Решения для управления](log-analytics-add-solutions.md) добавить tooOMS функциональность, предоставляя дополнительные данные и tooLog средства анализа Analytics.  Они также могут определять новые типы записей toobe собираются, можно проанализировать с помощью запросов поиска журналов или дополнительный пользовательский интерфейс, предоставляемый решение hello в панель мониторинга hello.  Изображение примера Hello ниже показано hello [решения для отслеживания изменений](log-analytics-change-tracking.md)

![Решение для отслеживания изменений](media/log-analytics-overview/change-tracking.png)

Существуют решения для самых разных функций. Но помимо доступных решений постоянно добавляются также и новые.  Можно легко просматривать доступные решения и [добавить их в рабочей области OMS tooyour](log-analytics-add-solutions.md) из коллекции решений hello или Azure Marketplace.  Многие из них развертываются автоматически и начинают работать сразу, а другие требуют определенной настройки.

![Коллекция решений](media/log-analytics-overview/solution-gallery.png)

## <a name="log-analytics-components"></a>Компоненты службы Log Analytics
Hello центр аналитика журналов является hello репозиторий OMS, размещаемой в облаке Azure hello.  Данные собираются в репозиторий hello из подключенных источников по настройке источников данных и Добавление подписки tooyour решения.  Источники данных и решений каждого создаст записей различных типов, которые имеют свой собственный набор свойств, но может по-прежнему проанализировать вместе в репозиторий toohello запросов.  Это позволяет toouse hello же toowork средств и методов с разными типами данных, собираемых различных источников.

![Репозиторий OMS](media/log-analytics-overview/overview.png)

Подключенные источники являются hello компьютерам и другим ресурсам, которые создают данные, собранные службой аналитики журналов.  К этим источникам относятся агенты, установленные на компьютеры [Windows](log-analytics-windows-agents.md) и [Linux](log-analytics-linux-agents.md), подключенные напрямую, или агенты в [подключенной группе управления System Center Operations Manager](log-analytics-om-agents.md).  Log Analytics собирает данные ресурсов Azure с [Azure Monitor и системы диагностики Azure](log-analytics-azure-storage.md).

[Источники данных](log-analytics-data-sources.md) hello разных типов данных, собранных из каждого подключенного источника.  Сюда входят [событий](log-analytics-data-sources-windows-events.md) и [данные о производительности](log-analytics-data-sources-performance-counters.md) из [Windows](log-analytics-data-sources-windows-events.md) агентов и Linux в toosources сложения, например [журналы IIS](log-analytics-data-sources-iis-logs.md)и [настраиваемые текстовые журналы](log-analytics-data-sources-custom-logs.md).  Можно настроить каждый источник данных, что требуется toocollect и конфигурации hello автоматически доставленный tooeach подключенного источника.

Если у вас есть особые требования, к, то можно использовать hello [HTTP API-Интерфейс сборщика данных](log-analytics-data-collector-api.md) репозитории toohello toowrite данных от клиента REST API.

## <a name="log-analytics-architecture"></a>Архитектура службы Log Analytics
требования к развертыванию Hello аналитики журналов минимальны, поскольку hello центра компоненты размещаются в облаке Azure hello.  Добавление toohello служб, которые позволяют вам toocorrelate и анализировать собранные данные в нем hello репозитория.  могут ли посещать портал Hello из любого браузера, поэтому нет необходимости для клиентского программного обеспечения.

Агенты необходимо устанавливать на компьютеры [Windows](log-analytics-windows-agents.md) и [Linux](log-analytics-linux-agents.md), но для компьютеров, которые уже входят в [подключенную группу управления SCOM](log-analytics-om-agents.md), дополнительный агент не требуется.  SCOM агенты по-прежнему toocommunicate с серверами управления, которые будет отправлять свои данные tooLog Analytics.  Однако некоторые решения потребуется toocommunicate агентов непосредственно с помощью аналитики журналов.  Hello документацию для каждого решения указывается его требования к подключениям.

[Регистрируясь в службе Log Analytics](log-analytics-get-started.md), вы создаете рабочую область OMS.  Hello рабочую область можно считать уникальной средой анализа журналов с собственный репозиторий данных, источники данных и решений. Можно создать несколько рабочих областей в вашей подписке toosupport несколько сред, таких как производственная и тестирования.

![Архитектура службы Log Analytics](media/log-analytics-overview/architecture.png)

## <a name="next-steps"></a>Дальнейшие действия
* [Зарегистрируйтесь для получения бесплатной учетной записи службы анализа журналов](log-analytics-get-started.md) tootest в собственной среде.
* Представление hello различных [источники данных](log-analytics-data-sources.md) toocollect доступные данные в репозиторий OMS hello.
* [Обзор hello решения, доступные в коллекции решений hello](log-analytics-add-solutions.md) tooLog tooadd функциональные возможности анализа.

