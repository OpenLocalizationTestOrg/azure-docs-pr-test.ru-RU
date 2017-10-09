---
title: "aaaMake SQL базы данных пользователей стек Azure доступны tooyour | Документы Microsoft"
description: "Учебника tooinstall hello поставщик ресурсов SQL Server и создание предложения, позволяющих пользователям Azure стека создавать базы данных SQL."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/03/2017
ms.author: erikje
ms.custom: mvc
ms.openlocfilehash: 778513ba982981895afe2d57b3b5dda71ead8886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="make-sql-databases-available-tooyour-azure-stack-users"></a><span data-ttu-id="b3ca7-103">Сделать доступных tooyour стека Azure пользователи баз данных SQL</span><span class="sxs-lookup"><span data-stu-id="b3ca7-103">Make SQL databases available tooyour Azure Stack users</span></span>

<span data-ttu-id="b3ca7-104">Как администратор облака Azure стека, можно создать предложения, предоставив пользователям возможность создания баз данных SQL, которые используются с их собственный облачных приложений, веб-сайты и рабочие нагрузки (клиентами).</span><span class="sxs-lookup"><span data-stu-id="b3ca7-104">As an Azure Stack cloud administrator, you can create offers that let your users (tenants) create SQL databases that they can use with their cloud-native apps, websites, and workloads.</span></span> <span data-ttu-id="b3ca7-105">Предоставляя эти пользовательские, по запросу, tooyour пользователей баз данных на основе облака, их можно сохранить время и ресурсы.</span><span class="sxs-lookup"><span data-stu-id="b3ca7-105">By providing these custom, on-demand, cloud-based databases tooyour users, you can save them time and resources.</span></span> <span data-ttu-id="b3ca7-106">tooset этот показатель будет:</span><span class="sxs-lookup"><span data-stu-id="b3ca7-106">tooset this up, you will:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b3ca7-107">Разверните hello поставщик ресурсов SQL Server</span><span class="sxs-lookup"><span data-stu-id="b3ca7-107">Deploy hello SQL Server resource provider</span></span>
> * <span data-ttu-id="b3ca7-108">Создание предложения</span><span class="sxs-lookup"><span data-stu-id="b3ca7-108">Create an offer</span></span>
> * <span data-ttu-id="b3ca7-109">Предложение hello теста</span><span class="sxs-lookup"><span data-stu-id="b3ca7-109">Test hello offer</span></span>

## <a name="deploy-hello-sql-server-resource-provider"></a><span data-ttu-id="b3ca7-110">Разверните hello поставщик ресурсов SQL Server</span><span class="sxs-lookup"><span data-stu-id="b3ca7-110">Deploy hello SQL Server resource provider</span></span>

<span data-ttu-id="b3ca7-111">процесс развертывания Hello подробно в hello [баз данных SQL используйте статьи стек Azure](azure-stack-sql-resource-provider-deploy.md)и состоит из следующих основных шага hello:</span><span class="sxs-lookup"><span data-stu-id="b3ca7-111">hello deployment process is described in detail in hello [Use SQL databases on Azure Stack article](azure-stack-sql-resource-provider-deploy.md), and is comprised of hello following primary steps:</span></span>

