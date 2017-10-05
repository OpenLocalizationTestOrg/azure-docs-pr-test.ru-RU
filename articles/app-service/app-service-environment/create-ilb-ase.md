---
title: "Создание и использование внутреннего балансировщика нагрузки со средой службы приложений Azure"
description: "Сведения о создании и использовании изолированной от Интернета среды службы приложений Azure"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 0f4c1fa4-e344-46e7-8d24-a25e247ae138
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: e7f85aaf2d940f114248d5925a1e97fe0f6bda6c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-use-an-internal-load-balancer-with-an-app-service-environment"></a><span data-ttu-id="9bc8f-103">Создание и использование внутреннего балансировщика нагрузки со средой службы приложений</span><span class="sxs-lookup"><span data-stu-id="9bc8f-103">Create and use an internal load balancer with an App Service environment</span></span> #

 <span data-ttu-id="9bc8f-104">Среда службы приложений — это развернутая служба приложений Azure в подсети виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-104">Azure App Service Environment is a deployment of Azure App Service into a subnet in an Azure virtual network (VNet).</span></span> <span data-ttu-id="9bc8f-105">Существует два способа развертывания среды службы приложений (ASE):</span><span class="sxs-lookup"><span data-stu-id="9bc8f-105">There are two ways to deploy an App Service environment (ASE):</span></span> 

- <span data-ttu-id="9bc8f-106">с виртуальным IP-адресом на основе внешнего IP-адреса, что часто называют внешней средой ASE;</span><span class="sxs-lookup"><span data-stu-id="9bc8f-106">With a VIP on an external IP address, often called an External ASE.</span></span>
- <span data-ttu-id="9bc8f-107">с виртуальным IP-адресом на основе внутреннего IP-адреса, что часто называют средой службы приложений с внутренним балансировщиком нагрузки, так как внутренней конечной точкой является внутренний балансировщик нагрузки (ILB).</span><span class="sxs-lookup"><span data-stu-id="9bc8f-107">With a VIP on an internal IP address, often called an ILB ASE because the internal endpoint is an internal load balancer (ILB).</span></span> 

<span data-ttu-id="9bc8f-108">В этой статье показано, как создать ASE с внутренним балансировщиком нагрузки.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-108">This article shows you how to create an ILB ASE.</span></span> <span data-ttu-id="9bc8f-109">Общие сведения см. в статье [Общие сведения о среде службы приложений][Intro].</span><span class="sxs-lookup"><span data-stu-id="9bc8f-109">For an overview on the ASE, see [Introduction to App Service environments][Intro].</span></span> <span data-ttu-id="9bc8f-110">Сведения о создании внешней среды ASE см. в статье[Создание внешней среды службы приложений][MakeExternalASE].</span><span class="sxs-lookup"><span data-stu-id="9bc8f-110">To learn how to create an External ASE, see [Create an External ASE][MakeExternalASE].</span></span>

## <a name="overview"></a><span data-ttu-id="9bc8f-111">Обзор</span><span class="sxs-lookup"><span data-stu-id="9bc8f-111">Overview</span></span> ##

<span data-ttu-id="9bc8f-112">Вы можете развернуть ASE с конечной точкой, доступной из Интернета, или IP-адресом в вашей виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-112">You can deploy an ASE with an internet-accessible endpoint or with an IP address in your VNet.</span></span> <span data-ttu-id="9bc8f-113">Чтобы задать IP-адрес виртуальной сети, среду службы приложений необходимо развернуть с внутренним балансировщиком нагрузки.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-113">To set the IP address to a VNet address, the ASE must be deployed with an ILB.</span></span> <span data-ttu-id="9bc8f-114">При развертывании среды службы приложений с внутренним балансировщиком нагрузки необходимо наличие следующих компонентов:</span><span class="sxs-lookup"><span data-stu-id="9bc8f-114">When you deploy your ASE with an ILB, you must provide:</span></span>

-   <span data-ttu-id="9bc8f-115">Ваш собственный домен, в котором создаются приложения.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-115">Your own domain that you use when you create your apps.</span></span>
-   <span data-ttu-id="9bc8f-116">Сертификат, используемый для HTTPS.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-116">The certificate used for HTTPS.</span></span>
-   <span data-ttu-id="9bc8f-117">Управление службой DNS для домена.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-117">DNS management for your domain.</span></span>

<span data-ttu-id="9bc8f-118">Это дает следующие возможности:</span><span class="sxs-lookup"><span data-stu-id="9bc8f-118">In return, you can do things such as:</span></span>

-   <span data-ttu-id="9bc8f-119">Безопасное размещение в облаке приложений из интрасети, доступ к которым осуществляется через VPN типа "сеть — сеть" или Azure ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-119">Host intranet applications securely in the cloud, which you access through a site-to-site or Azure ExpressRoute VPN.</span></span>
-   <span data-ttu-id="9bc8f-120">Размещение в облаке приложений, которые не указаны на общедоступных DNS-серверах.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-120">Host apps in the cloud that aren't listed in public DNS servers.</span></span>
-   <span data-ttu-id="9bc8f-121">Создание изолированных от Интернета внутренних приложений, с которыми можно безопасно интегрировать свои внешние приложения.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-121">Create internet-isolated back-end apps, which your front-end apps can securely integrate with.</span></span>

