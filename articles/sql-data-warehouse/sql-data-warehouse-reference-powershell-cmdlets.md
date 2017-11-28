---
title: "командлеты aaaPowerShell для хранилища данных SQL Azure"
description: "Найти hello top командлеты PowerShell для хранилища данных SQL Azure включая то, как toopause и возобновление базы данных."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 6f0d5772-f05f-4cc8-9749-4adb153dfd50
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: reference
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: 84353b56131cf856e0724d338d7ed186fd2ceeaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="powershell-cmdlets-and-rest-apis-for-sql-data-warehouse"></a><span data-ttu-id="a0d73-103">Использование командлетов PowerShell и интерфейсов REST API при работе с хранилищем данных SQL</span><span class="sxs-lookup"><span data-stu-id="a0d73-103">PowerShell cmdlets and REST APIs for SQL Data Warehouse</span></span>
<span data-ttu-id="a0d73-104">Многими задачами по администрированию хранилища данных SQL можно управлять с помощью командлетов Azure PowerShell или интерфейсов API REST.</span><span class="sxs-lookup"><span data-stu-id="a0d73-104">Many SQL Data Warehouse administration tasks can be managed using either Azure PowerShell cmdlets or REST APIs.</span></span>  <span data-ttu-id="a0d73-105">Ниже приведены некоторые примеры как toouse PowerShell команды tooautomate распространенные задачи в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="a0d73-105">Below are some examples of how toouse PowerShell commands tooautomate common tasks in your SQL Data Warehouse.</span></span>  <span data-ttu-id="a0d73-106">Хорошие примеры REST, в статье hello [управление масштабируемости с ОСТАЛЬНОЙ][Manage scalability with REST].</span><span class="sxs-lookup"><span data-stu-id="a0d73-106">For some good REST examples, see hello article [Manage scalability with REST][Manage scalability with REST].</span></span>

