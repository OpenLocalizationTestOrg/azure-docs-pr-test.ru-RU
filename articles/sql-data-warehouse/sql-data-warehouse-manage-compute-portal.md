---
title: "aaaManage вычислительная мощность в хранилище данных SQL Azure (портал Azure) | Документы Microsoft"
description: "Задачи на портале Azure toomanage вычислительной мощности. Масштабирование вычислительных ресурсов путем изменения числа единиц DWU. Или, приостанавливать и возобновлять toosave затраты вычислительных ресурсов."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 233b0da5-4abd-4d1d-9586-4ccc5f50b071
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: b2e84b3763e97ce88c190eecfb64b2d06f727229
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-azure-portal"></a>Управление вычислительными ресурсами в хранилище данных SQL Azure (портал Azure)
> [!div class="op_single_selector"]
> * [Обзор](sql-data-warehouse-manage-compute-overview.md)
> * [Портал](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>


## <a name="scale-compute-power"></a>Масштабирование вычислительных ресурсов
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

toochange вычислительные ресурсы:

1. Откройте hello [портал Azure][Azure portal], откройте базу данных и нажмите кнопку **шкалы**.

    ![Щелкните пункт Масштаб][1]
2. В колонке шкалы hello hello ползунок влево или вправо параметра DWU toochange hello.

    ![Переместите ползунок][2]
3. Щелкните **Сохранить**. Появится сообщение с подтверждением. Нажмите кнопку **Да** tooconfirm или **не** toocancel.

    ![Щелкните Сохранить][3]

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a>Приостановка работы вычислительных ресурсов
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

toopause базы данных:

1. Откройте hello [портал Azure] [ Azure portal] и открыть базу данных. Обратите внимание, что hello, находится в состоянии **Online**.

    ![Состояние "В сети"][6]
2. ресурсы toosuspend вычислительных ресурсов и памяти, нажмите кнопку **Пауза**, а затем появится сообщение с подтверждением. Нажмите кнопку **Да** tooconfirm или **не** toocancel.

    ![Подтверждение приостановки][7]
3. Во время запуска hello базы данных хранилища данных SQL, находится в состоянии hello **Приостановка**.
4. Если имеет состояние hello **приостановлено**, выполнить операцию приостановки hello и вы больше не взимается плата за Dwu.

    ![Состояние "Приостановка"][4]

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a>Возобновление работы вычислительных ресурсов
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

tooresume базы данных:

1. Откройте hello [портал Azure] [ Azure portal] и открыть базу данных. Обратите внимание, что hello, находится в состоянии **приостановлено**.

    ![Приостановка базы данных][4]
2. tooresume hello базы данных щелкните **запустить**, а затем появится сообщение с подтверждением. Нажмите кнопку **Да** tooconfirm или **не** toocancel.

    ![Подтверждение возобновления][5]
3. Во время запуска hello базы данных хранилища данных SQL, hello состояние — «Возобновление».
4. Если имеет состояние hello **online**, hello база данных готова.

    ![Состояние "В сети"][6]

<a name="next-steps-bk"></a>

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения см. в [обзоре средств управления][Management overview].

<!--Image references-->
[1]: ./media/sql-data-warehouse-manage-compute-portal/click-scale.png
[2]: ./media/sql-data-warehouse-manage-compute-portal/move-slider.png
[3]: ./media/sql-data-warehouse-manage-compute-portal/click-save.png
[4]: ./media/sql-data-warehouse-manage-compute-portal/resume-database.png
[5]: ./media/sql-data-warehouse-manage-compute-portal/resume-confirm.png
[6]: ./media/sql-data-warehouse-manage-compute-portal/pause-database.png
[7]: ./media/sql-data-warehouse-manage-compute-portal/pause-confirm.png

<!--Article references-->
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