### <a name="disabled-functionality"></a><span data-ttu-id="9bc8f-122">Отключенные функциональные возможности</span><span class="sxs-lookup"><span data-stu-id="9bc8f-122">Disabled functionality</span></span> ###

<span data-ttu-id="9bc8f-123">Существуют некоторые функции, недоступные при использовании ASE с внутренним балансировщиком нагрузки.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-123">There are some things that you can't do when you use an ILB ASE:</span></span>

-   <span data-ttu-id="9bc8f-124">Использование SSL на основе IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-124">Use IP-based SSL.</span></span>
-   <span data-ttu-id="9bc8f-125">Назначение IP-адресов конкретным приложениям.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-125">Assign IP addresses to specific apps.</span></span>
-   <span data-ttu-id="9bc8f-126">Приобретение и использование сертификата с приложением на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-126">Buy and use a certificate with an app through the Azure portal.</span></span> <span data-ttu-id="9bc8f-127">Вы можете получить сертификаты непосредственно в центре сертификации и использовать их вместе со своими приложениями.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-127">You can obtain certificates directly from a certificate authority and use them with your apps.</span></span> <span data-ttu-id="9bc8f-128">Их нельзя получить на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-128">You can't obtain them through the Azure portal.</span></span>

## <a name="create-an-ilb-ase"></a><span data-ttu-id="9bc8f-129">Создание среды службы приложений с внутренней подсистемой балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="9bc8f-129">Create an ILB ASE</span></span> ##

<span data-ttu-id="9bc8f-130">Чтобы создать ASE с внутренним балансировщиком нагрузки, выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-130">To create an ILB ASE:</span></span>

1. <span data-ttu-id="9bc8f-131">На портале Azure выберите **Создать** > **Интернет+мобильные устройства** > **Среда службы приложений**.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-131">In the Azure portal, select **New** > **Web + Mobile** > **App Service Environment**.</span></span>

2. <span data-ttu-id="9bc8f-132">Выберите свою подписку.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-132">Select your subscription.</span></span>

3. <span data-ttu-id="9bc8f-133">Выберите или создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-133">Select or create a resource group.</span></span>

4. <span data-ttu-id="9bc8f-134">Выберите или создайте виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-134">Select or create a VNet.</span></span>

5. <span data-ttu-id="9bc8f-135">При выборе существующей виртуальной сети необходимо создать подсеть для размещения ASE.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-135">If you select an existing VNet, you need to create a subnet to hold the ASE.</span></span> <span data-ttu-id="9bc8f-136">Задайте для подсети достаточно большой размер с учетом увеличения среды службы приложений в будущем.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-136">Make sure to set a subnet size large enough to accommodate any future growth of your ASE.</span></span> <span data-ttu-id="9bc8f-137">Рекомендуемый размер — `/25`. Такая подсеть содержит 128 адресов и может обслуживать среду службы приложений максимального размера.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-137">We recommend a size of `/25`, which has 128 addresses and can handle a maximum-sized ASE.</span></span> <span data-ttu-id="9bc8f-138">Минимальный размер составляет `/28`.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-138">The minimum size you can select is a `/28`.</span></span> <span data-ttu-id="9bc8f-139">В соответствии с потребностями инфраструктуры этот размер может масштабироваться максимум до 11 экземпляров.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-139">After infrastructure needs, this size can be scaled to a maximum of 11 instances.</span></span>

    * <span data-ttu-id="9bc8f-140">Можно превысить максимальное количество в 100 экземпляров в планах службы приложений.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-140">Go beyond the default maximum of 100 instances in your App Service plans.</span></span>

    * <span data-ttu-id="9bc8f-141">Можно выполнить масштабирование примерно до 100 экземпляров, но путем более быстрого масштабирования внешнего интерфейса.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-141">Scale near 100 but with more rapid front-end scaling.</span></span>

6. <span data-ttu-id="9bc8f-142">Выберите **Виртуальная сеть/расположение** > **Конфигурация виртуальной сети**.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-142">Select **Virtual Network/Location** > **Virtual Network Configuration**.</span></span> <span data-ttu-id="9bc8f-143">Задайте для параметра **Тип VIP** значение **Внутренний**.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-143">Set the **VIP Type** to **Internal**.</span></span>

