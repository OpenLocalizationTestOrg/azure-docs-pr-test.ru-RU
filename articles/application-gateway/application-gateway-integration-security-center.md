---
title: "Интеграция шлюза приложений с центром безопасности Azure | Документация Майкрософт"
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
ms.openlocfilehash: 737cdff3140be68cf9d6d396b470dd09c65c52f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="overview-of-integration-between-application-gateway-and-azure-security-center"></a><span data-ttu-id="a52a1-103">Общие сведения об интеграции шлюза приложений с центром безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="a52a1-103">Overview of integration between Application Gateway and Azure Security Center</span></span>

<span data-ttu-id="a52a1-104">В этой статье приведены сведения о том, как интеграция шлюза приложений с центром безопасности Azure позволяет обеспечить защиту ресурсов веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="a52a1-104">Learn how Application Gateway and Security Center help protect your web application resources.</span></span> <span data-ttu-id="a52a1-105">Брандмауэр веб-приложения (WAF) шлюза приложений можно интегрировать с [центром безопасности](../security-center/security-center-intro.md). Это позволяет обеспечить полный обзор всей среды, благодаря чему вы сможете выявлять и предотвращать угрозы от незащищенных веб-приложений, а также реагировать на них.</span><span class="sxs-lookup"><span data-stu-id="a52a1-105">Application gateway web application firewall (WAF) integrates with [Security Center](../security-center/security-center-intro.md) to provide a seamless view to prevent, detect and respond to threats to unprotected web applications in your environment.</span></span>

## <a name="overview"></a><span data-ttu-id="a52a1-106">Обзор</span><span class="sxs-lookup"><span data-stu-id="a52a1-106">Overview</span></span>

<span data-ttu-id="a52a1-107">Брандмауэр веб-приложения шлюза приложений — это рекомендуемый компонент центра безопасности, обеспечивающий защиту веб-приложений от распространенных эксплойтов и уязвимостей.</span><span class="sxs-lookup"><span data-stu-id="a52a1-107">Application Gateway WAF is a recommendation in Security Center for protecting web applications from exploits and vulnerabilities.</span></span> <span data-ttu-id="a52a1-108">Веб-ресурсы, не защищенные WAF, имеют в центре безопасности рекомендации высокого уровня серьезности.</span><span class="sxs-lookup"><span data-stu-id="a52a1-108">Web enabled resources that are not protected by WAF show in the security center as high severity recommendations.</span></span> <span data-ttu-id="a52a1-109">Рекомендации в отношении брандмауэров веб-приложений приведены на странице **Обзор** в разделе **Приложения**.</span><span class="sxs-lookup"><span data-stu-id="a52a1-109">Recommendations for web application firewalls are shown on the **Overview** page, under **Applications**.</span></span>

![Интеграция с центром безопасности][1]

<span data-ttu-id="a52a1-111">Если щелкнуть любую рекомендацию в отношении брандмауэра веб-приложения, откроется новая колонка с подробными сведениями о ней.</span><span class="sxs-lookup"><span data-stu-id="a52a1-111">Clicking any recommendations regarding web application firewall opens a new blade showing the details of the recommendation.</span></span>

## <a name="add-a-web-application-firewall-to-an-existing-resource"></a><span data-ttu-id="a52a1-112">Добавление брандмауэра веб-приложения в имеющийся шлюз приложений</span><span class="sxs-lookup"><span data-stu-id="a52a1-112">Add a web application firewall to an existing resource</span></span>

<span data-ttu-id="a52a1-113">Выберите **Другие службы** > **Безопасность+идентификация** > **Центр безопасности**, а затем в колонке **Центр безопасности — Обзор** щелкните **Приложения**.</span><span class="sxs-lookup"><span data-stu-id="a52a1-113">Navigate to **More Services** > **Security + Identity** > **Security Center** and on the **Security Center - Overview** blade, click **Applications**.</span></span> <span data-ttu-id="a52a1-114">Таблица в колонке **Центр безопасности — Приложения** содержит список приложений, обнаруженных центром безопасности в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="a52a1-114">On the **Security Center - Applications** blade, the table contains a list of applications that Security Center detected in your subscription.</span></span>

![Веб-приложения][3]

<span data-ttu-id="a52a1-116">Если щелкнуть веб-приложения с критической ошибкой, откроется колонка **Состояние защиты приложения**.</span><span class="sxs-lookup"><span data-stu-id="a52a1-116">By clicking on a web application with a critical issue, you get the **Application security health** blade.</span></span> <span data-ttu-id="a52a1-117">На рисунке ниже показан пример веб-приложение, незащищенного брандмауэром веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="a52a1-117">In the image below, the web application that is not protected by a web application firewall.</span></span> 

