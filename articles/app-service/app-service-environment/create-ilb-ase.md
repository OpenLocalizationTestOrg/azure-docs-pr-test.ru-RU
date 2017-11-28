---
title: "aaaCreate и использование внутренней подсистемы балансировки нагрузки с среду службы приложений Azure"
description: "Сведения о том, как toocreate и использование изолированной от Интернета среды службы приложений Azure"
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
ms.openlocfilehash: d019ca6f231c3acfdab4cd380db375a076802f7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-use-an-internal-load-balancer-with-an-app-service-environment"></a><span data-ttu-id="f272e-103">Создание и использование внутреннего балансировщика нагрузки со средой службы приложений</span><span class="sxs-lookup"><span data-stu-id="f272e-103">Create and use an internal load balancer with an App Service environment</span></span> #

 <span data-ttu-id="f272e-104">Среда службы приложений — это развернутая служба приложений Azure в подсети виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="f272e-104">Azure App Service Environment is a deployment of Azure App Service into a subnet in an Azure virtual network (VNet).</span></span> <span data-ttu-id="f272e-105">Существует два способа toodeploy среду службы приложений (ASE):</span><span class="sxs-lookup"><span data-stu-id="f272e-105">There are two ways toodeploy an App Service environment (ASE):</span></span> 

- <span data-ttu-id="f272e-106">с виртуальным IP-адресом на основе внешнего IP-адреса, что часто называют внешней средой ASE;</span><span class="sxs-lookup"><span data-stu-id="f272e-106">With a VIP on an external IP address, often called an External ASE.</span></span>
- <span data-ttu-id="f272e-107">VIP-адрес, на внутренний IP-адрес часто называют ILB ASE, поскольку внутренняя Подсистема балансировки нагрузки (ILB) hello внутренней конечной точки.</span><span class="sxs-lookup"><span data-stu-id="f272e-107">With a VIP on an internal IP address, often called an ILB ASE because hello internal endpoint is an internal load balancer (ILB).</span></span> 

<span data-ttu-id="f272e-108">В этой статье показано, как toocreate ILB ASE.</span><span class="sxs-lookup"><span data-stu-id="f272e-108">This article shows you how toocreate an ILB ASE.</span></span> <span data-ttu-id="f272e-109">Обзор на hello ASE см. в разделе [введение среды службы tooApp][Intro].</span><span class="sxs-lookup"><span data-stu-id="f272e-109">For an overview on hello ASE, see [Introduction tooApp Service environments][Intro].</span></span> <span data-ttu-id="f272e-110">статье toocreate внешних ASE toolearn [Создание внешних ASE][MakeExternalASE].</span><span class="sxs-lookup"><span data-stu-id="f272e-110">toolearn how toocreate an External ASE, see [Create an External ASE][MakeExternalASE].</span></span>

## <a name="overview"></a><span data-ttu-id="f272e-111">Обзор</span><span class="sxs-lookup"><span data-stu-id="f272e-111">Overview</span></span> ##

<span data-ttu-id="f272e-112">Вы можете развернуть ASE с конечной точкой, доступной из Интернета, или IP-адресом в вашей виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="f272e-112">You can deploy an ASE with an internet-accessible endpoint or with an IP address in your VNet.</span></span> <span data-ttu-id="f272e-113">tooset в hello IP-адресов tooa адрес виртуальной сети, приветствия ASE должны быть развернуты вместе с ILB.</span><span class="sxs-lookup"><span data-stu-id="f272e-113">tooset hello IP address tooa VNet address, hello ASE must be deployed with an ILB.</span></span> <span data-ttu-id="f272e-114">При развертывании среды службы приложений с внутренним балансировщиком нагрузки необходимо наличие следующих компонентов:</span><span class="sxs-lookup"><span data-stu-id="f272e-114">When you deploy your ASE with an ILB, you must provide:</span></span>

-   <span data-ttu-id="f272e-115">Ваш собственный домен, в котором создаются приложения.</span><span class="sxs-lookup"><span data-stu-id="f272e-115">Your own domain that you use when you create your apps.</span></span>
-   <span data-ttu-id="f272e-116">Hello сертификат, используемый для HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f272e-116">hello certificate used for HTTPS.</span></span>
-   <span data-ttu-id="f272e-117">Управление службой DNS для домена.</span><span class="sxs-lookup"><span data-stu-id="f272e-117">DNS management for your domain.</span></span>

<span data-ttu-id="f272e-118">Это дает следующие возможности:</span><span class="sxs-lookup"><span data-stu-id="f272e-118">In return, you can do things such as:</span></span>

-   <span data-ttu-id="f272e-119">Узел приложения интрасети безопасно в облаке hello, доступ к которому осуществляется через сайт сайт или Azure ExpressRoute VPN.</span><span class="sxs-lookup"><span data-stu-id="f272e-119">Host intranet applications securely in hello cloud, which you access through a site-to-site or Azure ExpressRoute VPN.</span></span>
-   <span data-ttu-id="f272e-120">Приложения узлов в облаке hello, не перечисленным в общедоступные DNS-серверы.</span><span class="sxs-lookup"><span data-stu-id="f272e-120">Host apps in hello cloud that aren't listed in public DNS servers.</span></span>
-   <span data-ttu-id="f272e-121">Создание изолированных от Интернета внутренних приложений, с которыми можно безопасно интегрировать свои внешние приложения.</span><span class="sxs-lookup"><span data-stu-id="f272e-121">Create internet-isolated back-end apps, which your front-end apps can securely integrate with.</span></span>

### <a name="disabled-functionality"></a><span data-ttu-id="f272e-122">Отключенные функциональные возможности</span><span class="sxs-lookup"><span data-stu-id="f272e-122">Disabled functionality</span></span> ###

<span data-ttu-id="f272e-123">Существуют некоторые функции, недоступные при использовании ASE с внутренним балансировщиком нагрузки.</span><span class="sxs-lookup"><span data-stu-id="f272e-123">There are some things that you can't do when you use an ILB ASE:</span></span>

