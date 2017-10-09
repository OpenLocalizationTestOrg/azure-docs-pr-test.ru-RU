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
# <a name="manage-compute-power-in-azure-sql-data-warehouse-azure-portal"></a><span data-ttu-id="7cf12-105">Управление вычислительными ресурсами в хранилище данных SQL Azure (портал Azure)</span><span class="sxs-lookup"><span data-stu-id="7cf12-105">Manage compute power in Azure SQL Data Warehouse (Azure portal)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7cf12-106">Обзор</span><span class="sxs-lookup"><span data-stu-id="7cf12-106">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="7cf12-107">Портал</span><span class="sxs-lookup"><span data-stu-id="7cf12-107">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="7cf12-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7cf12-108">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="7cf12-109">REST</span><span class="sxs-lookup"><span data-stu-id="7cf12-109">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="7cf12-110">TSQL</span><span class="sxs-lookup"><span data-stu-id="7cf12-110">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>


## <a name="scale-compute-power"></a><span data-ttu-id="7cf12-111">Масштабирование вычислительных ресурсов</span><span class="sxs-lookup"><span data-stu-id="7cf12-111">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="7cf12-112">toochange вычислительные ресурсы:</span><span class="sxs-lookup"><span data-stu-id="7cf12-112">toochange compute resources:</span></span>

1. <span data-ttu-id="7cf12-113">Откройте hello [портал Azure][Azure portal], откройте базу данных и нажмите кнопку **шкалы**.</span><span class="sxs-lookup"><span data-stu-id="7cf12-113">Open hello [Azure portal][Azure portal], open your database, and click **Scale**.</span></span>

    ![Щелкните пункт Масштаб][1]
2. <span data-ttu-id="7cf12-115">В колонке шкалы hello hello ползунок влево или вправо параметра DWU toochange hello.</span><span class="sxs-lookup"><span data-stu-id="7cf12-115">In hello Scale blade, move hello slider left or right toochange hello DWU setting.</span></span>

    ![Переместите ползунок][2]
3. <span data-ttu-id="7cf12-117">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="7cf12-117">Click **Save**.</span></span> <span data-ttu-id="7cf12-118">Появится сообщение с подтверждением.</span><span class="sxs-lookup"><span data-stu-id="7cf12-118">A confirmation message appears.</span></span> <span data-ttu-id="7cf12-119">Нажмите кнопку **Да** tooconfirm или **не** toocancel.</span><span class="sxs-lookup"><span data-stu-id="7cf12-119">Click **yes** tooconfirm or **no** toocancel.</span></span>

    ![Щелкните Сохранить][3]

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="7cf12-121">Приостановка работы вычислительных ресурсов</span><span class="sxs-lookup"><span data-stu-id="7cf12-121">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="7cf12-122">toopause базы данных:</span><span class="sxs-lookup"><span data-stu-id="7cf12-122">toopause a database:</span></span>

1. <span data-ttu-id="7cf12-123">Откройте hello [портал Azure] [ Azure portal] и открыть базу данных.</span><span class="sxs-lookup"><span data-stu-id="7cf12-123">Open hello [Azure portal][Azure portal] and open your database.</span></span> <span data-ttu-id="7cf12-124">Обратите внимание, что hello, находится в состоянии **Online**.</span><span class="sxs-lookup"><span data-stu-id="7cf12-124">Notice that hello Status is **Online**.</span></span>

    ![Состояние "В сети"][6]
2. <span data-ttu-id="7cf12-126">ресурсы toosuspend вычислительных ресурсов и памяти, нажмите кнопку **Пауза**, а затем появится сообщение с подтверждением.</span><span class="sxs-lookup"><span data-stu-id="7cf12-126">toosuspend compute and memory resources, click **Pause**, and then a confirmation message appears.</span></span> <span data-ttu-id="7cf12-127">Нажмите кнопку **Да** tooconfirm или **не** toocancel.</span><span class="sxs-lookup"><span data-stu-id="7cf12-127">Click **yes** tooconfirm or **no** toocancel.</span></span>

    ![Подтверждение приостановки][7]
3. <span data-ttu-id="7cf12-129">Во время запуска hello базы данных хранилища данных SQL, находится в состоянии hello **Приостановка**.</span><span class="sxs-lookup"><span data-stu-id="7cf12-129">While SQL Data Warehouse is starting hello database, hello status is **Pausing**.</span></span>
4. <span data-ttu-id="7cf12-130">Если имеет состояние hello **приостановлено**, выполнить операцию приостановки hello и вы больше не взимается плата за Dwu.</span><span class="sxs-lookup"><span data-stu-id="7cf12-130">When hello status is **Paused**, hello pause operation is done and you are no longer being charged for DWUs.</span></span>

    ![Состояние "Приостановка"][4]

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="7cf12-132">Возобновление работы вычислительных ресурсов</span><span class="sxs-lookup"><span data-stu-id="7cf12-132">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="7cf12-133">tooresume базы данных:</span><span class="sxs-lookup"><span data-stu-id="7cf12-133">tooresume a database:</span></span>

1. <span data-ttu-id="7cf12-134">Откройте hello [портал Azure] [ Azure portal] и открыть базу данных.</span><span class="sxs-lookup"><span data-stu-id="7cf12-134">Open hello [Azure portal][Azure portal] and open your database.</span></span> <span data-ttu-id="7cf12-135">Обратите внимание, что hello, находится в состоянии **приостановлено**.</span><span class="sxs-lookup"><span data-stu-id="7cf12-135">Notice that hello Status is **Paused**.</span></span>

    ![Приостановка базы данных][4]
2. <span data-ttu-id="7cf12-137">tooresume hello базы данных щелкните **запустить**, а затем появится сообщение с подтверждением.</span><span class="sxs-lookup"><span data-stu-id="7cf12-137">tooresume hello database click **Start**, and then a confirmation message appears.</span></span> <span data-ttu-id="7cf12-138">Нажмите кнопку **Да** tooconfirm или **не** toocancel.</span><span class="sxs-lookup"><span data-stu-id="7cf12-138">Click **yes** tooconfirm or **no** toocancel.</span></span>

    ![Подтверждение возобновления][5]
3. <span data-ttu-id="7cf12-140">Во время запуска hello базы данных хранилища данных SQL, hello состояние — «Возобновление».</span><span class="sxs-lookup"><span data-stu-id="7cf12-140">While SQL Data Warehouse is starting hello database, hello status is "Resuming".</span></span>
4. <span data-ttu-id="7cf12-141">Если имеет состояние hello **online**, hello база данных готова.</span><span class="sxs-lookup"><span data-stu-id="7cf12-141">When hello status is **online**, hello database is ready.</span></span>

    ![Состояние "В сети"][6]

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="7cf12-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7cf12-143">Next steps</span></span>
<span data-ttu-id="7cf12-144">Дополнительные сведения см. в [обзоре средств управления][Management overview].</span><span class="sxs-lookup"><span data-stu-id="7cf12-144">For more information, see [Management overview][Management overview].</span></span>

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
