---
title: "Здравствуйте, aaaCreate виртуальной сети с помощью Azure CLI 1.0 | Документы Microsoft"
description: "Узнайте, как toocreate виртуальной сети с помощью hello Azure CLI 1.0 | Диспетчер ресурсов."
services: virtual-network
documentationcenter: 
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.openlocfilehash: f48a8b23a5994164b71c9b51ee8a6810d17f9392
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-hello-azure-cli"></a>Создание виртуальной сети с помощью hello Azure CLI

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

Azure предоставляет две модели развертывания: с помощью Azure Resource Manager и классическую. Корпорация Майкрософт рекомендует создать ресурсы с помощью модели развертывания диспетчера ресурсов hello. Дополнительные сведения о toolearn hello различий между моделями hello двух чтения hello [модели развертывания Azure понять](../azure-resource-manager/resource-manager-deployment-model.md) статьи.

## <a name="cli-versions-toocomplete-hello-task"></a>Задача hello toocomplete версии CLI
Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.

- [Azure CLI 2.0](virtual-networks-create-vnet-arm-cli.md) -нашей нового поколения CLI для модели развертывания hello ресурсов управления
- [Azure CLI 1.0](#create-a-virtual-network) — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)

 
[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a>Создать виртуальную сеть

в виртуальной сети с помощью toocreate hello Azure CLI, полный hello, следующие шаги:

1. Установка и настройка hello Azure CLI, hello следующие шаги в hello [Установка и настройка hello Azure CLI](../cli-install-nodejs.md) статьи.

2. Создайте виртуальную сеть и подсеть.

    ```azurecli
    azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
    ```

    Ожидаемые выходные данные:
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK

    Используемые параметры:

   * **--vnet**. Имя создания toobe виртуальной сети hello. В данном сценарии это *TestVNet*
   * **-e (или --address-space)**. Адресное пространство виртуальной сети. В данном сценарии это *192.168.0.0*
   * **-i (или -cidr)**. Маска подсети в формате CIDR. В данном сценарии это *16*.
   * **-n (или --subnet-name**). Имя первой подсети hello. В данном сценарии это *FrontEnd*.
   * **-p (или --subnet-start-ip)**. Начальный IP-адрес для подсети или адресное пространство подсети. В нашем сценарии это *192.168.1.0*.
   * **-r (или --subnet-cidr)**. Маска подсети в формате CIDR для подсети. В данном сценарии это *24*.
   * **-l (или --location)**. Регион Azure, где создается hello виртуальной сети. В данном сценарии это *Central US*.

3. Создайте подсеть.

    ```azurecli
    azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
    ```
   
    Ожидаемые выходные данные:

            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK

    Используемые параметры:

   * **-t (или --vnet-name**. Имя виртуальной сети, где будут создаваться подсети hello hello. В данном сценарии это *TestVNet*.
   * **-n (или --name)**. Имя новой подсети hello. В нашем сценарии это *BackEnd*.
   * **-a (или --address-prefix)**. Блок подсети CIDR. В данном сценарии это *192.168.2.0/24*.
   
4. свойства hello tooview hello новой виртуальной сети:

    ```azurecli
    azure network vnet show
    ```
   
    Ожидаемые выходные данные:
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

## <a name="next-steps"></a>Дальнейшие действия

Узнайте, как tooconnect:

- Виртуальная сеть виртуальной машины (VM) tooa, считывая hello [создания виртуальной Машины Linux](../virtual-machines/linux/quick-create-cli.md) статьи. Вместо создания виртуальной сети и подсети в шагах hello hello статей, можно выбрать существующей виртуальной сети и подсети tooconnect для виртуальной Машины.
- Здравствуйте, считывая hello виртуальных сетей в виртуальной сети tooother [подключение виртуальных сетей](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) статьи.
- tooan Hello виртуальной сети в локальной сети с помощью виртуальной частной сети сеть сеть (VPN) или канал ExpressRoute. Дополнительные сведения в разделе hello [подключения локальной сети tooan виртуальной сети с помощью VPN сайтами](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) и [связывание виртуальной сети tooan канал ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).
