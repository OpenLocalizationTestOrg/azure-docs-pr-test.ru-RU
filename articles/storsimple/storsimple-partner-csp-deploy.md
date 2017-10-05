---
title: "Обзор Microsoft Azure StorSimple и программы поставщика облачных решений | Документация Майкрософт"
description: "Общие сведения о StorSimple и CSP для партнеров StorSimple."
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
ms.openlocfilehash: c8cb51093142146fc7d43b51a62d949f6cc38988
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-storsimple-virtual-array-for-cloud-solution-provider-program"></a><span data-ttu-id="3fba5-103">Развертывание виртуального массива StorSimple для программы поставщика облачных решений</span><span class="sxs-lookup"><span data-stu-id="3fba5-103">Deploy StorSimple Virtual Array for Cloud Solution Provider Program</span></span>

## <a name="overview"></a><span data-ttu-id="3fba5-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="3fba5-104">Overview</span></span>

<span data-ttu-id="3fba5-105">Партнеры поставщика облачных решений (CSP) могут развернуть виртуальный массив StorSimple для своих клиентов.</span><span class="sxs-lookup"><span data-stu-id="3fba5-105">StorSimple Virtual Array can be deployed by the Cloud Solution Provider (CSP) partners for their customers.</span></span> <span data-ttu-id="3fba5-106">Партнер CSP может создать службу диспетчера устройств StorSimple.</span><span class="sxs-lookup"><span data-stu-id="3fba5-106">A CSP partner can create a StorSimple Device Manager service.</span></span> <span data-ttu-id="3fba5-107">Эта служба затем используется для развертывания виртуального массива StorSimple и связанных общих папок, томов и резервных копий и управления ими.</span><span class="sxs-lookup"><span data-stu-id="3fba5-107">This service can then be used to deploy and manage StorSimple Virtual Array and the associated shares, volumes, and backups.</span></span>

<span data-ttu-id="3fba5-108">В этой статье описывается, как партнер CSP может добавить клиента или новую подписку имеющегося клиента, а затем создать службу для развертывания виртуального массива StorSimple в CSP.</span><span class="sxs-lookup"><span data-stu-id="3fba5-108">This article describes how a CSP partner can add a customer or a new subscription to an existing customer and then create a service to deploy a StorSimple Virtual Array in CSP.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3fba5-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3fba5-109">Prerequisites</span></span>

<span data-ttu-id="3fba5-110">Перед началом работы убедитесь, что выполнены следующие условия:</span><span class="sxs-lookup"><span data-stu-id="3fba5-110">Before you begin, ensure that:</span></span>

