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
# <a name="create-an-azure-sql-data-warehouse"></a>Создание хранилища данных SQL Azure
> [!div class="op_single_selector"]
> * [Портал Azure](sql-data-warehouse-get-started-provision.md)
> * [TSQL](sql-data-warehouse-get-started-create-database-tsql.md)
> * [PowerShell](sql-data-warehouse-get-started-provision-powershell.md)
>
>

В этом учебнике используется hello Azure портала toocreate хранилища данных SQL, содержащий образце базы данных AdventureWorksDW.

## <a name="prerequisites"></a>Предварительные требования
tooget работы, необходимо:

* **Учетная запись Azure**: посетите [бесплатная пробная версия] [ Azure Free Trial] или [кредиты Azure MSDN] [ MSDN Azure Credits] toocreate учетную запись.
* **Azure SQL server**: в разделе [создать базу данных Azure SQL с портала Azure hello] [ Create an Azure SQL database in hello Azure portal] для получения дополнительных сведений.

> [!NOTE]
> Создание хранилища данных SQL может привести к дополнительным расходам.  Дополнительные сведения см. на странице [с ценами на хранилище данных SQL][SQL Data Warehouse pricing].
>
>

## <a name="create-a-sql-data-warehouse"></a>Создание хранилища данных SQL
1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Последовательно выберите **+ Создать** > **Базы данных** > **Хранилище данных SQL**.

    ![Создание](./media/sql-data-warehouse-get-started-provision/create-sample.gif)
3. В hello **хранилище данных SQL** колонки, заполните hello сведения, необходимые, нажмите клавишу toocreate «Создать».

    ![Создание базы данных](./media/sql-data-warehouse-get-started-provision/create-database.png)

   * **Сервер**. Рекомендуется сначала выбрать сервер.  
   * **Имя базы данных**: hello имя, которое используется tooreference hello хранилище данных SQL.  Оно должно быть уникальным toohello сервера.
   * **Производительность**. Мы рекомендуем начать с 400 [DWU][DWU]. Можно переместить влево toohello ползунок hello или правой tooadjust hello производительности хранилища данных или масштабирования вверх или вниз после ее создания.  toolearn Дополнительные сведения о Dwu, см. на нашей документации [масштабирование](sql-data-warehouse-manage-compute-overview.md) или [странице цен][SQL Data Warehouse pricing].
   * **Подписки**: выберите hello [подписки] , это хранилище данных SQL будет выставлять счета на.
   * **Группа ресурсов**: [групп ресурсов] [ Resource group] , toohelp контейнеры предназначены управлять коллекцией ресурсов Azure. Дополнительная информация о [группах ресурсов](../azure-resource-manager/resource-group-overview.md).
   * **Выбор источника**. Последовательно щелкните **Выбрать источник** > **Пример**. Azure автоматически заполняет hello **выберите образец** параметр с AdventureWorksDW.

   > [!NOTE]
   > параметры сортировки по умолчанию Hello для хранилища данных SQL — SQL_Latin1_General_CP1_CI_AS. При необходимости другие параметры сортировки [T-SQL] [ T-SQL] может быть база данных hello используется toocreate с другими параметрами сортировки.
   >
   >

1. Нажмите кнопку **создать** toocreate хранилище данных SQL.
2. Подождите несколько минут. Когда хранилищу данных готова, вы должны быть возвращены toohello [портал Azure](https://portal.azure.com). Можно найти хранилище данных SQL на панели мониторинга, перечисленные в базах данных SQL, или в ресурсе hello группы, toocreate вы использовали его.

    ![Портал](./media/sql-data-warehouse-get-started-provision/database-portal-view.png)

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="next-steps"></a>Дальнейшие действия
После создания хранилища данных SQL можно приступать слишком[Connect](sql-data-warehouse-connect-overview.md) и выполнять запросы.

tooload данных в хранилище данных SQL, в разделе hello [Общие сведения о загрузке](sql-data-warehouse-overview-load.md).

Если вы пытаетесь toomigrate tooSQL существующей базы данных хранилища данных, см. раздел hello [Общие сведения о миграции](sql-data-warehouse-overview-migrate.md) или использовать [программа миграции](sql-data-warehouse-migrate-migration-utility.md).

Можно также настроить правила брандмауэра с помощью Transact-SQL. Дополнительные сведения см. в документации [sp_set_firewall_rule][sp_set_firewall_rule] и [sp_set_database_firewall_rule][sp_set_database_firewall_rule].

Это также toolook идея в hello [рекомендации][Best practices].

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