1.  <span data-ttu-id="b3ca7-112">[Развертывание поставщика ресурсов SQL hello]( azure-stack-sql-resource-provider-deploy.md#deploy-the-resource-provider).</span><span class="sxs-lookup"><span data-stu-id="b3ca7-112">[Deploy hello SQL resource provider]( azure-stack-sql-resource-provider-deploy.md#deploy-the-resource-provider).</span></span>
2.  <span data-ttu-id="b3ca7-113">[Проверка развертывания hello]( azure-stack-sql-resource-provider-deploy.md#verify-the-deployment-using-the-azure-stack-portal).</span><span class="sxs-lookup"><span data-stu-id="b3ca7-113">[Verify hello deployment]( azure-stack-sql-resource-provider-deploy.md#verify-the-deployment-using-the-azure-stack-portal).</span></span>
3.  <span data-ttu-id="b3ca7-114">[Предоставляют емкость, подключив tooa, где размещен SQL server]( azure-stack-sql-resource-provider-deploy.md#provide-capacity-by-connecting-to-a-hosting-sql-server).</span><span class="sxs-lookup"><span data-stu-id="b3ca7-114">[Provide capacity by connecting tooa hosting SQL server]( azure-stack-sql-resource-provider-deploy.md#provide-capacity-by-connecting-to-a-hosting-sql-server).</span></span>

## <a name="create-an-offer"></a><span data-ttu-id="b3ca7-115">Создание предложения</span><span class="sxs-lookup"><span data-stu-id="b3ca7-115">Create an offer</span></span>

1.  <span data-ttu-id="b3ca7-116">[Задать квоты](azure-stack-setting-quotas.md) и назовите его *SQLServerQuota*.</span><span class="sxs-lookup"><span data-stu-id="b3ca7-116">[Set a quota](azure-stack-setting-quotas.md) and name it *SQLServerQuota*.</span></span> <span data-ttu-id="b3ca7-117">Выберите **Microsoft.SQLAdapter** для hello **имен** поля.</span><span class="sxs-lookup"><span data-stu-id="b3ca7-117">Select **Microsoft.SQLAdapter** for hello **Namespace** field.</span></span>
2.  <span data-ttu-id="b3ca7-118">[Создание плана](azure-stack-create-plan.md).</span><span class="sxs-lookup"><span data-stu-id="b3ca7-118">[Create a plan](azure-stack-create-plan.md).</span></span> <span data-ttu-id="b3ca7-119">Назовите его *TestSQLServerPlan*выберите hello **Microsoft.SQLAdapter** службы, и **SQLServerQuota** квоты.</span><span class="sxs-lookup"><span data-stu-id="b3ca7-119">Name it *TestSQLServerPlan*, select hello **Microsoft.SQLAdapter** service, and **SQLServerQuota** quota.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b3ca7-120">Пользователи toolet создавать другие приложения, в плане hello могут потребоваться другие службы.</span><span class="sxs-lookup"><span data-stu-id="b3ca7-120">toolet users create other apps, other services might be required in hello plan.</span></span> <span data-ttu-id="b3ca7-121">Например, функции Azure требует этого плана hello hello **хранилища Майкрософт** обслуживание, когда требуется Wordpress **Microsoft.MySQLAdapter**.</span><span class="sxs-lookup"><span data-stu-id="b3ca7-121">For example, Azure Functions requires that hello plan include hello **Microsoft.Storage** service, while Wordpress requires **Microsoft.MySQLAdapter**.</span></span>
    > 
    >

3.  <span data-ttu-id="b3ca7-122">[Создать предложение](azure-stack-create-offer.md), назовите его **TestSQLServerOffer** и выберите hello **TestSQLServerPlan** плана.</span><span class="sxs-lookup"><span data-stu-id="b3ca7-122">[Create an offer](azure-stack-create-offer.md), name it **TestSQLServerOffer** and select hello **TestSQLServerPlan** plan.</span></span>

## <a name="test-hello-offer"></a><span data-ttu-id="b3ca7-123">Предложение hello теста</span><span class="sxs-lookup"><span data-stu-id="b3ca7-123">Test hello offer</span></span>

<span data-ttu-id="b3ca7-124">Теперь, когда вы развернули hello поставщик ресурсов SQL Server и создать предложение, вы сможете войти как пользователь, подписаться toohello предложение и создать базу данных.</span><span class="sxs-lookup"><span data-stu-id="b3ca7-124">Now that you've deployed hello SQL Server resource provider and created an offer, you can sign in as a user, subscribe toohello offer, and create a database.</span></span>

### <a name="subscribe-toohello-offer"></a><span data-ttu-id="b3ca7-125">Подписаться на предложение toohello</span><span class="sxs-lookup"><span data-stu-id="b3ca7-125">Subscribe toohello offer</span></span>
1. <span data-ttu-id="b3ca7-126">Войдите в toohello портала Azure стека (https://portal.local.azurestack.external) как клиента.</span><span class="sxs-lookup"><span data-stu-id="b3ca7-126">Sign in toohello Azure Stack portal (https://portal.local.azurestack.external) as a tenant.</span></span>
2. <span data-ttu-id="b3ca7-127">Нажмите кнопку **получить подписку** , а затем введите **TestSQLServerSubscription** под **отображаемое имя**.</span><span class="sxs-lookup"><span data-stu-id="b3ca7-127">Click **Get a subscription** and then type **TestSQLServerSubscription** under **Display Name**.</span></span>
3. <span data-ttu-id="b3ca7-128">Нажмите кнопку **выберите предложение** > **TestSQLServerOffer** > **создать**.</span><span class="sxs-lookup"><span data-stu-id="b3ca7-128">Click **Select an offer** > **TestSQLServerOffer** > **Create**.</span></span>
4. <span data-ttu-id="b3ca7-129">Нажмите кнопку **дополнительные службы** > **подписки** > **TestSQLServerSubscription** > **ресурсов Поставщики**.</span><span class="sxs-lookup"><span data-stu-id="b3ca7-129">Click **More services** > **Subscriptions** > **TestSQLServerSubscription** > **Resource providers**.</span></span>
5. <span data-ttu-id="b3ca7-130">Нажмите кнопку **зарегистрировать** Далее toohello **Microsoft.SQLAdapter** поставщика.</span><span class="sxs-lookup"><span data-stu-id="b3ca7-130">Click **Register** next toohello **Microsoft.SQLAdapter** provider.</span></span>

### <a name="create-a-sql-database"></a><span data-ttu-id="b3ca7-131">Создание базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="b3ca7-131">Create a SQL database</span></span>

1. <span data-ttu-id="b3ca7-132">Нажмите кнопку  **+**   >  **данные + хранилище** > **базы данных SQL**.</span><span class="sxs-lookup"><span data-stu-id="b3ca7-132">Click **+** > **Data + Storage** > **SQL Database**.</span></span>
2. <span data-ttu-id="b3ca7-133">Значения по умолчанию hello оставьте поля hello, или можно использовать эти примеры:</span><span class="sxs-lookup"><span data-stu-id="b3ca7-133">Leave hello defaults for hello fields, or you can use these examples:</span></span>
    - <span data-ttu-id="b3ca7-134">**Имя базы данных**: SQLdb</span><span class="sxs-lookup"><span data-stu-id="b3ca7-134">**Database Name**: SQLdb</span></span>
    - <span data-ttu-id="b3ca7-135">**Максимальный размер в МБ**: 100</span><span class="sxs-lookup"><span data-stu-id="b3ca7-135">**Max Size in MB**: 100</span></span>
    - <span data-ttu-id="b3ca7-136">**Подписки**: TestSQLOffer</span><span class="sxs-lookup"><span data-stu-id="b3ca7-136">**Subscription**: TestSQLOffer</span></span>
    - <span data-ttu-id="b3ca7-137">**Группа ресурсов**: SQL RG</span><span class="sxs-lookup"><span data-stu-id="b3ca7-137">**Resource Group**: SQL-RG</span></span>
3. <span data-ttu-id="b3ca7-138">Нажмите кнопку **параметры входа**, введите учетные данные для базы данных hello и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b3ca7-138">Click **Login Settings**, enter credentials for hello database, and then click **OK**.</span></span>
4. <span data-ttu-id="b3ca7-139">Нажмите кнопку **SKU** > выберите hello SKU SQL, созданный для hello сервер размещения SQL > **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b3ca7-139">Click **SKU** > select hello SQL SKU that you created for hello SQL Hosting Server > **OK**.</span></span>
5. <span data-ttu-id="b3ca7-140">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b3ca7-140">Click **Create**.</span></span>

<span data-ttu-id="b3ca7-141">Из этого руководства вы узнали, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="b3ca7-141">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b3ca7-142">Разверните hello поставщик ресурсов SQL Server</span><span class="sxs-lookup"><span data-stu-id="b3ca7-142">Deploy hello SQL Server resource provider</span></span>
> * <span data-ttu-id="b3ca7-143">Создание предложения</span><span class="sxs-lookup"><span data-stu-id="b3ca7-143">Create an offer</span></span>
> * <span data-ttu-id="b3ca7-144">Предложение hello теста</span><span class="sxs-lookup"><span data-stu-id="b3ca7-144">Test hello offer</span></span>

<span data-ttu-id="b3ca7-145">Как переместить следующий учебник toolearn toohello для:</span><span class="sxs-lookup"><span data-stu-id="b3ca7-145">Advance toohello next tutorial toolearn how to:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b3ca7-146">Сделать web, мобильных устройств и пользователей доступны tooyour приложения API</span><span class="sxs-lookup"><span data-stu-id="b3ca7-146">Make web, mobile, and API apps available tooyour users</span></span>]( azure-stack-tutorial-app-service.md)

