---
title: "aaaCreate шлюза приложения Azure - Azure CLI 1.0 | Документы Microsoft"
description: "Узнайте, как toocreate шлюза с помощью приложения hello Azure CLI 1.0 в диспетчере ресурсов"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 3c0d2d96b6be404d0372d00f0deb2a32959ca419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-cli"></a><span data-ttu-id="5dd2b-103">Создание шлюза приложения с помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5dd2b-103">Create an application gateway by using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5dd2b-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="5dd2b-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="5dd2b-105">PowerShell и диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="5dd2b-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="5dd2b-106">Классическая модель — Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5dd2b-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="5dd2b-107">Шаблон Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5dd2b-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="5dd2b-108">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="5dd2b-108">Azure CLI 1.0</span></span>](application-gateway-create-gateway-cli.md)
> * [<span data-ttu-id="5dd2b-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5dd2b-109">Azure CLI 2.0</span></span>](application-gateway-create-gateway-cli.md)
> 
> 

<span data-ttu-id="5dd2b-110">Шлюз приложений — это балансировщик нагрузки уровня 7.</span><span class="sxs-lookup"><span data-stu-id="5dd2b-110">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="5dd2b-111">Он обеспечивает отработку отказа, маршрутизации производительности HTTP-запросы между различными серверами, являются ли они на hello облачной или локальной.</span><span class="sxs-lookup"><span data-stu-id="5dd2b-111">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="5dd2b-112">Шлюз приложений имеет следующие возможности доставки приложения hello: HTTP загрузить пробы пользовательских работоспособности балансировки, сходство сеансов на основе файлов cookie и разгрузки Secure Sockets Layer (SSL) и поддержка нескольких сайтов.</span><span class="sxs-lookup"><span data-stu-id="5dd2b-112">Application gateway has hello following application delivery features: HTTP load balancing, cookie-based session affinity, and Secure Sockets Layer (SSL) offload, custom health probes, and support for multi-site.</span></span>

## <a name="prerequisite-install-hello-azure-cli"></a><span data-ttu-id="5dd2b-113">Необходимое условие: Установите hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5dd2b-113">Prerequisite: Install hello Azure CLI</span></span>

