---
title: "aaaCreate хранилище данных SQL с помощью PowerShell | Документы Microsoft"
description: "Создание хранилища данных SQL с помощью PowerShell"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 97434863-7938-4129-8949-5a119f5949e3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: d8af29ec285a11285785ab5474e4dfc8c36bc3ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-sql-data-warehouse-using-powershell"></a><span data-ttu-id="904f2-103">Создание хранилища данных SQL с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="904f2-103">Create SQL Data Warehouse using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="904f2-104">портале Azure</span><span class="sxs-lookup"><span data-stu-id="904f2-104">Azure Portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="904f2-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="904f2-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="904f2-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="904f2-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="904f2-107">В этой статье показано, как toocreate SQL в хранилище данных с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="904f2-107">This article shows you how toocreate a SQL Data Warehouse using PowerShell.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="904f2-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="904f2-108">Prerequisites</span></span>
<span data-ttu-id="904f2-109">tooget работы, необходимо:</span><span class="sxs-lookup"><span data-stu-id="904f2-109">tooget started, you need:</span></span>

* <span data-ttu-id="904f2-110">**Учетная запись Azure**: посетите [бесплатная пробная версия] [ Azure Free Trial] или [кредиты Azure MSDN] [ MSDN Azure Credits] toocreate учетную запись.</span><span class="sxs-lookup"><span data-stu-id="904f2-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] toocreate an account.</span></span>
* <span data-ttu-id="904f2-111">**Сервер SQL Azure**: в разделе [создать базу данных Azure SQL в портале Azure hello] [ Create an Azure SQL database in hello Azure Portal] или [Создание базы данных Azure SQL с помощью PowerShell] [ Create an Azure SQL database with PowerShell] для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="904f2-111">**Azure SQL server**:  See [Create an Azure SQL database in hello Azure Portal][Create an Azure SQL database in hello Azure Portal] or [Create an Azure SQL database with PowerShell][Create an Azure SQL database with PowerShell] for more details.</span></span>
* <span data-ttu-id="904f2-112">**Группа ресурсов**: используйте hello того же ресурса группу, что сервер Azure SQL или в разделе [как toocreate группу ресурсов](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="904f2-112">**Resource group**: Either use hello same resource group as your Azure SQL server or see [how toocreate a resource group](../azure-resource-manager/resource-group-portal.md).</span></span>
* <span data-ttu-id="904f2-113">**PowerShell версии 1.0.3 или более поздней.** Чтобы узнать версию, выполните командлет **Get-Module -ListAvailable -Name Azure**.</span><span class="sxs-lookup"><span data-stu-id="904f2-113">**PowerShell version 1.0.3 or greater**:  You can check your version by running **Get-Module -ListAvailable -Name Azure**.</span></span>  <span data-ttu-id="904f2-114">может быть установлена последняя версия Hello из [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="904f2-114">hello latest version can be installed from [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="904f2-115">Дополнительные сведения об установке последней версии hello см. в разделе [как tooinstall и настройка Azure PowerShell][How tooinstall and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="904f2-115">For more information on installing hello latest version, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>

> [!NOTE]
> <span data-ttu-id="904f2-116">Создание хранилища данных SQL может привести к дополнительным расходам.</span><span class="sxs-lookup"><span data-stu-id="904f2-116">Creating a SQL Data Warehouse may result in a new billable service.</span></span>  <span data-ttu-id="904f2-117">Дополнительные сведения о ценах на хранилище данных SQL см. на [этой странице][SQL Data Warehouse pricing].</span><span class="sxs-lookup"><span data-stu-id="904f2-117">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details on pricing.</span></span>
>
>

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="904f2-118">Создание хранилища данных SQL</span><span class="sxs-lookup"><span data-stu-id="904f2-118">Create a SQL Data Warehouse</span></span>
1. <span data-ttu-id="904f2-119">Откройте Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="904f2-119">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="904f2-120">Запустите этот командлет toologin tooAzure диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="904f2-120">Run this cmdlet toologin tooAzure Resource Manager.</span></span>

    ```Powershell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="904f2-121">Выберите подписку hello требуется toouse во время текущего сеанса.</span><span class="sxs-lookup"><span data-stu-id="904f2-121">Select hello subscription you want toouse for your current session.</span></span>

    ```Powershell
    Get-AzureRmSubscription    -SubscriptionName "MySubscription" | Select-AzureRmSubscription
    ```
4. <span data-ttu-id="904f2-122">Создайте базу данных.</span><span class="sxs-lookup"><span data-stu-id="904f2-122">Create database.</span></span> <span data-ttu-id="904f2-123">Этот пример создает базу данных с именем «mynewsqldw» с целевой уровень обслуживания «DW400» toohello сервера с именем «sqldwserver1», который находится в группе ресурсов hello с именем «mywesteuroperesgp1».</span><span class="sxs-lookup"><span data-stu-id="904f2-123">This example creates a database named "mynewsqldw", with service objective level "DW400", toohello server named "sqldwserver1", which is in hello resource group named "mywesteuroperesgp1".</span></span>

   ```Powershell
   New-AzureRmSqlDatabase -RequestedServiceObjectiveName "DW400" -DatabaseName "mynewsqldw" -ServerName "sqldwserver1" -ResourceGroupName "mywesteuroperesgp1" -Edition "DataWarehouse" -CollationName "SQL_Latin1_General_CP1_CI_AS" -MaxSizeBytes 10995116277760
   ```

<span data-ttu-id="904f2-124">Ниже перечислены необходимые параметры.</span><span class="sxs-lookup"><span data-stu-id="904f2-124">Required Parameters are:</span></span>

* <span data-ttu-id="904f2-125">**RequestedServiceObjectiveName**: hello объем [DWU] [ DWU] которого запрашивается.</span><span class="sxs-lookup"><span data-stu-id="904f2-125">**RequestedServiceObjectiveName**: hello amount of [DWU][DWU] you are requesting.</span></span>  <span data-ttu-id="904f2-126">Поддерживаемые значения: DW100, DW200, DW300, DW400, DW500, DW600, DW1000, DW1200, DW1500, DW2000, DW3000 и DW6000.</span><span class="sxs-lookup"><span data-stu-id="904f2-126">Supported values are: DW100, DW200, DW300, DW400, DW500, DW600, DW1000, DW1200, DW1500, DW2000, DW3000, and DW6000.</span></span>
* <span data-ttu-id="904f2-127">**Имя базы данных**: hello хранилище данных SQL, для которого создается имя hello.</span><span class="sxs-lookup"><span data-stu-id="904f2-127">**DatabaseName**: hello name of hello SQL Data Warehouse that you are creating.</span></span>
* <span data-ttu-id="904f2-128">**ServerName**: hello имя сервера "hello", который используется для создания (должен быть версии 12).</span><span class="sxs-lookup"><span data-stu-id="904f2-128">**ServerName**: hello name of hello server that you are using for creation (must be V12).</span></span>
* <span data-ttu-id="904f2-129">**ResourceGroupName**: используемая группа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="904f2-129">**ResourceGroupName**: Resource group you are using.</span></span>  <span data-ttu-id="904f2-130">toofind доступных групп ресурсов в вашей подписке используйте Get-AzureResource.</span><span class="sxs-lookup"><span data-stu-id="904f2-130">toofind available resource groups in your subscription use Get-AzureResource.</span></span>
* <span data-ttu-id="904f2-131">**Выпуск**: должно быть toocreate «Хранилище данных» хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="904f2-131">**Edition**: Must be "DataWarehouse" toocreate a SQL Data Warehouse.</span></span>

<span data-ttu-id="904f2-132">Необязательные параметры.</span><span class="sxs-lookup"><span data-stu-id="904f2-132">Optional Parameters are:</span></span>

* <span data-ttu-id="904f2-133">**CollationName**: hello параметры сортировки по умолчанию, если не указано: SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="904f2-133">**CollationName**: hello default collation if not specified is SQL_Latin1_General_CP1_CI_AS.</span></span>  <span data-ttu-id="904f2-134">Нельзя изменить параметры сортировки базы данных.</span><span class="sxs-lookup"><span data-stu-id="904f2-134">Collation cannot be changed on a database.</span></span>
* <span data-ttu-id="904f2-135">**MaxSizeBytes**: hello по умолчанию максимальный размер базы данных составляет 10 ГБ.</span><span class="sxs-lookup"><span data-stu-id="904f2-135">**MaxSizeBytes**: hello default max size of a database is 10 GB.</span></span>

<span data-ttu-id="904f2-136">Дополнительные сведения о настройки параметров hello. в разделе [New AzureRmSqlDatabase] [ New-AzureRmSqlDatabase] и [Create Database (хранилище данных SQL Azure)][Create Database (Azure SQL Data Warehouse)].</span><span class="sxs-lookup"><span data-stu-id="904f2-136">For more details on hello parameter options, see [New-AzureRmSqlDatabase][New-AzureRmSqlDatabase] and [Create Database (Azure SQL Data Warehouse)][Create Database (Azure SQL Data Warehouse)].</span></span>

## <a name="next-steps"></a><span data-ttu-id="904f2-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="904f2-137">Next steps</span></span>
<span data-ttu-id="904f2-138">После завершения хранилище данных SQL подготовки, вы можете tootry [загрузки образцов данных] [ loading sample data] или узнать о возможностях слишком[разработки] [ develop] , [загрузить][load], или [перенести][migrate].</span><span class="sxs-lookup"><span data-stu-id="904f2-138">After your SQL Data Warehouse has finished provisioning you may want tootry [loading sample data][loading sample data] or check out how too[develop][develop], [load][load], or [migrate][migrate].</span></span>

<span data-ttu-id="904f2-139">Если вы заинтересованы в Дополнительные сведения о toomanage хранилище данных SQL программными средствами, извлечь наши статьи о том, как toouse [командлеты PowerShell и API-интерфейс REST][PowerShell cmdlets and REST APIs].</span><span class="sxs-lookup"><span data-stu-id="904f2-139">If you're interested in more on how toomanage SQL Data Warehouse programmatically, check out our article on how toouse [PowerShell cmdlets and REST APIs][PowerShell cmdlets and REST APIs].</span></span>

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[migrate]: ./sql-data-warehouse-overview-migrate.md
[develop]: ./sql-data-warehouse-overview-develop.md
[load]: ./sql-data-warehouse-load-with-bcp.md
[loading sample data]: ./sql-data-warehouse-load-sample-databases.md
[PowerShell cmdlets and REST APIs]: ./sql-data-warehouse-reference-powershell-cmdlets.md
[firewall rules]: ../sql-database-configure-firewall-settings.md

[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[how toocreate a SQL Data Warehouse from hello Azure Portal]: ./sql-data-warehouse-get-started-provision.md
[Create an Azure SQL database in hello Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-get-started-powershell.md
[how toocreate a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group

<!--MSDN references-->
[MSDN]: https://msdn.microsoft.com/library/azure/dn546722.aspx
[New-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619339.aspx
[Create Database (Azure SQL Data Warehouse)]: https://msdn.microsoft.com/library/mt204021.aspx

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
