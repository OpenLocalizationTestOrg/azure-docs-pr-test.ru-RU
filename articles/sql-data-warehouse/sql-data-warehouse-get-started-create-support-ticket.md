---
title: "aaaHow toocreate обращение в службу поддержки для хранилища данных SQL | Документы Microsoft"
description: "Как toocreate поддержка билета в хранилище данных SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: a91d1f53-03cb-464b-9d5b-4a9c1a194ed3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: 72f7eac82112fb7f1bfb05abca4ce40aeb3c828c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-support-ticket-for-sql-data-warehouse"></a><span data-ttu-id="ca2d9-103">Как билета toocreate технической поддержки для хранилища данных SQL</span><span class="sxs-lookup"><span data-stu-id="ca2d9-103">How toocreate a support ticket for SQL Data Warehouse</span></span>
<span data-ttu-id="ca2d9-104">Если у вас возникли проблемы с хранилищем данных SQL, создайте запрос в службу поддержки, чтобы получить помощь от нашей команды разработчиков.</span><span class="sxs-lookup"><span data-stu-id="ca2d9-104">If you are having any issues with your SQL Data Warehouse, please create a support ticket so that our engineering team can assist you.</span></span>

> [!NOTE] 
> <span data-ttu-id="ca2d9-105">Начиная с 12/20/2016 hello проверки работоспособности ресурса в hello портал Azure не является точным.</span><span class="sxs-lookup"><span data-stu-id="ca2d9-105">As of 12/20/2016, hello resource health check in hello Azure portal is not accurate.</span></span> <span data-ttu-id="ca2d9-106">Мы активно работаем toofix эту проблему.</span><span class="sxs-lookup"><span data-stu-id="ca2d9-106">We are actively working toofix this issue.</span></span> 


