---
title: "Образец aaaWebhook действие предупреждения в аналитику журнала OMS | Документы Microsoft"
description: "Одно из действий hello, можно запустить в ответ tooa предупреждение анализа журналов — * веб-перехватчика *, позволяющий tooinvoke внешний процесс через один HTTP-запроса. В этой статье рассматривается пример создания действия webhook в оповещении Log Analytics с использованием Slack."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 13c39f0f-fd3c-472d-8324-ddf7538be45e
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: bwren
ms.openlocfilehash: e60bdc4922347073d572c2e4719461b13e8e7d1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-alert-webhook-action-in-oms-log-analytics-toosend-message-tooslack"></a>Создание предупреждения веб-перехватчика действия в tooSlack сообщения toosend анализа журналов OMS
Одно из действий hello, можно запустить в ответ tooa [предупреждение анализа журналов](log-analytics-alerts.md) — *веб-перехватчика*, позволяющее tooinvoke внешний процесс через один HTTP-запроса.  Подробные сведения об оповещениях и действиях webhook см. в статье [Оповещения в Log Analytics](log-analytics-alerts.md).

В этой статье рассматривается пример создания действия webhook в оповещении Log Analytics с использованием службы обмена сообщениями Slack.

> [!NOTE]
> В этом примере необходимо иметь toocomplete учетная запись Slack.  Ее можно получить бесплатно на сайте [slack.com](http://slack.com).
> 
> 

## <a name="step-1---enable-webhooks-in-slack"></a>Шаг 1. Включение действий webhook в Slack
1. Войдите в tooSlack на [slack.com](http://slack.com).
2. Выберите канал в hello **каналы** hello левой области.  Это hello канала будет отправляться сообщение hello.  Выберите один из каналов по умолчанию hello например **Общие** или **случайных**.  В рабочих сценариях чаще всего создается специальный канал, например **criticalservicealerts**. <br>
   
   ![Каналы Slack](media/log-analytics-alerts-webhooks/oms-webhooks01.png)
3. Нажмите кнопку **добавить приложения или индивидуальная настройка** tooopen hello каталога приложения.
4. Тип *веб-перехватчиков* в поле поиска hello, а затем выберите **входящего веб-перехватчиков**. <br>
   
   ![Каналы Slack](media/log-analytics-alerts-webhooks/oms-webhooks02.png)
5. Нажмите кнопку **установить** следующее имя команды tooyour.
6. Щелкните **Add Configuration**(Добавить конфигурацию).
7. Выберите hello hello канала будем toouse для этого примера и нажмите кнопку **интеграции Добавление входящего веб-перехватчиков**.  
8. Копировать hello **URL-адрес веб-перехватчика**.  Вы сможете вставить это в конфигурации оповещений hello. <br>
   
    ![Каналы Slack](media/log-analytics-alerts-webhooks/oms-webhooks05.png)

## <a name="step-2---create-alert-rule-in-log-analytics"></a>Шаг 2. Создание правила генерации оповещений в Log Analytics
1. [Создать правило оповещения](log-analytics-alerts.md) с hello следующие параметры.
   * Запрос: ```    Type=Event EventLevelName=error ```
   * Check for this alert every: 5 minutes (Проверять это оповещение: каждые 5 минут)
   * Hello количество результатов: больше 10
   * Over this time window: 60 minutes (За период: 60 минут)
   * Выберите **Да** для **веб-перехватчика** и **нет** для hello других действий.
2. Вставить hello URL-адрес Slack в hello **URL-адрес веб-перехватчика** поля.
3. Выберите параметр hello слишком**включить настраиваемые полезные данные JSON**.
4. Slack ожидает полезные данные в формате JSON с параметром *text*.  Это текст hello, которые будут отображаться в приветственное сообщение, он создает.  Можно использовать один или несколько параметров hello предупреждений с помощью hello  *#*  символов, таких как следующий пример hello.
   
    ```
    {
    "text":"#alertrulename fired with #searchresultcount records which exceeds hello over threshold of #thresholdvalue ."
    }
    ```
   
    ![пример полезных данных JSON](media/log-analytics-alerts-webhooks/oms-webhooks07.png)
5. Нажмите кнопку **Сохранить** правило оповещения toosave hello.
6. Подождите достаточное время для оповещения toobe создан и проверьте для сообщения, которое будет иметь примерно следующий toohello Slack.
   
   ![пример webhook в Slack](media/log-analytics-alerts-webhooks/oms-webhooks08.png)

### <a name="advanced-webhook-payload-for-slack"></a>Расширенные полезные данные webhook для Slack
Slack позволяет настроить входные сообщения в широких пределах. Дополнительные сведения см. в разделе [входящего веб-перехватчиков](https://api.slack.com/incoming-webhooks) резерв hello веб-сайта. Ниже приведен более сложные toocreate полезных данных форматированного сообщения с форматированием.

    {
        "attachments": [
            {
                "title":"OMS Alerts Custom Payload",
                "fields": [
                    {
                        "title": "Alert Rule Name",
                        "value": "#alertrulename"},
                    {
                        "title": "Link tooSearchResults",
                        "value": "<#linktosearchresults|OMS Search Results>"},
                    {
                        "title": "Search Interval",
                        "value": "#searchinterval"},
                    {
                        "title": "Threshold Operator",
                        "value": "#thresholdoperator"},
                    {
                        "title": "Threshold Value",
                        "value": "#thresholdvalue"}
                ],
                "color": "#F35A00"
            }
        ]
    }


Это вызовет сообщение в резерв аналогичные toohello ниже.

![пример сообщения в Slack](media/log-analytics-alerts-webhooks/oms-webhooks09.png)

## <a name="summary"></a>Сводка
С помощью этого правила оповещения в месте tooSlack сообщение, отправленное бы каждый раз hello условий.  

Это только один пример действия, которые можно создавать в предупреждении tooan ответа.  Можно создать веб-перехватчика действие, которое вызывает другой внешней службы, действие runbook toostart runbook в автоматизации Azure или toosend действия электронной почты tooyourself почты или другим получателям.   

## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения о [действиях оповещения в Log Analytics](log-analytics-alerts-actions.md), включая другие действия.


