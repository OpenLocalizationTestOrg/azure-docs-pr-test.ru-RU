---
title: "aaaCreate шлюза приложения Azure - CLI Azure 2.0 | Документы Microsoft"
description: "Узнайте, как toocreate шлюза с помощью приложения hello Azure CLI 2.0 в диспетчере ресурсов"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 952065586cd87d253882438bb779b768d9fd59fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-cli-20"></a><span data-ttu-id="ef955-103">Создание шлюза приложения с помощью Azure CLI 2.0 hello</span><span class="sxs-lookup"><span data-stu-id="ef955-103">Create an application gateway by using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ef955-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="ef955-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="ef955-105">PowerShell и диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="ef955-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="ef955-106">Классическая модель — Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef955-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="ef955-107">Шаблон Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ef955-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="ef955-108">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="ef955-108">Azure CLI 1.0</span></span>](application-gateway-create-gateway-cli.md)
> * [<span data-ttu-id="ef955-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ef955-109">Azure CLI 2.0</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="ef955-110">Шлюз приложений — это выделенный виртуальный модуль, предоставляющий контроллер доставки приложений (ADC) как услугу, который обеспечивает для приложения множество функций балансировки нагрузки уровня 7.</span><span class="sxs-lookup"><span data-stu-id="ef955-110">Application Gateway is a dedicated virtual appliance that provides application delivery controller (ADC) as a service, offering various layer 7 load balancing capabilities for your application.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="ef955-111">Задача hello toocomplete версии CLI</span><span class="sxs-lookup"><span data-stu-id="ef955-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="ef955-112">Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.</span><span class="sxs-lookup"><span data-stu-id="ef955-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="ef955-113">[Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) -нашей CLI для hello классический и ресурса управления развертывания моделей.</span><span class="sxs-lookup"><span data-stu-id="ef955-113">[Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="ef955-114">[Azure CLI 2.0](application-gateway-create-gateway-cli.md) -нашей нового поколения CLI для модели развертывания hello ресурсов управления</span><span class="sxs-lookup"><span data-stu-id="ef955-114">[Azure CLI 2.0](application-gateway-create-gateway-cli.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="prerequisite-install-hello-azure-cli-20"></a><span data-ttu-id="ef955-115">Необходимое условие: Установите hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ef955-115">Prerequisite: Install hello Azure CLI 2.0</span></span>

<span data-ttu-id="ef955-116">tooperform hello шаги в этой статье, вы должны слишком[Установка hello интерфейса командной строки Azure для Mac, Linux и Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="ef955-116">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

> [!NOTE]
> <span data-ttu-id="ef955-117">Если у вас нет учетной записи Azure, то вам потребуется получить ее.</span><span class="sxs-lookup"><span data-stu-id="ef955-117">If you don't have an Azure account, you need one.</span></span> <span data-ttu-id="ef955-118">Зарегистрируйтесь, чтобы получить [бесплатную пробную версию](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="ef955-118">Go sign up for a [free trial here](../active-directory/sign-up-organization.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="ef955-119">Сценарий</span><span class="sxs-lookup"><span data-stu-id="ef955-119">Scenario</span></span>

<span data-ttu-id="ef955-120">В этом сценарии вы узнаете, как шлюз приложения с помощью toocreate hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ef955-120">In this scenario, you learn how toocreate an application gateway using hello Azure portal.</span></span>

<span data-ttu-id="ef955-121">Вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="ef955-121">This scenario will:</span></span>

* <span data-ttu-id="ef955-122">как создать средний шлюз приложений с двумя экземплярами;</span><span class="sxs-lookup"><span data-stu-id="ef955-122">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="ef955-123">как создать виртуальную сеть AdatumAppGatewayVNET с зарезервированным блоком CIDR (10.0.0.0/16);</span><span class="sxs-lookup"><span data-stu-id="ef955-123">Create a virtual network named AdatumAppGatewayVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="ef955-124">как создать подсеть с именем Appgatewaysubnet и блоком CIDR (10.0.0.0/28);</span><span class="sxs-lookup"><span data-stu-id="ef955-124">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>

> [!NOTE]
> <span data-ttu-id="ef955-125">Дополнительная настройка шлюза приложения hello, включая пользовательские работоспособности проверяет, пул адресов серверной части и дополнительные правила настраиваются после настройки шлюза приложения hello, а не во время первоначального развертывания.</span><span class="sxs-lookup"><span data-stu-id="ef955-125">Additional configuration of hello application gateway, including custom health probes, backend pool addresses, and additional rules are configured after hello application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ef955-126">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="ef955-126">Before you begin</span></span>

<span data-ttu-id="ef955-127">Шлюзу приложений Azure требуется собственная подсеть.</span><span class="sxs-lookup"><span data-stu-id="ef955-127">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="ef955-128">При создании виртуальной сети, убедитесь, оставьте достаточно toohave пространства адресов несколько подсетей.</span><span class="sxs-lookup"><span data-stu-id="ef955-128">When creating a virtual network, ensure that you leave enough address space toohave multiple subnets.</span></span> <span data-ttu-id="ef955-129">После развертывания приложения шлюза tooa подсети шлюзы только дополнительное приложение можно добавить toohello подсети.</span><span class="sxs-lookup"><span data-stu-id="ef955-129">Once you deploy an application gateway tooa subnet, only additional application gateways can be added toohello subnet.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="ef955-130">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="ef955-130">Log in tooAzure</span></span>

<span data-ttu-id="ef955-131">Откройте hello **командной строки пакета Microsoft Azure**и войдите в систему.</span><span class="sxs-lookup"><span data-stu-id="ef955-131">Open hello **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli-interactive
az login -u "username"
```

> [!NOTE]
> <span data-ttu-id="ef955-132">Можно также использовать `az login` без ключа hello для входа устройство, которое требуется ввод кода на aka.ms/devicelogin.</span><span class="sxs-lookup"><span data-stu-id="ef955-132">You can also use `az login` without hello switch for device login that requires entering a code at aka.ms/devicelogin.</span></span>

<span data-ttu-id="ef955-133">После ввода предшествующий пример hello предоставляется код.</span><span class="sxs-lookup"><span data-stu-id="ef955-133">Once you type hello preceding example, a code is provided.</span></span> <span data-ttu-id="ef955-134">Перейдите toohttps://aka.ms/devicelogin в процессе входа hello toocontinue браузера.</span><span class="sxs-lookup"><span data-stu-id="ef955-134">Navigate toohttps://aka.ms/devicelogin in a browser toocontinue hello login process.</span></span>

![Команда, выводящая имя пользователя устройства][1]

<span data-ttu-id="ef955-136">В браузере hello введите полученный код hello.</span><span class="sxs-lookup"><span data-stu-id="ef955-136">In hello browser, enter hello code you received.</span></span> <span data-ttu-id="ef955-137">Все перенаправленные tooa-на страницу входа.</span><span class="sxs-lookup"><span data-stu-id="ef955-137">You are redirected tooa sign-in page.</span></span>

![Код tooenter браузера][2]

<span data-ttu-id="ef955-139">После ввода кода hello вы войдете в toocontinue hello закрыть браузер на со сценарием hello.</span><span class="sxs-lookup"><span data-stu-id="ef955-139">Once hello code has been entered you are signed in, close hello browser toocontinue on with hello scenario.</span></span>

![Вход выполнен][3]

## <a name="create-hello-resource-group"></a><span data-ttu-id="ef955-141">Создать группу ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="ef955-141">Create hello resource group</span></span>

<span data-ttu-id="ef955-142">Перед созданием шлюза приложения hello, шлюз приложения hello toocontain создания группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ef955-142">Before creating hello application gateway, a resource group is created toocontain hello application gateway.</span></span> <span data-ttu-id="ef955-143">Hello ниже показана команда hello.</span><span class="sxs-lookup"><span data-stu-id="ef955-143">hello following shows hello command.</span></span>

```azurecli-interactive
az group create --name myresourcegroup --location "eastus"
```

## <a name="create-hello-application-gateway"></a><span data-ttu-id="ef955-144">Создание шлюза приложения hello</span><span class="sxs-lookup"><span data-stu-id="ef955-144">Create hello application gateway</span></span>

<span data-ttu-id="ef955-145">IP-адреса Hello для внутренних hello — hello IP-адреса для сервера базы данных.</span><span class="sxs-lookup"><span data-stu-id="ef955-145">hello IP addresses used for hello backend are hello IP addresses for your backend server.</span></span> <span data-ttu-id="ef955-146">Эти значения могут быть либо частных IP-адресов в виртуальной сети hello, общедоступные IP-адреса или полные доменные имена для внутренних серверов.</span><span class="sxs-lookup"><span data-stu-id="ef955-146">These values can be either private IPs in hello virtual network, public ips, or fully qualified domain names for your backend servers.</span></span> <span data-ttu-id="ef955-147">Hello пример создает шлюза приложения с дополнительными параметрами конфигурации для настройки http, порты и правил.</span><span class="sxs-lookup"><span data-stu-id="ef955-147">hello following example creates an application gateway with additional configuration settings for http settings, ports, and rules.</span></span>

```azurecli-interactive
az network application-gateway create \
--name "AdatumAppGateway" \
--location "eastus" \
--resource-group "myresourcegroup" \
--vnet-name "AdatumAppGatewayVNET" \
--vnet-address-prefix "10.0.0.0/16" \
--subnet "Appgatewaysubnet" \
--subnet-address-prefix "10.0.0.0/28" \
--servers 10.0.0.4 10.0.0.5 \
--capacity 2 \
--sku Standard_Small \
--http-settings-cookie-based-affinity Enabled \
--http-settings-protocol Http \
--frontend-port 80 \
--routing-rule-type Basic \
--http-settings-port 80 \
--public-ip-address "pip2" \
--public-ip-address-allocation "dynamic" \

```

<span data-ttu-id="ef955-148">Hello выше примере многие свойства, которые не требуются во время создания шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ef955-148">hello preceding example shows many properties that are not required during hello creation of an application gateway.</span></span> <span data-ttu-id="ef955-149">Следующий пример кода Hello создает шлюза приложения hello необходимые сведения.</span><span class="sxs-lookup"><span data-stu-id="ef955-149">hello following code example creates an application gateway with hello required information.</span></span>

```azurecli-interactive
az network application-gateway create \
--name "AdatumAppGateway" \
--location "eastus" \
--resource-group "myresourcegroup" \
--vnet-name "AdatumAppGatewayVNET" \
--vnet-address-prefix "10.0.0.0/16" \
--subnet "Appgatewaysubnet \
--subnet-address-prefix "10.0.0.0/28" \
--servers "10.0.0.5"  \
--public-ip-address pip
```
 
> [!NOTE]
> <span data-ttu-id="ef955-150">Список параметров, которые могут быть предоставлены во время создания запуска hello следующую команду: `az network application-gateway create --help`.</span><span class="sxs-lookup"><span data-stu-id="ef955-150">For a list of parameters that can be provided during creation run hello following command: `az network application-gateway create --help`.</span></span>

<span data-ttu-id="ef955-151">Этот пример создает шлюз простое приложение с параметрами по умолчанию для прослушивателя hello, внутреннего пула, параметров серверного http и правил.</span><span class="sxs-lookup"><span data-stu-id="ef955-151">This example creates a basic application gateway with default settings for hello listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="ef955-152">Вы можете изменить эти параметры toosuit развертывания после успешной подготовки hello.</span><span class="sxs-lookup"><span data-stu-id="ef955-152">You can modify these settings toosuit your deployment once hello provisioning is successful.</span></span>
<span data-ttu-id="ef955-153">Балансировка нагрузки начинается при наличии веб-приложения с внутреннего пула hello в предыдущих шагах, после ее создания, hello.</span><span class="sxs-lookup"><span data-stu-id="ef955-153">If you already have your web application defined with hello backend pool in hello preceding steps, once created, load balancing begins.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="ef955-154">Получение DNS-имени шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="ef955-154">Get application gateway DNS name</span></span>

<span data-ttu-id="ef955-155">После создания шлюза hello hello следующим шагом является tooconfigure hello внешнего интерфейса для обмена данными.</span><span class="sxs-lookup"><span data-stu-id="ef955-155">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="ef955-156">Если вы используете общедоступный IP-адрес, шлюзу приложений требуется динамически назначаемое непонятное имя DNS.</span><span class="sxs-lookup"><span data-stu-id="ef955-156">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="ef955-157">tooensure конечным пользователям возможность нажать шлюза приложения hello, запись CNAME может быть используется toopoint toohello общедоступную конечную точку шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ef955-157">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="ef955-158">[Настройка пользовательского имени домена в Azure](../dns/dns-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="ef955-158">[Configuring a custom domain name for in Azure](../dns/dns-custom-domain.md).</span></span> <span data-ttu-id="ef955-159">tooconfigure псевдоним, получить сведения о шлюза приложения hello и соответствующее IP или DNS-имя с помощью шлюза hello PublicIPAddress элемент toohello подключенных приложений.</span><span class="sxs-lookup"><span data-stu-id="ef955-159">tooconfigure an alias, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="ef955-160">шлюз приложения Hello DNS-имя должно быть используется toocreate запись CNAME, какие точки hello двух web приложений toothis DNS-имя.</span><span class="sxs-lookup"><span data-stu-id="ef955-160">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="ef955-161">Использование Hello записи A не рекомендуется, поскольку hello виртуального IP-адреса могут изменяться при перезагрузке шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="ef955-161">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>


```azurecli-interactive
az network public-ip show --name "pip" --resource-group "AdatumAppGatewayRG"
```

```
{
  "dnsSettings": {
    "domainNameLabel": null,
    "fqdn": "8c786058-96d4-4f3e-bb41-660860ceae4c.cloudapp.net",
    "reverseFqdn": null
  },
  "etag": "W/\"3b0ac031-01f0-4860-b572-e3c25e0c57ad\"",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/publicIPAddresses/pip2",
  "idleTimeoutInMinutes": 4,
  "ipAddress": "40.121.167.250",
  "ipConfiguration": {
    "etag": null,
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/applicationGateways/AdatumAppGateway2/frontendIPConfigurations/appGatewayFrontendIP",
    "name": null,
    "privateIpAddress": null,
    "privateIpAllocationMethod": null,
    "provisioningState": null,
    "publicIpAddress": null,
    "resourceGroup": "AdatumAppGatewayRG",
    "subnet": null
  },
  "location": "eastus",
  "name": "pip2",
  "provisioningState": "Succeeded",
  "publicIpAddressVersion": "IPv4",
  "publicIpAllocationMethod": "Dynamic",
  "resourceGroup": "AdatumAppGatewayRG",
  "resourceGuid": "3c30d310-c543-4e9d-9c72-bbacd7fe9b05",
  "tags": {
    "cli[2] owner[administrator]": ""
  },
  "type": "Microsoft.Network/publicIPAddresses"
}
```

## <a name="delete-all-resources"></a><span data-ttu-id="ef955-162">Удаление всех ресурсов</span><span class="sxs-lookup"><span data-stu-id="ef955-162">Delete all resources</span></span>

<span data-ttu-id="ef955-163">toodelete все ресурсы, которые созданы в этой статье завершения hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="ef955-163">toodelete all resources created in this article, complete hello following steps:</span></span>

```azurecli-interactive
az group delete --name AdatumAppGatewayRG
```
 
## <a name="next-steps"></a><span data-ttu-id="ef955-164">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ef955-164">Next steps</span></span>

<span data-ttu-id="ef955-165">Узнайте, как пользовательские работоспособности toocreate проверяет, посетив [пробу пользовательского состояния](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="ef955-165">Learn how toocreate custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="ef955-166">Узнайте, как tooconfigure разгрузки SSL и дешифрования SSL дорогостоящих take hello off веб-серверов, посетив [Настройка разгрузки SSL](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="ef955-166">Learn how tooconfigure SSL Offloading and take hello costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli/scenario.png
[1]: ./media/application-gateway-create-gateway-cli/figure1.png
[2]: ./media/application-gateway-create-gateway-cli/figure2.png
[3]: ./media/application-gateway-create-gateway-cli/figure3.png
