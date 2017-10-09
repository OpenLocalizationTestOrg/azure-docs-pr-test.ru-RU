---
title: "брандмауэр веб-приложения aaaConfigure - шлюз приложений Azure | Документы Microsoft"
description: "Это статье предоставлены рекомендации по как с помощью toostart веб-приложение брандмауэра на шлюза существующего или нового приложения."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 670b9732-874b-43e6-843b-d2585c160982
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: gwallace
ms.openlocfilehash: d5354984760ceab12ed49efa9e18836e9f1d3c96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway-with-azure-cli"></a><span data-ttu-id="b252a-103">Настройка брандмауэра веб-приложения на новом или имеющемся шлюзе приложений с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b252a-103">Configure web application firewall on a new or existing Application Gateway with Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b252a-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="b252a-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="b252a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b252a-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="b252a-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="b252a-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="b252a-107">Узнайте, как toocreate брандмауэр веб-приложения включено использование шлюза приложений или добавить веб-приложение брандмауэра tooan существующие приложения шлюза.</span><span class="sxs-lookup"><span data-stu-id="b252a-107">Learn how toocreate a web application firewall enabled application gateway or add web application firewall tooan existing application gateway.</span></span>

<span data-ttu-id="b252a-108">Hello брандмауэр веб-приложения (WAF) в шлюз приложений Azure защищает веб-приложений из распространенных веб-атак, например путем внедрения кода SQL, атак с использованием межсайтовых сценариев и сеанса захвата.</span><span class="sxs-lookup"><span data-stu-id="b252a-108">hello web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span>