7. <span data-ttu-id="9bc8f-144">Введите имя домена.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-144">Enter a domain name.</span></span> <span data-ttu-id="9bc8f-145">Указанный домен будет использоваться для приложений, создаваемых в этой среде службы приложений.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-145">This domain is the one used for apps created in this ASE.</span></span> <span data-ttu-id="9bc8f-146">Существуют некоторые ограничения.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-146">There are some restrictions.</span></span> <span data-ttu-id="9bc8f-147">Нельзя использовать такие имена:</span><span class="sxs-lookup"><span data-stu-id="9bc8f-147">It can't be:</span></span>

    * <span data-ttu-id="9bc8f-148">net;</span><span class="sxs-lookup"><span data-stu-id="9bc8f-148">net</span></span>   

    * <span data-ttu-id="9bc8f-149">azurewebsites.net;</span><span class="sxs-lookup"><span data-stu-id="9bc8f-149">azurewebsites.net</span></span>

    * <span data-ttu-id="9bc8f-150">p.azurewebsites.net;</span><span class="sxs-lookup"><span data-stu-id="9bc8f-150">p.azurewebsites.net</span></span>

    * <span data-ttu-id="9bc8f-151">&lt;имя_ASE&gt;.p.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-151">&lt;asename&gt;.p.azurewebsites.net</span></span>

   <span data-ttu-id="9bc8f-152">Пользовательское имя домена, используемое для приложений, и имя домена, используемое средой ASE, не должны перекрываться.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-152">The custom domain name used for apps and the domain name used by your ASE can't overlap.</span></span> <span data-ttu-id="9bc8f-153">В среде ASE с внутренним балансировщиком нагрузки с доменным именем _contoso.com_ нельзя использовать следующие пользовательские доменные имена для приложений:</span><span class="sxs-lookup"><span data-stu-id="9bc8f-153">For an ILB ASE with the domain name _contoso.com_, you can't use custom domain names for your apps like:</span></span>

    * <span data-ttu-id="9bc8f-154">www.contoso.com;</span><span class="sxs-lookup"><span data-stu-id="9bc8f-154">www.contoso.com</span></span>

    * <span data-ttu-id="9bc8f-155">abcd.def.contoso.com;</span><span class="sxs-lookup"><span data-stu-id="9bc8f-155">abcd.def.contoso.com</span></span>

    * <span data-ttu-id="9bc8f-156">abcd.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-156">abcd.contoso.com</span></span>

   <span data-ttu-id="9bc8f-157">Если вы знаете, какие пользовательские доменные имена будете использовать для приложений, выберите для среды ASE с ILB домен, который не будет конфликтовать с этими именами.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-157">If you know the custom domain names for your apps, choose a domain for the ILB ASE that won’t have a conflict with those custom domain names.</span></span> <span data-ttu-id="9bc8f-158">В этом примере для домена ASE можно использовать такое имя, как *contoso-internal.com*, так как оно не конфликтует с пользовательскими доменными именами, которые заканчиваются на *.contoso.com*.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-158">In this example, you can use something like *contoso-internal.com* for the domain of your ASE because that won't conflict with custom domain names that end in *.contoso.com*.</span></span>

8. <span data-ttu-id="9bc8f-159">Щелкните **ОК**, а затем выберите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-159">Select **OK**, and then select **Create**.</span></span>

    ![создание ASE][1]

<span data-ttu-id="9bc8f-161">В колонке **Виртуальная сеть** есть параметр **Конфигурация виртуальной сети**.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-161">On the **Virtual Network** blade, there is a **Virtual Network Configuration** option.</span></span> <span data-ttu-id="9bc8f-162">Он позволяет выбрать внешний или внутренний виртуальный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-162">You can use it to select an External VIP or an Internal VIP.</span></span> <span data-ttu-id="9bc8f-163">По умолчанию используется значение **Внешний**.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-163">The default is **External**.</span></span> <span data-ttu-id="9bc8f-164">Если выбрать значение **Внешний**, для среды службы приложений будет использоваться виртуальный IP-адрес, доступный из Интернета.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-164">If you select **External**, your ASE uses an internet-accessible VIP.</span></span> <span data-ttu-id="9bc8f-165">Если выбрать **внутренний** виртуальный IP-адрес, то для ASE будет настроена внутренний балансировщик нагрузки с IP-адресом в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-165">If you select **Internal**, your ASE is configured with an ILB on an IP address within your VNet.</span></span>

<span data-ttu-id="9bc8f-166">После выбора варианта **Внутренний** возможность добавлять дополнительные IP-адреса для среды службы приложений исчезнет.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-166">After you select **Internal**, the ability to add more IP addresses to your ASE is removed.</span></span> <span data-ttu-id="9bc8f-167">Вместо этого необходимо будет указать домен ASE.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-167">Instead, you need to provide the domain of the ASE.</span></span> <span data-ttu-id="9bc8f-168">В ASE с внешним виртуальным IP-адресом имя среды указывается в домене для приложений, создаваемых в этой среде.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-168">In an ASE with an External VIP, the name of the ASE is used in the domain for apps created in that ASE.</span></span>

<span data-ttu-id="9bc8f-169">Если указан **Внутренний** **виртуальный IP-адрес**, имя среды ASE не используется в имени домена для этой среды.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-169">If you set **VIP Type** to **Internal**, your ASE name is not used in the domain for the ASE.</span></span> <span data-ttu-id="9bc8f-170">В этом случае домен указывается явным образом.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-170">You specify the domain explicitly.</span></span> <span data-ttu-id="9bc8f-171">Если используется домен *contoso.corp.net* и вы создали в этой среде ASE приложение с именем *timereporting*, URL-адрес этого приложения будет выглядеть так: timereporting.contoso.corp.net.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-171">If your domain is *contoso.corp.net* and you create an app in that ASE named *timereporting*, the URL for that app is timereporting.contoso.corp.net.</span></span>


## <a name="create-an-app-in-an-ilb-ase"></a><span data-ttu-id="9bc8f-172">Создание приложения в ASE с внутренним балансировщиком нагрузки</span><span class="sxs-lookup"><span data-stu-id="9bc8f-172">Create an app in an ILB ASE</span></span> ##

<span data-ttu-id="9bc8f-173">Создание приложения в обычной среде ASE и в ASE с внутренним балансировщиком нагрузки ничем не отличается.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-173">You create an app in an ILB ASE in the same way that you create an app in an ASE normally.</span></span>

