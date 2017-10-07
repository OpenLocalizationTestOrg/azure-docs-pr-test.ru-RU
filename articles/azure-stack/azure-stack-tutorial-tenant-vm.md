---
title: "Доступные tooyour стека Azure aaaMake виртуальных машин пользователей | Документы Microsoft"
description: "Учебник toomake виртуальных машин на стек Azure"
services: azure-stack
documentationcenter: 
author: vhorne
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/22/2017
ms.author: victorh
ms.custom: mvc
ms.openlocfilehash: 345206912f17662e51341c71175c5fe87b692ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="make-virtual-machines-available-tooyour-azure-stack-users"></a><span data-ttu-id="be76c-103">Делает доступной tooyour виртуальных машин пользователей стек Azure</span><span class="sxs-lookup"><span data-stu-id="be76c-103">Make virtual machines available tooyour Azure Stack users</span></span>
<span data-ttu-id="be76c-104">Как администратор облака Azure стека можно создать пользователей (который иногда ссылается tooas клиентов) можно подписаться на предложения.</span><span class="sxs-lookup"><span data-stu-id="be76c-104">As an Azure Stack cloud administrator, you can create offers that your users (sometimes referred tooas tenants) can subscribe to.</span></span> <span data-ttu-id="be76c-105">С помощью подписки, пользователи смогут использовать службы Azure стека.</span><span class="sxs-lookup"><span data-stu-id="be76c-105">Using their subscription, users can then consume Azure Stack services.</span></span>

<span data-ttu-id="be76c-106">В этой статье показано, как toocreate в предложение, а затем проверить.</span><span class="sxs-lookup"><span data-stu-id="be76c-106">This article shows you how toocreate an offer, and then test it.</span></span> <span data-ttu-id="be76c-107">Для теста hello войдите в портал toohello имени пользователя, toohello предложения подписки и затем создать виртуальную машину с помощью подписки hello.</span><span class="sxs-lookup"><span data-stu-id="be76c-107">For hello test, you will log in toohello portal as a user, subscribe toohello offer, and then create a virtual machine using hello subscription.</span></span>

<span data-ttu-id="be76c-108">Обзор учебника:</span><span class="sxs-lookup"><span data-stu-id="be76c-108">What you will learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="be76c-109">Создание предложения</span><span class="sxs-lookup"><span data-stu-id="be76c-109">Create an offer</span></span>
> * <span data-ttu-id="be76c-110">Добавление изображения</span><span class="sxs-lookup"><span data-stu-id="be76c-110">Add an image</span></span>
> * <span data-ttu-id="be76c-111">Предложение hello теста</span><span class="sxs-lookup"><span data-stu-id="be76c-111">Test hello offer</span></span>


<span data-ttu-id="be76c-112">Стек Azure служб доставки toousers с помощью подписок, предложения и планы.</span><span class="sxs-lookup"><span data-stu-id="be76c-112">In Azure Stack, services are delivered toousers using subscriptions, offers, and plans.</span></span> <span data-ttu-id="be76c-113">Пользователи смогут подписаться toomultiple предложения.</span><span class="sxs-lookup"><span data-stu-id="be76c-113">Users can subscribe toomultiple offers.</span></span> <span data-ttu-id="be76c-114">В предложении может быть один или несколько планов, а в плане может быть одна или несколько служб.</span><span class="sxs-lookup"><span data-stu-id="be76c-114">Offers can have one or more plans, and plans can have one or more services.</span></span>

![Подписки, предложений и планов](media/azure-stack-key-features/image4.png)

<span data-ttu-id="be76c-116">toolearn более, в разделе [ключевые компоненты и основные понятия в стек Azure](azure-stack-key-features.md).</span><span class="sxs-lookup"><span data-stu-id="be76c-116">toolearn more, see [Key features and concepts in Azure Stack](azure-stack-key-features.md).</span></span>

## <a name="create-an-offer"></a><span data-ttu-id="be76c-117">Создание предложения</span><span class="sxs-lookup"><span data-stu-id="be76c-117">Create an offer</span></span>

