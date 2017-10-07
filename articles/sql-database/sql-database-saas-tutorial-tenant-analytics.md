---
title: "aaaRun аналитические запросы к нескольким базам данных Azure SQL | Документы Microsoft"
description: "Извлечение данных из баз данных клиента в базу данных аналитики для автономного анализа."
keywords: "руководство по базе данных sql"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: billgib; sstein
ms.openlocfilehash: f2664e4aafd2fecc98d20d229342bca19b0b08c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="extract-data-from-tenant-databases-into-an-analytics-database-for-offline-analysis"></a>Извлечение данных из баз данных клиента в базу данных аналитики для автономного анализа.

В этом учебнике используется запросов toorun эластичной заданий для каждой базы данных клиента. Hello задание извлекает данные о продажах билета и загружает их в базу данных аналитики (или хранилище данных) для анализа. Hello базы данных аналитики будет запрашивать tooextract полезные сведения из этого повседневных рабочих данных всех клиентов.


Из этого руководства вы узнаете, как выполнить следующие задачи:

> [!div class="checklist"]
> * Создать базу данных аналитики клиента hello
> * Создание запланированного задания tooretrieve данных и заполнить базу данных аналитики hello

toocomplete этого учебника, убедитесь, что hello следующие необходимые условия выполнены:

* приложение Wingtip SaaS Hello развертывается. toodeploy менее чем за пять минут. в разделе [развертывание и просмотр приложения Wingtip SaaS hello](sql-database-saas-tutorial.md)
* Установите Azure PowerShell. Дополнительные сведения см. в статье [Начало работы с Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps).
* будет установлена последняя версия Hello объекта SQL Server Management Studio (SSMS). [Download SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (Скачивание SQL Server Management Studio (SSMS))

## <a name="tenant-operational-analytics-pattern"></a>Шаблон операционной аналитики клиента

Одним из hello значительные возможности с приложениями SaaS является toouse hello многофункциональный клиентский данные, хранящиеся в облаке hello. Используйте этот данных toogain анализировать операции hello и использования приложения и клиенты. Эти данные проводит разработки функции, улучшения удобства использования и прочие вложения в приложение hello и платформы. Доступ к этим данным получить очень просто, если они содержатся в отдельной мультитенантной базе данных, но не так просто, если они распределены по тысячам масштабируемых баз данных. Один подход tooaccessing эти данные являются toouse эластичной заданий, позволяющие возвращение результата от toobe выполнения задания, записанные в выходных данных базы данных и таблицы результатов запроса.

## <a name="get-hello-wingtip-application-scripts"></a>Получение скриптов приложения Wingtip hello

Hello Wingtip SaaS скриптов и исходный код приложения были доступны в hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) в репозитории github. [Действия скриптов Wingtip SaaS hello toodownload](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="deploy-a-database-for-tenant-analytics-results"></a>Развертывание базы данных для результатов аналитики клиента

Этот учебник требует toohave, hello toocapture развернутой базы данных полученный в результате выполнения скриптов, которые содержат запросы, возвращающие результаты задания. Для этого давайте создадим базу данных с именем tenantanalytics.

1. Открыть... \\Модулей обучения\\оперативной аналитики\\аналитика клиента\\*Демонстрация TenantAnalyticsDB.ps1* в hello *интегрированной среды Сценариев PowerShell* и задайте Здравствуйте, следующие значения:
   * **$DemoScenario** = **2**, чтобы *развернуть базы данных операционной аналитики*.
1. Нажмите клавишу **F5** toorun hello демонстрационный сценарий (hello, вызовы *TenantAnalyticsDB.ps1 развернуть* сценария) создает базы данных аналитики hello клиента.

## <a name="create-some-data-for-hello-demo"></a>Создание некоторых данных для образца hello

1. Открыть... \\Модулей обучения\\оперативной аналитики\\аналитика клиента\\*Демонстрация TenantAnalyticsDB.ps1* в hello *интегрированной среды Сценариев PowerShell* и задайте Здравствуйте, следующие значения:
   * **$DemoScenario** = **1**, чтобы *приобрести билеты на мероприятия во всех местах проведения*.
1. Нажмите клавишу **F5** toorun hello скрипт и создать журнал приобретения билета.


## <a name="create-a-scheduled-job-tooretrieve-tenant-analytics-about-ticket-purchases"></a>Создание аналитика клиента tooretrieve запланированного задания, о покупках билета

Этот скрипт создает задание информации о приобретении tooretrieve билетов от всех клиентов. После статистическую обработку в одну таблицу, можно получить форматированного информативные метрики о билет приобретение шаблоны hello клиентов.

1. Откройте SSMS и подключите каталог toohello -&lt;пользователя&gt;. database.windows.net сервера
1. Откройте файл ...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*TicketPurchasesfromAllTenants.sql*.
1. Изменить &lt;пользователя&gt;, используйте hello имя пользователя при развертывании приложение Wingtip SaaS hello hello верхней части сценария hello **sp\_добавить\_целевой\_группы\_член** и **sp\_добавить\_шага задания**
1. Щелкните правой кнопкой мыши, выберите **подключения**и подключите каталог toohello -&lt;пользователя&gt;. database.windows.net сервер, если еще не подключены
1. Убедитесь, подключенных toohello **jobaccount** базы данных и нажмите клавишу **F5** для выполнения сценария hello

* **SP\_добавить\_целевой\_группы** создает имя целевой группы hello *TenantGroup*, теперь мы должны tooadd целевые элементы.
* **SP\_добавить\_целевой\_группы\_член** добавляет *сервера* целевой тип члена, который рассматривается всех баз данных в пределах сервера (Обратите внимание, это hello customer1 - &lt;Пользователя&gt; сервер, содержащий базы данных клиента hello) во время задания выполнения должны быть включены в задание hello.
* **sp\_add\_job** создает еженедельное запланированное задание "Покупка билетов клиентами".
* **SP\_добавить\_jobstep** создает все hello билета закупки hello шаг задания, содержащий tooretrieve текст команды T-SQL со всех клиентов и возвращение результирующего набора в таблицу с именем hello копирования  *AllTicketsPurchasesfromAllTenants*
* Оставшиеся представления Hello в скрипте hello отображают существование hello hello объектов и монитор выполнения задания. Просмотрите значение состояния hello из hello **жизненного цикла** состояние hello toomonitor столбца. Один раз прошло успешно, задание hello успешного завершения работы для всех баз данных клиента и hello два дополнительных баз данных, содержащих hello ссылаются на таблицу.

Успешно запустить скрипт hello следует результат такой же результат:

![results](media/sql-database-saas-tutorial-tenant-analytics/ticket-purchases-job.png)

## <a name="create-a-job-tooretrieve-a-summary-count-of-ticket-purchases-from-all-tenants"></a>Создание задания tooretrieve, общее число билет покупки от всех клиентов

Этот скрипт создает задание tooretrieve сумму всех покупок билет от всех клиентов.

1. Откройте SSMS и подключите toohello *каталога -&lt;пользователя&gt;. database.windows.net* сервера
1. Привет открыть файл... \\Модулях обучения\\подготовки и каталога\\оперативной аналитики\\клиента Analytics\\*TicketPurchasesfromAllTenants.sql результатов*
1. Изменить &lt;пользователя&gt;, используйте hello имя пользователя при развертывании приложения Wingtip SaaS hello в скрипте hello в hello **sp\_добавить\_шага задания** хранимой процедуры
1. Щелкните правой кнопкой мыши, выберите **подключения**и подключите каталог toohello -&lt;пользователя&gt;. database.windows.net сервер, если еще не подключены
1. Убедитесь, подключенных toohello **tenantanalytics** базы данных и нажмите клавишу **F5** для выполнения сценария hello

Успешно запустить скрипт hello следует результат такой же результат:

![results](media/sql-database-saas-tutorial-tenant-analytics/total-sales.png)



* **sp\_add\_job** создает еженедельное запланированное задание ResultsTicketsOrders.

* **SP\_добавить\_шага задания** создает все hello билета закупки hello шаг задания, содержащий tooretrieve текст команды T-SQL со всех клиентов и возвращение результирующего набора в таблицу с именем CountofTicketOrders hello копирования

* Оставшиеся представления Hello в скрипте hello отображают существование hello hello объектов и монитор выполнения задания. Просмотрите значение состояния hello из hello **жизненного цикла** состояние hello toomonitor столбца. Один раз прошло успешно, задание hello успешного завершения работы для всех баз данных клиента и hello два дополнительных баз данных, содержащих hello ссылаются на таблицу.


## <a name="next-steps"></a>Дальнейшие действия

Из этого руководства вы узнали, как выполнять такие задачи:

> [!div class="checklist"]
> * Развертывание базы данных аналитики клиента.
> * Создать запланированное задание tooretrieve аналитических данных в другие клиенты

Поздравляем!

## <a name="additional-resources"></a>Дополнительные ресурсы

* Дополнительные [учебники, которые созданы на основе Wingtip SaaS приложения hello](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Управление масштабируемыми облачными базами данных](sql-database-elastic-jobs-overview.md)
