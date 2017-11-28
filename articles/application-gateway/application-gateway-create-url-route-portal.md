---
title: "Портал Azure — шлюз приложений Azure — правило aaaCreate, основанную на пути | Документы Microsoft"
description: "Узнайте, как правило на основе пути для шлюза приложения с помощью toocreate hello портала"
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
ms.openlocfilehash: 21cb52c426ca5f7dfedf07a96e87fbc85d243647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-path-based-rule-for-an-application-gateway-by-using-hello-portal"></a><span data-ttu-id="7b4f8-103">Создание правила на основе пути для шлюза приложения с помощью портала hello</span><span class="sxs-lookup"><span data-stu-id="7b4f8-103">Create a Path-based rule for an application gateway by using hello portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7b4f8-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="7b4f8-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="7b4f8-105">PowerShell и диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="7b4f8-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="7b4f8-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="7b4f8-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="7b4f8-107">Маршрутизация URL-адрес на основе пути позволяет вам tooassociate маршрутов на основе hello пути URL-адреса HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="7b4f8-107">URL Path-based routing enables you tooassociate routes based on hello URL path of Http request.</span></span> <span data-ttu-id="7b4f8-108">Он проверяет при внутреннем пул tooa маршрута, настроенный для hello URL, перечисленных в hello шлюза приложений и отправляет hello сетевой трафик toohello определенного пула серверной части.</span><span class="sxs-lookup"><span data-stu-id="7b4f8-108">It checks if there is a route tooa back-end pool configured for hello URL listed in hello Application Gateway and sends hello network traffic toohello defined back-end pool.</span></span> <span data-ttu-id="7b4f8-109">Обычно используются для маршрутизации на основе URL-адрес — tooload балансировать нагрузку по запросам для различных типов содержимого toodifferent серверных пулов.</span><span class="sxs-lookup"><span data-stu-id="7b4f8-109">A common use for URL-based routing is tooload balance requests for different content types toodifferent back-end server pools.</span></span>

<span data-ttu-id="7b4f8-110">Маршрутизация на основе URL-адрес появился новый шлюз tooapplication тип правила.</span><span class="sxs-lookup"><span data-stu-id="7b4f8-110">URL-based routing introduces a new rule type tooapplication gateway.</span></span> <span data-ttu-id="7b4f8-111">Шлюз приложений имеет два типа правил: базовые правила и правила на основе пути.</span><span class="sxs-lookup"><span data-stu-id="7b4f8-111">Application gateway has two rule types: basic and path-based rules.</span></span> <span data-ttu-id="7b4f8-112">Здравствуйте, тип основные правила, предоставляет циклического службы для внутреннего интерфейса hello пулов при правила на основе пути Кроме распространения tooround циклический перебор, также учитывает шаблон пути URL-адреса запроса hello при выборе hello соответствующий внутренний пул.</span><span class="sxs-lookup"><span data-stu-id="7b4f8-112">hello basic rule type, provides round-robin service for hello back-end pools while path-based rules in addition tooround robin distribution, also takes path pattern of hello request URL into account while choosing hello appropriate backend pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="7b4f8-113">Сценарий</span><span class="sxs-lookup"><span data-stu-id="7b4f8-113">Scenario</span></span>