<span data-ttu-id="be76c-118">Теперь вы можете использовать действия готова для пользователей.</span><span class="sxs-lookup"><span data-stu-id="be76c-118">Now you can get things ready for your users.</span></span> <span data-ttu-id="be76c-119">При запуске процесса hello, используется первый запрос toocreate hello предложение, а затем план и наконец квоты.</span><span class="sxs-lookup"><span data-stu-id="be76c-119">When you start hello process, you are first prompted toocreate hello offer, then a plan, and finally quotas.</span></span>

3. <span data-ttu-id="be76c-120">**Создание предложения**</span><span class="sxs-lookup"><span data-stu-id="be76c-120">**Create an offer**</span></span>

   <span data-ttu-id="be76c-121">Предложения представляют собой группы один или несколько планов, поставщики присутствует toousers toopurchase или подписаться.</span><span class="sxs-lookup"><span data-stu-id="be76c-121">Offers are groups of one or more plans that providers present toousers toopurchase or subscribe to.</span></span>

   <span data-ttu-id="be76c-122">а.</span><span class="sxs-lookup"><span data-stu-id="be76c-122">a.</span></span> <span data-ttu-id="be76c-123">[Войдите в](azure-stack-connect-azure-stack.md) toohello портал администратора облака и нажмите кнопку **New** > **клиента предлагает + планы** > **предлагают**.</span><span class="sxs-lookup"><span data-stu-id="be76c-123">[Sign in](azure-stack-connect-azure-stack.md) toohello portal as a cloud administrator and then click **New** > **Tenant Offers + Plans** > **Offer**.</span></span>
   <span data-ttu-id="be76c-124">![Новое предложение](media/azure-stack-tutorial-tenant-vm/image01.png)</span><span class="sxs-lookup"><span data-stu-id="be76c-124">![New offer](media/azure-stack-tutorial-tenant-vm/image01.png)</span></span>

   <span data-ttu-id="be76c-125">b.</span><span class="sxs-lookup"><span data-stu-id="be76c-125">b.</span></span> <span data-ttu-id="be76c-126">В hello **предлагают новый** статьи, заполните **отображаемое имя** и **имя ресурса**, а затем выберите новую или существующую **группы ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="be76c-126">In hello **New Offer** section, fill in **Display Name** and **Resource Name**, and then select a new or existing **Resource Group**.</span></span> <span data-ttu-id="be76c-127">Hello отображаемое имя — предложение hello понятное имя.</span><span class="sxs-lookup"><span data-stu-id="be76c-127">hello Display Name is hello offer's friendly name.</span></span> <span data-ttu-id="be76c-128">Только оператор hello облака можно увидеть hello имя ресурса.</span><span class="sxs-lookup"><span data-stu-id="be76c-128">Only hello cloud operator can see hello Resource Name.</span></span> <span data-ttu-id="be76c-129">Он является hello имя, "Администраторы" использовать toowork с hello предложения в качестве ресурса диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="be76c-129">It's hello name that admins use toowork with hello offer as an Azure Resource Manager resource.</span></span>

   ![Отображаемое имя](media/azure-stack-tutorial-tenant-vm/image02.png)

   <span data-ttu-id="be76c-131">c.</span><span class="sxs-lookup"><span data-stu-id="be76c-131">c.</span></span> <span data-ttu-id="be76c-132">Нажмите кнопку **базовые планы**и в hello **план** щелкните **добавить** tooadd новое предложение toohello плана.</span><span class="sxs-lookup"><span data-stu-id="be76c-132">Click **Base plans**, and in hello **Plan** section, click **Add** tooadd a new plan toohello offer.</span></span>

   ![Добавление плана](media/azure-stack-tutorial-tenant-vm/image03.png)

   <span data-ttu-id="be76c-134">d.</span><span class="sxs-lookup"><span data-stu-id="be76c-134">d.</span></span> <span data-ttu-id="be76c-135">В hello **создать план** статьи, заполните **отображаемое имя** и **имя ресурса**.</span><span class="sxs-lookup"><span data-stu-id="be76c-135">In hello **New Plan** section, fill in **Display Name** and **Resource Name**.</span></span> <span data-ttu-id="be76c-136">Hello отображаемое имя — hello плана понятное имя, которое будет отображаться для пользователей.</span><span class="sxs-lookup"><span data-stu-id="be76c-136">hello Display Name is hello plan's friendly name that users see.</span></span> <span data-ttu-id="be76c-137">Только оператор hello облака можно увидеть hello имя ресурса.</span><span class="sxs-lookup"><span data-stu-id="be76c-137">Only hello cloud operator can see hello Resource Name.</span></span> <span data-ttu-id="be76c-138">Hello имени, операторов облачных использования toowork с планом hello в качестве ресурса диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="be76c-138">It's hello name that cloud operators use toowork with hello plan as an Azure Resource Manager resource.</span></span>

   ![Отображаемое имя плана](media/azure-stack-tutorial-tenant-vm/image04.png)

   <span data-ttu-id="be76c-140">д.</span><span class="sxs-lookup"><span data-stu-id="be76c-140">e.</span></span> <span data-ttu-id="be76c-141">Нажмите кнопку **службы**выберите **Microsoft.Compute**, **Microsoft.Network**, и **хранилища Майкрософт**, а затем нажмите кнопку **Выберите**.</span><span class="sxs-lookup"><span data-stu-id="be76c-141">Click **Services**, select **Microsoft.Compute**, **Microsoft.Network**, and **Microsoft.Storage**, and then click **Select**.</span></span>

   ![Планирование служб](media/azure-stack-tutorial-tenant-vm/image05.png)

   <span data-ttu-id="be76c-143">f.</span><span class="sxs-lookup"><span data-stu-id="be76c-143">f.</span></span> <span data-ttu-id="be76c-144">Нажмите кнопку **квоты**, а затем выберите первую службу hello, для которого требуется toocreate квоты.</span><span class="sxs-lookup"><span data-stu-id="be76c-144">Click **Quotas**, and then select hello first service for which you want toocreate a quota.</span></span> <span data-ttu-id="be76c-145">Квоты IaaS выполните следующие действия для службы hello вычисления, сети и хранилища.</span><span class="sxs-lookup"><span data-stu-id="be76c-145">For an IaaS quota, follow these steps for hello Compute, Network, and Storage services.</span></span>

   <span data-ttu-id="be76c-146">В этом примере сначала создается квоты для службы вычислений hello.</span><span class="sxs-lookup"><span data-stu-id="be76c-146">In this example, we first create a quota for hello Compute service.</span></span> <span data-ttu-id="be76c-147">В списке имен hello выберите hello **Microsoft.Compute** пространство имен и нажмите кнопку **Создание новой квоте**.</span><span class="sxs-lookup"><span data-stu-id="be76c-147">In hello namespace list, select hello **Microsoft.Compute** namespace and then click **Create new quota**.</span></span>
   
   ![Создание новой квоты](media/azure-stack-tutorial-tenant-vm/image06.png)

   <span data-ttu-id="be76c-149">ж.</span><span class="sxs-lookup"><span data-stu-id="be76c-149">g.</span></span> <span data-ttu-id="be76c-150">На hello **создать квоту** статьи, введите имя для квоты hello и набор hello требуемые параметры для квот hello и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="be76c-150">On hello **Create quota** section, type a name for hello quota and set hello desired parameters for hello quota and click **OK**.</span></span>

   ![Имя квоты](media/azure-stack-tutorial-tenant-vm/image07.png)

   <span data-ttu-id="be76c-152">h.</span><span class="sxs-lookup"><span data-stu-id="be76c-152">h.</span></span> <span data-ttu-id="be76c-153">Теперь для **Microsoft.Compute**выберите hello квоты, созданный вами.</span><span class="sxs-lookup"><span data-stu-id="be76c-153">Now, for **Microsoft.Compute**, select hello quota that you created.</span></span>

   ![Выберите квоты](media/azure-stack-tutorial-tenant-vm/image08.png)

   <span data-ttu-id="be76c-155">Повторите эти шаги для hello сетевой службы и службы хранилища, а затем нажмите кнопку **ОК** на hello **квоты** раздела.</span><span class="sxs-lookup"><span data-stu-id="be76c-155">Repeat these steps for hello Network and Storage services, and then click **OK** on hello **Quotas** section.</span></span>

   <span data-ttu-id="be76c-156">i.</span><span class="sxs-lookup"><span data-stu-id="be76c-156">i.</span></span> <span data-ttu-id="be76c-157">Нажмите кнопку **ОК** на hello **новый план** раздела.</span><span class="sxs-lookup"><span data-stu-id="be76c-157">Click **OK** on hello **New plan** section.</span></span>

   <span data-ttu-id="be76c-158">j.</span><span class="sxs-lookup"><span data-stu-id="be76c-158">j.</span></span> <span data-ttu-id="be76c-159">На hello **план** выберите hello новый план и щелкните **выберите**.</span><span class="sxs-lookup"><span data-stu-id="be76c-159">On hello **Plan** section, select hello new plan and click **Select**.</span></span>

   <span data-ttu-id="be76c-160">k.</span><span class="sxs-lookup"><span data-stu-id="be76c-160">k.</span></span> <span data-ttu-id="be76c-161">На hello **новое предложение** щелкните **создать**.</span><span class="sxs-lookup"><span data-stu-id="be76c-161">On hello **New offer** section, click **Create**.</span></span> <span data-ttu-id="be76c-162">Вы видите уведомление при создании предложения hello.</span><span class="sxs-lookup"><span data-stu-id="be76c-162">You see a notification when hello offer has been created.</span></span>

   <span data-ttu-id="be76c-163">l.</span><span class="sxs-lookup"><span data-stu-id="be76c-163">l.</span></span> <span data-ttu-id="be76c-164">Пункт меню панели мониторинга hello, **предлагает** и выберите созданный предложение hello.</span><span class="sxs-lookup"><span data-stu-id="be76c-164">On hello dashboard menu, click **Offers** and then click hello offer you created.</span></span>

   <span data-ttu-id="be76c-165">m.</span><span class="sxs-lookup"><span data-stu-id="be76c-165">m.</span></span> <span data-ttu-id="be76c-166">Нажмите кнопку **изменению состояния**, а затем нажмите кнопку **открытый**.</span><span class="sxs-lookup"><span data-stu-id="be76c-166">Click **Change State**, and then click **Public**.</span></span>

   ![Общего состояния](media/azure-stack-tutorial-tenant-vm/image09.png)