-   <span data-ttu-id="f272e-124">Использование SSL на основе IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="f272e-124">Use IP-based SSL.</span></span>
-   <span data-ttu-id="f272e-125">Назначьте IP-адреса toospecific приложений.</span><span class="sxs-lookup"><span data-stu-id="f272e-125">Assign IP addresses toospecific apps.</span></span>
-   <span data-ttu-id="f272e-126">Приобретение и использование сертификата с помощью приложения через портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f272e-126">Buy and use a certificate with an app through hello Azure portal.</span></span> <span data-ttu-id="f272e-127">Вы можете получить сертификаты непосредственно в центре сертификации и использовать их вместе со своими приложениями.</span><span class="sxs-lookup"><span data-stu-id="f272e-127">You can obtain certificates directly from a certificate authority and use them with your apps.</span></span> <span data-ttu-id="f272e-128">Не удается получить их через портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f272e-128">You can't obtain them through hello Azure portal.</span></span>

## <a name="create-an-ilb-ase"></a><span data-ttu-id="f272e-129">Создание среды службы приложений с внутренней подсистемой балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="f272e-129">Create an ILB ASE</span></span> ##

<span data-ttu-id="f272e-130">toocreate ILB ASE:</span><span class="sxs-lookup"><span data-stu-id="f272e-130">toocreate an ILB ASE:</span></span>

1. <span data-ttu-id="f272e-131">В hello портал Azure, выберите **New** > **Интернет + мобильные устройства** > **среды службы приложений**.</span><span class="sxs-lookup"><span data-stu-id="f272e-131">In hello Azure portal, select **New** > **Web + Mobile** > **App Service Environment**.</span></span>

2. <span data-ttu-id="f272e-132">Выберите свою подписку.</span><span class="sxs-lookup"><span data-stu-id="f272e-132">Select your subscription.</span></span>

3. <span data-ttu-id="f272e-133">Выберите или создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f272e-133">Select or create a resource group.</span></span>

4. <span data-ttu-id="f272e-134">Выберите или создайте виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="f272e-134">Select or create a VNet.</span></span>

5. <span data-ttu-id="f272e-135">При выборе существующей виртуальной сети необходимо toocreate hello toohold подсети ASE.</span><span class="sxs-lookup"><span data-stu-id="f272e-135">If you select an existing VNet, you need toocreate a subnet toohold hello ASE.</span></span> <span data-ttu-id="f272e-136">Убедитесь, что tooset подсети размер достаточно большой tooaccommodate к дальнейшему росту Вашего ASE.</span><span class="sxs-lookup"><span data-stu-id="f272e-136">Make sure tooset a subnet size large enough tooaccommodate any future growth of your ASE.</span></span> <span data-ttu-id="f272e-137">Рекомендуемый размер — `/25`. Такая подсеть содержит 128 адресов и может обслуживать среду службы приложений максимального размера.</span><span class="sxs-lookup"><span data-stu-id="f272e-137">We recommend a size of `/25`, which has 128 addresses and can handle a maximum-sized ASE.</span></span> <span data-ttu-id="f272e-138">можно выбрать минимальный размер Hello — `/28`.</span><span class="sxs-lookup"><span data-stu-id="f272e-138">hello minimum size you can select is a `/28`.</span></span> <span data-ttu-id="f272e-139">После должен инфраструктуры, этот размер может быть более масштабированный tooa 11 экземпляров.</span><span class="sxs-lookup"><span data-stu-id="f272e-139">After infrastructure needs, this size can be scaled tooa maximum of 11 instances.</span></span>

    * <span data-ttu-id="f272e-140">Выходят за рамки максимум 100 экземпляров по умолчанию hello в планах службы приложений.</span><span class="sxs-lookup"><span data-stu-id="f272e-140">Go beyond hello default maximum of 100 instances in your App Service plans.</span></span>

    * <span data-ttu-id="f272e-141">Можно выполнить масштабирование примерно до 100 экземпляров, но путем более быстрого масштабирования внешнего интерфейса.</span><span class="sxs-lookup"><span data-stu-id="f272e-141">Scale near 100 but with more rapid front-end scaling.</span></span>

6. <span data-ttu-id="f272e-142">Выберите **Виртуальная сеть/расположение** > **Конфигурация виртуальной сети**.</span><span class="sxs-lookup"><span data-stu-id="f272e-142">Select **Virtual Network/Location** > **Virtual Network Configuration**.</span></span> <span data-ttu-id="f272e-143">Набор hello **тип виртуального IP-адреса** слишком**внутренний**.</span><span class="sxs-lookup"><span data-stu-id="f272e-143">Set hello **VIP Type** too**Internal**.</span></span>

