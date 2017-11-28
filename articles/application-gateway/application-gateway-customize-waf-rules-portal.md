---
title: "Настройка правил брандмауэра веб-приложения для шлюза приложений Azure с помощью портала Azure | Документация Майкрософт"
description: "Эта статья содержит сведения о том, как настроить правила брандмауэра веб-приложения в шлюзе приложений с помощью портала Azure."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 1159500b-17ba-41e7-88d6-b96986795084
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 03/28/2017
ms.author: gwallace
ms.openlocfilehash: cdcbadbc3765dfc583c26e1b1453863d421c9a72
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="customize-web-application-firewall-rules-through-the-azure-portal"></a><span data-ttu-id="2811f-103">Настройка правил брандмауэра веб-приложения с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="2811f-103">Customize web application firewall rules through the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2811f-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="2811f-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="2811f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2811f-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="2811f-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2811f-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="2811f-107">Брандмауэр веб-приложения (WAF) шлюза приложений Azure обеспечивает защиту веб-приложений</span><span class="sxs-lookup"><span data-stu-id="2811f-107">The Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="2811f-108">с помощью основного набора правил (CRS) открытого проекта безопасности веб-приложений (OWASP).</span><span class="sxs-lookup"><span data-stu-id="2811f-108">These protections are provided by the Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="2811f-109">Некоторые правила могут приводить к ложным срабатываниям и блокировке реального трафика.</span><span class="sxs-lookup"><span data-stu-id="2811f-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="2811f-110">Поэтому шлюз приложений предоставляет возможность настроить правила и группы правил.</span><span class="sxs-lookup"><span data-stu-id="2811f-110">For this reason, Application Gateway provides the capability to customize rule groups and rules.</span></span> <span data-ttu-id="2811f-111">Дополнительные сведения о конкретных правилах и группах правил см. в статье [Список групп правил и правил CRS брандмауэра веб-приложения](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="2811f-111">For more information on the specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

>[!NOTE]
> <span data-ttu-id="2811f-112">Если шлюз приложений не использует уровень WAF, на правой панели будет предоставлена возможность обновить шлюз приложений до уровня WAF.</span><span class="sxs-lookup"><span data-stu-id="2811f-112">If your application gateway is not using the WAF tier, the option to upgrade the application gateway to the WAF tier appears in the right pane.</span></span> 

![Включение WAF][fig1]

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="2811f-114">Просмотр правил и групп правил</span><span class="sxs-lookup"><span data-stu-id="2811f-114">View rule groups and rules</span></span>

<span data-ttu-id="2811f-115">**Чтобы просмотреть правила и группы правил, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="2811f-115">**To view rule groups and rules**</span></span>
   1. <span data-ttu-id="2811f-116">Перейдите к шлюзу приложений, а затем выберите **Брандмауэр веб-приложения**.</span><span class="sxs-lookup"><span data-stu-id="2811f-116">Browse to the application gateway, and then select **Web application firewall**.</span></span>  
   2. <span data-ttu-id="2811f-117">Выберите **Advanced rule configuration** (Расширенная настройка правил).</span><span class="sxs-lookup"><span data-stu-id="2811f-117">Select **Advanced rule configuration**.</span></span>  
   <span data-ttu-id="2811f-118">В этом представлении появится страница со всеми группами правил и таблицей с выбранным набором правил.</span><span class="sxs-lookup"><span data-stu-id="2811f-118">This view shows a table on the page of all the rule groups provided with the chosen rule set.</span></span> <span data-ttu-id="2811f-119">Для правила установлены все флажки.</span><span class="sxs-lookup"><span data-stu-id="2811f-119">All of the rule's check boxes are selected.</span></span>

![Настройка отключенных правил][1]

## <a name="search-for-rules-to-disable"></a><span data-ttu-id="2811f-121">Поиск правил для отключения</span><span class="sxs-lookup"><span data-stu-id="2811f-121">Search for rules to disable</span></span>

<span data-ttu-id="2811f-122">В колонке **параметров брандмауэра веб-приложения** есть функция фильтрации правил по текстовому поиску.</span><span class="sxs-lookup"><span data-stu-id="2811f-122">The **Web application firewall settings** blade provides the capability to filter the rules through a text search.</span></span> <span data-ttu-id="2811f-123">Отобразятся только правила и группы правил, которые содержат искомый текст.</span><span class="sxs-lookup"><span data-stu-id="2811f-123">The result displays only the rule groups and rules that contain the text you searched for.</span></span>

![Поиск правил][2]

## <a name="disable-rule-groups-and-rules"></a><span data-ttu-id="2811f-125">Отключение правил и групп правил</span><span class="sxs-lookup"><span data-stu-id="2811f-125">Disable rule groups and rules</span></span>

<span data-ttu-id="2811f-126">При отключении правил можно отключить всю группу правил или определенные правила в одной или нескольких группах.</span><span class="sxs-lookup"><span data-stu-id="2811f-126">When your're disabling rules, you can disable an entire rule group or specific rules under one or more rule groups.</span></span> 

<span data-ttu-id="2811f-127">**Чтобы отключить группы правил или конкретные правила, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="2811f-127">**To disable rule groups or specific rules**</span></span>

   1. <span data-ttu-id="2811f-128">Найдите правила или группы правил, которые необходимо отключить.</span><span class="sxs-lookup"><span data-stu-id="2811f-128">Search for the rules or rule groups that you want to disable.</span></span>
   2. <span data-ttu-id="2811f-129">Снимите флажки для правил, которые необходимо отключить.</span><span class="sxs-lookup"><span data-stu-id="2811f-129">Clear the check boxes for the rules that you want to disable.</span></span> 
   2. <span data-ttu-id="2811f-130">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="2811f-130">Select **Save**.</span></span> 

![Сохранение изменений][3]

## <a name="next-steps"></a><span data-ttu-id="2811f-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2811f-132">Next steps</span></span>

<span data-ttu-id="2811f-133">После настройки с отключением правил вы можете узнать, как просматривать журналы WAF.</span><span class="sxs-lookup"><span data-stu-id="2811f-133">After you configure your disabled rules, you can learn how to view your WAF logs.</span></span> <span data-ttu-id="2811f-134">Дополнительные сведения см. в разделе [Журналы диагностики](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="2811f-134">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
