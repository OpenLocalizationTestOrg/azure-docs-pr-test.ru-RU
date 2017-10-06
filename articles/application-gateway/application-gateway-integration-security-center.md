---
title: "Интеграция шлюза центра безопасности Azure aaaApplication | Документы Microsoft"
description: "Сведения об интеграции шлюза приложения с центром безопасности Azure."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.assetid: e5ea5cf9-3b41-4b85-a12c-e758bff7f3ec
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 06/07/2017
ms.author: gwallace
ms.openlocfilehash: 6f6ace105e84c01f525ab02938e81ce040c5c9d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-integration-between-application-gateway-and-azure-security-center"></a><span data-ttu-id="5af35-103">Общие сведения об интеграции шлюза приложений с центром безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="5af35-103">Overview of integration between Application Gateway and Azure Security Center</span></span>

<span data-ttu-id="5af35-104">В этой статье приведены сведения о том, как интеграция шлюза приложений с центром безопасности Azure позволяет обеспечить защиту ресурсов веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="5af35-104">Learn how Application Gateway and Security Center help protect your web application resources.</span></span> <span data-ttu-id="5af35-105">Брандмауэр веб-приложения шлюза приложений (WAF) интегрируется с [центра обеспечения безопасности](../security-center/security-center-intro.md) tooprovide tooprevent непрерывного просмотра обнаружить и отреагировать toothreats toounprotected веб-приложений в вашей среде.</span><span class="sxs-lookup"><span data-stu-id="5af35-105">Application gateway web application firewall (WAF) integrates with [Security Center](../security-center/security-center-intro.md) tooprovide a seamless view tooprevent, detect and respond toothreats toounprotected web applications in your environment.</span></span>

## <a name="overview"></a><span data-ttu-id="5af35-106">Обзор</span><span class="sxs-lookup"><span data-stu-id="5af35-106">Overview</span></span>

<span data-ttu-id="5af35-107">Брандмауэр веб-приложения шлюза приложений — это рекомендуемый компонент центра безопасности, обеспечивающий защиту веб-приложений от распространенных эксплойтов и уязвимостей.</span><span class="sxs-lookup"><span data-stu-id="5af35-107">Application Gateway WAF is a recommendation in Security Center for protecting web applications from exploits and vulnerabilities.</span></span> <span data-ttu-id="5af35-108">Включить веб-ресурсам, не защищены WAF показывает hello центра обеспечения безопасности от рекомендаций высокого уровня серьезности.</span><span class="sxs-lookup"><span data-stu-id="5af35-108">Web enabled resources that are not protected by WAF show in hello security center as high severity recommendations.</span></span> <span data-ttu-id="5af35-109">Рекомендации для брандмауэров приложения web отображаются на hello **Обзор** в разделе **приложений**.</span><span class="sxs-lookup"><span data-stu-id="5af35-109">Recommendations for web application firewalls are shown on hello **Overview** page, under **Applications**.</span></span>

![Интеграция с центром безопасности][1]

<span data-ttu-id="5af35-111">Никаких рекомендаций относительно брандмауэр веб-приложения при нажатии открывается новая колонка с подробными сведениями hello hello рекомендации.</span><span class="sxs-lookup"><span data-stu-id="5af35-111">Clicking any recommendations regarding web application firewall opens a new blade showing hello details of hello recommendation.</span></span>

## <a name="add-a-web-application-firewall-tooan-existing-resource"></a><span data-ttu-id="5af35-112">Добавить веб-приложение брандмауэра tooan существующий ресурс</span><span class="sxs-lookup"><span data-stu-id="5af35-112">Add a web application firewall tooan existing resource</span></span>

<span data-ttu-id="5af35-113">Перейдите слишком**более служб** > **безопасность + удостоверения** > **центра обеспечения безопасности** и на hello **центра обеспечения безопасности - Обзор**  колонка, щелкните **приложений**.</span><span class="sxs-lookup"><span data-stu-id="5af35-113">Navigate too**More Services** > **Security + Identity** > **Security Center** and on hello **Security Center - Overview** blade, click **Applications**.</span></span> <span data-ttu-id="5af35-114">На hello **центра обеспечения безопасности - приложений** колонке hello таблица содержит список приложений, которые обнаруживаются центра обеспечения безопасности в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="5af35-114">On hello **Security Center - Applications** blade, hello table contains a list of applications that Security Center detected in your subscription.</span></span>

![Веб-приложения][3]

<span data-ttu-id="5af35-116">Щелкнув веб-приложения с критическую ошибку, получите hello **индекс безопасности приложений** колонку.</span><span class="sxs-lookup"><span data-stu-id="5af35-116">By clicking on a web application with a critical issue, you get hello **Application security health** blade.</span></span> <span data-ttu-id="5af35-117">На рисунке hello ниже hello веб-приложение, которое не защищено брандмауэр веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="5af35-117">In hello image below, hello web application that is not protected by a web application firewall.</span></span> 

