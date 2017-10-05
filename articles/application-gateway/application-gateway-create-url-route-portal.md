---
title: "Создание правила на основе пути для шлюза приложений Azure с помощью портала Azure | Документация Майкрософт"
description: "Узнайте, как создать правило на основе пути для шлюза приложений с помощью портала."
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 87bd93bc-e1a6-45db-a226-555948f1feb7
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: c184e94a04cfbdedcae70ed154aeb7dd134d1baf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-path-based-rule-for-an-application-gateway-by-using-the-portal"></a><span data-ttu-id="b2ecd-103">Создание правила на основе пути для шлюза приложений с помощью портала</span><span class="sxs-lookup"><span data-stu-id="b2ecd-103">Create a Path-based rule for an application gateway by using the portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b2ecd-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="b2ecd-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="b2ecd-105">PowerShell и диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="b2ecd-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="b2ecd-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b2ecd-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="b2ecd-107">Маршрутизация на основе URL-адресов позволяет связывать маршруты на основе URL-пути HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="b2ecd-107">URL Path-based routing enables you to associate routes based on the URL path of Http request.</span></span> <span data-ttu-id="b2ecd-108">Она проверяет, настроен ли для URL-адресов в шлюзе приложений маршрут к пулу тыловых серверов, и отправляет сетевой трафик в указанный пул.</span><span class="sxs-lookup"><span data-stu-id="b2ecd-108">It checks if there is a route to a back-end pool configured for the URL listed in the Application Gateway and sends the network traffic to the defined back-end pool.</span></span> <span data-ttu-id="b2ecd-109">Как правило, маршрутизация на основе URL-адресов используется для распределения запросов содержимого разных типов между разными пулами тыловых серверов.</span><span class="sxs-lookup"><span data-stu-id="b2ecd-109">A common use for URL-based routing is to load balance requests for different content types to different back-end server pools.</span></span>

<span data-ttu-id="b2ecd-110">При маршрутизации на основе URL-адресов к шлюзу приложений добавляется новый тип правил.</span><span class="sxs-lookup"><span data-stu-id="b2ecd-110">URL-based routing introduces a new rule type to application gateway.</span></span> <span data-ttu-id="b2ecd-111">Шлюз приложений имеет два типа правил: базовые правила и правила на основе пути.</span><span class="sxs-lookup"><span data-stu-id="b2ecd-111">Application gateway has two rule types: basic and path-based rules.</span></span> <span data-ttu-id="b2ecd-112">Правила базового типа выполняют циклический перебор пулов тыловых серверов, а правила на основе пути учитывают при выборе соответствующего пула тыловых серверов еще и шаблон URL-адреса запроса.</span><span class="sxs-lookup"><span data-stu-id="b2ecd-112">The basic rule type, provides round-robin service for the back-end pools while path-based rules in addition to round robin distribution, also takes path pattern of the request URL into account while choosing the appropriate backend pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="b2ecd-113">Сценарий</span><span class="sxs-lookup"><span data-stu-id="b2ecd-113">Scenario</span></span>