7. <span data-ttu-id="f272e-144">Введите имя домена.</span><span class="sxs-lookup"><span data-stu-id="f272e-144">Enter a domain name.</span></span> <span data-ttu-id="f272e-145">Привет, другая — для приложений, созданных в этом ASE является этот домен.</span><span class="sxs-lookup"><span data-stu-id="f272e-145">This domain is hello one used for apps created in this ASE.</span></span> <span data-ttu-id="f272e-146">Существуют некоторые ограничения.</span><span class="sxs-lookup"><span data-stu-id="f272e-146">There are some restrictions.</span></span> <span data-ttu-id="f272e-147">Нельзя использовать такие имена:</span><span class="sxs-lookup"><span data-stu-id="f272e-147">It can't be:</span></span>

    * <span data-ttu-id="f272e-148">net;</span><span class="sxs-lookup"><span data-stu-id="f272e-148">net</span></span>   

    * <span data-ttu-id="f272e-149">azurewebsites.net;</span><span class="sxs-lookup"><span data-stu-id="f272e-149">azurewebsites.net</span></span>

    * <span data-ttu-id="f272e-150">p.azurewebsites.net;</span><span class="sxs-lookup"><span data-stu-id="f272e-150">p.azurewebsites.net</span></span>

    * <span data-ttu-id="f272e-151">&lt;имя_ASE&gt;.p.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="f272e-151">&lt;asename&gt;.p.azurewebsites.net</span></span>

   <span data-ttu-id="f272e-152">Hello пользовательское доменное имя, используемое для приложений и имя домена hello, используемых вашей ASE не могут перекрываться.</span><span class="sxs-lookup"><span data-stu-id="f272e-152">hello custom domain name used for apps and hello domain name used by your ASE can't overlap.</span></span> <span data-ttu-id="f272e-153">Для ILB ASE доменным именем hello _contoso.com_, нельзя использовать пользовательские доменные имена для приложений, как:</span><span class="sxs-lookup"><span data-stu-id="f272e-153">For an ILB ASE with hello domain name _contoso.com_, you can't use custom domain names for your apps like:</span></span>

    * <span data-ttu-id="f272e-154">www.contoso.com;</span><span class="sxs-lookup"><span data-stu-id="f272e-154">www.contoso.com</span></span>

    * <span data-ttu-id="f272e-155">abcd.def.contoso.com;</span><span class="sxs-lookup"><span data-stu-id="f272e-155">abcd.def.contoso.com</span></span>

    * <span data-ttu-id="f272e-156">abcd.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="f272e-156">abcd.contoso.com</span></span>

   <span data-ttu-id="f272e-157">Если вы знаете hello пользовательских доменных имен для приложений, выберите домен для hello ASE ILB, не имеется конфликт с именами соответствующих пользовательского домена.</span><span class="sxs-lookup"><span data-stu-id="f272e-157">If you know hello custom domain names for your apps, choose a domain for hello ILB ASE that won’t have a conflict with those custom domain names.</span></span> <span data-ttu-id="f272e-158">В этом примере можно использовать нечто похожее на *contoso internal.com* для домена вашей ASE hello, так как не противоречит пользовательские доменные имена, заканчивающиеся на *. contoso.com*.</span><span class="sxs-lookup"><span data-stu-id="f272e-158">In this example, you can use something like *contoso-internal.com* for hello domain of your ASE because that won't conflict with custom domain names that end in *.contoso.com*.</span></span>

8. <span data-ttu-id="f272e-159">Щелкните **ОК**, а затем выберите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f272e-159">Select **OK**, and then select **Create**.</span></span>

    ![создание ASE][1]

<span data-ttu-id="f272e-161">На hello **виртуальной сети** колонке имеется **конфигурации виртуальной сети** параметр.</span><span class="sxs-lookup"><span data-stu-id="f272e-161">On hello **Virtual Network** blade, there is a **Virtual Network Configuration** option.</span></span> <span data-ttu-id="f272e-162">Его можно использовать tooselect букве виртуального IP-адреса внешних или внутренних виртуальных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="f272e-162">You can use it tooselect an External VIP or an Internal VIP.</span></span> <span data-ttu-id="f272e-163">по умолчанию Hello — **внешних**.</span><span class="sxs-lookup"><span data-stu-id="f272e-163">hello default is **External**.</span></span> <span data-ttu-id="f272e-164">Если выбрать значение **Внешний**, для среды службы приложений будет использоваться виртуальный IP-адрес, доступный из Интернета.</span><span class="sxs-lookup"><span data-stu-id="f272e-164">If you select **External**, your ASE uses an internet-accessible VIP.</span></span> <span data-ttu-id="f272e-165">Если выбрать **внутренний** виртуальный IP-адрес, то для ASE будет настроена внутренний балансировщик нагрузки с IP-адресом в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="f272e-165">If you select **Internal**, your ASE is configured with an ILB on an IP address within your VNet.</span></span>

<span data-ttu-id="f272e-166">После выбора **внутренний**, tooadd возможность hello несколько IP-адресов tooyour ASE удаляется.</span><span class="sxs-lookup"><span data-stu-id="f272e-166">After you select **Internal**, hello ability tooadd more IP addresses tooyour ASE is removed.</span></span> <span data-ttu-id="f272e-167">Вместо этого необходим домен hello tooprovide hello ASE.</span><span class="sxs-lookup"><span data-stu-id="f272e-167">Instead, you need tooprovide hello domain of hello ASE.</span></span> <span data-ttu-id="f272e-168">В ASE с внешнего виртуального IP-адреса hello hello ASE имя используется в домене hello для приложений, созданных в этом ASE.</span><span class="sxs-lookup"><span data-stu-id="f272e-168">In an ASE with an External VIP, hello name of hello ASE is used in hello domain for apps created in that ASE.</span></span>

<span data-ttu-id="f272e-169">Если задать **тип виртуального IP-адреса** слишком**внутренний**, название ASE не используется в домене hello для hello ASE.</span><span class="sxs-lookup"><span data-stu-id="f272e-169">If you set **VIP Type** too**Internal**, your ASE name is not used in hello domain for hello ASE.</span></span> <span data-ttu-id="f272e-170">Укажите домен hello явным образом.</span><span class="sxs-lookup"><span data-stu-id="f272e-170">You specify hello domain explicitly.</span></span> <span data-ttu-id="f272e-171">Если ваш домен называется *contoso.corp.net* и создать приложение, в том, что с именем ASE *timereporting*, hello URL-адрес для этого приложения является timereporting.contoso.corp.net.</span><span class="sxs-lookup"><span data-stu-id="f272e-171">If your domain is *contoso.corp.net* and you create an app in that ASE named *timereporting*, hello URL for that app is timereporting.contoso.corp.net.</span></span>


## <a name="create-an-app-in-an-ilb-ase"></a><span data-ttu-id="f272e-172">Создание приложения в ASE с внутренним балансировщиком нагрузки</span><span class="sxs-lookup"><span data-stu-id="f272e-172">Create an app in an ILB ASE</span></span> ##

<span data-ttu-id="f272e-173">Создайте приложение в ASE ILB в hello так же, что создается приложение, в ASE обычно.</span><span class="sxs-lookup"><span data-stu-id="f272e-173">You create an app in an ILB ASE in hello same way that you create an app in an ASE normally.</span></span>

1. <span data-ttu-id="f272e-174">В hello портал Azure, выберите **New** > **Интернет + мобильные устройства** > **Web** или **Mobile** или  **Приложения API**.</span><span class="sxs-lookup"><span data-stu-id="f272e-174">In hello Azure portal, select **New** > **Web + Mobile** > **Web** or **Mobile** or **API App**.</span></span>

