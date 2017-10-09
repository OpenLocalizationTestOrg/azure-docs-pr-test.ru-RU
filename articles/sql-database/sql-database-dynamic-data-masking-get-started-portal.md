---
title: "Портал Azure: динамическое маскирование данных базы данных SQL | Документация Майкрософт"
description: "Как tooget работу с динамического маскирования в портале Azure hello данных базы данных SQL"
services: sql-database
documentationcenter: 
author: ronitr
manager: jhubbard
editor: 
ms.assetid: "2"
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 11/22/2016
ms.author: ronitr; ronmat
ms.openlocfilehash: 5c5f74682a15d42eceb78c3ca0705401e1ac0ae7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-database-dynamic-data-masking-with-hello-azure-portal"></a><span data-ttu-id="ccd72-103">Приступая к работе с базой данных SQL с портала Azure hello маскировки данных</span><span class="sxs-lookup"><span data-stu-id="ccd72-103">Get started with SQL Database dynamic data masking with hello Azure Portal</span></span>

<span data-ttu-id="ccd72-104">В этом разделе показано, как tooimplement [маскирование динамических данных](sql-database-dynamic-data-masking-get-started.md) с hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ccd72-104">This topic shows you how tooimplement [dynamic data masking](sql-database-dynamic-data-masking-get-started.md) with hello Azure portal.</span></span> <span data-ttu-id="ccd72-105">Также можно реализовать с помощью маскирования динамических данных [командлеты базы данных SQL Azure](https://msdn.microsoft.com/library/azure/mt574084.aspx) или hello [API-интерфейса REST](https://msdn.microsoft.com/library/dn505719.aspx).</span><span class="sxs-lookup"><span data-stu-id="ccd72-105">You can also implement dynamic data masking using [Azure SQL Database cmdlets](https://msdn.microsoft.com/library/azure/mt574084.aspx) or hello [REST API](https://msdn.microsoft.com/library/dn505719.aspx).</span></span>


