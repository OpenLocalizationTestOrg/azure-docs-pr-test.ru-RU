---
title: "Здравствуйте, toocreate aaaHow Nsg в классическом режиме с помощью Azure CLI | Документы Microsoft"
description: "Узнайте, как toocreate и развернуть Nsg в классическом режиме, с помощью hello Azure CLI"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: 17d98950-5fbb-4653-bef6-d822ab37541e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: eb78861e10a0dd950bb2c3783ee957d1cce55016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-nsgs-classic-in-hello-azure-cli"></a>Как toocreate Nsg (классической) для hello Azure CLI
[!INCLUDE [virtual-networks-create-nsg-selectors-classic-include](../../includes/virtual-networks-create-nsg-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

В этой статье рассматриваются hello классической модели развертывания. Вы также можете [создать Nsg в модели развертывания диспетчера ресурсов hello](virtual-networks-create-nsg-arm-cli.md).

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

приведенную ниже команду Azure CLI Образец Hello ожидать простой среде уже создан на основании hello сценарии выше. Требуется toorun hello команд, отображаемых в этом документе, вначале построить hello тестовой среды, [создания виртуальной сети](virtual-networks-create-vnet-classic-cli.md).

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a>Как toocreate hello NSG для подсети hello переднего плана
toocreate с именем NSG с именем **NSG-FrontEnd** на основании hello сценарии выше, выполните следующие шаги hello.

1. Если ранее не пользовались Azure CLI, см. раздел [Установка и настройка hello Azure CLI](../cli-install-nodejs.md) и следуйте инструкциям hello toohello точку, где выбирается учетная запись Azure и подписки.
2. Запустите hello  **`azure config mode`**  tooswitch tooclassic команда режим, как показано ниже.
   
        azure config mode asm
   
    Ожидаемые выходные данные:
   
        info:    New mode is asm
3. Запустите hello  **`azure network nsg create`**  toocreate команда NSG.
   
        azure network nsg create -l uswest -n NSG-FrontEnd
   
    Ожидаемые выходные данные:
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Name                            : NSG-FrontEnd
        data:    Location                        : West US
        data:    Security group rules:
        data:    Name                               Source IP           Source Port  Destination IP   Destination Port  Protocol  Type      Action  Prior
        ity  Default
        data:    ---------------------------------  ------------------  -----------  ---------------  ----------------  --------  --------  ------  -----
        ---  -------
        data:    ALLOW VNET OUTBOUND                VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Outbound  Allow   65000
             true   
        data:    ALLOW VNET INBOUND                 VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Inbound   Allow   65000
             true   
        data:    ALLOW AZURE LOAD BALANCER INBOUND  AZURE_LOADBALANCER  *            *                *                 *         Inbound   Allow   65001
             true   
        data:    ALLOW INTERNET OUTBOUND            *                   *            INTERNET         *                 *         Outbound  Allow   65001
             true   
        data:    DENY ALL OUTBOUND                  *                   *            *                *                 *         Outbound  Deny    65500
             true   
        data:    DENY ALL INBOUND                   *                   *            *                *                 *         Inbound   Deny    65500
             true   
        info:    network nsg create command OK
   
    Параметры
   
   * **-l (или --location)**. Регион Azure, где hello новой NSG будет создан. В нашем случае это *westus*.
   * **-n (или --name)**. Имя для hello новая NSG. В данном сценарии это *NSG-FrontEnd*.
4. Запустите hello  **`azure network nsg rule create`**  toocreate команда правило, разрешающее доступ tooport 3389 (RDP) из Интернета hello.
   
        azure network nsg rule create -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    Ожидаемые выходные данные:
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Name                            : rdp-rule
        data:    Source address prefix           : INTERNET
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 3389
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
   
    Параметры
   
   * **-a (или --nsg-name)**. Имя в какие hello будет создано правило NSG hello. В данном сценарии это *NSG-FrontEnd*.
   * **-n (или --name)**. Имя для нового правила hello. В нашем случае это *rdp-rule*.
   * **-c (или --action)**. Уровень доступа для правила hello (запретить или разрешить).
   * **-p (или --protocol)**. Протокол (Tcp, Udp или *) для правила hello.
   * **-r (или --type)**. Направление подключения (Inbound или Outbound).
   * **-y (или --priority)**. Приоритет для правила hello.
   * **-f (или --source-address-prefix)**. Префикс адреса источника в CIDR или использование тегов по умолчанию.
   * **-o (или --source-port-range)**. Исходный порт или диапазон портов.
   * **-e (или --destination-address-prefix)**. Префикс адреса назначения в CIDR или использование тегов по умолчанию.
   * **-u (или --destination-port-range)**. Конечный порт или диапазон портов.
5. Запустите hello  **`azure network nsg rule create`**  toocreate команда правило, разрешающее доступ tooport 80 (HTTP) из Интернета hello.
   
        azure network nsg rule create -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    Ожидаемые выходные данные:
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Name                            : web-rule
        data:    Source address prefix           : INTERNET
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 80
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 200
        info:    network nsg rule create command OK
6. Запустите hello  **`azure network nsg subnet add`**  команда toolink hello NSG toohello внешнего интерфейса подсети.
   
        azure network nsg subnet add -a NSG-FrontEnd --vnet-name TestVNet --subnet-name FrontEnd
   
    Ожидаемые выходные данные:
   
        info:    Executing command network nsg subnet add
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-FrontEnd"
        info:    network nsg subnet add command OK

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a>Hello toocreate NSG для hello обратно конечного подсети
toocreate с именем NSG с именем *NSG серверной* на основании hello сценарии выше, выполните следующие шаги hello.

1. Запустите hello  **`azure network nsg create`**  toocreate команда NSG.
   
        azure network nsg create -l uswest -n NSG-BackEnd
   
    Ожидаемые выходные данные:
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Name                            : NSG-BackEnd
        data:    Location                        : West US
        data:    Security group rules:
        data:    Name                               Source IP           Source Port  Destination IP   Destination Port  Protocol  Type      Action  Prior
        ity  Default
        data:    ---------------------------------  ------------------  -----------  ---------------  ----------------  --------  --------  ------  -----
        ---  -------
        data:    ALLOW VNET OUTBOUND                VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Outbound  Allow   65000
             true   
        data:    ALLOW VNET INBOUND                 VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Inbound   Allow   65000
             true   
        data:    ALLOW AZURE LOAD BALANCER INBOUND  AZURE_LOADBALANCER  *            *                *                 *         Inbound   Allow   65001
             true   
        data:    ALLOW INTERNET OUTBOUND            *                   *            INTERNET         *                 *         Outbound  Allow   65001
             true   
        data:    DENY ALL OUTBOUND                  *                   *            *                *                 *         Outbound  Deny    65500
             true   
        data:    DENY ALL INBOUND                   *                   *            *                *                 *         Inbound   Deny    65500
             true   
        info:    network nsg create command OK
   
    Параметры
   
   * **-l (или --location)**. Регион Azure, где hello новой NSG будет создан. В нашем случае это *westus*.
   * **-n (или --name)**. Имя для hello новая NSG. В данном сценарии это *NSG-FrontEnd*.
2. Запустите hello  **`azure network nsg rule create`**  toocreate команда правило, разрешающее доступ tooport 1433 (SQL) из подсети hello переднего плана.
   
        azure network nsg rule create -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    Ожидаемые выходные данные:
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Name                            : sql-rule
        data:    Source address prefix           : 192.168.1.0/24
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 1433
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
3. Запустите hello  **`azure network nsg rule create`**  toocreate команда правило, запрещающее доступ toohello Интернета.
   
        azure network nsg rule create -a NSG-BackEnd -n web-rule -c Deny -p Tcp -r Outbound -y 200 -f * -o * -e Internet -u 80
   
    Ожидаемые выходные данные:
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Name                            : web-rule
        data:    Source address prefix           : *
        data:    Source Port                     : *
        data:    Destination address prefix      : INTERNET
        data:    Destination Port                : 80
        data:    Protocol                        : TCP
        data:    Type                            : Outbound
        data:    Action                          : Deny
        data:    Priority                        : 200
        info:    network nsg rule create command OK
4. Запустите hello  **`azure network nsg subnet add`**  toohello NSG hello toolink обратно завершить подсети команды.
   
        azure network nsg subnet add -a NSG-BackEnd --vnet-name TestVNet --subnet-name BackEnd
   
    Ожидаемые выходные данные:
   
        info:    Executing command network nsg subnet add
        info:    Looking up hello network security group "NSG-BackEndX"
        info:    Looking up hello subnet "BackEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-BackEndX"
        info:    network nsg subnet add command OK

