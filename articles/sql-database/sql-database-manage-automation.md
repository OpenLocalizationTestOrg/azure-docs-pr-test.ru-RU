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
# <a name="managing-azure-sql-databases-using-azure-automation"></a><span data-ttu-id="fcf22-103">Управление базами данных SQL Azure с помощью службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="fcf22-103">Managing Azure SQL Databases using Azure Automation</span></span>
<span data-ttu-id="fcf22-104">В этом руководстве приведены toohello службы автоматизации Azure и как можно toosimplify используется управление базами данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="fcf22-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of your Azure SQL databases.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="fcf22-105">Что такое служба автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="fcf22-105">What is Azure Automation?</span></span>
<span data-ttu-id="fcf22-106">[Служба автоматизации Azure](https://azure.microsoft.com/services/automation/) — это служба Azure для упрощения управления облаком путем автоматизации процессов.</span><span class="sxs-lookup"><span data-stu-id="fcf22-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="fcf22-107">С помощью службы автоматизации Azure, длительные, вручную, ошибкам и часто повторяющиеся задачи может быть автоматизированные tooincrease надежность, эффективность и toovalue времени для вашей организации.</span><span class="sxs-lookup"><span data-stu-id="fcf22-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="fcf22-108">Служба автоматизации Azure обеспечивает механизм выполнения рабочих процессов очень надежное и высокой доступности, которая масштабируется toomeet вашим потребностям по мере роста организации.</span><span class="sxs-lookup"><span data-stu-id="fcf22-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="fcf22-109">В службе автоматизации Azure процессы можно запустить вручную, в сторонних системах или по расписанию, чтобы все задачи выполнялись в нужное время.</span><span class="sxs-lookup"><span data-stu-id="fcf22-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="fcf22-110">Снизить операционные издержки и освободить ИТ / автоматический запуск DevOps toofocus сотрудников на работу, которая добавляет ценность для бизнеса, перемещая toobe задачи управления вашей облачной службой автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="fcf22-110">Lower operational overhead and free up IT / DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-sql-databases"></a><span data-ttu-id="fcf22-111">Как служба автоматизации Azure может помочь управлять базами данных SQL Azure?</span><span class="sxs-lookup"><span data-stu-id="fcf22-111">How can Azure Automation help manage Azure SQL databases?</span></span>
<span data-ttu-id="fcf22-112">База данных SQL Azure можно управлять в службе автоматизации Azure с помощью hello [базы данных SQL Azure PowerShell командлеты](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/) , которые доступны в hello [средства Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fcf22-112">Azure SQL Database can be managed in Azure Automation by using hello [Azure SQL Database PowerShell cmdlets](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/) that are available in hello [Azure PowerShell tools](/powershell/azure/overview).</span></span> <span data-ttu-id="fcf22-113">Служба автоматизации Azure имеет этих командлетов PowerShell базы данных SQL Azure, доступных стандартной hello, что позволяет выполнять все задачи управления баз данных SQL Server в службе hello.</span><span class="sxs-lookup"><span data-stu-id="fcf22-113">Azure Automation has these Azure SQL Database PowerShell cmdlets available out of hello box, so that you can perform all of your SQL DB management tasks within hello service.</span></span> <span data-ttu-id="fcf22-114">Также вы можете обеспечить эти командлеты в службе автоматизации Azure с помощью командлетов hello для других служб Azure, tooautomate сложные задачи служб Azure и систем сторонних разработчиков.</span><span class="sxs-lookup"><span data-stu-id="fcf22-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="fcf22-115">Автоматизации Azure также имеет toocommunicate возможность hello с серверами SQL непосредственно, путем выполнения команды SQL, с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fcf22-115">Azure Automation also has hello ability toocommunicate with SQL servers directly, by issuing SQL commands using PowerShell.</span></span>

<span data-ttu-id="fcf22-116">Hello [коллекции модулей runbook службы автоматизации Azure](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) содержит разнообразные продукта team и сообщества runbooks tooget работы автоматизации управления базами данных SQL Azure, других служб Azure и систем сторонних разработчиков.</span><span class="sxs-lookup"><span data-stu-id="fcf22-116">hello [Azure Automation runbook gallery](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contains a variety of product team and community runbooks tooget started automating management of Azure SQL Databases, other Azure services, and 3rd party systems.</span></span> <span data-ttu-id="fcf22-117">Коллекция модулей Runbook содержит:</span><span class="sxs-lookup"><span data-stu-id="fcf22-117">Gallery runbooks include:</span></span>

* [<span data-ttu-id="fcf22-118">Выполнение запросов SQL к базе данных SQL Server</span><span class="sxs-lookup"><span data-stu-id="fcf22-118">Run SQL queries against a SQL Server database</span></span>](https://gallery.technet.microsoft.com/scriptcenter/How-to-use-a-SQL-Command-be77f9d2)
* [<span data-ttu-id="fcf22-119">Вертикальное масштабирование (вверх или вниз) базы данных SQL Azure по расписанию</span><span class="sxs-lookup"><span data-stu-id="fcf22-119">Vertically scale (up or down) an Azure SQL Database on a schedule</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-e957354f)
* [<span data-ttu-id="fcf22-120">Усечение таблицы SQL, когда база данных достигает максимального размера</span><span class="sxs-lookup"><span data-stu-id="fcf22-120">Truncate a SQL table if its database approaches its maximum size</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Azure-Automation-Your-SQL-30f8736b)
* [<span data-ttu-id="fcf22-121">Индексирование таблиц в базе данных SQL Azure при их высокой фрагментации</span><span class="sxs-lookup"><span data-stu-id="fcf22-121">Index tables in an Azure SQL Database if they are highly fragmented</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Indexes-tables-in-an-Azure-73a2a8ea)

## <a name="next-steps"></a><span data-ttu-id="fcf22-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fcf22-122">Next steps</span></span>
<span data-ttu-id="fcf22-123">Теперь, когда вы узнали основы hello автоматизации Azure и как можно использовать toomanage баз данных Azure SQL, выполните следующие дополнительные сведения об автоматизации Azure toolearn ссылки.</span><span class="sxs-lookup"><span data-stu-id="fcf22-123">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure SQL databases, follow these links toolearn more about Azure Automation.</span></span>

* [<span data-ttu-id="fcf22-124">Обзор службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="fcf22-124">Azure Automation Overview</span></span>](../automation/automation-intro.md)
* [<span data-ttu-id="fcf22-125">Мой первый Runbook</span><span class="sxs-lookup"><span data-stu-id="fcf22-125">My first runbook</span></span>](../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="fcf22-126">План обучения работе со службой автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="fcf22-126">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)
* [<span data-ttu-id="fcf22-127">Служба автоматизации Azure: Вашей агента SQL в облаке hello</span><span class="sxs-lookup"><span data-stu-id="fcf22-127">Azure Automation: Your SQL Agent in hello Cloud</span></span>](https://azure.microsoft.com/blog/2014/06/26/azure-automation-your-sql-agent-in-the-cloud/) 

