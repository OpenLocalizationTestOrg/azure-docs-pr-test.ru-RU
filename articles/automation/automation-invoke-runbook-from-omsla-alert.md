---
title: "aaaCalling Runbook автоматизации Azure из предупреждение аналитика журналов | Документы Microsoft"
description: "В этой статье содержатся общие сведения о том, как tooinvoke runbook автоматизации из предупреждения анализа журналов OMS корпорации Майкрософт."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/31/2017
ms.author: magoedte
ms.openlocfilehash: 8b745d6e6c2b0294d676e010f52855cd51741cf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="calling-an-azure-automation-runbook-from-an-oms-log-analytics-alert"></a>Вызов модуля Runbook службы автоматизации Azure из оповещения OMS Log Analytics

При настройке предупреждения в службе анализа журналов toocreate запись предупреждения, если результаты соответствуют определенным условиям, например длительного пика загрузки процессора или процесс для конкретного приложения критические toohello функциональные возможности бизнес-приложения завершается ошибкой и записывает соответствующее событие в журнале событий Windows hello, что оповещение автоматически можно запустить runbook автоматизации в tooauto попытки-устранять проблему hello.  

Существует два toocall параметры модуля runbook при настройке предупреждения hello.   В частности:

1. Использование объекта Webhook.
   * Это hello единственный доступный параметр, если рабочую область OMS не tooan связанной учетной записи автоматизации.
   * При наличии рабочей области OMS tooan связанной учетной записи автоматизации, этот параметр по-прежнему доступен.  

2. Непосредственный выбор модуля Runbook.
   * Этот параметр доступен только в том случае, если рабочая область OMS hello — tooan связанной учетной записи автоматизации.  

## <a name="calling-a-runbook-using-a-webhook"></a>Вызов модуля Runbook с помощью объекта Webhook

