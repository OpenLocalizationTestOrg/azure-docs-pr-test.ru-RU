---
title: "Хранилище данных SQL Azure (REST API) aaaRestore | Документы Microsoft"
description: "Задачи REST API для восстановления хранилища данных SQL."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: fca922c6-b675-49c7-907e-5dcf26d451dd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: cf6678d71aafff71b1ea715f447e41e25f20d1b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-data-warehouse-rest-api"></a>Восстановление хранилища данных SQL Azure (REST API)
> [!div class="op_single_selector"]
> * [Обзор][Overview]
> * [Портал][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
> 
> 

В этой статье вы узнаете, как хранилище данных SQL Azure с помощью toorestore hello REST API.

## <a name="before-you-begin"></a>Перед началом работы
**Проверьте ресурсы DTU.** Каждое хранилище данных SQL размещается на сервере SQL Server (например, myserver.database.windows.net), которому выделена квота DTU по умолчанию.  Перед началом восстановления хранилища данных SQL, убедитесь, что hello, SQL server имеет достаточно оставшиеся квоту DTU для hello восстанавливаемой базы данных. toolearn как необходимые toocalculate DTU или toorequest дополнительные DTU см [запроса на изменение квоты DTU][Request a DTU quota change].

## <a name="restore-an-active-or-paused-database"></a>Восстановление активной или приостановленной базы данных
toorestore базы данных:

1. Получите список hello точки восстановления базы данных с помощью операции Get точки восстановления базы данных hello.
2. Перед началом восстановления с помощью hello [Создание запроса на восстановление базы данных] [ Create database restore request] операции.
3. Отслеживать состояние hello восстановления с помощью hello [состояние операции базы данных] [ Database operation status] операции.

> [!NOTE]
> После завершения восстановления hello восстановленной базы данных можно настроить, выполнив [настроить базу данных после восстановления][Configure your database after recovery].
> 
> 

## <a name="restore-a-deleted-database"></a>Восстановление удаленной базы данных.
toorestore удаленной базы данных:

1. Список всех доступных для восстановления удаленных баз данных с помощью hello [удаленные базы данных, могут быть восстановлены список] [ List restorable dropped databases] операции.
2. Получить сведения о hello hello удалить базы данных, которая toorestore с помощью hello [базы данных удалены Get, которые могут быть восстановлены] [ Get restorable dropped database] операции.
3. Перед началом восстановления с помощью hello [Создание запроса на восстановление базы данных] [ Create database restore request] операции.
4. Отслеживать состояние hello восстановления с помощью hello [состояние операции базы данных] [ Database operation status] операции.

> [!NOTE]
> см. базы данных после завершения восстановления hello tooconfigure [настроить базу данных после восстановления][Configure your database after recovery].
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
toolearn о функциях обеспечения непрерывности бизнеса hello выпусков базы данных SQL Azure, прочитайте hello [непрерывности бизнес-базы данных SQL Azure обзора][Azure SQL Database business continuity overview].

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md

<!--MSDN references-->
[Create database restore request]: https://msdn.microsoft.com/library/azure/dn509571.aspx
[Database operation status]: https://msdn.microsoft.com/library/azure/dn720371.aspx
[Get restorable dropped database]: https://msdn.microsoft.com/library/azure/dn509574.aspx
[List restorable dropped databases]: https://msdn.microsoft.com/library/azure/dn509562.aspx
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx

<!--Other Web references-->
[Azure Portal]: https://portal.azure.com/
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
