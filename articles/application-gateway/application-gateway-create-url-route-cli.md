---
title: "Создание шлюза приложений с использованием правил маршрутизации URL-адресов с помощью Azure CLI 2.0 | Документация Майкрософт"
description: "На этой странице приводятся инструкции по созданию и настройке шлюза приложений Azure с помощью правил маршрутизации URL-адресов."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: 958049830d6753ec26635f18f8f8b2fabdec0733
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-gateway-using-path-based-routing-with-azure-cli-20"></a><span data-ttu-id="77cbf-103">Создание шлюза приложений с помощью маршрутизации на основе пути с использованием Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="77cbf-103">Create an application gateway using Path-based routing with Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="77cbf-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="77cbf-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="77cbf-105">PowerShell и диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="77cbf-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="77cbf-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="77cbf-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="77cbf-107">Маршрутизация на основе URL-адресов позволяет связывать маршруты на основе URL-пути HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="77cbf-107">URL Path-based routing enables you to associate routes based on the URL path of an Http request.</span></span> <span data-ttu-id="77cbf-108">Она проверяет, настроен ли для URL-адресов в шлюзе приложений маршрут к пулу тыловых серверов, и отправляет сетевой трафик в указанный пул.</span><span class="sxs-lookup"><span data-stu-id="77cbf-108">It checks if there is a route to a back-end pool configured for the URL presented in the Application Gateway and sends the network traffic to the defined back-end pool.</span></span> <span data-ttu-id="77cbf-109">Как правило, маршрутизация на основе URL-адресов используется для распределения запросов содержимого разных типов между разными пулами тыловых серверов.</span><span class="sxs-lookup"><span data-stu-id="77cbf-109">A common use for URL-based routing is to load balance requests for different content types to different back-end server pools.</span></span>

<span data-ttu-id="77cbf-110">При маршрутизации на основе URL-адресов к шлюзу приложений добавляется новый тип правил.</span><span class="sxs-lookup"><span data-stu-id="77cbf-110">URL-based routing introduces a new rule type to application gateway.</span></span> <span data-ttu-id="77cbf-111">Шлюз приложений имеет два типа правил: базовые правила и правила на основе пути.</span><span class="sxs-lookup"><span data-stu-id="77cbf-111">Application gateway has two rule types: basic and PathBasedRouting.</span></span> <span data-ttu-id="77cbf-112">Основной тип правил обеспечивает циклическое обслуживание пулов тыловых серверов, а PathBasedRouting наряду с циклическим распространением при выборе пула тыловых серверов учитывает также шаблон URL-адреса запроса.</span><span class="sxs-lookup"><span data-stu-id="77cbf-112">Basic rule type provides round-robin service for the back-end pools while PathBasedRouting in addition to round robin distribution, also takes path pattern of the request URL into account while choosing the back-end pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="77cbf-113">Сценарий</span><span class="sxs-lookup"><span data-stu-id="77cbf-113">Scenario</span></span>

<span data-ttu-id="77cbf-114">В следующем примере шлюз приложений обслуживает трафик веб-сайта contoso.com с помощью двух пулов тыловых серверов: пула серверов по умолчанию и пула серверов для изображений.</span><span class="sxs-lookup"><span data-stu-id="77cbf-114">In the following example, Application Gateway is serving traffic for contoso.com with two back-end server pools: a default server pool and an image server pool.</span></span>

<span data-ttu-id="77cbf-115">Запросы http://contoso.com/image* направляются в пул серверов для изображений (imagesBackendPool). Если шаблон пути не совпадает, выбирается пул серверов по умолчанию (appGatewayBackendPool).</span><span class="sxs-lookup"><span data-stu-id="77cbf-115">Requests for http://contoso.com/image* are routed to image server pool (imagesBackendPool), if the path pattern does not match, a default server pool (appGatewayBackendPool) is selected.</span></span>

![Маршрут URL-адреса](./media/application-gateway-create-url-route-cli/scenario.png)