![Незащищенные веб-ресурсы][2]

<span data-ttu-id="a52a1-119">В разделе **Рекомендации** щелкните **Добавить брандмауэр веб-приложения**, чтобы открыть колонку **Добавить брандмауэр веб-приложения**.</span><span class="sxs-lookup"><span data-stu-id="a52a1-119">Click **Add a web application firewall** under **Recommendations** to open the **Add a Web Application Firewall** blade.</span></span>

<span data-ttu-id="a52a1-120">Если у вас нет шлюза приложений или вы хотите создать другой, в колонке **Create a new Web Application Firewall** (Создание брандмауэра веб-приложения) нажмите кнопку **Создать** и выберите **Microsoft — Шлюз приложений**.</span><span class="sxs-lookup"><span data-stu-id="a52a1-120">If you do not have an existing Application Gateway, or want to create a new one, click **Create New** and on the **Create a new Web Application Firewall** blade, and click **Microsoft - Application Gateway**.</span></span> <span data-ttu-id="a52a1-121">Выполните шаги по созданию шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="a52a1-121">This takes you through the steps to create an application gateway.</span></span> <span data-ttu-id="a52a1-122">На этом этапе вы добавили веб-приложение как защищенный ресурс. Теперь этот ресурс помечен в центре безопасности как защищенный брандмауэром веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="a52a1-122">At this point, your web application is added as a protected resource, Security Center now tracks that this resource is protected by a web application firewall.</span></span> <span data-ttu-id="a52a1-123">Но он еще не добавлен как элемент внутреннего пула.</span><span class="sxs-lookup"><span data-stu-id="a52a1-123">This does not add it as a backend pool member.</span></span>

<span data-ttu-id="a52a1-124">Имеющийся шлюз приложений можно выбрать в разделе **Использование существующего решения**.</span><span class="sxs-lookup"><span data-stu-id="a52a1-124">If you have an existing application gateway, you can choose it under **Use existing solution**</span></span>

![Колонка добавления брандмауэра веб-приложения][4]

<span data-ttu-id="a52a1-126">Если вы добавляете веб-приложение в шлюз приложений через центр безопасности, этот ресурс автоматически не добавляется как элемент внутреннего пула. Это необходимо сделать напрямую в ресурсе шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="a52a1-126">Adding a web application to an application gateway through Security Center does not add the resource as a backend pool member, this must be done on the application gateway resource directly.</span></span>

## <a name="add-a-resource-to-an-existing-web-application-firewall"></a><span data-ttu-id="a52a1-127">Добавление ресурса в имеющийся брандмауэр веб-приложения</span><span class="sxs-lookup"><span data-stu-id="a52a1-127">Add a resource to an existing web application firewall</span></span>

<span data-ttu-id="a52a1-128">Выберите **Другие службы** > **Безопасность+идентификация** > **Центр безопасности**, а затем в колонке **Центр безопасности — Обзор** щелкните **Решения партнеров**.</span><span class="sxs-lookup"><span data-stu-id="a52a1-128">Navigate to **More Services** > **Security + Identity** > **Security Center** and on the **Security Center - Overview** blade, click **Partner solutions**.</span></span> <span data-ttu-id="a52a1-129">Имеющиеся шлюзы приложений, поддерживающие центр безопасности, отображаются в колонке **Решения партнеров**.</span><span class="sxs-lookup"><span data-stu-id="a52a1-129">Existing Security Center aware application gateways show in the **Partner Solutions** blade.</span></span>

![Решения партнеров][7]

<span data-ttu-id="a52a1-131">Щелкните **Связать приложение**, чтобы открыть колонку **Связь приложений**. Здесь можно выбрать имеющиеся приложения.</span><span class="sxs-lookup"><span data-stu-id="a52a1-131">Click **Link app** to open the **Link Applications** blade, here you are given the options to select existing applications.</span></span> <span data-ttu-id="a52a1-132">Выберите приложения, которые необходимо защитить, и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a52a1-132">Choose the applications to protect and click **OK**.</span></span> <span data-ttu-id="a52a1-133">Эти действия не добавляют веб-приложение во внутренний пул.</span><span class="sxs-lookup"><span data-stu-id="a52a1-133">This does not add the web application to the backend pool of the application gateway.</span></span> <span data-ttu-id="a52a1-134">Ресурсы только помечаются как защищенные, за счет чего центр безопасности может отслеживать их.</span><span class="sxs-lookup"><span data-stu-id="a52a1-134">This sets the resources as a protected resource so Security Center can track it.</span></span> <span data-ttu-id="a52a1-135">Чтобы добавить ресурс как элемент внутреннего пула, необходимо войти в шлюз приложений. Для этого в текущей колонке щелкните **Консоль решений**, чтобы перейти к ресурсу шлюза приложений, где веб-приложение можно добавить во внутренний пул.</span><span class="sxs-lookup"><span data-stu-id="a52a1-135">To add the resource as a backend pool member, this must be done on the application gateway, from the current blade you can click **Solution console** to be taken to the application gateway resource where you can add the web application to the backend pool.</span></span>

