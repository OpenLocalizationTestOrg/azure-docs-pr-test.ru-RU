---
title: "aaaManage баз данных в хранилище данных SQL Azure | Документы Microsoft"
description: "Общие сведения об управлении базами данных в хранилище данных SQL. Рассматриваются средства управления, динамические административные представления и масштабирование производительности, устранение неполадок с запросами, создание надлежащих политик безопасности и восстановление базы данных после повреждения данных или регионального сбоя."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 8576fdb3-71fe-4b3b-a4e0-5e8a7f148acf
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: caec6572c4ab395107c3b095adc69a53eae8bd88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-databases-in-azure-sql-data-warehouse"></a>Управление базами данных в хранилище данных SQL Azure
Хранилище данных SQL позволяет автоматизировать многие аспекты управления базами данных. Например производительности tooscale достаточно tooadjust и платить за hello справа уровня вычислительных ресурсов и подождите, пока хранилище данных SQL выполните все процессы hello масштабное развертывание и масштабирование назад.

Без сомнения требуется toomonitor вашей рабочей нагрузки tooidentify производительность требуется, а также устранение неполадок длительных запросов. Необходимо также tooperform несколько задач toomanage права доступа для пользователей и имена входа.

В этом обзоре рассматриваются следующие аспекты управления хранилищем данных SQL.

* Средства управления
* Масштабирование вычислительных ресурсов
* Остановка и возобновление
* Рекомендации по производительности
* Мониторинг запросов
* Безопасность
* Архивация и восстановление

## <a name="management-tools"></a>Средства управления
Можно использовать различные базы данных toomanage средства в хранилище данных SQL. При управлении баз данных, будет разрабатывать средства настройки для каждого типа задач необходимо tooperform.

### <a name="azure-portal"></a>Портал Azure
Hello [портал Azure] [ Azure portal] является веб-порталом, где можно создавать, обновлять и удаление баз данных и отслеживать ресурсы базы данных. Это средство удобно — Если вы новичок в Azure, управлять небольшим числом баз данных хранилища данных, либо требуется tooquickly каким-либо.

tooget к работе с hello портал Azure в разделе [Создание хранилища данных SQL (портал Azure)][Create a SQL Data Warehouse (Azure portal)].

### <a name="sql-server-data-tools-in-visual-studio"></a>SQL Server Data Tools в Visual Studio
[SQL Server Data Tools] [ SQL Server Data Tools] (SSDT) в Visual Studio позволяет вам tooconnect для управления и разработки баз данных. Если вы не новичок в разработке приложений и уже знакомы с Visual Studio или другими интегрированными средами разработки (IDE), предлагаем обратить внимание на SSDT в составе Visual Studio.

Средства SSDT включают hello обозреватель объектов SQL Server, позволяющий toovisualize, подключитесь и выполните сценарий на основе баз данных хранилища данных SQL. tooquickly подключения tooSQL хранилища данных, можно просто щелкнуть hello **в среде Visual Studio** кнопки на панели команд hello при просмотре сведений базы данных hello в hello классический портал Azure.  

tooget к работе с SSDT в Visual Studio в разделе [запросов хранилища данных SQL Azure с помощью Visual Studio][Query Azure SQL Data Warehouse with Visual Studio].

### <a name="command-line-tools"></a>Программы командной строки
Средства командной строки идеально подходят для автоматизации рабочих нагрузок.  PowerShell и sqlcmd являются двумя tooautomate замечательные возможности процессы.  Рекомендуется, чтобы эти средства для управления большим числом логических серверов и развертывание изменения ресурсов в рабочей среде, как можно в скрипт и затем автоматизировать необходимые задачи hello.

### <a name="dynamic-management-views"></a>Динамические административные представления
Динамические административные представления являются hello хлеб совершенно необходимые для управления хранилищем данных SQL. Почти все сведения, который предоставляет доступ к порталу hello полагается на динамические административные представления. toosee список DMV хранилища данных SQL, в разделе [системных представлений SQL Data Warehouse][SQL Data Warehouse system views].

tooget работы см. в разделе [подключение и запрос с помощью sqlcmd][Connect and query with sqlcmd], и [Создание базы данных (PowerShell)][Create a database (PowerShell)].

## <a name="scale-compute"></a>Масштабирование вычислительных ресурсов
В хранилище данных SQL можно быстро увеличить или уменьшить производительность, настроив объем вычислительных ресурсов ЦП, памяти и пропускной способности ввода-вывода. производительность tooscale все что нужно toodo — задайте число hello единицы хранилища данных (Dwu), что хранилище данных SQL выделяет tooyour базы данных. Хранилище данных SQL быстро делает изменить hello и обрабатывает все базовые изменения toohardware hello или программного обеспечения.

