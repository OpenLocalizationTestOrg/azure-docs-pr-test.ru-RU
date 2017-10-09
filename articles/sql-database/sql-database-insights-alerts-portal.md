---
title: "предупреждения базы данных SQL Azure портала toocreate aaaUse | Документы Microsoft"
description: "Используйте базу данных SQL Azure портала toocreate hello предупреждения, которые могут привести к уведомления или автоматизации при соблюдении заданных условий hello."
author: aamalvea
manager: jhubbard
editor: 
services: sql-database
documentationcenter: 
ms.assetid: f7457655-ced6-4102-a9dd-7ddf2265c0e2
ms.service: sql-database
ms.custom: monitor and tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: aamalvea
ms.openlocfilehash: 4e494b130a26c4cdf42445cb49648fce9bf4d300
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-toocreate-alerts-for-azure-sql-database-and-data-warehouse"></a>Используйте Azure портала toocreate предупреждения для базы данных SQL Azure и хранилища данных

## <a name="overview"></a>Обзор
В этой статье показано, как tooset предупреждений базы данных SQL Azure и хранилище данных с помощью hello портал Azure. В этой статье также приведены рекомендации по настройке периодов оповещений.    

Вы можете получать оповещения на основе отслеживания метрик или событий в службах Azure.

* **Значения метрик** - hello предупредить триггеры hello значение указанной метрики пересекает пороговое значение, присваиваемое в любом направлении. То есть, и триггеров при hello сначала условия, и затем позже при, условия больше не выполнены.    
* **События журнала действий**. Оповещение может активироваться при *каждом* событии или только тогда, когда выполняется определенное число событий.

Можно настроить предупреждения toodo hello следующие при инициировании:

* Отправить администратору службы toohello уведомлений электронной почты и соадминистраторы
* Отправьте по электронной почте tooadditional сообщений электронной почты, указанных вами.
* вызов webhook;

Для настройки правил генерации оповещений и получении сведений о них можно использовать:

* [Портал Azure](../monitoring-and-diagnostics/insights-alerts-portal.md)
* [PowerShell](../monitoring-and-diagnostics/insights-alerts-powershell.md)
* [интерфейс командной строки (CLI)](../monitoring-and-diagnostics/insights-alerts-command-line-interface.md)
* [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-with-hello-azure-portal"></a>Создать правило генерации оповещений на метрики с hello портал Azure
1. В hello [портала](https://portal.azure.com/)вас интересуют мониторинг ресурсов hello найдите и выберите его.
2. Этот шаг выполняется по-разному для баз данных SQL Server и эластичных пулов и хранилищ данных SQL. 

   - **Баз данных SQL Server & только эластичных пулов**: выберите **оповещения** или **предупреждения правила** под hello МОНИТОРИНГ раздела. текст Hello и значок, могут немного отличаться для разных ресурсов.  
   
     ![Мониторинг](../monitoring-and-diagnostics/media/insights-alerts-portal/AlertRulesButton.png)
  
   - **Хранилища данных SQL только**: выберите **мониторинг** под hello раздел ОБЩИХ задач. Нажмите кнопку hello **DWU использование** графа.

     ![ОБЩИЕ ЗАДАЧИ](../monitoring-and-diagnostics/media/insights-alerts-portal/AlertRulesButtonDW.png)

3. Выберите hello **добавить оповещение** команды и заполните поля hello.
   
    ![Добавить оповещение](../monitoring-and-diagnostics/media/insights-alerts-portal/AddDBAlertPage.png)
4. Введите **имя** правила генерации оповещений и укажите **описание**, отображаемое также в уведомлениях по электронной почте.
5. Выберите hello **метрика** toomonitor и нажмите кнопку **условие** и **пороговое значение** значение метрики hello. Также флажок hello **период** hello метрику времени правила должны соблюдаться hello предупреждения триггеры. Например при использовании hello период «PT5M» и оповещения ищет ЦП превышает 80%, hello предупреждение срабатывает при hello ЦП был постоянно выше 80% 5 минут. При возникновении hello первый триггер, снова запускает при hello ЦП будет ниже 80% в течение 5 минут. Hello измерения ЦП происходит каждую минуту.   
6. Проверьте **электронной почты владельцев...**  при необходимости администраторы и соадминистраторы toobe по электронной почте hello оповещений активируется.
7. Если дополнительные сообщения электронной почты tooreceive уведомление, когда hello срабатывает предупреждение, добавьте их в hello **email(s) дополнительного администратора** поля. При указании нескольких электронных адресов разделите их точкой с запятой: *email@contoso.com;email2@contoso.com*
8. Поместите в допустимый URI hello **веб-перехватчика** поле при необходимости его вызывается при hello оповещений активируется.
9. Выберите **ОК** при done toocreate hello предупреждение.   

В течение нескольких минут hello предупреждения является активным и триггеры, как описано выше.

## <a name="managing-your-alerts"></a>Управление оповещениями
После создания оповещение можно выбрать и:

* Просмотрите диаграмму, показывающую пороговое значение метрики hello и фактическими значениями hello из hello предыдущий день.
* изменить или удалить его;
* **Отключить** или **включить** его, если вы желаете tootemporarily остановить или возобновить получение уведомлений для данного предупреждения.


## <a name="sql-database-alert-values"></a>Значения оповещений базы данных SQL

| Тип ресурса | Имя метрики | Понятное имя | Тип статистической обработки | Минимальный интервал времени для оповещений|
| --- | --- | --- | --- | --- |
| База данных SQL | cpu_percent | Процент использования ЦП | Средняя | 5 мин |
| База данных SQL | physical_data_read_percent | Процент операций ввода/вывода данных | Средняя | 5 мин |
| База данных SQL | log_write_percent | Log IO percentage | Средняя | 5 мин |
| База данных SQL | dtu_consumption_percent | Процент использования DTU | Средняя | 5 мин |
| База данных SQL | storage | Total database size | Максимальная | 30 минут |
| База данных SQL | connection_successful | Успешные подключения | Всего | 10 минут |
| База данных SQL | connection_failed | Неудачные подключения | Всего | 10 минут |
| База данных SQL | blocked_by_firewall | Заблокировано брандмауэром | Всего | 10 минут |
| База данных SQL | deadlock | Взаимоблокировки | Всего | 10 минут |
| База данных SQL | storage_percent | Размер базы данных в процентах | Максимальная | 30 минут |
| База данных SQL | xtp_storage_percent | In-Memory OLTP storage percent (Preview) | Средняя | 5 мин |
| База данных SQL | workers_percent | Workers percentage | Средняя | 5 мин |
| База данных SQL | sessions_percent | Sessions percent | Средняя | 5 мин |
| База данных SQL | dtu_limit | DTU limit | Средняя | 5 мин |
| База данных SQL | dtu_used | DTU used | Средняя | 5 мин |
||||||
| Эластичный пул | cpu_percent | Процент использования ЦП | Средняя | 10 минут |
| Эластичный пул | physical_data_read_percent | Процент операций ввода/вывода данных | Средняя | 10 минут |
| Эластичный пул | log_write_percent | Log IO percentage | Средняя | 10 минут |
| Эластичный пул | dtu_consumption_percent | Процент использования DTU | Средняя | 10 минут |
| Эластичный пул | storage_percent | Storage percentage | Средняя | 10 минут |
| Эластичный пул | workers_percent | Workers percentage | Средняя | 10 минут |
| Эластичный пул | eDTU_limit | eDTU limit | Средняя | 10 минут |
| Эластичный пул | storage_limit | Storage limit | Средняя | 10 минут |
| Эластичный пул | eDTU_used | eDTU used | Средняя | 10 минут |
| Эластичный пул | storage_used | Storage used | Средняя | 10 минут |
||||||               
| Хранилище данных SQL | cpu_percent | Процент использования ЦП | Средняя | 10 минут |
| Хранилище данных SQL | physical_data_read_percent | Процент операций ввода/вывода данных | Средняя | 10 минут |
| Хранилище данных SQL | storage | Total database size | Максимальная | 10 минут |
| Хранилище данных SQL | connection_successful | Успешные подключения | Всего | 10 минут |
| Хранилище данных SQL | connection_failed | Неудачные подключения | Всего | 10 минут |
| Хранилище данных SQL | blocked_by_firewall | Заблокировано брандмауэром | Всего | 10 минут |
| Хранилище данных SQL | service_level_objective | Уровень обслуживания базы данных hello | Всего | 10 минут |
| Хранилище данных SQL | dwu_limit | Лимит DWU. | Максимальная | 10 минут |
| Хранилище данных SQL | dwu_consumption_percent | DWU percentage | Средняя | 10 минут |
| Хранилище данных SQL | dwu_used | DWU used | Средняя | 10 минут |
||||||


## <a name="next-steps"></a>Дальнейшие действия
* [Обзор мониторинг Azure](../monitoring-and-diagnostics/monitoring-overview.md) включая hello типы данных, можно собирать и контролировать.
* Узнайте больше о [настройке веб-перехватчиков webhook в оповещениях](../monitoring-and-diagnostics/insights-webhooks-alerts.md).
* Ознакомьтесь с [обзором журналов диагностики](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) , чтобы собирать подробные метрики о службе с высокой частотой.
* Получить [Обзор сбора метрик](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) toomake убедиться, что служба становится доступной и отвечать на запросы.
