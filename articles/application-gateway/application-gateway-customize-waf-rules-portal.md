---
title: "правила брандмауэра приложения web aaaCustomize в шлюз приложений Azure — портал Azure | Документы Microsoft"
description: "Это статье содержатся сведения о работе правил toocustomize брандмауэр веб-приложения в приложение шлюза с портала Azure hello."
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
ms.openlocfilehash: 36a999279e0370b9f803e12257856a56753b23a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="customize-web-application-firewall-rules-through-hello-azure-portal"></a><span data-ttu-id="704d7-103">Настроить правила брандмауэра веб-приложения через портал Azure hello</span><span class="sxs-lookup"><span data-stu-id="704d7-103">Customize web application firewall rules through hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="704d7-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="704d7-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="704d7-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="704d7-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="704d7-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="704d7-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="704d7-107">брандмауэр веб-приложения Azure шлюза приложения Hello (WAF) обеспечивает защиту веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="704d7-107">hello Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="704d7-108">Эти протоколы предоставляются Привет открыть Web приложения безопасности проекта (OWASP) задайте правило Core (CRS).</span><span class="sxs-lookup"><span data-stu-id="704d7-108">These protections are provided by hello Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="704d7-109">Некоторые правила могут приводить к ложным срабатываниям и блокировке реального трафика.</span><span class="sxs-lookup"><span data-stu-id="704d7-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="704d7-110">По этой причине использование шлюза приложений содержит группы правил toocustomize возможность hello и правила.</span><span class="sxs-lookup"><span data-stu-id="704d7-110">For this reason, Application Gateway provides hello capability toocustomize rule groups and rules.</span></span> <span data-ttu-id="704d7-111">Дополнительные сведения о hello конкретных групп правил и правил см. в разделе [список правил и групп правил CRS брандмауэра приложения web](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="704d7-111">For more information on hello specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

>[!NOTE]
> <span data-ttu-id="704d7-112">Если шлюз приложений не использует уровень WAF hello, hello параметр tooupgrade hello шлюза toohello WAF уровня приложения отображается hello правой панели.</span><span class="sxs-lookup"><span data-stu-id="704d7-112">If your application gateway is not using hello WAF tier, hello option tooupgrade hello application gateway toohello WAF tier appears in hello right pane.</span></span> 

![Включение WAF][fig1]

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="704d7-114">Просмотр правил и групп правил</span><span class="sxs-lookup"><span data-stu-id="704d7-114">View rule groups and rules</span></span>

<span data-ttu-id="704d7-115">**tooview группы правил и правила**</span><span class="sxs-lookup"><span data-stu-id="704d7-115">**tooview rule groups and rules**</span></span>
   1. <span data-ttu-id="704d7-116">Обзор шлюза toohello приложений, а затем выберите **брандмауэр веб-приложения**.</span><span class="sxs-lookup"><span data-stu-id="704d7-116">Browse toohello application gateway, and then select **Web application firewall**.</span></span>  
   2. <span data-ttu-id="704d7-117">Выберите **Advanced rule configuration** (Расширенная настройка правил).</span><span class="sxs-lookup"><span data-stu-id="704d7-117">Select **Advanced rule configuration**.</span></span>  
   <span data-ttu-id="704d7-118">В этом представлении отображается таблица на странице приветствия все группы правил hello, в состав hello выбранный набор правил.</span><span class="sxs-lookup"><span data-stu-id="704d7-118">This view shows a table on hello page of all hello rule groups provided with hello chosen rule set.</span></span> <span data-ttu-id="704d7-119">Будут выбраны все флажки hello правило.</span><span class="sxs-lookup"><span data-stu-id="704d7-119">All of hello rule's check boxes are selected.</span></span>

![Настройка отключенных правил][1]

## <a name="search-for-rules-toodisable"></a><span data-ttu-id="704d7-121">Поиск правил toodisable</span><span class="sxs-lookup"><span data-stu-id="704d7-121">Search for rules toodisable</span></span>

<span data-ttu-id="704d7-122">Hello **веб-приложения параметры брандмауэра** колонке предоставляет возможность hello toofilter hello правил при помощи полнотекстового поиска.</span><span class="sxs-lookup"><span data-stu-id="704d7-122">hello **Web application firewall settings** blade provides hello capability toofilter hello rules through a text search.</span></span> <span data-ttu-id="704d7-123">результат Hello отображает только группы правил hello и правила, которые содержат текст hello, который вы ищете.</span><span class="sxs-lookup"><span data-stu-id="704d7-123">hello result displays only hello rule groups and rules that contain hello text you searched for.</span></span>

![Поиск правил][2]

## <a name="disable-rule-groups-and-rules"></a><span data-ttu-id="704d7-125">Отключение правил и групп правил</span><span class="sxs-lookup"><span data-stu-id="704d7-125">Disable rule groups and rules</span></span>

<span data-ttu-id="704d7-126">При отключении правил можно отключить всю группу правил или определенные правила в одной или нескольких группах.</span><span class="sxs-lookup"><span data-stu-id="704d7-126">When your're disabling rules, you can disable an entire rule group or specific rules under one or more rule groups.</span></span> 

<span data-ttu-id="704d7-127">**группы правил toodisable или определенные правила**</span><span class="sxs-lookup"><span data-stu-id="704d7-127">**toodisable rule groups or specific rules**</span></span>

   1. <span data-ttu-id="704d7-128">Поиск правил hello или группы правил, которые должны toodisable.</span><span class="sxs-lookup"><span data-stu-id="704d7-128">Search for hello rules or rule groups that you want toodisable.</span></span>
   2. <span data-ttu-id="704d7-129">Снимите флажки hello hello правил, которые должны toodisable.</span><span class="sxs-lookup"><span data-stu-id="704d7-129">Clear hello check boxes for hello rules that you want toodisable.</span></span> 
   2. <span data-ttu-id="704d7-130">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="704d7-130">Select **Save**.</span></span> 

![Сохранение изменений][3]

## <a name="next-steps"></a><span data-ttu-id="704d7-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="704d7-132">Next steps</span></span>

<span data-ttu-id="704d7-133">После настройки вашей отключенные правила, вы узнаете как tooview WAF журналов.</span><span class="sxs-lookup"><span data-stu-id="704d7-133">After you configure your disabled rules, you can learn how tooview your WAF logs.</span></span> <span data-ttu-id="704d7-134">Дополнительные сведения см. в разделе [Журналы диагностики](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="704d7-134">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
