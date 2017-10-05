---
title: "Настройка разгрузки SSL для шлюза приложений Azure с помощью Azure CLI 2.0 | Документация Майкрософт"
description: "На этой странице приводятся инструкции по созданию шлюза приложений с разгрузкой SSL с помощью Azure CLI 2.0."
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
ms.openlocfilehash: e8c1ba09daef09ef5002e33345905772961c1d93
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-cli-20"></a><span data-ttu-id="09b64-103">Настройка шлюза приложений для разгрузки SSL с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="09b64-103">Configure an application gateway for SSL offload by using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="09b64-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="09b64-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="09b64-105">PowerShell и диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="09b64-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="09b64-106">Классическая модель — Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="09b64-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="09b64-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="09b64-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="09b64-108">Шлюз приложений Azure можно настроить на завершение сеанса SSL в шлюзе, что позволит избежать выполнения дорогостоящей задачи SSL-шифрования на веб-ферме.</span><span class="sxs-lookup"><span data-stu-id="09b64-108">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span></span> <span data-ttu-id="09b64-109">Разгрузка SSL также упрощает управление сертификатами на сервере переднего плана.</span><span class="sxs-lookup"><span data-stu-id="09b64-109">SSL offload also simplifies certificate management at the front-end server.</span></span>

## <a name="prerequisite-install-the-azure-cli-20"></a><span data-ttu-id="09b64-110">Предварительные требования. Установка Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="09b64-110">Prerequisite: Install the Azure CLI 2.0</span></span>