## <a name="add-an-image"></a><span data-ttu-id="be76c-168">Добавление изображения</span><span class="sxs-lookup"><span data-stu-id="be76c-168">Add an image</span></span>

<span data-ttu-id="be76c-169">Перед последующей подготовки виртуальных машин, необходимо добавить изображение toohello стека Azure marketplace.</span><span class="sxs-lookup"><span data-stu-id="be76c-169">Before you can provision virtual machines, you must add an image toohello Azure Stack marketplace.</span></span> <span data-ttu-id="be76c-170">Можно добавить изображения hello по своему усмотрению, включая образы Linux из hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="be76c-170">You can add hello image of your choice, including Linux images, from hello Azure Marketplace.</span></span>

<span data-ttu-id="be76c-171">Если вы работаете в сценарии подключенных и если вы зарегистрировали экземпляра Azure стека с Azure, затем можно загрузить образ виртуальной Машины Windows Server 2016 hello из hello Azure Marketplace с помощью hello действия, описанные в hello [загрузки элементы Marketplace из Azure tooAzure стека](azure-stack-download-azure-marketplace-item.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="be76c-171">If you are operating in a connected scenario and if you have registered your Azure Stack instance with Azure, then you can download hello Windows Server 2016 VM image from hello Azure Marketplace by using hello steps described in hello [Download marketplace items from Azure tooAzure Stack](azure-stack-download-azure-marketplace-item.md) topic.</span></span>

<span data-ttu-id="be76c-172">Сведения о добавлении различных элементов toohello marketplace см. в разделе [hello Azure Marketplace стека](azure-stack-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="be76c-172">For information about adding different items toohello marketplace, see [hello Azure Stack Marketplace](azure-stack-marketplace.md).</span></span>

## <a name="test-hello-offer"></a><span data-ttu-id="be76c-173">Предложение hello теста</span><span class="sxs-lookup"><span data-stu-id="be76c-173">Test hello offer</span></span>

<span data-ttu-id="be76c-174">После создания предложения можно проверить его.</span><span class="sxs-lookup"><span data-stu-id="be76c-174">Now that you’ve created an offer, you can test it.</span></span> <span data-ttu-id="be76c-175">Войдите в систему как пользователь и подписываться toohello предложение, а затем добавить виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="be76c-175">Log in as a user and subscribe toohello offer and then add a virtual machine.</span></span>

1. <span data-ttu-id="be76c-176">**Подписаться на предложение tooan**</span><span class="sxs-lookup"><span data-stu-id="be76c-176">**Subscribe tooan offer**</span></span>

   <span data-ttu-id="be76c-177">Теперь вы можете войти портала toohello как предложение tooan toosubscribe пользователя.</span><span class="sxs-lookup"><span data-stu-id="be76c-177">Now you can log in toohello portal as a user toosubscribe tooan offer.</span></span>

   <span data-ttu-id="be76c-178">а.</span><span class="sxs-lookup"><span data-stu-id="be76c-178">a.</span></span> <span data-ttu-id="be76c-179">На компьютере комплект средств для развертывания Azure стека hello выполните вход слишком`https://portal.local.azurestack.external` пользователя и нажмите кнопку **получить подписку**.</span><span class="sxs-lookup"><span data-stu-id="be76c-179">On hello Azure Stack Deployment Kit computer, log in too`https://portal.local.azurestack.external` as a user and click **Get a Subscription**.</span></span>

   ![Получить подписку](media/azure-stack-subscribe-plan-provision-vm/image01.png)

   <span data-ttu-id="be76c-181">b.</span><span class="sxs-lookup"><span data-stu-id="be76c-181">b.</span></span> <span data-ttu-id="be76c-182">В hello **отображаемое имя** поле введите имя для вашей подписки, щелкните **предлагают**, выберите один из предложения hello в hello **выберите предложение** , а затем выберите **Создания**.</span><span class="sxs-lookup"><span data-stu-id="be76c-182">In hello **Display Name** field, type a name for your subscription, click **Offer**, click one of hello offers in hello **Choose an offer** section, and then click **Create**.</span></span>

   ![Создание предложения](media/azure-stack-subscribe-plan-provision-vm/image02.png)

   <span data-ttu-id="be76c-184">c.</span><span class="sxs-lookup"><span data-stu-id="be76c-184">c.</span></span> <span data-ttu-id="be76c-185">созданный tooview hello подписки, нажмите кнопку **дополнительные службы**, нажмите кнопку **подписки**, нажмите кнопку в новую подписку.</span><span class="sxs-lookup"><span data-stu-id="be76c-185">tooview hello subscription you created, click **More services**, click **Subscriptions**, then click your new subscription.</span></span>  

   <span data-ttu-id="be76c-186">После оформления подписки tooan предложение обновите hello портала toosee службы, которые являются частью hello новую подписку.</span><span class="sxs-lookup"><span data-stu-id="be76c-186">After you subscribe tooan offer, refresh hello portal toosee which services are part of hello new subscription.</span></span>

2. <span data-ttu-id="be76c-187">**Подготовка виртуальной машины**</span><span class="sxs-lookup"><span data-stu-id="be76c-187">**Provision a virtual machine**</span></span>

   <span data-ttu-id="be76c-188">Теперь вы можете войти портала toohello как tooprovision пользователя виртуальной машины с помощью подписки hello.</span><span class="sxs-lookup"><span data-stu-id="be76c-188">Now you can log in toohello portal as a user tooprovision a virtual machine using hello subscription.</span></span> 

   <span data-ttu-id="be76c-189">а.</span><span class="sxs-lookup"><span data-stu-id="be76c-189">a.</span></span> <span data-ttu-id="be76c-190">На компьютере комплект средств для развертывания Azure стека hello выполните вход слишком`https://portal.local.azurestack.external` как пользователя, а затем щелкните **New** > **вычислений** > **Windows Server 2016 Datacenter Eval**.</span><span class="sxs-lookup"><span data-stu-id="be76c-190">On hello Azure Stack Deployment Kit computer, log in too`https://portal.local.azurestack.external` as a user, and then click **New** > **Compute** > **Windows Server 2016 Datacenter Eval**.</span></span>  

   <span data-ttu-id="be76c-191">b.</span><span class="sxs-lookup"><span data-stu-id="be76c-191">b.</span></span> <span data-ttu-id="be76c-192">В hello **основы** введите **имя**, **имя пользователя**, и **пароль**.</span><span class="sxs-lookup"><span data-stu-id="be76c-192">In hello **Basics** section, type a **Name**, **User name**, and **Password**.</span></span> <span data-ttu-id="be76c-193">Для **тип диска виртуальной Машины**, выберите **HDD**.</span><span class="sxs-lookup"><span data-stu-id="be76c-193">For **VM disk type**, choose **HDD**.</span></span> <span data-ttu-id="be76c-194">Выберите **подписку**.</span><span class="sxs-lookup"><span data-stu-id="be76c-194">Choose a **Subscription**.</span></span> <span data-ttu-id="be76c-195">Создание **группы ресурсов**, или выберите существующий и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="be76c-195">Create a **Resource group**, or select an existing one, and then click **OK**.</span></span>  

   <span data-ttu-id="be76c-196">c.</span><span class="sxs-lookup"><span data-stu-id="be76c-196">c.</span></span> <span data-ttu-id="be76c-197">В hello **выберите размер** щелкните **A1 основные**, а затем нажмите кнопку **выберите**.</span><span class="sxs-lookup"><span data-stu-id="be76c-197">In hello **Choose a size** section, click **A1 Basic**, and then click **Select**.</span></span>  

   <span data-ttu-id="be76c-198">d.</span><span class="sxs-lookup"><span data-stu-id="be76c-198">d.</span></span> <span data-ttu-id="be76c-199">В hello **параметры** щелкните **виртуальная сеть**.</span><span class="sxs-lookup"><span data-stu-id="be76c-199">In hello **Settings** section, click **Virtual network**.</span></span> <span data-ttu-id="be76c-200">В hello **виртуальной сети выберите** щелкните **создать новый**.</span><span class="sxs-lookup"><span data-stu-id="be76c-200">In hello **Choose virtual network** section, click **Create new**.</span></span> <span data-ttu-id="be76c-201">В hello **Создание виртуальной сети** статьи, примите все значения по умолчанию hello и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="be76c-201">In hello **Create virtual network** section, accept all hello defaults, and click **OK**.</span></span> <span data-ttu-id="be76c-202">В hello **параметры** щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="be76c-202">In hello **Settings** section, click **OK**.</span></span>

   ![Создание виртуальной сети](media/azure-stack-provision-vm/image04.png)

   <span data-ttu-id="be76c-204">д.</span><span class="sxs-lookup"><span data-stu-id="be76c-204">e.</span></span> <span data-ttu-id="be76c-205">В hello **Сводка** щелкните **ОК** toocreate hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="be76c-205">In hello **Summary** section, click **OK** toocreate hello virtual machine.</span></span>  

   <span data-ttu-id="be76c-206">f.</span><span class="sxs-lookup"><span data-stu-id="be76c-206">f.</span></span> <span data-ttu-id="be76c-207">toosee новой виртуальной машины, нажмите кнопку **все ресурсы**, а затем найдите hello виртуальную машину и щелкните ее имя.</span><span class="sxs-lookup"><span data-stu-id="be76c-207">toosee your new virtual machine, click **All resources**, then search for hello virtual machine and click its name.</span></span>

    ![Все ресурсы](media/azure-stack-provision-vm/image06.png)

<span data-ttu-id="be76c-209">Знания в этом учебнике:</span><span class="sxs-lookup"><span data-stu-id="be76c-209">What you learned in this tutorial:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="be76c-210">Создание предложения</span><span class="sxs-lookup"><span data-stu-id="be76c-210">Create an offer</span></span>
> * <span data-ttu-id="be76c-211">Добавление изображения</span><span class="sxs-lookup"><span data-stu-id="be76c-211">Add an image</span></span>
> * <span data-ttu-id="be76c-212">Предложение hello теста</span><span class="sxs-lookup"><span data-stu-id="be76c-212">Test hello offer</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="be76c-213">Сделать веб, мобильных устройств и пользователей стек Azure доступны tooyour приложения API</span><span class="sxs-lookup"><span data-stu-id="be76c-213">Make web, mobile, and API apps available tooyour Azure Stack users</span></span>](azure-stack-tutorial-app-service.md)
