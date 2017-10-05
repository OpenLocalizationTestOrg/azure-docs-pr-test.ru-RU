---
title: "Устранение проблем с подключением между виртуальными машинами Azure | Документация Майкрософт"
description: "Сведения об устранении проблем с подключениями между виртуальными машинами Azure."
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
ms.openlocfilehash: fd0f25c07cb3f385d3e8480ce1e33dec1ae0a214
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshooting-connectivity-problems-between-azure-vms"></a>Устранение проблем с подключением между виртуальными машинами Azure

Могут возникнуть проблемы с подключением между виртуальными машинами Azure. В этой статье приведены действия по устранению этой проблемы. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="symptom"></a>Симптом

ВМ Azure не удается подключиться к другой виртуальной Машине Azure.

## <a name="troubleshooting-guidance"></a>Рекомендации по устранению неполадок 

1. [Проверьте, если сетевой Адаптер настроен неправильно](#step-1-check-if-nic-is-misconfigured)
2. [Проверьте, если сетевой трафик блокируется NSG или UDR](#step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr)
3. [Проверьте, если сетевой трафик блокируется брандмауэром виртуальной Машины](#step-3-check-if-network-traffic-is-blocked-by-vm-firewall)
4. [Проверьте, прослушивается ли порт приложением или службой виртуальной машины](#step-4-check-whether-vm-app-or-service-is-listening-on-the-port).
5. [Проверьте, не вызвана ли проблема SNAT](#step-5-check-whether-the-problem-is-caused-by-snat).
6. [Проверьте, блокируется ли трафик классической виртуальной машины списками управления доступом (ACL)](#step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm).
7. [Проверьте, создана ли конечная точка классической виртуальной машины](#step-7-check-whether-the-endpoint-is-created-for-the-classic-vm).
8. [Не удается подключиться к общей сетевой папке виртуальной Машины](#step-8-unable-to-connect-to-a-vm-network-share)
9. [Подключения между Vnet](#step-9-inter-vnet-connectivity)

## <a name="troubleshooting-steps"></a>Действия по устранению неполадок

Чтобы устранить проблему, выполните действия ниже, Проверьте, устранена ли проблема после каждого шага. 

### <a name="step-1-check-if-nic-is-misconfigured"></a>Шаг 1: Проверьте, если сетевой Адаптер настроен неправильно

Выполните [сброс сетевого интерфейса для виртуальной Машины Windows Azure](../virtual-machines/windows/reset-network-interface.md). 

Если изменение конфигурации сетевого интерфейса не решило проблему, выполните указанные ниже действия.

**Виртуальные машины Mulit-NIC**

1. Добавьте сетевой интерфейс.
2. Устраните проблемы в неверный сетевой Адаптер или удалить неверный сетевой адаптер.  Затем readd сетевого адаптера.

Дополнительные сведения см. в статье [Добавление или удаление сетевых интерфейсов виртуальных машин](virtual-network-network-interface-vm.md).

**Виртуальные машины с одним сетевым интерфейсом** 

- [Повторное развертывание виртуальной машины Windows](../virtual-machines/windows/redeploy-to-new-node.md)
- [Повторное развертывание виртуальной машины Linux](../virtual-machines/linux/redeploy-to-new-node.md)

### <a name="step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr"></a>Шаг 2: Проверьте, если сетевой трафик блокируется NSG или UDR

Использовать [проверить поток сети наблюдателя IP](../network-watcher/network-watcher-ip-flow-verify-overview.md) и [NSG ведение журнала потока](../network-watcher/network-watcher-nsg-flow-logging-overview.md) для идентификации при наличии группы безопасности сети или определяемые пользователем маршрута, который мешает трафику.

### <a name="step-3-check-if-network-traffic-is-blocked-by-vm-firewall"></a>Шаг 3: Проверьте, если сетевой трафик блокируется брандмауэром виртуальной Машины

Отключите брандмауэр и проверьте результат. Если проблема будет устранена, проверьте параметры брандмауэра и повторно включить.

### <a name="step-4-check-whether-vm-app-or-service-is-listening-on-the-port"></a>Шаг 4. Проверка прослушивания порта приложением или службой виртуальной машины

Можно использовать один из следующих методов для проверки ли виртуальная машина приложение или служба прослушивает порт

- Чтобы проверить, прослушивается ли порт сервером, выполните команды ниже.

**Виртуальные машины Windows**

    netstat –ano

**Виртуальные машины Linux**

    netstat -l

- Запустите **Telnet** команду на виртуальной Машине для тестирования порт на самого себя. Если тест не пройден, приложение или служба не настроен для прослушивания порта.

### <a name="step-5-check-whether-the-problem-is-caused-by-snat"></a>Шаг 5. Проверка проблемы из-за SNAT

В некоторых сценариях ВМ помещается за решение балансировки нагрузки, которое имеет зависимость ресурсов за пределами Azure. Проблемы с промежуточными соединениями в этих сценариях могут возникать из-за [нехватки портов SNAT](../load-balancer/load-balancer-outbound-connections.md). Чтобы устранить проблему, создайте виртуальный IP-адрес (или ILPIP для классической) для каждой виртуальной Машины, в которой находится за подсистемой балансировки нагрузки и защиты с NSG или ACL. 

### <a name="step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm"></a>Шаг 6. Проверка блокировки трафика классической виртуальной машины списками управления доступом

Список ACL дает возможность выборочно разрешать или блокировать трафик для конечной точки виртуальной машины. Дополнительные сведения см. в разделе [Управление ACL для конечной точки](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).

### <a name="step-7-check-whether-the-endpoint-is-created-for-the-classic-vm"></a>Шаг 7. Проверка наличия конечной точки классической виртуальной машины

Все виртуальные машины, созданные в Azure с помощью классической модели развертывания могут автоматически взаимодействовать через канал частной сети с другими виртуальными машинами в той же облачной службе или виртуальной сети. Однако компьютерам в других виртуальных сетях требуются конечные точки, чтобы направить входящий трафик к виртуальной машине. Дополнительные сведения см. в статье [Настройка конечных точек в классической виртуальной машине Windows в Azure](../virtual-machines/windows/classic/setup-endpoints.md).

### <a name="step-8-unable-to-connect-to-a-vm-network-share"></a>Шаг 8: Не удается подключиться к общей сетевой папке виртуальной Машины

Если не удается подключиться к общей сетевой папке виртуальной Машины, проблема может вызываться недоступен сетевых адаптеров в виртуальной Машине. Сведения об удалении недоступных сетевых интерфейсов см. в [этом разделе](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics).

### <a name="step-9-inter-vnet-connectivity"></a>Шаг 9: Подключения между Vnet

Использовать [проверить поток сети наблюдателя IP](../network-watcher/network-watcher-ip-flow-verify-overview.md) и [NSG ведение журнала потока](../network-watcher/network-watcher-nsg-flow-logging-overview.md) для идентификации при наличии группы безопасности сети или определяемые пользователем маршрута, который мешает трафику. Также можно проверить конфигурацию виртуальной сети внутри [здесь](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).

### <a name="need-help-contact-support"></a>Требуется помощь? Обратитесь в службу поддержки.
Если вам все еще нужна помощь, [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade), которая поможет быстро устранить проблему.