1. <span data-ttu-id="9bc8f-174">На портале Azure выберите **Создать** > **Интернет+мобильные устройства** > **Интернет**, **Мобильные** или **Приложение API**.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-174">In the Azure portal, select **New** > **Web + Mobile** > **Web** or **Mobile** or **API App**.</span></span>

2. <span data-ttu-id="9bc8f-175">Введите имя приложения.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-175">Enter the name of the app.</span></span>

3. <span data-ttu-id="9bc8f-176">Выберите подписку.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-176">Select the subscription.</span></span>

4. <span data-ttu-id="9bc8f-177">Выберите или создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-177">Select or create a resource group.</span></span>

5. <span data-ttu-id="9bc8f-178">Выбор или создание плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="9bc8f-178">Select or create an App Service plan.</span></span> <span data-ttu-id="9bc8f-179">Если необходимо создать план службы приложений, выберите свою среду ASE в качестве расположения.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-179">If you want to create a new App Service plan, select your ASE as the location.</span></span> <span data-ttu-id="9bc8f-180">Выберите рабочий пул, в котором будет создан этот план.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-180">Select the worker pool where you want your App Service plan to be created.</span></span> <span data-ttu-id="9bc8f-181">При создании плана службы приложений следует выбрать ASE в качестве расположения и рабочий пул.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-181">When you create the App Service plan, select your ASE as the location and the worker pool.</span></span> <span data-ttu-id="9bc8f-182">При указании имени приложения домен в имени вашего приложения заменяется доменом ASE.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-182">When you specify the name of the app, the domain under your app name is replaced by the domain for your ASE.</span></span>

6. <span data-ttu-id="9bc8f-183">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-183">Select **Create**.</span></span> <span data-ttu-id="9bc8f-184">Если требуется отобразить приложение на панели мониторинга, следует установить флажок **Закрепить на панели мониторинга**.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-184">If you want the app to appear on your dashboard, select the **Pin to dashboard** check box.</span></span>

    ![Создание плана служб приложений][2]

    <span data-ttu-id="9bc8f-186">Доменное имя в **имени приложения** обновится с учетом домена ASE.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-186">Under **App name**, the domain name is updated to reflect the domain of your ASE.</span></span>

## <a name="post-ilb-ase-creation-validation"></a><span data-ttu-id="9bc8f-187">Проверка после создания ASE с внутренним балансировщиком нагрузки</span><span class="sxs-lookup"><span data-stu-id="9bc8f-187">Post-ILB ASE creation validation</span></span> ##

<span data-ttu-id="9bc8f-188">ASE с внутренним балансировщиком нагрузки немного отличается от ASE без такового.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-188">An ILB ASE is slightly different than the non-ILB ASE.</span></span> <span data-ttu-id="9bc8f-189">Как уже было сказано, вам нужно управлять собственной службой DNS.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-189">As already noted, you need to manage your own DNS.</span></span> <span data-ttu-id="9bc8f-190">Также необходимо предоставить собственный сертификат для подключений по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-190">You also have to provide your own certificate for HTTPS connections.</span></span>

<span data-ttu-id="9bc8f-191">После создания среды ASE вы заметите, что в доменном имени отображается указанный вами домен.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-191">After you create your ASE, the domain name shows the domain you specified.</span></span> <span data-ttu-id="9bc8f-192">В меню **Параметры** появился новый пункт **Сертификат ILB**.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-192">A new item appears in the **Setting** menu called **ILB Certificate**.</span></span> <span data-ttu-id="9bc8f-193">ASE создается с сертификатом, в котором не указан домен ASE с ILB.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-193">The ASE is created with a certificate that doesn't specify the ILB ASE domain.</span></span> <span data-ttu-id="9bc8f-194">Если использовать ASE с этим сертификатом, в браузере отобразится сообщение о том, что указан недопустимый сертификат.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-194">If you use the ASE with that certificate, your browser tells you that it's invalid.</span></span> <span data-ttu-id="9bc8f-195">Этот сертификат упрощает тестирование протокола HTTPS. Но вам необходимо отправить собственный сертификат, связанный с доменом ASE с внутренним балансировщиком нагрузки.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-195">This certificate makes it easier to test HTTPS, but you need to upload your own certificate that's tied to your ILB ASE domain.</span></span> <span data-ttu-id="9bc8f-196">Этот шаг является обязательным независимо от типа сертификата: самозаверяющий или получен из ЦС.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-196">This step is necessary regardless of whether your certificate is self-signed or acquired from a certificate authority.</span></span>

![Имя домена ASE с ILB][3]

<span data-ttu-id="9bc8f-198">Для ASE с внутренним балансировщиком нагрузки требуется допустимый сертификат SSL.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-198">Your ILB ASE needs a valid SSL certificate.</span></span> <span data-ttu-id="9bc8f-199">Можно получить сертификат от внутреннего центра сертификации, приобрести его у внешнего поставщика и использовать самозаверяющий сертификат.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-199">Use internal certificate authorities, purchase a certificate from an external issuer, or use a self-signed certificate.</span></span> <span data-ttu-id="9bc8f-200">Независимо от источника SSL-сертификата для него необходимо соответствующим образом настроить следующие атрибуты:</span><span class="sxs-lookup"><span data-stu-id="9bc8f-200">Regardless of the source of the SSL certificate, the following certificate attributes need to be configured properly:</span></span>

