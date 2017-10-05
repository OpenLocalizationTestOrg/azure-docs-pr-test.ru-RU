---
title: "Развертывание SAP S/4HANA или BW/4HANA на виртуальной машине Azure | Документация Майкрософт"
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
ms.openlocfilehash: 4788fa14a6c49d39b5a3096a69b6738f4a5d8cca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-sap-s4hana-or-bw4hana-on-azure"></a><span data-ttu-id="a7e9e-103">Развертывание SAP S/4HANA или BW/4HANA в Azure</span><span class="sxs-lookup"><span data-stu-id="a7e9e-103">Deploy SAP S/4HANA or BW/4HANA on Azure</span></span>
<span data-ttu-id="a7e9e-104">В этой статье описывается, как развернуть платформу S/4HANA в Azure с помощью SAP Cloud Appliance Library (SAP CAL) 3.0.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-104">This article describes how to deploy S/4HANA on Azure by using the SAP Cloud Appliance Library (SAP CAL) 3.0.</span></span> <span data-ttu-id="a7e9e-105">Чтобы развернуть другие решения на основе SAP HANA, например BW/4HANA, выполните те же действия.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-105">To deploy other SAP HANA-based solutions, such as BW/4HANA, follow the same steps.</span></span>

> [!NOTE]
<span data-ttu-id="a7e9e-106">Дополнительные сведения о лицензии SAP см. на веб-сайте [Библиотека SAP Cloud Appliance Library](https://cal.sap.com/).</span><span class="sxs-lookup"><span data-stu-id="a7e9e-106">For more information about the SAP CAL, go to the [SAP Cloud Appliance Library](https://cal.sap.com/) website.</span></span> <span data-ttu-id="a7e9e-107">У SAP также есть блог о [библиотеке SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span><span class="sxs-lookup"><span data-stu-id="a7e9e-107">SAP also has a blog about the [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span></span>

> [!NOTE]
<span data-ttu-id="a7e9e-108">Начиная с 29 мая 2017 г. для развертывания SAP CAL можно использовать модель развертывания с помощью Azure Resource Manager в дополнение к менее популярной классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-108">As of May 29, 2017, you can use the Azure Resource Manager deployment model in addition to the less-preferred classic deployment model to deploy the SAP CAL.</span></span> <span data-ttu-id="a7e9e-109">Мы рекомендуем использовать новую модель развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-109">We recommend that you use the new Resource Manager deployment model and disregard the classic deployment model.</span></span>

## <a name="step-by-step-process-to-deploy-the-solution"></a><span data-ttu-id="a7e9e-110">Пошаговый процесс развертывания решения</span><span class="sxs-lookup"><span data-stu-id="a7e9e-110">Step-by-step process to deploy the solution</span></span>

<span data-ttu-id="a7e9e-111">На снимках экрана, представленных ниже, показано развертывание S/4HANA в Azure с использованием SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-111">The following sequence of screenshots shows you how to deploy S/4HANA on Azure by using the SAP CAL.</span></span> <span data-ttu-id="a7e9e-112">Процесс развертывания других решений, например BW/4 HANA, аналогичен описанному ниже.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-112">The process works the same way for other solutions, such as BW/4HANA.</span></span>

<span data-ttu-id="a7e9e-113">Страница **Решения** отображает некоторые решения на основе SAP CAL HANA, доступные в Azure.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-113">The **Solutions** page shows some of the SAP CAL HANA-based solutions available on Azure.</span></span> <span data-ttu-id="a7e9e-114">Пункт **SAP S/4HANA 1610 FPS01, полностью активное устройство** находится в строке посередине:</span><span class="sxs-lookup"><span data-stu-id="a7e9e-114">**SAP S/4HANA 1610 FPS01, Fully-Activated Appliance** is in the middle row:</span></span>

![Решения SAP CAL](./media/cal-s4h/s4h-pic-1c.png)

### <a name="create-an-account-in-the-sap-cal"></a><span data-ttu-id="a7e9e-116">Создание учетной записи в SAP CAL</span><span class="sxs-lookup"><span data-stu-id="a7e9e-116">Create an account in the SAP CAL</span></span>
1. <span data-ttu-id="a7e9e-117">Для входа в SAP CAL впервые используйте пользователя S-User SAP или других пользователей, зарегистрированных в SAP.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-117">To sign in to the SAP CAL for the first time, use your SAP S-User or other user registered with SAP.</span></span> <span data-ttu-id="a7e9e-118">Затем определите учетную запись SAP CAL, которая используется SAP CAL для развертывания устройств в Azure.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-118">Then define an SAP CAL account that is used by the SAP CAL to deploy appliances on Azure.</span></span> <span data-ttu-id="a7e9e-119">Вот что нужно сделать в определении учетной записи:</span><span class="sxs-lookup"><span data-stu-id="a7e9e-119">In the account definition, you need to:</span></span>

    <span data-ttu-id="a7e9e-120">а.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-120">a.</span></span> <span data-ttu-id="a7e9e-121">Выберите модель развертывания в Azure (Resource Manager или классическая).</span><span class="sxs-lookup"><span data-stu-id="a7e9e-121">Select the deployment model on Azure (Resource Manager or classic).</span></span>

    <span data-ttu-id="a7e9e-122">b.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-122">b.</span></span> <span data-ttu-id="a7e9e-123">Введите подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-123">Enter your Azure subscription.</span></span> <span data-ttu-id="a7e9e-124">Учетную запись SAP CAL можно назначить только одной подписке.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-124">An SAP CAL account can be assigned to one subscription only.</span></span> <span data-ttu-id="a7e9e-125">Если вам требуется несколько подписок, необходимо создать еще одну учетную запись SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-125">If you need more than one subscription, you need to create another SAP CAL account.</span></span>

    <span data-ttu-id="a7e9e-126">c.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-126">c.</span></span> <span data-ttu-id="a7e9e-127">Предоставьте SAP CAL разрешение на развертывание в вашей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-127">Give the SAP CAL permission to deploy into your Azure subscription.</span></span>

    > [!NOTE]
    <span data-ttu-id="a7e9e-128">Далее показано, как создать учетную запись SAP CAL для развертываний Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-128">The next steps show how to create an SAP CAL account for Resource Manager deployments.</span></span> <span data-ttu-id="a7e9e-129">При наличии учетной записи SAP CAL, связанной с классической моделью развертывания, *выполните* следующие действия, чтобы создать учетную запись SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-129">If you already have an SAP CAL account that is linked to the classic deployment model, you *need* to follow these steps to create a new SAP CAL account.</span></span> <span data-ttu-id="a7e9e-130">Новую учетную запись SAP CAL нужно развернуть в модели Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-130">The new SAP CAL account needs to deploy in the Resource Manager model.</span></span>

2. <span data-ttu-id="a7e9e-131">Создайте учетную запись SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-131">Create a new SAP CAL account.</span></span> <span data-ttu-id="a7e9e-132">На странице **Учетные записи** отображается три варианта для Azure:</span><span class="sxs-lookup"><span data-stu-id="a7e9e-132">The **Accounts** page shows three choices for Azure:</span></span> 

    <span data-ttu-id="a7e9e-133">а.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-133">a.</span></span> <span data-ttu-id="a7e9e-134">**Microsoft Azure (classic)** (Microsoft Azure (классическая)) — это классическая модель развертывания. Мы не рекомендуем ее использовать.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-134">**Microsoft Azure (classic)** is the classic deployment model and is no longer preferred.</span></span>

    <span data-ttu-id="a7e9e-135">b.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-135">b.</span></span> <span data-ttu-id="a7e9e-136">**Microsoft Azure** — это новая модель развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-136">**Microsoft Azure** is the new Resource Manager deployment model.</span></span>

    <span data-ttu-id="a7e9e-137">c.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-137">c.</span></span> <span data-ttu-id="a7e9e-138">**Windows Azure operated by 21Vianet** (Windows Azure, управляемый 21Vianet) — это вариант для Китая, который использует классическую модель развертывания.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-138">**Windows Azure operated by 21Vianet** is an option in China that uses the classic deployment model.</span></span>

    <span data-ttu-id="a7e9e-139">Чтобы выполнить развертывание с использованием модели Resource Manager, выберите **Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-139">To deploy in the Resource Manager model, select **Microsoft Azure**.</span></span>

    ![Сведения об учетной записи SAP CAL](./media/cal-s4h/s4h-pic-2a.png)

3. <span data-ttu-id="a7e9e-141">Введите **идентификатор подписки** Azure, который можно найти на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-141">Enter the Azure **Subscription ID** that can be found on the Azure portal.</span></span>

   ![Учетные записи CAL SAP](./media/cal-s4h/s4h-pic3c.png)

4. <span data-ttu-id="a7e9e-143">Чтобы разрешить SAP CAL выполнить развертывание в указанной подписке Azure, щелкните **Авторизовать**.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-143">To authorize the SAP CAL to deploy into the Azure subscription you defined, click **Authorize**.</span></span> <span data-ttu-id="a7e9e-144">На вкладке браузера появится следующая страница:</span><span class="sxs-lookup"><span data-stu-id="a7e9e-144">The following page appears in the browser tab:</span></span>

   ![Вход в облачные службы в Internet Explorer](./media/cal-s4h/s4h-pic4c.png)

5. <span data-ttu-id="a7e9e-146">Если в списке указано несколько пользователей, выберите связанную учетную запись Майкрософт с назначенной ролью соадминистратора в выбранной подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-146">If more than one user is listed, choose the Microsoft account that is linked to be the coadministrator of the Azure subscription you selected.</span></span> <span data-ttu-id="a7e9e-147">На вкладке браузера появится следующая страница:</span><span class="sxs-lookup"><span data-stu-id="a7e9e-147">The following page appears in the browser tab:</span></span>

   ![Подтверждение входа в облачные службы в Internet Explorer](./media/cal-s4h/s4h-pic5a.png)

6. <span data-ttu-id="a7e9e-149">Нажмите кнопку **Принимаю**.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-149">Click **Accept**.</span></span> <span data-ttu-id="a7e9e-150">При успешном выполнении авторизации снова появится определение учетной записи SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-150">If the authorization is successful, the SAP CAL account definition displays again.</span></span> <span data-ttu-id="a7e9e-151">Через некоторое время появится сообщение с подтверждением успешного выполнения авторизации.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-151">After a short time, a message confirms that the authorization process was successful.</span></span>

7. <span data-ttu-id="a7e9e-152">Чтобы назначить новую учетную запись SAP CAL пользователю, в поле справа введите **идентификатор пользователя** и щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-152">To assign the newly created SAP CAL account to your user, enter your **User ID** in the text box on the right and click **Add**.</span></span>

   ![Сопоставление учетной записи с пользователем](./media/cal-s4h/s4h-pic8a.png)

8. <span data-ttu-id="a7e9e-154">Чтобы сопоставить учетную запись с пользователем, использованным для входа в SAP CAL, щелкните **Просмотр**.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-154">To associate your account with the user that you use to sign in to the SAP CAL, click **Review**.</span></span> 
 
9. <span data-ttu-id="a7e9e-155">Чтобы создать сопоставление между пользователем и новой учетной записью SAP CAL, щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-155">To create the association between your user and the newly created SAP CAL account, click **Create**.</span></span>

   ![Сопоставление учетной записи пользователя и SAP CAL](./media/cal-s4h/s4h-pic9b.png)

<span data-ttu-id="a7e9e-157">Вы успешно создали учетную запись SAP CAL, позволяющую выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="a7e9e-157">You successfully created an SAP CAL account that is able to:</span></span>

- <span data-ttu-id="a7e9e-158">использовать модель развертывания с помощью Resource Manager;</span><span class="sxs-lookup"><span data-stu-id="a7e9e-158">Use the Resource Manager deployment model.</span></span>
- <span data-ttu-id="a7e9e-159">развертывать системы SAP в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-159">Deploy SAP systems into your Azure subscription.</span></span>

<span data-ttu-id="a7e9e-160">Теперь можно начать развертывание S/4HANA в подписку пользователя в Azure.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-160">Now you can start to deploy S/4HANA into your user subscription in Azure.</span></span>

> [!NOTE]
<span data-ttu-id="a7e9e-161">Прежде чем продолжить, проверьте, есть ли у вас квоты ядер Azure для виртуальных машин Azure серии H.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-161">Before you continue, determine whether you have Azure core quotas for Azure H-Series VMs.</span></span> <span data-ttu-id="a7e9e-162">Сейчас SAP CAL использует виртуальные машины Azure серии H для развертывания некоторых решений на основе SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-162">At the moment, the SAP CAL uses H-Series VMs of Azure to deploy some of the SAP HANA-based solutions.</span></span> <span data-ttu-id="a7e9e-163">Ваша подписка может не иметь квот ядер для серии Н.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-163">Your Azure subscription might not have any H-Series core quotas for H-Series.</span></span> <span data-ttu-id="a7e9e-164">В этом случае обратитесь в службу поддержки Azure, чтобы получить квоту на не менее 16 ядер серии H.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-164">If so, you might need to contact Azure support to get a quota of at least 16 H-Series cores.</span></span>

> [!NOTE]
<span data-ttu-id="a7e9e-165">При развертывании решения на Azure в SAP CAL может оказаться, что можно выбрать только один регион Azure.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-165">When you deploy a solution on Azure in the SAP CAL, you might find that you can choose only one Azure region.</span></span> <span data-ttu-id="a7e9e-166">Чтобы выполнить развертывание в регионе Azure, отличном от предложенного SAP CAL, необходимо приобрести подписку CAL от SAP.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-166">To deploy into Azure regions other than the one suggested by the SAP CAL, you need to purchase a CAL subscription from SAP.</span></span> <span data-ttu-id="a7e9e-167">Также может потребоваться написать SAP сообщение, чтобы активировать для вашей учетной записи CAL возможность доставки в регионы Azure, отличные от тех, которые были изначально предложены.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-167">You also might need to open a message with SAP to have your CAL account enabled to deliver into Azure regions other than the ones initially suggested.</span></span>

### <a name="deploy-a-solution"></a><span data-ttu-id="a7e9e-168">Развертывание решения</span><span class="sxs-lookup"><span data-stu-id="a7e9e-168">Deploy a solution</span></span>

<span data-ttu-id="a7e9e-169">Давайте развернем решение со страницы **Решения** SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-169">Let's deploy a solution from the **Solutions** page of the SAP CAL.</span></span> <span data-ttu-id="a7e9e-170">В SAP CAL есть две последовательности развертывания:</span><span class="sxs-lookup"><span data-stu-id="a7e9e-170">The SAP CAL has two sequences to deploy:</span></span>

- <span data-ttu-id="a7e9e-171">Базовая последовательность, которая использует одну страницу для определения развертываемой системы.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-171">A basic sequence that uses one page to define the system to be deployed</span></span>
- <span data-ttu-id="a7e9e-172">Расширенная последовательность, которая позволяет выбрать определенные размеры виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-172">An advanced sequence that gives you certain choices on VM sizes</span></span> 

<span data-ttu-id="a7e9e-173">Здесь мы рассмотрим базовый путь развертывания.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-173">We demonstrate the basic path to deployment here.</span></span>

1. <span data-ttu-id="a7e9e-174">На странице**Сведения об учетной записи** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="a7e9e-174">On the **Account Details** page, you need to:</span></span>

    <span data-ttu-id="a7e9e-175">а.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-175">a.</span></span> <span data-ttu-id="a7e9e-176">Выберите учетную запись SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-176">Select an SAP CAL account.</span></span> <span data-ttu-id="a7e9e-177">(Используйте учетную запись, которая связана с моделью развертывания Resource Manager.)</span><span class="sxs-lookup"><span data-stu-id="a7e9e-177">(Use an account that is associated to deploy with the Resource Manager deployment model.)</span></span>

    <span data-ttu-id="a7e9e-178">b.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-178">b.</span></span> <span data-ttu-id="a7e9e-179">Введите **имя** экземпляра.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-179">Enter an instance **Name**.</span></span>

    <span data-ttu-id="a7e9e-180">c.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-180">c.</span></span> <span data-ttu-id="a7e9e-181">Выберите **регион** Azure.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-181">Select an Azure **Region**.</span></span> <span data-ttu-id="a7e9e-182">SAP CAL предложит регион.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-182">The SAP CAL suggests a region.</span></span> <span data-ttu-id="a7e9e-183">Если необходим другой регион Azure и у вас нет подписки SAP CAL, необходимо заказать подписку CAL с SAP.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-183">If you need another Azure region and you don't have an SAP CAL subscription, you need to order a CAL subscription with SAP.</span></span>

    <span data-ttu-id="a7e9e-184">г)</span><span class="sxs-lookup"><span data-stu-id="a7e9e-184">d.</span></span> <span data-ttu-id="a7e9e-185">Введите главный **пароль** для решения длиной восемь или девять знаков.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-185">Enter a master **Password** for the solution of eight or nine characters.</span></span> <span data-ttu-id="a7e9e-186">Пароль используется администраторами различных компонентов.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-186">The password is used for the administrators of the different components.</span></span>

   ![Базовый режим SAP CAL: создание экземпляра](./media/cal-s4h/s4h-pic10a.png)

