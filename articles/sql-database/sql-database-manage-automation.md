---
title: "Управление базами данных SQL Azure с помощью службы автоматизации Azure | Документация Майкрософт"
description: "Способы использования службы автоматизации Azure для управления базами данных SQL Azure при масштабировании."
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
ms.openlocfilehash: 7f45b8b654691063823c13bee61e9bb874a6a13a
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="managing-azure-sql-databases-using-azure-automation"></a>Управление базами данных SQL Azure с помощью службы автоматизации Azure
В этом руководстве будет представлена служба автоматизации Azure и способы ее использования для упрощения управления базами данных SQL Azure.

## <a name="what-is-azure-automation"></a>Что такое служба автоматизации Azure
[Служба автоматизации Azure](https://azure.microsoft.com/services/automation/) — это служба Azure для упрощения управления облаком путем автоматизации процессов. С помощью службы автоматизации Azure можно автоматизировать длительные, выполняемые вручную, ненадежные и часто повторяющиеся задачи для повышения надежности, эффективности и ускорения вывода продукта на рынок.

Служба автоматизации Azure предоставляет высоконадежную и высокодоступную подсистему выполнения рабочих процессов с масштабированием в соответствии с требованиями организации по мере ее роста. В службе автоматизации Azure процессы можно запустить вручную, в сторонних системах или по расписанию, чтобы все задачи выполнялись в нужное время.

Уменьшите операционные затраты и освободите ИТ-сотрудников и специалистов по разработке и операциям для работы над повышением бизнес-ценности ПО и автоматизации задач управления облаком в службе автоматизации Azure.

## <a name="how-can-azure-automation-help-manage-azure-sql-databases"></a>Как служба автоматизации Azure может помочь управлять базами данных SQL Azure?
Базой данных SQL Azure можно управлять в службе автоматизации Azure, используя [командлеты PowerShell для базы данных SQL Azure](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/), доступные в разделе со [средствами Azure PowerShell](/powershell/azure/overview). Служба автоматизации Azure предоставляет командлеты PowerShell базы данных SQL Azure в готовом виде, чтобы вы могли выполнять все задачи управления базами данных SQL, не выходя из службы. Вы также можете связать эти командлеты в службе автоматизации Azure с командлетами для других служб Azure, чтобы автоматизировать сложные задачи в службах Azure и системах сторонних производителей.

Служба автоматизации Azure также может взаимодействовать непосредственно с серверами SQL Server, выполняя команды SQL с помощью PowerShell.

[Коллекция модулей Runbook службы автоматизации Azure](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) содержит различные модули Runbook групп разработки продуктов и сообществ для начала работы по автоматизации управления базой данных SQL Azure, другими службами Azure, а также системами сторонних производителей. Коллекция модулей Runbook содержит:

* [Выполнение запросов SQL к базе данных SQL Server](https://gallery.technet.microsoft.com/scriptcenter/How-to-use-a-SQL-Command-be77f9d2)
* [Вертикальное масштабирование (вверх или вниз) базы данных SQL Azure по расписанию](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-e957354f)
* [Усечение таблицы SQL, когда база данных достигает максимального размера](https://gallery.technet.microsoft.com/scriptcenter/Azure-Automation-Your-SQL-30f8736b)
* [Индексирование таблиц в базе данных SQL Azure при их высокой фрагментации](https://gallery.technet.microsoft.com/scriptcenter/Indexes-tables-in-an-Azure-73a2a8ea)

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы познакомились с основами службы автоматизации Azure и способах ее использования для управления базами данных SQL Azure, пройдите по ссылкам, чтобы получить дополнительные сведения о службе автоматизации Azure.

* [Обзор службы автоматизации Azure](../automation/automation-intro.md)
* [Мой первый Runbook](../automation/automation-first-runbook-graphical.md)
* [План обучения работе со службой автоматизации Azure](https://azure.microsoft.com/documentation/learning-paths/automation/)
* [Служба автоматизации Azure: ваш агент SQL в облаке](https://azure.microsoft.com/blog/2014/06/26/azure-automation-your-sql-agent-in-the-cloud/) 

