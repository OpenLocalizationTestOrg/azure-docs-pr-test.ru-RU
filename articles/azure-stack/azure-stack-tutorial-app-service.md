---
title: "Предоставить web, мобильных устройств и приложения API Azure стека пользователям | Документы Microsoft"
description: "Учебник, чтобы установить поставщик ресурсов службы приложений и создать предлагает, предоставить пользователям Azure стека возможность создавать веб-мобильных устройств и приложения API."
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
ms.openlocfilehash: 11ecaa8ec017a9eb1285928e3d3d367ddfc43022
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="make-web-mobile-and-api-apps-available-to-your-azure-stack-users"></a><span data-ttu-id="04f5a-103">Предоставить web, мобильных устройств и приложения API пользователям стек Azure</span><span class="sxs-lookup"><span data-stu-id="04f5a-103">Make web, mobile, and API apps available to your Azure Stack users</span></span>

<span data-ttu-id="04f5a-104">Как администратор облака Azure стека, можно создать предложения, которые позволяют пользователям (клиентов) создавать приложения Azure функции и web, мобильных устройств и API.</span><span class="sxs-lookup"><span data-stu-id="04f5a-104">As an Azure Stack cloud administrator, you can create offers that let your users (tenants) create Azure Functions and web, mobile, and API applications.</span></span> <span data-ttu-id="04f5a-105">Предоставляя доступ к этим приложениям по требованию, основанное на облаке для пользователей, их можно сохранить время и ресурсы.</span><span class="sxs-lookup"><span data-stu-id="04f5a-105">By providing access to these on-demand, cloud-based apps to your users, you can save them time and resources.</span></span> <span data-ttu-id="04f5a-106">Чтобы настроить это подключение, выполняет следующие действия:</span><span class="sxs-lookup"><span data-stu-id="04f5a-106">To set this up, you will:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="04f5a-107">Разверните поставщик ресурсов службы приложений</span><span class="sxs-lookup"><span data-stu-id="04f5a-107">Deploy the App Service resource provider</span></span>
> * <span data-ttu-id="04f5a-108">Создание предложения</span><span class="sxs-lookup"><span data-stu-id="04f5a-108">Create an offer</span></span>
> * <span data-ttu-id="04f5a-109">Тестирование предложение</span><span class="sxs-lookup"><span data-stu-id="04f5a-109">Test the offer</span></span>

## <a name="deploy-the-app-service-resource-provider"></a><span data-ttu-id="04f5a-110">Разверните поставщик ресурсов службы приложений</span><span class="sxs-lookup"><span data-stu-id="04f5a-110">Deploy the App Service resource provider</span></span>