<span data-ttu-id="09b64-111">Для выполнения действий, описанных в этой статье, требуется [установить интерфейс командной строки Azure для Mac, Linux и Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="09b64-111">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="required-components"></a><span data-ttu-id="09b64-112">Необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="09b64-112">Required components</span></span>

* <span data-ttu-id="09b64-113">**Внутренний пул серверов**. Список IP-адресов внутренних серверов.</span><span class="sxs-lookup"><span data-stu-id="09b64-113">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="09b64-114">Указанные IP-адреса должны относиться к подсети виртуальной сети либо представлять собой общедоступные или виртуальные IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="09b64-114">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="09b64-115">**Параметры внутреннего пула серверов**. Каждый пул имеет такие параметры, как порт, протокол и сходство на основе файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="09b64-115">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="09b64-116">Эти параметры привязываются к пулу и применяются ко всем серверам в этом пуле.</span><span class="sxs-lookup"><span data-stu-id="09b64-116">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="09b64-117">**Интерфейсный порт**. Общедоступный порт, открытый в шлюзе приложений.</span><span class="sxs-lookup"><span data-stu-id="09b64-117">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="09b64-118">Трафик поступает на этот порт, а затем перенаправляется на один из тыловых серверов.</span><span class="sxs-lookup"><span data-stu-id="09b64-118">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="09b64-119">**Прослушиватель**. У прослушивателя есть интерфейсный порт, протокол (Http или Https, с учетом регистра) и имя SSL-сертификата (при настройке разгрузки SSL).</span><span class="sxs-lookup"><span data-stu-id="09b64-119">**Listener:** The listener has a front-end port, a protocol (Http or Https, these settings are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="09b64-120">**Правило**. Правило связывает прослушиватель и внутренний пул серверов, а также определяет, в какой внутренний пул серверов следует направлять трафик, поступающий на определенный прослушиватель.</span><span class="sxs-lookup"><span data-stu-id="09b64-120">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="09b64-121">В настоящее время поддерживается только *основное* правило.</span><span class="sxs-lookup"><span data-stu-id="09b64-121">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="09b64-122">*Основное* правило предусматривает циклическое распределение нагрузки.</span><span class="sxs-lookup"><span data-stu-id="09b64-122">The *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="09b64-123">**Дополнительные примечания по настройке конфигурации**</span><span class="sxs-lookup"><span data-stu-id="09b64-123">**Additional configuration notes**</span></span>

<span data-ttu-id="09b64-124">Чтобы настроить конфигурацию SSL-сертификатов, протокол в элементе **HttpListener** следует изменить на *Https* (с учетом регистра).</span><span class="sxs-lookup"><span data-stu-id="09b64-124">For SSL certificates configuration, the protocol in **HttpListener** should change to *Https* (case sensitive).</span></span> <span data-ttu-id="09b64-125">Элемент **SslCertificate** нужно добавить в **HttpListener**, указав в качестве значения переменную, настроенную для SSL-сертификата.</span><span class="sxs-lookup"><span data-stu-id="09b64-125">The **SslCertificate** element is added to **HttpListener** with the variable value configured for the SSL certificate.</span></span> <span data-ttu-id="09b64-126">Внешний порт следует изменить на 443.</span><span class="sxs-lookup"><span data-stu-id="09b64-126">The front-end port should be updated to 443.</span></span>

<span data-ttu-id="09b64-127">**Включение сходства на основе файлов cookie**. Шлюз приложений можно настроить так, чтобы запросы от клиентского сеанса всегда направлялись на одну виртуальную машину в веб-ферме.</span><span class="sxs-lookup"><span data-stu-id="09b64-127">**To enable cookie-based affinity**: An application gateway can be configured to ensure that a request from a client session is always directed to the same VM in the web farm.</span></span> <span data-ttu-id="09b64-128">Это делается с помощью внедрения файлов cookie сеанса, что позволяет шлюзу перенаправлять трафик соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="09b64-128">This scenario is done by injection of a session cookie that allows the gateway to direct traffic appropriately.</span></span> <span data-ttu-id="09b64-129">Чтобы включить сходство на основе файлов cookie, присвойте параметру **CookieBasedAffinity** в элементе *BackendHttpSettings* значение **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="09b64-129">To enable cookie-based affinity, set **CookieBasedAffinity** to *Enabled* in the **BackendHttpSettings** element.</span></span>

## <a name="configure-ssl-offload-on-an-existing-application-gateway"></a><span data-ttu-id="09b64-130">Настройка разгрузки SSL на имеющемся шлюзе приложений</span><span class="sxs-lookup"><span data-stu-id="09b64-130">Configure SSL offload on an existing application gateway</span></span>

```azurecli-interactive
#!/bin/bash

# Create a new front end port to be used for SSL
az network application-gateway frontend-port create \
  --name sslport \
  --port 443 \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Upload the .pfx certificate for SSL offload
az network application-gateway ssl-cert create \
  --name "newcert" \
  --cert-file /home/azureuser/self-signed/AdatumAppGatewayCert.pfx \
  --cert-password P@ssw0rd \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new listener referencing the port and certificate created earlier
az network application-gateway http-listener create \
  --frontend-ip "appGatewayFrontendIP" \
  --frontend-port sslport  \
  --name sslListener \
  --ssl-cert newcert \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new back-end pool to be used
az network application-gateway address-pool create \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG" \
  --name "appGatewayBackendPool2" \
  --servers 10.0.0.7 10.0.0.8

# Create a new back-end HTTP settings using the new probe
az network application-gateway http-settings create \
  --name "settings2" \
  --port 80 \
  --cookie-based-affinity Enabled \
  --protocol "Http" \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new rule linking the listener to the back-end pool
az network application-gateway rule create \
  --name "rule2" \
  --rule-type Basic \
  --http-settings settings2 \
  --http-listener ssllistener \
  --address-pool temp1 \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

```

## <a name="create-an-application-gateway-with-ssl-offload"></a><span data-ttu-id="09b64-131">Создание шлюза приложений с разгрузкой SSL</span><span class="sxs-lookup"><span data-stu-id="09b64-131">Create an application gateway with SSL Offload</span></span>

<span data-ttu-id="09b64-132">В следующем примере создается шлюз приложений с разгрузкой SSL.</span><span class="sxs-lookup"><span data-stu-id="09b64-132">The following sample creates an application gateway with SSL offload.</span></span>  <span data-ttu-id="09b64-133">Сертификат и пароль для сертификата необходимо обновить для действительного закрытого ключа.</span><span class="sxs-lookup"><span data-stu-id="09b64-133">The certificate and certificate password must be updated to a valid private key.</span></span>

```azurecli-interactive
#!/bin/bash

# Creates an application gateway with SSL offload
az network application-gateway create \
  --name "AdatumAppGateway3" \
  --location "eastus" \
  --resource-group "AdatumAppGatewayRG2" \
  --vnet-name "AdatumAppGatewayVNET2" \
  --cert-file /home/azureuser/self-signed/AdatumAppGatewayCert.pfx \
  --cert-password P@ssw0rd \
  --vnet-address-prefix "10.0.0.0/16" \
  --subnet "Appgatewaysubnet" \
  --subnet-address-prefix "10.0.0.0/28" \
  --frontend-port 443 \
  --servers "10.0.0.5 10.0.0.4" \
  --capacity 2 \
  --sku "Standard_Small" \
  --http-settings-cookie-based-affinity "Enabled" \
  --http-settings-protocol "Http" \
  --frontend-port "80" \
  --routing-rule-type "Basic" \
  --http-settings-port "80" \
  --public-ip-address "pip" \
  --public-ip-address-allocation "dynamic"
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="09b64-134">Получение DNS-имени шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="09b64-134">Get application gateway DNS name</span></span>

<span data-ttu-id="09b64-135">После создания шлюза следует настроить внешний интерфейс для обмена данными.</span><span class="sxs-lookup"><span data-stu-id="09b64-135">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="09b64-136">Если вы используете общедоступный IP-адрес, шлюзу приложений требуется динамически назначаемое непонятное имя DNS.</span><span class="sxs-lookup"><span data-stu-id="09b64-136">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="09b64-137">Чтобы гарантировать попадание пользователей на шлюз приложений, можно использовать запись CNAME, чтобы указать общедоступную конечную точку шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="09b64-137">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="09b64-138">[Настройка пользовательского имени домена в Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="09b64-138">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="09b64-139">Чтобы настроить псевдоним, извлеките подробные сведения о шлюзе приложений и соответствующий IP-адрес или DNS-имя с помощью элемента PublicIPAddress, связанного со шлюзом приложений.</span><span class="sxs-lookup"><span data-stu-id="09b64-139">To configure an alias, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="09b64-140">DNS-имя шлюза приложений должно использоваться для создания записи CNAME, указывающей двум веб-приложениям на это DNS-имя.</span><span class="sxs-lookup"><span data-stu-id="09b64-140">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="09b64-141">Использование записи A не рекомендуется, так как виртуальный IP-адрес может измениться после перезапуска приложения шлюза.</span><span class="sxs-lookup"><span data-stu-id="09b64-141">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>


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

## <a name="next-steps"></a><span data-ttu-id="09b64-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="09b64-142">Next steps</span></span>

<span data-ttu-id="09b64-143">Указания по настройке шлюза приложений для использования с внутренним балансировщиком нагрузки см. в статье [Создание шлюза приложений с внутренним балансировщиком нагрузки (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="09b64-143">If you want to configure an application gateway to use with an internal load balancer (ILB), see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="09b64-144">Дополнительные сведения о параметрах балансировки нагрузки в целом см. в статьях:</span><span class="sxs-lookup"><span data-stu-id="09b64-144">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="09b64-145">Подсистема балансировщика нагрузки Azure</span><span class="sxs-lookup"><span data-stu-id="09b64-145">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="09b64-146">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="09b64-146">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)