## <a name="create-a-support-ticket"></a><span data-ttu-id="ca2d9-107">Создание запроса в службу поддержки</span><span class="sxs-lookup"><span data-stu-id="ca2d9-107">Create a support ticket</span></span>
1. <span data-ttu-id="ca2d9-108">Откройте hello [портал Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="ca2d9-108">Open hello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="ca2d9-109">На экране приветствия домашней щелкните hello **Справка и поддержка** плитки.</span><span class="sxs-lookup"><span data-stu-id="ca2d9-109">On hello Home screen, click hello **Help + support** tile.</span></span>
   
    ![Справка + поддержка](./media/sql-data-warehouse-get-started-create-support-ticket/help-support.png)
3. <span data-ttu-id="ca2d9-111">Hello Справка + поддержка колонка, щелкните **запрос поддержки создания**.</span><span class="sxs-lookup"><span data-stu-id="ca2d9-111">On hello Help + Support blade, click **Create support request**.</span></span>
   
    ![Новый запрос на техническую поддержку](./media/sql-data-warehouse-get-started-create-support-ticket/create-support-request.png)
   
    <a name="request-quota-change"></a> 
4. <span data-ttu-id="ca2d9-113">Выберите hello **запрос типа**.</span><span class="sxs-lookup"><span data-stu-id="ca2d9-113">Select hello **Request Type**.</span></span>
   
    ![Тип запроса](./media/sql-data-warehouse-get-started-create-support-ticket/request-type.png)
   
   > [!NOTE]
   > <span data-ttu-id="ca2d9-115">По умолчанию для каждого экземпляра SQL Server (например, myserver.database.windows.net) предусмотрена следующая **квота на DTU**: 45 000.</span><span class="sxs-lookup"><span data-stu-id="ca2d9-115">By default, each SQL server (e.g. myserver.database.windows.net) has a **DTU Quota** of 45,000.</span></span> <span data-ttu-id="ca2d9-116">Эта квота является просто ограничением для безопасности.</span><span class="sxs-lookup"><span data-stu-id="ca2d9-116">This quota is simply a safety limit.</span></span> <span data-ttu-id="ca2d9-117">Можно увеличить квоту, создав запрос в службу поддержки и выбрав *квоты* как тип запроса hello.</span><span class="sxs-lookup"><span data-stu-id="ca2d9-117">You can increase your quota by creating a support ticket and selecting *Quota* as hello request type.</span></span> <span data-ttu-id="ca2d9-118">toocalculate вашей DTU умножьте hello 7.5 с hello общее [DWU] [ DWU] необходимости.</span><span class="sxs-lookup"><span data-stu-id="ca2d9-118">toocalculate your DTU needs, multiply hello 7.5 by hello total [DWU][DWU] needed.</span></span> <span data-ttu-id="ca2d9-119">Например, вы хотите toohost двух DW6000s на один сервер SQL server, то следует запросить квоту DTU 90,000.</span><span class="sxs-lookup"><span data-stu-id="ca2d9-119">For example, you would like toohost two DW6000s on one SQL server, then you should request a DTU quota of 90,000.</span></span>  <span data-ttu-id="ca2d9-120">Можно просмотреть вашего текущего потребления DTU в колонке сервера SQL hello hello портала.</span><span class="sxs-lookup"><span data-stu-id="ca2d9-120">You can view your current DTU consumption from hello SQL server blade in hello portal.</span></span> <span data-ttu-id="ca2d9-121">Приостановлен, Отмена приостановленных баз данных учитываются hello Квота DTU.</span><span class="sxs-lookup"><span data-stu-id="ca2d9-121">Both paused and un-paused databases count toward hello DTU quota.</span></span> 
   > 
   > 
5. <span data-ttu-id="ca2d9-122">Выберите hello **подписки** Здравствуйте, узлы, базы данных с ошибкой hello, вы сообщаете.</span><span class="sxs-lookup"><span data-stu-id="ca2d9-122">Select hello **Subscription** that hosts hello database with hello problem you are reporting.</span></span>
   
    ![Подписки](./media/sql-data-warehouse-get-started-create-support-ticket/subscription.png)
6. <span data-ttu-id="ca2d9-124">Выберите **хранилище данных SQL** как hello ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ca2d9-124">Select **SQL Data Warehouse** as hello Resource.</span></span>
   
    ![Ресурс](./media/sql-data-warehouse-get-started-create-support-ticket/resource.png)
7. <span data-ttu-id="ca2d9-126">Выберите свой [план поддержки Azure][Azure support plan].</span><span class="sxs-lookup"><span data-stu-id="ca2d9-126">Select your [Azure support plan][Azure support plan].</span></span>
   
   * <span data-ttu-id="ca2d9-127">**вопросам, связанным с выставлением счетов, квотами и управлением подпиской** , доступна на всех уровнях.</span><span class="sxs-lookup"><span data-stu-id="ca2d9-127">**Billing, quota and subscription management** support is available at all support levels.</span></span>
   * <span data-ttu-id="ca2d9-128">Поддержка по **замене или ремонту** обеспечивается на уровнях [Developer][Developer], [Standard][Standard], [Professional Direct][Professional Direct] и [Premier][Premier].</span><span class="sxs-lookup"><span data-stu-id="ca2d9-128">**Break-fix** support is provided through [Developer][Developer], [Standard][Standard], [Professional Direct][Professional Direct] or [Premier][Premier] support.</span></span> <span data-ttu-id="ca2d9-129">Устранения неполадок возникли неполадки, из-за клиентов при использовании Azure там, где имеется проблема оправданное предположение, вызвавшего Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="ca2d9-129">Break-fix issues are problems experienced by customers while using Azure where there is a reasonable expectation that Microsoft caused hello problem.</span></span>
   * <span data-ttu-id="ca2d9-130">**Разработчик обучения** и **советы по службами** можно найти по адресу hello [Professional Direct] [ Professional Direct] и [Premier] [ Premier] уровней поддержки.</span><span class="sxs-lookup"><span data-stu-id="ca2d9-130">**Developer mentoring** and **advisory services** are available at hello [Professional Direct][Professional Direct] and [Premier][Premier] support levels.</span></span> 
     
     <span data-ttu-id="ca2d9-131">Если у вас есть Premier support плана, отчет можно также хранилище данных SQL проблем на hello [портал Microsoft Premier online][Microsoft Premier online portal].</span><span class="sxs-lookup"><span data-stu-id="ca2d9-131">If you have a Premier support plan, you can also report SQL Data Warehouse related issues on hello [Microsoft Premier online portal][Microsoft Premier online portal].</span></span>  <span data-ttu-id="ca2d9-132">В разделе [планами поддержки Azure] [ Azure support plan] toolearn Дополнительные сведения о различных поддержки схем, включая области, время цен, ответа hello и т. д.  Часто задаваемые вопросы о поддержке Azure см. на [этой странице][Azure support FAQs].</span><span class="sxs-lookup"><span data-stu-id="ca2d9-132">See [Azure support plans][Azure support plan] toolearn more about hello various support plans, including scope, response times, pricing, etc.  For frequently asked questions about Azure support, see [Azure support FAQs][Azure support FAQs].</span></span>  
     
     ![План поддержки](./media/sql-data-warehouse-get-started-create-support-ticket/support-plan.png)
8. <span data-ttu-id="ca2d9-134">Выберите hello **тип проблемы** и **категории**.</span><span class="sxs-lookup"><span data-stu-id="ca2d9-134">Select hello **Problem Type** and **Category**.</span></span> <span data-ttu-id="ca2d9-135">В этом примере мы выбрали hello тип проблемы «средства» и «Клиентские средства» как категория hello.</span><span class="sxs-lookup"><span data-stu-id="ca2d9-135">In this example, we have chosen "Tools" as hello Problem type and "Client tools" as hello category.</span></span> 
   
    ![Категория типов проблем](./media/sql-data-warehouse-get-started-create-support-ticket/problem-type-category.png)
9. <span data-ttu-id="ca2d9-137">Опишите проблему hello и выбрать уровень hello влияние на бизнес.</span><span class="sxs-lookup"><span data-stu-id="ca2d9-137">Describe hello problem and choose hello level of business impact.</span></span>
   
    ![Описание проблемы](./media/sql-data-warehouse-get-started-create-support-ticket/problem-description.png)
10. <span data-ttu-id="ca2d9-139">Ваши **контактные данные** для этого запроса в службу поддержки будут заполнены предварительно.</span><span class="sxs-lookup"><span data-stu-id="ca2d9-139">Your **contact information** for this support ticket will be pre-filled.</span></span> <span data-ttu-id="ca2d9-140">При необходимости обновите их.</span><span class="sxs-lookup"><span data-stu-id="ca2d9-140">Update this if necessary.</span></span>
    
    ![Контактные данные](./media/sql-data-warehouse-get-started-create-support-ticket/contact-info.png)
11. <span data-ttu-id="ca2d9-142">Нажмите кнопку **создать** запроса на поддержку toosubmit hello.</span><span class="sxs-lookup"><span data-stu-id="ca2d9-142">Click **Create** toosubmit hello support request.</span></span>

## <a name="monitor-a-support-ticket"></a><span data-ttu-id="ca2d9-143">Мониторинг запроса в службу поддержки</span><span class="sxs-lookup"><span data-stu-id="ca2d9-143">Monitor a support ticket</span></span>
<span data-ttu-id="ca2d9-144">После отправки запроса на поддержку hello hello Azure поддержки свяжется с вами.</span><span class="sxs-lookup"><span data-stu-id="ca2d9-144">After you have submitted hello support request, hello Azure support team will contact you.</span></span> <span data-ttu-id="ca2d9-145">toocheck состояние запроса и сведения, нажмите кнопку **запросов поддержки управление** на панели мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="ca2d9-145">toocheck your request status and details, click **Manage support requests** on hello dashboard.</span></span>

![Проверка состояния](./media/sql-data-warehouse-get-started-create-support-ticket/check-status.png)

## <a name="other-resources"></a><span data-ttu-id="ca2d9-147">Другие ресурсы</span><span class="sxs-lookup"><span data-stu-id="ca2d9-147">Other Resources</span></span>
<span data-ttu-id="ca2d9-148">Кроме того, можно подключиться, используя hello сообщества хранилище данных SQL на [переполнения стека] [ Stack Overflow] или на hello [форум MSDN хранилища данных SQL Azure] [ Azure SQL Data Warehouse MSDN forum].</span><span class="sxs-lookup"><span data-stu-id="ca2d9-148">Additionally, you can connect with hello SQL Data Warehouse community on [Stack Overflow][Stack Overflow] or on hello [Azure SQL Data Warehouse MSDN forum][Azure SQL Data Warehouse MSDN forum].</span></span>

<!--Image references--> 

<!--Article references--> 
[DWU]: ./sql-data-warehouse-overview-what-is.md

<!--MSDN references--> 

<!--Other web references--> 
[Azure portal]: https://portal.azure.com/
[Azure support plan]: https://azure.microsoft.com/support/plans/?WT.mc_id=Support_Plan_510979/  
[Developer]: https://azure.microsoft.com/support/plans/developer/  
[Standard]: https://azure.microsoft.com/support/plans/standard/  
[Professional Direct]: https://azure.microsoft.com/support/plans/prodirect/  
[Premier]: https://azure.microsoft.com/support/plans/premier/  
[Azure support FAQs]: https://azure.microsoft.com/support/faq/
[Microsoft Premier online portal]: https://premier.microsoft.com/
[Stack Overflow]: https://stackoverflow.com/questions/tagged/azure-sqldw/
[Azure SQL Data Warehouse MSDN forum]: https://social.msdn.microsoft.com/Forums/home?forum=AzureSQLDataWarehouse/

