---
title: "aaaConfigure частных IP-адресов для виртуальных машин (обычная) — Azure CLI 1.0 | Документы Microsoft"
description: "Узнайте, как tooconfigure частных IP-адресов для виртуальных машин (классические) с помощью hello Azure командной строки (CLI) 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17386acf-c708-4103-9b22-ff9bf04b778d
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 417a57181bcf5c2e6101bf3bdf63fc94ebc99df5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-cli-10"></a>Настройка частного IP-адреса для виртуальной машины (классические) с помощью hello Azure CLI 1.0

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

В этой статье рассматриваются hello классической модели развертывания. Вы также можете [управление статический частный IP-адрес в модели развертывания диспетчера ресурсов hello](virtual-networks-static-private-ip-arm-cli.md).

приведенную ниже команду Azure CLI Образец Hello ожидать простой среде уже создан. Если требуется toorun hello команд, отображаемых в этом документе, вначале построить hello тестовой среды, описанные в [создании виртуальной сети](virtual-networks-create-vnet-classic-cli.md).

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a>Как toospecify статических частных IP-адресов при создании виртуальной Машины
Новая виртуальная машина с именем toocreate *DNS01* в новой облачной службы с именем *TestService* на основании hello сценарии выше, выполните следующие действия:

1. Если ранее не пользовались Azure CLI, см. раздел [Установка и настройка hello Azure CLI](../cli-install-nodejs.md) и следуйте инструкциям hello toohello точку, где выбирается учетная запись Azure и подписки.
2. Запустите hello **создания службы azure** команды toocreate hello облачной службы.
   
        azure service create TestService --location uscentral
   
    Ожидаемые выходные данные:
   
        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name TestService
        info:    service create command OK
3. Запустите hello **azure создать ВМ** команда toocreate hello виртуальной Машины. Обратите внимание, значение hello статический частный IP-адрес. Список Hello отображаться после вывода hello объясняется hello параметров, используемых.
   
        azure vm create -l centralus -n DNS01 -w TestVNet -S "192.168.1.101" TestService bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 adminuser AdminP@ssw0rd
   
    Ожидаемые выходные данные:
   
        info:    Executing command vm create
        warn:    --vm-size has not been specified. Defaulting too"Small".
        info:    Looking up image bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2
        info:    Looking up virtual network
        info:    Looking up cloud service
        warn:    --location option will be ignored
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Retrieving storage accounts
        info:    Creating VM
        info:    OK
        info:    vm create command OK
   
   * **-l (или --location)**. Регион Azure, где будут создаваться hello виртуальной Машины. В данном случае это — *centralus*.
   * **-n (или --vm-name)**. Имя создания toobe ВМ hello.
   * **-w (или --virtual-network-name)**. Имя виртуальной сети, где будут создаваться hello ВМ hello. 
   * **-S (или --static-ip)**. Статический частный IP-адрес для hello виртуальной Машины.
   * **TestService**. Имя облачной службы hello, где будут создаваться hello виртуальной Машины.
   * **bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2.** Изображение, используемое toocreate hello виртуальной Машины.
   * **adminuser**. Локальный администратор для виртуальной Машины Windows hello.
   * **AdminP@ssw0rd**. Пароль локального администратора для виртуальной Машины Windows hello.

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a>Как статических частных IP-tooretrieve адресов сведения для виртуальной Машины
tooview hello статических частного IP-адреса сведения для hello создания ВМ с hello-сценарий, приведенный выше, запустите следующую команду Azure CLI hello и просмотрите значение hello *StaticIP сети*:

    azure vm static-ip show DNS01

Ожидаемые выходные данные:

    info:    Executing command vm static-ip show
    info:    Getting virtual machines
    data:    Network StaticIP "192.168.1.101"
    info:    vm static-ip show command OK

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a>Как tooremove статических частных IP-адресов из виртуальной Машины
tooremove hello статический частный IP-адрес добавлен toohello ВМ в скрипте hello выше выполнения hello следующую команду Azure CLI:

    azure vm static-ip remove DNS01

Ожидаемые выходные данные:

    info:    Executing command vm static-ip remove
    info:    Getting virtual machines
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip remove command OK

## <a name="how-tooadd-a-static-private-ip-tooan-existing-vm"></a>Как tooadd статических закрытый tooan IP существующей виртуальной Машины
tooadd статические частного IP адрес toohello виртуальной Машины, созданной с помощью скрипта hello выше runt следующей команды:

    azure vm static-ip set DNS01 192.168.1.101

Ожидаемые выходные данные:

    info:    Executing command vm static-ip set
    info:    Getting virtual machines
    info:    Looking up virtual network
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip set command OK

## <a name="next-steps"></a>Дальнейшие действия
* Ознакомьтесь с информацией о [зарезервированных общедоступных IP-адресах](virtual-networks-reserved-public-ip.md) .
* Узнайте об [общедоступных IP-адресах уровня экземпляра (ILPIP)](virtual-networks-instance-level-public-ip.md) .
* Обратитесь к hello [зарезервированные интерфейсы REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx).