<span data-ttu-id="b252a-109">Шлюз приложений — это балансировщик нагрузки уровня 7.</span><span class="sxs-lookup"><span data-stu-id="b252a-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="b252a-110">Он обеспечивает отработку отказа, маршрутизации производительности HTTP-запросы между различными серверами, являются ли они на hello облачной или локальной.</span><span class="sxs-lookup"><span data-stu-id="b252a-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="b252a-111">Шлюз приложений выполняет многие функции контроллера доставки приложений (ADC), включая балансировку нагрузки HTTP, определение сходства сеансов на основе файлов cookie, разгрузку SSL, выполнение пользовательской проверки работоспособности, поддержку нескольких сайтов и т. д.</span><span class="sxs-lookup"><span data-stu-id="b252a-111">Application gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, secure sockets layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="b252a-112">Полный список поддерживаемых функций toofind посетите: [шлюза Обзор приложений](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b252a-112">toofind a complete list of supported features, visit: [Overview of Application Gateway](application-gateway-introduction.md).</span></span>

<span data-ttu-id="b252a-113">Hello следующей статье показано, каким образом слишком[добавить веб-приложение брандмауэра tooan существующие приложения шлюза](#add-web-application-firewall-to-an-existing-application-gateway) и [создания шлюза приложения, использующего брандмауэр веб-приложения](#create-an-application-gateway-with-web-application-firewall).</span><span class="sxs-lookup"><span data-stu-id="b252a-113">hello following article shows how too[add web application firewall tooan existing application gateway](#add-web-application-firewall-to-an-existing-application-gateway) and [create an application gateway that uses web application firewall](#create-an-application-gateway-with-web-application-firewall).</span></span>

![Изображение для сценария][scenario]

## <a name="prerequisite-install-hello-azure-cli-20"></a><span data-ttu-id="b252a-115">Необходимое условие: Установите hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b252a-115">Prerequisite: Install hello Azure CLI 2.0</span></span>

<span data-ttu-id="b252a-116">tooperform hello шаги в этой статье, вы должны слишком[Установка hello интерфейса командной строки Azure для Mac, Linux и Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="b252a-116">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="waf-configuration-differences"></a><span data-ttu-id="b252a-117">Различия в конфигурации WAF</span><span class="sxs-lookup"><span data-stu-id="b252a-117">WAF configuration differences</span></span>

<span data-ttu-id="b252a-118">Если вы прочитали [создать шлюз приложений с Azure CLI](application-gateway-create-gateway-cli.md), при создании шлюза приложения, понять tooconfigure параметры hello SKU.</span><span class="sxs-lookup"><span data-stu-id="b252a-118">If you have read [Create an Application Gateway with Azure CLI](application-gateway-create-gateway-cli.md), you understand hello SKU settings tooconfigure when creating an application gateway.</span></span> <span data-ttu-id="b252a-119">WAF предоставляет дополнительные параметры toodefine при настройке hello SKU для шлюза приложения.</span><span class="sxs-lookup"><span data-stu-id="b252a-119">WAF provides additional settings toodefine when configuring hello SKU on an application gateway.</span></span> <span data-ttu-id="b252a-120">Отсутствуют дополнительные изменения, внесенные на сам шлюз приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b252a-120">There are no additional changes that you make on hello application gateway itself.</span></span>

| <span data-ttu-id="b252a-121">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="b252a-121">**Setting**</span></span> | <span data-ttu-id="b252a-122">**Дополнительные сведения**</span><span class="sxs-lookup"><span data-stu-id="b252a-122">**Details**</span></span>
|---|---|
|<span data-ttu-id="b252a-123">**SKU**</span><span class="sxs-lookup"><span data-stu-id="b252a-123">**SKU**</span></span> |<span data-ttu-id="b252a-124">Обычный шлюз приложений без WAF поддерживает размеры **Standard\_Small**, **Standard\_Medium** и **Standard\_Large**.</span><span class="sxs-lookup"><span data-stu-id="b252a-124">A normal application gateway without WAF supports **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large** sizes.</span></span> <span data-ttu-id="b252a-125">С появлением hello WAF, приведены два дополнительных конфигураций, **WAF\_Средний** и **WAF\_большой**.</span><span class="sxs-lookup"><span data-stu-id="b252a-125">With hello introduction of WAF, there are two additional SKUs, **WAF\_Medium** and **WAF\_Large**.</span></span> <span data-ttu-id="b252a-126">WAF не поддерживается в шлюзах приложения уровня "Мелкий".</span><span class="sxs-lookup"><span data-stu-id="b252a-126">WAF is not supported on small application gateways.</span></span>|
|<span data-ttu-id="b252a-127">**Режим**</span><span class="sxs-lookup"><span data-stu-id="b252a-127">**Mode**</span></span> | <span data-ttu-id="b252a-128">Этот параметр является режимом hello WAF.</span><span class="sxs-lookup"><span data-stu-id="b252a-128">This setting is hello mode of WAF.</span></span> <span data-ttu-id="b252a-129">Допустимые значения: **Обнаружение** и **Предотвращение**.</span><span class="sxs-lookup"><span data-stu-id="b252a-129">allowed values are **Detection** and **Prevention**.</span></span> <span data-ttu-id="b252a-130">Если WAF работает в режиме обнаружения, все угрозы заносятся в файл журнала.</span><span class="sxs-lookup"><span data-stu-id="b252a-130">When WAF is set up in detection mode, all threats are stored in a log file.</span></span> <span data-ttu-id="b252a-131">В режиме защиты от событий по-прежнему регистрируются, но hello злоумышленник получит 403 несанкционированного ответ от шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b252a-131">In prevention mode, events are still logged but hello attacker receives a 403 unauthorized response from hello application gateway.</span></span>|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a><span data-ttu-id="b252a-132">Добавить веб-приложение брандмауэра tooan существующие приложения шлюза</span><span class="sxs-lookup"><span data-stu-id="b252a-132">Add web application firewall tooan existing application gateway</span></span>

<span data-ttu-id="b252a-133">Hello выполните команду изменения существующего приложения с поддержкой шлюза tooa WAF стандартного приложения шлюза.</span><span class="sxs-lookup"><span data-stu-id="b252a-133">hello follow command changes an existing standard application gateway tooa WAF enabled application gateway.</span></span>

```azurecli-interactive
#!/bin/bash

az network application-gateway waf-config set \
  --enabled true \
  --firewall-mode Prevention \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"
```

<span data-ttu-id="b252a-134">Эта команда обновляет шлюза приложения hello брандмауэр веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="b252a-134">This command updates hello application gateway with web application firewall.</span></span> <span data-ttu-id="b252a-135">Посетите [диагностику шлюза приложения](application-gateway-diagnostics.md) toounderstand как tooview журналы для шлюза приложения.</span><span class="sxs-lookup"><span data-stu-id="b252a-135">Visit [Application Gateway Diagnostics](application-gateway-diagnostics.md) toounderstand how tooview logs for your application gateway.</span></span> <span data-ttu-id="b252a-136">Из-за особенностей безопасности toohello WAF toobe необходимость журналы регулярно контролировать состояние безопасности hello toounderstand веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="b252a-136">Due toohello security nature of WAF, logs need toobe reviewed regularly toounderstand hello security posture of your web applications.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="b252a-137">Создание шлюза приложений с брандмауэром веб-приложения</span><span class="sxs-lookup"><span data-stu-id="b252a-137">Create an Application Gateway with web application firewall</span></span>

<span data-ttu-id="b252a-138">Привет, следующая команда создает шлюза приложения с брандмауэр веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="b252a-138">hello following command creates an Application Gateway with web application firewall.</span></span>

```azurecli-interactive
#!/bin/bash

az network application-gateway create \
  --name "AdatumAppGateway2" \
  --location "eastus" \
  --resource-group "AdatumAppGatewayRG" \
  --vnet-name "AdatumAppGatewayVNET2" \
  --vnet-address-prefix "10.0.0.0/16" \
  --subnet "Appgatewaysubnet2" \
  --subnet-address-prefix "10.0.0.0/28" \
 --servers "10.0.0.5 10.0.0.4" \
  --capacity 2 
  --sku "WAF_Medium" \
  --http-settings-cookie-based-affinity "Enabled" \
  --http-settings-protocol "Http" \
  --frontend-port "80" \
  --routing-rule-type "Basic" \
  --http-settings-port "80" \
  --public-ip-address "pip2" \
  --public-ip-address-allocation "dynamic" \
  --tags "cli[2] owner[administrator]"
```

> [!NOTE]
> <span data-ttu-id="b252a-139">Шлюзы приложений, созданных с помощью конфигурации брандмауэра hello основные веб-приложений, настроенных с CRS 3.0 для защиты.</span><span class="sxs-lookup"><span data-stu-id="b252a-139">Application gateways created with hello basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="b252a-140">Получение DNS-имени шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="b252a-140">Get application gateway DNS name</span></span>

<span data-ttu-id="b252a-141">После создания шлюза hello hello следующим шагом является tooconfigure hello внешнего интерфейса для обмена данными.</span><span class="sxs-lookup"><span data-stu-id="b252a-141">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="b252a-142">Если вы используете общедоступный IP-адрес, шлюзу приложений требуется динамически назначаемое непонятное имя DNS.</span><span class="sxs-lookup"><span data-stu-id="b252a-142">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="b252a-143">tooensure конечным пользователям возможность нажать шлюза приложения hello, запись CNAME может быть используется toopoint toohello общедоступную конечную точку шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b252a-143">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="b252a-144">[Настройка пользовательского имени домена в Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b252a-144">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="b252a-145">tooconfigure запись CNAME, получить сведения о шлюза приложения hello и соответствующее IP или DNS-имя с помощью шлюза hello PublicIPAddress элемент toohello подключенных приложений.</span><span class="sxs-lookup"><span data-stu-id="b252a-145">tooconfigure a CNAME record, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="b252a-146">шлюз приложения Hello DNS-имя должно быть используется toocreate запись CNAME, какие точки hello двух web приложений toothis DNS-имя.</span><span class="sxs-lookup"><span data-stu-id="b252a-146">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="b252a-147">Использование Hello записи A не рекомендуется, поскольку hello виртуального IP-адреса могут изменяться при перезагрузке шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="b252a-147">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

```azurecli-interactive
#!/bin/bash

az network public-ip show \
  --name pip2 \
  --resource-group "AdatumAppGatewayRG"
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

## <a name="next-steps"></a><span data-ttu-id="b252a-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b252a-148">Next steps</span></span>

<span data-ttu-id="b252a-149">Узнайте, как toocustomize WAF правила, посетив: [настроить правила брандмауэра приложения web через hello Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b252a-149">Learn how toocustomize WAF rules by visiting: [Customize web application firewall rules through hello Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md).</span></span>

[scenario]: ./media/application-gateway-web-application-firewall-cli/scenario.png