* <span data-ttu-id="9bc8f-201">**Subject** — для этого атрибута необходимо задать значение *.имя_корневого_домена.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-201">**Subject**: This attribute must be set to *.your-root-domain-here.</span></span>
* <span data-ttu-id="9bc8f-202">**Subject Alternative Name** — этот атрибут должен содержать два значения: **.имя_корневого_домена* и **.scm.имя_корневого_домена*.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-202">**Subject Alternative Name**: This attribute must include both **.your-root-domain-here* and **.scm.your-root-domain-here*.</span></span> <span data-ttu-id="9bc8f-203">Для SSL-соединения с сайтом SCM или Kudu, связанным с каждым приложением, будет использоваться адрес в формате *имя_приложения.scm.имя_корневого_домена*.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-203">SSL connections to the SCM/Kudu site associated with each app use an address of the form *your-app-name.scm.your-root-domain-here*.</span></span>

<span data-ttu-id="9bc8f-204">SSL-сертификат необходимо преобразовать в PFX-файл и сохранить в таком формате.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-204">Convert/save the SSL certificate as a .pfx file.</span></span> <span data-ttu-id="9bc8f-205">PFX-файл должен содержать все промежуточные и корневые сертификаты.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-205">The .pfx file must include all intermediate and root certificates.</span></span> <span data-ttu-id="9bc8f-206">Защитите его паролем.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-206">Secure it with a password.</span></span>

<span data-ttu-id="9bc8f-207">Чтобы создать собственный сертификат, можно использовать приведенные ниже команды PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-207">If you want to create a self-signed certificate, you can use the PowerShell commands here.</span></span> <span data-ttu-id="9bc8f-208">Обязательно укажите доменное имя среды ASE с ILB вместо *internal.contoso.com*.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-208">Be sure to use your ILB ASE domain name instead of *internal.contoso.com*:</span></span> 

    $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "\*.internal-contoso.com","\*.scm.internal-contoso.com"
    
    $certThumbprint = "cert:\localMachine\my\" +$certificate.Thumbprint
    $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText
    
    $fileName = "exportedcert.pfx" 
    Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password

<span data-ttu-id="9bc8f-209">Сертификат, созданный с помощью этих команд PowerShell, по-прежнему будет вызывать ошибку в браузерах, так как он не был создан ЦС из цепочки сертификатов браузера.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-209">The certificate that these PowerShell commands generate is flagged by browsers because the certificate wasn't created by a certificate authority that's in your browser's chain of trust.</span></span> <span data-ttu-id="9bc8f-210">Чтобы получить сертификат, которому доверяет браузер, необходимо приобрести его в коммерческом ЦС из цепочки сертификатов браузера.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-210">To get a certificate that your browser trusts, procure it from a commercial certificate authority in your browser's chain of trust.</span></span> 

![Задание сертификата ILB][4]

<span data-ttu-id="9bc8f-212">Чтобы отправить сертификаты и протестировать доступ, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="9bc8f-212">To upload your own certificates and test access:</span></span>

1. <span data-ttu-id="9bc8f-213">Перейдите к пользовательскому интерфейсу среды ASE после ее создания.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-213">After the ASE is created, go to the ASE UI.</span></span> <span data-ttu-id="9bc8f-214">Выберите **ASE** > **Параметры** > **Сертификат ILB**.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-214">Select **ASE** > **Settings** > **ILB Certificate**.</span></span>

2. <span data-ttu-id="9bc8f-215">Задайте сертификат ILB, выбрав PFX-файл сертификата, и введите пароль.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-215">To set the ILB certificate, select the certificate .pfx file and enter the password.</span></span> <span data-ttu-id="9bc8f-216">На выполнение этой операции потребуется некоторое время.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-216">This step takes some time to process.</span></span> <span data-ttu-id="9bc8f-217">Появится сообщение о том, что выполняется отправка.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-217">A message appears stating that an upload operation is in progress.</span></span>

3. <span data-ttu-id="9bc8f-218">Получите адрес ILB для ASE.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-218">Get the ILB address for your ASE.</span></span> <span data-ttu-id="9bc8f-219">Выберите **ASE** > **Свойства** > **Виртуальный IP-адрес**.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-219">Select **ASE** > **Properties** > **Virtual IP Address**.</span></span>

4. <span data-ttu-id="9bc8f-220">Создайте веб-приложение в среде ASE после ее создания.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-220">Create a web app in your ASE after the ASE is created.</span></span>

5. <span data-ttu-id="9bc8f-221">Создайте виртуальную машину в этой виртуальной сети (если вы этого еще не сделали).</span><span class="sxs-lookup"><span data-stu-id="9bc8f-221">Create a VM if you don't have one in that VNet.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9bc8f-222">Не создавайте виртуальную машину в одной подсети с ASE. В противном случае настройка будет прервана или возникнут проблемы.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-222">Don't try to create this VM in the same subnet as the ASE because it will fail or cause problems.</span></span>
    >
    >

