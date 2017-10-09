---
title: "Здравствуйте, aaaOpen порты tooa виртуальной Машины с помощью портала Azure | Документы Microsoft"
description: "Узнайте, как tooopen порт / create tooyour конечной точки виртуальной Машины Windows с помощью модели развертывания диспетчера ресурсов hello в hello портала Azure"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: f7cf0319-5ee7-435e-8f94-c484bf5ee6f1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: aba789c65254651899aa688f256fe616c3d0126d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-tooa-virtual-machine-with-hello-azure-portal"></a>Как tooopen порты tooa виртуальную машину с портала Azure hello
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a>Быстрые команды
Эти действия также можно [выполнить с помощью Azure PowerShell](nsg-quickstart-powershell.md).

Сначала создайте группу безопасности сети. Выберите группу ресурсов в портале hello, выберите **добавить**, а затем найдите и выберите **сетевой группы безопасности**:

![Добавление группы безопасности сети](./media/nsg-quickstart-portal/add-nsg.png)

Введите имя группы безопасности сети, выберите или создайте группу ресурсов и выберите расположение. По завершении выберите **Создание**:

![Создание группы безопасности сети](./media/nsg-quickstart-portal/create-nsg.png)

Выберите созданную группу безопасности сети. Выберите «Правила для входящих подключений безопасности», а затем hello **добавить** кнопку toocreate правила:

![Добавление правила для входящих подключений](./media/nsg-quickstart-portal/add-inbound-rule.png)

Выберите общий **службы** hello раскрывающегося меню, таких как *HTTP*. Можно также выбрать *настраиваемый* tooprovide toouse определенный порт. При необходимости, измените приоритет hello, или имя. Hello приоритет влияет на порядок hello, в котором применяются правила - числовое значение нижней hello hello, hello предыдущих hello применяется правило. Можно также выбрать **Дополнительно** вверху hello этот экран tooenter конкретного источника IP-диапазон блока или порта, например. Когда будете готовы, выберите **ОК** toocreate hello правила:

![Создание правила для входящих подключений](./media/nsg-quickstart-portal/create-inbound-rule.png)

Последняя операция — tooassociate группы безопасности сети с подсетью или определенного сетевого интерфейса. Давайте связать hello сетевой группы безопасности с подсетью. Выберите **Подсети**, а затем — **Привязать**:

![Связывание группы безопасности сети с подсетью](./media/nsg-quickstart-portal/associate-subnet.png)

Выберите виртуальную сеть, а затем выберите соответствующую подсеть hello:

![Связывание группы безопасности сети с виртуальной сетью](./media/nsg-quickstart-portal/select-vnet-subnet.png)

Вы создали группу безопасности сети, создали правило для входящих подключений, которое пропускает трафик через порт 80, и связали эту группу с подсетью. Все виртуальные машины, подключение toothat подсети должны быть доступны через порт 80.

## <a name="more-information-on-network-security-groups"></a>Дополнительная информация о группах безопасности сети
Hello здесь Быстрые команды позволяют tooget вверх и работает с tooyour передачу трафика виртуальных Машин. Сетевые группы безопасности предоставляют много замечательных функций и гранулярности для управления доступа к ресурсам tooyour. [Здесь](../../virtual-network/virtual-networks-create-nsg-arm-ps.md)вы можете больше прочитать о создании группы безопасности сети и правил ACL.

Для веб-приложений с высокой доступностью необходимо поместить виртуальную машину за Azure Load Balancer. Подсистема балансировки нагрузки Hello распределяет трафик tooVMs, с группой безопасности сети, которая обеспечивает фильтрацию трафика. Дополнительные сведения см. в разделе [как баланс tooload Linux виртуальных машин в Azure toocreate приложение с высокой доступностью](tutorial-load-balancer.md).

## <a name="next-steps"></a>Дальнейшие действия
В этом примере вы создали трафика tooallow HTTP простое правило. Можно найти сведения о создании более подробные сред в hello в следующих статьях:

* [Общие сведения об Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)
* [Группа безопасности сети](../../virtual-network/virtual-networks-nsg.md)