. в разделе toolearn Дополнительные сведения о масштабировании Dwu, [масштабирования производительности].

## <a name="pause-and-resume"></a>Остановка и возобновление
toosave затраты, можно приостановить и возобновить вычислительные ресурсы по требованию. Например если не будет использоваться hello базы данных во время ночь hello и по выходным, можно приостановить ее работу в то время и возобновите ее работу в течение дня hello. Вы не будете платить за Dwu во время приостановки базы данных hello.

Дополнительные сведения см. в статьях [Приостановка работы вычислительных ресурсов][Pause compute] и [Возобновление работы вычислительных ресурсов][Resume compute].

## <a name="performance-best-practices"></a>Рекомендации по производительности
Когда Приступая к работе с новой технологией, обнаружение hello советы и рекомендации, которые работают наилучшим справа от начала hello может сэкономить много времени.  Рекомендации приводятся во многих наших разделах.

toosee много Сводка hello наиболее важные вопросы при разработке рабочей нагрузки в разделе [рекомендации данных SQL хранилища][SQL Data Warehouse Best Practices].

## <a name="query-monitoring"></a>Мониторинг запросов
Иногда запрос выполняется слишком много времени, но точно не известно, какой из них является причиной hello. Хранилище данных SQL содержит динамические административные представления (DMV), которые можно использовать toofigure ожидания какой запрос занимает слишком много времени.

toofind долго выполняющихся запросов, в разделе [мониторинг рабочей нагрузки с помощью динамических административных представлений][Monitor your workload using DMVs].

## <a name="security"></a>Безопасность
toomaintain система безопасности, должен быть предупреждение hello и защиты от несанкционированного доступа любого типа. Система безопасности должна toomake убедитесь, что правила брандмауэра на месте, что только авторизованных можно подключиться с помощью IP-адреса. Также требуется надлежащая проверка подлинности учетных данных пользователя. После подключения пользователя базы данных toohello hello пользователя должна иметь только разрешения tooperform минимальное количество действий. toosecure данных, можно использовать шифрование. Это также важно toohave аудит и отслеживание, поэтому вы сможете события, если все подозрительные действия.

toolearn об управлении безопасностью заголовок над toohello [Общие сведения о безопасности][Security overview].

## <a name="backup-and-restore"></a>Архивация и восстановление
Наличие надежных резервных копий данных является важной частью любой рабочей базы данных. Хранилище данных SQL защищает ваши данные за счет автоматической архивации активных баз данных через регулярные интервалы. Эти резервные копии позволяют toorecover из сценариев, где были повреждены данные или случайному удалению данных или базы данных.  Для hello данных расписания резервного копирования, политика хранения и как увидеть toorestore базы данных, [восстановление из снимка][Restore from snapshot].

## <a name="next-steps"></a>Дальнейшие действия
Применение принципы проектирования базы данных позволит упростить toomanage баз данных в хранилище данных SQL. Дополнительные, toolearn head через toohello [Общие сведения о разработке][Development overview].

<!--Image references-->

<!--Article references-->
[Create a SQL Data Warehouse (Azure Portal)]: sql-data-warehouse-get-started-provision.md
[Create a database (PowerShell)]: sql-data-warehouse-get-started-provision-powershell.md
[connection]: sql-data-warehouse-develop-connections.md
[Query Azure SQL Data Warehouse with Visual Studio]: sql-data-warehouse-query-visual-studio.md
[Connect and query with sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md
[Development overview]: sql-data-warehouse-overview-develop.md
[Monitor your workload using DMVs]: sql-data-warehouse-manage-monitor.md
[Pause compute]: sql-data-warehouse-manage-compute-overview.md#pause-compute-bk
[Restore from snapshot]: sql-data-warehouse-restore-database-overview.md
[Resume compute]: sql-data-warehouse-manage-compute-overview.md#resume-compute-bk
[масштабирования производительности]: sql-data-warehouse-manage-compute-overview.md#scale-compute
[Security overview]: sql-data-warehouse-overview-manage-security.md
[SQL Data Warehouse Best Practices]: sql-data-warehouse-best-practices.md
[SQL Data Warehouse system views]: sql-data-warehouse-reference-tsql-system-views.md

<!--MSDN references-->
[SQL Server Data Tools]: https://msdn.microsoft.com/library/mt204009.aspx

<!--Other web references-->
[Azure portal]: http://portal.azure.com/