6. <span data-ttu-id="9bc8f-223">Задайте DNS для домена среды ASE.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-223">Set the DNS for your ASE domain.</span></span> <span data-ttu-id="9bc8f-224">Можно указать в DNS подстановочные знаки с именем домена.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-224">You can use a wildcard with your domain in your DNS.</span></span> <span data-ttu-id="9bc8f-225">Чтобы выполнить несколько простых проверок, можно изменить файл hosts на виртуальной машине, чтобы в качестве имени веб-приложения задать виртуальный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-225">To do some simple tests, edit the hosts file on your VM to set the web app name to the VIP IP address:</span></span>

    <span data-ttu-id="9bc8f-226">а.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-226">a.</span></span> <span data-ttu-id="9bc8f-227">Если доменное имя вашей среды ASE — _.ilbase.com_ и вы создали веб-приложение с именем _mytestapp_, его адрес — _mytestapp.ilbase.com_. Позднее вы настроите разрешение имени _mytestapp.ilbase.com_ в адрес ILB.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-227">If your ASE has the domain name _.ilbase.com_ and you create the web app named _mytestapp_, it's addressed at _mytestapp.ilbase.com_. You then set _mytestapp.ilbase.com_ to resolve to the ILB address.</span></span> <span data-ttu-id="9bc8f-228">(В Windows файл hosts находится в папке C:\Windows\System32\drivers\…\_)</span><span class="sxs-lookup"><span data-stu-id="9bc8f-228">(On Windows, the hosts file is at _C:\Windows\System32\drivers\etc\_.)</span></span>

    <span data-ttu-id="9bc8f-229">b.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-229">b.</span></span> <span data-ttu-id="9bc8f-230">Чтобы протестировать публикацию веб-развертывания или доступ к расширенной консоли, создайте запись для _mytestapp.scm.ilbase.com_.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-230">To test web deployment publishing or access to the advanced console, create a record for _mytestapp.scm.ilbase.com_.</span></span>

7. <span data-ttu-id="9bc8f-231">Откройте браузер на этой виртуальной машине и перейдите по адресу http://mytestapp.ilbase.com. (Или перейдите к любому имени веб-приложения в вашем домене.)</span><span class="sxs-lookup"><span data-stu-id="9bc8f-231">Use a browser on that VM and go to http://mytestapp.ilbase.com. (Or go to whatever your web app name is with your domain.)</span></span>

8. <span data-ttu-id="9bc8f-232">Откройте браузер на этой виртуальной машине и перейдите по адресу https://mytestapp.ilbase.com. Если используется самозаверяющий сертификат, учтите, что уровень безопасности будет снижен.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-232">Use a browser on that VM and go to https://mytestapp.ilbase.com. If you use a self-signed certificate, accept the lack of security.</span></span>

    <span data-ttu-id="9bc8f-233">IP-адрес ILB указан в разделе **IP-адреса**.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-233">The IP address for your ILB is listed under **IP addresses**.</span></span> <span data-ttu-id="9bc8f-234">В нем также указаны внешние виртуальные IP-адреса и IP-адреса для входящего трафика управления.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-234">This list also has the IP addresses used by the external VIP and for inbound management traffic.</span></span>

    ![IP-адрес ILB][5]

### <a name="web-jobs-functions-and-the-ilb-ase"></a><span data-ttu-id="9bc8f-236">Веб-задания, функции и ASE с ILB</span><span class="sxs-lookup"><span data-stu-id="9bc8f-236">Web jobs, Functions and the ILB ASE</span></span>

<span data-ttu-id="9bc8f-237">Функции и веб-задания поддерживаются в ASE с ILB, но чтобы работать с ними на портале, необходимо иметь сетевой доступ к сайту диспетчера служб.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-237">Both Functions and web jobs are supported on an ILB ASE but for the portal to work with them, you must have network access to the SCM site.</span></span>  <span data-ttu-id="9bc8f-238">Это означает, что браузер должен быть запущен на узле, который либо находится в виртуальной сети, либо подключен к ней.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-238">This means your browser must either be on a host that is either in or connected to the virtual network.</span></span>  

<span data-ttu-id="9bc8f-239">При использовании Функций Azure в среде ASE с ILB может возникнуть сообщение об ошибке "Сейчас не удается извлечь ваши функции.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-239">When you use Azure Functions on an ILB ASE, you might get an error message that says "We are not able to retrieve your functions right now.</span></span> <span data-ttu-id="9bc8f-240">Повторите попытку позже".</span><span class="sxs-lookup"><span data-stu-id="9bc8f-240">Please try again later."</span></span> <span data-ttu-id="9bc8f-241">Эта ошибка возникает, так как пользовательский интерфейс функций использует сайт диспетчера служб через протокол HTTPS, а корневой сертификат не находится цепочке сертификатов браузера.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-241">This error occurs because the Functions UI leverages the SCM site over HTTPS and the root certificate is not in the browser chain of trust.</span></span> <span data-ttu-id="9bc8f-242">Веб-задания могут вызывать подобную проблему.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-242">Web jobs has a similar problem.</span></span> <span data-ttu-id="9bc8f-243">Чтобы избежать этой проблемы, выполните одно из следующих действий.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-243">To avoid this problem you can do one of the following:</span></span>

- <span data-ttu-id="9bc8f-244">Добавьте сертификат в хранилище доверенных сертификатов.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-244">Add the certificate to your trusted certificate store.</span></span> <span data-ttu-id="9bc8f-245">Это позволит разблокировать Edge и Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-245">This unblocks Edge and Internet Explorer.</span></span>
- <span data-ttu-id="9bc8f-246">Сначала в Chrome перейдите на сайт диспетчера служб, примите недоверенный сертификат, а затем перейти на портал.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-246">Use Chrome and go to the SCM site first, accept the untrusted certificate and then go to the portal.</span></span>
- <span data-ttu-id="9bc8f-247">Используйте коммерческий сертификат, который находится в цепочке сертификатов браузера.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-247">Use a commercial certificate that is in your browser chain of trust.</span></span>  <span data-ttu-id="9bc8f-248">Это наилучший вариант.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-248">This is the best option.</span></span>  

