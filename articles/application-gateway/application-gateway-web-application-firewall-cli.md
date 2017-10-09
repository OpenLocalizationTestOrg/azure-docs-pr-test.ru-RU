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
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway-with-azure-cli"></a>Настройка брандмауэра веб-приложения на новом или имеющемся шлюзе приложений с помощью Azure CLI

> [!div class="op_single_selector"]
> * [Портал Azure](application-gateway-web-application-firewall-portal.md)
> * [PowerShell](application-gateway-web-application-firewall-powershell.md)
> * [Интерфейс командной строки Azure](application-gateway-web-application-firewall-cli.md)

Узнайте, как toocreate брандмауэр веб-приложения включено использование шлюза приложений или добавить веб-приложение брандмауэра tooan существующие приложения шлюза.

Hello брандмауэр веб-приложения (WAF) в шлюз приложений Azure защищает веб-приложений из распространенных веб-атак, например путем внедрения кода SQL, атак с использованием межсайтовых сценариев и сеанса захвата.

Шлюз приложений — это балансировщик нагрузки уровня 7. Он обеспечивает отработку отказа, маршрутизации производительности HTTP-запросы между различными серверами, являются ли они на hello облачной или локальной. Шлюз приложений выполняет многие функции контроллера доставки приложений (ADC), включая балансировку нагрузки HTTP, определение сходства сеансов на основе файлов cookie, разгрузку SSL, выполнение пользовательской проверки работоспособности, поддержку нескольких сайтов и т. д. Полный список поддерживаемых функций toofind посетите: [шлюза Обзор приложений](application-gateway-introduction.md).

Hello следующей статье показано, каким образом слишком[добавить веб-приложение брандмауэра tooan существующие приложения шлюза](#add-web-application-firewall-to-an-existing-application-gateway) и [создания шлюза приложения, использующего брандмауэр веб-приложения](#create-an-application-gateway-with-web-application-firewall).

![Изображение для сценария][scenario]

## <a name="prerequisite-install-hello-azure-cli-20"></a>Необходимое условие: Установите hello Azure CLI 2.0

tooperform hello шаги в этой статье, вы должны слишком[Установка hello интерфейса командной строки Azure для Mac, Linux и Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

## <a name="waf-configuration-differences"></a>Различия в конфигурации WAF

Если вы прочитали [создать шлюз приложений с Azure CLI](application-gateway-create-gateway-cli.md), при создании шлюза приложения, понять tooconfigure параметры hello SKU. WAF предоставляет дополнительные параметры toodefine при настройке hello SKU для шлюза приложения. Отсутствуют дополнительные изменения, внесенные на сам шлюз приложения hello.

| **Параметр** | **Дополнительные сведения**
|---|---|
|**SKU** |Обычный шлюз приложений без WAF поддерживает размеры **Standard\_Small**, **Standard\_Medium** и **Standard\_Large**. С появлением hello WAF, приведены два дополнительных конфигураций, **WAF\_Средний** и **WAF\_большой**. WAF не поддерживается в шлюзах приложения уровня "Мелкий".|
|**Режим** | Этот параметр является режимом hello WAF. Допустимые значения: **Обнаружение** и **Предотвращение**. Если WAF работает в режиме обнаружения, все угрозы заносятся в файл журнала. В режиме защиты от событий по-прежнему регистрируются, но hello злоумышленник получит 403 несанкционированного ответ от шлюза приложения hello.|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a>Добавить веб-приложение брандмауэра tooan существующие приложения шлюза

Hello выполните команду изменения существующего приложения с поддержкой шлюза tooa WAF стандартного приложения шлюза.

```azurecli-interactive
#!/bin/bash

az network application-gateway waf-config set \
  --enabled true \
  --firewall-mode Prevention \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"
```

Эта команда обновляет шлюза приложения hello брандмауэр веб-приложения. Посетите [диагностику шлюза приложения](application-gateway-diagnostics.md) toounderstand как tooview журналы для шлюза приложения. Из-за особенностей безопасности toohello WAF toobe необходимость журналы регулярно контролировать состояние безопасности hello toounderstand веб-приложений.

## <a name="create-an-application-gateway-with-web-application-firewall"></a>Создание шлюза приложений с брандмауэром веб-приложения

Привет, следующая команда создает шлюза приложения с брандмауэр веб-приложения.

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
> Шлюзы приложений, созданных с помощью конфигурации брандмауэра hello основные веб-приложений, настроенных с CRS 3.0 для защиты.

## <a name="get-application-gateway-dns-name"></a>Получение DNS-имени шлюза приложений

После создания шлюза hello hello следующим шагом является tooconfigure hello внешнего интерфейса для обмена данными. Если вы используете общедоступный IP-адрес, шлюзу приложений требуется динамически назначаемое непонятное имя DNS. tooensure конечным пользователям возможность нажать шлюза приложения hello, запись CNAME может быть используется toopoint toohello общедоступную конечную точку шлюза приложения hello. [Настройка пользовательского имени домена в Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). tooconfigure запись CNAME, получить сведения о шлюза приложения hello и соответствующее IP или DNS-имя с помощью шлюза hello PublicIPAddress элемент toohello подключенных приложений. шлюз приложения Hello DNS-имя должно быть используется toocreate запись CNAME, какие точки hello двух web приложений toothis DNS-имя. Использование Hello записи A не рекомендуется, поскольку hello виртуального IP-адреса могут изменяться при перезагрузке шлюз приложений.

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

## <a name="next-steps"></a>Дальнейшие действия

Узнайте, как toocustomize WAF правила, посетив: [настроить правила брандмауэра приложения web через hello Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md).

[scenario]: ./media/application-gateway-web-application-firewall-cli/scenario.png