2. <span data-ttu-id="a7e9e-188">Щелкните **Создать** и в появившемся диалоговом окне щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-188">Click **Create**, and in the message box that appears, click **OK**.</span></span>

   ![Поддерживаемые SAP CAL размеры виртуальных машин](./media/cal-s4h/s4h-pic10b.png)

3. <span data-ttu-id="a7e9e-190">В диалоговом окне **Закрытый ключ** щелкните **Хранилище**, чтобы сохранить закрытый ключ в SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-190">In the **Private Key** dialog box, click **Store** to store the private key in the SAP CAL.</span></span> <span data-ttu-id="a7e9e-191">Чтобы использовать защиту паролем для закрытого ключа, щелкните **Скачать**.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-191">To use password protection for the private key, click **Download**.</span></span> 

   ![Закрытый ключ SAP CAL](./media/cal-s4h/s4h-pic10c.png)

4. <span data-ttu-id="a7e9e-193">Ознакомьтесь с сообщением в разделе **Предупреждение** и щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-193">Read the SAP CAL **Warning** message, and click **OK**.</span></span>

   ![Предупреждения SAP CAL](./media/cal-s4h/s4h-pic10d.png)

    <span data-ttu-id="a7e9e-195">После этого начнется развертывание.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-195">Now the deployment takes place.</span></span> <span data-ttu-id="a7e9e-196">В зависимости от размера и сложности решения (оценку предоставляет SAP CAL) через некоторое время состояние экземпляра сменится на "Активный", и он будет готов к использованию.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-196">After some time, depending on the size and complexity of the solution (the SAP CAL provides an estimate), the status is shown as active and ready for use.</span></span>