## <a name="set-up-dynamic-data-masking-for-your-database-using-hello-azure-portal"></a><span data-ttu-id="ccd72-106">Настройка динамического маскирования данных для базы данных с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="ccd72-106">Set up dynamic data masking for your database using hello Azure Portal</span></span>
1. <span data-ttu-id="ccd72-107">Здравствуйте, запустить портал Azure на [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ccd72-107">Launch hello Azure Portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ccd72-108">Перейдите в колонку параметров toohello hello базы данных, которая включает в себя hello конфиденциальных данных, toomask.</span><span class="sxs-lookup"><span data-stu-id="ccd72-108">Navigate toohello settings blade of hello database that includes hello sensitive data you want toomask.</span></span>
3. <span data-ttu-id="ccd72-109">Нажмите кнопку hello **динамической маскировки данных** плитку, которая запускает hello **динамической маскировки данных** колонке конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ccd72-109">Click hello **Dynamic Data Masking** tile which launches hello **Dynamic Data Masking** configuration blade.</span></span>
   
   * <span data-ttu-id="ccd72-110">Кроме того, может воспользоваться прокруткой вниз toohello **операции** и нажмите кнопку **динамической маскировки данных**.</span><span class="sxs-lookup"><span data-stu-id="ccd72-110">Alternatively, you can scroll down toohello **Operations** section and click **Dynamic Data Masking**.</span></span>
     
     ![Область навигации](./media/sql-database-dynamic-data-masking-get-started/4_ddm_settings_tile.png)<br/><br/>
4. <span data-ttu-id="ccd72-112">В hello **динамической маскировки данных** колонке конфигурации, вы можете увидеть некоторые столбцы базы данных, подсистемы рекомендаций hello отметила для маски.</span><span class="sxs-lookup"><span data-stu-id="ccd72-112">In hello **Dynamic Data Masking** configuration blade you may see some database columns that hello recommendations engine has flagged for masking.</span></span> <span data-ttu-id="ccd72-113">Чтобы tooaccept рекомендации hello, просто нажав кнопку **Добавить маску** для одного или нескольких столбцов и маски будет создана на основе типа hello по умолчанию для этого столбца.</span><span class="sxs-lookup"><span data-stu-id="ccd72-113">In order tooaccept hello recommendations, just click **Add Mask** for one or more columns and a mask will be created based on hello default type for this column.</span></span> <span data-ttu-id="ccd72-114">Вы можете изменить hello функции маскировки, щелкнув правило маскирования hello и редактирования hello маскирования другой формат поля формата tooa по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="ccd72-114">You can change hello masking function by clicking on hello masking rule and editing hello masking field format tooa different format of your choice.</span></span> <span data-ttu-id="ccd72-115">Быть убедиться, что tooclick **Сохранить** toosave параметры.</span><span class="sxs-lookup"><span data-stu-id="ccd72-115">Be sure tooclick **Save** toosave your settings.</span></span>
   
    ![Область навигации](./media/sql-database-dynamic-data-masking-get-started/5_ddm_recommendations.png)<br/><br/>
5. <span data-ttu-id="ccd72-117">Маска для любого столбца в базе данных, вверху hello hello tooadd **динамической маскировки данных** настройку колонке нажмите кнопку **Добавить маску** tooopen hello **добавить правило маскировки** колонке конфигурации</span><span class="sxs-lookup"><span data-stu-id="ccd72-117">tooadd a mask for any column in your database, at hello top of hello **Dynamic Data Masking** configuration blade click **Add Mask** tooopen hello **Add Masking Rule** configuration blade</span></span>
   
    ![Область навигации](./media/sql-database-dynamic-data-masking-get-started/6_ddm_add_mask.png)<br/><br/>
6. <span data-ttu-id="ccd72-119">Выберите hello **схемы**, **таблицы** и **столбца** toodefine hello, назначенный полю, будут замаскированы.</span><span class="sxs-lookup"><span data-stu-id="ccd72-119">Select hello **Schema**, **Table** and **Column** toodefine hello designated field that will be masked.</span></span>
7. <span data-ttu-id="ccd72-120">Выберите **формат поля маскировки** из списка hello маскирования категории конфиденциальных данных.</span><span class="sxs-lookup"><span data-stu-id="ccd72-120">Choose a **Masking Field Format** from hello list of sensitive data masking categories.</span></span>
   
    ![Область навигации](./media/sql-database-dynamic-data-masking-get-started/7_ddm_mask_field_format.png)<br/><br/>        
8. <span data-ttu-id="ccd72-122">Нажмите кнопку **Сохранить** в маскировки правило колонке tooupdate hello набор правил в hello политики динамического маскирования данных маскировки данных hello.</span><span class="sxs-lookup"><span data-stu-id="ccd72-122">Click **Save** in hello data masking rule blade tooupdate hello set of masking rules in hello dynamic data masking policy.</span></span>
9. <span data-ttu-id="ccd72-123">Тип hello SQL пользователям или удостоверений AAD, которые должны быть исключены из маски и иметь доступ к конфиденциальным данным немаскированные toohello.</span><span class="sxs-lookup"><span data-stu-id="ccd72-123">Type hello SQL users or AAD identities that should be excluded from masking, and have access toohello unmasked sensitive data.</span></span> <span data-ttu-id="ccd72-124">Это должен быть список пользователей, разделенных точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="ccd72-124">This should be a semicolon-separated list of users.</span></span> <span data-ttu-id="ccd72-125">Обратите внимание, что пользователи с правами администратора всегда доступа toohello исходного немаскированные данные.</span><span class="sxs-lookup"><span data-stu-id="ccd72-125">Note that users with administrator privileges always have access toohello original unmasked data.</span></span>
   
    ![Область навигации](./media/sql-database-dynamic-data-masking-get-started/8_ddm_excluded_users.png)
   
   > [!TIP]
   > <span data-ttu-id="ccd72-127">toomake, поэтому Здравствуйте, прикладной уровень может отобразить конфиденциальных данных для пользователей приложений, для работы в привилегированном режиме, hello SQL-пользователь или приложение hello удостоверений AAD используется база данных tooquery hello.</span><span class="sxs-lookup"><span data-stu-id="ccd72-127">toomake it so hello application layer can display sensitive data for application privileged users, add hello SQL user or AAD identity hello application uses tooquery hello database.</span></span> <span data-ttu-id="ccd72-128">Настоятельно рекомендуется, что этот список содержит минимальное количество привилегированных пользователей toominimize раскрытия конфиденциальных данных hello.</span><span class="sxs-lookup"><span data-stu-id="ccd72-128">It is highly recommended that this list contain a minimal number of privileged users toominimize exposure of hello sensitive data.</span></span>
   > 
   > 
10. <span data-ttu-id="ccd72-129">Нажмите кнопку **Сохранить** в hello политики маскирования данных конфигурации колонке toosave hello новых или обновленных маски.</span><span class="sxs-lookup"><span data-stu-id="ccd72-129">Click **Save** in hello data masking configuration blade toosave hello new or updated masking policy.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ccd72-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ccd72-130">Next steps</span></span>

* <span data-ttu-id="ccd72-131">Обзор динамического маскирования данных см. в разделе [Динамическое маскирование данных](sql-database-dynamic-data-masking-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ccd72-131">For an overview of dynamic data masking, see [dynamic data masking](sql-database-dynamic-data-masking-get-started.md).</span></span>
* <span data-ttu-id="ccd72-132">Также можно реализовать с помощью маскирования динамических данных [командлеты базы данных SQL Azure](https://msdn.microsoft.com/library/azure/mt574084.aspx) или hello [API-интерфейса REST](https://msdn.microsoft.com/library/dn505719.aspx).</span><span class="sxs-lookup"><span data-stu-id="ccd72-132">You can also implement dynamic data masking using [Azure SQL Database cmdlets](https://msdn.microsoft.com/library/azure/mt574084.aspx) or hello [REST API](https://msdn.microsoft.com/library/dn505719.aspx).</span></span>