<span data-ttu-id="b2ecd-114">В следующем сценарии рассматривается создание правила на основе пути в существующем шлюзе приложений.</span><span class="sxs-lookup"><span data-stu-id="b2ecd-114">The following scenario goes through creating a Path-based rule in an existing application gateway.</span></span>
<span data-ttu-id="b2ecd-115">Предполагается, что действия по [созданию шлюза приложений](application-gateway-create-gateway-portal.md)уже выполнены.</span><span class="sxs-lookup"><span data-stu-id="b2ecd-115">The scenario assumes that you have already followed the steps to [Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

![Маршрут URL-адреса][scenario]

## <span data-ttu-id="b2ecd-117"><a name="createrule"></a>Создание правила на основе пути</span><span class="sxs-lookup"><span data-stu-id="b2ecd-117"><a name="createrule"></a>Create the Path-based rule</span></span>

<span data-ttu-id="b2ecd-118">Для правила на основе пути требуется собственный прослушиватель, поэтому, прежде чем создавать правило, нужно убедиться в наличии свободного прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="b2ecd-118">A Path-based rule requires its own listener, before creating the rule be sure to verify you have an available listener to use.</span></span>

### <a name="step-1"></a><span data-ttu-id="b2ecd-119">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="b2ecd-119">Step 1</span></span>

<span data-ttu-id="b2ecd-120">Перейдите на [портал Azure](http://portal.azure.com) и выберите существующий шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="b2ecd-120">Navigate to the [Azure portal](http://portal.azure.com) and select an existing application gateway.</span></span> <span data-ttu-id="b2ecd-121">Щелкните **Правила**</span><span class="sxs-lookup"><span data-stu-id="b2ecd-121">Click **Rules**</span></span>

![Обзор шлюза приложений][1]

### <a name="step-2"></a><span data-ttu-id="b2ecd-123">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="b2ecd-123">Step 2</span></span>

<span data-ttu-id="b2ecd-124">Нажмите кнопку **На основе пути** , чтобы добавить новое правило на основе пути.</span><span class="sxs-lookup"><span data-stu-id="b2ecd-124">Click **Path-based** button to add a new Path-based rule.</span></span>

### <a name="step-3"></a><span data-ttu-id="b2ecd-125">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="b2ecd-125">Step 3</span></span>

<span data-ttu-id="b2ecd-126">Колонка **добавления правила на основе пути** состоит из двух разделов.</span><span class="sxs-lookup"><span data-stu-id="b2ecd-126">The **Add path-based rule** blade has two sections.</span></span> <span data-ttu-id="b2ecd-127">В первом разделе вы определяете прослушиватель, имя правила и параметры пути по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b2ecd-127">The first section is where you defined the listener, the name of the rule and the default path settings.</span></span> <span data-ttu-id="b2ecd-128">Параметры пути по умолчанию используются для тех маршрутов, которые не соответствуют пользовательским маршрутам на основе пути.</span><span class="sxs-lookup"><span data-stu-id="b2ecd-128">The default path settings are for routes that do not fall under the custom path-based route.</span></span> <span data-ttu-id="b2ecd-129">Во второй части колонки **добавления правила на основе пути** определяются сами правила на основе пути.</span><span class="sxs-lookup"><span data-stu-id="b2ecd-129">The second section of the **Add path-based rule** blade is where you define the path-based rules themselves.</span></span>

<span data-ttu-id="b2ecd-130">**Основные параметры**</span><span class="sxs-lookup"><span data-stu-id="b2ecd-130">**Basic Settings**</span></span>

* <span data-ttu-id="b2ecd-131">**Имя** — понятное имя правила, которое отображается на портале.</span><span class="sxs-lookup"><span data-stu-id="b2ecd-131">**Name** - This value is a friendly name to the rule that is accessible in the portal.</span></span>
* <span data-ttu-id="b2ecd-132">**Прослушиватель** — прослушиватель, который используется для этого правила.</span><span class="sxs-lookup"><span data-stu-id="b2ecd-132">**Listener** - This value is the listener that is used for the rule.</span></span>
* <span data-ttu-id="b2ecd-133">**Пул тыловых серверов по умолчанию** — этот параметр определяет, какие тыловые серверы будут использоваться для правила по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b2ecd-133">**Default backend pool** - This setting is the setting that defines the back-end to be used for the default rule</span></span>
* <span data-ttu-id="b2ecd-134">**Параметр HTTP по умолчанию** — этот параметр определяет, какие параметры HTTP будут использоваться для правила по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b2ecd-134">**Default HTTP settings** - This setting is the setting that defines the HTTP settings to be used for the default rule.</span></span>

<span data-ttu-id="b2ecd-135">**Правила на основе пути**</span><span class="sxs-lookup"><span data-stu-id="b2ecd-135">**Path-based rules**</span></span>

* <span data-ttu-id="b2ecd-136">**Имя** — понятное пользователю имя правила на основе пути.</span><span class="sxs-lookup"><span data-stu-id="b2ecd-136">**Name** - This value is a friendly name to path-based rule.</span></span>
* <span data-ttu-id="b2ecd-137">**Пути** — этот параметр определяет путь, который будет использоваться правилом для перенаправления трафика.</span><span class="sxs-lookup"><span data-stu-id="b2ecd-137">**Paths** - This setting defines the path the rule looks for when forwarding traffic</span></span>
* <span data-ttu-id="b2ecd-138">**Пул тыловых серверов** — этот параметр определяет, какие тыловые серверы будут использоваться для этого правила.</span><span class="sxs-lookup"><span data-stu-id="b2ecd-138">**Backend Pool** - This setting is the setting that defines the back-end to be used for the rule</span></span>
* <span data-ttu-id="b2ecd-139">**Параметры HTTP** — этот параметр определяет, какие параметры HTTP будут использоваться для этого правила.</span><span class="sxs-lookup"><span data-stu-id="b2ecd-139">**HTTP setting** - This setting is the setting that defines the HTTP settings to be used for the rule.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b2ecd-140">Пути: список шаблонов пути для сопоставления.</span><span class="sxs-lookup"><span data-stu-id="b2ecd-140">Paths: The list of path patterns to match.</span></span> <span data-ttu-id="b2ecd-141">Каждый шаблон должен начинаться с косой черты (/). Знак "\*" может находиться только в конце.</span><span class="sxs-lookup"><span data-stu-id="b2ecd-141">Each must start with / and the only place a "\*" is allowed is at the end.</span></span> <span data-ttu-id="b2ecd-142">Примеры допустимых значений: /xyz, /xyz* или /xyz/*.</span><span class="sxs-lookup"><span data-stu-id="b2ecd-142">Valid examples are /xyz, /xyz* or /xyz/*.</span></span>  

![Колонка добавления правила на основе пути с заполненной информацией][2]

<span data-ttu-id="b2ecd-144">Добавить правило на основе пути к существующему шлюзу приложения на портале очень просто.</span><span class="sxs-lookup"><span data-stu-id="b2ecd-144">Adding a path-based rule to an existing application gateway is an easy process through the portal.</span></span> <span data-ttu-id="b2ecd-145">Созданное правило на основе пути можно легко изменить, добавив дополнительные правила.</span><span class="sxs-lookup"><span data-stu-id="b2ecd-145">After a path-based rule has been created, it can be edited to add additional rules.</span></span> 

![добавление правил на основе пути][3]

<span data-ttu-id="b2ecd-147">Так настраивается маршрут на основе пути.</span><span class="sxs-lookup"><span data-stu-id="b2ecd-147">This step configures a path-based route.</span></span> <span data-ttu-id="b2ecd-148">Очень важно понять, что запросы не перезаписываются, так как запросы шлюза приложений проверяются при поступлении, а базовый элемент шаблона URL-адреса отправляет запрос к соответствующему серверу.</span><span class="sxs-lookup"><span data-stu-id="b2ecd-148">It is important to understand that requests are not rewritten, as requests come in application gateway inspects the request and basic on the url pattern sends the request to the appropriate back-end.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2ecd-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b2ecd-149">Next steps</span></span>

<span data-ttu-id="b2ecd-150">Сведения по настройке разгрузки SSL с использованием шлюза приложений Azure см. в статье [Настройка шлюза приложений для разгрузки SSL с помощью портала](application-gateway-ssl-portal.md)</span><span class="sxs-lookup"><span data-stu-id="b2ecd-150">To learn how to configure SSL Offloading with Azure Application Gateway, see [Configure SSL Offload](application-gateway-ssl-portal.md)</span></span>

[1]: ./media/application-gateway-create-url-route-portal/figure1.png
[2]: ./media/application-gateway-create-url-route-portal/figure2.png
[3]: ./media/application-gateway-create-url-route-portal/figure3.png
[scenario]: ./media/application-gateway-create-url-route-portal/scenario.png