## <a name="dns-configuration"></a><span data-ttu-id="9bc8f-249">Настройка DNS</span><span class="sxs-lookup"><span data-stu-id="9bc8f-249">DNS configuration</span></span> ##

<span data-ttu-id="9bc8f-250">При использовании внешнего виртуального IP-адреса службой DNS управляет Azure.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-250">When you use an External VIP, the DNS is managed by Azure.</span></span> <span data-ttu-id="9bc8f-251">Любое приложение, созданное в ASE, автоматически добавляется в службу DNS Azure, которая является общедоступной.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-251">Any app created in your ASE is automatically added to Azure DNS, which is a public DNS.</span></span> <span data-ttu-id="9bc8f-252">В ASE с ILB необходимо управлять собственной службой DNS.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-252">In an ILB ASE, you must manage your own DNS.</span></span> <span data-ttu-id="9bc8f-253">Для заданного домена, например _contoso.net_, необходимо создать записи А в DNS, указывающие на адрес ILB, для:</span><span class="sxs-lookup"><span data-stu-id="9bc8f-253">For a given domain such as _contoso.net_, you need to create DNS A records in your DNS that point to your ILB address for:</span></span>

- <span data-ttu-id="9bc8f-254">*.contoso.net;</span><span class="sxs-lookup"><span data-stu-id="9bc8f-254">*.contoso.net</span></span>
- <span data-ttu-id="9bc8f-255">*.scm.contoso.net.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-255">*.scm.contoso.net</span></span>

<span data-ttu-id="9bc8f-256">Если домен среды ASE с ILB используется для нескольких операций за пределами этой среды, может потребоваться управлять службой DNS для каждого имени приложения.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-256">If your ILB ASE domain is used for multiple things outside this ASE, you might need to manage DNS on a per-app-name basis.</span></span> <span data-ttu-id="9bc8f-257">Это усложняет задачу, так как необходимо добавлять имя каждого нового приложения в службу DNS при его создании.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-257">This method is challenging because you need to add each new app name into your DNS when you create it.</span></span> <span data-ttu-id="9bc8f-258">По этой причине рекомендуется использовать выделенный домен.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-258">For this reason, we recommend that you use a dedicated domain.</span></span>

## <a name="publish-with-an-ilb-ase"></a><span data-ttu-id="9bc8f-259">Публикация с использованием ASE с внутренним балансировщиком нагрузки</span><span class="sxs-lookup"><span data-stu-id="9bc8f-259">Publish with an ILB ASE</span></span> ##

<span data-ttu-id="9bc8f-260">Для каждого создаваемого приложения предоставляются две конечные точки.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-260">For every app that's created, there are two endpoints.</span></span> <span data-ttu-id="9bc8f-261">В ASE с ILB это *&lt;имя_приложения>.&lt;домен_ASE_с_ILB>* и *&lt;имя_приложения>.scm.&lt;домен_ASE_с_ILB>*.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-261">In an ILB ASE, you have *&lt;app name>.&lt;ILB ASE Domain>* and *&lt;app name>.scm.&lt;ILB ASE Domain>*.</span></span> 

<span data-ttu-id="9bc8f-262">Если выбрать имя сайта SCM, вы перейдете в консоль Kudu, которая называется **расширенным порталом**, на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-262">The SCM site name takes you to the Kudu console, called the **Advanced portal**, within the Azure portal.</span></span> <span data-ttu-id="9bc8f-263">Консоль Kudu позволяет просматривать переменные среды, просматривать данные диска, использовать консоль и многое другое.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-263">The Kudu console lets you view environment variables, explore the disk, use a console, and much more.</span></span> <span data-ttu-id="9bc8f-264">Дополнительные сведения см. на странице, посвященной [консоли Kudu для службы приложений Azure][Kudu].</span><span class="sxs-lookup"><span data-stu-id="9bc8f-264">For more information, see [Kudu console for Azure App Service][Kudu].</span></span> 

<span data-ttu-id="9bc8f-265">В мультитенантной службе приложений и внешней среде ASE применяется единый вход между порталом Azure и консолью Kudu.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-265">In the multitenant App Service and in an External ASE, there's single sign-on between the Azure portal and the Kudu console.</span></span> <span data-ttu-id="9bc8f-266">Тем не менее в среде ASE с ILB необходимо использовать учетные данные публикации для входа в консоль Kudu.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-266">For the ILB ASE, however, you need to use your publishing credentials to sign into the Kudu console.</span></span>

<span data-ttu-id="9bc8f-267">Веб-системы непрерывной интеграции, такие как GitHub и Visual Studio Team Services, не работают со средой ASE с ILB, так как конечная точка публикации недоступна через Интернет.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-267">Internet-based CI systems, such as GitHub and Visual Studio Team Services, don't work with an ILB ASE because the publishing endpoint isn't internet accessible.</span></span> <span data-ttu-id="9bc8f-268">Вместо этого необходимо использовать систему непрерывной интеграции, в которой применяется модель полного извлечения, например Dropbox.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-268">Instead, you need to use a CI system that uses a pull model, such as Dropbox.</span></span>

