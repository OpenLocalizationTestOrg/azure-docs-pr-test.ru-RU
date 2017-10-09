---
title: "aaaCreate хранилища данных SQL в hello портал Azure | Документы Microsoft"
description: "Узнайте, как toocreate в хранилище данных SQL Azure в hello портал Azure"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: 552e496e-d560-419c-9996-6bbc80c521cb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: f5be6e3f2936e3af9d099854a468f8ce66fd8fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-sql-data-warehouse"></a><span data-ttu-id="22569-103">Создание хранилища данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="22569-103">Create an Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="22569-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="22569-104">Azure portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="22569-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="22569-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="22569-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="22569-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="22569-107">В этом учебнике используется hello Azure портала toocreate хранилища данных SQL, содержащий образце базы данных AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="22569-107">This tutorial uses hello Azure portal toocreate a SQL Data Warehouse that contains an AdventureWorksDW sample database.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22569-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="22569-108">Prerequisites</span></span>
<span data-ttu-id="22569-109">tooget работы, необходимо:</span><span class="sxs-lookup"><span data-stu-id="22569-109">tooget started, you need:</span></span>

* <span data-ttu-id="22569-110">**Учетная запись Azure**: посетите [бесплатная пробная версия] [ Azure Free Trial] или [кредиты Azure MSDN] [ MSDN Azure Credits] toocreate учетную запись.</span><span class="sxs-lookup"><span data-stu-id="22569-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] toocreate an account.</span></span>
* <span data-ttu-id="22569-111">**Azure SQL server**: в разделе [создать базу данных Azure SQL с портала Azure hello] [ Create an Azure SQL database in hello Azure portal] для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="22569-111">**Azure SQL server**:  See [Create an Azure SQL database with hello Azure portal][Create an Azure SQL database in hello Azure portal] for more details.</span></span>

> [!NOTE]
> <span data-ttu-id="22569-112">Создание хранилища данных SQL может привести к дополнительным расходам.</span><span class="sxs-lookup"><span data-stu-id="22569-112">Creating a SQL Data Warehouse might result in a new billable service.</span></span>  <span data-ttu-id="22569-113">Дополнительные сведения см. на странице [с ценами на хранилище данных SQL][SQL Data Warehouse pricing].</span><span class="sxs-lookup"><span data-stu-id="22569-113">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details.</span></span>
>
>

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="22569-114">Создание хранилища данных SQL</span><span class="sxs-lookup"><span data-stu-id="22569-114">Create a SQL Data Warehouse</span></span>
1. <span data-ttu-id="22569-115">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="22569-115">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="22569-116">Последовательно выберите **+ Создать** > **Базы данных** > **Хранилище данных SQL**.</span><span class="sxs-lookup"><span data-stu-id="22569-116">Click **+ New** > **Databases** > **SQL Data Warehouse**.</span></span>

    ![Создание](./media/sql-data-warehouse-get-started-provision/create-sample.gif)
