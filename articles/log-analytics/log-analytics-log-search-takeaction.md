---
title: "aaaUser Azure Automation Runbook действие, инициируемое в службе анализа журналов | Документы Microsoft"
description: "В этой статье описывается, как toorun runbook автоматизации из службы анализа журналов поиск результат по требованию."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 53c25431572babd5fd54bf964e4683077e2a4c2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="take-action-with-an-automation-runbook-from-a-log-analytics-log-search-result"></a>Выполнение действия с Runbook службы автоматизации на основе результатов поиска Log Analytics

В результате поиска журнала в службе анализа журналов Azure теперь можно выбрать **действие** toorun runbook автоматизации.  Hello его можно использовать tooremediate hello проблема выполнение некоторых действий, таких как собирать сведения об устранении неполадок, отправьте сообщение электронной почты или создание запроса на обслуживание. 

## <a name="components-and-features-used"></a>Используемые компоненты и функции
* [Учетная запись службы автоматизации Azure](../automation/automation-offering-get-started.md)
* [Рабочая область Log Analytics](../log-analytics/log-analytics-overview.md)

## <a name="tooinitiate-runbook-from-log-search"></a>tooinitiate runbook из поиска журналов

Действие tootake на события и инициирование runbook из результатов поиска журналов, сначала нужно создать поиска журналов и результатов hello можно вызвать runbook по запросу.  Это можно сделать из hello функция поиска журналов в hello Azure или [портал OMS](../log-analytics/log-analytics-log-searches.md).  В этом примере мы выполняется поиск журнала из hello портал Azure с basic демонстрацию этой функции.

1. В hello портал Azure, hello концентратора пункт меню **дополнительные службы** и выберите **анализа журналов**.  
2. В колонке анализа журналов hello, выберите рабочую область службы анализа журналов и колонке hello рабочей области выберите **поиска журналов**.  
3. В колонке hello поиска журналов выполните поиск журнала.  
4. Из результатов поиска журналов hello, нажмите кнопку слева toohello эллипса hello одного полей hello и из контекстного меню hello, выберите **реагировать на**.<br><br> ![Выбор "Выполнить действие" в результатах поиска](./media/log-analytics-log-search-takeaction/log-search-takeaction-menuoption.png) 
5. Hello Take действие колонке выберите **запуск runbook**и на hello **запуск runbook** колонки, можно выбрать runbook toorun.  Можно выбрать любого модуля runbook в учетной записи автоматизации, является рабочей областью аналитики журналов связанного toohello hello.  Обратите внимание hello следующие:

    * Модули runbook группируются по тегам.
    * Значения входных параметров Runbook можно выбрать непосредственно из поля hello hello результат поиска.  Раскрывающегося списка будет отображаться все доступные поля hello из tooselect результат hello из.  
    * Вы можете toorun hello runbook [гибридной рабочей ролью runbook](../automation/automation-hybrid-runbook-worker.md) , установки на компьютере hello с проблемой hello, при наличии соответствующих групп гибридную рабочую роль Runbook, содержит только эту машину как член.  Если имя hello группу гибридных рабочих ролей hello совпадает имя hello hello компьютера, находящегося в результат поиска журнала hello, hello группы выбирается автоматически.    

6. После нажатия кнопки **запуска**, колонки задания runbook Привет открыть tooallow вы tooreview hello состояние hello задания.   

При выборе модуля runbook, который был настроенных toobe [вызывается из предупреждения анализа журналов](../automation/automation-invoke-runbook-from-omsla-alert.md), она имеет входной параметр **WebhookData** , **объект** типа.  Если входной параметр hello является обязательной, необходимо toopass hello поиска результаты toohello runbook, чтобы его можно преобразовать строку в формате JSON hello в тип объекта, позволяя toofilter для конкретных элементов, которые будет ссылаться в действия runbook.  Это можно сделать, выбрав **(Object) результат поиска** из раскрывающегося списка hello.<br><br> ![Выбор объекта данных Webhook для параметра runbook](media/log-analytics-log-search-takeaction/select-runbook-and-properties.png)   
    
## <a name="next-steps"></a>Дальнейшие действия

* Просмотрите hello [Справочник поиска журнала анализа журналов](log-analytics-search-reference.md) tooview все hello поиск поля и аспекты, доступных в службе анализа журналов.
* как автоматически, проверьте tooinvoke runbook автоматизации toolearn [вызов runbook службы автоматизации Azure из службы анализа журналов OMS предупреждение](../automation/automation-invoke-runbook-from-omsla-alert.md).  
