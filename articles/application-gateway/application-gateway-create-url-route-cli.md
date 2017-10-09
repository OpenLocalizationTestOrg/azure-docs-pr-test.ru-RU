---
title: "правила с помощью маршрутизации URL-адрес шлюза приложения - aaaCreate Azure CLI 2.0 | Документы Microsoft"
description: "На этой странице представлены инструкции toocreate, настройте шлюз приложения Azure с помощью правила маршрутизации URL-адрес"
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
ms.openlocfilehash: 335b52be258945e1172eb0252b732e0e6ecb2ef0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-using-path-based-routing-with-azure-cli-20"></a><span data-ttu-id="2b1f0-103">Создание шлюза приложений с помощью маршрутизации на основе пути с использованием Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2b1f0-103">Create an application gateway using Path-based routing with Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2b1f0-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="2b1f0-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="2b1f0-105">PowerShell и диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="2b1f0-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="2b1f0-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2b1f0-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="2b1f0-107">Маршрутизация URL-адрес на основе пути позволяет вам tooassociate маршрутов на основе hello пути URL-адреса HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="2b1f0-107">URL Path-based routing enables you tooassociate routes based on hello URL path of an Http request.</span></span> <span data-ttu-id="2b1f0-108">Он проверяет при внутреннем пул tooa маршрута, настроенный для hello URL-адрес, представленных в hello шлюза приложений и отправляет hello сетевой трафик toohello определенного пула серверной части.</span><span class="sxs-lookup"><span data-stu-id="2b1f0-108">It checks if there is a route tooa back-end pool configured for hello URL presented in hello Application Gateway and sends hello network traffic toohello defined back-end pool.</span></span> <span data-ttu-id="2b1f0-109">Обычно используются для маршрутизации на основе URL-адрес — tooload балансировать нагрузку по запросам для различных типов содержимого toodifferent серверных пулов.</span><span class="sxs-lookup"><span data-stu-id="2b1f0-109">A common use for URL-based routing is tooload balance requests for different content types toodifferent back-end server pools.</span></span>

<span data-ttu-id="2b1f0-110">Маршрутизация на основе URL-адрес появился новый шлюз tooapplication тип правила.</span><span class="sxs-lookup"><span data-stu-id="2b1f0-110">URL-based routing introduces a new rule type tooapplication gateway.</span></span> <span data-ttu-id="2b1f0-111">Шлюз приложений имеет два типа правил: базовые правила и правила на основе пути.</span><span class="sxs-lookup"><span data-stu-id="2b1f0-111">Application gateway has two rule types: basic and PathBasedRouting.</span></span> <span data-ttu-id="2b1f0-112">Основное правило тип предоставляет циклического службы для внутреннего интерфейса hello пулов при PathBasedRouting Кроме распространения tooround циклический перебор, также учитывает шаблон пути URL-адреса запроса hello при выборе пула hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="2b1f0-112">Basic rule type provides round-robin service for hello back-end pools while PathBasedRouting in addition tooround robin distribution, also takes path pattern of hello request URL into account while choosing hello back-end pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="2b1f0-113">Сценарий</span><span class="sxs-lookup"><span data-stu-id="2b1f0-113">Scenario</span></span>

<span data-ttu-id="2b1f0-114">В следующем примере hello, шлюз приложений обслуживает трафика для contoso.com с помощью двух серверных пулов: пул сервера по умолчанию и пул образ сервера.</span><span class="sxs-lookup"><span data-stu-id="2b1f0-114">In hello following example, Application Gateway is serving traffic for contoso.com with two back-end server pools: a default server pool and an image server pool.</span></span>

<span data-ttu-id="2b1f0-115">Запросы для http://contoso.com/image * направлено пул серверов tooimage (imagesBackendPool), если hello не соответствует шаблон пути, выбранного пула сервера по умолчанию (appGatewayBackendPool).</span><span class="sxs-lookup"><span data-stu-id="2b1f0-115">Requests for http://contoso.com/image* are routed tooimage server pool (imagesBackendPool), if hello path pattern does not match, a default server pool (appGatewayBackendPool) is selected.</span></span>

