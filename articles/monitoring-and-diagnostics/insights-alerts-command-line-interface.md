---
title: "оповещения aaaCreate для служб Azure - CLI кросс платформенных | Документы Microsoft"
description: "Триггер сообщения электронной почты, уведомления, вызовите URL-адреса веб-сайтов (веб-перехватчиков) или автоматизации при соблюдении заданных условий hello."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 5c6a2d27-7dcc-4f89-8752-9bb31b05ff35
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: robb
ms.openlocfilehash: e53701e5377a415038a69fbd32f1e5fc5fe99be9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---cross-platform-cli"></a>Создание оповещений метрик в Azure Monitor для служб Azure с помощью кроссплатформенного интерфейса командной строки
> [!div class="op_single_selector"]
> * [Портал](insights-alerts-portal.md)
> * [PowerShell](insights-alerts-powershell.md)
> * [ИНТЕРФЕЙС КОМАНДНОЙ СТРОКИ](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a>Обзор
В этой статье показано, как tooset Azure метрики предупреждений с помощью hello кросс платформенных интерфейс командной строки (CLI).

> [!NOTE]
> Монитор Azure — новое имя hello что был вызван «Azure Insights» до 25 сентября 2016 года. Однако hello пространств имен и поэтому приведенную ниже команду hello по-прежнему содержать аналитики «hello».
>
>

Вы можете получать оповещения на основе отслеживания метрик или событий в службах Azure.

* **Значения метрик** - hello предупредить триггеры hello значение указанной метрики пересекает пороговое значение, присваиваемое в любом направлении. То есть, и триггеров при hello сначала условия, и затем позже при, условия больше не выполнены.    
* **События журнала действий**. Оповещение может активироваться при *каждом* событии или только тогда, когда выполняются определенные события. Дополнительные сведения об активности журнала предупреждений toolearn [щелкните здесь](monitoring-activity-log-alerts.md)

Вы можете настроить метрики оповещений toodo hello следующие при инициировании:

* Отправить администратору службы toohello уведомлений электронной почты и соадминистраторы
* Отправьте по электронной почте tooadditional сообщений электронной почты, указанных вами.
* вызов webhook;
* Запустите выполнение runbook для Azure (только из hello портал Azure в настоящее время)

Для настройки правил генерации оповещений метрик и получении сведений о них можно использовать:

* [Портал Azure](insights-alerts-portal.md)
* [PowerShell](insights-alerts-powershell.md)
* [интерфейс командной строки (CLI)](insights-alerts-command-line-interface.md)
* [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931945.aspx)

Всегда можно получать справки для команд с помощью команд и помещения - помочь в конце hello. Например:

    ```console
    azure insights alerts -help
    azure insights alerts actions email create -help
    ```

## <a name="create-alert-rules-using-hello-cli"></a>Создание правил оповещений с помощью hello CLI
1. Выполните необходимые условия hello и tooAzure входа. См. [примеры CLI для Azure Monitor](insights-cli-samples.md). Иными словами установите hello CLI и выполните следующие команды. Они вам войти, будет отображена какие подписки используется и подготовки команды toorun монитора Azure.

    ```console
    azure login
    azure account show
    azure config mode arm

    ```

2. toolist существующие правила в группе ресурсов, используйте следующие формы hello **аналитики azure, список правил оповещения** *[параметры] &lt;группа ресурсов&gt;*

   ```console
   azure insights alerts rule list myresourcegroupname

   ```
3. toocreate правило, требуется toohave несколько важных аспекта сведений сначала.
  * Hello **идентификатор ресурса** для hello ресурса требуется tooset оповещение для
  * Hello **определения показателей** доступны для этого ресурса

     Одним из способов tooget hello идентификатор ресурса — toouse hello портал Azure. Предположим, что ресурс hello уже создан, выберите его в портал hello. Выберите в колонке Далее hello *свойства* под hello *параметры* раздела. Hello *идентификатор РЕСУРСА* — это поле в колонке Далее hello. Другим способом является toouse hello [обозревателя ресурсов Azure](https://resources.azure.com/).

     Ниже приведен пример идентификатора ресурса для веб-приложения.

     ```console
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     tooget список доступных показателей hello и единицы измерения для этих метрик для предыдущего примера ресурсов hello, hello используйте следующую команду CLI:  

     ```console
     azure insights metrics list /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename PT1M
     ```

     *PT1M* — hello гранулярности измерения доступны hello (1-минутные интервалы). Выбор различных уровней детализации позволяет использовать разные параметры метрик.
4. toocreate основе метрика правилом оповещений, используйте команду hello следующие формы:

    **azure insights alerts rule metric set** *[параметры] &lt;имя_правила&gt; &lt;расположение&gt; &lt;группа_ресурсов&gt; &lt;размер_окна&gt; &lt;оператор&gt; &lt;пороговое_значение&gt; &lt;ИД_целевого_ресурса&gt; &lt;имя_метрики&gt; &lt;оператор_агрегата_времени&gt;*

    Здравствуйте, следующий пример настраивает оповещение на ресурс веб-сайта. Hello предупреждения триггеры всякий раз, когда постоянно получает любой трафик, 5 минут, и снова при получении трафика на 5 минут.

    ```console
    azure insights alerts rule metric set myrule eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total

    ```
5. toocreate веб-перехватчик или отправить по электронной почте при выводе метрики предупреждения, сначала создайте hello электронной почты и/или веб-привязок. Создать правило hello немедленно после него. Не удалось связать веб-перехватчик или сообщения электронной почты с уже созданные правила, использующие hello CLI.

    ```console
    azure insights alerts actions email create --customEmails myemail@contoso.com

    azure insights alerts actions webhook create https://www.contoso.com

    azure insights alerts rule metric set myrulewithwebhookandemail eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total
    ```

6. Можно проверить, правильно ли созданы оповещения, просмотрев отдельное правило.

    ```console
    azure insights alerts rule list myresourcegroup --ruleName myrule
    ```
7. правила toodelete команда hello формы:

    **insights alerts rule delete** [параметры] &lt;группа_ресурсов&gt; &lt;имя_правила&gt;

    Эти команды удаляют hello правила, созданные ранее в этой статье.

    ```console
    azure insights alerts rule delete myresourcegroup myrule
    azure insights alerts rule delete myresourcegroup myrulewithwebhookandemail
    azure insights alerts rule delete myresourcegroup myActivityLogRule
    ```

## <a name="next-steps"></a>Дальнейшие действия
* [Обзор мониторинг Azure](monitoring-overview.md) включая hello типы данных, можно собирать и контролировать.
* Узнайте больше о [настройке веб-перехватчиков webhook в оповещениях](insights-webhooks-alerts.md).
* Узнайте больше о [настройке оповещений о событиях журнала действий](monitoring-activity-log-alerts.md).
* Узнайте больше о [модулях Runbook службы автоматизации Azure](../automation/automation-starting-a-runbook.md).
* Получить [Обзор сбора журналов диагностики](monitoring-overview-of-diagnostic-logs.md) toocollect подробные показатели высокой частотой в службе.
* Получить [Обзор сбора метрик](insights-how-to-customize-monitoring.md) toomake убедиться, что служба становится доступной и отвечать на запросы.
