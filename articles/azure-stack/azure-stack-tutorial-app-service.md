---
title: "aaaMake веб, мобильных устройств и пользователей стек Azure доступны tooyour приложения API | Документы Microsoft"
description: "Учебника tooinstall hello поставщик ресурсов службы приложений и создание предложения, обеспечивающие вашей стек Azure пользователи hello возможность toocreate web, мобильных устройств и приложения API."
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
ms.openlocfilehash: 62b86cf6288b8f629bc92dade003c712fe523187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="make-web-mobile-and-api-apps-available-tooyour-azure-stack-users"></a><span data-ttu-id="cdcdd-103">Сделать веб, мобильных устройств и пользователей стек Azure доступны tooyour приложения API</span><span class="sxs-lookup"><span data-stu-id="cdcdd-103">Make web, mobile, and API apps available tooyour Azure Stack users</span></span>

<span data-ttu-id="cdcdd-104">Как администратор облака Azure стека, можно создать предложения, которые позволяют пользователям (клиентов) создавать приложения Azure функции и web, мобильных устройств и API.</span><span class="sxs-lookup"><span data-stu-id="cdcdd-104">As an Azure Stack cloud administrator, you can create offers that let your users (tenants) create Azure Functions and web, mobile, and API applications.</span></span> <span data-ttu-id="cdcdd-105">Путем предоставления доступа пользователям tooyour toothese по требованию, облачные приложения, их можно сэкономить время и ресурсы.</span><span class="sxs-lookup"><span data-stu-id="cdcdd-105">By providing access toothese on-demand, cloud-based apps tooyour users, you can save them time and resources.</span></span> <span data-ttu-id="cdcdd-106">tooset этот показатель будет:</span><span class="sxs-lookup"><span data-stu-id="cdcdd-106">tooset this up, you will:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cdcdd-107">Развертывание hello поставщик ресурсов службы приложений</span><span class="sxs-lookup"><span data-stu-id="cdcdd-107">Deploy hello App Service resource provider</span></span>
> * <span data-ttu-id="cdcdd-108">Создание предложения</span><span class="sxs-lookup"><span data-stu-id="cdcdd-108">Create an offer</span></span>
> * <span data-ttu-id="cdcdd-109">Предложение hello теста</span><span class="sxs-lookup"><span data-stu-id="cdcdd-109">Test hello offer</span></span>

## <a name="deploy-hello-app-service-resource-provider"></a><span data-ttu-id="cdcdd-110">Развертывание hello поставщик ресурсов службы приложений</span><span class="sxs-lookup"><span data-stu-id="cdcdd-110">Deploy hello App Service resource provider</span></span>

