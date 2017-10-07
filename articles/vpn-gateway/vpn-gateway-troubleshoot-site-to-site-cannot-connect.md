---
title: "aaaTroubleshoot Azure VPN-подключение с сайт сайт, который не может подключиться | Документы Microsoft"
description: "Узнайте, как tootroubleshoot сеть сеть VPN-подключения, внезапно перестает работать и будет невозможно."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/21/2017
ms.author: genli
ms.openlocfilehash: 632c75bfcfb93a532eeead2855d43e6614569a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-an-azure-site-to-site-vpn-connection-cannot-connect-and-stops-working"></a>Устранение проблемы подключения VPN типа "сеть — сеть" Azure

После настройки VPN-подключения сеть сеть между локальной сетью и виртуальной сети Azure hello VPN-подключение неожиданно перестанет работать и будет невозможно. В этой статье приведены по устранению неполадок toohelp действия при решении этой проблемы. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a>Действия по устранению неполадок

tooresolve hello проблему, сначала воспользуйтесь слишком[сброса hello VPN-шлюз Azure](vpn-gateway-resetgw-classic.md) и сбросить hello туннеля VPN-устройство локальной hello. При повторном возникновении проблемы hello, выполните эти шаги tooidentify hello причины проблемы hello.

### <a name="prerequisite-step"></a>Предварительные действия

Проверка типа hello hello шлюза Azure VPN.

1. Go toohello [портал Azure](https://portal.azure.com).

2. Проверьте hello **Обзор** страницы приветствия VPN-шлюза hello сведений о типе.
    
    ![Общие сведения о шлюзе hello](media\vpn-gateway-troubleshoot-site-to-site-cannot-connect\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a>Шаг 1. Проверьте, выполняется ли проверка hello локального VPN-устройства

1. Узнайте, используете ли вы [проверенную версию VPN-устройства и операционной системы](vpn-gateway-about-vpn-devices.md#devicetable). Если устройство hello не проверенные устройства VPN, toosee изготовителя устройства hello toocontact может потребоваться при наличии проблемы совместимости.

2. Убедитесь в том, что это устройство VPN hello настроен правильно. Дополнительные сведения см. на странице об [изменении примеров конфигурации устройств](/vpn-gateway-about-vpn-devices.md#editing).

### <a name="step-2-verify-hello-shared-key"></a>Шаг 2. Проверка общего ключа hello

Сравните hello общий ключ для hello локального VPN устройства toohello виртуальной сети VPN Azure toomake убедиться, что hello ключи совпадают. 

tooview hello общий ключ для hello Azure VPN-подключения, используйте один из следующих методов hello:

**Портал Azure**

1. Go toohello шлюза сеть сеть через VPN, созданный.

2. В hello **параметры** щелкните **общий ключ**.
    
    ![Общий ключ](media/vpn-gateway-troubleshoot-site-to-site-cannot-connect/sharedkey.png)

**Azure PowerShell**

Для модели развертывания диспетчера ресурсов Azure hello:

    Get-AzureRmVirtualNetworkGatewayConnectionSharedKey -Name <Connection name> -ResourceGroupName <Resource group name>

Для hello классической модели развертывания:

    Get-AzureVNetGatewayKey -VNetName -LocalNetworkSiteName

### <a name="step-3-verify-hello-vpn-peer-ips"></a>Шаг 3. Проверьте одноранговых VPN hello IP-адресов

-   Здравствуйте, определение IP в hello **шлюза локальной сети** объекта в Azure должны совпадать IP-адрес устройства в локальной среде hello.
-   Hello определения IP шлюз Azure, установленного на hello локального устройства должен совпадать IP-адреса hello Azure шлюза.

### <a name="step-4-check-udr-and-nsgs-on-hello-gateway-subnet"></a>Шаг 4. Проверьте UDR и Nsg из подсети шлюза hello

Поиск и удаление определяемых пользователем маршрутизации (UDR) или группы безопасности сети (Nsg) в подсети шлюза hello затем hello результат теста. Если hello проблема не будет устранена, проверьте параметры hello, примененные UDR или NSG.

### <a name="step-5-check-hello-on-premises-vpn-device-external-interface-address"></a>Шаг 5. Проверка hello локальный адрес внешнего интерфейса VPN-устройства

- Если hello из Интернета IP-адрес устройства VPN hello включается в hello **локальной сети** определение в Azure, могут возникать нерегулярные отключения.
- Hello внешнего интерфейса устройства должны находиться непосредственно в Интернет hello. Должна существовать без преобразования сетевых адресов или брандмауэра между hello Интернета и устройством hello.
- tooconfigure брандмауэра кластеризации toohave виртуального IP-адреса, необходимо разорвать кластера hello и предоставлять hello VPN-устройством напрямую tooa открытый интерфейс, hello шлюза может взаимодействовать с.

### <a name="step-6-verify-that-hello-subnets-match-exactly-azure-policy-based-gateways"></a>Шаг 6. Убедитесь, что подсети hello точно соответствуют (шлюзы Azure на основе политики)

-   Проверьте соответствие подсети hello точно между hello виртуальной сети Azure и локальной определения для hello виртуальной сети Azure.
-   Проверьте соответствие подсети hello точно между hello **шлюза локальной сети** и локальными определения для hello в локальной сети.

### <a name="step-7-verify-hello-azure-gateway-health-probe"></a>Шаг 7. Проверьте проверки работоспособности hello шлюз Azure

1. Go toohello [проверки работоспособности](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).

2. Пролистайте hello предупреждение сертификата.
3. Если ответ получен, считается исправной hello VPN-шлюз. Если ответ не получен, hello шлюза не может быть работоспособное или NSG из подсети шлюза hello является причиной hello. После текста Hello приведен образец ответа:

    &lt;?xml version="1.0"?> <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">Основной экземпляр: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6</string&gt;

### <a name="step-8-check-whether-hello-on-premises-vpn-device-has-hello-perfect-forward-secrecy-feature-enabled"></a>Шаг 8. Проверьте ли hello из локального VPN-устройства включена hello безопасной пересылки

функция безопасной пересылки Hello может вызвать проблемы разрыва соединения. Если VPN-устройства hello безопасной пересылки включен, отключите функцию hello. Затем обновите политику IPsec шлюза VPN hello.

## <a name="next-steps"></a>Дальнейшие действия

-   [Настройка виртуальной сети tooa подключения сеть сеть](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
-   [Настройка политики IPsec/IKE для VPN-подключений типа "сеть — сеть" или "виртуальная сеть — виртуальная сеть"](vpn-gateway-ipsecikepolicy-rm-powershell.md)
