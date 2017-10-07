---
title: "aaaDeploy SAP EHP7 интегрированными средами разработки с пакетом обновления 3 для 6.0 ERP SAP в Azure | Документы Microsoft"
description: "Развертывание SAP IDES EHP7 SP3 для SAP ERP 6.0 в Azure"
services: virtual-machines-windows
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 626c1523-1026-478f-bd8a-22c83b869231
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 09/16/2016
ms.author: hermannd
ms.openlocfilehash: 26d88c7b48a91d35602464c4f89ca7a30502c4b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-ides-ehp7-sp3-for-sap-erp-60-on-azure"></a><span data-ttu-id="792e5-103">Развертывание SAP IDES EHP7 SP3 для SAP ERP 6.0 в Azure</span><span class="sxs-lookup"><span data-stu-id="792e5-103">Deploy SAP IDES EHP7 SP3 for SAP ERP 6.0 on Azure</span></span>
<span data-ttu-id="792e5-104">В этой статье описывается как toodeploy SAP интегрированными средами разработки системы с SQL Server и операционной системы Windows hello на Azure через hello SAP облачной устройства библиотеки (SAP CAL) 3.0.</span><span class="sxs-lookup"><span data-stu-id="792e5-104">This article describes how toodeploy an SAP IDES system running with SQL Server and hello Windows operating system on Azure via hello SAP Cloud Appliance Library (SAP CAL) 3.0.</span></span> <span data-ttu-id="792e5-105">снимки экрана приветствия Показать пошаговый процесс hello.</span><span class="sxs-lookup"><span data-stu-id="792e5-105">hello screenshots show hello step-by-step process.</span></span> <span data-ttu-id="792e5-106">Выполните toodeploy другого решения hello одну последовательность шагов.</span><span class="sxs-lookup"><span data-stu-id="792e5-106">toodeploy a different solution, follow hello same steps.</span></span>

