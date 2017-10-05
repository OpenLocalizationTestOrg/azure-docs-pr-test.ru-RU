---
title: "Создание шлюза приложений Azure с помощью Azure CLI 2.0 | Документация Майкрософт"
description: "Узнайте, как создать шлюз приложений с помощью Azure CLI 2.0 в Resource Manager"
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
ms.openlocfilehash: 052410db8c7619c7990dc319951a55663f2c2ba1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-gateway-by-using-the-azure-cli-20"></a><span data-ttu-id="57ed5-103">Создание шлюза приложений с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="57ed5-103">Create an application gateway by using the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="57ed5-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="57ed5-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="57ed5-105">PowerShell и диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="57ed5-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="57ed5-106">Классическая модель — Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="57ed5-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="57ed5-107">Шаблон Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="57ed5-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="57ed5-108">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="57ed5-108">Azure CLI 1.0</span></span>](application-gateway-create-gateway-cli.md)
> * [<span data-ttu-id="57ed5-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="57ed5-109">Azure CLI 2.0</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="57ed5-110">Шлюз приложений — это выделенный виртуальный модуль, предоставляющий контроллер доставки приложений (ADC) как услугу, который обеспечивает для приложения множество функций балансировки нагрузки уровня 7.</span><span class="sxs-lookup"><span data-stu-id="57ed5-110">Application Gateway is a dedicated virtual appliance that provides application delivery controller (ADC) as a service, offering various layer 7 load balancing capabilities for your application.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="57ed5-111">Версии интерфейса командной строки для выполнения задачи</span><span class="sxs-lookup"><span data-stu-id="57ed5-111">CLI versions to complete the task</span></span>

<span data-ttu-id="57ed5-112">Вы можете выполнить задачу, используя одну из следующих версий интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="57ed5-112">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="57ed5-113">[Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) — это интерфейс командной строки для классической модели развертывания и модели развертывания Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="57ed5-113">[Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="57ed5-114">[Azure CLI 2.0](application-gateway-create-gateway-cli.md) — это интерфейс командной строки нового поколения для модели развертывания Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="57ed5-114">[Azure CLI 2.0](application-gateway-create-gateway-cli.md) - our next generation CLI for the resource management deployment model</span></span>

## <a name="prerequisite-install-the-azure-cli-20"></a><span data-ttu-id="57ed5-115">Предварительные требования. Установка Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="57ed5-115">Prerequisite: Install the Azure CLI 2.0</span></span>

<span data-ttu-id="57ed5-116">Для выполнения действий, описанных в этой статье, требуется [установить интерфейс командной строки Azure для Mac, Linux и Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="57ed5-116">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

> [!NOTE]
> <span data-ttu-id="57ed5-117">Если у вас нет учетной записи Azure, то вам потребуется получить ее.</span><span class="sxs-lookup"><span data-stu-id="57ed5-117">If you don't have an Azure account, you need one.</span></span> <span data-ttu-id="57ed5-118">Зарегистрируйтесь, чтобы получить [бесплатную пробную версию](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="57ed5-118">Go sign up for a [free trial here](../active-directory/sign-up-organization.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="57ed5-119">Сценарий</span><span class="sxs-lookup"><span data-stu-id="57ed5-119">Scenario</span></span>

<span data-ttu-id="57ed5-120">В этом сценарии вы узнаете, как создать шлюз приложений с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="57ed5-120">In this scenario, you learn how to create an application gateway using the Azure portal.</span></span>

<span data-ttu-id="57ed5-121">Вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="57ed5-121">This scenario will:</span></span>

* <span data-ttu-id="57ed5-122">как создать средний шлюз приложений с двумя экземплярами;</span><span class="sxs-lookup"><span data-stu-id="57ed5-122">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="57ed5-123">как создать виртуальную сеть AdatumAppGatewayVNET с зарезервированным блоком CIDR (10.0.0.0/16);</span><span class="sxs-lookup"><span data-stu-id="57ed5-123">Create a virtual network named AdatumAppGatewayVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="57ed5-124">как создать подсеть с именем Appgatewaysubnet и блоком CIDR (10.0.0.0/28);</span><span class="sxs-lookup"><span data-stu-id="57ed5-124">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>

> [!NOTE]
> <span data-ttu-id="57ed5-125">Дополнительная настройка шлюза приложений, включая пользовательские пробы работоспособности, серверный пул адресов и дополнительные правила, осуществляется после настройки шлюза приложений, а не во время первоначального развертывания.</span><span class="sxs-lookup"><span data-stu-id="57ed5-125">Additional configuration of the application gateway, including custom health probes, backend pool addresses, and additional rules are configured after the application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="57ed5-126">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="57ed5-126">Before you begin</span></span>

<span data-ttu-id="57ed5-127">Шлюзу приложений Azure требуется собственная подсеть.</span><span class="sxs-lookup"><span data-stu-id="57ed5-127">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="57ed5-128">При создании виртуальной сети обязательно оставьте достаточно адресного пространства для нескольких подсетей.</span><span class="sxs-lookup"><span data-stu-id="57ed5-128">When creating a virtual network, ensure that you leave enough address space to have multiple subnets.</span></span> <span data-ttu-id="57ed5-129">После развертывания шлюза приложений в подсети в нее можно добавлять только дополнительные шлюзы приложений.</span><span class="sxs-lookup"><span data-stu-id="57ed5-129">Once you deploy an application gateway to a subnet, only additional application gateways can be added to the subnet.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="57ed5-130">Вход в Azure</span><span class="sxs-lookup"><span data-stu-id="57ed5-130">Log in to Azure</span></span>

<span data-ttu-id="57ed5-131">Откройте **командную строку Microsoft Azure**, и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="57ed5-131">Open the **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli-interactive
az login -u "username"
```

> [!NOTE]
> <span data-ttu-id="57ed5-132">Команду `az login` также можно использовать без параметра для входа на устройство, при котором требуется ввести код на странице aka.ms/devicelogin.</span><span class="sxs-lookup"><span data-stu-id="57ed5-132">You can also use `az login` without the switch for device login that requires entering a code at aka.ms/devicelogin.</span></span>

<span data-ttu-id="57ed5-133">Введя предыдущий пример, вы получите код.</span><span class="sxs-lookup"><span data-stu-id="57ed5-133">Once you type the preceding example, a code is provided.</span></span> <span data-ttu-id="57ed5-134">В браузере перейдите по адресу https://aka.ms/devicelogin, чтобы продолжить процедуру входа.</span><span class="sxs-lookup"><span data-stu-id="57ed5-134">Navigate to https://aka.ms/devicelogin in a browser to continue the login process.</span></span>

![Команда, выводящая имя пользователя устройства][1]

<span data-ttu-id="57ed5-136">В браузере введите полученный код.</span><span class="sxs-lookup"><span data-stu-id="57ed5-136">In the browser, enter the code you received.</span></span> <span data-ttu-id="57ed5-137">Вы будете перенаправлены на страницу входа.</span><span class="sxs-lookup"><span data-stu-id="57ed5-137">You are redirected to a sign-in page.</span></span>

![Ввод кода в браузере][2]

<span data-ttu-id="57ed5-139">Когда вы выполните вход, введя код, закройте браузер, чтобы продолжить работу.</span><span class="sxs-lookup"><span data-stu-id="57ed5-139">Once the code has been entered you are signed in, close the browser to continue on with the scenario.</span></span>

![Вход выполнен][3]

## <a name="create-the-resource-group"></a><span data-ttu-id="57ed5-141">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="57ed5-141">Create the resource group</span></span>

<span data-ttu-id="57ed5-142">Перед созданием шлюза приложений создается группа ресурсов, которая будет содержать шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="57ed5-142">Before creating the application gateway, a resource group is created to contain the application gateway.</span></span> <span data-ttu-id="57ed5-143">Ниже показана команда для создания группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="57ed5-143">The following shows the command.</span></span>

```azurecli-interactive
az group create --name myresourcegroup --location "eastus"
```

## <a name="create-the-application-gateway"></a><span data-ttu-id="57ed5-144">Создание шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="57ed5-144">Create the application gateway</span></span>

<span data-ttu-id="57ed5-145">IP-адреса серверной части — это IP-адреса внутреннего сервера.</span><span class="sxs-lookup"><span data-stu-id="57ed5-145">The IP addresses used for the backend are the IP addresses for your backend server.</span></span> <span data-ttu-id="57ed5-146">Эти значения могут быть частными IP-адресами в виртуальной сети, общедоступными IP-адресами или полными доменными именами для внутренних серверов.</span><span class="sxs-lookup"><span data-stu-id="57ed5-146">These values can be either private IPs in the virtual network, public ips, or fully qualified domain names for your backend servers.</span></span> <span data-ttu-id="57ed5-147">В следующем примере создается шлюз приложений с дополнительными параметрами конфигурации, задающими настройки HTTP, порты и правила.</span><span class="sxs-lookup"><span data-stu-id="57ed5-147">The following example creates an application gateway with additional configuration settings for http settings, ports, and rules.</span></span>

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

<span data-ttu-id="57ed5-148">В предыдущем примере показано множество свойств, которые не являются обязательными во время создания шлюза приложения.</span><span class="sxs-lookup"><span data-stu-id="57ed5-148">The preceding example shows many properties that are not required during the creation of an application gateway.</span></span> <span data-ttu-id="57ed5-149">Следующий пример кода создает шлюз приложений с использованием требуемой информации.</span><span class="sxs-lookup"><span data-stu-id="57ed5-149">The following code example creates an application gateway with the required information.</span></span>

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
> <span data-ttu-id="57ed5-150">Чтобы вывести список параметров, которые можно указать во время создания, выполните команду `az network application-gateway create --help`.</span><span class="sxs-lookup"><span data-stu-id="57ed5-150">For a list of parameters that can be provided during creation run the following command: `az network application-gateway create --help`.</span></span>

<span data-ttu-id="57ed5-151">В этом примере создается базовый шлюз приложений с параметрами по умолчанию для прослушивателя, серверного пула, протокола HTTP серверной части и правил.</span><span class="sxs-lookup"><span data-stu-id="57ed5-151">This example creates a basic application gateway with default settings for the listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="57ed5-152">Вы сможете изменить эти параметры в соответствии с развертыванием после успешного завершения подготовки.</span><span class="sxs-lookup"><span data-stu-id="57ed5-152">You can modify these settings to suit your deployment once the provisioning is successful.</span></span>
<span data-ttu-id="57ed5-153">Если на предыдущем шаге вы уже определили для веб-приложения внутренний пул, то после создания шлюза запускается балансировка нагрузки.</span><span class="sxs-lookup"><span data-stu-id="57ed5-153">If you already have your web application defined with the backend pool in the preceding steps, once created, load balancing begins.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="57ed5-154">Получение DNS-имени шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="57ed5-154">Get application gateway DNS name</span></span>

<span data-ttu-id="57ed5-155">После создания шлюза следует настроить внешний интерфейс для обмена данными.</span><span class="sxs-lookup"><span data-stu-id="57ed5-155">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="57ed5-156">Если вы используете общедоступный IP-адрес, шлюзу приложений требуется динамически назначаемое непонятное имя DNS.</span><span class="sxs-lookup"><span data-stu-id="57ed5-156">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="57ed5-157">Чтобы гарантировать попадание пользователей на шлюз приложений, можно использовать запись CNAME, чтобы указать общедоступную конечную точку шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="57ed5-157">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="57ed5-158">[Настройка пользовательского имени домена в Azure](../dns/dns-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="57ed5-158">[Configuring a custom domain name for in Azure](../dns/dns-custom-domain.md).</span></span> <span data-ttu-id="57ed5-159">Чтобы настроить псевдоним, извлеките подробные сведения о шлюзе приложений и соответствующий IP-адрес или DNS-имя с помощью элемента PublicIPAddress, связанного со шлюзом приложений.</span><span class="sxs-lookup"><span data-stu-id="57ed5-159">To configure an alias, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="57ed5-160">DNS-имя шлюза приложений должно использоваться для создания записи CNAME, указывающей двум веб-приложениям на это DNS-имя.</span><span class="sxs-lookup"><span data-stu-id="57ed5-160">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="57ed5-161">Использование записи A не рекомендуется, так как виртуальный IP-адрес может измениться после перезапуска приложения шлюза.</span><span class="sxs-lookup"><span data-stu-id="57ed5-161">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>


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

## <a name="delete-all-resources"></a><span data-ttu-id="57ed5-162">Удаление всех ресурсов</span><span class="sxs-lookup"><span data-stu-id="57ed5-162">Delete all resources</span></span>

<span data-ttu-id="57ed5-163">Чтобы удалить все ресурсы, созданные в этой статье, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="57ed5-163">To delete all resources created in this article, complete the following steps:</span></span>

```azurecli-interactive
az group delete --name AdatumAppGatewayRG
```
 
## <a name="next-steps"></a><span data-ttu-id="57ed5-164">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="57ed5-164">Next steps</span></span>

<span data-ttu-id="57ed5-165">Узнайте, как создавать пользовательские пробы работоспособности, посетив страницу [Create a custom probe for Application Gateway by using the portal](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="57ed5-165">Learn how to create custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="57ed5-166">Узнайте, как настроить разгрузку SSL и убрать дорогостоящее шифрование SSL с веб-серверов, посетив страницу [Настройка шлюза приложений для разгрузки SSL с помощью диспетчера ресурсов Azure](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="57ed5-166">Learn how to configure SSL Offloading and take the costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli/scenario.png
[1]: ./media/application-gateway-create-gateway-cli/figure1.png
[2]: ./media/application-gateway-create-gateway-cli/figure2.png
[3]: ./media/application-gateway-create-gateway-cli/figure3.png