<span data-ttu-id="9bc8f-269">Для конечных точек публикации приложений в среде ASE с ILB используется домен, созданный вместе со средой.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-269">The publishing endpoints for apps in an ILB ASE use the domain that the ILB ASE was created with.</span></span> <span data-ttu-id="9bc8f-270">Этот домен можно увидеть в профиле публикации приложения и в колонке приложения на портале (в разделе **Обзор** > **Основное** и в разделе **Свойства**).</span><span class="sxs-lookup"><span data-stu-id="9bc8f-270">This domain appears in the app's publishing profile and in the app's portal blade (**Overview** > **Essentials** and also **Properties**).</span></span> <span data-ttu-id="9bc8f-271">При наличии среды ASE с ILB с поддоменом *contoso.net* и приложения с именем *mytest* вы перейдете по протоколу FTP по адресу *mytest.contoso.net* и выполните веб-развертывание по адресу *mytest.scm.contoso.net*.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-271">If you have an ILB ASE with the subdomain *contoso.net* and an app named *mytest*, use *mytest.contoso.net* for FTP and *mytest.scm.contoso.net* for web deployment.</span></span>

## <a name="couple-an-ilb-ase-with-a-waf-device"></a><span data-ttu-id="9bc8f-272">Взаимозависимость среды ASE с внутренним балансировщиком нагрузки и устройства WAF</span><span class="sxs-lookup"><span data-stu-id="9bc8f-272">Couple an ILB ASE with a WAF device</span></span> ##

<span data-ttu-id="9bc8f-273">Служба приложений Azure предоставляет множество мер безопасности для защиты системы.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-273">Azure App Service provides many security measures that protect the system.</span></span> <span data-ttu-id="9bc8f-274">Она также помогает определить, было ли взломано приложение.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-274">They also help to determine whether an app was hacked.</span></span> <span data-ttu-id="9bc8f-275">Лучший способ защиты веб-приложения — создание зависимости между платформой размещения, например службой приложений Azure, и брандмауэром веб-приложения (WAF).</span><span class="sxs-lookup"><span data-stu-id="9bc8f-275">The best protection for a web application is to couple a hosting platform, such as Azure App Service, with a web application firewall (WAF).</span></span> <span data-ttu-id="9bc8f-276">Так как конечная точка приложения в среде ASE с ILB изолирована от сети, этот способ подойдет идеально.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-276">Because the ILB ASE has a network-isolated application endpoint, it's appropriate for such a use.</span></span>

<span data-ttu-id="9bc8f-277">Дополнительные сведения о настройке ASE с ILB и устройства WAF см. в статье [Настройка брандмауэра веб-приложения (WAF) для среды службы приложений][ASEWAF].</span><span class="sxs-lookup"><span data-stu-id="9bc8f-277">To learn more about how to configure your ILB ASE with a WAF device, see [Configure a web application firewall with your App Service environment][ASEWAF].</span></span> <span data-ttu-id="9bc8f-278">В этой статье объясняется, как использовать виртуальный модуль Barracuda со средой ASE.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-278">This article shows how to use a Barracuda virtual appliance with your ASE.</span></span> <span data-ttu-id="9bc8f-279">Другой способ — использовать шлюз приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-279">Another option is to use Azure Application Gateway.</span></span> <span data-ttu-id="9bc8f-280">Шлюз приложений использует основные правила OWASP для защиты всех приложений, размещенных за этим шлюзом.</span><span class="sxs-lookup"><span data-stu-id="9bc8f-280">Application Gateway uses the OWASP core rules to secure any applications placed behind it.</span></span> <span data-ttu-id="9bc8f-281">Дополнительные сведения о шлюзе приложений см. в статье [Брандмауэр веб-приложения (WAF)][AppGW].</span><span class="sxs-lookup"><span data-stu-id="9bc8f-281">For more information about Application Gateway, see [Introduction to the Azure web application firewall][AppGW].</span></span>

## <a name="get-started"></a><span data-ttu-id="9bc8f-282">Начало работы</span><span class="sxs-lookup"><span data-stu-id="9bc8f-282">Get started</span></span> ##

<span data-ttu-id="9bc8f-283">Все статьи о средах ASE и соответствующие пошаговые инструкции доступны в [файле сведений для сред службы приложений][ASEReadme].</span><span class="sxs-lookup"><span data-stu-id="9bc8f-283">All articles and how-to instructions for ASEs are available in the [README for App Service environments][ASEReadme].</span></span>

* <span data-ttu-id="9bc8f-284">Сведения о том, как начать работу со средами службы приложений, см. в статье [Общие сведения о среде службы приложений][Intro].</span><span class="sxs-lookup"><span data-stu-id="9bc8f-284">To get started with ASEs, see [Introduction to App Service environments][Intro].</span></span>
* <span data-ttu-id="9bc8f-285">Дополнительные сведения о платформе службы приложений Azure см. в [этой статье](http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/).</span><span class="sxs-lookup"><span data-stu-id="9bc8f-285">For more information about the Azure App Service platform, see [Azure App Service](http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/).</span></span>
 
<!--Image references-->
[1]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-network.png
[2]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-webapp.png
[3]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-certificate.png
[4]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-certificate2.png
[5]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-ipaddresses.png

<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
