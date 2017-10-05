---
title: "Развертывание SAP IDES EHP7 SP3 для SAP ERP 6.0 в Azure | Документация Майкрософт"
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
ms.openlocfilehash: 91eed294077ff72d0760018b10c98f32db88f3be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-sap-ides-ehp7-sp3-for-sap-erp-60-on-azure"></a><span data-ttu-id="ebf18-103">Развертывание SAP IDES EHP7 SP3 для SAP ERP 6.0 в Azure</span><span class="sxs-lookup"><span data-stu-id="ebf18-103">Deploy SAP IDES EHP7 SP3 for SAP ERP 6.0 on Azure</span></span>
<span data-ttu-id="ebf18-104">В этой статье описывается, как развернуть SAP IDES с SQL Server и Windows в Azure с помощью SAP Cloud Appliance Library (SAP CAL) 3.0.</span><span class="sxs-lookup"><span data-stu-id="ebf18-104">This article describes how to deploy an SAP IDES system running with SQL Server and the Windows operating system on Azure via the SAP Cloud Appliance Library (SAP CAL) 3.0.</span></span> <span data-ttu-id="ebf18-105">На снимках экрана наглядно показан пошаговый процесс.</span><span class="sxs-lookup"><span data-stu-id="ebf18-105">The screenshots show the step-by-step process.</span></span> <span data-ttu-id="ebf18-106">Для развертывания другого решения выполните те же действия.</span><span class="sxs-lookup"><span data-stu-id="ebf18-106">To deploy a different solution, follow the same steps.</span></span>