2. <span data-ttu-id="f272e-175">Введите имя hello приложение hello.</span><span class="sxs-lookup"><span data-stu-id="f272e-175">Enter hello name of hello app.</span></span>

3. <span data-ttu-id="f272e-176">Выберите подписку hello.</span><span class="sxs-lookup"><span data-stu-id="f272e-176">Select hello subscription.</span></span>

4. <span data-ttu-id="f272e-177">Выберите или создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f272e-177">Select or create a resource group.</span></span>

5. <span data-ttu-id="f272e-178">Выбор или создание плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="f272e-178">Select or create an App Service plan.</span></span> <span data-ttu-id="f272e-179">Toocreate новый план служб приложений, выберите ваш ASE как расположение hello.</span><span class="sxs-lookup"><span data-stu-id="f272e-179">If you want toocreate a new App Service plan, select your ASE as hello location.</span></span> <span data-ttu-id="f272e-180">Выберите место создания плана toobe вашей службы приложений система пул рабочих hello.</span><span class="sxs-lookup"><span data-stu-id="f272e-180">Select hello worker pool where you want your App Service plan toobe created.</span></span> <span data-ttu-id="f272e-181">При создании hello план служб приложений, выберите ваш ASE как расположение hello и hello рабочего пула.</span><span class="sxs-lookup"><span data-stu-id="f272e-181">When you create hello App Service plan, select your ASE as hello location and hello worker pool.</span></span> <span data-ttu-id="f272e-182">При указании имени hello приложение hello hello домена в списке имя вашего приложения заменяется hello домена для вашей ASE.</span><span class="sxs-lookup"><span data-stu-id="f272e-182">When you specify hello name of hello app, hello domain under your app name is replaced by hello domain for your ASE.</span></span>

6. <span data-ttu-id="f272e-183">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f272e-183">Select **Create**.</span></span> <span data-ttu-id="f272e-184">Tooappear приложения hello на панели мониторинга, установите **toodashboard ПИН-код** флажок.</span><span class="sxs-lookup"><span data-stu-id="f272e-184">If you want hello app tooappear on your dashboard, select the **Pin toodashboard** check box.</span></span>

    ![Создание плана служб приложений][2]

    <span data-ttu-id="f272e-186">В разделе **имя приложения**, hello доменное имя — домен вашей ASE обновленные tooreflect hello.</span><span class="sxs-lookup"><span data-stu-id="f272e-186">Under **App name**, hello domain name is updated tooreflect hello domain of your ASE.</span></span>

## <a name="post-ilb-ase-creation-validation"></a><span data-ttu-id="f272e-187">Проверка после создания ASE с внутренним балансировщиком нагрузки</span><span class="sxs-lookup"><span data-stu-id="f272e-187">Post-ILB ASE creation validation</span></span> ##

<span data-ttu-id="f272e-188">ILB ASE немного отличается от hello не - ILB ASE.</span><span class="sxs-lookup"><span data-stu-id="f272e-188">An ILB ASE is slightly different than hello non-ILB ASE.</span></span> <span data-ttu-id="f272e-189">Как уже отмечалось необходимо toomanage собственный DNS-сервера.</span><span class="sxs-lookup"><span data-stu-id="f272e-189">As already noted, you need toomanage your own DNS.</span></span> <span data-ttu-id="f272e-190">Также имеется tooprovide собственный сертификат для подключения по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f272e-190">You also have tooprovide your own certificate for HTTPS connections.</span></span>

<span data-ttu-id="f272e-191">После создания вашей ASE hello доменное имя показывает hello указанного домена.</span><span class="sxs-lookup"><span data-stu-id="f272e-191">After you create your ASE, hello domain name shows hello domain you specified.</span></span> <span data-ttu-id="f272e-192">В меню **Параметры** появился новый пункт **Сертификат ILB**.</span><span class="sxs-lookup"><span data-stu-id="f272e-192">A new item appears in the **Setting** menu called **ILB Certificate**.</span></span> <span data-ttu-id="f272e-193">Hello ASE создается сертификатом, который не указывает hello ILB ASE домена.</span><span class="sxs-lookup"><span data-stu-id="f272e-193">hello ASE is created with a certificate that doesn't specify hello ILB ASE domain.</span></span> <span data-ttu-id="f272e-194">Если hello ASE использовать с этим сертификатом, браузер показывает, что не допускается.</span><span class="sxs-lookup"><span data-stu-id="f272e-194">If you use hello ASE with that certificate, your browser tells you that it's invalid.</span></span> <span data-ttu-id="f272e-195">Этот сертификат позволяет проще tootest HTTPS, но требуется tooupload собственный сертификат равноценных tooyour ILB ASE доменом.</span><span class="sxs-lookup"><span data-stu-id="f272e-195">This certificate makes it easier tootest HTTPS, but you need tooupload your own certificate that's tied tooyour ILB ASE domain.</span></span> <span data-ttu-id="f272e-196">Этот шаг является обязательным независимо от типа сертификата: самозаверяющий или получен из ЦС.</span><span class="sxs-lookup"><span data-stu-id="f272e-196">This step is necessary regardless of whether your certificate is self-signed or acquired from a certificate authority.</span></span>

![Имя домена ASE с ILB][3]

<span data-ttu-id="f272e-198">Для ASE с внутренним балансировщиком нагрузки требуется допустимый сертификат SSL.</span><span class="sxs-lookup"><span data-stu-id="f272e-198">Your ILB ASE needs a valid SSL certificate.</span></span> <span data-ttu-id="f272e-199">Можно получить сертификат от внутреннего центра сертификации, приобрести его у внешнего поставщика и использовать самозаверяющий сертификат.</span><span class="sxs-lookup"><span data-stu-id="f272e-199">Use internal certificate authorities, purchase a certificate from an external issuer, or use a self-signed certificate.</span></span> <span data-ttu-id="f272e-200">Вне зависимости от источника hello hello SSL-сертификат hello следующие атрибуты сертификатов, необходимые toobe настроен должным образом.</span><span class="sxs-lookup"><span data-stu-id="f272e-200">Regardless of hello source of hello SSL certificate, hello following certificate attributes need toobe configured properly:</span></span>