<span data-ttu-id="5dd2b-114">tooperform hello шаги в этой статье, вы должны слишком[Установка hello интерфейса командной строки Azure для Mac, Linux и Windows (Azure CLI)](../xplat-cli-install.md) и необходимо слишком[вход tooAzure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="5dd2b-114">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](../xplat-cli-install.md) and you need too[log on tooAzure](../xplat-cli-connect.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="5dd2b-115">Если у вас нет учетной записи Azure, то вам потребуется получить ее.</span><span class="sxs-lookup"><span data-stu-id="5dd2b-115">If you don't have an Azure account, you need one.</span></span> <span data-ttu-id="5dd2b-116">Зарегистрируйтесь, чтобы получить [бесплатную пробную версию](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="5dd2b-116">Go sign up for a [free trial here](../active-directory/sign-up-organization.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="5dd2b-117">Сценарий</span><span class="sxs-lookup"><span data-stu-id="5dd2b-117">Scenario</span></span>

<span data-ttu-id="5dd2b-118">В этом сценарии вы узнаете, как шлюз приложения с помощью toocreate hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="5dd2b-118">In this scenario, you learn how toocreate an application gateway using hello Azure portal.</span></span>

<span data-ttu-id="5dd2b-119">Вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="5dd2b-119">This scenario will:</span></span>

* <span data-ttu-id="5dd2b-120">как создать средний шлюз приложений с двумя экземплярами;</span><span class="sxs-lookup"><span data-stu-id="5dd2b-120">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="5dd2b-121">как создать виртуальную сеть ContosoVNET с зарезервированным блоком CIDR (10.0.0.0/16);</span><span class="sxs-lookup"><span data-stu-id="5dd2b-121">Create a virtual network named ContosoVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="5dd2b-122">как создать подсеть subnet01 с блоком CIDR (10.0.0.0/28).</span><span class="sxs-lookup"><span data-stu-id="5dd2b-122">Create a subnet called subnet01 that uses 10.0.0.0/28 as its CIDR block.</span></span>

> [!NOTE]
> <span data-ttu-id="5dd2b-123">Дополнительная настройка шлюза приложения hello, включая пользовательские работоспособности проверяет, пул адресов серверной части и дополнительные правила настраиваются после настройки шлюза приложения hello, а не во время первоначального развертывания.</span><span class="sxs-lookup"><span data-stu-id="5dd2b-123">Additional configuration of hello application gateway, including custom health probes, backend pool addresses, and additional rules are configured after hello application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5dd2b-124">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="5dd2b-124">Before you begin</span></span>

<span data-ttu-id="5dd2b-125">Шлюзу приложений Azure требуется собственная подсеть.</span><span class="sxs-lookup"><span data-stu-id="5dd2b-125">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="5dd2b-126">При создании виртуальной сети, убедитесь, оставьте достаточно toohave пространства адресов несколько подсетей.</span><span class="sxs-lookup"><span data-stu-id="5dd2b-126">When creating a virtual network, ensure that you leave enough address space toohave multiple subnets.</span></span> <span data-ttu-id="5dd2b-127">После развертывания приложения шлюза tooa подсети шлюзы только дополнительных приложений, могут toobe добавлены toohello подсети.</span><span class="sxs-lookup"><span data-stu-id="5dd2b-127">Once you deploy an application gateway tooa subnet, only additional application gateways are able toobe added toohello subnet.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="5dd2b-128">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="5dd2b-128">Log in tooAzure</span></span>

<span data-ttu-id="5dd2b-129">Откройте hello **командной строки пакета Microsoft Azure**и войдите в систему.</span><span class="sxs-lookup"><span data-stu-id="5dd2b-129">Open hello **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli-interactive
azure login
```

<span data-ttu-id="5dd2b-130">После ввода предшествующий пример hello предоставляется код.</span><span class="sxs-lookup"><span data-stu-id="5dd2b-130">Once you type hello preceding example, a code is provided.</span></span> <span data-ttu-id="5dd2b-131">Перейдите toohttps://aka.ms/devicelogin в процессе входа hello toocontinue браузера.</span><span class="sxs-lookup"><span data-stu-id="5dd2b-131">Navigate toohttps://aka.ms/devicelogin in a browser toocontinue hello login process.</span></span>

![Команда, выводящая имя пользователя устройства][1]

<span data-ttu-id="5dd2b-133">В браузере hello введите полученный код hello.</span><span class="sxs-lookup"><span data-stu-id="5dd2b-133">In hello browser, enter hello code you received.</span></span> <span data-ttu-id="5dd2b-134">Все перенаправленные tooa-на страницу входа.</span><span class="sxs-lookup"><span data-stu-id="5dd2b-134">You are redirected tooa sign-in page.</span></span>

![Код tooenter браузера][2]

<span data-ttu-id="5dd2b-136">После ввода кода hello вы войдете в toocontinue hello закрыть браузер на со сценарием hello.</span><span class="sxs-lookup"><span data-stu-id="5dd2b-136">Once hello code has been entered you are signed in, close hello browser toocontinue on with hello scenario.</span></span>

![Вход выполнен][3]

## <a name="switch-tooresource-manager-mode"></a><span data-ttu-id="5dd2b-138">Переключение режима диспетчера tooResource</span><span class="sxs-lookup"><span data-stu-id="5dd2b-138">Switch tooResource Manager Mode</span></span>

```azurecli-interactive
azure config mode arm
```

## <a name="create-hello-resource-group"></a><span data-ttu-id="5dd2b-139">Создать группу ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="5dd2b-139">Create hello resource group</span></span>

<span data-ttu-id="5dd2b-140">Перед созданием шлюза приложения hello, шлюз приложения hello toocontain создания группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5dd2b-140">Before creating hello application gateway, a resource group is created toocontain hello application gateway.</span></span> <span data-ttu-id="5dd2b-141">Hello ниже показана команда hello.</span><span class="sxs-lookup"><span data-stu-id="5dd2b-141">hello following shows hello command.</span></span>

```azurecli-interactive
azure group create \
--name ContosoRG \
--location eastus
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="5dd2b-142">Создать виртуальную сеть</span><span class="sxs-lookup"><span data-stu-id="5dd2b-142">Create a virtual network</span></span>

<span data-ttu-id="5dd2b-143">После создания группы ресурсов hello виртуальной сети создается для шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="5dd2b-143">Once hello resource group is created, a virtual network is created for hello application gateway.</span></span>  <span data-ttu-id="5dd2b-144">В следующем примере hello hello адресное пространство было как 10.0.0.0/16 как это определено в hello предшествующий сценарий заметки.</span><span class="sxs-lookup"><span data-stu-id="5dd2b-144">In hello following example, hello address space was as 10.0.0.0/16 as defined in hello preceding scenario notes.</span></span>

```azurecli-interactive
azure network vnet create \
--name ContosoVNET \
--address-prefixes 10.0.0.0/16 \
--resource-group ContosoRG \
--location eastus
```

## <a name="create-a-subnet"></a><span data-ttu-id="5dd2b-145">Создание подсети</span><span class="sxs-lookup"><span data-stu-id="5dd2b-145">Create a subnet</span></span>

<span data-ttu-id="5dd2b-146">После создания виртуальной сети hello подсети добавляется для шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="5dd2b-146">After hello virtual network is created, a subnet is added for hello application gateway.</span></span>  <span data-ttu-id="5dd2b-147">Если планируется toouse шлюз приложения с веб-приложения размещенного в hello же виртуальной сети как шлюз приложения hello, быть достаточно места для другой подсети, что tooleave.</span><span class="sxs-lookup"><span data-stu-id="5dd2b-147">If you plan toouse application gateway with a web app hosted in hello same virtual network as hello application gateway, be sure tooleave enough room for another subnet.</span></span>

```azurecli-interactive
azure network vnet subnet create \
--resource-group ContosoRG \
--name subnet01 \
--vnet-name ContosoVNET \
--address-prefix 10.0.0.0/28 
```

## <a name="create-hello-application-gateway"></a><span data-ttu-id="5dd2b-148">Создание шлюза приложения hello</span><span class="sxs-lookup"><span data-stu-id="5dd2b-148">Create hello application gateway</span></span>

<span data-ttu-id="5dd2b-149">После создания hello виртуальную сеть и подсеть hello необходимые компоненты для шлюза приложения hello являются полными.</span><span class="sxs-lookup"><span data-stu-id="5dd2b-149">Once hello virtual network and subnet are created, hello pre-requisites for hello application gateway are complete.</span></span> <span data-ttu-id="5dd2b-150">Кроме того, ранее экспортированный PFX-файл сертификата и hello пароль для сертификата hello требуются для hello, следующий шаг: hello IP-адреса, используемые для внутреннего hello — hello IP-адреса для сервера базы данных.</span><span class="sxs-lookup"><span data-stu-id="5dd2b-150">Additionally a previously exported .pfx certificate and hello password for hello certificate are required for hello following step: hello IP addresses used for hello backend are hello IP addresses for your backend server.</span></span> <span data-ttu-id="5dd2b-151">Эти значения могут быть либо частных IP-адресов в виртуальной сети hello, общедоступные IP-адреса или полные доменные имена для внутренних серверов.</span><span class="sxs-lookup"><span data-stu-id="5dd2b-151">These values can be either private IPs in hello virtual network, public ips, or fully qualified domain names for your backend servers.</span></span>

```azurecli-interactive
azure network application-gateway create \
--name AdatumAppGateway \
--location eastus \
--resource-group ContosoRG \
--vnet-name ContosoVNET \
--subnet-name subnet01 \
--servers 134.170.185.46,134.170.188.221,134.170.185.50 \
--capacity 2 \
--sku-tier Standard \
--routing-rule-type Basic \
--frontend-port 80 \
--http-settings-cookie-based-affinity Enabled \
--http-settings-port 80 \
--http-settings-protocol http \
--frontend-port http \
--sku-name Standard_Medium
```

> [!NOTE]
> <span data-ttu-id="5dd2b-152">Список параметров, которые могут быть предоставлены во время создания, запуска hello следующую команду: **создать шлюз приложений сеть azure — помочь**.</span><span class="sxs-lookup"><span data-stu-id="5dd2b-152">For a list of parameters that can be provided during creation run hello following command: **azure network application-gateway create --help**.</span></span>

<span data-ttu-id="5dd2b-153">Этот пример создает шлюз простое приложение с параметрами по умолчанию для прослушивателя hello, внутреннего пула, параметров серверного http и правил.</span><span class="sxs-lookup"><span data-stu-id="5dd2b-153">This example creates a basic application gateway with default settings for hello listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="5dd2b-154">Вы можете изменить эти параметры toosuit развертывания после успешной подготовки hello.</span><span class="sxs-lookup"><span data-stu-id="5dd2b-154">You can modify these settings toosuit your deployment once hello provisioning is successful.</span></span>
<span data-ttu-id="5dd2b-155">Балансировка нагрузки начинается при наличии веб-приложения с внутреннего пула hello в предыдущих шагах, после ее создания, hello.</span><span class="sxs-lookup"><span data-stu-id="5dd2b-155">If you already have your web application defined with hello backend pool in hello preceding steps, once created, load balancing begins.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5dd2b-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5dd2b-156">Next steps</span></span>

<span data-ttu-id="5dd2b-157">Узнайте, как пользовательские работоспособности toocreate проверяет, посетив [пробу пользовательского состояния](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="5dd2b-157">Learn how toocreate custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="5dd2b-158">Узнайте, как tooconfigure разгрузки SSL и дешифрования SSL дорогостоящих take hello off веб-серверов, посетив [Настройка разгрузки SSL](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="5dd2b-158">Learn how tooconfigure SSL Offloading and take hello costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli-nodejs/scenario.png
[1]: ./media/application-gateway-create-gateway-cli-nodejs/figure1.png
[2]: ./media/application-gateway-create-gateway-cli-nodejs/figure2.png
[3]: ./media/application-gateway-create-gateway-cli-nodejs/figure3.png
