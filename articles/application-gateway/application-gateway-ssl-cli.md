---
title: "aaaConfigure SSL разгрузки - шлюз приложения Azure - Azure CLI 2.0 | Документы Microsoft"
description: "На этой странице представлены инструкции toocreate разгрузки шлюза приложения с использованием SSL 2.0 Azure CLI"
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
ms.openlocfilehash: f8d50e0c6ffef17c807938d816410e6d85321c9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-cli-20"></a><span data-ttu-id="f2666-103">Настройка шлюза приложений для разгрузки SSL с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f2666-103">Configure an application gateway for SSL offload by using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f2666-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="f2666-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="f2666-105">PowerShell и диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="f2666-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="f2666-106">Классическая модель — Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f2666-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="f2666-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f2666-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="f2666-108">Шлюз приложения Azure может быть настроенный tooterminate hello Secure Sockets Layer (SSL) сеанс при hello шлюза tooavoid дорогостоящих SSL расшифровки задачи toohappen на hello веб-фермы.</span><span class="sxs-lookup"><span data-stu-id="f2666-108">Azure Application Gateway can be configured tooterminate hello Secure Sockets Layer (SSL) session at hello gateway tooavoid costly SSL decryption tasks toohappen at hello web farm.</span></span> <span data-ttu-id="f2666-109">Разгрузка SSL также упрощает управление сертификатами на внешнем сервере hello.</span><span class="sxs-lookup"><span data-stu-id="f2666-109">SSL offload also simplifies certificate management at hello front-end server.</span></span>

## <a name="prerequisite-install-hello-azure-cli-20"></a><span data-ttu-id="f2666-110">Необходимое условие: Установите hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f2666-110">Prerequisite: Install hello Azure CLI 2.0</span></span>

