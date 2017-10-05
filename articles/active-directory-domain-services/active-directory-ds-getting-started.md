---
title: "Доменные службы Azure Active Directory: начало работы | Документы Майкрософт"
description: "Включение доменных служб Azure Active Directory с помощью портала Azure (предварительная версия)"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2017
ms.author: maheshu
ms.openlocfilehash: 47507096a6245d4f1ba57a652ddf5167b3776ae9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-portal-preview"></a><span data-ttu-id="168a0-103">Включение доменных служб Azure Active Directory с помощью портала Azure (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="168a0-103">Enable Azure Active Directory Domain Services using the Azure portal (Preview)</span></span>
<span data-ttu-id="168a0-104">В этой статье показано, как включить доменные службы Azure Active Directory (Azure AD DS) с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="168a0-104">This article shows how to enable Azure Active Directory Domain Services (Azure AD DS) using the Azure portal.</span></span>


<span data-ttu-id="168a0-105">Чтобы запустить мастер **включения доменных служб Azure AD**, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="168a0-105">To launch the **Enable Azure AD Domain Services** wizard, complete the following steps:</span></span>

1. <span data-ttu-id="168a0-106">Перейдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="168a0-106">Go to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="168a0-107">В левой области щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="168a0-107">In the left pane, click on **New**.</span></span>
3. <span data-ttu-id="168a0-108">В колонке **Создать** введите в поле поиска текст **Доменные службы**.</span><span class="sxs-lookup"><span data-stu-id="168a0-108">In the **New** blade, type **Domain Services** into the search bar.</span></span>

    ![Поиск доменных служб](./media/getting-started/search-domain-services.png)

4. <span data-ttu-id="168a0-110">В списке результатов поиска выберите **Доменные службы Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="168a0-110">Click to select **Azure AD Domain Services** from the list of search suggestions.</span></span> <span data-ttu-id="168a0-111">В колонке **Доменные службы Azure AD** нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="168a0-111">On the **Azure AD Domain Services** blade, click the **Create** button.</span></span>

    ![Колонка "Доменные службы"](./media/getting-started/domain-services-blade.png)

5. <span data-ttu-id="168a0-113">Запустится мастер **включения доменных служб Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="168a0-113">The **Enable Azure AD Domain Services** wizard is launched.</span></span>


## <a name="task-1-configure-basic-settings"></a><span data-ttu-id="168a0-114">Задача 1. Настройка основных параметров</span><span class="sxs-lookup"><span data-stu-id="168a0-114">Task 1: configure basic settings</span></span>
<span data-ttu-id="168a0-115">На странице **Основные сведения** мастера можно указать DNS-имя управляемого домена.</span><span class="sxs-lookup"><span data-stu-id="168a0-115">In the **Basics** page of the wizard, you can specify the DNS domain name for the managed domain.</span></span> <span data-ttu-id="168a0-116">Вы также можете выбрать группу ресурсов и расположение Azure, в которых должен быть развернут управляемый домен.</span><span class="sxs-lookup"><span data-stu-id="168a0-116">You can also choose the resource group and Azure location to which the managed domain should be deployed.</span></span>

![Настройка основных сведений](./media/getting-started/domain-services-blade-basics.png)

1. <span data-ttu-id="168a0-118">Выберите **DNS-имя** управляемого домена.</span><span class="sxs-lookup"><span data-stu-id="168a0-118">Choose the **DNS domain name** for your managed domain.</span></span>

   * <span data-ttu-id="168a0-119">По умолчанию указано доменное имя для каталога (с суффиксом **.onmicrosoft.com**).</span><span class="sxs-lookup"><span data-stu-id="168a0-119">The default domain name of the directory (with a **.onmicrosoft.com** suffix) is specified by default.</span></span>

   * <span data-ttu-id="168a0-120">Можно также ввести пользовательское доменное имя.</span><span class="sxs-lookup"><span data-stu-id="168a0-120">You can also type in a custom domain name.</span></span> <span data-ttu-id="168a0-121">В этом примере в качестве имени пользовательского домена мы используем *contoso100.com*.</span><span class="sxs-lookup"><span data-stu-id="168a0-121">In this example, the custom domain name is *contoso100.com*.</span></span>

     > [!WARNING]
     > <span data-ttu-id="168a0-122">Длина указанного префикса доменного имени (например, *contoso100* для доменного имени *contoso100.com*) не должна превышать 15 символов.</span><span class="sxs-lookup"><span data-stu-id="168a0-122">The prefix of your specified domain name (for example, *contoso100* in the *contoso100.com* domain name) must contain 15 or fewer characters.</span></span> <span data-ttu-id="168a0-123">Невозможно создать управляемый домен с префиксом длиннее 15 символов.</span><span class="sxs-lookup"><span data-stu-id="168a0-123">You cannot create a managed domain with a prefix longer than 15 characters.</span></span>
     >
     >