* <span data-ttu-id="f272e-201">**Тема**: этот атрибут должен быть задан too*.your корневого домена здесь.</span><span class="sxs-lookup"><span data-stu-id="f272e-201">**Subject**: This attribute must be set too*.your-root-domain-here.</span></span>
* <span data-ttu-id="f272e-202">**Subject Alternative Name** — этот атрибут должен содержать два значения: **.имя_корневого_домена* и **.scm.имя_корневого_домена*.</span><span class="sxs-lookup"><span data-stu-id="f272e-202">**Subject Alternative Name**: This attribute must include both **.your-root-domain-here* and **.scm.your-root-domain-here*.</span></span> <span data-ttu-id="f272e-203">SCM/Kudu сайта, связанные с каждой приложением toohello подключений SSL использует адрес формы hello *your-app-name.scm.your-root-domain-here*.</span><span class="sxs-lookup"><span data-stu-id="f272e-203">SSL connections toohello SCM/Kudu site associated with each app use an address of hello form *your-app-name.scm.your-root-domain-here*.</span></span>

<span data-ttu-id="f272e-204">Преобразования и сохранения hello SSL-сертификата в PFX-файл.</span><span class="sxs-lookup"><span data-stu-id="f272e-204">Convert/save hello SSL certificate as a .pfx file.</span></span> <span data-ttu-id="f272e-205">Hello PFX-файл должен включать все промежуточные и корневые сертификаты.</span><span class="sxs-lookup"><span data-stu-id="f272e-205">hello .pfx file must include all intermediate and root certificates.</span></span> <span data-ttu-id="f272e-206">Защитите его паролем.</span><span class="sxs-lookup"><span data-stu-id="f272e-206">Secure it with a password.</span></span>

<span data-ttu-id="f272e-207">Если вы хотите toocreate самозаверяющий сертификат, можно использовать команды PowerShell hello здесь.</span><span class="sxs-lookup"><span data-stu-id="f272e-207">If you want toocreate a self-signed certificate, you can use hello PowerShell commands here.</span></span> <span data-ttu-id="f272e-208">Быть toouse убедиться, что имя домена ILB ASE вместо *internal.contoso.com*:</span><span class="sxs-lookup"><span data-stu-id="f272e-208">Be sure toouse your ILB ASE domain name instead of *internal.contoso.com*:</span></span> 

    $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "\*.internal-contoso.com","\*.scm.internal-contoso.com"
    
    $certThumbprint = "cert:\localMachine\my\" +$certificate.Thumbprint
    $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText
    
    $fileName = "exportedcert.pfx" 
    Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password

<span data-ttu-id="f272e-209">сертификат Hello, создания этих команд PowerShell помечается в браузерах, так как сертификат hello не была создана, в браузере цепочка доверия центром сертификации.</span><span class="sxs-lookup"><span data-stu-id="f272e-209">hello certificate that these PowerShell commands generate is flagged by browsers because hello certificate wasn't created by a certificate authority that's in your browser's chain of trust.</span></span> <span data-ttu-id="f272e-210">сертификат, который доверяет браузер, tooget получения ключа из коммерческого центра сертификации в цепи доверия в браузере.</span><span class="sxs-lookup"><span data-stu-id="f272e-210">tooget a certificate that your browser trusts, procure it from a commercial certificate authority in your browser's chain of trust.</span></span> 

![Задание сертификата ILB][4]

<span data-ttu-id="f272e-212">tooupload сертификаты и доступа теста:</span><span class="sxs-lookup"><span data-stu-id="f272e-212">tooupload your own certificates and test access:</span></span>

1. <span data-ttu-id="f272e-213">После создания hello ASE перейдите toohello ASE пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="f272e-213">After hello ASE is created, go toohello ASE UI.</span></span> <span data-ttu-id="f272e-214">Выберите **ASE** > **Параметры** > **Сертификат ILB**.</span><span class="sxs-lookup"><span data-stu-id="f272e-214">Select **ASE** > **Settings** > **ILB Certificate**.</span></span>

2. <span data-ttu-id="f272e-215">tooset hello ILB сертификат, выберите PFX-файл сертификата hello и введите пароль hello.</span><span class="sxs-lookup"><span data-stu-id="f272e-215">tooset hello ILB certificate, select hello certificate .pfx file and enter hello password.</span></span> <span data-ttu-id="f272e-216">Этот шаг займет некоторое время tooprocess.</span><span class="sxs-lookup"><span data-stu-id="f272e-216">This step takes some time tooprocess.</span></span> <span data-ttu-id="f272e-217">Появится сообщение о том, что выполняется отправка.</span><span class="sxs-lookup"><span data-stu-id="f272e-217">A message appears stating that an upload operation is in progress.</span></span>

3. <span data-ttu-id="f272e-218">Получите адрес ILB hello для вашего ASE.</span><span class="sxs-lookup"><span data-stu-id="f272e-218">Get hello ILB address for your ASE.</span></span> <span data-ttu-id="f272e-219">Выберите **ASE** > **Свойства** > **Виртуальный IP-адрес**.</span><span class="sxs-lookup"><span data-stu-id="f272e-219">Select **ASE** > **Properties** > **Virtual IP Address**.</span></span>

4. <span data-ttu-id="f272e-220">Создание веб-приложения в вашей ASE после создания hello ASE.</span><span class="sxs-lookup"><span data-stu-id="f272e-220">Create a web app in your ASE after hello ASE is created.</span></span>

5. <span data-ttu-id="f272e-221">Создайте виртуальную машину в этой виртуальной сети (если вы этого еще не сделали).</span><span class="sxs-lookup"><span data-stu-id="f272e-221">Create a VM if you don't have one in that VNet.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f272e-222">Старайтесь не toocreate эту виртуальную Машину в hello одной подсети как hello ASE, так как он будут завершаться ошибкой или вызвать проблемы.</span><span class="sxs-lookup"><span data-stu-id="f272e-222">Don't try toocreate this VM in hello same subnet as hello ASE because it will fail or cause problems.</span></span>
    >
    >