![Незащищенные веб-ресурсы][2]

<span data-ttu-id="5af35-119">Нажмите кнопку **добавьте брандмауэр веб-приложения** под **рекомендации** tooopen hello **добавьте брандмауэр веб-приложения** колонку.</span><span class="sxs-lookup"><span data-stu-id="5af35-119">Click **Add a web application firewall** under **Recommendations** tooopen hello **Add a Web Application Firewall** blade.</span></span>

<span data-ttu-id="5af35-120">Если требуется не имеют существующего шлюза приложения, или toocreate новый, нажмите кнопку **создать новый** и на hello **создать новый брандмауэр веб-приложения** и, при необходимости щелкните **Microsoft - Шлюз приложений**.</span><span class="sxs-lookup"><span data-stu-id="5af35-120">If you do not have an existing Application Gateway, or want toocreate a new one, click **Create New** and on hello **Create a new Web Application Firewall** blade, and click **Microsoft - Application Gateway**.</span></span> <span data-ttu-id="5af35-121">Это проводит пользователя через шаги hello toocreate шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="5af35-121">This takes you through hello steps toocreate an application gateway.</span></span> <span data-ttu-id="5af35-122">На этом этапе вы добавили веб-приложение как защищенный ресурс. Теперь этот ресурс помечен в центре безопасности как защищенный брандмауэром веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="5af35-122">At this point, your web application is added as a protected resource, Security Center now tracks that this resource is protected by a web application firewall.</span></span> <span data-ttu-id="5af35-123">Но он еще не добавлен как элемент внутреннего пула.</span><span class="sxs-lookup"><span data-stu-id="5af35-123">This does not add it as a backend pool member.</span></span>

<span data-ttu-id="5af35-124">Имеющийся шлюз приложений можно выбрать в разделе **Использование существующего решения**.</span><span class="sxs-lookup"><span data-stu-id="5af35-124">If you have an existing application gateway, you can choose it under **Use existing solution**</span></span>

![Колонка добавления брандмауэра веб-приложения][4]

<span data-ttu-id="5af35-126">Добавление Интернет-приложения tooan приложения шлюза, через Центр обеспечения безопасности не добавить hello ресурсов в качестве члена внутреннего пула, это необходимо сделать для ресурса шлюза приложения hello напрямую.</span><span class="sxs-lookup"><span data-stu-id="5af35-126">Adding a web application tooan application gateway through Security Center does not add hello resource as a backend pool member, this must be done on hello application gateway resource directly.</span></span>

## <a name="add-a-resource-tooan-existing-web-application-firewall"></a><span data-ttu-id="5af35-127">Добавление ресурсов tooan существующие брандмауэр веб-приложения</span><span class="sxs-lookup"><span data-stu-id="5af35-127">Add a resource tooan existing web application firewall</span></span>

<span data-ttu-id="5af35-128">Перейдите слишком**более служб** > **безопасность + удостоверения** > **центра обеспечения безопасности** и на hello **центра обеспечения безопасности - Обзор**  колонка, щелкните **решения партнеров**.</span><span class="sxs-lookup"><span data-stu-id="5af35-128">Navigate too**More Services** > **Security + Identity** > **Security Center** and on hello **Security Center - Overview** blade, click **Partner solutions**.</span></span> <span data-ttu-id="5af35-129">Показать существующие шлюзов центра обеспечения безопасности приложения, работающего в hello **решения партнеров** колонку.</span><span class="sxs-lookup"><span data-stu-id="5af35-129">Existing Security Center aware application gateways show in hello **Partner Solutions** blade.</span></span>

![Решения партнеров][7]

<span data-ttu-id="5af35-131">Нажмите кнопку **ссылку приложения** tooopen hello **ссылку приложения** колонки, здесь можно выбрать существующие приложения hello параметры tooselect.</span><span class="sxs-lookup"><span data-stu-id="5af35-131">Click **Link app** tooopen hello **Link Applications** blade, here you are given hello options tooselect existing applications.</span></span> <span data-ttu-id="5af35-132">Выберите tooprotect приложения hello и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="5af35-132">Choose hello applications tooprotect and click **OK**.</span></span> <span data-ttu-id="5af35-133">Hello пула веб-приложений toohello серверной шлюза приложения hello не добавляется.</span><span class="sxs-lookup"><span data-stu-id="5af35-133">This does not add hello web application toohello backend pool of hello application gateway.</span></span> <span data-ttu-id="5af35-134">Это задает hello ресурсы как защищенный ресурс, поэтому центра обеспечения безопасности можно отслеживать его.</span><span class="sxs-lookup"><span data-stu-id="5af35-134">This sets hello resources as a protected resource so Security Center can track it.</span></span> <span data-ttu-id="5af35-135">ресурс hello tooadd как член серверной части пула, это необходимо сделать для шлюза приложения hello, из текущего колонки hello можно нажать **консоли решения** toobe копии ресурса шлюза toohello приложения можно добавлять hello web внутренний пул toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="5af35-135">tooadd hello resource as a backend pool member, this must be done on hello application gateway, from hello current blade you can click **Solution console** toobe taken toohello application gateway resource where you can add hello web application toohello backend pool.</span></span>

