---
title: "aaaRestore хранилище данных SQL Azure (портал Azure) | Документы Microsoft"
description: "Задачи портала Azure для восстановления хранилища данных SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: barbkess
editor: 
ms.assetid: b0aef539-7657-4b0e-9899-74098f5c21bc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 09/21/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: cb225d2a21b61acab70a51b69c266f8d3ffacc9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="restore-azure-sql-data-warehouse-portal"></a>Восстановление хранилища данных SQL Azure (портал)
> [!div class="op_single_selector"]
> * [Обзор][Overview]
> * [Портал][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
>
>
В этой статье вы узнаете, как toorestore хранилище данных SQL Azure с помощью hello портал Azure.

## <a name="before-you-begin"></a>Перед началом работы
**Проверьте ресурсы DTU.** Каждый экземпляр хранилища данных SQL размещается на сервере SQL Server (например, myserver.database.windows.net), которому выделена квота единиц пропускной способности данных (DTU) по умолчанию. Перед началом восстановления хранилища данных SQL, убедитесь, что SQL server имеет достаточно оставшиеся квоту DTU для базы данных hello, производится восстановление. toolearn квоты DTU toocalculate или toorequest дополнительные Dtu. в статье [запроса на изменение квоты DTU][Request a DTU quota change].

## <a name="restore-an-active-or-paused-database"></a>Восстановление активной или приостановленной базы данных
toorestore базы данных:

1. Войдите в toohello [портал Azure][Azure portal].
2. Hello левой панели выберите **Обзор**, а затем выберите **серверов SQL Server**.

    ![Выбор "Обзор" > "Серверы SQL Server"](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. Найдите свой сервер и выберите его.

    ![Выбор своего сервера](./media/sql-data-warehouse-restore-database-portal/01-select-server.png)
4. Найти hello экземпляр хранилища данных SQL требуется toorestore из и выберите его.

    ![Выберите экземпляр hello toorestore хранилище данных SQL](./media/sql-data-warehouse-restore-database-portal/01-select-active-dw.png)
5. Hello верхней части колонки hello хранилища данных, выберите **восстановить**.

    ![Выбор "Восстановить"](./media/sql-data-warehouse-restore-database-portal/01-select-restore-from-active.png)
6. Укажите новое значение в поле **Имя базы данных**.
7. Выберите hello последней **точку восстановления**.

   Убедитесь в том, что выбрано hello последнюю точку восстановления. Поскольку точки восстановления, отображаются в формате UTC, параметр по умолчанию hello может быть hello последнюю точку восстановления.

      ![Выбор точки восстановления](./media/sql-data-warehouse-restore-database-portal/01-restore-blade-from-active.png)
8. Нажмите кнопку **ОК**.
9. начнется процесс восстановления базы данных Hello, а также можно использовать **уведомления** toomonitor hello процесса.

> [!NOTE]
> После завершения восстановления hello восстановленной базы данных можно настроить, выполнив [настроить базу данных после восстановления][Configure your database after recovery].
>
>

## <a name="restore-a-deleted-database"></a>Восстановление удаленной базы данных.
toorestore удаленной базы данных:

1. Войдите в toohello [портал Azure][Azure portal].
2. Hello левой панели выберите **Обзор**, а затем выберите **серверов SQL Server**.

    ![Выбор "Обзор" > "Серверы SQL Server"](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. Найдите свой сервер и выберите его.

    ![Выбор своего сервера](./media/sql-data-warehouse-restore-database-portal/02-select-server.png)
4. Прокрутите вниз toohello **операции** раздел в колонке сервера.
5. Выберите hello **удаленных баз данных** плитки.

    ![Выберите плитку баз данных удалено hello](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dws.png)
6. Выберите hello удалить базу данных, что необходимо toorestore.

    ![Выберите toorestore базы данных](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dw.png)
7. Укажите новое значение в поле **Имя базы данных**.

    ![Добавьте имя для базы данных hello](./media/sql-data-warehouse-restore-database-portal/02-restore-blade-from-deleted.png)
8. Нажмите кнопку **ОК**.
9. начнется процесс восстановления базы данных Hello, а также можно использовать **уведомления** toomonitor hello процесса.

> [!NOTE]
> см. базы данных после завершения восстановления hello tooconfigure [настроить базу данных после восстановления][Configure your database after recovery].
>
>

## <a name="next-steps"></a>Дальнейшие действия
toolearn о функциях обеспечения непрерывности бизнеса hello выпусков базы данных SQL Azure, чтение hello [непрерывности бизнес-базы данных SQL Azure обзора][Azure SQL Database business continuity overview].

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change

<!--MSDN references-->

<!--Blog references-->

<!--Other Web references-->
[Azure portal]: https://portal.azure.com/