3. <span data-ttu-id="22569-118">В hello **хранилище данных SQL** колонки, заполните hello сведения, необходимые, нажмите клавишу toocreate «Создать».</span><span class="sxs-lookup"><span data-stu-id="22569-118">In hello **SQL Data Warehouse** blade, fill in hello information needed, then press 'Create' toocreate.</span></span>

    ![Создание базы данных](./media/sql-data-warehouse-get-started-provision/create-database.png)

   * <span data-ttu-id="22569-120">**Сервер**. Рекомендуется сначала выбрать сервер.</span><span class="sxs-lookup"><span data-stu-id="22569-120">**Server**: We recommend you select your server first.</span></span>  
   * <span data-ttu-id="22569-121">**Имя базы данных**: hello имя, которое используется tooreference hello хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="22569-121">**Database name**: hello name that is used tooreference hello SQL Data Warehouse.</span></span>  <span data-ttu-id="22569-122">Оно должно быть уникальным toohello сервера.</span><span class="sxs-lookup"><span data-stu-id="22569-122">It must be unique toohello server.</span></span>
   * <span data-ttu-id="22569-123">**Производительность**. Мы рекомендуем начать с 400 [DWU][DWU].</span><span class="sxs-lookup"><span data-stu-id="22569-123">**Performance**: We recommend starting with 400 [DWUs][DWU].</span></span> <span data-ttu-id="22569-124">Можно переместить влево toohello ползунок hello или правой tooadjust hello производительности хранилища данных или масштабирования вверх или вниз после ее создания.</span><span class="sxs-lookup"><span data-stu-id="22569-124">You can move hello slider toohello left or right tooadjust hello performance of your data warehouse, or scale up or down after creation.</span></span>  <span data-ttu-id="22569-125">toolearn Дополнительные сведения о Dwu, см. на нашей документации [масштабирование](sql-data-warehouse-manage-compute-overview.md) или [странице цен][SQL Data Warehouse pricing].</span><span class="sxs-lookup"><span data-stu-id="22569-125">toolearn more about DWUs, see our documentation on [scaling](sql-data-warehouse-manage-compute-overview.md) or our [pricing page][SQL Data Warehouse pricing].</span></span>
   * <span data-ttu-id="22569-126">**Подписки**: выберите hello [подписки] , это хранилище данных SQL будет выставлять счета на.</span><span class="sxs-lookup"><span data-stu-id="22569-126">**Subscription**: Select hello [subscription] that this SQL Data Warehouse will bill to.</span></span>
   * <span data-ttu-id="22569-127">**Группа ресурсов**: [групп ресурсов] [ Resource group] , toohelp контейнеры предназначены управлять коллекцией ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="22569-127">**Resource group**: [Resource groups][Resource group] are containers designed toohelp you manage a collection of Azure resources.</span></span> <span data-ttu-id="22569-128">Дополнительная информация о [группах ресурсов](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="22569-128">Learn more about [resource groups](../azure-resource-manager/resource-group-overview.md).</span></span>
   * <span data-ttu-id="22569-129">**Выбор источника**. Последовательно щелкните **Выбрать источник** > **Пример**.</span><span class="sxs-lookup"><span data-stu-id="22569-129">**Select source**: Click **Select source** > **Sample**.</span></span> <span data-ttu-id="22569-130">Azure автоматически заполняет hello **выберите образец** параметр с AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="22569-130">Azure automatically populates hello **Select sample** option with AdventureWorksDW.</span></span>

   > [!NOTE]
   > <span data-ttu-id="22569-131">параметры сортировки по умолчанию Hello для хранилища данных SQL — SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="22569-131">hello default collation for a SQL Data Warehouse is SQL_Latin1_General_CP1_CI_AS.</span></span> <span data-ttu-id="22569-132">При необходимости другие параметры сортировки [T-SQL] [ T-SQL] может быть база данных hello используется toocreate с другими параметрами сортировки.</span><span class="sxs-lookup"><span data-stu-id="22569-132">If a different collation is needed, [T-SQL][T-SQL] can be used toocreate hello database with a different collation.</span></span>
   >
   >

1. <span data-ttu-id="22569-133">Нажмите кнопку **создать** toocreate хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="22569-133">Click **Create** toocreate your SQL Data Warehouse.</span></span>
2. <span data-ttu-id="22569-134">Подождите несколько минут.</span><span class="sxs-lookup"><span data-stu-id="22569-134">Wait for a few minutes.</span></span> <span data-ttu-id="22569-135">Когда хранилищу данных готова, вы должны быть возвращены toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="22569-135">When your data warehouse is ready, you should be returned toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="22569-136">Можно найти хранилище данных SQL на панели мониторинга, перечисленные в базах данных SQL, или в ресурсе hello группы, toocreate вы использовали его.</span><span class="sxs-lookup"><span data-stu-id="22569-136">You can find your SQL Data Warehouse on your dashboard, listed under your SQL Databases, or in hello resource group that you used toocreate it.</span></span>

    ![Портал](./media/sql-data-warehouse-get-started-provision/database-portal-view.png)

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="22569-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="22569-138">Next steps</span></span>
<span data-ttu-id="22569-139">После создания хранилища данных SQL можно приступать слишком[Connect](sql-data-warehouse-connect-overview.md) и выполнять запросы.</span><span class="sxs-lookup"><span data-stu-id="22569-139">Now that you have created a SQL Data Warehouse, you are ready too[Connect](sql-data-warehouse-connect-overview.md) and begin querying.</span></span>

<span data-ttu-id="22569-140">tooload данных в хранилище данных SQL, в разделе hello [Общие сведения о загрузке](sql-data-warehouse-overview-load.md).</span><span class="sxs-lookup"><span data-stu-id="22569-140">tooload data into SQL Data Warehouse, see hello [loading overview](sql-data-warehouse-overview-load.md).</span></span>

<span data-ttu-id="22569-141">Если вы пытаетесь toomigrate tooSQL существующей базы данных хранилища данных, см. раздел hello [Общие сведения о миграции](sql-data-warehouse-overview-migrate.md) или использовать [программа миграции](sql-data-warehouse-migrate-migration-utility.md).</span><span class="sxs-lookup"><span data-stu-id="22569-141">If you are trying toomigrate an existing database tooSQL Data Warehouse, see hello [Migration overview](sql-data-warehouse-overview-migrate.md) or use [Migration Utility](sql-data-warehouse-migrate-migration-utility.md).</span></span>

<span data-ttu-id="22569-142">Можно также настроить правила брандмауэра с помощью Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="22569-142">Firewall rules can also be configured using Transact-SQL.</span></span> <span data-ttu-id="22569-143">Дополнительные сведения см. в документации [sp_set_firewall_rule][sp_set_firewall_rule] и [sp_set_database_firewall_rule][sp_set_database_firewall_rule].</span><span class="sxs-lookup"><span data-stu-id="22569-143">For more information, see [sp_set_firewall_rule][sp_set_firewall_rule] and [sp_set_database_firewall_rule][sp_set_database_firewall_rule].</span></span>

<span data-ttu-id="22569-144">Это также toolook идея в hello [рекомендации][Best practices].</span><span class="sxs-lookup"><span data-stu-id="22569-144">It's also a great idea toolook at hello [Best practices][Best practices].</span></span>

<!--Article references-->
[Create an Azure SQL database in hello Azure portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[resource groups]: ../azure-resource-manager/resource-group-template-deploy-portal.md
[Best practices]: sql-data-warehouse-best-practices.md
[DWU]: sql-data-warehouse-overview-what-is.md
[подписки]: ../azure-glossary-cloud-terminology.md#subscription
[resource group]: ../azure-glossary-cloud-terminology.md#resource-group
[T-SQL]: ./sql-data-warehouse-get-started-create-database-tsql.md

<!--MSDN references-->
[sp_set_firewall_rule]: https://msdn.microsoft.com/library/dn270017.aspx
[sp_set_database_firewall_rule]: https://msdn.microsoft.com/library/dn270010.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