![Сторонние приложения][6]

## <a name="finalize-configuration"></a><span data-ttu-id="a52a1-137">Завершение конфигурации</span><span class="sxs-lookup"><span data-stu-id="a52a1-137">Finalize configuration</span></span>

<span data-ttu-id="a52a1-138">Центр безопасности отслеживает приложения, добавленные в шлюз приложений как защищенный ресурс.</span><span class="sxs-lookup"><span data-stu-id="a52a1-138">Security Center tracks applications added to an application gateway as a protected resource.</span></span>  <span data-ttu-id="a52a1-139">Он отслеживает работоспособность этого ресурса и обеспечивает его защиту в шлюзе приложений.</span><span class="sxs-lookup"><span data-stu-id="a52a1-139">It monitors the health of this resource and ensures that it is protected by an application gateway.</span></span> <span data-ttu-id="a52a1-140">Далее во внутренний пул шлюза приложений необходимо добавить частный IP-адрес, общедоступный IP-адрес или сетевой адаптер виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a52a1-140">The next step is to add the private IP, public IP, or NIC of your virtual machine to the backend pool of the application gateway.</span></span> <span data-ttu-id="a52a1-141">Во время выполнения этих действий отображаются дополнительные рекомендации по **завершению защиты приложения**.</span><span class="sxs-lookup"><span data-stu-id="a52a1-141">Until this is done an additional recommendation of **Finalize application protection** is shown until the resource is added.</span></span>

![Колонка добавления брандмауэра веб-приложения][5]

## <a name="security-alerts"></a><span data-ttu-id="a52a1-143">Оповещения системы безопасности</span><span class="sxs-lookup"><span data-stu-id="a52a1-143">Security Alerts</span></span>

<span data-ttu-id="a52a1-144">В центре безопасности выберите **Обнаружение** > **Оповещения системы безопасности**.</span><span class="sxs-lookup"><span data-stu-id="a52a1-144">Within Security Center navigate to **DETECTION** > **Security Alerts**.</span></span>  <span data-ttu-id="a52a1-145">Здесь отображаются оповещения WAF для шлюзов приложений.</span><span class="sxs-lookup"><span data-stu-id="a52a1-145">Here you find WAF alerts for your application gateways.</span></span> <span data-ttu-id="a52a1-146">Оповещения упорядочены по правилу WAF.</span><span class="sxs-lookup"><span data-stu-id="a52a1-146">Alerts are broken down by WAF rule.</span></span>

![Оповещения системы безопасности][8]

<span data-ttu-id="a52a1-148">Если щелкнуть конкретное правило WAF, откроется список оповещений.</span><span class="sxs-lookup"><span data-stu-id="a52a1-148">Clicking an rule will provide a list of alerts for that specific WAF rule.</span></span> <span data-ttu-id="a52a1-149">Каждое оповещение содержит дополнительные сведения,</span><span class="sxs-lookup"><span data-stu-id="a52a1-149">Each alert shows additional details on the finding.</span></span> <span data-ttu-id="a52a1-150">а также ссылку на шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="a52a1-150">The details provide a link to the application gateway.</span></span>
 
![Сведения в оповещении][9]

## <a name="next-steps"></a><span data-ttu-id="a52a1-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a52a1-152">Next steps</span></span>

<span data-ttu-id="a52a1-153">Дополнительные сведения о включении брандмауэра веб-приложения в имеющемся шлюзе приложений см. в [этом разделе](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway).</span><span class="sxs-lookup"><span data-stu-id="a52a1-153">To learn how to enable web application firewall on an existing application gateway, visit [Create or update an Azure Application Gateway with web application firewall](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)</span></span>

[1]: ./media/application-gateway-integration-security-center/figure1.png
[2]: ./media/application-gateway-integration-security-center/figure2.png
[3]: ./media/application-gateway-integration-security-center/figure3.png
[4]: ./media/application-gateway-integration-security-center/figure4.png
[5]: ./media/application-gateway-integration-security-center/figure5.png
[6]: ./media/application-gateway-integration-security-center/figure6.png
[7]: ./media/application-gateway-integration-security-center/figure7.png
[8]: ./media/application-gateway-integration-security-center/securitycenter.png
[9]: ./media/application-gateway-integration-security-center/figure9.png