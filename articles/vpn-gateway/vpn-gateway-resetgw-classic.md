---
title: "Сброс tooreestablish шлюза Azure VPN туннелей IPsec | Документы Microsoft"
description: "В этой статье описывается сброс вашей туннелей IPsec шлюза VPN Azure tooreestablish. статья Hello относится tooVPN шлюзов в классическом hello и модели развертывания диспетчера ресурсов hello."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 79d77cb8-d175-4273-93ac-712d7d45b1fe
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: cherylmc
ms.openlocfilehash: 84dd741f0bebd6b18cb235216a68a88da5fe17b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="reset-a-vpn-gateway"></a>Сброс VPN-шлюза

Сброс настроек VPN-шлюза Azure полезен при потере распределенного VPN-подключения в одном или нескольких VPN-туннелях типа "сеть-сеть". В этой ситуации локального VPN-устройств являются все работает правильно, но не удается tooestablish туннелей IPsec со шлюзами Azure VPN hello. Эта статья поможет вам сбросить VPN-шлюз.

### <a name="what-happens-during-a-reset"></a>Что происходит при сбросе?

VPN-шлюз состоит из двух экземпляров виртуальной машины (активного и резервного) с соответствующими конфигурациями. При сбросе hello шлюза будет перезагружен шлюза hello и затем повторно применяет hello между организациями tooit конфигурации. шлюз Hello сохраняет hello общедоступный IP-адрес, который уже имеет. Это означает, что не нужно конфигурация маршрутизатора tooupdate hello VPN с новый общедоступный IP-адрес для шлюза Azure VPN.

При использовании функции hello команда tooreset hello шлюза hello текущий активный экземпляр шлюза Azure VPN hello перезагружен немедленно. При отработке отказа hello из hello активный экземпляр (перезагружается), резервный экземпляр toohello будет краткий промежуток. Разрыв Hello должно быть меньше одной минуты.

Если подключение hello не восстанавливается после первой перезагрузки hello, проблема hello же команда снова tooreboot hello второй экземпляр виртуальной Машины (hello новый active шлюз). Если дважды выполнить перезагрузку hello запрошенный tooback назад, будет немного больше времени периода перезагружаются где оба экземпляра виртуальной Машины (активные и резервные). Это приведет к более длинная пауза на VPN-подключение hello вверх too2 too4 минут после перезагрузки hello toocomplete виртуальных машин.

После двух перезагрузок Если по-прежнему возникают проблемы с подключением между организациями, создайте запрос в службу поддержки из hello портал Azure.

## <a name="before"></a>Перед началом работы

Перед сбросом шлюз проверьте hello ключевые элементы, перечисленные ниже, для каждого туннеля VPN IPsec-сайтами (S2S). Любые различия в элементах hello приведет к disconnect hello туннелей S2S VPN. Проверка и исправление hello конфигурации для локальной и VPN-шлюзы Azure позволяет избежать ненужных после перезагрузки и нарушений в работе для hello другие соединения работу на шлюзах hello.

Проверьте hello следующих элементов перед сбросом шлюза.

* Hello Интернета IP адресов (VIP) для обоих hello VPN-шлюз Azure и hello локального VPN-шлюз настроены правильно в обе hello Azure и hello локального VPN политики.
* Hello общий ключ должен hello же на Azure и локальных шлюзах VPN.
* Если применить конкретной конфигурации IPsec/IKE, такие как гарантировать шифрования, хэширования алгоритмы и PFS (включить режим PFS), оба hello Azure и локальным VPN-шлюзов hello и те же конфигурации.

## <a name="portal"></a>Портал Azure

Вы можете сбросить шлюз VPN диспетчера ресурсов с помощью hello портал Azure. Tooreset классический шлюза, в статье hello [PowerShell](#resetclassic) действия.

### <a name="resource-manager-deployment-model"></a>Модель развертывания диспетчера ресурсов

1. Откройте hello [портал Azure](https://portal.azure.com) и шлюз виртуальной сети toohello диспетчера ресурсов, что требуется tooreset перехода.
2. В колонке hello для hello шлюза виртуальной сети нажмите кнопку «Сброс».

  ![Колонка сброса VPN-шлюза](./media/vpn-gateway-howto-reset-gateway/reset-vpn-gateway-portal.png)
3. На hello восстановить колонку, нажмите hello **Сброс** кнопки.

## <a name="ps"></a>PowerShell

### <a name="resource-manager-deployment-model"></a>Модель развертывания диспетчера ресурсов

Здравствуйте командлет Сброс шлюза является **AzureRmVirtualNetworkGateway Сброс**. Прежде чем выполнять сброс, убедитесь, что у вас есть последняя версия hello hello [командлеты PowerShell диспетчера ресурсов](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0). Hello следующий пример сбрасывает шлюз виртуальной сети с именем VNet1GW в группе ресурсов TestRG1 hello:

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroup TestRG1
Reset-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw
```

Результат:

При получении возвращают результат, можно предположить, был успешно сброшен hello шлюза. Однако нет ничего hello возвращаемого результата, который явно указывает, был успешно сброшен, hello. Если требуется, чтобы toolook поближе toosee журнал hello точно шлюза hello сбрасывать произошла, эти сведения можно просмотреть в hello [портал Azure](https://portal.azure.com). На портале hello перейдите слишком**«GatewayName» -> исправности ресурсов**.

### <a name="resetclassic"></a>Классическая модель развертывания

Здравствуйте командлет Сброс шлюза является **AzureVNetGateway Сброс**. Прежде чем выполнять сброс, убедитесь, что у вас есть последняя версия hello hello [командлеты PowerShell для службы управления (SM)](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0). Hello следующий пример сбрасывает hello шлюза для виртуальной сети с именем «ContosoVNet»:

```powershell
Reset-AzureVNetGateway –VnetName “ContosoVNet”
```

Результат:

```powershell
Error          :
HttpStatusCode : OK
Id             : f1600632-c819-4b2f-ac0e-f4126bec1ff8
Status         : Successful
RequestId      : 9ca273de2c4d01e986480ce1ffa4d6d9
StatusCode     : OK
```

## <a name="cli"></a>Интерфейс командной строки Azure

шлюз tooreset hello, используйте hello [сброс виртуальной сети — шлюз сети az](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset) команды. Hello следующий пример сбрасывает шлюз виртуальной сети с именем VNet5GW в группе ресурсов TestRG5 hello:

```azurecli
az network vnet-gateway reset -n VNet5GW -g TestRG5
```

Результат:

При получении возвращают результат, можно предположить, был успешно сброшен hello шлюза. Однако нет ничего hello возвращаемого результата, который явно указывает, был успешно сброшен, hello. Если требуется, чтобы toolook поближе toosee журнал hello точно шлюза hello сбрасывать произошла, эти сведения можно просмотреть в hello [портал Azure](https://portal.azure.com). На портале hello перейдите слишком**«GatewayName» -> исправности ресурсов**.
