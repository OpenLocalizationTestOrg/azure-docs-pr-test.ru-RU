---
title: "aaaDeploy SAP S/4HANA или BW/4HANA на Виртуальной машине Azure | Документы Microsoft"
description: "Развертывание SAP S/4HANA или BW/4HANA на виртуальной машине Azure"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 44bbd2b6-a376-4b5c-b824-e76917117fa9
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/15/2016
ms.author: hermannd
ms.openlocfilehash: 7e57f7daa7667b7c7dbcb86f6892a54e4295b74c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-s4hana-or-bw4hana-on-azure"></a><span data-ttu-id="fd3c7-103">Развертывание SAP S/4HANA или BW/4HANA в Azure</span><span class="sxs-lookup"><span data-stu-id="fd3c7-103">Deploy SAP S/4HANA or BW/4HANA on Azure</span></span>
<span data-ttu-id="fd3c7-104">В этой статье описывается, как toodeploy S/4HANA в Azure с помощью hello SAP облачной устройства библиотеки (SAP CAL) 3.0.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-104">This article describes how toodeploy S/4HANA on Azure by using hello SAP Cloud Appliance Library (SAP CAL) 3.0.</span></span> <span data-ttu-id="fd3c7-105">toodeploy других решений на основе SAP HANA, например BW/4HANA выполните hello одну последовательность шагов.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-105">toodeploy other SAP HANA-based solutions, such as BW/4HANA, follow hello same steps.</span></span>