5. <span data-ttu-id="a7e9e-197">Чтобы найти виртуальные машины, собранные вместе со связанными ресурсами в одну группу ресурсов, перейдите на портал Azure:</span><span class="sxs-lookup"><span data-stu-id="a7e9e-197">To find the virtual machines collected with the other associated resources in one resource group, go to the Azure portal:</span></span> 

   ![Объекты SAP CAL, развернутые на новом портале](./media/cal-s4h/sapcaldeplyment_portalview.png)

6. <span data-ttu-id="a7e9e-199">На портале SAP CAL состояние отображается как **Активный**.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-199">On the SAP CAL portal, the status appears as **Active**.</span></span> <span data-ttu-id="a7e9e-200">Чтобы подключиться к решению, щелкните **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-200">To connect to the solution, click **Connect**.</span></span> <span data-ttu-id="a7e9e-201">В рамках этого решения развернуты разные параметры для подключения к различным компонентам.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-201">Different options to connect to the different components are deployed within this solution.</span></span>

   ![Экземпляры SAP CAL](./media/cal-s4h/active_solution.png)

7. <span data-ttu-id="a7e9e-203">Прежде чем вы сможете использовать один из вариантов подключения к развернутой системе, щелкните **Руководство по началу работы**.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-203">Before you can use one of the options to connect to the deployed systems, click **Getting Started Guide**.</span></span> 

   ![Подключение к экземпляру](./media/cal-s4h/connect_to_solution.png)

    <span data-ttu-id="a7e9e-205">В документации указаны пользователи для каждого из способов подключения.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-205">The documentation names the users for each of the connectivity methods.</span></span> <span data-ttu-id="a7e9e-206">Для этих пользователей заданы основные пароли, указанные в начале развертывания.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-206">The passwords for those users are set to the master password you defined at the beginning of the deployment process.</span></span> <span data-ttu-id="a7e9e-207">В документации также представлены другие пользователи с более широкими возможностями и их пароли, которые можно использовать для входа в развернутую систему.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-207">In the documentation, other more functional users are listed with their passwords, which you can use to sign in to the deployed system.</span></span> 

    <span data-ttu-id="a7e9e-208">Например, при использовании графического пользовательского интерфейса SAP, предварительно установленного на компьютере с удаленным рабочим столом Windows, система S/4 может выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a7e9e-208">For example, if you use the SAP GUI that's preinstalled on the Windows Remote Desktop machine, the S/4 system might look like this:</span></span>

   ![SM50 в предварительно установленном графическом пользовательском интерфейсе SAP](./media/cal-s4h/gui_sm50.png)

    <span data-ttu-id="a7e9e-210">Или при использовании DBACockpit экземпляр может выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a7e9e-210">Or if you use the DBACockpit, the instance might look like this:</span></span>

   ![SM50 в DBACockpit в графическом пользовательском интерфейсе SAP](./media/cal-s4h/dbacockpit.png)

<span data-ttu-id="a7e9e-212">В течение нескольких часов в Azure будет развернуто работоспособное устройство S/4SAP.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-212">Within a few hours, a healthy SAP S/4 appliance is deployed in Azure.</span></span>

<span data-ttu-id="a7e9e-213">Если вы приобрели подписку SAP CAL, SAP полностью поддерживает развертывание с помощью SAP CAL в Azure.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-213">If you bought an SAP CAL subscription, SAP fully supports deployments through the SAP CAL on Azure.</span></span> <span data-ttu-id="a7e9e-214">Используется очередь поддержки BC-VCM-CAL.</span><span class="sxs-lookup"><span data-stu-id="a7e9e-214">The support queue is BC-VCM-CAL.</span></span>







