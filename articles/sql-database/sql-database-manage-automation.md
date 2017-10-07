---
title: "aaaManage баз данных SQL Azure с помощью службы автоматизации Azure | Документы Microsoft"
description: "Узнайте, как hello службы автоматизации Azure можно использовать toomanage баз данных Azure SQL в масштабе."
services: sql-database, automation
documentationcenter: 
author: jodoglevy
manager: jhubbard
editor: monicar
ms.assetid: 77c262a1-9b93-456d-b3c7-b2f23bdfcd61
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: jhubbard
ms.openlocfilehash: d613cca32ba86e27b9c1b952c4e723ea7f07beb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-sql-databases-using-azure-automation"></a>Управление базами данных SQL Azure с помощью службы автоматизации Azure
В этом руководстве приведены toohello службы автоматизации Azure и как можно toosimplify используется управление базами данных Azure SQL.

## <a name="what-is-azure-automation"></a>Что такое служба автоматизации Azure
[Служба автоматизации Azure](https://azure.microsoft.com/services/automation/) — это служба Azure для упрощения управления облаком путем автоматизации процессов. С помощью службы автоматизации Azure, длительные, вручную, ошибкам и часто повторяющиеся задачи может быть автоматизированные tooincrease надежность, эффективность и toovalue времени для вашей организации.

Служба автоматизации Azure обеспечивает механизм выполнения рабочих процессов очень надежное и высокой доступности, которая масштабируется toomeet вашим потребностям по мере роста организации. В службе автоматизации Azure процессы можно запустить вручную, в сторонних системах или по расписанию, чтобы все задачи выполнялись в нужное время.

Снизить операционные издержки и освободить ИТ / автоматический запуск DevOps toofocus сотрудников на работу, которая добавляет ценность для бизнеса, перемещая toobe задачи управления вашей облачной службой автоматизации Azure.

## <a name="how-can-azure-automation-help-manage-azure-sql-databases"></a>Как служба автоматизации Azure может помочь управлять базами данных SQL Azure?
База данных SQL Azure можно управлять в службе автоматизации Azure с помощью hello [базы данных SQL Azure PowerShell командлеты](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/) , которые доступны в hello [средства Azure PowerShell](/powershell/azure/overview). Служба автоматизации Azure имеет этих командлетов PowerShell базы данных SQL Azure, доступных стандартной hello, что позволяет выполнять все задачи управления баз данных SQL Server в службе hello. Также вы можете обеспечить эти командлеты в службе автоматизации Azure с помощью командлетов hello для других служб Azure, tooautomate сложные задачи служб Azure и систем сторонних разработчиков.

Автоматизации Azure также имеет toocommunicate возможность hello с серверами SQL непосредственно, путем выполнения команды SQL, с помощью PowerShell.

Hello [коллекции модулей runbook службы автоматизации Azure](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) содержит разнообразные продукта team и сообщества runbooks tooget работы автоматизации управления базами данных SQL Azure, других служб Azure и систем сторонних разработчиков. Коллекция модулей Runbook содержит:

* [Выполнение запросов SQL к базе данных SQL Server](https://gallery.technet.microsoft.com/scriptcenter/How-to-use-a-SQL-Command-be77f9d2)
* [Вертикальное масштабирование (вверх или вниз) базы данных SQL Azure по расписанию](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-e957354f)
* [Усечение таблицы SQL, когда база данных достигает максимального размера](https://gallery.technet.microsoft.com/scriptcenter/Azure-Automation-Your-SQL-30f8736b)
* [Индексирование таблиц в базе данных SQL Azure при их высокой фрагментации](https://gallery.technet.microsoft.com/scriptcenter/Indexes-tables-in-an-Azure-73a2a8ea)

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы узнали основы hello автоматизации Azure и как можно использовать toomanage баз данных Azure SQL, выполните следующие дополнительные сведения об автоматизации Azure toolearn ссылки.

* [Обзор службы автоматизации Azure](../automation/automation-intro.md)
* [Мой первый Runbook](../automation/automation-first-runbook-graphical.md)
* [План обучения работе со службой автоматизации Azure](https://azure.microsoft.com/documentation/learning-paths/automation/)
* [Служба автоматизации Azure: Вашей агента SQL в облаке hello](https://azure.microsoft.com/blog/2014/06/26/azure-automation-your-sql-agent-in-the-cloud/) 

