---
title: "рекомендации по aaaOMSManagement решения | Документы Microsoft"
description: 
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
ms.date: 04/27/2017
ms.author: bwren
ms.openlocfilehash: 08cf1c101e301d24fb5c2bf4bc02a978e508a198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-creating-management-solutions-in-operations-management-suite-oms-preview"></a>Рекомендации по созданию решений для управления в Operations Management Suite (OMS) (предварительная версия)
> [!NOTE]
> Это предварительная документация для создания решений для управления в консоли OMS, которая доступна в данный момент в режиме предварительной версии. Ни одной схеме, описанной ниже — toochange субъекта.  

В этой статье приводятся рекомендации по [созданию файла решения для управления](operations-management-suite-solutions-solution-file.md) в Operations Management Suite (OMS).  Эти сведения будут обновляться по мере появления дополнительных рекомендаций.

## <a name="data-sources"></a>Источники данных
- Источники данных можно [настроить с помощью шаблона Resource Manager](../log-analytics/log-analytics-template-workspace-configuration.md), но их не следует включать в файл решения.  Hello обусловлено, Настройка источников данных не в настоящее время это означает, что решение может перезаписать существующую конфигурацию в рабочей области пользователя hello идемпотентными.<br><br>Например решение может потребоваться события предупреждений и ошибок из журнала событий приложения hello.  Если это указать в качестве источника данных в решении, то существует риск удаление информацию о событиях, если у пользователя hello, настройки в рабочей области.  Если включены все события, затем вы может собирать избыточные сведения события в рабочей области пользователя hello.

- Если решение требует данные из одной hello стандартных источников данных, необходимо определить это как необходимый компонент.  Состояния в документации по этому клиенту hello необходимо настроить hello источник данных по отдельности.  
- Добавить [проверке потока данных](../log-analytics/log-analytics-view-designer-tiles.md) собранные сообщения tooany представления в пользователя hello tooinstruct решения на источниках данных, необходимость toobe, настроенных для toobe необходимых данных.  Это сообщение отображается на плитке приветствия hello представления, когда не удалось найти необходимые данные.


## <a name="runbooks"></a>Модули Runbook
- Добавить [расписание автоматизации](../automation/automation-schedules.md) для каждого модуля runbook в решении, для которого требуется toorun по расписанию.
- Включить hello [IngestionAPI модуль](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) в вашей toobe решение использовать модули Runbook записи данных toohello анализа журналов репозитория.  Настройка решения hello слишком[ссылки](operations-management-suite-solutions-solution-file.md#solution-resource) этот ресурс, так что он остается при удалении решения hello.  Это позволяет модулю hello tooshare несколько решений.
- Используйте [переменных автоматизации](../automation/automation-schedules.md) tooprovide значения toohello решение, что пользователям руководств может пригодиться toochange позже.  Даже если решение hello настроенных toocontain hello переменной, это значение можно изменить по-прежнему.

## <a name="views"></a>Views
- Все решения должно включать одно представление, отображаемое в hello пользовательского портала.  Hello представление может содержать несколько [визуализации частей](../log-analytics/log-analytics-view-designer-parts.md) tooillustrate различных наборов данных.
- Добавить [проверке потока данных](../log-analytics/log-analytics-view-designer-tiles.md) собранные сообщения tooany представления в пользователя hello tooinstruct решения на источниках данных, необходимость toobe, настроенных для toobe необходимых данных.
- Настройка решения hello слишком[содержат](operations-management-suite-solutions-solution-file.md#solution-resource) hello представление, чтобы он удаляется при удалении решения hello.

## <a name="alerts"></a>Оповещения
- Определяет список получателей hello как параметр в файле решения hello, поэтому пользователь hello их можно определить при установке решения hello.
- Настройка решения hello слишком[ссылки](operations-management-suite-solutions-solution-file.md#solution-resource) правила оповещения так, он может изменять свои параметры.  Им хотелось toomake изменения, такие как изменение списка получателей hello, изменение hello пороговое значение предупреждения hello или отключить правило генерации оповещений hello. 


## <a name="next-steps"></a>Дальнейшие действия
* Показывает, как процесс basic hello [проектирование и создание решения управления](operations-management-suite-solutions-creating.md).
* Узнайте, каким образом слишком[создайте файл решения](operations-management-suite-solutions-solution-file.md).
* [Добавьте сохраненные поисковые запросы и оповещения](operations-management-suite-solutions-resources-searches-alerts.md) tooyour решение для управления.
* [Добавление представления](operations-management-suite-solutions-resources-views.md) tooyour решение для управления.
* [Добавить Runbook автоматизации и другим ресурсам](operations-management-suite-solutions-resources-automation.md) tooyour решение для управления.

