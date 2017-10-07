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
# <a name="powershell-cmdlets-and-rest-apis-for-sql-data-warehouse"></a>Использование командлетов PowerShell и интерфейсов REST API при работе с хранилищем данных SQL
Многими задачами по администрированию хранилища данных SQL можно управлять с помощью командлетов Azure PowerShell или интерфейсов API REST.  Ниже приведены некоторые примеры как toouse PowerShell команды tooautomate распространенные задачи в хранилище данных SQL.  Хорошие примеры REST, в статье hello [управление масштабируемости с ОСТАЛЬНОЙ][Manage scalability with REST].

> [!NOTE]
> В порядке toouse Azure PowerShell с хранилищем данных SQL, необходим Azure PowerShell версия 1.0.3 или выше.  Чтобы узнать версию, выполните командлет **Get-Module -ListAvailable -Name Azure**.  может быть установлена последняя версия Hello из [Microsoft Web Platform Installer][Microsoft Web Platform Installer].  Дополнительные сведения об установке последней версии hello см. в разделе [как tooinstall и настройка Azure PowerShell][How tooinstall and configure Azure PowerShell].
> 
> 

## <a name="get-started-with-azure-powershell-cmdlets"></a>Приступая к работе с командлетами Azure PowerShell
1. Откройте Windows PowerShell.
2. В командной строке PowerShell hello запустите эти команды toosign в toohello диспетчера ресурсов Azure и выберите подписку.
   
    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

## <a name="pause-sql-data-warehouse-example"></a>Пример приостановки хранилища данных SQL
Приостанавливает базу данных с именем Database02, размещенную на сервере с именем Server01.  Hello сервер находится в группе ресурсов Azure с именем «ResourceGroup1.»

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
```
Вариант, в этом примере передает полученные hello объекта слишком[Suspend AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].  В результате hello базы данных приостановлено. Последняя команда Hello показывает результаты hello.

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

## <a name="start-sql-data-warehouse-example"></a>Пример запуска хранилища данных SQL
Возобновляет работу базы данных с именем Database02, размещенную на сервере с именем Server01. Hello server содержится в группе ресурсов с именем «ResourceGroup1.»

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" -DatabaseName "Database02"
```

Как вариант, в этом примере извлекается база данных с именем Database02 с сервера Server01, который находится в группе ресурсов с именем ResourceGroup1. Она передает полученные hello объекта слишком[Resume AzureRmSqlDatabase][Resume-AzureRmSqlDatabase].

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
```

> [!NOTE]
> Обратите внимание, что если сервер является foo.database.windows.net, используйте «foo» как hello - ServerName в командлеты PowerShell hello.
> 
> 

## <a name="other-supported-powershell-cmdlets"></a>Другие поддерживаемые командлеты PowerShell
Перечисленные ниже командлеты PowerShell поддерживаются хранилищем данных SQL Azure.

* [Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase]
* [Get-AzureRmSqlDeletedDatabaseBackup][Get-AzureRmSqlDeletedDatabaseBackup]
* [Get-AzureRmSqlDatabaseRestorePoints][Get-AzureRmSqlDatabaseRestorePoints]
* [New-AzureRmSqlDatabase][New-AzureRmSqlDatabase]
* [Remove-AzureRmSqlDatabase][Remove-AzureRmSqlDatabase]
* [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase]
* [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]
* [Select-AzureRmSubscription][Select-AzureRmSubscription]
* [Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase]
* [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные примеры PowerShell см. в указанных далее документах.

* [Создание хранилища данных SQL с помощью PowerShell][Create a SQL Data Warehouse using PowerShell]
* [Восстановление базы данных][Database restore]

Другие задачи, которые можно автоматизировать с помощью PowerShell, описаны в статье о [командлетах Базы данных SQL Azure][Azure SQL Database Cmdlets]. Обратите внимание, что хранилище данных SQL Azure поддерживает не все командлеты для базы данных SQL Azure.  Список задач, которые можно автоматизировать с помощью REST, см. в статье [Operations for Azure SQL Databases][Operations for Azure SQL Databases] (Операции для баз данных SQL Azure).

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