1. <span data-ttu-id="cdcdd-111">[Подготовка узла Azure стека Development Kit hello](azure-stack-app-service-before-you-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="cdcdd-111">[Prepare hello Azure Stack Development Kit host](azure-stack-app-service-before-you-get-started.md).</span></span> <span data-ttu-id="cdcdd-112">Это включает в себя развертывание hello поставщик ресурсов SQL Server, который необходим для создания некоторых приложений.</span><span class="sxs-lookup"><span data-stu-id="cdcdd-112">This includes deploying hello SQL Server resource provider, which is required for creating some apps.</span></span>
2. <span data-ttu-id="cdcdd-113">[Загрузите скрипты установки и вспомогательные hello](azure-stack-app-service-deploy.md#download-the-required-components).</span><span class="sxs-lookup"><span data-stu-id="cdcdd-113">[Download hello installer and helper scripts](azure-stack-app-service-deploy.md#download-the-required-components).</span></span>
3. <span data-ttu-id="cdcdd-114">[Запустите сценарий вспомогательный hello toocreate необходимые сертификаты](azure-stack-app-service-deploy.md#create-certificates-required-by-app-service-on-azure-stack).</span><span class="sxs-lookup"><span data-stu-id="cdcdd-114">[Run hello helper script toocreate required certificates](azure-stack-app-service-deploy.md#create-certificates-required-by-app-service-on-azure-stack).</span></span>
4. <span data-ttu-id="cdcdd-115">[Установить поставщик ресурсов службы приложения hello](azure-stack-app-service-deploy.md#use-the-installer-to-download-and-install-app-service-on-azure-stack) (может занять несколько часов tooinstall и для всех hello tooappear рабочих ролей).</span><span class="sxs-lookup"><span data-stu-id="cdcdd-115">[Install hello App Service resource provider](azure-stack-app-service-deploy.md#use-the-installer-to-download-and-install-app-service-on-azure-stack) (it will take a couple hours tooinstall and for all hello worker roles tooappear).</span></span>
5. <span data-ttu-id="cdcdd-116">[Проверка установки hello](azure-stack-app-service-deploy.md#validate-the-app-service-on-azure-stack-installation).</span><span class="sxs-lookup"><span data-stu-id="cdcdd-116">[Validate hello installation](azure-stack-app-service-deploy.md#validate-the-app-service-on-azure-stack-installation).</span></span>

## <a name="create-an-offer"></a><span data-ttu-id="cdcdd-117">Создание предложения</span><span class="sxs-lookup"><span data-stu-id="cdcdd-117">Create an offer</span></span>

<span data-ttu-id="cdcdd-118">Например можно создать предложение, которое позволяет пользователям создавать DNN веб-системы управления содержимым.</span><span class="sxs-lookup"><span data-stu-id="cdcdd-118">As an example, you can create an offer that lets users create DNN web content management systems.</span></span> <span data-ttu-id="cdcdd-119">Он требует hello службы SQL Server, которая уже включена, установив hello поставщик ресурсов SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cdcdd-119">It requires hello SQL Server service which you already enabled by installing hello SQL Server resource provider.</span></span>

1.  <span data-ttu-id="cdcdd-120">[Задать квоты](azure-stack-setting-quotas.md) и назовите его *AppServiceQuota*.</span><span class="sxs-lookup"><span data-stu-id="cdcdd-120">[Set a quota](azure-stack-setting-quotas.md) and name it *AppServiceQuota*.</span></span> <span data-ttu-id="cdcdd-121">Выберите **Microsoft.Web** для hello **имен** поля.</span><span class="sxs-lookup"><span data-stu-id="cdcdd-121">Select **Microsoft.Web** for hello **Namespace** field.</span></span>
2.  <span data-ttu-id="cdcdd-122">[Создание плана](azure-stack-create-plan.md).</span><span class="sxs-lookup"><span data-stu-id="cdcdd-122">[Create a plan](azure-stack-create-plan.md).</span></span> <span data-ttu-id="cdcdd-123">Назовите его *TestAppServicePlan*выберите hello hello **Microsoft.SQL** службы, и **AppService квоты** квоты.</span><span class="sxs-lookup"><span data-stu-id="cdcdd-123">Name it *TestAppServicePlan*, select hello hello **Microsoft.SQL** service, and **AppService Quota** quota.</span></span>

    > [!NOTE]
    > <span data-ttu-id="cdcdd-124">Пользователи toolet создавать другие приложения, в плане hello могут потребоваться другие службы.</span><span class="sxs-lookup"><span data-stu-id="cdcdd-124">toolet users create other apps, other services might be required in hello plan.</span></span> <span data-ttu-id="cdcdd-125">Например, функции Azure требует этого плана hello hello **хранилища Майкрософт** обслуживание, когда требуется Wordpress **Microsoft.MySQL**.</span><span class="sxs-lookup"><span data-stu-id="cdcdd-125">For example, Azure Functions requires that hello plan     include hello **Microsoft.Storage** service, while Wordpress requires **Microsoft.MySQL**.</span></span>
    > 
    >

3.  <span data-ttu-id="cdcdd-126">[Создать предложение](azure-stack-create-offer.md), назовите его **TestAppServiceOffer** и выберите hello **TestAppServicePlan** плана.</span><span class="sxs-lookup"><span data-stu-id="cdcdd-126">[Create an offer](azure-stack-create-offer.md), name it **TestAppServiceOffer** and select hello **TestAppServicePlan** plan.</span></span>

## <a name="test-hello-offer"></a><span data-ttu-id="cdcdd-127">Предложение hello теста</span><span class="sxs-lookup"><span data-stu-id="cdcdd-127">Test hello offer</span></span>

<span data-ttu-id="cdcdd-128">Теперь, когда вы развернули hello поставщик ресурсов службы приложений и создать предложение, вы сможете войти как пользователь, подписаться toohello предложение и создать приложение.</span><span class="sxs-lookup"><span data-stu-id="cdcdd-128">Now that you've deployed hello App Service resource provider and created an offer, you can sign in as a user, subscribe toohello offer, and create an app.</span></span> <span data-ttu-id="cdcdd-129">В этом примере мы создадим платформы DNN системы управления контентом.</span><span class="sxs-lookup"><span data-stu-id="cdcdd-129">For this example, we'll create a DNN Platform content management system.</span></span> <span data-ttu-id="cdcdd-130">Сначала необходимо создать базу данных SQL и hello DNN веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="cdcdd-130">You must first create a SQL database and then hello DNN web app.</span></span>

### <a name="subscribe-toohello-offer"></a><span data-ttu-id="cdcdd-131">Подписаться на предложение toohello</span><span class="sxs-lookup"><span data-stu-id="cdcdd-131">Subscribe toohello offer</span></span>
1. <span data-ttu-id="cdcdd-132">Войдите в toohello портала Azure стека (https://portal.local.azurestack.external) как клиента.</span><span class="sxs-lookup"><span data-stu-id="cdcdd-132">Sign in toohello Azure Stack portal (https://portal.local.azurestack.external) as a tenant.</span></span>
2. <span data-ttu-id="cdcdd-133">Нажмите кнопку **получить подписку** > тип **TestAppServiceSubscription** под **отображаемое имя** > **выберите предложение**  >  **TestAppServiceOffer** > **создания**.</span><span class="sxs-lookup"><span data-stu-id="cdcdd-133">Click **Get a subscription** > type **TestAppServiceSubscription** under **Display Name** > **Select an offer** > **TestAppServiceOffer** > **Create**.</span></span>

### <a name="create-a-sql-database"></a><span data-ttu-id="cdcdd-134">Создание базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="cdcdd-134">Create a SQL database</span></span>

1. <span data-ttu-id="cdcdd-135">Нажмите кнопку  **+**   >  **данные + хранилище** > **базы данных SQL**.</span><span class="sxs-lookup"><span data-stu-id="cdcdd-135">Click **+** > **Data + Storage** > **SQL Database**.</span></span>
2. <span data-ttu-id="cdcdd-136">Оставьте hello значения по умолчанию для полей hello, за исключением того, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="cdcdd-136">Leave hello defaults for hello fields, except as follows:</span></span>
    - <span data-ttu-id="cdcdd-137">**Имя базы данных**: DNNdb</span><span class="sxs-lookup"><span data-stu-id="cdcdd-137">**Database Name**: DNNdb</span></span>
    - <span data-ttu-id="cdcdd-138">**Максимальный размер в МБ**: 100</span><span class="sxs-lookup"><span data-stu-id="cdcdd-138">**Max Size in MB**: 100</span></span>
    - <span data-ttu-id="cdcdd-139">**Подписки**: TestAppServiceOffer</span><span class="sxs-lookup"><span data-stu-id="cdcdd-139">**Subscription**: TestAppServiceOffer</span></span>
    - <span data-ttu-id="cdcdd-140">**Группа ресурсов**: DNN RG</span><span class="sxs-lookup"><span data-stu-id="cdcdd-140">**Resource Group**: DNN-RG</span></span>
3. <span data-ttu-id="cdcdd-141">Нажмите кнопку **параметры входа**, введите учетные данные для базы данных hello и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="cdcdd-141">Click **Login Settings**, enter credentials for hello database, and then click **OK**.</span></span> <span data-ttu-id="cdcdd-142">Эти учетные данные будут использоваться позже в следующие действия.</span><span class="sxs-lookup"><span data-stu-id="cdcdd-142">You'll use these credentials later in these steps.</span></span>
4. <span data-ttu-id="cdcdd-143">Нажмите кнопку **SKU** > выберите hello SKU SQL, созданный для hello сервер размещения SQL > **ОК**.</span><span class="sxs-lookup"><span data-stu-id="cdcdd-143">Click **SKU** > select hello SQL SKU that you created for hello SQL Hosting Server > **OK**.</span></span>
5. <span data-ttu-id="cdcdd-144">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="cdcdd-144">Click **Create**.</span></span>

### <a name="create-a-dnn-app"></a><span data-ttu-id="cdcdd-145">Создание приложения DNN</span><span class="sxs-lookup"><span data-stu-id="cdcdd-145">Create a DNN app</span></span>    

1. <span data-ttu-id="cdcdd-146">Нажмите кнопку  **+**   >  **все** > **Предварительная версия платформы DNN** > **создать**.</span><span class="sxs-lookup"><span data-stu-id="cdcdd-146">Click **+** > **See all** > **DNN Platform preview** > **Create**.</span></span>
2. <span data-ttu-id="cdcdd-147">Тип *DNNapp* под **имя приложения** и выберите **TestAppServiceOffer** под **подписки**.</span><span class="sxs-lookup"><span data-stu-id="cdcdd-147">Type *DNNapp* under **App name** and select **TestAppServiceOffer** under **Subscription**.</span></span>
3. <span data-ttu-id="cdcdd-148">Нажмите кнопку **настроить необходимые параметры** > **создать новый** > тип **план служб приложений** имя.</span><span class="sxs-lookup"><span data-stu-id="cdcdd-148">Click **Configure required settings** > **Create New** > type an **App Service plan** name.</span></span>
4. <span data-ttu-id="cdcdd-149">Нажмите кнопку **Ценовая категория** > **F1 свободного** > **выберите** > **ОК**.</span><span class="sxs-lookup"><span data-stu-id="cdcdd-149">Click **Pricing tier** > **F1 Free** > **Select** > **OK**.</span></span>
5. <span data-ttu-id="cdcdd-150">Нажмите кнопку **базы данных** и введите данные hello hello базы данных SQL, созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="cdcdd-150">Click **Database** and enter hello information for hello SQL database you created earlier.</span></span>
6. <span data-ttu-id="cdcdd-151">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="cdcdd-151">Click **Create**.</span></span>

<span data-ttu-id="cdcdd-152">Из этого руководства вы узнали, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="cdcdd-152">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cdcdd-153">Развертывание hello поставщик ресурсов службы приложений</span><span class="sxs-lookup"><span data-stu-id="cdcdd-153">Deploy hello App Service resource provider</span></span>
> * <span data-ttu-id="cdcdd-154">Создание предложения</span><span class="sxs-lookup"><span data-stu-id="cdcdd-154">Create an offer</span></span>
> * <span data-ttu-id="cdcdd-155">Предложение hello теста</span><span class="sxs-lookup"><span data-stu-id="cdcdd-155">Test hello offer</span></span>

<span data-ttu-id="cdcdd-156">Как переместить следующий учебник toolearn toohello для:</span><span class="sxs-lookup"><span data-stu-id="cdcdd-156">Advance toohello next tutorial toolearn how to:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cdcdd-157">Развертывание приложений tooAzure и стек Azure</span><span class="sxs-lookup"><span data-stu-id="cdcdd-157">Deploy apps tooAzure and Azure Stack</span></span>](azure-stack-solution-pipeline.md)