<span data-ttu-id="f2666-111">tooperform hello шаги в этой статье, вы должны слишком[Установка hello интерфейса командной строки Azure для Mac, Linux и Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="f2666-111">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="required-components"></a><span data-ttu-id="f2666-112">Необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="f2666-112">Required components</span></span>

* <span data-ttu-id="f2666-113">**Пул серверных:** hello список IP-адресов серверов hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="f2666-113">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="f2666-114">Hello IP-адресов либо должен принадлежать подсети виртуальной сети toohello или должен быть открытый IP-адрес или VIP.</span><span class="sxs-lookup"><span data-stu-id="f2666-114">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="f2666-115">**Параметры внутреннего пула серверов**. Каждый пул имеет такие параметры, как порт, протокол и сходство на основе файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="f2666-115">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="f2666-116">Эти параметры являются связанные tooa пул, а также примененные tooall серверы в пуле hello.</span><span class="sxs-lookup"><span data-stu-id="f2666-116">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="f2666-117">**Интерфейсный порт:** этой цели используется порт hello открытый порт, который открыт в шлюзе приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f2666-117">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="f2666-118">Трафик обращений к этому порту, а затем возвращает перенаправляется tooone серверов hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="f2666-118">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="f2666-119">**Прослушиватель:** hello прослушиватель имеет интерфейсный порт, протокол (Http или Https, эти параметры зависят от регистра) и имя сертификата SSL hello (при настройке протокола SSL разгрузки).</span><span class="sxs-lookup"><span data-stu-id="f2666-119">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these settings are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="f2666-120">**Правило:** правило hello привязывает прослушивателя hello и пул серверных hello и определяет, какие серверных пула hello трафику следует применять направленной toowhen попадании конкретного прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="f2666-120">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="f2666-121">В настоящее время только hello *основные* правило поддерживается.</span><span class="sxs-lookup"><span data-stu-id="f2666-121">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="f2666-122">Hello *основные* правило — распределение нагрузки с циклическим перебором.</span><span class="sxs-lookup"><span data-stu-id="f2666-122">hello *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="f2666-123">**Дополнительные примечания по настройке конфигурации**</span><span class="sxs-lookup"><span data-stu-id="f2666-123">**Additional configuration notes**</span></span>

<span data-ttu-id="f2666-124">Для настройки сертификатов SSL, hello протокола в **HttpListener** следует изменить слишком*Https* (с учетом регистра).</span><span class="sxs-lookup"><span data-stu-id="f2666-124">For SSL certificates configuration, hello protocol in **HttpListener** should change too*Https* (case sensitive).</span></span> <span data-ttu-id="f2666-125">Hello **SslCertificate** слишком добавляется элемент**HttpListener** с hello значения переменной, настроенных для hello SSL-сертификат.</span><span class="sxs-lookup"><span data-stu-id="f2666-125">hello **SslCertificate** element is added too**HttpListener** with hello variable value configured for hello SSL certificate.</span></span> <span data-ttu-id="f2666-126">Hello интерфейсный порт должен быть обновленные too443.</span><span class="sxs-lookup"><span data-stu-id="f2666-126">hello front-end port should be updated too443.</span></span>

<span data-ttu-id="f2666-127">**сопоставление на основе файла cookie tooenable**: шлюза приложения может быть настроенный tooensure запроса из сеанса клиента всегда является направленным toohello одной виртуальной Машины hello веб-ферме.</span><span class="sxs-lookup"><span data-stu-id="f2666-127">**tooenable cookie-based affinity**: An application gateway can be configured tooensure that a request from a client session is always directed toohello same VM in hello web farm.</span></span> <span data-ttu-id="f2666-128">Этот сценарий выполняется путем внедрения кода файла cookie сеанса, которое разрешает трафик toodirect шлюза hello соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="f2666-128">This scenario is done by injection of a session cookie that allows hello gateway toodirect traffic appropriately.</span></span> <span data-ttu-id="f2666-129">Задайте сопоставление на основе файла cookie tooenable **CookieBasedAffinity** слишком*включено* в hello **BackendHttpSettings** элемента.</span><span class="sxs-lookup"><span data-stu-id="f2666-129">tooenable cookie-based affinity, set **CookieBasedAffinity** too*Enabled* in hello **BackendHttpSettings** element.</span></span>

## <a name="configure-ssl-offload-on-an-existing-application-gateway"></a><span data-ttu-id="f2666-130">Настройка разгрузки SSL на имеющемся шлюзе приложений</span><span class="sxs-lookup"><span data-stu-id="f2666-130">Configure SSL offload on an existing application gateway</span></span>

```azurecli-interactive
#!/bin/bash

# Create a new front end port toobe used for SSL
az network application-gateway frontend-port create \
  --name sslport \
  --port 443 \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Upload hello .pfx certificate for SSL offload
az network application-gateway ssl-cert create \
  --name "newcert" \
  --cert-file /home/azureuser/self-signed/AdatumAppGatewayCert.pfx \
  --cert-password P@ssw0rd \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new listener referencing hello port and certificate created earlier
az network application-gateway http-listener create \
  --frontend-ip "appGatewayFrontendIP" \
  --frontend-port sslport  \
  --name sslListener \
  --ssl-cert newcert \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new back-end pool toobe used
az network application-gateway address-pool create \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG" \
  --name "appGatewayBackendPool2" \
  --servers 10.0.0.7 10.0.0.8

# Create a new back-end HTTP settings using hello new probe
az network application-gateway http-settings create \
  --name "settings2" \
  --port 80 \
  --cookie-based-affinity Enabled \
  --protocol "Http" \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new rule linking hello listener toohello back-end pool
az network application-gateway rule create \
  --name "rule2" \
  --rule-type Basic \
  --http-settings settings2 \
  --http-listener ssllistener \
  --address-pool temp1 \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

```

## <a name="create-an-application-gateway-with-ssl-offload"></a><span data-ttu-id="f2666-131">Создание шлюза приложений с разгрузкой SSL</span><span class="sxs-lookup"><span data-stu-id="f2666-131">Create an application gateway with SSL Offload</span></span>

<span data-ttu-id="f2666-132">Следующий образец Hello создает шлюза приложения с разгрузки SSL.</span><span class="sxs-lookup"><span data-stu-id="f2666-132">hello following sample creates an application gateway with SSL offload.</span></span>  <span data-ttu-id="f2666-133">Hello сертификат и пароль для сертификата должен быть обновленные tooa действительного закрытого ключа.</span><span class="sxs-lookup"><span data-stu-id="f2666-133">hello certificate and certificate password must be updated tooa valid private key.</span></span>

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

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="f2666-134">Получение DNS-имени шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="f2666-134">Get application gateway DNS name</span></span>

<span data-ttu-id="f2666-135">После создания шлюза hello hello следующим шагом является tooconfigure hello внешнего интерфейса для обмена данными.</span><span class="sxs-lookup"><span data-stu-id="f2666-135">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="f2666-136">Если вы используете общедоступный IP-адрес, шлюзу приложений требуется динамически назначаемое непонятное имя DNS.</span><span class="sxs-lookup"><span data-stu-id="f2666-136">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="f2666-137">tooensure конечным пользователям возможность нажать шлюза приложения hello, запись CNAME может быть используется toopoint toohello общедоступную конечную точку шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f2666-137">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="f2666-138">[Настройка пользовательского имени домена в Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f2666-138">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="f2666-139">tooconfigure псевдоним, получить сведения о шлюза приложения hello и соответствующее IP или DNS-имя с помощью шлюза hello PublicIPAddress элемент toohello подключенных приложений.</span><span class="sxs-lookup"><span data-stu-id="f2666-139">tooconfigure an alias, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="f2666-140">шлюз приложения Hello DNS-имя должно быть используется toocreate запись CNAME, какие точки hello двух web приложений toothis DNS-имя.</span><span class="sxs-lookup"><span data-stu-id="f2666-140">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="f2666-141">Использование Hello записи A не рекомендуется, поскольку hello виртуального IP-адреса могут изменяться при перезагрузке шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="f2666-141">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>


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

## <a name="next-steps"></a><span data-ttu-id="f2666-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f2666-142">Next steps</span></span>

<span data-ttu-id="f2666-143">Если tooconfigure toouse шлюза приложения с внутренней подсистемы балансировки нагрузки (ILB), см. [создать шлюз приложений с внутренней подсистемы балансировки нагрузки (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="f2666-143">If you want tooconfigure an application gateway toouse with an internal load balancer (ILB), see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="f2666-144">Дополнительные сведения о параметрах балансировки нагрузки в целом см. в статьях:</span><span class="sxs-lookup"><span data-stu-id="f2666-144">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="f2666-145">Подсистема балансировщика нагрузки Azure</span><span class="sxs-lookup"><span data-stu-id="f2666-145">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="f2666-146">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="f2666-146">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)