![Маршрут URL-адреса](./media/application-gateway-create-url-route-cli/scenario.png)

## <a name="log-in-tooazure"></a><span data-ttu-id="2b1f0-117">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="2b1f0-117">Log in tooAzure</span></span>

<span data-ttu-id="2b1f0-118">Откройте hello **командной строки пакета Microsoft Azure**и войдите в систему.</span><span class="sxs-lookup"><span data-stu-id="2b1f0-118">Open hello **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli
az login -u "username"
```

> [!NOTE]
> <span data-ttu-id="2b1f0-119">Можно также использовать `az login` без ключа hello для входа устройство, которое требуется ввод кода на aka.ms/devicelogin.</span><span class="sxs-lookup"><span data-stu-id="2b1f0-119">You can also use `az login` without hello switch for device login that requires entering a code at aka.ms/devicelogin.</span></span>

<span data-ttu-id="2b1f0-120">После ввода предшествующий пример hello предоставляется код.</span><span class="sxs-lookup"><span data-stu-id="2b1f0-120">Once you type hello preceding example, a code is provided.</span></span> <span data-ttu-id="2b1f0-121">Перейдите toohttps://aka.ms/devicelogin в процессе входа hello toocontinue браузера.</span><span class="sxs-lookup"><span data-stu-id="2b1f0-121">Navigate toohttps://aka.ms/devicelogin in a browser toocontinue hello login process.</span></span>

![Команда, выводящая имя пользователя устройства][1]

<span data-ttu-id="2b1f0-123">В браузере hello введите полученный код hello.</span><span class="sxs-lookup"><span data-stu-id="2b1f0-123">In hello browser, enter hello code you received.</span></span> <span data-ttu-id="2b1f0-124">Все перенаправленные tooa-на страницу входа.</span><span class="sxs-lookup"><span data-stu-id="2b1f0-124">You are redirected tooa sign-in page.</span></span>

![Код tooenter браузера][2]

<span data-ttu-id="2b1f0-126">После ввода кода hello вы войдете в toocontinue hello закрыть браузер на со сценарием hello.</span><span class="sxs-lookup"><span data-stu-id="2b1f0-126">Once hello code has been entered you are signed in, close hello browser toocontinue on with hello scenario.</span></span>

![Вход выполнен][3]

## <a name="add-a-path-based-rule-tooan-existing-application-gateway"></a><span data-ttu-id="2b1f0-128">Добавление правила на основе пути tooan существующие приложения шлюза</span><span class="sxs-lookup"><span data-stu-id="2b1f0-128">Add a path-based rule tooan existing application gateway</span></span>

<span data-ttu-id="2b1f0-129">Создание шлюза приложений с определенным правилом на основе пути</span><span class="sxs-lookup"><span data-stu-id="2b1f0-129">Create an application gateway with a path rule defined</span></span>

### <a name="create-a-new-back-end-pool"></a><span data-ttu-id="2b1f0-130">Создание внутреннего пула</span><span class="sxs-lookup"><span data-stu-id="2b1f0-130">Create a new back-end pool</span></span>

<span data-ttu-id="2b1f0-131">Настройка параметров шлюза приложения **imagesBackendPool** hello балансировки нагрузки сетевого трафика в пуле hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="2b1f0-131">Configure application gateway setting **imagesBackendPool** for hello load-balanced network traffic in hello back-end pool.</span></span> <span data-ttu-id="2b1f0-132">В этом примере вы настройки другой пул серверной части для нового пула внутренней hello.</span><span class="sxs-lookup"><span data-stu-id="2b1f0-132">In this example, you configure different back-end pool settings for hello new back-end pool.</span></span> <span data-ttu-id="2b1f0-133">Для каждого пула тыловых серверов параметры можно настроить отдельно.</span><span class="sxs-lookup"><span data-stu-id="2b1f0-133">Each back-end pool can have its own back-end pool setting.</span></span>  <span data-ttu-id="2b1f0-134">Параметры HTTP серверной используются членами правила tooroute трафика toohello правильный внутренний пул.</span><span class="sxs-lookup"><span data-stu-id="2b1f0-134">Backend HTTP settings are used by rules tooroute traffic toohello correct backend pool members.</span></span> <span data-ttu-id="2b1f0-135">Определяет hello протокол и порт, используемый при отправке трафика члены пула toohello серверной части.</span><span class="sxs-lookup"><span data-stu-id="2b1f0-135">This determines hello protocol and port that is used when sending traffic toohello backend pool members.</span></span> <span data-ttu-id="2b1f0-136">Сеансы на основе файлов cookie, также определяются hello параметров серверного HTTP.</span><span class="sxs-lookup"><span data-stu-id="2b1f0-136">Cookie-based sessions are also determined by hello backend HTTP settings.</span></span>  <span data-ttu-id="2b1f0-137">Если параметр включен, сходство сеансов на основе файлов cookie отправляет трафик toohello один внутренний как предыдущие запросы для каждого пакета.</span><span class="sxs-lookup"><span data-stu-id="2b1f0-137">If enabled, cookie-based session affinity sends traffic toohello same backend as previous requests for each packet.</span></span>

```azurecli-interactive
az network application-gateway address-pool create \
--gateway-name AdatumAppGateway \
--name imagesBackendPool  \
--resource-group myresourcegroup \
--servers 10.0.0.6 10.0.0.7
```

### <a name="create-a-new-front-end-port"></a><span data-ttu-id="2b1f0-138">Создание внешнего порта</span><span class="sxs-lookup"><span data-stu-id="2b1f0-138">Create a new front-end port</span></span>

<span data-ttu-id="2b1f0-139">Настройте hello интерфейсный порт для шлюза приложения.</span><span class="sxs-lookup"><span data-stu-id="2b1f0-139">Configure hello front-end port for an application gateway.</span></span> <span data-ttu-id="2b1f0-140">Объект конфигурации Hello интерфейсный порт используется toodefine прослушивателя что порт прослушивает трафик через прослушиватель hello шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="2b1f0-140">hello front-end port configuration object is used by a listener toodefine what port hello Application Gateway listens for traffic on hello listener.</span></span>

```azurecli-interactive
az network application-gateway frontend-port create --port 82 --gateway-name AdatumAppGateway --resource-group myresourcegroup --name port82
```

### <a name="create-a-new-listener"></a><span data-ttu-id="2b1f0-141">Создание прослушивателя</span><span class="sxs-lookup"><span data-stu-id="2b1f0-141">Create a new listener</span></span>

<span data-ttu-id="2b1f0-142">Настройте прослушиватель hello.</span><span class="sxs-lookup"><span data-stu-id="2b1f0-142">Configure hello listener.</span></span> <span data-ttu-id="2b1f0-143">Этот шаг позволяет настроить прослушиватель hello hello общедоступный IP-адрес и порт, используемый tooreceive входящего сетевого трафика.</span><span class="sxs-lookup"><span data-stu-id="2b1f0-143">This step configures hello listener for hello public IP address and port used tooreceive incoming network traffic.</span></span> <span data-ttu-id="2b1f0-144">Следующий пример Hello принимает hello ранее настроен интерфейсный IP-конфигурации, конфигурацию интерфейсный порт и протокол (http или https) и настраивает hello прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="2b1f0-144">hello following example takes hello previously configured front-end IP configuration,  front-end port configuration, and a protocol (http or https) and configures hello listener.</span></span> <span data-ttu-id="2b1f0-145">В этом примере hello прослушиватель прослушивает трафик tooHTTP порт 82 hello общедоступный IP-адрес, который был создан ранее.</span><span class="sxs-lookup"><span data-stu-id="2b1f0-145">In this example, hello listener listens tooHTTP traffic on port 82 on hello public IP address that was created earlier.</span></span>

```azurecli-interactive
az network application-gateway http-listener create --name imageListener --frontend-ip appGatewayFrontendIP  --frontend-port port82 --resource-group myresourcegroup --gateway-name AdatumAppGateway
```

### <a name="create-hello-url-path-map"></a><span data-ttu-id="2b1f0-146">Создать сопоставление пути hello URL-адресов</span><span class="sxs-lookup"><span data-stu-id="2b1f0-146">Create hello Url path map</span></span>

<span data-ttu-id="2b1f0-147">Настройте правило пути URL-адресов для пулов hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="2b1f0-147">Configure URL rule paths for hello back-end pools.</span></span> <span data-ttu-id="2b1f0-148">Этот шаг позволяет настроить hello относительный путь, используемый службой приложения шлюза toodefine hello сопоставления URL-адрес и какой пул внутренней назначается toohandle hello входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="2b1f0-148">This step configures hello relative path used by application gateway toodefine hello mapping between URL path and which back-end pool is assigned toohandle hello incoming traffic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2b1f0-149">Каждый путь должен начинаться с / и hello единственное место «\*» допускается, находится в конце hello.</span><span class="sxs-lookup"><span data-stu-id="2b1f0-149">Each path must start with / and hello only place a "\*" is allowed, is at hello end.</span></span> <span data-ttu-id="2b1f0-150">Примеры допустимых значений: /xyz, /xyz* или /xyz/*.</span><span class="sxs-lookup"><span data-stu-id="2b1f0-150">Valid examples are /xyz, /xyz* or /xyz/*.</span></span> <span data-ttu-id="2b1f0-151">Hello строка переданы сопоставителе toohello путь не содержит текст после hello сначала «?» или «#» и эти знаки не допускаются.</span><span class="sxs-lookup"><span data-stu-id="2b1f0-151">hello string fed toohello path matcher does not include any text after hello first "?" or "#", and those characters are not allowed.</span></span> 

<span data-ttu-id="2b1f0-152">Hello следующий пример создает одно правило для «/ images / *» путь маршрутизации трафика tooback-end «imagesBackendPool».</span><span class="sxs-lookup"><span data-stu-id="2b1f0-152">hello following example creates one rule for "/images/*" path routing traffic tooback-end "imagesBackendPool."</span></span> <span data-ttu-id="2b1f0-153">Это правило обеспечивает трафика для каждого набора URL-адресов серверной части перенаправленного toohello.</span><span class="sxs-lookup"><span data-stu-id="2b1f0-153">This rule ensures that traffic for each set of urls is routed toohello backend.</span></span> <span data-ttu-id="2b1f0-154">Например, http://adatum.com/images/figure1.jpg становится слишком «imagesBackendPool».</span><span class="sxs-lookup"><span data-stu-id="2b1f0-154">For example, http://adatum.com/images/figure1.jpg goes too"imagesBackendPool."</span></span> <span data-ttu-id="2b1f0-155">Если путь hello не соответствует ни одному из правил предопределенный путь hello, hello правило пути карты конфигурация также настраивает пул адресов серверной части по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2b1f0-155">If hello path doesn't match any of hello pre-defined path rules, hello rule path map configuration also configures a default back-end address pool.</span></span> <span data-ttu-id="2b1f0-156">Например http://adatum.com/shoppingcart/test.html переходит toopool1 как она определена в качестве пула по умолчанию hello для несопоставленных трафика.</span><span class="sxs-lookup"><span data-stu-id="2b1f0-156">For example, http://adatum.com/shoppingcart/test.html goes toopool1 as it is defined as hello default pool for unmatched traffic.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2b1f0-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2b1f0-157">Next steps</span></span>

<span data-ttu-id="2b1f0-158">Если toolearn о разгрузки Secure Sockets Layer (SSL), см. [настройки шлюза приложения для разгрузки SSL](application-gateway-ssl-cli.md).</span><span class="sxs-lookup"><span data-stu-id="2b1f0-158">If you want toolearn about Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl-cli.md).</span></span>


[scenario]: ./media/application-gateway-create-url-route-cli/scenario.png
[1]: ./media/application-gateway-create-url-route-cli/figure1.png
[2]: ./media/application-gateway-create-url-route-cli/figure2.png
[3]: ./media/application-gateway-create-url-route-cli/figure3.png