6. <span data-ttu-id="f272e-223">Задайте hello DNS для домена ASE.</span><span class="sxs-lookup"><span data-stu-id="f272e-223">Set hello DNS for your ASE domain.</span></span> <span data-ttu-id="f272e-224">Можно указать в DNS подстановочные знаки с именем домена.</span><span class="sxs-lookup"><span data-stu-id="f272e-224">You can use a wildcard with your domain in your DNS.</span></span> <span data-ttu-id="f272e-225">toodo несколько простых тестов, измените файл hosts hello на вашей виртуальной Машины tooset hello web app имя toohello виртуального IP-адреса IP-адрес:</span><span class="sxs-lookup"><span data-stu-id="f272e-225">toodo some simple tests, edit hello hosts file on your VM tooset hello web app name toohello VIP IP address:</span></span>

    <span data-ttu-id="f272e-226">а.</span><span class="sxs-lookup"><span data-stu-id="f272e-226">a.</span></span> <span data-ttu-id="f272e-227">Если ваш ASE hello доменных имен _. ilbase.com_ и создать hello веб-приложения с именем _mytestapp_, она описана в _mytestapp.ilbase.com_. Затем установите _mytestapp.ilbase.com_ tooresolve toohello ILB адрес.</span><span class="sxs-lookup"><span data-stu-id="f272e-227">If your ASE has hello domain name _.ilbase.com_ and you create hello web app named _mytestapp_, it's addressed at _mytestapp.ilbase.com_. You then set _mytestapp.ilbase.com_ tooresolve toohello ILB address.</span></span> <span data-ttu-id="f272e-228">(В Windows hello файл hosts находится в _C:\Windows\System32\drivers\etc\_.)</span><span class="sxs-lookup"><span data-stu-id="f272e-228">(On Windows, hello hosts file is at _C:\Windows\System32\drivers\etc\_.)</span></span>

    <span data-ttu-id="f272e-229">b.</span><span class="sxs-lookup"><span data-stu-id="f272e-229">b.</span></span> <span data-ttu-id="f272e-230">tootest web развертывания публикации или доступа toohello дополнительные консоли, создайте запись для _mytestapp.scm.ilbase.com_.</span><span class="sxs-lookup"><span data-stu-id="f272e-230">tootest web deployment publishing or access toohello advanced console, create a record for _mytestapp.scm.ilbase.com_.</span></span>

7. <span data-ttu-id="f272e-231">Откройте браузер на этой виртуальной машине и перейдите по адресу http://mytestapp.ilbase.com. (Или перейти toowhatever — имя вашего веб-приложения с вашим доменом).</span><span class="sxs-lookup"><span data-stu-id="f272e-231">Use a browser on that VM and go to http://mytestapp.ilbase.com. (Or go toowhatever your web app name is with your domain.)</span></span>

8. <span data-ttu-id="f272e-232">Откройте браузер на этой виртуальной машине и перейдите по адресу https://mytestapp.ilbase.com. Если вы используете самозаверяющий сертификат, примите hello отсутствие безопасности.</span><span class="sxs-lookup"><span data-stu-id="f272e-232">Use a browser on that VM and go to https://mytestapp.ilbase.com. If you use a self-signed certificate, accept hello lack of security.</span></span>

    <span data-ttu-id="f272e-233">Hello IP-адрес для вашего ILB находится в списке **IP-адреса**.</span><span class="sxs-lookup"><span data-stu-id="f272e-233">hello IP address for your ILB is listed under **IP addresses**.</span></span> <span data-ttu-id="f272e-234">Этот список также содержит hello IP-адреса, используемые для hello внешних виртуальных IP-адресов для входящего трафика управления трафиком.</span><span class="sxs-lookup"><span data-stu-id="f272e-234">This list also has hello IP addresses used by hello external VIP and for inbound management traffic.</span></span>

    ![IP-адрес ILB][5]

### <a name="web-jobs-functions-and-hello-ilb-ase"></a><span data-ttu-id="f272e-236">Веб-задания, функции и hello ILB ASE</span><span class="sxs-lookup"><span data-stu-id="f272e-236">Web jobs, Functions and hello ILB ASE</span></span>

<span data-ttu-id="f272e-237">Функции и веб-задания поддерживаются в ILB ASE, но для hello портала toowork с ними, необходимо иметь сетевой доступ toohello SCM сайт.</span><span class="sxs-lookup"><span data-stu-id="f272e-237">Both Functions and web jobs are supported on an ILB ASE but for hello portal toowork with them, you must have network access toohello SCM site.</span></span>  <span data-ttu-id="f272e-238">Это означает, что браузер должен быть на узле, либо подключены toohello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="f272e-238">This means your browser must either be on a host that is either in or connected toohello virtual network.</span></span>  

<span data-ttu-id="f272e-239">При использовании функции Azure на ILB ASE может появиться сообщение об ошибке «не может tooretrieve функций в данный момент.</span><span class="sxs-lookup"><span data-stu-id="f272e-239">When you use Azure Functions on an ILB ASE, you might get an error message that says "We are not able tooretrieve your functions right now.</span></span> <span data-ttu-id="f272e-240">Повторите попытку позже".</span><span class="sxs-lookup"><span data-stu-id="f272e-240">Please try again later."</span></span> <span data-ttu-id="f272e-241">Эта ошибка возникает, поскольку hello функций пользовательского интерфейса использует hello SCM сайта по протоколу HTTPS и hello корневой сертификат не hello браузера цепочки сертификатов.</span><span class="sxs-lookup"><span data-stu-id="f272e-241">This error occurs because hello Functions UI leverages hello SCM site over HTTPS and hello root certificate is not in hello browser chain of trust.</span></span> <span data-ttu-id="f272e-242">Веб-задания могут вызывать подобную проблему.</span><span class="sxs-lookup"><span data-stu-id="f272e-242">Web jobs has a similar problem.</span></span> <span data-ttu-id="f272e-243">tooavoid эту проблему, можно выполнить одно из следующих hello:</span><span class="sxs-lookup"><span data-stu-id="f272e-243">tooavoid this problem you can do one of hello following:</span></span>

