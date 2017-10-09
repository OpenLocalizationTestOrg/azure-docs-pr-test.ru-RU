---
title: "aaaHosting нескольких сайтов на использование шлюза приложений Azure | Документы Microsoft"
description: "Эта страница обзор поддержки нескольких сайтов шлюза приложения hello."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: 
ms.assetid: 49993fd2-87e5-4a66-b386-8d22056a616d
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: amsriva
ms.openlocfilehash: 4ab6faa97f1891d7525affdaa36463681bf99e9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-multiple-site-hosting"></a>Размещение нескольких сайтов с помощью шлюза приложений

Размещение нескольких сайтов позволяет tooconfigure более одного веб-приложения на hello одного экземпляра шлюза приложения. Эта функция позволяет tooconfigure эффективнее топологию развертывания путем добавления шлюза приложений tooone too20 веб-сайтов. Каждый сайт может направляться tooits владельцем внутренний пул. В следующем примере hello шлюз приложений обслуживает трафик для contoso.com и fabrikam.com из двух серверных пулов, называется ContosoServerPool и FabrikamServerPool.

![imageURLroute](./media/application-gateway-multi-site-overview/multisite.png)

> [!IMPORTANT]
> Правила обрабатываются в порядке hello, в котором они перечислены в портале hello. Это весьма рекомендуемые к использованию tooconfigure несколькими сайтами прослушивателей первый предыдущего tooconfiguring основные прослушивателя.  Это позволит гарантировать завершение этого трафика получает перенаправленное toohello самому началу. Если базовый прослушиватель стоит первым в списке и совпадает с входящим запросом, он будет обрабатываться прослушивателем.

Запросы для http://contoso.com перенаправленное tooContosoServerPool, и http://fabrikam.com это перенаправленное tooFabrikamServerPool.

Аналогичным образом две поддомены одного родительского домена может быть размещена на приветствия hello развертывания шлюза того же приложения. К примерам использования поддоменов можно отнести http://blog.contoso.com и http://app.contoso.com, размещенные в одном развернутом шлюзе приложений.

## <a name="host-headers-and-server-name-indication-sni"></a>Заголовки узлов и указание имени сервера (SNI)

Существует три распространенных механизмов для включения нескольких узел размещения на hello же инфраструктуры.

1. Размещение нескольких веб-приложений с уникальным IP-адресом у каждого из них.
2. Имя узла используйте, toohost несколько веб-приложений на hello же IP-адрес.
3. Использование разных портов toohost несколько веб-приложений на hello же IP-адрес.

В настоящее время шлюз приложений получает один общедоступный IP-адрес, на котором он прослушивает трафик. Поэтому поддержка нескольких приложений, каждое из которых имеет собственный IP-адрес, сейчас не обеспечивается. Шлюз приложений поддерживает размещение нескольких приложений каждого прослушивание по различным портам, но этот сценарий требуют трафик tooaccept приложения hello нестандартные порты и часто не является требуемой конфигурацией. Шлюз приложений использует протокол HTTP 1.1 toohost заголовки узлов более одного веб-сайта на hello же общедоступный IP-адрес и порт. Hello сайтов, размещенных на использование шлюза приложений также возможность поддержки разгрузки SSL с расширением TLS Указание имени сервера (SNI). Это означает, что этой hello клиента браузера и внутреннего веб-фермы должны поддерживать HTTP/1.1 и TLS модуля определению в RFC 6066.

## <a name="listener-configuration-element"></a>Элемент конфигурации прослушивателя

Существующие HTTPListener которой элемент конфигурации усиленной toosupport узла имя сервера имя указывает элементы и, используемой приложения шлюза tooroute трафика tooappropriate внутренний пул. Hello следующий пример кода представляет фрагмент кода hello HTTP-прослушивателей элемента из файла шаблона.

```json
"httpListeners": [
    {
        "name": "appGatewayHttpsListener1",
        "properties": {
            "FrontendIPConfiguration": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendIPConfigurations/DefaultFrontendPublicIP"
            },
            "FrontendPort": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendPorts/appGatewayFrontendPort443'"
            },
            "Protocol": "Https",
            "SslCertificate": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/sslCertificates/appGatewaySslCert1'"
            },
            "HostName": "contoso.com",
            "RequireServerNameIndication": "true"
        }
    },
    {
        "name": "appGatewayHttpListener2",
        "properties": {
            "FrontendIPConfiguration": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendIPConfigurations/appGatewayFrontendIP'"
            },
            "FrontendPort": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendPorts/appGatewayFrontendPort80'"
            },
            "Protocol": "Http",
            "HostName": "fabrikam.com",
            "RequireServerNameIndication": "false"
        }
    }
],
```

Вы можете посетить [шаблона диспетчера ресурсов с помощью нескольких размещения сайта](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) для процесса tooend на основе шаблона развертывания.

## <a name="routing-rule"></a>Правило маршрутизации

Нет изменений в правила маршрутизации hello. Здравствуйте, правило маршрутизации «Basic» следует продолжить toobe выбран tootie hello подходящий сайт прослушивателя toohello соответствующего пула адресов серверной части.

```json
"requestRoutingRules": [
{
    "name": "<ruleName1>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/httpListeners/appGatewayHttpsListener1')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/ContosoServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

},
{
    "name": "<ruleName2>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/httpListeners/appGatewayHttpListener2')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/FabrikamServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

}
]
```

## <a name="next-steps"></a>Дальнейшие действия

После обучения о размещении нескольких сайта перейдите слишком[создания шлюза приложения с помощью нескольких размещения сайта](application-gateway-create-multisite-azureresourcemanager-powershell.md) toocreate шлюза приложения с возможностью toosupport более одного веб-приложения.