<span data-ttu-id="7b4f8-114">Hello следующий сценарий рассмотрено создание правила на основе пути в существующего шлюза приложения.</span><span class="sxs-lookup"><span data-stu-id="7b4f8-114">hello following scenario goes through creating a Path-based rule in an existing application gateway.</span></span>
<span data-ttu-id="7b4f8-115">Hello сценарии предполагается, что уже выполнены действия hello слишком[создания шлюза приложения](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7b4f8-115">hello scenario assumes that you have already followed hello steps too[Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

![Маршрут URL-адреса][scenario]

## <span data-ttu-id="7b4f8-117"><a name="createrule"></a>Создание правила на основе пути hello</span><span class="sxs-lookup"><span data-stu-id="7b4f8-117"><a name="createrule"></a>Create hello Path-based rule</span></span>

<span data-ttu-id="7b4f8-118">Правила на основе пути требуется собственный прослушиватель перед созданием hello правило будет убедиться, что tooverify, у вас есть toouse доступных прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="7b4f8-118">A Path-based rule requires its own listener, before creating hello rule be sure tooverify you have an available listener toouse.</span></span>

### <a name="step-1"></a><span data-ttu-id="7b4f8-119">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="7b4f8-119">Step 1</span></span>

<span data-ttu-id="7b4f8-120">Перейдите toohello [портал Azure](http://portal.azure.com) и выберите существующий шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="7b4f8-120">Navigate toohello [Azure portal](http://portal.azure.com) and select an existing application gateway.</span></span> <span data-ttu-id="7b4f8-121">Щелкните **Правила**</span><span class="sxs-lookup"><span data-stu-id="7b4f8-121">Click **Rules**</span></span>

![Обзор шлюза приложений][1]

### <a name="step-2"></a><span data-ttu-id="7b4f8-123">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="7b4f8-123">Step 2</span></span>

<span data-ttu-id="7b4f8-124">Нажмите кнопку **основанную на пути** tooadd кнопку новое правило пути.</span><span class="sxs-lookup"><span data-stu-id="7b4f8-124">Click **Path-based** button tooadd a new Path-based rule.</span></span>

### <a name="step-3"></a><span data-ttu-id="7b4f8-125">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="7b4f8-125">Step 3</span></span>

<span data-ttu-id="7b4f8-126">Hello **добавить правило на основе пути** колонке состоит из двух разделов.</span><span class="sxs-lookup"><span data-stu-id="7b4f8-126">hello **Add path-based rule** blade has two sections.</span></span> <span data-ttu-id="7b4f8-127">Первый раздел Hello —, где определен прослушиватель hello, имя hello hello правила и параметры пути по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="7b4f8-127">hello first section is where you defined hello listener, hello name of hello rule and hello default path settings.</span></span> <span data-ttu-id="7b4f8-128">параметры пути по умолчанию Hello предназначены для маршрутов, не вошедшие в hello пользовательский путь маршрутов на основе.</span><span class="sxs-lookup"><span data-stu-id="7b4f8-128">hello default path settings are for routes that do not fall under hello custom path-based route.</span></span> <span data-ttu-id="7b4f8-129">Здравствуйте, во второй части hello **добавить правило на основе пути** колонка является определение правила на основе пути hello сами.</span><span class="sxs-lookup"><span data-stu-id="7b4f8-129">hello second section of hello **Add path-based rule** blade is where you define hello path-based rules themselves.</span></span>

<span data-ttu-id="7b4f8-130">**Основные параметры**</span><span class="sxs-lookup"><span data-stu-id="7b4f8-130">**Basic Settings**</span></span>

* <span data-ttu-id="7b4f8-131">**Имя** -это значение является понятное имя toohello правило, доступной на портале hello.</span><span class="sxs-lookup"><span data-stu-id="7b4f8-131">**Name** - This value is a friendly name toohello rule that is accessible in hello portal.</span></span>
* <span data-ttu-id="7b4f8-132">**Прослушиватель** -это значение равно hello прослушиватель, который используется для правила hello.</span><span class="sxs-lookup"><span data-stu-id="7b4f8-132">**Listener** - This value is hello listener that is used for hello rule.</span></span>
* <span data-ttu-id="7b4f8-133">**По умолчанию серверный пул** -это является параметром hello, который определяет toobe hello серверной части, используемые для правила по умолчанию hello</span><span class="sxs-lookup"><span data-stu-id="7b4f8-133">**Default backend pool** - This setting is hello setting that defines hello back-end toobe used for hello default rule</span></span>
* <span data-ttu-id="7b4f8-134">**Параметры HTTP по умолчанию** -это является параметром hello, который определяет параметры toobe hello HTTP, используемый для правила по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="7b4f8-134">**Default HTTP settings** - This setting is hello setting that defines hello HTTP settings toobe used for hello default rule.</span></span>

<span data-ttu-id="7b4f8-135">**Правила на основе пути**</span><span class="sxs-lookup"><span data-stu-id="7b4f8-135">**Path-based rules**</span></span>

* <span data-ttu-id="7b4f8-136">**Имя** -это значение — это понятное имя на основе toopath правило.</span><span class="sxs-lookup"><span data-stu-id="7b4f8-136">**Name** - This value is a friendly name toopath-based rule.</span></span>
* <span data-ttu-id="7b4f8-137">**Пути** -этот параметр определяет hello путь hello правило ищет перенаправления трафика</span><span class="sxs-lookup"><span data-stu-id="7b4f8-137">**Paths** - This setting defines hello path hello rule looks for when forwarding traffic</span></span>
* <span data-ttu-id="7b4f8-138">**Внутренний пул** -это является параметром hello, который определяет toobe серверной части hello, используемый для правила hello</span><span class="sxs-lookup"><span data-stu-id="7b4f8-138">**Backend Pool** - This setting is hello setting that defines hello back-end toobe used for hello rule</span></span>
* <span data-ttu-id="7b4f8-139">**Параметр HTTP** -это является параметром hello, который определяет параметры toobe hello HTTP, используется для правила hello.</span><span class="sxs-lookup"><span data-stu-id="7b4f8-139">**HTTP setting** - This setting is hello setting that defines hello HTTP settings toobe used for hello rule.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7b4f8-140">Путей: список hello toomatch шаблонов пути.</span><span class="sxs-lookup"><span data-stu-id="7b4f8-140">Paths: hello list of path patterns toomatch.</span></span> <span data-ttu-id="7b4f8-141">Каждый должно начинаться с / и hello единственное место «\*» может быть на стороне hello.</span><span class="sxs-lookup"><span data-stu-id="7b4f8-141">Each must start with / and hello only place a "\*" is allowed is at hello end.</span></span> <span data-ttu-id="7b4f8-142">Примеры допустимых значений: /xyz, /xyz* или /xyz/*.</span><span class="sxs-lookup"><span data-stu-id="7b4f8-142">Valid examples are /xyz, /xyz* or /xyz/*.</span></span>  

![Колонка добавления правила на основе пути с заполненной информацией][2]

<span data-ttu-id="7b4f8-144">Добавление tooan правила на основе пути существующего шлюза приложения — это простой процесс, через портал hello.</span><span class="sxs-lookup"><span data-stu-id="7b4f8-144">Adding a path-based rule tooan existing application gateway is an easy process through hello portal.</span></span> <span data-ttu-id="7b4f8-145">После создания правила на основе путь может быть измененного tooadd Дополнительные правила.</span><span class="sxs-lookup"><span data-stu-id="7b4f8-145">After a path-based rule has been created, it can be edited tooadd additional rules.</span></span> 

![добавление правил на основе пути][3]

<span data-ttu-id="7b4f8-147">Так настраивается маршрут на основе пути.</span><span class="sxs-lookup"><span data-stu-id="7b4f8-147">This step configures a path-based route.</span></span> <span data-ttu-id="7b4f8-148">Важные toounderstand запросы не перезаписываются, при поступлении запросов шлюз приложений проверяет запрос hello и basic на hello URL-адрес шаблона отправляет hello запроса toohello соответствующие серверной части.</span><span class="sxs-lookup"><span data-stu-id="7b4f8-148">It is important toounderstand that requests are not rewritten, as requests come in application gateway inspects hello request and basic on hello url pattern sends hello request toohello appropriate back-end.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b4f8-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7b4f8-149">Next steps</span></span>

<span data-ttu-id="7b4f8-150">toolearn tooconfigure разгрузки SSL со шлюзом приложения Azure, в статье [Настройка разгрузки SSL](application-gateway-ssl-portal.md)</span><span class="sxs-lookup"><span data-stu-id="7b4f8-150">toolearn how tooconfigure SSL Offloading with Azure Application Gateway, see [Configure SSL Offload](application-gateway-ssl-portal.md)</span></span>

[1]: ./media/application-gateway-create-url-route-portal/figure1.png
[2]: ./media/application-gateway-create-url-route-portal/figure2.png
[3]: ./media/application-gateway-create-url-route-portal/figure3.png
[scenario]: ./media/application-gateway-create-url-route-portal/scenario.png
