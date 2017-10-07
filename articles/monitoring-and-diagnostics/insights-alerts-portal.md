---
title: "оповещения aaaCreate для служб Azure - портал Azure | Документы Microsoft"
description: "Триггер сообщения электронной почты, уведомления, вызовите URL-адреса веб-сайтов (веб-перехватчиков) или автоматизации при соблюдении заданных условий hello."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: f7457655-ced6-4102-a9dd-7ddf2265c0e2
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/23/2016
ms.author: robb
ms.openlocfilehash: 78d862d25255cda9fdfe347329e908a471c39846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---azure-portal"></a>Создание оповещений метрик в Azure Monitor для служб Azure с помощью портала Azure
> [!div class="op_single_selector"]
> * [Портал](insights-alerts-portal.md)
> * [PowerShell](insights-alerts-powershell.md)
> * [ИНТЕРФЕЙС КОМАНДНОЙ СТРОКИ](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a>Обзор
В этой статье показано, как tooset Azure метрики предупреждений с помощью hello портал Azure.   

Вы можете получать оповещения на основе отслеживания метрик или событий в службах Azure.

* **Значения метрик** - hello предупредить триггеры hello значение указанной метрики пересекает пороговое значение, присваиваемое в любом направлении. То есть, и триггеров при hello сначала условия, и затем позже при, условия больше не выполнены.    
* **События журнала действий**. Оповещение может активироваться при *каждом* событии или только тогда, когда выполняются определенные события. Дополнительные сведения об активности журнала предупреждений toolearn [щелкните здесь](monitoring-activity-log-alerts.md)

Вы можете настроить метрики оповещений toodo hello следующие при инициировании:

* Отправить администратору службы toohello уведомлений электронной почты и соадминистраторы
* Отправьте по электронной почте tooadditional сообщений электронной почты, указанных вами.
* вызов webhook;
* Запустите выполнение runbook для Azure (только из hello портал Azure)

Для настройки правил генерации оповещений метрик и получении сведений о них можно использовать:

* [Портал Azure](insights-alerts-portal.md)
* [PowerShell](insights-alerts-powershell.md)
* [интерфейс командной строки (CLI)](insights-alerts-command-line-interface.md)
* [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-with-hello-azure-portal"></a>Создать правило генерации оповещений на метрики с hello портал Azure
1. В hello [портала](https://portal.azure.com/)вас интересуют мониторинг ресурсов hello найдите и выберите его.

2. Выберите **оповещения** или **предупреждения правила** под hello МОНИТОРИНГ раздела. текст Hello и значок, могут немного отличаться для разных ресурсов.  

    ![Мониторинг](./media/insights-alerts-portal/AlertRulesButton.png)

3. Выберите hello **добавить оповещение** команды и заполните поля hello.

    ![Добавить оповещение](./media/insights-alerts-portal/AddAlertOnlyParamsPage.png)

4. Введите **имя** правила генерации оповещений и укажите **описание**, отображаемое также в уведомлениях по электронной почте.

5. Выберите hello **метрика** toomonitor и нажмите кнопку **условие** и **пороговое значение** значение метрики hello. Также флажок hello **период** hello метрику времени правила должны соблюдаться hello предупреждения триггеры. Например при использовании hello период «PT5M» и оповещения ищет ЦП превышает 80%, hello предупреждение срабатывает при hello ЦП был постоянно выше 80% 5 минут. При возникновении hello первый триггер, снова запускает при hello ЦП будет ниже 80% в течение 5 минут. Hello измерения ЦП происходит каждую минуту.   

6. Проверьте **электронной почты владельцев...**  при необходимости администраторы и соадминистраторы toobe по электронной почте hello оповещений активируется.

7. Если дополнительные сообщения электронной почты tooreceive уведомление, когда hello срабатывает предупреждение, добавьте их в hello **email(s) дополнительного администратора** поля. При указании нескольких электронных адресов разделите их точкой с запятой: *email@contoso.com;email2@contoso.com*

8. Поместите в допустимый URI hello **веб-перехватчика** поле при необходимости его вызывается при hello оповещений активируется.

9. Если вы используете службы автоматизации Azure, можно выбрать toobe Runbook, при выводе предупреждения hello.

10. Выберите **ОК** при done toocreate hello предупреждение.   

В течение нескольких минут hello предупреждения является активным и триггеры, как описано выше.

## <a name="managing-your-alerts"></a>Управление оповещениями
После создания оповещение можно выбрать и:

* Просмотрите диаграмму, показывающую пороговое значение метрики hello и фактическими значениями hello из hello предыдущий день.
* изменить или удалить его;
* **Отключить** или **включить** его, если вы желаете tootemporarily остановить или возобновить получение уведомлений для данного предупреждения.

## <a name="next-steps"></a>Дальнейшие действия
* [Обзор мониторинг Azure](monitoring-overview.md) включая hello типы данных, можно собирать и контролировать.
* Узнайте больше о [настройке веб-перехватчиков webhook в оповещениях](insights-webhooks-alerts.md).
* Узнайте больше о [настройке оповещений о событиях журнала действий](monitoring-activity-log-alerts.md).
* Узнайте больше о [модулях Runbook службы автоматизации Azure](../automation/automation-starting-a-runbook.md).
* Ознакомьтесь с [обзором журналов диагностики](monitoring-overview-of-diagnostic-logs.md) , чтобы собирать подробные метрики о службе с высокой частотой.
* Получить [Обзор сбора метрик](insights-how-to-customize-monitoring.md) toomake убедиться, что служба становится доступной и отвечать на запросы.
