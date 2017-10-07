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
# <a name="create-sql-data-warehouse-using-powershell"></a>Создание хранилища данных SQL с помощью PowerShell
> [!div class="op_single_selector"]
> * [портале Azure](sql-data-warehouse-get-started-provision.md)
> * [TSQL](sql-data-warehouse-get-started-create-database-tsql.md)
> * [PowerShell](sql-data-warehouse-get-started-provision-powershell.md)
>
>

В этой статье показано, как toocreate SQL в хранилище данных с помощью PowerShell.

## <a name="prerequisites"></a>Предварительные требования
tooget работы, необходимо:

* **Учетная запись Azure**: посетите [бесплатная пробная версия] [ Azure Free Trial] или [кредиты Azure MSDN] [ MSDN Azure Credits] toocreate учетную запись.
* **Сервер SQL Azure**: в разделе [создать базу данных Azure SQL в портале Azure hello] [ Create an Azure SQL database in hello Azure Portal] или [Создание базы данных Azure SQL с помощью PowerShell] [ Create an Azure SQL database with PowerShell] для получения дополнительных сведений.
* **Группа ресурсов**: используйте hello того же ресурса группу, что сервер Azure SQL или в разделе [как toocreate группу ресурсов](../azure-resource-manager/resource-group-portal.md).
* **PowerShell версии 1.0.3 или более поздней.** Чтобы узнать версию, выполните командлет **Get-Module -ListAvailable -Name Azure**.  может быть установлена последняя версия Hello из [Microsoft Web Platform Installer][Microsoft Web Platform Installer].  Дополнительные сведения об установке последней версии hello см. в разделе [как tooinstall и настройка Azure PowerShell][How tooinstall and configure Azure PowerShell].

> [!NOTE]
> Создание хранилища данных SQL может привести к дополнительным расходам.  Дополнительные сведения о ценах на хранилище данных SQL см. на [этой странице][SQL Data Warehouse pricing].
>
>

## <a name="create-a-sql-data-warehouse"></a>Создание хранилища данных SQL
1. Откройте Windows PowerShell.
2. Запустите этот командлет toologin tooAzure диспетчера ресурсов.

    ```Powershell
    Login-AzureRmAccount
    ```
3. Выберите подписку hello требуется toouse во время текущего сеанса.

    ```Powershell
    Get-AzureRmSubscription    -SubscriptionName "MySubscription" | Select-AzureRmSubscription
    ```
4. Создайте базу данных. Этот пример создает базу данных с именем «mynewsqldw» с целевой уровень обслуживания «DW400» toohello сервера с именем «sqldwserver1», который находится в группе ресурсов hello с именем «mywesteuroperesgp1».

   ```Powershell
   New-AzureRmSqlDatabase -RequestedServiceObjectiveName "DW400" -DatabaseName "mynewsqldw" -ServerName "sqldwserver1" -ResourceGroupName "mywesteuroperesgp1" -Edition "DataWarehouse" -CollationName "SQL_Latin1_General_CP1_CI_AS" -MaxSizeBytes 10995116277760
   ```

Ниже перечислены необходимые параметры.

* **RequestedServiceObjectiveName**: hello объем [DWU] [ DWU] которого запрашивается.  Поддерживаемые значения: DW100, DW200, DW300, DW400, DW500, DW600, DW1000, DW1200, DW1500, DW2000, DW3000 и DW6000.
* **Имя базы данных**: hello хранилище данных SQL, для которого создается имя hello.
* **ServerName**: hello имя сервера "hello", который используется для создания (должен быть версии 12).
* **ResourceGroupName**: используемая группа ресурсов.  toofind доступных групп ресурсов в вашей подписке используйте Get-AzureResource.
* **Выпуск**: должно быть toocreate «Хранилище данных» хранилища данных SQL.

Необязательные параметры.

* **CollationName**: hello параметры сортировки по умолчанию, если не указано: SQL_Latin1_General_CP1_CI_AS.  Нельзя изменить параметры сортировки базы данных.
* **MaxSizeBytes**: hello по умолчанию максимальный размер базы данных составляет 10 ГБ.

Дополнительные сведения о настройки параметров hello. в разделе [New AzureRmSqlDatabase] [ New-AzureRmSqlDatabase] и [Create Database (хранилище данных SQL Azure)][Create Database (Azure SQL Data Warehouse)].

## <a name="next-steps"></a>Дальнейшие действия
После завершения хранилище данных SQL подготовки, вы можете tootry [загрузки образцов данных] [ loading sample data] или узнать о возможностях слишком[разработки] [ develop] , [загрузить][load], или [перенести][migrate].

Если вы заинтересованы в Дополнительные сведения о toomanage хранилище данных SQL программными средствами, извлечь наши статьи о том, как toouse [командлеты PowerShell и API-интерфейс REST][PowerShell cmdlets and REST APIs].

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