- <span data-ttu-id="3fba5-111">Вы зарегистрированы в программе CSP.</span><span class="sxs-lookup"><span data-stu-id="3fba5-111">You are enrolled under the CSP program.</span></span>
- <span data-ttu-id="3fba5-112">У вас есть допустимые учетные данные для входа в [Центр партнеров](http://partnercenter.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="3fba5-112">You have valid [Partner Center](http://partnercenter.microsoft.com/) login credentials.</span></span> <span data-ttu-id="3fba5-113">Учетные данные позволяют выполнять вход на портал партнеров, чтобы добавлять новых клиентов, искать клиентов или переходить в учетную запись клиента с панели мониторинга партнеров.</span><span class="sxs-lookup"><span data-stu-id="3fba5-113">The credentials enable you to sign in to the Partner portal to add new customers, search for customers, or navigate to a customer account from the Partner dashboard.</span></span> <span data-ttu-id="3fba5-114">CSP может работать как администратор StorSimple от имени клиента на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="3fba5-114">The CSP can function as a StorSimple administrator on behalf of the customer in the Azure portal.</span></span>
                             
## <a name="add-a-customer"></a><span data-ttu-id="3fba5-115">Добавление клиента</span><span class="sxs-lookup"><span data-stu-id="3fba5-115">Add a customer</span></span>

<span data-ttu-id="3fba5-116">При добавлении клиента автоматически создается подписка.</span><span class="sxs-lookup"><span data-stu-id="3fba5-116">If you add a customer, a subscription is automatically created.</span></span> <span data-ttu-id="3fba5-117">Чтобы добавить клиента (и автоматически создать подписку), на портале партнеров сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="3fba5-117">To add a customer (and automatically create a subscription), perform the following steps in the Partner portal.</span></span>

1. <span data-ttu-id="3fba5-118">Перейдите в [Центр партнеров](http://partnercenter.microsoft.com/) и выполните вход с использованием учетных данных CSP.</span><span class="sxs-lookup"><span data-stu-id="3fba5-118">Go to the [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span></span> <span data-ttu-id="3fba5-119">Нажмите на кнопку **Панель мониторинга**.</span><span class="sxs-lookup"><span data-stu-id="3fba5-119">Click **Dashboard**.</span></span>

     ![Панель мониторинга в Центре партнеров](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. <span data-ttu-id="3fba5-121">В левой области щелкните **Клиенты**.</span><span class="sxs-lookup"><span data-stu-id="3fba5-121">In the left-pane, click **Customers**.</span></span> <span data-ttu-id="3fba5-122">В правой области щелкните **Добавить клиентов**.</span><span class="sxs-lookup"><span data-stu-id="3fba5-122">In the right-pane, click **Add customers**.</span></span> <span data-ttu-id="3fba5-123">Введите сведения о клиенте.</span><span class="sxs-lookup"><span data-stu-id="3fba5-123">Enter the details of the customer.</span></span> <span data-ttu-id="3fba5-124">Щелкните **Далее: подписки**, чтобы создать подписку клиента.</span><span class="sxs-lookup"><span data-stu-id="3fba5-124">Click **Next: Subscriptions** to create a customer subscription.</span></span>

    ![Добавление клиента](./media/storsimple-partner-csp-deploy/image2.png)

3.  <span data-ttu-id="3fba5-126">Выберите предложение **Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="3fba5-126">Select **Microsoft Azure** offer.</span></span> <span data-ttu-id="3fba5-127">Прокрутите к нижней части страницы и щелкните **Просмотр**.</span><span class="sxs-lookup"><span data-stu-id="3fba5-127">Scroll to the bottom of the page and click **Review**.</span></span>

    ![Просмотр сведений о подписке](./media/storsimple-partner-csp-deploy/image3.png)
                              
4. <span data-ttu-id="3fba5-129">Проверьте данные и нажмите кнопку **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="3fba5-129">Review the information and click **Submit**.</span></span>

    ![Отправка подписки](./media/storsimple-partner-csp-deploy/image4.png)

5. <span data-ttu-id="3fba5-131">Сохраните сведения о подтверждении для дальнейшего использования.</span><span class="sxs-lookup"><span data-stu-id="3fba5-131">Save the confirmation information for future reference.</span></span>

    ![Сохранение подтверждения](./media/storsimple-partner-csp-deploy/image5.png)

6. <span data-ttu-id="3fba5-133">Найдите только что добавленного клиента или перейдите к нему.</span><span class="sxs-lookup"><span data-stu-id="3fba5-133">Find or navigate to the customer you just added.</span></span> <span data-ttu-id="3fba5-134">Щелкните **Название компании**, чтобы получить подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="3fba5-134">Click the **Company name** to drill down into the details.</span></span>

    ![Поиск клиента](./media/storsimple-partner-csp-deploy/image6.png)  

7. <span data-ttu-id="3fba5-136">В левой области выберите **Управление службой**.</span><span class="sxs-lookup"><span data-stu-id="3fba5-136">In the left-pane, select **Service management**.</span></span> <span data-ttu-id="3fba5-137">В правой области в разделе **Администрирование служб** щелкните **Портал управления Microsoft Azure**, чтобы войти в систему в качестве администратора Azure для вашего клиента.</span><span class="sxs-lookup"><span data-stu-id="3fba5-137">In the right-pane, under **Administer services**, click **Microsoft Azure Management Portal** to sign in as an Azure administrator for your customer.</span></span>

    ![Вход на портал Azure](./media/storsimple-partner-csp-deploy/image9.png)

8. <span data-ttu-id="3fba5-139">Чтобы создать диспетчер устройств StorSimple, выберите **+ Создать** и найдите элемент **Серия виртуального устройства StorSimple** или перейдите к нему.</span><span class="sxs-lookup"><span data-stu-id="3fba5-139">To create a StorSimple Device Manager, click **+ New** and search for or navigate to **StorSimple Virtual Device Series**.</span></span> <span data-ttu-id="3fba5-140">Дополнительные сведения см. в статье [Развертывание службы диспетчера устройств StorSimple для виртуального массива StorSimple](storsimple-virtual-array-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="3fba5-140">For more information, go to [Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span></span>

    ![Создание службы диспетчера устройств StorSimple](./media/storsimple-partner-csp-deploy/image8.png)


## <a name="add-a-subscription"></a><span data-ttu-id="3fba5-142">Добавление подписки</span><span class="sxs-lookup"><span data-stu-id="3fba5-142">Add a subscription</span></span>

<span data-ttu-id="3fba5-143">В некоторых случаях, когда у вас уже есть клиент, вам может понадобиться добавить подписку.</span><span class="sxs-lookup"><span data-stu-id="3fba5-143">In some instances, you may have an existing customer, and you need to add a subscription.</span></span> <span data-ttu-id="3fba5-144">Чтобы добавить подписку для имеющегося клиента, на портале партнеров сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="3fba5-144">To add a subscription to an existing customer, perform the following steps in the Partner portal.</span></span>

1. <span data-ttu-id="3fba5-145">Перейдите в [Центр партнеров](http://partnercenter.microsoft.com/) и выполните вход с использованием учетных данных CSP.</span><span class="sxs-lookup"><span data-stu-id="3fba5-145">Go to the [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span></span> <span data-ttu-id="3fba5-146">Нажмите на кнопку **Панель мониторинга**.</span><span class="sxs-lookup"><span data-stu-id="3fba5-146">Click **Dashboard**.</span></span>

     ![Панель мониторинга в Центре партнеров](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. <span data-ttu-id="3fba5-148">В левой области щелкните **Клиенты**.</span><span class="sxs-lookup"><span data-stu-id="3fba5-148">In the left-pane, click **Customers**.</span></span> <span data-ttu-id="3fba5-149">Найдите клиента, для которого требуется добавить подписку, или перейдите к нему.</span><span class="sxs-lookup"><span data-stu-id="3fba5-149">Find or navigate to the customer you want to add a subscription to.</span></span> <span data-ttu-id="3fba5-150">Щелкните значок ![значок галочки развертывания](./media/storsimple-partner-csp-deploy/expand_pane_icon.png), чтобы развернуть строку имени компании для клиента.</span><span class="sxs-lookup"><span data-stu-id="3fba5-150">Click the ![Expand check icon](./media/storsimple-partner-csp-deploy/expand_pane_icon.png) icon to expand the row for the company name for your customer.</span></span> <span data-ttu-id="3fba5-151">В области сведений щелкните **Добавить подписки**.</span><span class="sxs-lookup"><span data-stu-id="3fba5-151">In the details, click **Add subscriptions**.</span></span>

    ![Клиенты](./media/storsimple-partner-csp-deploy/image10.png)

3. <span data-ttu-id="3fba5-153">Проверьте **Microsoft Azure** на наличие лучших предложений в разделе **Лучшие предложения** в подписку и нажмите кнопку **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="3fba5-153">Check **Microsoft Azure** for the **Top offers** in the subscription and click **Submit**.</span></span> <span data-ttu-id="3fba5-154">После этого будет создана подписка.</span><span class="sxs-lookup"><span data-stu-id="3fba5-154">This creates a new subscription.</span></span>

    ![Добавление новой подписки](./media/storsimple-partner-csp-deploy/image11.png)

6. <span data-ttu-id="3fba5-156">После создания подписки щелкните **<-- Клиенты** в области слева, чтобы вернуться на страницу **Клиенты**.</span><span class="sxs-lookup"><span data-stu-id="3fba5-156">After a new subscription is created, click **<-- Customers** in the left-pane to return to the **Customers** page.</span></span> <span data-ttu-id="3fba5-157">Найдите клиента, для которого только что создали подписку.</span><span class="sxs-lookup"><span data-stu-id="3fba5-157">Search for the customer for whom you just created a subscription.</span></span> <span data-ttu-id="3fba5-158">Щелкните **Название компании**, чтобы получить подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="3fba5-158">Click the **Company name** to drill down into the details.</span></span>

    ![Поиск клиента](./media/storsimple-partner-csp-deploy/image6.png)  

7. <span data-ttu-id="3fba5-160">В левой области выберите **Управление службой**.</span><span class="sxs-lookup"><span data-stu-id="3fba5-160">In the left-pane, select **Service management**.</span></span> <span data-ttu-id="3fba5-161">В правой области в разделе **Администрирование служб** щелкните **Портал управления Microsoft Azure**, чтобы войти в систему в качестве администратора Azure для вашего клиента.</span><span class="sxs-lookup"><span data-stu-id="3fba5-161">In the right-pane, under **Administer services**, click **Microsoft Azure Management Portal** to sign in as an Azure administrator for your customer.</span></span>

    ![Вход на портал Azure](./media/storsimple-partner-csp-deploy/image9.png)

8. <span data-ttu-id="3fba5-163">Чтобы создать диспетчер устройств StorSimple, выберите **+ Создать** и найдите элемент **Серия виртуального устройства StorSimple** или перейдите к нему.</span><span class="sxs-lookup"><span data-stu-id="3fba5-163">To create a StorSimple Device Manager, click **+ New** and search for or navigate to **StorSimple Virtual Device Series**.</span></span> <span data-ttu-id="3fba5-164">Дополнительные сведения см. в статье [Развертывание службы диспетчера устройств StorSimple для виртуального массива StorSimple](storsimple-virtual-array-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="3fba5-164">For more information, go to [Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span></span>

    ![Создание службы диспетчера устройств StorSimple](./media/storsimple-partner-csp-deploy/image8.png)

## <a name="next-steps"></a><span data-ttu-id="3fba5-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3fba5-166">Next steps</span></span>

- <span data-ttu-id="3fba5-167">Если у вас есть дополнительные вопросы о StorSimple в CSP, перейдите к статье [StorSimple in CSP: Frequently asked questions](storsimple-partner-csp-faq.md) (StorSimple в CSP: часто задаваемые вопросы).</span><span class="sxs-lookup"><span data-stu-id="3fba5-167">If you have more questions regarding the StorSimple in CSP, go to [StorSimple in CSP: Frequently asked questions](storsimple-partner-csp-faq.md).</span></span>
- <span data-ttu-id="3fba5-168">Если вы уже готовы развернуть StorSimple, перейдите к статье [Развертывание виртуального массива StorSimple для программы поставщика облачных решений](storsimple-partner-csp-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="3fba5-168">If you are ready to deploy your StorSimple, go to [Deploy your StorSimple in CSP](storsimple-partner-csp-deploy.md).</span></span>
