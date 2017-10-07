---
title: "Хранилище данных SQL с TSQL aaaCreate | Документы Microsoft"
description: "Узнайте, как toocreate Azure хранилище данных SQL с помощью TSQL"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: a4e2e68e-aa9c-4dd3-abb0-f7df997d237a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 81ef59a66c61452ff8a2aca29837f155e87d017d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-sql-data-warehouse-database-by-using-transact-sql-tsql"></a>Создание базы данных хранилища данных SQL с помощью Transact-SQL (TSQL)
> [!div class="op_single_selector"]
> * [портале Azure](sql-data-warehouse-get-started-provision.md)
> * [TSQL](sql-data-warehouse-get-started-create-database-tsql.md)
> * [PowerShell](sql-data-warehouse-get-started-provision-powershell.md)
>
>

В этой статье показано, как toocreate SQL в хранилище данных с помощью T-SQL.

## <a name="prerequisites"></a>Предварительные требования
tooget работы, необходимо:

* **Учетная запись Azure**: посетите [бесплатная пробная версия] [ Azure Free Trial] или [кредиты Azure MSDN] [ MSDN Azure Credits] toocreate учетную запись.
* **Сервер SQL Azure**: см. раздел [создание логического сервера базы данных SQL Azure с портала Azure hello] [создание логического сервера базы данных SQL Azure с портала Azure hello] или [создание логического сервера базы данных SQL Azure с помощью PowerShell] [создание Azure SQL Логический сервер базы данных с помощью PowerShell] для получения дополнительных сведений.
* **Группа ресурсов**: используйте hello того же ресурса группу, что сервер Azure SQL или в разделе [как toocreate группу ресурсов][how toocreate a resource group].
* **Среда tooexecute T-SQL**: можно использовать [Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd], или [SSMS] [ SSMS] tooexecute T-SQL.

> [!NOTE]
> Создание хранилища данных SQL может привести к дополнительным расходам.  Дополнительные сведения о ценах на хранилище данных SQL см. на [этой странице][SQL Data Warehouse pricing].
>
>

## <a name="create-a-database-with-visual-studio"></a>Создание базы данных с помощью Visual Studio
Если новый tooVisual Studio, см. в статье hello [запросов хранилища данных SQL Azure (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)].  toostart, откройте обозреватель объектов SQL Server в Visual Studio и подключитесь toohello сервера, на котором размещена в базе данных хранилища данных SQL.  После подключения хранилища данных SQL можно создать, запустив следующую команду SQL для hello hello **master** базы данных.  Эта команда создает базу данных hello MySqlDwDb с целью службы DW400 и разрешить hello toogrow tooa максимальному размеру базы данных составляет 10 ТБ.

```sql
CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB);
```

## <a name="create-a-database-with-sqlcmd"></a>Создание базы данных с помощью служебной программы sqlcmd
Кроме того можно запустить hello в одной команде с помощью sqlcmd, запустив hello, выполнив в командной строке.

```sql
sqlcmd -S <Server Name>.database.windows.net -I -U <User> -P <Password> -Q "CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB)"
```

параметры сортировки по умолчанию Hello при его отсутствии — COLLATE SQL_Latin1_General_CP1_CI_AS.  Hello `MAXSIZE` может находиться в диапазоне от 250 ГБ и ТБ 240.  Hello `SERVICE_OBJECTIVE` может находиться в диапазоне от DW100 и DW2000 [DWU][DWU].  Список всех допустимых значений см. в разделе документации MSDN hello [CREATE DATABASE][CREATE DATABASE].  Hello MAXSIZE и SERVICE_OBJECTIVE можно изменить с помощью [инструкции ALTER DATABASE] [ ALTER DATABASE] команды T-SQL.  Hello параметры сортировки базы данных нельзя изменить после создания.   Следует соблюдать осторожность, когда изменение hello SERVICE_OBJECTIVE как изменение DWU приводит перезапустить службы, которая отменяет все запросы в процессе передачи.  При изменении параметра MAXSIZE службы не перезапускаются, так как это всего лишь простая операция с метаданными.

## <a name="next-steps"></a>Дальнейшие действия
После завершения подготовки, вы можете хранилище данных SQL [загрузить образцы данных] [ load sample data] или узнать о возможностях слишком[разработки][develop], [загрузки][load], или [перенести][migrate].

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[how toocreate a SQL Data Warehouse from hello Azure portal]: sql-data-warehouse-get-started-provision.md
[Query Azure SQL Data Warehouse (Visual Studio)]: sql-data-warehouse-query-visual-studio.md
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data]: sql-data-warehouse-load-sample-databases.md
[Create an Azure SQL database with hello Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[how toocreate a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md

<!--MSDN references-->
[CREATE DATABASE]: https://msdn.microsoft.com/library/mt204021.aspx
[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx
[SSMS]: https://msdn.microsoft.com/library/mt238290.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
