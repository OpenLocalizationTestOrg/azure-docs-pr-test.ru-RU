---
title: "aaaMicrosoft Azure StorSimple и обзор программы поставщика облачных решений | Документы Microsoft"
description: "Общие сведения о hello StorSimple и CSP для партнеров StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/08/2017
ms.author: alkohli
ms.openlocfilehash: b5d999f2fbb9a27e7404ff454957b29dbef56af6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array-for-cloud-solution-provider-program"></a><span data-ttu-id="66a86-103">Развертывание виртуального массива StorSimple для программы поставщика облачных решений</span><span class="sxs-lookup"><span data-stu-id="66a86-103">Deploy StorSimple Virtual Array for Cloud Solution Provider Program</span></span>

## <a name="overview"></a><span data-ttu-id="66a86-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="66a86-104">Overview</span></span>

<span data-ttu-id="66a86-105">Можно развернуть StorSimple Virtual Array hello партнеры поставщика облачных решений (CSP) для своих клиентов.</span><span class="sxs-lookup"><span data-stu-id="66a86-105">StorSimple Virtual Array can be deployed by hello Cloud Solution Provider (CSP) partners for their customers.</span></span> <span data-ttu-id="66a86-106">Партнер CSP может создать службу диспетчера устройств StorSimple.</span><span class="sxs-lookup"><span data-stu-id="66a86-106">A CSP partner can create a StorSimple Device Manager service.</span></span> <span data-ttu-id="66a86-107">Эту службу можно использовать toodeploy и управление StorSimple Virtual Array и hello связанных общих папок, томов и резервных копий.</span><span class="sxs-lookup"><span data-stu-id="66a86-107">This service can then be used toodeploy and manage StorSimple Virtual Array and hello associated shares, volumes, and backups.</span></span>

<span data-ttu-id="66a86-108">В этой статье описывается, как можно добавить клиента или нового клиента существующие подписки tooan CSP партнера, а затем создать toodeploy службы StorSimple Virtual Array в CSP.</span><span class="sxs-lookup"><span data-stu-id="66a86-108">This article describes how a CSP partner can add a customer or a new subscription tooan existing customer and then create a service toodeploy a StorSimple Virtual Array in CSP.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66a86-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="66a86-109">Prerequisites</span></span>

<span data-ttu-id="66a86-110">Перед началом работы убедитесь, что выполнены следующие условия:</span><span class="sxs-lookup"><span data-stu-id="66a86-110">Before you begin, ensure that:</span></span>