- <span data-ttu-id="f272e-244">Добавьте хранилище доверенных сертификатов tooyour hello сертификата.</span><span class="sxs-lookup"><span data-stu-id="f272e-244">Add hello certificate tooyour trusted certificate store.</span></span> <span data-ttu-id="f272e-245">Это позволит разблокировать Edge и Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="f272e-245">This unblocks Edge and Internet Explorer.</span></span>
- <span data-ttu-id="f272e-246">Используйте Chrome и сначала перейдите toohello SCM сайт, примите hello ненадежный сертификат, а затем перейдите toohello портала.</span><span class="sxs-lookup"><span data-stu-id="f272e-246">Use Chrome and go toohello SCM site first, accept hello untrusted certificate and then go toohello portal.</span></span>
- <span data-ttu-id="f272e-247">Используйте коммерческий сертификат, который находится в цепочке сертификатов браузера.</span><span class="sxs-lookup"><span data-stu-id="f272e-247">Use a commercial certificate that is in your browser chain of trust.</span></span>  <span data-ttu-id="f272e-248">Это лучший вариант hello.</span><span class="sxs-lookup"><span data-stu-id="f272e-248">This is hello best option.</span></span>  

## <a name="dns-configuration"></a><span data-ttu-id="f272e-249">Настройка DNS</span><span class="sxs-lookup"><span data-stu-id="f272e-249">DNS configuration</span></span> ##

<span data-ttu-id="f272e-250">При использовании внешних виртуальных IP-адресов, hello DNS управляется Azure.</span><span class="sxs-lookup"><span data-stu-id="f272e-250">When you use an External VIP, hello DNS is managed by Azure.</span></span> <span data-ttu-id="f272e-251">Любое приложение, созданных в вашей ASE автоматически добавляется tooAzure DNS, передаваемый в общедоступном DNS-Сервере.</span><span class="sxs-lookup"><span data-stu-id="f272e-251">Any app created in your ASE is automatically added tooAzure DNS, which is a public DNS.</span></span> <span data-ttu-id="f272e-252">В ASE с ILB необходимо управлять собственной службой DNS.</span><span class="sxs-lookup"><span data-stu-id="f272e-252">In an ILB ASE, you must manage your own DNS.</span></span> <span data-ttu-id="f272e-253">Для данного домена, такие как _contoso.net_, требуется toocreate DNS типа записей в DNS этот адрес tooyour точки ILB для:</span><span class="sxs-lookup"><span data-stu-id="f272e-253">For a given domain such as _contoso.net_, you need toocreate DNS A records in your DNS that point tooyour ILB address for:</span></span>

- <span data-ttu-id="f272e-254">*.contoso.net;</span><span class="sxs-lookup"><span data-stu-id="f272e-254">*.contoso.net</span></span>
- <span data-ttu-id="f272e-255">*.scm.contoso.net.</span><span class="sxs-lookup"><span data-stu-id="f272e-255">*.scm.contoso.net</span></span>

<span data-ttu-id="f272e-256">Если домен ILB ASE используется для нескольких операций за пределами этого ASE, может потребоваться toomanage DNS на основе имени приложения.</span><span class="sxs-lookup"><span data-stu-id="f272e-256">If your ILB ASE domain is used for multiple things outside this ASE, you might need toomanage DNS on a per-app-name basis.</span></span> <span data-ttu-id="f272e-257">Этот метод весьма сложно, поскольку требуется tooadd каждого нового имени приложения в DNS-сервера при ее создании.</span><span class="sxs-lookup"><span data-stu-id="f272e-257">This method is challenging because you need tooadd each new app name into your DNS when you create it.</span></span> <span data-ttu-id="f272e-258">По этой причине рекомендуется использовать выделенный домен.</span><span class="sxs-lookup"><span data-stu-id="f272e-258">For this reason, we recommend that you use a dedicated domain.</span></span>

## <a name="publish-with-an-ilb-ase"></a><span data-ttu-id="f272e-259">Публикация с использованием ASE с внутренним балансировщиком нагрузки</span><span class="sxs-lookup"><span data-stu-id="f272e-259">Publish with an ILB ASE</span></span> ##

<span data-ttu-id="f272e-260">Для каждого создаваемого приложения предоставляются две конечные точки.</span><span class="sxs-lookup"><span data-stu-id="f272e-260">For every app that's created, there are two endpoints.</span></span> <span data-ttu-id="f272e-261">В ASE с ILB это *&lt;имя_приложения>.&lt;домен_ASE_с_ILB>* и *&lt;имя_приложения>.scm.&lt;домен_ASE_с_ILB>*.</span><span class="sxs-lookup"><span data-stu-id="f272e-261">In an ILB ASE, you have *&lt;app name>.&lt;ILB ASE Domain>* and *&lt;app name>.scm.&lt;ILB ASE Domain>*.</span></span> 

<span data-ttu-id="f272e-262">Имя сайта SCM Hello принимает toohello Kudu консоли называется hello **Дополнительно портала**внутри hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f272e-262">hello SCM site name takes you toohello Kudu console, called hello **Advanced portal**, within hello Azure portal.</span></span> <span data-ttu-id="f272e-263">консоль Kudu Hello позволяет просмотреть переменные среды, исследовать hello диска, используйте консоль и многое другое.</span><span class="sxs-lookup"><span data-stu-id="f272e-263">hello Kudu console lets you view environment variables, explore hello disk, use a console, and much more.</span></span> <span data-ttu-id="f272e-264">Дополнительные сведения см. на странице, посвященной [консоли Kudu для службы приложений Azure][Kudu].</span><span class="sxs-lookup"><span data-stu-id="f272e-264">For more information, see [Kudu console for Azure App Service][Kudu].</span></span> 

<span data-ttu-id="f272e-265">Мультитенантный hello службы приложений и внешних ASE нет единого входа между hello портал Azure и консоли Kudu hello.</span><span class="sxs-lookup"><span data-stu-id="f272e-265">In hello multitenant App Service and in an External ASE, there's single sign-on between hello Azure portal and hello Kudu console.</span></span> <span data-ttu-id="f272e-266">Для hello ILB ASE Однако необходимо toouse вашей публикации toosign учетные данные в консоль Kudu hello.</span><span class="sxs-lookup"><span data-stu-id="f272e-266">For hello ILB ASE, however, you need toouse your publishing credentials toosign into hello Kudu console.</span></span>