<span data-ttu-id="ebf18-107">Чтобы начать работу с SAP CAL, перейдите на веб-сайт [SAP Cloud Appliance Library](https://cal.sap.com/).</span><span class="sxs-lookup"><span data-stu-id="ebf18-107">To start with the SAP CAL, go to the [SAP Cloud Appliance Library](https://cal.sap.com/) website.</span></span> <span data-ttu-id="ebf18-108">В SAP также есть блог о новой версии [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span><span class="sxs-lookup"><span data-stu-id="ebf18-108">SAP also has a blog about the new [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span></span> 

> [!NOTE]
<span data-ttu-id="ebf18-109">Начиная с 29 мая 2017 г. для развертывания SAP CAL можно использовать модель развертывания с помощью Azure Resource Manager в дополнение к менее популярной классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="ebf18-109">As of May 29, 2017, you can use the Azure Resource Manager deployment model in addition to the less-preferred classic deployment model to deploy the SAP CAL.</span></span> <span data-ttu-id="ebf18-110">Мы рекомендуем использовать новую модель развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ebf18-110">We recommend that you use the new Resource Manager deployment model and disregard the classic deployment model.</span></span>

<span data-ttu-id="ebf18-111">Если вы создали учетную запись SAP CAL, использующую классическую модель, *создайте другую учетную запись SAP CAL*.</span><span class="sxs-lookup"><span data-stu-id="ebf18-111">If you already created an SAP CAL account that uses the classic model, *you need to create another SAP CAL account*.</span></span> <span data-ttu-id="ebf18-112">Эту учетную запись нужно развернуть исключительно в Azure с помощью модели Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ebf18-112">This account needs to exclusively deploy into Azure by using the Resource Manager model.</span></span>

<span data-ttu-id="ebf18-113">После входа в SAP CAL с первой страницы обычно можно перейти на страницу **решений**.</span><span class="sxs-lookup"><span data-stu-id="ebf18-113">After you sign in to the SAP CAL, the first page usually leads you to the **Solutions** page.</span></span> <span data-ttu-id="ebf18-114">Количество решений SAP CAL неуклонно растет, поэтому, чтобы найти требуемое решение, может понадобиться много времени.</span><span class="sxs-lookup"><span data-stu-id="ebf18-114">The solutions offered on the SAP CAL are steadily increasing, so you might need to scroll quite a bit to find the solution you want.</span></span> <span data-ttu-id="ebf18-115">На примере выделенного решения SAP IDES на основе Windows, доступного только в Azure, можно ознакомиться с процессом развертывания:</span><span class="sxs-lookup"><span data-stu-id="ebf18-115">The highlighted Windows-based SAP IDES solution that is available exclusively on Azure demonstrates the deployment process:</span></span>

![Решения SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic1.jpg)

### <a name="create-an-account-in-the-sap-cal"></a><span data-ttu-id="ebf18-117">Создание учетной записи в SAP CAL</span><span class="sxs-lookup"><span data-stu-id="ebf18-117">Create an account in the SAP CAL</span></span>
1. <span data-ttu-id="ebf18-118">Для входа в SAP CAL впервые используйте пользователя S-User SAP или других пользователей, зарегистрированных в SAP.</span><span class="sxs-lookup"><span data-stu-id="ebf18-118">To sign in to the SAP CAL for the first time, use your SAP S-User or other user registered with SAP.</span></span> <span data-ttu-id="ebf18-119">Затем определите учетную запись SAP CAL, которая используется SAP CAL для развертывания устройств в Azure.</span><span class="sxs-lookup"><span data-stu-id="ebf18-119">Then define an SAP CAL account that is used by the SAP CAL to deploy appliances on Azure.</span></span> <span data-ttu-id="ebf18-120">Вот что нужно сделать в определении учетной записи:</span><span class="sxs-lookup"><span data-stu-id="ebf18-120">In the account definition, you need to:</span></span>

    <span data-ttu-id="ebf18-121">а.</span><span class="sxs-lookup"><span data-stu-id="ebf18-121">a.</span></span> <span data-ttu-id="ebf18-122">Выберите модель развертывания в Azure (Resource Manager или классическая).</span><span class="sxs-lookup"><span data-stu-id="ebf18-122">Select the deployment model on Azure (Resource Manager or classic).</span></span>

    <span data-ttu-id="ebf18-123">b.</span><span class="sxs-lookup"><span data-stu-id="ebf18-123">b.</span></span> <span data-ttu-id="ebf18-124">Введите подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="ebf18-124">Enter your Azure subscription.</span></span> <span data-ttu-id="ebf18-125">Учетную запись SAP CAL можно назначить только одной подписке.</span><span class="sxs-lookup"><span data-stu-id="ebf18-125">An SAP CAL account can be assigned to one subscription only.</span></span> <span data-ttu-id="ebf18-126">Если вам требуется несколько подписок, необходимо создать еще одну учетную запись SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="ebf18-126">If you need more than one subscription, you need to create another SAP CAL account.</span></span>
    
    <span data-ttu-id="ebf18-127">c.</span><span class="sxs-lookup"><span data-stu-id="ebf18-127">c.</span></span> <span data-ttu-id="ebf18-128">Предоставьте SAP CAL разрешение на развертывание в вашей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="ebf18-128">Give the SAP CAL permission to deploy into your Azure subscription.</span></span>

    > [!NOTE]
    <span data-ttu-id="ebf18-129">Далее показано, как создать учетную запись SAP CAL для развертываний Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ebf18-129">The next steps show how to create an SAP CAL account for Resource Manager deployments.</span></span> <span data-ttu-id="ebf18-130">При наличии учетной записи SAP CAL, связанной с классической моделью развертывания, *выполните* следующие действия, чтобы создать учетную запись SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="ebf18-130">If you already have an SAP CAL account that is linked to the classic deployment model, you *need* to follow these steps to create a new SAP CAL account.</span></span> <span data-ttu-id="ebf18-131">Новую учетную запись SAP CAL нужно развернуть в модели диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ebf18-131">The new SAP CAL account needs to deploy in the Resource Manager model.</span></span>

2. <span data-ttu-id="ebf18-132">При создании учетной записи SAP CAL на странице **Учетные записи** отображаются два варианта для Azure:</span><span class="sxs-lookup"><span data-stu-id="ebf18-132">To create a new SAP CAL account, the **Accounts** page shows two choices for Azure:</span></span> 

    <span data-ttu-id="ebf18-133">а.</span><span class="sxs-lookup"><span data-stu-id="ebf18-133">a.</span></span> <span data-ttu-id="ebf18-134">**Microsoft Azure (classic)** (Microsoft Azure (классическая)) — это классическая модель развертывания. Мы не рекомендуем ее использовать.</span><span class="sxs-lookup"><span data-stu-id="ebf18-134">**Microsoft Azure (classic)** is the classic deployment model and is no longer preferred.</span></span>

    <span data-ttu-id="ebf18-135">b.</span><span class="sxs-lookup"><span data-stu-id="ebf18-135">b.</span></span> <span data-ttu-id="ebf18-136">**Microsoft Azure** — это новая модель развертывания с помощью диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ebf18-136">**Microsoft Azure** is the new Resource Manager deployment model.</span></span>

    ![Учетные записи CAL SAP](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic-2a.PNG)

    <span data-ttu-id="ebf18-138">Чтобы выполнить развертывание с использованием модели диспетчера ресурсов, выберите **Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="ebf18-138">To deploy in the Resource Manager model, select **Microsoft Azure**.</span></span>

    ![Учетные записи CAL SAP](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

3. <span data-ttu-id="ebf18-140">Введите **идентификатор подписки** Azure, который можно найти на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="ebf18-140">Enter the Azure **Subscription ID** that can be found on the Azure portal.</span></span> 

    ![Идентификатор подписки SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

4. <span data-ttu-id="ebf18-142">Чтобы разрешить SAP CAL выполнить развертывание в указанной подписке Azure, щелкните **Авторизовать**.</span><span class="sxs-lookup"><span data-stu-id="ebf18-142">To authorize the SAP CAL to deploy into the Azure subscription you defined, click **Authorize**.</span></span> <span data-ttu-id="ebf18-143">На вкладке браузера появится следующая страница:</span><span class="sxs-lookup"><span data-stu-id="ebf18-143">The following page appears in the browser tab:</span></span>

    ![Вход в облачные службы в Internet Explorer](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic4c.PNG)

5. <span data-ttu-id="ebf18-145">Если в списке указано несколько пользователей, выберите связанную учетную запись Майкрософт с назначенной ролью соадминистратора в выбранной подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="ebf18-145">If more than one user is listed, choose the Microsoft account that is linked to be the coadministrator of the Azure subscription you selected.</span></span> <span data-ttu-id="ebf18-146">На вкладке браузера появится следующая страница:</span><span class="sxs-lookup"><span data-stu-id="ebf18-146">The following page appears in the browser tab:</span></span>

    ![Подтверждение входа в облачные службы в Internet Explorer](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic5a.PNG)

6. <span data-ttu-id="ebf18-148">Нажмите кнопку **Принимаю**.</span><span class="sxs-lookup"><span data-stu-id="ebf18-148">Click **Accept**.</span></span> <span data-ttu-id="ebf18-149">При успешном выполнении авторизации снова появится определение учетной записи SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="ebf18-149">If the authorization is successful, the SAP CAL account definition displays again.</span></span> <span data-ttu-id="ebf18-150">Через некоторое время появится сообщение с подтверждением успешного выполнения авторизации.</span><span class="sxs-lookup"><span data-stu-id="ebf18-150">After a short time, a message confirms that the authorization process was successful.</span></span>

7. <span data-ttu-id="ebf18-151">Чтобы назначить новую учетную запись SAP CAL пользователю, в поле справа введите **идентификатор пользователя** и щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ebf18-151">To assign the newly created SAP CAL account to your user, enter your **User ID** in the text box on the right and click **Add**.</span></span> 

    ![Сопоставление учетной записи с пользователем](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic8a.PNG)

8. <span data-ttu-id="ebf18-153">Чтобы сопоставить учетную запись с пользователем, использованным для входа в SAP CAL, щелкните **Просмотр**.</span><span class="sxs-lookup"><span data-stu-id="ebf18-153">To associate your account with the user that you use to sign in to the SAP CAL, click **Review**.</span></span> 

9. <span data-ttu-id="ebf18-154">Чтобы создать сопоставление между пользователем и новой учетной записью SAP CAL, щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ebf18-154">To create the association between your user and the newly created SAP CAL account, click **Create**.</span></span>

    ![Сопоставление пользователя с учетной записью](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic9b.PNG)

<span data-ttu-id="ebf18-156">Вы успешно создали учетную запись SAP CAL, позволяющую выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="ebf18-156">You successfully created an SAP CAL account that is able to:</span></span>

- <span data-ttu-id="ebf18-157">использовать модель развертывания с помощью Resource Manager;</span><span class="sxs-lookup"><span data-stu-id="ebf18-157">Use the Resource Manager deployment model.</span></span>
- <span data-ttu-id="ebf18-158">развертывать системы SAP в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="ebf18-158">Deploy SAP systems into your Azure subscription.</span></span>

> [!NOTE]
<span data-ttu-id="ebf18-159">Перед развертыванием решения SAP IDES на основе Windows и SQL Server может потребоваться зарегистрировать подписку SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="ebf18-159">Before you can deploy the SAP IDES solution based on Windows and SQL Server, you might need to sign up for an SAP CAL subscription.</span></span> <span data-ttu-id="ebf18-160">В противном случае на странице обзора решение может отображаться как **заблокированное**.</span><span class="sxs-lookup"><span data-stu-id="ebf18-160">Otherwise, the solution might show up as **Locked** on the overview page.</span></span>

### <a name="deploy-a-solution"></a><span data-ttu-id="ebf18-161">Развертывание решения</span><span class="sxs-lookup"><span data-stu-id="ebf18-161">Deploy a solution</span></span>
1. <span data-ttu-id="ebf18-162">После настройки учетной записи SAP CAL выберите **решение SAP IDES под управлением Windows и SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="ebf18-162">After you set up an SAP CAL account, select **The SAP IDES solution on Windows and SQL Server** solution.</span></span> <span data-ttu-id="ebf18-163">Щелкните **Create Instance** (Создать экземпляр) и согласитесь с условиями использования.</span><span class="sxs-lookup"><span data-stu-id="ebf18-163">Click **Create Instance**, and confirm the usage and terms conditions.</span></span> 

2. <span data-ttu-id="ebf18-164">На странице **Basic Mode: Create Instance** (Базовый режим: создание экземпляра) сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="ebf18-164">On the **Basic Mode: Create Instance** page, you need to:</span></span>

    <span data-ttu-id="ebf18-165">а.</span><span class="sxs-lookup"><span data-stu-id="ebf18-165">a.</span></span> <span data-ttu-id="ebf18-166">Введите **имя** экземпляра.</span><span class="sxs-lookup"><span data-stu-id="ebf18-166">Enter an instance **Name**.</span></span>

    <span data-ttu-id="ebf18-167">b.</span><span class="sxs-lookup"><span data-stu-id="ebf18-167">b.</span></span> <span data-ttu-id="ebf18-168">Выберите **регион** Azure.</span><span class="sxs-lookup"><span data-stu-id="ebf18-168">Select an Azure **Region**.</span></span> <span data-ttu-id="ebf18-169">Чтобы получить несколько регионов Azure на выбор, может потребоваться подписка SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="ebf18-169">You might need an SAP CAL subscription to get multiple Azure regions offered.</span></span>

    <span data-ttu-id="ebf18-170">c.</span><span class="sxs-lookup"><span data-stu-id="ebf18-170">c.</span></span>  <span data-ttu-id="ebf18-171">Введите основной **пароль** для доступа к решению, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="ebf18-171">Enter the master **Password** for the solution, as shown:</span></span>

    ![Страница SAP CAL Basic Mode: Create Instance (Базовый режим: создание экземпляра)](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic10a.png)

3. <span data-ttu-id="ebf18-173">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ebf18-173">Click **Create**.</span></span> <span data-ttu-id="ebf18-174">В зависимости от размера и сложности решения (оценку предоставляет SAP CAL) через некоторое время состояние экземпляра сменится на "Активный", и он будет готов к использованию.</span><span class="sxs-lookup"><span data-stu-id="ebf18-174">After some time, depending on the size and complexity of the solution (the SAP CAL provides an estimate), the status is shown as active and ready for use:</span></span> 

    ![Экземпляры SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic12a.png)

4. <span data-ttu-id="ebf18-176">Чтобы найти группу ресурсов и все ее объекты, созданные с помощью SAP CAL, перейдите на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ebf18-176">To find the resource group and all its objects that were created by the SAP CAL, go to the Azure portal.</span></span> <span data-ttu-id="ebf18-177">Виртуальную машину можно найти по имени экземпляра, указанному в SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="ebf18-177">The virtual machine can be found starting with the same instance name that was given in the SAP CAL.</span></span>

    ![Объекты группы ресурсов](./media/cal-ides-erp6-ehp7-sp3-sql/ides_resource_group.PNG)

5. <span data-ttu-id="ebf18-179">На портале SAP CAL перейдите к развернутым экземплярам и щелкните **Подключиться**.</span><span class="sxs-lookup"><span data-stu-id="ebf18-179">On the SAP CAL portal, go to the deployed instances and click **Connect**.</span></span> <span data-ttu-id="ebf18-180">Появится следующее всплывающее окно:</span><span class="sxs-lookup"><span data-stu-id="ebf18-180">The following pop-up window appears:</span></span> 

    ![Подключение к экземпляру](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic14a.PNG)

6. <span data-ttu-id="ebf18-182">Прежде чем вы сможете использовать один из вариантов подключения к развернутой системе, щелкните **Руководство по началу работы**.</span><span class="sxs-lookup"><span data-stu-id="ebf18-182">Before you can use one of the options to connect to the deployed systems, click **Getting Started Guide**.</span></span> <span data-ttu-id="ebf18-183">В документации указаны пользователи для каждого из способов подключения.</span><span class="sxs-lookup"><span data-stu-id="ebf18-183">The documentation names the users for each of the connectivity methods.</span></span> <span data-ttu-id="ebf18-184">Для этих пользователей заданы основные пароли, указанные в начале развертывания.</span><span class="sxs-lookup"><span data-stu-id="ebf18-184">The passwords for those users are set to the master password you defined at the beginning of the deployment process.</span></span> <span data-ttu-id="ebf18-185">В документации также представлены другие пользователи с более широкими возможностями и их пароли, которые можно использовать для входа в развернутую систему.</span><span class="sxs-lookup"><span data-stu-id="ebf18-185">In the documentation, other more functional users are listed with their passwords, which you can use to sign in to the deployed system.</span></span>

    ![Вводная документации по SAP](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic15.jpg)

<span data-ttu-id="ebf18-187">Работоспособная система SAP IDES развертывается в Azure в течение нескольких часов.</span><span class="sxs-lookup"><span data-stu-id="ebf18-187">Within a few hours, a healthy SAP IDES system is deployed in Azure.</span></span>

<span data-ttu-id="ebf18-188">Если вы приобрели подписку SAP CAL, SAP полностью поддерживает развертывания с помощью SAP CAL в Azure.</span><span class="sxs-lookup"><span data-stu-id="ebf18-188">If you bought an SAP CAL subscription, SAP fully supports deployments through the SAP CAL on Azure.</span></span> <span data-ttu-id="ebf18-189">Используется очередь поддержки BC-VCM-CAL.</span><span class="sxs-lookup"><span data-stu-id="ebf18-189">The support queue is BC-VCM-CAL.</span></span>