- <span data-ttu-id="66a86-111">Вы зарегистрированы в рамках программы hello CSP.</span><span class="sxs-lookup"><span data-stu-id="66a86-111">You are enrolled under hello CSP program.</span></span>
- <span data-ttu-id="66a86-112">У вас есть допустимые учетные данные для входа в [Центр партнеров](http://partnercenter.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="66a86-112">You have valid [Partner Center](http://partnercenter.microsoft.com/) login credentials.</span></span> <span data-ttu-id="66a86-113">Hello учетные данные позволяют toosign toohello партнера портала tooadd клиентов, искать клиентов или перейдите tooa учетной записи клиента из hello мониторинга для партнеров.</span><span class="sxs-lookup"><span data-stu-id="66a86-113">hello credentials enable you toosign in toohello Partner portal tooadd new customers, search for customers, or navigate tooa customer account from hello Partner dashboard.</span></span> <span data-ttu-id="66a86-114">Hello CSP могут функционировать как администратор StorSimple от имени клиента hello в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="66a86-114">hello CSP can function as a StorSimple administrator on behalf of hello customer in hello Azure portal.</span></span>
                             
## <a name="add-a-customer"></a><span data-ttu-id="66a86-115">Добавление клиента</span><span class="sxs-lookup"><span data-stu-id="66a86-115">Add a customer</span></span>

<span data-ttu-id="66a86-116">При добавлении клиента автоматически создается подписка.</span><span class="sxs-lookup"><span data-stu-id="66a86-116">If you add a customer, a subscription is automatically created.</span></span> <span data-ttu-id="66a86-117">tooadd клиента (и автоматически создавать подписки), выполните следующие действия на портале партнера hello hello.</span><span class="sxs-lookup"><span data-stu-id="66a86-117">tooadd a customer (and automatically create a subscription), perform hello following steps in hello Partner portal.</span></span>

1. <span data-ttu-id="66a86-118">Go toohello [партнерском центре](http://partnercenter.microsoft.com/) и войдите с использованием учетных данных поставщика служб Шифрования.</span><span class="sxs-lookup"><span data-stu-id="66a86-118">Go toohello [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span></span> <span data-ttu-id="66a86-119">Нажмите на кнопку **Панель мониторинга**.</span><span class="sxs-lookup"><span data-stu-id="66a86-119">Click **Dashboard**.</span></span>

     ![Панель мониторинга в Центре партнеров](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. <span data-ttu-id="66a86-121">В hello левой панели щелкните **клиентов**.</span><span class="sxs-lookup"><span data-stu-id="66a86-121">In hello left-pane, click **Customers**.</span></span> <span data-ttu-id="66a86-122">В hello на правой панели щелкните **добавить клиентов**.</span><span class="sxs-lookup"><span data-stu-id="66a86-122">In hello right-pane, click **Add customers**.</span></span> <span data-ttu-id="66a86-123">Введите сведения о hello hello клиента.</span><span class="sxs-lookup"><span data-stu-id="66a86-123">Enter hello details of hello customer.</span></span> <span data-ttu-id="66a86-124">Нажмите кнопку **далее: подписки** toocreate подписки клиента.</span><span class="sxs-lookup"><span data-stu-id="66a86-124">Click **Next: Subscriptions** toocreate a customer subscription.</span></span>

    ![Добавление клиента](./media/storsimple-partner-csp-deploy/image2.png)

3.  <span data-ttu-id="66a86-126">Выберите предложение **Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="66a86-126">Select **Microsoft Azure** offer.</span></span> <span data-ttu-id="66a86-127">Scroll toohello нижней части страницы приветствия и нажмите кнопку **проверки**.</span><span class="sxs-lookup"><span data-stu-id="66a86-127">Scroll toohello bottom of hello page and click **Review**.</span></span>

    ![Просмотр сведений о подписке](./media/storsimple-partner-csp-deploy/image3.png)
                              
4. <span data-ttu-id="66a86-129">Просмотрите сведения hello и нажмите кнопку **отправить**.</span><span class="sxs-lookup"><span data-stu-id="66a86-129">Review hello information and click **Submit**.</span></span>

    ![Отправка подписки](./media/storsimple-partner-csp-deploy/image4.png)

5. <span data-ttu-id="66a86-131">Сохраните сведения о подтверждении hello для дальнейшего использования.</span><span class="sxs-lookup"><span data-stu-id="66a86-131">Save hello confirmation information for future reference.</span></span>

    ![Сохранение подтверждения](./media/storsimple-partner-csp-deploy/image5.png)

6. <span data-ttu-id="66a86-133">Найдите или перейдите toohello клиента, для которого был только что добавлен.</span><span class="sxs-lookup"><span data-stu-id="66a86-133">Find or navigate toohello customer you just added.</span></span> <span data-ttu-id="66a86-134">Нажмите кнопку hello **название компании** toodrill работу в детали hello.</span><span class="sxs-lookup"><span data-stu-id="66a86-134">Click hello **Company name** toodrill down into hello details.</span></span>

    ![Поиск приветствия клиента](./media/storsimple-partner-csp-deploy/image6.png)  

7. <span data-ttu-id="66a86-136">В hello левой панели выберите **управление службой**.</span><span class="sxs-lookup"><span data-stu-id="66a86-136">In hello left-pane, select **Service management**.</span></span> <span data-ttu-id="66a86-137">В hello на правой панели в разделе **администрировать службы**, нажмите кнопку **Microsoft Azure Management Portal** toosign в Azure администратору клиента.</span><span class="sxs-lookup"><span data-stu-id="66a86-137">In hello right-pane, under **Administer services**, click **Microsoft Azure Management Portal** toosign in as an Azure administrator for your customer.</span></span>

    ![Войдите в портал tooAzure](./media/storsimple-partner-csp-deploy/image9.png)

8. <span data-ttu-id="66a86-139">Щелкните toocreate диспетчера устройств StorSimple, **+ создать** и поиска или перехода слишком**серией виртуальных устройств StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="66a86-139">toocreate a StorSimple Device Manager, click **+ New** and search for or navigate too**StorSimple Virtual Device Series**.</span></span> <span data-ttu-id="66a86-140">Дополнительные сведения см. слишком[развертывание службы диспетчера StorSimple устройство](storsimple-virtual-array-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="66a86-140">For more information, go too[Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span></span>

    ![Создание службы диспетчера устройств StorSimple](./media/storsimple-partner-csp-deploy/image8.png)


## <a name="add-a-subscription"></a><span data-ttu-id="66a86-142">Добавление подписки</span><span class="sxs-lookup"><span data-stu-id="66a86-142">Add a subscription</span></span>

<span data-ttu-id="66a86-143">В некоторых случаях может быть существующим клиентом, и требуется, чтобы tooadd подписки.</span><span class="sxs-lookup"><span data-stu-id="66a86-143">In some instances, you may have an existing customer, and you need tooadd a subscription.</span></span> <span data-ttu-id="66a86-144">tooadd tooan существующий клиент подписки, выполнить следующие шаги на портале партнера hello hello.</span><span class="sxs-lookup"><span data-stu-id="66a86-144">tooadd a subscription tooan existing customer, perform hello following steps in hello Partner portal.</span></span>

1. <span data-ttu-id="66a86-145">Go toohello [партнерском центре](http://partnercenter.microsoft.com/) и войдите с использованием учетных данных поставщика служб Шифрования.</span><span class="sxs-lookup"><span data-stu-id="66a86-145">Go toohello [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span></span> <span data-ttu-id="66a86-146">Нажмите на кнопку **Панель мониторинга**.</span><span class="sxs-lookup"><span data-stu-id="66a86-146">Click **Dashboard**.</span></span>

     ![Панель мониторинга в Центре партнеров](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. <span data-ttu-id="66a86-148">В hello левой панели щелкните **клиентов**.</span><span class="sxs-lookup"><span data-stu-id="66a86-148">In hello left-pane, click **Customers**.</span></span> <span data-ttu-id="66a86-149">Найдите или перейдите toohello клиента, для которого требуется задать подписку на tooadd.</span><span class="sxs-lookup"><span data-stu-id="66a86-149">Find or navigate toohello customer you want tooadd a subscription to.</span></span> <span data-ttu-id="66a86-150">Нажмите кнопку hello ![значок проверки развертывания](./media/storsimple-partner-csp-deploy/expand_pane_icon.png) строку hello tooexpand значок для hello название компании для вашего клиента.</span><span class="sxs-lookup"><span data-stu-id="66a86-150">Click hello ![Expand check icon](./media/storsimple-partner-csp-deploy/expand_pane_icon.png) icon tooexpand hello row for hello company name for your customer.</span></span> <span data-ttu-id="66a86-151">В сведениях о hello, нажмите кнопку **добавить подписки**.</span><span class="sxs-lookup"><span data-stu-id="66a86-151">In hello details, click **Add subscriptions**.</span></span>

    ![Клиенты](./media/storsimple-partner-csp-deploy/image10.png)

3. <span data-ttu-id="66a86-153">Проверьте **Microsoft Azure** для hello **предложения Top** в hello подписки и нажмите кнопку **отправить**.</span><span class="sxs-lookup"><span data-stu-id="66a86-153">Check **Microsoft Azure** for hello **Top offers** in hello subscription and click **Submit**.</span></span> <span data-ttu-id="66a86-154">После этого будет создана подписка.</span><span class="sxs-lookup"><span data-stu-id="66a86-154">This creates a new subscription.</span></span>

    ![Добавление новой подписки](./media/storsimple-partner-csp-deploy/image11.png)

6. <span data-ttu-id="66a86-156">После создания новой подписки щелкните **<--клиентов** в левой области tooreturn toohello hello **клиентов** страницы.</span><span class="sxs-lookup"><span data-stu-id="66a86-156">After a new subscription is created, click **<-- Customers** in hello left-pane tooreturn toohello **Customers** page.</span></span> <span data-ttu-id="66a86-157">Поиск hello клиента, для которого вы только что создали подписки.</span><span class="sxs-lookup"><span data-stu-id="66a86-157">Search for hello customer for whom you just created a subscription.</span></span> <span data-ttu-id="66a86-158">Нажмите кнопку hello **название компании** toodrill работу в детали hello.</span><span class="sxs-lookup"><span data-stu-id="66a86-158">Click hello **Company name** toodrill down into hello details.</span></span>

    ![Поиск приветствия клиента](./media/storsimple-partner-csp-deploy/image6.png)  

7. <span data-ttu-id="66a86-160">В hello левой панели выберите **управление службой**.</span><span class="sxs-lookup"><span data-stu-id="66a86-160">In hello left-pane, select **Service management**.</span></span> <span data-ttu-id="66a86-161">В hello на правой панели в разделе **администрировать службы**, нажмите кнопку **Microsoft Azure Management Portal** toosign в Azure администратору клиента.</span><span class="sxs-lookup"><span data-stu-id="66a86-161">In hello right-pane, under **Administer services**, click **Microsoft Azure Management Portal** toosign in as an Azure administrator for your customer.</span></span>

    ![Войдите в портал tooAzure](./media/storsimple-partner-csp-deploy/image9.png)

8. <span data-ttu-id="66a86-163">Щелкните toocreate диспетчера устройств StorSimple, **+ создать** и поиска или перехода слишком**серией виртуальных устройств StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="66a86-163">toocreate a StorSimple Device Manager, click **+ New** and search for or navigate too**StorSimple Virtual Device Series**.</span></span> <span data-ttu-id="66a86-164">Дополнительные сведения см. слишком[развертывание службы диспетчера StorSimple устройство](storsimple-virtual-array-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="66a86-164">For more information, go too[Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span></span>

    ![Создание службы диспетчера устройств StorSimple](./media/storsimple-partner-csp-deploy/image8.png)

## <a name="next-steps"></a><span data-ttu-id="66a86-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="66a86-166">Next steps</span></span>

- <span data-ttu-id="66a86-167">Если у вас есть дополнительные вопросы о hello StorSimple CSP, перейдите в слишком[StorSimple в CSP: часто задаваемые вопросы](storsimple-partner-csp-faq.md).</span><span class="sxs-lookup"><span data-stu-id="66a86-167">If you have more questions regarding hello StorSimple in CSP, go too[StorSimple in CSP: Frequently asked questions](storsimple-partner-csp-faq.md).</span></span>
- <span data-ttu-id="66a86-168">В случае готовности toodeploy StorSimple, go слишком[развертывания StorSimple в CSP](storsimple-partner-csp-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="66a86-168">If you are ready toodeploy your StorSimple, go too[Deploy your StorSimple in CSP](storsimple-partner-csp-deploy.md).</span></span>