Веб-перехватчика позволяет toostart конкретного модуля runbook в автоматизации Azure через один HTTP-запроса.  Перед настройкой hello [предупреждение анализа журналов](../log-analytics/log-analytics-alerts.md#alert-rules) runbook toocall hello, используя веб-перехватчик в качестве реакции на предупреждение, вам потребуется toofirst создать веб-перехватчика для hello runbook, который будет вызываться с помощью этого метода.  Просмотрите и следуйте указаниям hello hello [создать веб-перехватчика](automation-webhooks.md#creating-a-webhook) статью и запомнить URL-адрес веб-перехватчика toorecord hello, чтобы вы могли сослаться при настройке правила оповещения hello.   

## <a name="calling-a-runbook-directly"></a>Непосредственный вызов модуля Runbook

Если у вас есть hello автоматизации & предложения управления устанавливается и настраивается в рабочую область OMS, при настройке параметра действия Runbook hello для оповещения hello, можно просмотреть все модули Runbook из hello **выберите runbook** раскрывающегося списка и выберите hello требуется toorun в предупреждении toohello ответа определенного модуля runbook.  Hello выбранного модуля runbook можно запускать в рабочей области в облаке Azure hello или на гибридной рабочей роли runbook.  При создании с помощью параметра runbook hello предупреждение hello веб-перехватчика будут созданы для hello runbook.  Если перейти учетной записи автоматизации toohello и перейдите в колонку веб-перехватчика toohello hello выбранного модуля Runbook вы увидите веб-перехватчика hello.  При удалении предупреждения hello hello веб-перехватчика не удаляется, но hello пользователь может вручную удалить веб-перехватчика hello.  Он не является проблемой, если веб-перехватчика hello не удаляется, это просто потерянных элемента, который рано или поздно toobe удаления в порядке toomaintain организованную учетной записи автоматизации.  

## <a name="characteristics-of-a-runbook-for-both-options"></a>Характеристики модуля Runbook (для обоих способов)

Оба метода для вызова модуля runbook hello из предупреждения анализа журналов hello имеют характеристики по-разному, которые должны toobe понятны перед настройкой правилами генерации оповещений.  

* Для модуля Runbook необходим входной параметр с именем **WebhookData** и типом **Object**.  Этот параметр может быть обязательным или необязательным.  Предупреждение Hello передает hello результаты поиска toohello runbook с помощью этого входного параметра.

        param  
         (  
          [Parameter (Mandatory=$true)]  
          [object] $WebhookData  
         )

*  Необходимо иметь код tooconvert hello WebhookData tooa объект PowerShell.

    `$SearchResults = (ConvertFrom-Json $WebhookData.RequestBody).SearchResults.value`

    *$SearchResults* будет массивом объектов, каждый объект содержит hello поля со значениями из результатов поиска

### <a name="webhookdata-inconsistencies-between-hello-webhook-option-and-runbook-option"></a>WebhookData несоответствия между hello веб-перехватчика и runbook

* При настройке оповещений toocall веб-перехватчика, введите URL-адрес веб-перехватчика, созданных для модуля runbook и нажмите кнопку hello **тестирования веб-перехватчика** кнопки.  Hello результирующий WebhookData отправляемых toohello runbook не содержит либо *. SearchResult* или *. SearchResults*.

*  При сохранении этого предупреждения, когда предупреждение hello триггеров и вызывает веб-перехватчика hello hello WebhookData отправляемых toohello runbook содержит *. SearchResult*.
* Если создать предупреждение и настроить его toocall runbook (который также создает веб-перехватчика), когда hello предупреждения триггеры, он отправляет WebhookData toohello runbook, который содержит *. SearchResults*.

Поэтому в приведенном выше примере кода hello, нужно будет tooget *. SearchResult* Если предупреждение hello вызывает веб-перехватчика и потребуется tooget *. SearchResults* Если предупреждение hello вызывает runbook напрямую.

## <a name="example-walkthrough"></a>Пошаговое руководство по примеру

Мы покажем, как это работает, используя следующий пример графический runbook, который используется для запуска службы Windows hello.<br><br> ![Графический модуль Runbook запуска службы Windows](media/automation-invoke-runbook-from-omsla-alert/automation-runbook-restartservice.png)<br>

Hello runbook имеет один входной параметр типа **объекта** , вызываемого **WebhookData** и включает в себя данные веб-перехватчика hello, передаваемые от предупреждения содержащего hello *. SearchResults*.<br><br> ![Входные параметры модуля Runbook](media/automation-invoke-runbook-from-omsla-alert/automation-runbook-restartservice-inputparameter.png)<br>

Например, в службе анализа журналов мы создали два пользовательских полей, *SvcDisplayName_CF* и *SvcState_CF*, tooextract hello отображаемое имя и hello состояния службы hello службы (т. е. запущенной или остановленной) из события hello записывается toohello журнал системных событий.  Затем мы создать правило генерации оповещений с hello, следующий запрос поиска: `Type=Event SvcDisplayName_CF="Print Spooler" SvcState_CF="stopped"` , чтобы мы можно обнаружить при остановке службы диспетчера очереди печати hello на системы Windows hello.  Он может быть любой службы, представляющие интерес, но в этом примере мы ссылаются на один hello существующих служб, которые входят в состав ОС Windows hello.  действие предупреждения Hello настроенных tooexecute наших runbook, используемых в этом примере и запустите на hello гибридную рабочую роль Runbook, которой включены на целевых системах hello.   

Действие runbook кода Hello **получить имя службы из LA** преобразует строку в формате JSON hello в тип объекта и фильтр для элемента hello *SvcDisplayName_CF* tooextract hello отображаемое имя hello Службы Windows и передать этот на следующее действие hello, который проверит hello служба остановлена перед выполнением toorestart его.  *SvcDisplayName_CF* — [настраиваемое поле](../log-analytics/log-analytics-custom-fields.md) созданные в службе анализа журналов toodemonstrate в этом примере.

    $SearchResults = (ConvertFrom-Json $WebhookData.RequestBody).SearchResults.value
    $SearchResults.SvcDisplayName_CF  

При остановке службы hello, правило оповещения hello в службе анализа журналов обнаружит совпадения и запустить hello runbook и отправить runbook toohello hello контекст предупреждения. Hello runbook вступят в действие tooverify hello служба остановлена, и если поэтому попытка toorestart hello службы и для проверки правильной работы и hello вывода результатов.     

Можно также при отсутствии рабочую область OMS tooyour связанной учетной записи автоматизации можно настроить правила оповещений hello с tootrigger hello веб-перехватчика действие runbook и настроить hello runbook tooconvert hello строку в формате JSON и фильтр *. SearchResult* следующие hello рекомендации, приведенные выше.    

## <a name="next-steps"></a>Дальнейшие действия

* toolearn Дополнительные об оповещениях в службе анализа журналов и как увидеть toocreate, [предупреждения в службе анализа журналов](../log-analytics/log-analytics-alerts.md).

* tootrigger модули Runbook с помощью веб-перехватчика. в статье toounderstand [веб-службы автоматизации Azure привязок](automation-webhooks.md).