1. <span data-ttu-id="04f5a-111">[Подготовка узла Azure стека Development Kit](azure-stack-app-service-before-you-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="04f5a-111">[Prepare the Azure Stack Development Kit host](azure-stack-app-service-before-you-get-started.md).</span></span> <span data-ttu-id="04f5a-112">Это включает в себя развертывание поставщика ресурсов SQL Server, который необходим для создания некоторых приложений.</span><span class="sxs-lookup"><span data-stu-id="04f5a-112">This includes deploying the SQL Server resource provider, which is required for creating some apps.</span></span>
2. <span data-ttu-id="04f5a-113">[Загрузите скрипты установки и вспомогательные](azure-stack-app-service-deploy.md#download-the-required-components).</span><span class="sxs-lookup"><span data-stu-id="04f5a-113">[Download the installer and helper scripts](azure-stack-app-service-deploy.md#download-the-required-components).</span></span>
3. <span data-ttu-id="04f5a-114">[Запустите вспомогательный сценарий для создания необходимых сертификатов](azure-stack-app-service-deploy.md#create-certificates-required-by-app-service-on-azure-stack).</span><span class="sxs-lookup"><span data-stu-id="04f5a-114">[Run the helper script to create required certificates](azure-stack-app-service-deploy.md#create-certificates-required-by-app-service-on-azure-stack).</span></span>
4. <span data-ttu-id="04f5a-115">[Установка поставщика ресурсов службы приложений](azure-stack-app-service-deploy.md#use-the-installer-to-download-and-install-app-service-on-azure-stack) (может занять несколько часов для установки и для всех рабочих ролей для отображения).</span><span class="sxs-lookup"><span data-stu-id="04f5a-115">[Install the App Service resource provider](azure-stack-app-service-deploy.md#use-the-installer-to-download-and-install-app-service-on-azure-stack) (it will take a couple hours to install and for all the worker roles to appear).</span></span>
5. <span data-ttu-id="04f5a-116">[Проверка установки](azure-stack-app-service-deploy.md#validate-the-app-service-on-azure-stack-installation).</span><span class="sxs-lookup"><span data-stu-id="04f5a-116">[Validate the installation](azure-stack-app-service-deploy.md#validate-the-app-service-on-azure-stack-installation).</span></span>

## <a name="create-an-offer"></a><span data-ttu-id="04f5a-117">Создание предложения</span><span class="sxs-lookup"><span data-stu-id="04f5a-117">Create an offer</span></span>

<span data-ttu-id="04f5a-118">Например можно создать предложение, которое позволяет пользователям создавать DNN веб-системы управления содержимым.</span><span class="sxs-lookup"><span data-stu-id="04f5a-118">As an example, you can create an offer that lets users create DNN web content management systems.</span></span> <span data-ttu-id="04f5a-119">Требуется служба SQL Server, которая уже включена, установив поставщик ресурсов SQL Server.</span><span class="sxs-lookup"><span data-stu-id="04f5a-119">It requires the SQL Server service which you already enabled by installing the SQL Server resource provider.</span></span>

1.  <span data-ttu-id="04f5a-120">[Задать квоты](azure-stack-setting-quotas.md) и назовите его *AppServiceQuota*.</span><span class="sxs-lookup"><span data-stu-id="04f5a-120">[Set a quota](azure-stack-setting-quotas.md) and name it *AppServiceQuota*.</span></span> <span data-ttu-id="04f5a-121">Выберите **Microsoft.Web** для **имен** поля.</span><span class="sxs-lookup"><span data-stu-id="04f5a-121">Select **Microsoft.Web** for the **Namespace** field.</span></span>
2.  <span data-ttu-id="04f5a-122">[Создание плана](azure-stack-create-plan.md).</span><span class="sxs-lookup"><span data-stu-id="04f5a-122">[Create a plan](azure-stack-create-plan.md).</span></span> <span data-ttu-id="04f5a-123">Назовите его *TestAppServicePlan*выберите **Microsoft.SQL** службы, и **AppService квоты** квоты.</span><span class="sxs-lookup"><span data-stu-id="04f5a-123">Name it *TestAppServicePlan*, select the the **Microsoft.SQL** service, and **AppService Quota** quota.</span></span>

    > [!NOTE]
    > <span data-ttu-id="04f5a-124">Чтобы пользователи могли создавать другие приложения, могут потребоваться другие службы в плане.</span><span class="sxs-lookup"><span data-stu-id="04f5a-124">To let users create other apps, other services might be required in the plan.</span></span> <span data-ttu-id="04f5a-125">Например, функции Azure нужно будет добавить план **хранилища Майкрософт** обслуживание, когда требуется Wordpress **Microsoft.MySQL**.</span><span class="sxs-lookup"><span data-stu-id="04f5a-125">For example, Azure Functions requires that the plan     include the **Microsoft.Storage** service, while Wordpress requires **Microsoft.MySQL**.</span></span>
    > 
    >

3.  <span data-ttu-id="04f5a-126">[Создать предложение](azure-stack-create-offer.md), назовите его **TestAppServiceOffer** и выберите **TestAppServicePlan** плана.</span><span class="sxs-lookup"><span data-stu-id="04f5a-126">[Create an offer](azure-stack-create-offer.md), name it **TestAppServiceOffer** and select the **TestAppServicePlan** plan.</span></span>

## <a name="test-the-offer"></a><span data-ttu-id="04f5a-127">Тестирование предложение</span><span class="sxs-lookup"><span data-stu-id="04f5a-127">Test the offer</span></span>

<span data-ttu-id="04f5a-128">Теперь, после развертывания приложения службы поставщика ресурсов и создать предложение, вы сможете войти как пользователь, Подпишитесь на предложение и создать приложение.</span><span class="sxs-lookup"><span data-stu-id="04f5a-128">Now that you've deployed the App Service resource provider and created an offer, you can sign in as a user, subscribe to the offer, and create an app.</span></span> <span data-ttu-id="04f5a-129">В этом примере мы создадим платформы DNN системы управления контентом.</span><span class="sxs-lookup"><span data-stu-id="04f5a-129">For this example, we'll create a DNN Platform content management system.</span></span> <span data-ttu-id="04f5a-130">Сначала необходимо создать базу данных SQL, а затем DNN веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="04f5a-130">You must first create a SQL database and then the DNN web app.</span></span>

### <a name="subscribe-to-the-offer"></a><span data-ttu-id="04f5a-131">Подписаться на предложение</span><span class="sxs-lookup"><span data-stu-id="04f5a-131">Subscribe to the offer</span></span>
1. <span data-ttu-id="04f5a-132">Войдите на портал Azure стека (https://portal.local.azurestack.external) клиента.</span><span class="sxs-lookup"><span data-stu-id="04f5a-132">Sign in to the Azure Stack portal (https://portal.local.azurestack.external) as a tenant.</span></span>
2. <span data-ttu-id="04f5a-133">Нажмите кнопку **получить подписку** > тип **TestAppServiceSubscription** под **отображаемое имя** > **выберите предложение**  >  **TestAppServiceOffer** > **создания**.</span><span class="sxs-lookup"><span data-stu-id="04f5a-133">Click **Get a subscription** > type **TestAppServiceSubscription** under **Display Name** > **Select an offer** > **TestAppServiceOffer** > **Create**.</span></span>

### <a name="create-a-sql-database"></a><span data-ttu-id="04f5a-134">Создание базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="04f5a-134">Create a SQL database</span></span>

1. <span data-ttu-id="04f5a-135">Нажмите кнопку  **+**   >  **данные + хранилище** > **базы данных SQL**.</span><span class="sxs-lookup"><span data-stu-id="04f5a-135">Click **+** > **Data + Storage** > **SQL Database**.</span></span>
2. <span data-ttu-id="04f5a-136">Оставьте значения по умолчанию для полей, за исключением того, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04f5a-136">Leave the defaults for the fields, except as follows:</span></span>
    - <span data-ttu-id="04f5a-137">**Имя базы данных**: DNNdb</span><span class="sxs-lookup"><span data-stu-id="04f5a-137">**Database Name**: DNNdb</span></span>
    - <span data-ttu-id="04f5a-138">**Максимальный размер в МБ**: 100</span><span class="sxs-lookup"><span data-stu-id="04f5a-138">**Max Size in MB**: 100</span></span>
    - <span data-ttu-id="04f5a-139">**Подписки**: TestAppServiceOffer</span><span class="sxs-lookup"><span data-stu-id="04f5a-139">**Subscription**: TestAppServiceOffer</span></span>
    - <span data-ttu-id="04f5a-140">**Группа ресурсов**: DNN RG</span><span class="sxs-lookup"><span data-stu-id="04f5a-140">**Resource Group**: DNN-RG</span></span>
3. <span data-ttu-id="04f5a-141">Нажмите кнопку **параметры входа**, введите учетные данные для базы данных и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="04f5a-141">Click **Login Settings**, enter credentials for the database, and then click **OK**.</span></span> <span data-ttu-id="04f5a-142">Эти учетные данные будут использоваться позже в следующие действия.</span><span class="sxs-lookup"><span data-stu-id="04f5a-142">You'll use these credentials later in these steps.</span></span>
4. <span data-ttu-id="04f5a-143">Нажмите кнопку **SKU** > выберите SKU SQL, созданную для сервера размещения SQL > **ОК**.</span><span class="sxs-lookup"><span data-stu-id="04f5a-143">Click **SKU** > select the SQL SKU that you created for the SQL Hosting Server > **OK**.</span></span>
5. <span data-ttu-id="04f5a-144">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="04f5a-144">Click **Create**.</span></span>

### <a name="create-a-dnn-app"></a><span data-ttu-id="04f5a-145">Создание приложения DNN</span><span class="sxs-lookup"><span data-stu-id="04f5a-145">Create a DNN app</span></span>    

1. <span data-ttu-id="04f5a-146">Нажмите кнопку  **+**   >  **все** > **Предварительная версия платформы DNN** > **создать**.</span><span class="sxs-lookup"><span data-stu-id="04f5a-146">Click **+** > **See all** > **DNN Platform preview** > **Create**.</span></span>
2. <span data-ttu-id="04f5a-147">Тип *DNNapp* под **имя приложения** и выберите **TestAppServiceOffer** под **подписки**.</span><span class="sxs-lookup"><span data-stu-id="04f5a-147">Type *DNNapp* under **App name** and select **TestAppServiceOffer** under **Subscription**.</span></span>
3. <span data-ttu-id="04f5a-148">Нажмите кнопку **настроить необходимые параметры** > **создать новый** > тип **план служб приложений** имя.</span><span class="sxs-lookup"><span data-stu-id="04f5a-148">Click **Configure required settings** > **Create New** > type an **App Service plan** name.</span></span>
4. <span data-ttu-id="04f5a-149">Нажмите кнопку **Ценовая категория** > **F1 свободного** > **выберите** > **ОК**.</span><span class="sxs-lookup"><span data-stu-id="04f5a-149">Click **Pricing tier** > **F1 Free** > **Select** > **OK**.</span></span>
5. <span data-ttu-id="04f5a-150">Нажмите кнопку **базы данных** и введите данные для базы данных SQL, созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="04f5a-150">Click **Database** and enter the information for the SQL database you created earlier.</span></span>
6. <span data-ttu-id="04f5a-151">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="04f5a-151">Click **Create**.</span></span>

<span data-ttu-id="04f5a-152">Из этого руководства вы узнали, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="04f5a-152">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="04f5a-153">Разверните поставщик ресурсов службы приложений</span><span class="sxs-lookup"><span data-stu-id="04f5a-153">Deploy the App Service resource provider</span></span>
> * <span data-ttu-id="04f5a-154">Создание предложения</span><span class="sxs-lookup"><span data-stu-id="04f5a-154">Create an offer</span></span>
> * <span data-ttu-id="04f5a-155">Тестирование предложение</span><span class="sxs-lookup"><span data-stu-id="04f5a-155">Test the offer</span></span>

<span data-ttu-id="04f5a-156">Переход к следующей учебника, чтобы узнать, как:</span><span class="sxs-lookup"><span data-stu-id="04f5a-156">Advance to the next tutorial to learn how to:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="04f5a-157">Развертывание приложений для Azure и Azure стека</span><span class="sxs-lookup"><span data-stu-id="04f5a-157">Deploy apps to Azure and Azure Stack</span></span>](azure-stack-solution-pipeline.md)