<span data-ttu-id="792e5-107">toostart с hello CAL SAP, последовательно выберите toohello [устройство библиотеки SAP облака](https://cal.sap.com/) веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="792e5-107">toostart with hello SAP CAL, go toohello [SAP Cloud Appliance Library](https://cal.sap.com/) website.</span></span> <span data-ttu-id="792e5-108">SAP также есть блог о hello новый [устройство библиотеки SAP облака 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span><span class="sxs-lookup"><span data-stu-id="792e5-108">SAP also has a blog about hello new [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span></span> 

> [!NOTE]
<span data-ttu-id="792e5-109">Кроме как 29 мая 2017 г., можно использовать модель развертывания диспетчера ресурсов Azure hello toohello менее предпочтительным классическое развертывание модели toodeploy hello SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="792e5-109">As of May 29, 2017, you can use hello Azure Resource Manager deployment model in addition toohello less-preferred classic deployment model toodeploy hello SAP CAL.</span></span> <span data-ttu-id="792e5-110">Мы рекомендуем использовать hello новая модель развертывания диспетчера ресурсов и не принимать во внимание hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="792e5-110">We recommend that you use hello new Resource Manager deployment model and disregard hello classic deployment model.</span></span>

<span data-ttu-id="792e5-111">Если вы создали учетную запись SAP CAL, использующий hello классической модели, *toocreate требуется другой учетной записи SAP CAL*.</span><span class="sxs-lookup"><span data-stu-id="792e5-111">If you already created an SAP CAL account that uses hello classic model, *you need toocreate another SAP CAL account*.</span></span> <span data-ttu-id="792e5-112">Эта учетная запись должна tooexclusively развертывания в Azure с помощью модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="792e5-112">This account needs tooexclusively deploy into Azure by using hello Resource Manager model.</span></span>

<span data-ttu-id="792e5-113">После входа в toohello SAP CAL, первая страница hello обычно содержится руководство toohello **решения** страницы.</span><span class="sxs-lookup"><span data-stu-id="792e5-113">After you sign in toohello SAP CAL, hello first page usually leads you toohello **Solutions** page.</span></span> <span data-ttu-id="792e5-114">Hello решения, предлагаемые на hello SAP CAL неуклонно растет, поэтому может понадобиться tooscroll немного toofind hello решение, которое требуется.</span><span class="sxs-lookup"><span data-stu-id="792e5-114">hello solutions offered on hello SAP CAL are steadily increasing, so you might need tooscroll quite a bit toofind hello solution you want.</span></span> <span data-ttu-id="792e5-115">решение SAP интегрированными средами разработки на основе Windows Hello выделяются, доступен только в Azure показан процесс развертывания hello:</span><span class="sxs-lookup"><span data-stu-id="792e5-115">hello highlighted Windows-based SAP IDES solution that is available exclusively on Azure demonstrates hello deployment process:</span></span>

![Решения SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic1.jpg)

### <a name="create-an-account-in-hello-sap-cal"></a><span data-ttu-id="792e5-117">Создать учетную запись в hello SAP CAL</span><span class="sxs-lookup"><span data-stu-id="792e5-117">Create an account in hello SAP CAL</span></span>
1. <span data-ttu-id="792e5-118">toosign в toohello SAP CAL для hello первая команда пользователя S SAP или других пользователей, зарегистрированных в SAP.</span><span class="sxs-lookup"><span data-stu-id="792e5-118">toosign in toohello SAP CAL for hello first time, use your SAP S-User or other user registered with SAP.</span></span> <span data-ttu-id="792e5-119">Затем укажите учетную запись SAP клиентских лицензий, используемых устройств toodeploy hello SAP CAL в Azure.</span><span class="sxs-lookup"><span data-stu-id="792e5-119">Then define an SAP CAL account that is used by hello SAP CAL toodeploy appliances on Azure.</span></span> <span data-ttu-id="792e5-120">В определении hello учетной записи необходимо:</span><span class="sxs-lookup"><span data-stu-id="792e5-120">In hello account definition, you need to:</span></span>

    <span data-ttu-id="792e5-121">а.</span><span class="sxs-lookup"><span data-stu-id="792e5-121">a.</span></span> <span data-ttu-id="792e5-122">Выберите модель развертывания hello в Azure (диспетчера ресурсов или Классическая версия).</span><span class="sxs-lookup"><span data-stu-id="792e5-122">Select hello deployment model on Azure (Resource Manager or classic).</span></span>

    <span data-ttu-id="792e5-123">b.</span><span class="sxs-lookup"><span data-stu-id="792e5-123">b.</span></span> <span data-ttu-id="792e5-124">Введите подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="792e5-124">Enter your Azure subscription.</span></span> <span data-ttu-id="792e5-125">Учетной записи SAP CAL могут назначаться только tooone подписок.</span><span class="sxs-lookup"><span data-stu-id="792e5-125">An SAP CAL account can be assigned tooone subscription only.</span></span> <span data-ttu-id="792e5-126">Если вам требуется более чем одной подписке, toocreate требуется другой учетной записи SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="792e5-126">If you need more than one subscription, you need toocreate another SAP CAL account.</span></span>
    
    <span data-ttu-id="792e5-127">c.</span><span class="sxs-lookup"><span data-stu-id="792e5-127">c.</span></span> <span data-ttu-id="792e5-128">Предоставьте разрешение toodeploy hello SAP CAL в вашей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="792e5-128">Give hello SAP CAL permission toodeploy into your Azure subscription.</span></span>

    > [!NOTE]
    <span data-ttu-id="792e5-129">Hello следующие шаги показывают, как учетная запись toocreate CAL SAP для развертывания диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="792e5-129">hello next steps show how toocreate an SAP CAL account for Resource Manager deployments.</span></span> <span data-ttu-id="792e5-130">Если уже имеется связанный toohello классической модели развертывания, с учетной записью SAP CAL вы *требуется* toofollow toocreate эти действия учетной записи SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="792e5-130">If you already have an SAP CAL account that is linked toohello classic deployment model, you *need* toofollow these steps toocreate a new SAP CAL account.</span></span> <span data-ttu-id="792e5-131">Hello новой учетной записи SAP CAL должен toodeploy в модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="792e5-131">hello new SAP CAL account needs toodeploy in hello Resource Manager model.</span></span>

2. <span data-ttu-id="792e5-132">toocreate новой клиентской лицензии SAP учетной записи, hello **учетные записи** странице отображаются два варианта для Azure:</span><span class="sxs-lookup"><span data-stu-id="792e5-132">toocreate a new SAP CAL account, hello **Accounts** page shows two choices for Azure:</span></span> 

    <span data-ttu-id="792e5-133">а.</span><span class="sxs-lookup"><span data-stu-id="792e5-133">a.</span></span> <span data-ttu-id="792e5-134">**Microsoft Azure (классические)** является hello классической модели развертывания и больше не является предпочтительным.</span><span class="sxs-lookup"><span data-stu-id="792e5-134">**Microsoft Azure (classic)** is hello classic deployment model and is no longer preferred.</span></span>

    <span data-ttu-id="792e5-135">b.</span><span class="sxs-lookup"><span data-stu-id="792e5-135">b.</span></span> <span data-ttu-id="792e5-136">**Microsoft Azure** — hello новая модель развертывания диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="792e5-136">**Microsoft Azure** is hello new Resource Manager deployment model.</span></span>

    ![Учетные записи CAL SAP](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic-2a.PNG)

    <span data-ttu-id="792e5-138">Выберите toodeploy в модели hello диспетчер ресурсов, **Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="792e5-138">toodeploy in hello Resource Manager model, select **Microsoft Azure**.</span></span>

    ![Учетные записи CAL SAP](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

3. <span data-ttu-id="792e5-140">Введите hello Azure **идентификатор подписки** , можно найти на hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="792e5-140">Enter hello Azure **Subscription ID** that can be found on hello Azure portal.</span></span> 

    ![Идентификатор подписки SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

4. <span data-ttu-id="792e5-142">определенные tooauthorize toodeploy SAP CAL hello в hello подписки Azure, щелкните **авторизовать**.</span><span class="sxs-lookup"><span data-stu-id="792e5-142">tooauthorize hello SAP CAL toodeploy into hello Azure subscription you defined, click **Authorize**.</span></span> <span data-ttu-id="792e5-143">После страницы приветствия появляется hello вкладке браузера:</span><span class="sxs-lookup"><span data-stu-id="792e5-143">hello following page appears in hello browser tab:</span></span>

    ![Вход в облачные службы в Internet Explorer](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic4c.PNG)

5. <span data-ttu-id="792e5-145">Если в списке больше одного пользователя, выберите hello учетной записи Майкрософт, связанного toobe coadministrator hello объекта hello Azure подписку, которую вы выбрали.</span><span class="sxs-lookup"><span data-stu-id="792e5-145">If more than one user is listed, choose hello Microsoft account that is linked toobe hello coadministrator of hello Azure subscription you selected.</span></span> <span data-ttu-id="792e5-146">После страницы приветствия появляется hello вкладке браузера:</span><span class="sxs-lookup"><span data-stu-id="792e5-146">hello following page appears in hello browser tab:</span></span>

    ![Подтверждение входа в облачные службы в Internet Explorer](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic5a.PNG)

6. <span data-ttu-id="792e5-148">Нажмите кнопку **Принимаю**.</span><span class="sxs-lookup"><span data-stu-id="792e5-148">Click **Accept**.</span></span> <span data-ttu-id="792e5-149">При успешном выполнении авторизации hello hello определения учетной записи SAP CAL отображаются снова.</span><span class="sxs-lookup"><span data-stu-id="792e5-149">If hello authorization is successful, hello SAP CAL account definition displays again.</span></span> <span data-ttu-id="792e5-150">Через некоторое время сообщение подтверждает, что процесс авторизации hello была успешной.</span><span class="sxs-lookup"><span data-stu-id="792e5-150">After a short time, a message confirms that hello authorization process was successful.</span></span>

7. <span data-ttu-id="792e5-151">tooassign hello только что созданный пользователь tooyour учетной записи SAP CAL, введите ваш **идентификатор пользователя** в текстовое поле в правой hello hello и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="792e5-151">tooassign hello newly created SAP CAL account tooyour user, enter your **User ID** in hello text box on hello right and click **Add**.</span></span> 

    ![Сопоставление toouser учетной записи](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic8a.PNG)

8. <span data-ttu-id="792e5-153">Щелкните свою учетную запись с hello пользователя использовать toosign в toohello SAP CAL tooassociate **проверки**.</span><span class="sxs-lookup"><span data-stu-id="792e5-153">tooassociate your account with hello user that you use toosign in toohello SAP CAL, click **Review**.</span></span> 

9. <span data-ttu-id="792e5-154">Щелкните toocreate hello связь между пользователем и учетной записи SAP CAL вновь созданные hello, **создать**.</span><span class="sxs-lookup"><span data-stu-id="792e5-154">toocreate hello association between your user and hello newly created SAP CAL account, click **Create**.</span></span>

    ![Ассоциация tooaccount пользователя](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic9b.PNG)

<span data-ttu-id="792e5-156">Вы успешно создали учетную запись SAP CAL, позволяющую выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="792e5-156">You successfully created an SAP CAL account that is able to:</span></span>

- <span data-ttu-id="792e5-157">Использование модели развертывания диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="792e5-157">Use hello Resource Manager deployment model.</span></span>
- <span data-ttu-id="792e5-158">развертывать системы SAP в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="792e5-158">Deploy SAP systems into your Azure subscription.</span></span>

> [!NOTE]
<span data-ttu-id="792e5-159">Перед развертыванием hello SAP интегрированными средами разработки решений на базе Windows и SQL Server, может потребоваться toosign для подписки на SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="792e5-159">Before you can deploy hello SAP IDES solution based on Windows and SQL Server, you might need toosign up for an SAP CAL subscription.</span></span> <span data-ttu-id="792e5-160">В противном случае решение hello может отображаться как **заблокирована** на страницу обзора hello.</span><span class="sxs-lookup"><span data-stu-id="792e5-160">Otherwise, hello solution might show up as **Locked** on hello overview page.</span></span>

### <a name="deploy-a-solution"></a><span data-ttu-id="792e5-161">Развертывание решения</span><span class="sxs-lookup"><span data-stu-id="792e5-161">Deploy a solution</span></span>
1. <span data-ttu-id="792e5-162">После настройки учетной записи SAP CAL выберите **hello SAP интегрированными средами разработки решений на Windows и SQL Server** решения.</span><span class="sxs-lookup"><span data-stu-id="792e5-162">After you set up an SAP CAL account, select **hello SAP IDES solution on Windows and SQL Server** solution.</span></span> <span data-ttu-id="792e5-163">Нажмите кнопку **создать экземпляр**и подтвердите hello условия использования и условия.</span><span class="sxs-lookup"><span data-stu-id="792e5-163">Click **Create Instance**, and confirm hello usage and terms conditions.</span></span> 

2. <span data-ttu-id="792e5-164">На hello **основной режим: создать экземпляр** страницы, необходимо:</span><span class="sxs-lookup"><span data-stu-id="792e5-164">On hello **Basic Mode: Create Instance** page, you need to:</span></span>

    <span data-ttu-id="792e5-165">а.</span><span class="sxs-lookup"><span data-stu-id="792e5-165">a.</span></span> <span data-ttu-id="792e5-166">Введите **имя** экземпляра.</span><span class="sxs-lookup"><span data-stu-id="792e5-166">Enter an instance **Name**.</span></span>

    <span data-ttu-id="792e5-167">b.</span><span class="sxs-lookup"><span data-stu-id="792e5-167">b.</span></span> <span data-ttu-id="792e5-168">Выберите **регион** Azure.</span><span class="sxs-lookup"><span data-stu-id="792e5-168">Select an Azure **Region**.</span></span> <span data-ttu-id="792e5-169">Может потребоваться tooget подписки SAP CAL, предлагаемые в нескольких регионах Azure.</span><span class="sxs-lookup"><span data-stu-id="792e5-169">You might need an SAP CAL subscription tooget multiple Azure regions offered.</span></span>

    <span data-ttu-id="792e5-170">c.</span><span class="sxs-lookup"><span data-stu-id="792e5-170">c.</span></span>  <span data-ttu-id="792e5-171">Введите образец hello **пароль** hello решения, как показано:</span><span class="sxs-lookup"><span data-stu-id="792e5-171">Enter hello master **Password** for hello solution, as shown:</span></span>

    ![Базовый режим SAP CAL: создание экземпляра](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic10a.png)

3. <span data-ttu-id="792e5-173">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="792e5-173">Click **Create**.</span></span> <span data-ttu-id="792e5-174">Через некоторое время в зависимости от размера hello и сложности решения hello (приветствия SAP CAL предоставляет оценку), hello состояние отображается как активные и готов к использованию:</span><span class="sxs-lookup"><span data-stu-id="792e5-174">After some time, depending on hello size and complexity of hello solution (hello SAP CAL provides an estimate), hello status is shown as active and ready for use:</span></span> 

    ![Экземпляры SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic12a.png)

4. <span data-ttu-id="792e5-176">Группа ресурсов toofind hello и всех объектов, которые были созданы путем hello SAP CAL см. toohello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="792e5-176">toofind hello resource group and all its objects that were created by hello SAP CAL, go toohello Azure portal.</span></span> <span data-ttu-id="792e5-177">начиная с hello же экземпляра имени, указанному в hello SAP CAL можно найти Hello виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="792e5-177">hello virtual machine can be found starting with hello same instance name that was given in hello SAP CAL.</span></span>

    ![Объекты группы ресурсов](./media/cal-ides-erp6-ehp7-sp3-sql/ides_resource_group.PNG)

5. <span data-ttu-id="792e5-179">На портале hello SAP CAL, перейдите toohello развернуты экземпляры и нажмите кнопку **Connect**.</span><span class="sxs-lookup"><span data-stu-id="792e5-179">On hello SAP CAL portal, go toohello deployed instances and click **Connect**.</span></span> <span data-ttu-id="792e5-180">Появится следующая всплывающее окно приветствия:</span><span class="sxs-lookup"><span data-stu-id="792e5-180">hello following pop-up window appears:</span></span> 

    ![Подключение toohello экземпляра](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic14a.PNG)

6. <span data-ttu-id="792e5-182">Прежде чем использовать tooconnect toohello развернут hello параметры системы, нажмите кнопку **руководство по началу работы**.</span><span class="sxs-lookup"><span data-stu-id="792e5-182">Before you can use one of hello options tooconnect toohello deployed systems, click **Getting Started Guide**.</span></span> <span data-ttu-id="792e5-183">имена документации Hello hello пользователей для каждого из методов связи hello.</span><span class="sxs-lookup"><span data-stu-id="792e5-183">hello documentation names hello users for each of hello connectivity methods.</span></span> <span data-ttu-id="792e5-184">пароли Hello для тех пользователей, задаются toohello главный пароль, которые определены в начале процесса развертывания hello hello.</span><span class="sxs-lookup"><span data-stu-id="792e5-184">hello passwords for those users are set toohello master password you defined at hello beginning of hello deployment process.</span></span> <span data-ttu-id="792e5-185">В документации hello других более работы пользователей в списке свои пароли, которые можно использовать toosign в toohello развертывания системы.</span><span class="sxs-lookup"><span data-stu-id="792e5-185">In hello documentation, other more functional users are listed with their passwords, which you can use toosign in toohello deployed system.</span></span>

    ![Вводная документации по SAP](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic15.jpg)

<span data-ttu-id="792e5-187">Работоспособная система SAP IDES развертывается в Azure в течение нескольких часов.</span><span class="sxs-lookup"><span data-stu-id="792e5-187">Within a few hours, a healthy SAP IDES system is deployed in Azure.</span></span>

<span data-ttu-id="792e5-188">Если вы приобрели подписку на SAP CAL, SAP полностью поддерживает развертываниями с помощью hello SAP CAL в Azure.</span><span class="sxs-lookup"><span data-stu-id="792e5-188">If you bought an SAP CAL subscription, SAP fully supports deployments through hello SAP CAL on Azure.</span></span> <span data-ttu-id="792e5-189">очередь поддержки Hello — BC VCM клиентских лицензий.</span><span class="sxs-lookup"><span data-stu-id="792e5-189">hello support queue is BC-VCM-CAL.</span></span>