## <a name="log-in-to-azure"></a><span data-ttu-id="77cbf-117">Вход в Azure</span><span class="sxs-lookup"><span data-stu-id="77cbf-117">Log in to Azure</span></span>

<span data-ttu-id="77cbf-118">Откройте **командную строку Microsoft Azure**, и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="77cbf-118">Open the **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli
az login -u "username"
```

> [!NOTE]
> <span data-ttu-id="77cbf-119">Команду `az login` также можно использовать без параметра для входа на устройство, при котором требуется ввести код на странице aka.ms/devicelogin.</span><span class="sxs-lookup"><span data-stu-id="77cbf-119">You can also use `az login` without the switch for device login that requires entering a code at aka.ms/devicelogin.</span></span>

<span data-ttu-id="77cbf-120">Введя предыдущий пример, вы получите код.</span><span class="sxs-lookup"><span data-stu-id="77cbf-120">Once you type the preceding example, a code is provided.</span></span> <span data-ttu-id="77cbf-121">В браузере перейдите по адресу https://aka.ms/devicelogin, чтобы продолжить процедуру входа.</span><span class="sxs-lookup"><span data-stu-id="77cbf-121">Navigate to https://aka.ms/devicelogin in a browser to continue the login process.</span></span>

![Команда, выводящая имя пользователя устройства][1]

<span data-ttu-id="77cbf-123">В браузере введите полученный код.</span><span class="sxs-lookup"><span data-stu-id="77cbf-123">In the browser, enter the code you received.</span></span> <span data-ttu-id="77cbf-124">Вы будете перенаправлены на страницу входа.</span><span class="sxs-lookup"><span data-stu-id="77cbf-124">You are redirected to a sign-in page.</span></span>

![Ввод кода в браузере][2]

<span data-ttu-id="77cbf-126">Когда вы выполните вход, введя код, закройте браузер, чтобы продолжить работу.</span><span class="sxs-lookup"><span data-stu-id="77cbf-126">Once the code has been entered you are signed in, close the browser to continue on with the scenario.</span></span>

![Вход выполнен][3]

## <a name="add-a-path-based-rule-to-an-existing-application-gateway"></a><span data-ttu-id="77cbf-128">Добавление правила на основе пути для имеющегося шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="77cbf-128">Add a path-based rule to an existing application gateway</span></span>

<span data-ttu-id="77cbf-129">Создание шлюза приложений с определенным правилом на основе пути</span><span class="sxs-lookup"><span data-stu-id="77cbf-129">Create an application gateway with a path rule defined</span></span>

### <a name="create-a-new-back-end-pool"></a><span data-ttu-id="77cbf-130">Создание внутреннего пула</span><span class="sxs-lookup"><span data-stu-id="77cbf-130">Create a new back-end pool</span></span>

<span data-ttu-id="77cbf-131">Настройте параметр **imagesBackendPool** шлюза приложений для балансировки нагрузки сетевого трафика во внутреннем пуле.</span><span class="sxs-lookup"><span data-stu-id="77cbf-131">Configure application gateway setting **imagesBackendPool** for the load-balanced network traffic in the back-end pool.</span></span> <span data-ttu-id="77cbf-132">В этом примере вы настроите различные параметры новых пулов тыловых серверов.</span><span class="sxs-lookup"><span data-stu-id="77cbf-132">In this example, you configure different back-end pool settings for the new back-end pool.</span></span> <span data-ttu-id="77cbf-133">Для каждого пула тыловых серверов параметры можно настроить отдельно.</span><span class="sxs-lookup"><span data-stu-id="77cbf-133">Each back-end pool can have its own back-end pool setting.</span></span>  <span data-ttu-id="77cbf-134">Серверные параметры HTTP используются правилами для перенаправления трафика соответствующим участникам серверного пула.</span><span class="sxs-lookup"><span data-stu-id="77cbf-134">Backend HTTP settings are used by rules to route traffic to the correct backend pool members.</span></span> <span data-ttu-id="77cbf-135">Они определяют протокол и порт, используемый для отправки трафика участникам серверного пула.</span><span class="sxs-lookup"><span data-stu-id="77cbf-135">This determines the protocol and port that is used when sending traffic to the backend pool members.</span></span> <span data-ttu-id="77cbf-136">Сеансы на основе файлов cookie также определяются с помощью серверных параметров HTTP.</span><span class="sxs-lookup"><span data-stu-id="77cbf-136">Cookie-based sessions are also determined by the backend HTTP settings.</span></span>  <span data-ttu-id="77cbf-137">Если этот параметр включен, соответствие сеансу на основе файлов cookie отправляет для каждого пакета трафик в ту же серверную часть, что и для предыдущих запросов.</span><span class="sxs-lookup"><span data-stu-id="77cbf-137">If enabled, cookie-based session affinity sends traffic to the same backend as previous requests for each packet.</span></span>

```azurecli-interactive
az network application-gateway address-pool create \
--gateway-name AdatumAppGateway \
--name imagesBackendPool  \
--resource-group myresourcegroup \
--servers 10.0.0.6 10.0.0.7
```

### <a name="create-a-new-front-end-port"></a><span data-ttu-id="77cbf-138">Создание внешнего порта</span><span class="sxs-lookup"><span data-stu-id="77cbf-138">Create a new front-end port</span></span>

<span data-ttu-id="77cbf-139">Настройте внешний порт для шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="77cbf-139">Configure the front-end port for an application gateway.</span></span> <span data-ttu-id="77cbf-140">Объект конфигурации интерфейсного порта используется прослушивателем для определения порта, на котором шлюз приложений прослушивает трафик, поступающий в прослушиватель.</span><span class="sxs-lookup"><span data-stu-id="77cbf-140">The front-end port configuration object is used by a listener to define what port the Application Gateway listens for traffic on the listener.</span></span>

```azurecli-interactive
az network application-gateway frontend-port create --port 82 --gateway-name AdatumAppGateway --resource-group myresourcegroup --name port82
```

### <a name="create-a-new-listener"></a><span data-ttu-id="77cbf-141">Создание прослушивателя</span><span class="sxs-lookup"><span data-stu-id="77cbf-141">Create a new listener</span></span>

<span data-ttu-id="77cbf-142">Создайте прослушиватель.</span><span class="sxs-lookup"><span data-stu-id="77cbf-142">Configure the listener.</span></span> <span data-ttu-id="77cbf-143">Этот шаг позволяет настроить прослушиватель для общедоступного IP-адреса и порта, используемых для получения входящего сетевого трафика.</span><span class="sxs-lookup"><span data-stu-id="77cbf-143">This step configures the listener for the public IP address and port used to receive incoming network traffic.</span></span> <span data-ttu-id="77cbf-144">В следующем примере используются ранее настроенная внешняя IP-конфигурация, конфигурация интерфейсных портов и протокол (HTTP или HTTPS) и настраивается прослушиватель.</span><span class="sxs-lookup"><span data-stu-id="77cbf-144">The following example takes the previously configured front-end IP configuration,  front-end port configuration, and a protocol (http or https) and configures the listener.</span></span> <span data-ttu-id="77cbf-145">В этом примере прослушиватель прослушивает трафик HTTP через порт 82 для общедоступного IP-адреса, который был создан ранее.</span><span class="sxs-lookup"><span data-stu-id="77cbf-145">In this example, the listener listens to HTTP traffic on port 82 on the public IP address that was created earlier.</span></span>

```azurecli-interactive
az network application-gateway http-listener create --name imageListener --frontend-ip appGatewayFrontendIP  --frontend-port port82 --resource-group myresourcegroup --gateway-name AdatumAppGateway
```

### <a name="create-the-url-path-map"></a><span data-ttu-id="77cbf-146">Создание сопоставления URL-пути</span><span class="sxs-lookup"><span data-stu-id="77cbf-146">Create the Url path map</span></span>

<span data-ttu-id="77cbf-147">Настройте пути URL-правил для пулов тыловых серверов.</span><span class="sxs-lookup"><span data-stu-id="77cbf-147">Configure URL rule paths for the back-end pools.</span></span> <span data-ttu-id="77cbf-148">На этом этапе настраивается относительный путь, который шлюз приложений использует для сопоставления URL-пути с пулом тыловых серверов, который назначается для обработки входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="77cbf-148">This step configures the relative path used by application gateway to define the mapping between URL path and which back-end pool is assigned to handle the incoming traffic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="77cbf-149">Каждый путь должен начинаться с косой черты (/). Знак "\*" может находиться только в конце.</span><span class="sxs-lookup"><span data-stu-id="77cbf-149">Each path must start with / and the only place a "\*" is allowed, is at the end.</span></span> <span data-ttu-id="77cbf-150">Примеры допустимых значений: /xyz, /xyz* или /xyz/*.</span><span class="sxs-lookup"><span data-stu-id="77cbf-150">Valid examples are /xyz, /xyz* or /xyz/*.</span></span> <span data-ttu-id="77cbf-151">Строка, передаваемая для сопоставления пути, не должна содержать никакого текста после первого символа "?" или "#", и сами эти символы не допускаются.</span><span class="sxs-lookup"><span data-stu-id="77cbf-151">The string fed to the path matcher does not include any text after the first "?" or "#", and those characters are not allowed.</span></span> 

<span data-ttu-id="77cbf-152">В следующем примере создается одно правило для маршрутизации трафика от пути /images/* к пулу тыловых серверов imagesBackendPool.</span><span class="sxs-lookup"><span data-stu-id="77cbf-152">The following example creates one rule for "/images/*" path routing traffic to back-end "imagesBackendPool."</span></span> <span data-ttu-id="77cbf-153">Это правило гарантирует, что трафик для каждого набора URL-адресов направляется к серверной части.</span><span class="sxs-lookup"><span data-stu-id="77cbf-153">This rule ensures that traffic for each set of urls is routed to the backend.</span></span> <span data-ttu-id="77cbf-154">Например, файл http://adatum.com/images/figure1.jpg переходит в imagesBackendPool.</span><span class="sxs-lookup"><span data-stu-id="77cbf-154">For example, http://adatum.com/images/figure1.jpg goes to "imagesBackendPool."</span></span> <span data-ttu-id="77cbf-155">При настройке сопоставления для пути правил также настраивается пул серверной части по умолчанию, который будет использоваться, если путь не соответствует ни одному из предустановленных правил.</span><span class="sxs-lookup"><span data-stu-id="77cbf-155">If the path doesn't match any of the pre-defined path rules, the rule path map configuration also configures a default back-end address pool.</span></span> <span data-ttu-id="77cbf-156">Например, файл http://adatum.com/shoppingcart/test.html переходит в pool1, так как этот пул определен как пул по умолчанию для несоответствующего трафика.</span><span class="sxs-lookup"><span data-stu-id="77cbf-156">For example, http://adatum.com/shoppingcart/test.html goes to pool1 as it is defined as the default pool for unmatched traffic.</span></span>

```azurecli-interactive
az network application-gateway url-path-map create \
--gateway-name AdatumAppGateway \
--name imagespathmap \
--paths /images/* \
--resource-group myresourcegroup2 \
--address-pool imagesBackendPool \
--default-address-pool appGatewayBackendPool \
--default-http-settings appGatewayBackendHttpSettings \
--http-settings appGatewayBackendHttpSettings \
--rule-name images
```

## <a name="next-steps"></a><span data-ttu-id="77cbf-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="77cbf-157">Next steps</span></span>

<span data-ttu-id="77cbf-158">Информацию о разгрузке SSL см. в статье о [настройке шлюза приложений для разгрузки SSL](application-gateway-ssl-cli.md).</span><span class="sxs-lookup"><span data-stu-id="77cbf-158">If you want to learn about Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl-cli.md).</span></span>


[scenario]: ./media/application-gateway-create-url-route-cli/scenario.png
[1]: ./media/application-gateway-create-url-route-cli/figure1.png
[2]: ./media/application-gateway-create-url-route-cli/figure2.png
[3]: ./media/application-gateway-create-url-route-cli/figure3.png
