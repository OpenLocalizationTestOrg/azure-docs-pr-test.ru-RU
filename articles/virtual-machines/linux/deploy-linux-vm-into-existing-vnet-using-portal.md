---
title: "aaaDeploy виртуальных машин Linux в существующей сети с портала Azure | Документы Microsoft"
description: "Развертывание виртуальной Машины Linux в существующей виртуальной сети Azure с помощью портала hello."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 51272b8cdb1dc7f3fe768d2ebbf4ebe0d754cf19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-portal"></a>Как toodeploy виртуальной машины Linux в существующей виртуальной сети Azure с hello портал Azure

В этой статье показано, как toodeploy виртуальной машины (VM) в существующей виртуальной сети (VNet). Ресурсы Azure, такие как виртуальные сети и группы безопасности сети, должны быть статическими. Они должны долго храниться и редко развертываться. После развертывания виртуальной сети, он может быть использован с константой повторные без инфраструктуры toohello любой негативно влияет на. Размышления о виртуальной сети как обычный параметр сетевого оборудования — не потребуются tooconfigure нового оборудования переключиться с каждым развертыванием.  

С правильно настроенной виртуальной сети можно будет продолжить toodeploy новых серверов в этой виртуальной сети и снова несколько, если таковые имеются, изменения, необходимые протяжении hello hello виртуальной сети.

## <a name="create-hello-resource-group"></a>Создать группу ресурсов hello

Сначала необходимо создаете группы ресурсов tooorganize все данные, создаваемые в данном пошаговом руководстве. Дополнительные сведения о группах ресурсов Azure см. в статье [Общие сведения о диспетчере ресурсов Azure](../../azure-resource-manager/resource-group-overview.md).

![createResourceGroup](./media/deploy-linux-vm-into-existing-vnet-using-portal/createResourceGroup.png)


## <a name="create-hello-vnet"></a>Создать hello виртуальной сети

Затем выполнить сборку виртуальных машин в виртуальной сети toolaunch hello. Hello виртуальная сеть содержит одну подсеть и связан с hello сетевой группы безопасности с этой подсетью на более позднем этапе.

![createVNet](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNet.png)

## <a name="add-a-vnic-toohello-subnet"></a>Добавить подсеть toohello виртуального сетевого адаптера

Виртуальные сетевые адаптеры (VNics) являются важной, так как их можно соединить toodifferent виртуальных машин. Этот подход позволяет hello виртуального сетевого адаптера как статический ресурс, пока hello виртуальные машины могут быть как временными. Создание виртуального сетевого адаптера и связать его с подсетью hello на предыдущем шаге hello.

![createVNic](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNic.png)

## <a name="create-hello-network-security-group"></a>Создание группы безопасности сети hello

Эквивалентный tooa брандмауэра на уровне сети hello являются группы безопасности сети Azure. Дополнительные сведения о группах безопасности сети Azure см. в статье [Фильтрация сетевого трафика с помощью групп безопасности сети](../../virtual-network/virtual-networks-nsg.md).

![createNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/createNSG.png)

## <a name="add-an-inbound-ssh-allow-rule"></a>Добавление правила, разрешающего входящий трафик по протоколу SSH

Hello виртуальной Машины требуется доступ из hello Интернета, поэтому правило, разрешающее трафик toobe входящий порт 22 передаются через tooport сети hello 22 hello создается виртуальная машина.

![createInboundSSH](./media/deploy-linux-vm-into-existing-vnet-using-portal/createInboundSSH.png)

## <a name="associate-hello-nsg-with-hello-subnet"></a>Связать hello NSG с подсетью hello

Hello виртуальной сети и подсети hello создать свяжите hello сетевой группы безопасности с hello подсети. Группы безопасности сети можно связать со всей подсетью или с отдельной виртуальной сетевой картой. С помощью брандмауэра hello фильтрации трафика на уровне подсети hello все VNics и hello виртуальные машины в подсети hello защищаются с помощью группы безопасности сети hello. Hello другого подхода является hello, группы безопасности сети связан только один виртуальный сетевой адаптер и защиту только одна виртуальная машина.

![associateNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/associateNSG.png)


## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a>Развертывание hello виртуальной Машины в виртуальной сети hello и NSG

Использование hello портал Azure, hello виртуальных Машин Linux — развернутой toohello существующие группы ресурсов Azure, виртуальной сети, подсети и виртуального сетевого адаптера.

![createVM](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVM.png)

С помощью существующих ресурсов портала toochoose hello, вы указываете hello Azure toodeploy виртуальных Машин в существующей сети hello. После развертывания виртуальную сеть и подсеть можно оставить в качестве статических или постоянных ресурсов в регионе Azure.  

## <a name="next-steps"></a>Дальнейшие действия

* [Использовать toocreate шаблона диспетчера ресурсов Azure конкретного развертывания](../windows/cli-deploy-templates.md)
* [Создание полной среды Linux с помощью интерфейса командной строки Azure](create-cli-complete.md)
* [Создание виртуальной машины Linux с помощью шаблона Azure](create-ssh-secured-vm-from-template.md)
