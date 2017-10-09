---
title: "aaaManage вычислительная мощность в хранилище данных SQL Azure (PowerShell) | Документы Microsoft"
description: "PowerShell задачи toomanage вычислительной мощности. Масштабирование вычислительных ресурсов путем изменения числа единиц DWU. Или, приостанавливать и возобновлять toosave затраты вычислительных ресурсов."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 8354a3c1-4e04-4809-933f-db414a8c74dc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 8b379d4cf89570649767f6896d2c630d4f1111d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-powershell"></a>Управление вычислительными ресурсами в хранилище данных SQL Azure (PowerShell)
> [!div class="op_single_selector"]
> * [Обзор](sql-data-warehouse-manage-compute-overview.md)
> * [Портал](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>

## <a name="before-you-begin"></a>Перед началом работы
### <a name="install-hello-latest-version-of-azure-powershell"></a>Установите последнюю версию Azure PowerShell hello
> [!NOTE]
> toouse Azure PowerShell с хранилищем данных SQL необходимо Azure PowerShell версия 1.0.3 или выше.  tooverify текущей версии выполните команду hello **Get-Module - ListAvailable-Name Azure**. Можно установить последнюю версию hello с [Microsoft Web Platform Installer][Microsoft Web Platform Installer].  Дополнительные сведения см. в разделе [как tooinstall и настройка Azure PowerShell][How tooinstall and configure Azure PowerShell].
>
> 

### <a name="get-started-with-azure-powershell-cmdlets"></a>Приступая к работе с командлетами Azure PowerShell
tooget работы.

1. Откройте Azure PowerShell.
2. В командной строке PowerShell hello запустите эти команды toosign в toohello диспетчера ресурсов Azure и выберите подписку.

    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

<a name="scale-performance-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute-power"></a>Масштабирование вычислительных ресурсов
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

hello toochange Dwu, использовать hello [набор AzureRmSqlDatabase] [ Set-AzureRmSqlDatabase] командлета PowerShell. Hello следующем примере hello службы уровня цели tooDW1000 для базы данных hello MySQLDW, который размещается на сервере MyServer.

```Powershell
Set-AzureRmSqlDatabase -DatabaseName "MySQLDW" -ServerName "MyServer" -RequestedServiceObjectiveName "DW1000"
```

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a>Приостановка работы вычислительных ресурсов
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

toopause базы данных, используйте hello [Suspend AzureRmSqlDatabase] [ Suspend-AzureRmSqlDatabase] командлета. Hello следующем примере показана Приостановка базы данных с именем Database02, размещенный на сервере с именем Server01. Hello сервер находится в группе ресурсов Azure с именем ResourceGroup1.

> [!NOTE]
> Обратите внимание, что если сервер является foo.database.windows.net, используйте «foo» как hello - ServerName в командлеты PowerShell hello.
>
> 

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
```
Вариант, в следующем примере извлекает hello базы данных в hello $database объекта. Затем он передает hello объекта слишком[Suspend AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]. Hello результаты сохраняются в resultDatabase hello объекта. Последняя команда Hello показывает результаты hello.

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a>Возобновление работы вычислительных ресурсов
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

toostart базы данных, используйте hello [Resume AzureRmSqlDatabase] [ Resume-AzureRmSqlDatabase] командлета. Hello следующий пример запускает базы данных с именем Database02, размещенный на сервере с именем Server01. Hello сервер находится в группе ресурсов Azure с именем ResourceGroup1.

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" -DatabaseName "Database02"
```

Вариант, в следующем примере извлекает hello базы данных в hello $database объекта. Затем он передает hello объекта слишком[Resume AzureRmSqlDatabase] [ Resume-AzureRmSqlDatabase] и сохраняет результаты hello в $resultDatabase. Последняя команда Hello показывает результаты hello.

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
$resultDatabase
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state"></a>Проверка состояния базы данных

Как показано в hello выше примерах, можно использовать [Get AzureRmSqlDatabase] [ Get-AzureRmSqlDatabase] командлет tooget сведения из базы данных, тем самым Проверка состояния hello, но toouse в качестве аргумента. 

```powershell
Get-AzureRmSqlDatabase [-ResourceGroupName] <String> [-ServerName] <String> [[-DatabaseName] <String>]
 [-InformationAction <ActionPreference>] [-InformationVariable <String>] [-Confirm] [-WhatIf]
 [<CommonParameters>]
```

Ниже приведен пример результата при таком использовании. 

```powershell   
ResourceGroupName             : nytrg
ServerName                    : nytsvr
DatabaseName                  : nytdb
Location                      : West US
DatabaseId                    : 86461aae-8e3d-4ded-9389-ac9d4bc69bbb
Edition                       : DataWarehouse
CollationName                 : SQL_Latin1General_CP1CI_AS
CatalogCollation              :
MaxSizeBytes                  : 32212254720
Status                        : Online
CreationDate                  : 10/26/2016 4:33:14 PM
CurrentServiceObjectiveId     : 620323bf-2879-4807-b30d-c2e6d7b3b3aa
CurrentServiceObjectiveName   : System2
RequestedServiceObjectiveId   : 620323bf-2879-4807-b30d-c2e6d7b3b3aa
RequestedServiceObjectiveName :
ElasticPoolName               :
EarliestRestoreDate           : 1/1/0001 12:00:00 AM
```

Которой затем можно проверить toosee hello *состояние* hello базы данных. Как видите, в этом случае база данных находится в сети (Online). 

При выполнении этой команды должно отобразиться одно из следующих значений состояния: "Online" (В сети), "Pausing" (Приостановка), "Resuming" (Возобновление), "Scaling" (Масштабирование) и "Paused" (Приостановлена).

<a name="next-steps-bk"></a>

## <a name="next-steps"></a>Дальнейшие действия
Сведения о других задачах управления см. в статье [Управление базами данных в хранилище данных SQL Azure][Management overview].

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->
[Resume-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619347.aspx
[Suspend-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619337.aspx
[Set-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619433.aspx
[Get-AzureRmSqlDatabase]: /powershell/servicemanagement/azure.sqldatabase/v1.6.1/get-azuresqldatabase

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[Azure portal]: http://portal.azure.com/