> [!NOTE]
<span data-ttu-id="fd3c7-106">Дополнительные сведения о hello SAP CAL go toohello [SAP облачной устройства библиотеки](https://cal.sap.com/) веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-106">For more information about hello SAP CAL, go toohello [SAP Cloud Appliance Library](https://cal.sap.com/) website.</span></span> <span data-ttu-id="fd3c7-107">SAP также есть блог о hello [устройство библиотеки SAP облака 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span><span class="sxs-lookup"><span data-stu-id="fd3c7-107">SAP also has a blog about hello [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span></span>

> [!NOTE]
<span data-ttu-id="fd3c7-108">Кроме как 29 мая 2017 г., можно использовать модель развертывания диспетчера ресурсов Azure hello toohello менее предпочтительным классическое развертывание модели toodeploy hello SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-108">As of May 29, 2017, you can use hello Azure Resource Manager deployment model in addition toohello less-preferred classic deployment model toodeploy hello SAP CAL.</span></span> <span data-ttu-id="fd3c7-109">Мы рекомендуем использовать hello новая модель развертывания диспетчера ресурсов и не принимать во внимание hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-109">We recommend that you use hello new Resource Manager deployment model and disregard hello classic deployment model.</span></span>

## <a name="step-by-step-process-toodeploy-hello-solution"></a><span data-ttu-id="fd3c7-110">Пошаговый процесс toodeploy hello решения</span><span class="sxs-lookup"><span data-stu-id="fd3c7-110">Step-by-step process toodeploy hello solution</span></span>

<span data-ttu-id="fd3c7-111">Следующая последовательность снимков экрана приветствия показано, как toodeploy S/4HANA в Azure с помощью hello клиентская лицензия SAP.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-111">hello following sequence of screenshots shows you how toodeploy S/4HANA on Azure by using hello SAP CAL.</span></span> <span data-ttu-id="fd3c7-112">Hello процесс работает hello одинаково для других решений, таких как BW/4HANA.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-112">hello process works hello same way for other solutions, such as BW/4HANA.</span></span>

<span data-ttu-id="fd3c7-113">Hello **решения** странице отображаются некоторые hello доступных решений на основе SAP HANA клиентскую Лицензию в Azure.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-113">hello **Solutions** page shows some of hello SAP CAL HANA-based solutions available on Azure.</span></span> <span data-ttu-id="fd3c7-114">**SAP S/4HANA 1610 FPS01, устройство Fully-Activated** в среднем ряду hello:</span><span class="sxs-lookup"><span data-stu-id="fd3c7-114">**SAP S/4HANA 1610 FPS01, Fully-Activated Appliance** is in hello middle row:</span></span>

![Решения SAP CAL](./media/cal-s4h/s4h-pic-1c.png)

### <a name="create-an-account-in-hello-sap-cal"></a><span data-ttu-id="fd3c7-116">Создать учетную запись в hello SAP CAL</span><span class="sxs-lookup"><span data-stu-id="fd3c7-116">Create an account in hello SAP CAL</span></span>
1. <span data-ttu-id="fd3c7-117">toosign в toohello SAP CAL для hello первая команда пользователя S SAP или других пользователей, зарегистрированных в SAP.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-117">toosign in toohello SAP CAL for hello first time, use your SAP S-User or other user registered with SAP.</span></span> <span data-ttu-id="fd3c7-118">Затем укажите учетную запись SAP клиентских лицензий, используемых устройств toodeploy hello SAP CAL в Azure.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-118">Then define an SAP CAL account that is used by hello SAP CAL toodeploy appliances on Azure.</span></span> <span data-ttu-id="fd3c7-119">В определении hello учетной записи необходимо:</span><span class="sxs-lookup"><span data-stu-id="fd3c7-119">In hello account definition, you need to:</span></span>

    <span data-ttu-id="fd3c7-120">а.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-120">a.</span></span> <span data-ttu-id="fd3c7-121">Выберите модель развертывания hello в Azure (диспетчера ресурсов или Классическая версия).</span><span class="sxs-lookup"><span data-stu-id="fd3c7-121">Select hello deployment model on Azure (Resource Manager or classic).</span></span>

    <span data-ttu-id="fd3c7-122">b.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-122">b.</span></span> <span data-ttu-id="fd3c7-123">Введите подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-123">Enter your Azure subscription.</span></span> <span data-ttu-id="fd3c7-124">Учетной записи SAP CAL могут назначаться только tooone подписок.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-124">An SAP CAL account can be assigned tooone subscription only.</span></span> <span data-ttu-id="fd3c7-125">Если вам требуется более чем одной подписке, toocreate требуется другой учетной записи SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-125">If you need more than one subscription, you need toocreate another SAP CAL account.</span></span>

    <span data-ttu-id="fd3c7-126">c.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-126">c.</span></span> <span data-ttu-id="fd3c7-127">Предоставьте разрешение toodeploy hello SAP CAL в вашей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-127">Give hello SAP CAL permission toodeploy into your Azure subscription.</span></span>

    > [!NOTE]
    <span data-ttu-id="fd3c7-128">Hello следующие шаги показывают, как учетная запись toocreate CAL SAP для развертывания диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-128">hello next steps show how toocreate an SAP CAL account for Resource Manager deployments.</span></span> <span data-ttu-id="fd3c7-129">Если уже имеется связанный toohello классической модели развертывания, с учетной записью SAP CAL вы *требуется* toofollow toocreate эти действия учетной записи SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-129">If you already have an SAP CAL account that is linked toohello classic deployment model, you *need* toofollow these steps toocreate a new SAP CAL account.</span></span> <span data-ttu-id="fd3c7-130">Hello новой учетной записи SAP CAL должен toodeploy в модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-130">hello new SAP CAL account needs toodeploy in hello Resource Manager model.</span></span>

2. <span data-ttu-id="fd3c7-131">Создайте учетную запись SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-131">Create a new SAP CAL account.</span></span> <span data-ttu-id="fd3c7-132">Hello **учетные записи** странице отображаются три варианта для Azure:</span><span class="sxs-lookup"><span data-stu-id="fd3c7-132">hello **Accounts** page shows three choices for Azure:</span></span> 

    <span data-ttu-id="fd3c7-133">а.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-133">a.</span></span> <span data-ttu-id="fd3c7-134">**Microsoft Azure (классические)** является hello классической модели развертывания и больше не является предпочтительным.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-134">**Microsoft Azure (classic)** is hello classic deployment model and is no longer preferred.</span></span>

    <span data-ttu-id="fd3c7-135">b.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-135">b.</span></span> <span data-ttu-id="fd3c7-136">**Microsoft Azure** — hello новая модель развертывания диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-136">**Microsoft Azure** is hello new Resource Manager deployment model.</span></span>

    <span data-ttu-id="fd3c7-137">c.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-137">c.</span></span> <span data-ttu-id="fd3c7-138">**Эксплуатироваться Windows Azure, обслуживаемой 21Vianet** является параметром в Китае, использующий hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-138">**Windows Azure operated by 21Vianet** is an option in China that uses hello classic deployment model.</span></span>

    <span data-ttu-id="fd3c7-139">Выберите toodeploy в модели hello диспетчер ресурсов, **Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-139">toodeploy in hello Resource Manager model, select **Microsoft Azure**.</span></span>

    ![Сведения об учетной записи SAP CAL](./media/cal-s4h/s4h-pic-2a.png)

3. <span data-ttu-id="fd3c7-141">Введите hello Azure **идентификатор подписки** , можно найти на hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-141">Enter hello Azure **Subscription ID** that can be found on hello Azure portal.</span></span>

   ![Учетные записи CAL SAP](./media/cal-s4h/s4h-pic3c.png)

4. <span data-ttu-id="fd3c7-143">определенные tooauthorize toodeploy SAP CAL hello в hello подписки Azure, щелкните **авторизовать**.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-143">tooauthorize hello SAP CAL toodeploy into hello Azure subscription you defined, click **Authorize**.</span></span> <span data-ttu-id="fd3c7-144">После страницы приветствия появляется hello вкладке браузера:</span><span class="sxs-lookup"><span data-stu-id="fd3c7-144">hello following page appears in hello browser tab:</span></span>

   ![Вход в облачные службы в Internet Explorer](./media/cal-s4h/s4h-pic4c.png)

5. <span data-ttu-id="fd3c7-146">Если в списке больше одного пользователя, выберите hello учетной записи Майкрософт, связанного toobe coadministrator hello объекта hello Azure подписку, которую вы выбрали.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-146">If more than one user is listed, choose hello Microsoft account that is linked toobe hello coadministrator of hello Azure subscription you selected.</span></span> <span data-ttu-id="fd3c7-147">После страницы приветствия появляется hello вкладке браузера:</span><span class="sxs-lookup"><span data-stu-id="fd3c7-147">hello following page appears in hello browser tab:</span></span>

   ![Подтверждение входа в облачные службы в Internet Explorer](./media/cal-s4h/s4h-pic5a.png)

6. <span data-ttu-id="fd3c7-149">Нажмите кнопку **Принимаю**.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-149">Click **Accept**.</span></span> <span data-ttu-id="fd3c7-150">При успешном выполнении авторизации hello hello определения учетной записи SAP CAL отображаются снова.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-150">If hello authorization is successful, hello SAP CAL account definition displays again.</span></span> <span data-ttu-id="fd3c7-151">Через некоторое время сообщение подтверждает, что процесс авторизации hello была успешной.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-151">After a short time, a message confirms that hello authorization process was successful.</span></span>

7. <span data-ttu-id="fd3c7-152">tooassign hello только что созданный пользователь tooyour учетной записи SAP CAL, введите ваш **идентификатор пользователя** в текстовое поле в правой hello hello и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-152">tooassign hello newly created SAP CAL account tooyour user, enter your **User ID** in hello text box on hello right and click **Add**.</span></span>

   ![Сопоставление toouser учетной записи](./media/cal-s4h/s4h-pic8a.png)

8. <span data-ttu-id="fd3c7-154">Щелкните свою учетную запись с hello пользователя использовать toosign в toohello SAP CAL tooassociate **проверки**.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-154">tooassociate your account with hello user that you use toosign in toohello SAP CAL, click **Review**.</span></span> 
 
9. <span data-ttu-id="fd3c7-155">Щелкните toocreate hello связь между пользователем и учетной записи SAP CAL вновь созданные hello, **создать**.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-155">toocreate hello association between your user and hello newly created SAP CAL account, click **Create**.</span></span>

   ![Сопоставление учетной записи пользователя tooSAP клиентской лицензии](./media/cal-s4h/s4h-pic9b.png)

<span data-ttu-id="fd3c7-157">Вы успешно создали учетную запись SAP CAL, позволяющую выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="fd3c7-157">You successfully created an SAP CAL account that is able to:</span></span>

- <span data-ttu-id="fd3c7-158">Использование модели развертывания диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-158">Use hello Resource Manager deployment model.</span></span>
- <span data-ttu-id="fd3c7-159">развертывать системы SAP в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-159">Deploy SAP systems into your Azure subscription.</span></span>

<span data-ttu-id="fd3c7-160">Теперь вы можете запустить toodeploy S/4HANA в подписки пользователя в Azure.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-160">Now you can start toodeploy S/4HANA into your user subscription in Azure.</span></span>

> [!NOTE]
<span data-ttu-id="fd3c7-161">Прежде чем продолжить, проверьте, есть ли у вас квоты ядер Azure для виртуальных машин Azure серии H.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-161">Before you continue, determine whether you have Azure core quotas for Azure H-Series VMs.</span></span> <span data-ttu-id="fd3c7-162">В момент hello hello SAP CAL использует toodeploy H серии виртуальных машин Azure некоторые решения на основе SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-162">At hello moment, hello SAP CAL uses H-Series VMs of Azure toodeploy some of hello SAP HANA-based solutions.</span></span> <span data-ttu-id="fd3c7-163">Ваша подписка может не иметь квот ядер для серии Н.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-163">Your Azure subscription might not have any H-Series core quotas for H-Series.</span></span> <span data-ttu-id="fd3c7-164">В этом случае может потребоваться tooget поддержки Azure toocontact Квота ядер менее 16 H-Series.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-164">If so, you might need toocontact Azure support tooget a quota of at least 16 H-Series cores.</span></span>

> [!NOTE]
<span data-ttu-id="fd3c7-165">При развертывании решения на платформе Azure в hello SAP CAL, возможно, которые можно выбрать только один регион Azure.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-165">When you deploy a solution on Azure in hello SAP CAL, you might find that you can choose only one Azure region.</span></span> <span data-ttu-id="fd3c7-166">toodeploy в Azure регионах, отличных от hello один предложенными hello SAP CAL, необходимо toopurchase CAL подписки из SAP.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-166">toodeploy into Azure regions other than hello one suggested by hello SAP CAL, you need toopurchase a CAL subscription from SAP.</span></span> <span data-ttu-id="fd3c7-167">Также может потребоваться tooopen сообщение с SAP toohave вашей toodeliver CAL учетная запись включена в Azure регионах, отличных от тех, которые изначально предлагаются hello.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-167">You also might need tooopen a message with SAP toohave your CAL account enabled toodeliver into Azure regions other than hello ones initially suggested.</span></span>

### <a name="deploy-a-solution"></a><span data-ttu-id="fd3c7-168">Развертывание решения</span><span class="sxs-lookup"><span data-stu-id="fd3c7-168">Deploy a solution</span></span>

<span data-ttu-id="fd3c7-169">Давайте развертывание решения из hello **решения** страница hello клиентская лицензия SAP.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-169">Let's deploy a solution from hello **Solutions** page of hello SAP CAL.</span></span> <span data-ttu-id="fd3c7-170">Hello SAP CAL состоит из двух toodeploy последовательности.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-170">hello SAP CAL has two sequences toodeploy:</span></span>

- <span data-ttu-id="fd3c7-171">Базовой последовательности, использующий развернут toobe hello системы одной страницы toodefine</span><span class="sxs-lookup"><span data-stu-id="fd3c7-171">A basic sequence that uses one page toodefine hello system toobe deployed</span></span>
- <span data-ttu-id="fd3c7-172">Расширенная последовательность, которая позволяет выбрать определенные размеры виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-172">An advanced sequence that gives you certain choices on VM sizes</span></span> 

<span data-ttu-id="fd3c7-173">Показывается здесь toodeployment базовый путь hello.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-173">We demonstrate hello basic path toodeployment here.</span></span>

1. <span data-ttu-id="fd3c7-174">На hello **сведения об учетной записи** страницы, необходимо:</span><span class="sxs-lookup"><span data-stu-id="fd3c7-174">On hello **Account Details** page, you need to:</span></span>

    <span data-ttu-id="fd3c7-175">а.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-175">a.</span></span> <span data-ttu-id="fd3c7-176">Выберите учетную запись SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-176">Select an SAP CAL account.</span></span> <span data-ttu-id="fd3c7-177">(Использовать учетную запись, которая является toodeploy, связанные с моделью развертывания диспетчера ресурсов hello).</span><span class="sxs-lookup"><span data-stu-id="fd3c7-177">(Use an account that is associated toodeploy with hello Resource Manager deployment model.)</span></span>

    <span data-ttu-id="fd3c7-178">b.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-178">b.</span></span> <span data-ttu-id="fd3c7-179">Введите **имя** экземпляра.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-179">Enter an instance **Name**.</span></span>

    <span data-ttu-id="fd3c7-180">c.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-180">c.</span></span> <span data-ttu-id="fd3c7-181">Выберите **регион** Azure.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-181">Select an Azure **Region**.</span></span> <span data-ttu-id="fd3c7-182">Hello SAP CAL предлагает область.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-182">hello SAP CAL suggests a region.</span></span> <span data-ttu-id="fd3c7-183">Если требуется другой регион Azure, и у вас нет подписки SAP CAL, вам потребуется подписка tooorder клиентская лицензия с SAP.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-183">If you need another Azure region and you don't have an SAP CAL subscription, you need tooorder a CAL subscription with SAP.</span></span>

    <span data-ttu-id="fd3c7-184">d.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-184">d.</span></span> <span data-ttu-id="fd3c7-185">Введите главного **пароль** для решения hello 8 или 9 символов.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-185">Enter a master **Password** for hello solution of eight or nine characters.</span></span> <span data-ttu-id="fd3c7-186">Hello пароль используется для администраторов hello hello различных компонентов.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-186">hello password is used for hello administrators of hello different components.</span></span>

   ![Базовый режим SAP CAL: создание экземпляра](./media/cal-s4h/s4h-pic10a.png)

2. <span data-ttu-id="fd3c7-188">Нажмите кнопку **создать**, а в окне сообщения hello, которое отображается, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-188">Click **Create**, and in hello message box that appears, click **OK**.</span></span>

   ![Поддерживаемые SAP CAL размеры виртуальных машин](./media/cal-s4h/s4h-pic10b.png)

3. <span data-ttu-id="fd3c7-190">В hello **закрытый ключ** диалоговое окно, нажмите кнопку **хранилища** toostore hello закрытый ключ в hello клиентская лицензия SAP.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-190">In hello **Private Key** dialog box, click **Store** toostore hello private key in hello SAP CAL.</span></span> <span data-ttu-id="fd3c7-191">Защита паролем toouse для hello закрытый ключ, нажмите кнопку **загрузить**.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-191">toouse password protection for hello private key, click **Download**.</span></span> 

   ![Закрытый ключ SAP CAL](./media/cal-s4h/s4h-pic10c.png)

4. <span data-ttu-id="fd3c7-193">Чтение hello SAP CAL **предупреждение** сообщение и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-193">Read hello SAP CAL **Warning** message, and click **OK**.</span></span>

   ![Предупреждения SAP CAL](./media/cal-s4h/s4h-pic10d.png)

    <span data-ttu-id="fd3c7-195">Теперь развертывание hello вступает в силу.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-195">Now hello deployment takes place.</span></span> <span data-ttu-id="fd3c7-196">Через некоторое время в зависимости от размера hello и сложности решения hello (приветствия SAP CAL предоставляет оценку), hello состояние отображается как активные и готов к использованию.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-196">After some time, depending on hello size and complexity of hello solution (hello SAP CAL provides an estimate), hello status is shown as active and ready for use.</span></span>

5. <span data-ttu-id="fd3c7-197">виртуальные машины toofind hello, собранные с помощью hello других связанных ресурсов в одной группе ресурсов, перейдите toohello портала Azure:</span><span class="sxs-lookup"><span data-stu-id="fd3c7-197">toofind hello virtual machines collected with hello other associated resources in one resource group, go toohello Azure portal:</span></span> 

   ![Клиентская лицензия SAP объекты, развертываемые в новый портал hello](./media/cal-s4h/sapcaldeplyment_portalview.png)

6. <span data-ttu-id="fd3c7-199">На портале hello SAP CAL, hello состояние отображается как **Active**.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-199">On hello SAP CAL portal, hello status appears as **Active**.</span></span> <span data-ttu-id="fd3c7-200">tooconnect toohello решение, нажмите кнопку **Connect**.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-200">tooconnect toohello solution, click **Connect**.</span></span> <span data-ttu-id="fd3c7-201">Различные варианты tooconnect toohello различные компоненты развертываются в рамках этого решения.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-201">Different options tooconnect toohello different components are deployed within this solution.</span></span>

   ![Экземпляры SAP CAL](./media/cal-s4h/active_solution.png)

7. <span data-ttu-id="fd3c7-203">Прежде чем использовать tooconnect toohello развернут hello параметры системы, нажмите кнопку **руководство по началу работы**.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-203">Before you can use one of hello options tooconnect toohello deployed systems, click **Getting Started Guide**.</span></span> 

   ![Подключение toohello экземпляра](./media/cal-s4h/connect_to_solution.png)

    <span data-ttu-id="fd3c7-205">имена документации Hello hello пользователей для каждого из методов связи hello.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-205">hello documentation names hello users for each of hello connectivity methods.</span></span> <span data-ttu-id="fd3c7-206">пароли Hello для тех пользователей, задаются toohello главный пароль, которые определены в начале процесса развертывания hello hello.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-206">hello passwords for those users are set toohello master password you defined at hello beginning of hello deployment process.</span></span> <span data-ttu-id="fd3c7-207">В документации hello других более работы пользователей в списке свои пароли, которые можно использовать toosign в toohello развертывания системы.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-207">In hello documentation, other more functional users are listed with their passwords, which you can use toosign in toohello deployed system.</span></span> 

    <span data-ttu-id="fd3c7-208">Например если вы используете hello GUI SAP, предварительно установленное на компьютере удаленного рабочего стола Windows hello, hello S/4 системы может выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="fd3c7-208">For example, if you use hello SAP GUI that's preinstalled on hello Windows Remote Desktop machine, hello S/4 system might look like this:</span></span>

   ![SM50 в hello предустановлен SAP GUI](./media/cal-s4h/gui_sm50.png)

    <span data-ttu-id="fd3c7-210">Или, при использовании hello DBACockpit hello экземпляр может выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="fd3c7-210">Or if you use hello DBACockpit, hello instance might look like this:</span></span>

   ![SM50 в hello DBACockpit SAP GUI](./media/cal-s4h/dbacockpit.png)

<span data-ttu-id="fd3c7-212">В течение нескольких часов в Azure будет развернуто работоспособное устройство S/4SAP.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-212">Within a few hours, a healthy SAP S/4 appliance is deployed in Azure.</span></span>

<span data-ttu-id="fd3c7-213">Если вы приобрели подписку на SAP CAL, SAP полностью поддерживает развертываниями с помощью hello SAP CAL в Azure.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-213">If you bought an SAP CAL subscription, SAP fully supports deployments through hello SAP CAL on Azure.</span></span> <span data-ttu-id="fd3c7-214">очередь поддержки Hello — BC VCM клиентских лицензий.</span><span class="sxs-lookup"><span data-stu-id="fd3c7-214">hello support queue is BC-VCM-CAL.</span></span>







