---
title: "проблемы с подключением aaaTroubleshooting между виртуальными машинами Azure | Документы Microsoft"
description: "Узнайте, как tooTroubleshoot hello проблем с подключением между виртуальными машинами Azure."
services: virtual-network
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/25/2017
ms.author: genli
ms.openlocfilehash: ee0819178dcbee2bf529a495758e6c33f49e085e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-connectivity-problems-between-azure-vms"></a>Устранение проблем с подключением между виртуальными машинами Azure

Могут возникнуть проблемы с подключением между виртуальными машинами Azure. В этой статье приведены по устранению неполадок toohelp действия при решении этой проблемы. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="symptom"></a>Симптом

ВМ Azure не удается подключиться tooanother виртуальной Машине Azure.

## <a name="troubleshooting-guidance"></a>Рекомендации по устранению неполадок 

1. [Проверьте, если сетевой Адаптер настроен неправильно](#step-1-check-if-nic-is-misconfigured)
2. [Проверьте, если сетевой трафик блокируется NSG или UDR](#step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr)
3. [Проверьте, если сетевой трафик блокируется брандмауэром виртуальной Машины](#step-3-check-if-network-traffic-is-blocked-by-vm-firewall)
4. [Проверьте ли ВМ приложение или служба прослушивает порт hello](#step-4-check-whether-vm-app-or-service-is-listening-on-the-port)
5. [Проверьте, вызвана ли проблема hello SNAT](#step-5-check-whether-the-problem-is-caused-by-snat)
6. [Проверка ли трафик блокируется в списках управления доступом для hello классической виртуальной Машины](#step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm)
7. [Проверка ли hello конечная точка создана для hello классической виртуальной Машины](#step-7-check-whether-the-endpoint-is-created-for-the-classic-vm)
8. [Не удается tooconnect tooa ВМ сетевую папку](#step-8-unable-to-connect-to-a-vm-network-share)
9. [Подключения между Vnet](#step-9-inter-vnet-connectivity)

## <a name="troubleshooting-steps"></a>Действия по устранению неполадок

Выполните эти шаги tootroubleshoot hello проблему. Проверьте, устранена ли проблема hello после каждого шага. 

### <a name="step-1-check-if-nic-is-misconfigured"></a>Шаг 1: Проверьте, если сетевой Адаптер настроен неправильно

Выполните [как tooreset сетевой интерфейс для виртуальной Машины Windows Azure](../virtual-machines/windows/reset-network-interface.md). 

Если проблема hello возникает после изменения hello сетевого интерфейса (NIC), выполните следующие действия.

**Виртуальные машины Mulit-NIC**

1. Добавьте сетевой интерфейс.
2. Устранение проблем hello в hello неверный сетевой Адаптер или удалить неверный сетевой адаптер.  Затем readd hello сетевого адаптера.

Дополнительные сведения см. в разделе [tooor интерфейсы сети Добавить удалить из виртуальной машины](virtual-network-network-interface-vm.md).

**Виртуальные машины с одним сетевым интерфейсом** 

- [Повторное развертывание виртуальной машины Windows](../virtual-machines/windows/redeploy-to-new-node.md)
- [Повторное развертывание виртуальной машины Linux](../virtual-machines/linux/redeploy-to-new-node.md)

### <a name="step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr"></a>Шаг 2: Проверьте, если сетевой трафик блокируется NSG или UDR

Использовать [проверить поток сети наблюдателя IP](../network-watcher/network-watcher-ip-flow-verify-overview.md) и [NSG ведение журнала потока](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify при наличии группы безопасности сети или определяемые пользователем маршрута, который мешает трафику.

### <a name="step-3-check-if-network-traffic-is-blocked-by-vm-firewall"></a>Шаг 3: Проверьте, если сетевой трафик блокируется брандмауэром виртуальной Машины

Отключите брандмауэр hello и затем hello результата теста. Если hello проблему, проверьте параметры hello в брандмауэре hello и снова включите.

### <a name="step-4-check-whether-vm-app-or-service-is-listening-on-hello-port"></a>Шаг 4: Проверка ли ВМ приложение или служба прослушивает порт hello

Можно использовать один из следующих методов toocheck ли виртуальная машина приложение или служба прослушивает порт hello hello

- Выполните следующие команды toocheck ли сервер Здравствуй прослушивает этот порт hello.

**Виртуальные машины Windows**

    netstat –ano

**Виртуальные машины Linux**

    netstat -l

- Запустите hello **Telnet** на hello порт hello tootest tooitself ВМ. В случае сбоя проверки hello приложение или служба не toolisten настроенный порт hello.

### <a name="step-5-check-whether-hello-problem-is-caused-by-snat"></a>Шаг 5: Проверьте, вызвана ли проблема hello SNAT

В некоторых сценариях hello ВМ помещается за решение балансировки нагрузки, которое имеет зависимость ресурсов за пределами Azure. В этих сценариях при возникновении проблем временное подключение hello проблема может быть вызвана по [нехватку портов SNAT](../load-balancer/load-balancer-outbound-connections.md). проблема tooresolve hello, Создание виртуального IP-адреса (или ILPIP для классической) для каждой виртуальной Машины, балансировщиком нагрузки hello и защиту с NSG или списка управления Доступом. 

### <a name="step-6-check-whether-traffic-is-blocked-by-acls-for-hello-classic-vm"></a>Шаг 6: Проверка ли трафик блокируется в списках управления доступом для hello классической виртуальной Машины

Список управления Доступом предоставляет разрешения tooselectively возможность hello или запрещать трафик для конечной точки виртуальной машины. Дополнительные сведения см. в разделе [управление hello ACL в конечной точке](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).

### <a name="step-7-check-whether-hello-endpoint-is-created-for-hello-classic-vm"></a>Шаг 7: Проверка ли hello конечная точка создана для hello классической виртуальной Машины

Все виртуальные машины, созданные в Azure с помощью hello классической модели развертывания, могут автоматически взаимодействовать через канал частной сети с другими виртуальными машинами в hello, же облака службы или виртуальной сети. Тем не менее для компьютеров на других виртуальных сетей требуются конечные точки toodirect hello входящего сетевого трафика tooa виртуальной машины. Дополнительные сведения см. в разделе [как tooset настройке конечных точек](../virtual-machines/windows/classic/setup-endpoints.md).

### <a name="step-8-unable-tooconnect-tooa-vm-network-share"></a>Шаг 8: Не удается tooconnect tooa ВМ сетевую папку

Если не удается tooconnect tooa ВМ сетевую папку, hello проблема может вызываться недоступен сетевых адаптеров в hello виртуальной Машины. toodelete hello недоступен сетевых адаптеров см. в разделе [как toodelete hello недоступен сетевых адаптеров](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)

### <a name="step-9-inter-vnet-connectivity"></a>Шаг 9: Подключения между Vnet

Использовать [проверить поток сети наблюдателя IP](../network-watcher/network-watcher-ip-flow-verify-overview.md) и [NSG ведение журнала потока](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify при наличии группы безопасности сети или определяемые пользователем маршрута, который мешает трафику. Также можно проверить конфигурацию виртуальной сети внутри [здесь](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).

### <a name="need-help-contact-support"></a>Требуется помощь? Обратитесь в службу поддержки.
Если вы по-прежнему нужна помощь, [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget быстро устранить проблему.