> [!NOTE]
> <span data-ttu-id="a0d73-107">В порядке toouse Azure PowerShell с хранилищем данных SQL, необходим Azure PowerShell версия 1.0.3 или выше.</span><span class="sxs-lookup"><span data-stu-id="a0d73-107">In order toouse Azure PowerShell with SQL Data Warehouse, you need Azure PowerShell version 1.0.3 or greater.</span></span>  <span data-ttu-id="a0d73-108">Чтобы узнать версию, выполните командлет **Get-Module -ListAvailable -Name Azure**.</span><span class="sxs-lookup"><span data-stu-id="a0d73-108">You can check your version by running **Get-Module -ListAvailable -Name Azure**.</span></span>  <span data-ttu-id="a0d73-109">может быть установлена последняя версия Hello из [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="a0d73-109">hello latest version can be installed from  [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="a0d73-110">Дополнительные сведения об установке последней версии hello см. в разделе [как tooinstall и настройка Azure PowerShell][How tooinstall and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="a0d73-110">For more information on installing hello latest version, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>
> 
> 

## <a name="get-started-with-azure-powershell-cmdlets"></a><span data-ttu-id="a0d73-111">Приступая к работе с командлетами Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0d73-111">Get started with Azure PowerShell cmdlets</span></span>
1. <span data-ttu-id="a0d73-112">Откройте Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a0d73-112">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="a0d73-113">В командной строке PowerShell hello запустите эти команды toosign в toohello диспетчера ресурсов Azure и выберите подписку.</span><span class="sxs-lookup"><span data-stu-id="a0d73-113">At hello PowerShell prompt, run these commands toosign in toohello Azure Resource Manager and select your subscription.</span></span>
   
    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

## <a name="pause-sql-data-warehouse-example"></a><span data-ttu-id="a0d73-114">Пример приостановки хранилища данных SQL</span><span class="sxs-lookup"><span data-stu-id="a0d73-114">Pause SQL Data Warehouse Example</span></span>
<span data-ttu-id="a0d73-115">Приостанавливает базу данных с именем Database02, размещенную на сервере с именем Server01.</span><span class="sxs-lookup"><span data-stu-id="a0d73-115">Pause a database named "Database02" hosted on a server named "Server01."</span></span>  <span data-ttu-id="a0d73-116">Hello сервер находится в группе ресурсов Azure с именем «ResourceGroup1.»</span><span class="sxs-lookup"><span data-stu-id="a0d73-116">hello server is in an Azure resource group named "ResourceGroup1."</span></span>

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
```
<span data-ttu-id="a0d73-117">Вариант, в этом примере передает полученные hello объекта слишком[Suspend AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="a0d73-117">A variation, this example pipes hello retrieved object too[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span></span>  <span data-ttu-id="a0d73-118">В результате hello базы данных приостановлено.</span><span class="sxs-lookup"><span data-stu-id="a0d73-118">As a result, hello database is paused.</span></span> <span data-ttu-id="a0d73-119">Последняя команда Hello показывает результаты hello.</span><span class="sxs-lookup"><span data-stu-id="a0d73-119">hello final command shows hello results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

## <a name="start-sql-data-warehouse-example"></a><span data-ttu-id="a0d73-120">Пример запуска хранилища данных SQL</span><span class="sxs-lookup"><span data-stu-id="a0d73-120">Start SQL Data Warehouse Example</span></span>
<span data-ttu-id="a0d73-121">Возобновляет работу базы данных с именем Database02, размещенную на сервере с именем Server01.</span><span class="sxs-lookup"><span data-stu-id="a0d73-121">Resume operation of a database named "Database02" hosted on a server named "Server01."</span></span> <span data-ttu-id="a0d73-122">Hello server содержится в группе ресурсов с именем «ResourceGroup1.»</span><span class="sxs-lookup"><span data-stu-id="a0d73-122">hello server is contained in a resource group named "ResourceGroup1."</span></span>

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" -DatabaseName "Database02"
```

<span data-ttu-id="a0d73-123">Как вариант, в этом примере извлекается база данных с именем Database02 с сервера Server01, который находится в группе ресурсов с именем ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="a0d73-123">A variation, this example retrieves a database named "Database02" from a server named "Server01" that is contained in a resource group named "ResourceGroup1."</span></span> <span data-ttu-id="a0d73-124">Она передает полученные hello объекта слишком[Resume AzureRmSqlDatabase][Resume-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="a0d73-124">It pipes hello retrieved object too[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase].</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
```

> [!NOTE]
> <span data-ttu-id="a0d73-125">Обратите внимание, что если сервер является foo.database.windows.net, используйте «foo» как hello - ServerName в командлеты PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="a0d73-125">Note that if your server is foo.database.windows.net, use "foo" as hello -ServerName in hello PowerShell cmdlets.</span></span>
> 
> 

## <a name="other-supported-powershell-cmdlets"></a><span data-ttu-id="a0d73-126">Другие поддерживаемые командлеты PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0d73-126">Other supported PowerShell cmdlets</span></span>
<span data-ttu-id="a0d73-127">Перечисленные ниже командлеты PowerShell поддерживаются хранилищем данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a0d73-127">These PowerShell cmdlets are supported with Azure SQL Data Warehouse.</span></span>

* <span data-ttu-id="a0d73-128">[Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="a0d73-128">[Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="a0d73-129">[Get-AzureRmSqlDeletedDatabaseBackup][Get-AzureRmSqlDeletedDatabaseBackup]</span><span class="sxs-lookup"><span data-stu-id="a0d73-129">[Get-AzureRmSqlDeletedDatabaseBackup][Get-AzureRmSqlDeletedDatabaseBackup]</span></span>
* <span data-ttu-id="a0d73-130">[Get-AzureRmSqlDatabaseRestorePoints][Get-AzureRmSqlDatabaseRestorePoints]</span><span class="sxs-lookup"><span data-stu-id="a0d73-130">[Get-AzureRmSqlDatabaseRestorePoints][Get-AzureRmSqlDatabaseRestorePoints]</span></span>
* <span data-ttu-id="a0d73-131">[New-AzureRmSqlDatabase][New-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="a0d73-131">[New-AzureRmSqlDatabase][New-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="a0d73-132">[Remove-AzureRmSqlDatabase][Remove-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="a0d73-132">[Remove-AzureRmSqlDatabase][Remove-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="a0d73-133">[Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="a0d73-133">[Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="a0d73-134">[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="a0d73-134">[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="a0d73-135">[Select-AzureRmSubscription][Select-AzureRmSubscription]</span><span class="sxs-lookup"><span data-stu-id="a0d73-135">[Select-AzureRmSubscription][Select-AzureRmSubscription]</span></span>
* <span data-ttu-id="a0d73-136">[Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="a0d73-136">[Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="a0d73-137">[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="a0d73-137">[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0d73-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a0d73-138">Next steps</span></span>
<span data-ttu-id="a0d73-139">Дополнительные примеры PowerShell см. в указанных далее документах.</span><span class="sxs-lookup"><span data-stu-id="a0d73-139">For more PowerShell examples, see:</span></span>

* <span data-ttu-id="a0d73-140">[Создание хранилища данных SQL с помощью PowerShell][Create a SQL Data Warehouse using PowerShell]</span><span class="sxs-lookup"><span data-stu-id="a0d73-140">[Create a SQL Data Warehouse using PowerShell][Create a SQL Data Warehouse using PowerShell]</span></span>
* <span data-ttu-id="a0d73-141">[Восстановление базы данных][Database restore]</span><span class="sxs-lookup"><span data-stu-id="a0d73-141">[Database restore][Database restore]</span></span>

<span data-ttu-id="a0d73-142">Другие задачи, которые можно автоматизировать с помощью PowerShell, описаны в статье о [командлетах Базы данных SQL Azure][Azure SQL Database Cmdlets].</span><span class="sxs-lookup"><span data-stu-id="a0d73-142">For other tasks which can be automated with PowerShell, see [Azure SQL Database Cmdlets][Azure SQL Database Cmdlets].</span></span> <span data-ttu-id="a0d73-143">Обратите внимание, что хранилище данных SQL Azure поддерживает не все командлеты для базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a0d73-143">Note that not all Azure SQL Database cmdlets are supported for Azure SQL Data Warehouse.</span></span>  <span data-ttu-id="a0d73-144">Список задач, которые можно автоматизировать с помощью REST, см. в статье [Operations for Azure SQL Databases][Operations for Azure SQL Databases] (Операции для баз данных SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="a0d73-144">For a list of tasks which can be automated with REST, see [Operations for Azure SQL Databases][Operations for Azure SQL Databases].</span></span>

<!--Image references-->

<!--Article references-->
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Create a SQL Data Warehouse using PowerShell]: ./sql-data-warehouse-get-started-provision-powershell.md
[Database restore]: ./sql-data-warehouse-restore-database-powershell.md
[Manage scalability with REST]: ./sql-data-warehouse-manage-compute-rest-api.md

<!--MSDN references-->
[Azure SQL Database Cmdlets]: https://msdn.microsoft.com/library/mt574084.aspx
[Operations for Azure SQL Databases]: https://msdn.microsoft.com/library/azure/dn505719.aspx
[Get-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt603648.aspx
[Get-AzureRmSqlDeletedDatabaseBackup]: https://msdn.microsoft.com/library/mt693387.aspx
[Get-AzureRmSqlDatabaseRestorePoints]: https://msdn.microsoft.com/library/mt603642.aspx
[New-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619339.aspx
[Remove-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619368.aspx
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx
[Resume-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619347.aspx
<!-- It appears that Select-AzureRmSubscription isn't documented, so this points tooSelect-AzureSubscription -->
[Select-AzureRmSubscription]: https://msdn.microsoft.com/library/dn722499.aspx
[Set-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619433.aspx
[Suspend-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619337.aspx

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