![Сторонние приложения][6]

## <a name="finalize-configuration"></a><span data-ttu-id="5af35-137">Завершение конфигурации</span><span class="sxs-lookup"><span data-stu-id="5af35-137">Finalize configuration</span></span>

<span data-ttu-id="5af35-138">Центр обеспечения безопасности отслеживает приложения добавлены tooan шлюз приложений как защищенный ресурс.</span><span class="sxs-lookup"><span data-stu-id="5af35-138">Security Center tracks applications added tooan application gateway as a protected resource.</span></span>  <span data-ttu-id="5af35-139">Он отслеживает работоспособность hello этот ресурс и гарантирует, что он защищен шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="5af35-139">It monitors hello health of this resource and ensures that it is protected by an application gateway.</span></span> <span data-ttu-id="5af35-140">Hello следующим шагом является закрытым IP tooadd hello, общедоступный IP-адрес или сетевой Адаптер из виртуальной машины toohello внутреннего пула шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="5af35-140">hello next step is tooadd hello private IP, public IP, or NIC of your virtual machine toohello backend pool of hello application gateway.</span></span> <span data-ttu-id="5af35-141">До этого Дополнительные рекомендации **завершить подготовку защиты приложения** отображается, пока не будет добавлен hello ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5af35-141">Until this is done an additional recommendation of **Finalize application protection** is shown until hello resource is added.</span></span>

![Колонка добавления брандмауэра веб-приложения][5]

## <a name="security-alerts"></a><span data-ttu-id="5af35-143">Оповещения системы безопасности</span><span class="sxs-lookup"><span data-stu-id="5af35-143">Security Alerts</span></span>

<span data-ttu-id="5af35-144">Центр обеспечения безопасности переход в слишком**ОБНАРУЖЕНИЯ** > **оповещений системы безопасности**.</span><span class="sxs-lookup"><span data-stu-id="5af35-144">Within Security Center navigate too**DETECTION** > **Security Alerts**.</span></span>  <span data-ttu-id="5af35-145">Здесь отображаются оповещения WAF для шлюзов приложений.</span><span class="sxs-lookup"><span data-stu-id="5af35-145">Here you find WAF alerts for your application gateways.</span></span> <span data-ttu-id="5af35-146">Оповещения упорядочены по правилу WAF.</span><span class="sxs-lookup"><span data-stu-id="5af35-146">Alerts are broken down by WAF rule.</span></span>

![Оповещения системы безопасности][8]

<span data-ttu-id="5af35-148">Если щелкнуть конкретное правило WAF, откроется список оповещений.</span><span class="sxs-lookup"><span data-stu-id="5af35-148">Clicking an rule will provide a list of alerts for that specific WAF rule.</span></span> <span data-ttu-id="5af35-149">Каждого предупреждения отображает дополнительные подробные сведения на поиск hello.</span><span class="sxs-lookup"><span data-stu-id="5af35-149">Each alert shows additional details on hello finding.</span></span> <span data-ttu-id="5af35-150">Подробности Hello предоставляют шлюза приложения toohello ссылку.</span><span class="sxs-lookup"><span data-stu-id="5af35-150">hello details provide a link toohello application gateway.</span></span>
 
![Сведения в оповещении][9]

## <a name="next-steps"></a><span data-ttu-id="5af35-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5af35-152">Next steps</span></span>

<span data-ttu-id="5af35-153">как брандмауэр tooenable веб-приложения для существующего шлюза приложения, посетите toolearn [Создание или обновление шлюза приложения Azure с брандмауэр веб-приложения](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)</span><span class="sxs-lookup"><span data-stu-id="5af35-153">toolearn how tooenable web application firewall on an existing application gateway, visit [Create or update an Azure Application Gateway with web application firewall](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)</span></span>

[1]: ./media/application-gateway-integration-security-center/figure1.png
[2]: ./media/application-gateway-integration-security-center/figure2.png
[3]: ./media/application-gateway-integration-security-center/figure3.png
[4]: ./media/application-gateway-integration-security-center/figure4.png
[5]: ./media/application-gateway-integration-security-center/figure5.png
[6]: ./media/application-gateway-integration-security-center/figure6.png
[7]: ./media/application-gateway-integration-security-center/figure7.png
[8]: ./media/application-gateway-integration-security-center/securitycenter.png
[9]: ./media/application-gateway-integration-security-center/figure9.png