<span data-ttu-id="f272e-267">Интернет-CI системах, таких как GitHub и Visual Studio Team Services, не работают с ILB ASE, так как конечную точку публикации hello Интернет доступен.</span><span class="sxs-lookup"><span data-stu-id="f272e-267">Internet-based CI systems, such as GitHub and Visual Studio Team Services, don't work with an ILB ASE because hello publishing endpoint isn't internet accessible.</span></span> <span data-ttu-id="f272e-268">Вместо этого необходим toouse элементов конфигурации системы, где используется запросу модели, например Dropbox.</span><span class="sxs-lookup"><span data-stu-id="f272e-268">Instead, you need toouse a CI system that uses a pull model, such as Dropbox.</span></span>

<span data-ttu-id="f272e-269">Публикация конечных точек для приложений в ILB ASE Hello использовать домен hello, hello ILB ASE была создана с.</span><span class="sxs-lookup"><span data-stu-id="f272e-269">hello publishing endpoints for apps in an ILB ASE use hello domain that hello ILB ASE was created with.</span></span> <span data-ttu-id="f272e-270">Этот домен отображается в приложение hello профиль публикации и в колонке портала приложение hello (**Обзор** > **Essentials** , а также **свойства**).</span><span class="sxs-lookup"><span data-stu-id="f272e-270">This domain appears in hello app's publishing profile and in hello app's portal blade (**Overview** > **Essentials** and also **Properties**).</span></span> <span data-ttu-id="f272e-271">При наличии ASE ILB с поддомена hello *contoso.net* и приложения с именем *mytest*, используйте *mytest.contoso.net* для FTP-сервера и *mytest.scm.contoso.net*  для развертывания веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="f272e-271">If you have an ILB ASE with hello subdomain *contoso.net* and an app named *mytest*, use *mytest.contoso.net* for FTP and *mytest.scm.contoso.net* for web deployment.</span></span>

## <a name="couple-an-ilb-ase-with-a-waf-device"></a><span data-ttu-id="f272e-272">Взаимозависимость среды ASE с внутренним балансировщиком нагрузки и устройства WAF</span><span class="sxs-lookup"><span data-stu-id="f272e-272">Couple an ILB ASE with a WAF device</span></span> ##

<span data-ttu-id="f272e-273">Служба приложений Azure предоставляет множество мер безопасности, защитить систему hello.</span><span class="sxs-lookup"><span data-stu-id="f272e-273">Azure App Service provides many security measures that protect hello system.</span></span> <span data-ttu-id="f272e-274">Они также помогут toodetermine ли приложение было вредоносной атаки.</span><span class="sxs-lookup"><span data-stu-id="f272e-274">They also help toodetermine whether an app was hacked.</span></span> <span data-ttu-id="f272e-275">Лучший способ защиты Hello для веб-приложения — toocouple размещения платформы, такие как службы приложений Azure, с брандмауэр веб-приложения (WAF).</span><span class="sxs-lookup"><span data-stu-id="f272e-275">hello best protection for a web application is toocouple a hosting platform, such as Azure App Service, with a web application firewall (WAF).</span></span> <span data-ttu-id="f272e-276">Так как hello ILB ASE конечную точку приложения с сетевой изоляцией, подходит для такого использования.</span><span class="sxs-lookup"><span data-stu-id="f272e-276">Because hello ILB ASE has a network-isolated application endpoint, it's appropriate for such a use.</span></span>

<span data-ttu-id="f272e-277">Дополнительные сведения о tooconfigure вашей ASE ILB с устройством WAF статье toolearn [настроить брандмауэр веб-приложения со средой службы приложений][ASEWAF].</span><span class="sxs-lookup"><span data-stu-id="f272e-277">toolearn more about how tooconfigure your ILB ASE with a WAF device, see [Configure a web application firewall with your App Service environment][ASEWAF].</span></span> <span data-ttu-id="f272e-278">В этой статье показано, как toouse Barracuda с вашей ASE виртуального устройства.</span><span class="sxs-lookup"><span data-stu-id="f272e-278">This article shows how toouse a Barracuda virtual appliance with your ASE.</span></span> <span data-ttu-id="f272e-279">Другой вариант — toouse шлюза приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="f272e-279">Another option is toouse Azure Application Gateway.</span></span> <span data-ttu-id="f272e-280">Шлюз приложения использует hello OWASP основных правил toosecure любых приложений, расположенных позади его.</span><span class="sxs-lookup"><span data-stu-id="f272e-280">Application Gateway uses hello OWASP core rules toosecure any applications placed behind it.</span></span> <span data-ttu-id="f272e-281">Дополнительные сведения о шлюзе приложений см. в разделе [брандмауэр введение toohello Azure веб-приложения][AppGW].</span><span class="sxs-lookup"><span data-stu-id="f272e-281">For more information about Application Gateway, see [Introduction toohello Azure web application firewall][AppGW].</span></span>

## <a name="get-started"></a><span data-ttu-id="f272e-282">Начало работы</span><span class="sxs-lookup"><span data-stu-id="f272e-282">Get started</span></span> ##

<span data-ttu-id="f272e-283">Все статьи и как tooinstructions для ASEs доступны в [файл README для среды службы приложений][ASEReadme].</span><span class="sxs-lookup"><span data-stu-id="f272e-283">All articles and how-tooinstructions for ASEs are available in the [README for App Service environments][ASEReadme].</span></span>

* <span data-ttu-id="f272e-284">tooget к работе с ASEs, в разделе [введение среды службы tooApp][Intro].</span><span class="sxs-lookup"><span data-stu-id="f272e-284">tooget started with ASEs, see [Introduction tooApp Service environments][Intro].</span></span>
* <span data-ttu-id="f272e-285">Дополнительные сведения о платформе hello службе приложений Azure см. в разделе [службе приложений Azure](http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/).</span><span class="sxs-lookup"><span data-stu-id="f272e-285">For more information about hello Azure App Service platform, see [Azure App Service](http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/).</span></span>
 
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
