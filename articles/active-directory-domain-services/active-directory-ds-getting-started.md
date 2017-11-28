---
title: "Доменные службы Azure Active Directory: начало работы | Документы Майкрософт"
description: "Включение Azure доменных служб Active Directory с помощью hello портал Azure (Предварительная версия)"
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
ms.openlocfilehash: 79cbb21c4a50194f5ad8ca1a4a8493ee4a260a9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a><span data-ttu-id="c721f-103">Включение Azure доменных служб Active Directory с помощью hello портал Azure (Предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="c721f-103">Enable Azure Active Directory Domain Services using hello Azure portal (Preview)</span></span>
<span data-ttu-id="c721f-104">В этой статье показано, как tooenable Active Directory домена служб Azure (Azure AD DS) с помощью hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c721f-104">This article shows how tooenable Azure Active Directory Domain Services (Azure AD DS) using hello Azure portal.</span></span>


<span data-ttu-id="c721f-105">toolaunch hello **включить доменные службы Azure AD** мастера, завершенной hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="c721f-105">toolaunch hello **Enable Azure AD Domain Services** wizard, complete hello following steps:</span></span>

1. <span data-ttu-id="c721f-106">Go toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c721f-106">Go toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c721f-107">В левой области hello, нажмите кнопку **New**.</span><span class="sxs-lookup"><span data-stu-id="c721f-107">In hello left pane, click on **New**.</span></span>
3. <span data-ttu-id="c721f-108">В hello **New** колонки, тип **доменных служб** в строку поиска hello.</span><span class="sxs-lookup"><span data-stu-id="c721f-108">In hello **New** blade, type **Domain Services** into hello search bar.</span></span>

    ![Поиск доменных служб](./media/getting-started/search-domain-services.png)

4. <span data-ttu-id="c721f-110">Нажмите кнопку tooselect **доменные службы Azure AD** hello списке вариантов поиска.</span><span class="sxs-lookup"><span data-stu-id="c721f-110">Click tooselect **Azure AD Domain Services** from hello list of search suggestions.</span></span> <span data-ttu-id="c721f-111">На hello **доменные службы Azure AD** колонка, щелкните hello **создать** кнопки.</span><span class="sxs-lookup"><span data-stu-id="c721f-111">On hello **Azure AD Domain Services** blade, click hello **Create** button.</span></span>

    ![Колонка "Доменные службы"](./media/getting-started/domain-services-blade.png)

5. <span data-ttu-id="c721f-113">Hello **включить доменные службы Azure AD** запустить мастер.</span><span class="sxs-lookup"><span data-stu-id="c721f-113">hello **Enable Azure AD Domain Services** wizard is launched.</span></span>


## <a name="task-1-configure-basic-settings"></a><span data-ttu-id="c721f-114">Задача 1. Настройка основных параметров</span><span class="sxs-lookup"><span data-stu-id="c721f-114">Task 1: configure basic settings</span></span>
<span data-ttu-id="c721f-115">В hello **основы** страница приветствия мастера, можно указать hello DNS-имя домена для домена управляемого hello.</span><span class="sxs-lookup"><span data-stu-id="c721f-115">In hello **Basics** page of hello wizard, you can specify hello DNS domain name for hello managed domain.</span></span> <span data-ttu-id="c721f-116">Можно также выбрать группу ресурсов hello и расположение Azure toowhich hello управляемого домена следует развернуть.</span><span class="sxs-lookup"><span data-stu-id="c721f-116">You can also choose hello resource group and Azure location toowhich hello managed domain should be deployed.</span></span>

![Настройка основных сведений](./media/getting-started/domain-services-blade-basics.png)

1. <span data-ttu-id="c721f-118">Выберите hello **DNS-имя домена** управляемого домена.</span><span class="sxs-lookup"><span data-stu-id="c721f-118">Choose hello **DNS domain name** for your managed domain.</span></span>

   * <span data-ttu-id="c721f-119">имя домена по умолчанию Hello hello каталога (с **. onmicrosoft.com** суффикс) по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c721f-119">hello default domain name of hello directory (with a **.onmicrosoft.com** suffix) is specified by default.</span></span>

   * <span data-ttu-id="c721f-120">Можно также ввести пользовательское доменное имя.</span><span class="sxs-lookup"><span data-stu-id="c721f-120">You can also type in a custom domain name.</span></span> <span data-ttu-id="c721f-121">В этом примере — hello пользовательское имя домена *contoso100.com*.</span><span class="sxs-lookup"><span data-stu-id="c721f-121">In this example, hello custom domain name is *contoso100.com*.</span></span>

     > [!WARNING]
     > <span data-ttu-id="c721f-122">Hello префикс к имени домена (например, *contoso100* в hello *contoso100.com* доменное имя) должно содержать не более 15 символов.</span><span class="sxs-lookup"><span data-stu-id="c721f-122">hello prefix of your specified domain name (for example, *contoso100* in hello *contoso100.com* domain name) must contain 15 or fewer characters.</span></span> <span data-ttu-id="c721f-123">Невозможно создать управляемый домен с префиксом длиннее 15 символов.</span><span class="sxs-lookup"><span data-stu-id="c721f-123">You cannot create a managed domain with a prefix longer than 15 characters.</span></span>
     >
     >

2. <span data-ttu-id="c721f-124">Убедитесь, что hello DNS-имя домена, выбранный для hello управляемого домена еще не существует в виртуальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="c721f-124">Ensure that hello DNS domain name you have chosen for hello managed domain does not already exist in hello virtual network.</span></span> <span data-ttu-id="c721f-125">В частности, убедитесь в следующем:</span><span class="sxs-lookup"><span data-stu-id="c721f-125">Specifically, check whether:</span></span>

   * <span data-ttu-id="c721f-126">Уже имеется домен с hello же DNS-имя домена в виртуальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="c721f-126">You already have a domain with hello same DNS domain name on hello virtual network.</span></span>

   * <span data-ttu-id="c721f-127">Hello виртуальной сети, где планируется tooenable hello управляемый домен имеет VPN-подключение к локальной сети.</span><span class="sxs-lookup"><span data-stu-id="c721f-127">hello virtual network where you plan tooenable hello managed domain has a VPN connection with your on-premises network.</span></span> <span data-ttu-id="c721f-128">В этом случае убедитесь, не нужно, чтобы домен с hello же DNS-имя домена в локальной сети.</span><span class="sxs-lookup"><span data-stu-id="c721f-128">In this scenario, ensure you don't have a domain with hello same DNS domain name on your on-premises network.</span></span>

   * <span data-ttu-id="c721f-129">У вас есть существующей облачной службы с таким именем hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c721f-129">You have an existing cloud service with that name on hello virtual network.</span></span>

3. <span data-ttu-id="c721f-130">Выберите hello **тип виртуальной сети**.</span><span class="sxs-lookup"><span data-stu-id="c721f-130">Choose hello **type of virtual network**.</span></span> <span data-ttu-id="c721f-131">По умолчанию hello **диспетчера ресурсов** выбран тип виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c721f-131">By default, hello **Resource Manager** virtual network type is selected.</span></span> <span data-ttu-id="c721f-132">Мы рекомендуем использовать этот тип виртуальной сети для всех создаваемых управляемых доменов.</span><span class="sxs-lookup"><span data-stu-id="c721f-132">We recommend using this type of virtual network for all newly created managed domains.</span></span>

4. <span data-ttu-id="c721f-133">Выберите hello Azure **подписки** хотите toocreate hello управляемый домен.</span><span class="sxs-lookup"><span data-stu-id="c721f-133">Select hello Azure **Subscription** in which you would like toocreate hello managed domain.</span></span>

5. <span data-ttu-id="c721f-134">Выберите hello **группы ресурсов** должны принадлежать к управляемому домену toowhich hello.</span><span class="sxs-lookup"><span data-stu-id="c721f-134">Select hello **Resource group** toowhich hello managed domain should belong.</span></span> <span data-ttu-id="c721f-135">Вы можете либо hello **создать новый** или **использовать существующие** группы ресурсов hello tooselect параметры.</span><span class="sxs-lookup"><span data-stu-id="c721f-135">You can choose either hello **Create new** or **Use existing** options tooselect hello resource group.</span></span>

6. <span data-ttu-id="c721f-136">Выберите hello Azure **расположение** в какой hello следует создать управляемый домен.</span><span class="sxs-lookup"><span data-stu-id="c721f-136">Choose hello Azure **Location** in which hello managed domain should be created.</span></span> <span data-ttu-id="c721f-137">На hello **сети** страница приветствия мастера вы видите только виртуальные сети, которые принадлежат toohello расположение выбора.</span><span class="sxs-lookup"><span data-stu-id="c721f-137">On hello **Network** page of hello wizard, you see only virtual networks that belong toohello location you have selected.</span></span>

7. <span data-ttu-id="c721f-138">Закончив, нажмите кнопку **ОК** toomove на toohello **сети** на странице приветствия мастера.</span><span class="sxs-lookup"><span data-stu-id="c721f-138">When you are done, click **OK** toomove on toohello **Network** page of hello wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="c721f-139">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c721f-139">Next step</span></span>
[<span data-ttu-id="c721f-140">Задача 2. Настройка сетевых параметров</span><span class="sxs-lookup"><span data-stu-id="c721f-140">Task 2: configure network settings</span></span>](active-directory-ds-getting-started-network.md)