2. <span data-ttu-id="168a0-124">Убедитесь, что выбранное имя домена DNS для управляемого домена не существует в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="168a0-124">Ensure that the DNS domain name you have chosen for the managed domain does not already exist in the virtual network.</span></span> <span data-ttu-id="168a0-125">В частности, убедитесь в следующем:</span><span class="sxs-lookup"><span data-stu-id="168a0-125">Specifically, check whether:</span></span>

   * <span data-ttu-id="168a0-126">в виртуальной сети уже существует домен с таким же DNS-именем домена;</span><span class="sxs-lookup"><span data-stu-id="168a0-126">You already have a domain with the same DNS domain name on the virtual network.</span></span>

   * <span data-ttu-id="168a0-127">для виртуальной сети, в которой планируется использовать управляемый домен, установлено VPN-подключение к локальной сети;</span><span class="sxs-lookup"><span data-stu-id="168a0-127">The virtual network where you plan to enable the managed domain has a VPN connection with your on-premises network.</span></span> <span data-ttu-id="168a0-128">в этом случае необходимо убедиться в том, что в локальной сети нет домена с таким же DNS-именем домена;</span><span class="sxs-lookup"><span data-stu-id="168a0-128">In this scenario, ensure you don't have a domain with the same DNS domain name on your on-premises network.</span></span>

   * <span data-ttu-id="168a0-129">в виртуальной сети существует облачная служба с таким же именем.</span><span class="sxs-lookup"><span data-stu-id="168a0-129">You have an existing cloud service with that name on the virtual network.</span></span>

3. <span data-ttu-id="168a0-130">Выберите **тип виртуальной сети**.</span><span class="sxs-lookup"><span data-stu-id="168a0-130">Choose the **type of virtual network**.</span></span> <span data-ttu-id="168a0-131">По умолчанию выбран тип **Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="168a0-131">By default, the **Resource Manager** virtual network type is selected.</span></span> <span data-ttu-id="168a0-132">Мы рекомендуем использовать этот тип виртуальной сети для всех создаваемых управляемых доменов.</span><span class="sxs-lookup"><span data-stu-id="168a0-132">We recommend using this type of virtual network for all newly created managed domains.</span></span>

4. <span data-ttu-id="168a0-133">Выберите **подписку** Azure, в которой следует создать управляемый домен.</span><span class="sxs-lookup"><span data-stu-id="168a0-133">Select the Azure **Subscription** in which you would like to create the managed domain.</span></span>

5. <span data-ttu-id="168a0-134">Выберите **группу ресурсов**, к которой должен относиться управляемый домен.</span><span class="sxs-lookup"><span data-stu-id="168a0-134">Select the **Resource group** to which the managed domain should belong.</span></span> <span data-ttu-id="168a0-135">При выборе группы ресурсов можно использовать команду **Создать** или **Использовать существующую**.</span><span class="sxs-lookup"><span data-stu-id="168a0-135">You can choose either the **Create new** or **Use existing** options to select the resource group.</span></span>

6. <span data-ttu-id="168a0-136">Выберите **расположение** Azure, в котором необходимо создать управляемый домен.</span><span class="sxs-lookup"><span data-stu-id="168a0-136">Choose the Azure **Location** in which the managed domain should be created.</span></span> <span data-ttu-id="168a0-137">На странице **Сеть** мастера приводятся только те виртуальные сети, которые относятся к выбранному расположению.</span><span class="sxs-lookup"><span data-stu-id="168a0-137">On the **Network** page of the wizard, you see only virtual networks that belong to the location you have selected.</span></span>

7. <span data-ttu-id="168a0-138">Завершив настройку, нажмите кнопку **ОК** для перехода на страницу **Сеть** мастера.</span><span class="sxs-lookup"><span data-stu-id="168a0-138">When you are done, click **OK** to move on to the **Network** page of the wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="168a0-139">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="168a0-139">Next step</span></span>
[<span data-ttu-id="168a0-140">Задача 2. Настройка сетевых параметров</span><span class="sxs-lookup"><span data-stu-id="168a0-140">Task 2: configure network settings</span></span>](active-directory-ds-getting-started-network.md)
