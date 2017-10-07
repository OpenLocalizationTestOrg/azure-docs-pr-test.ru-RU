---
title: "aaaNetwork сопоставление двух регионов Azure в Azure Site Recovery | Документы Microsoft"
description: "Azure Site Recovery координирует hello репликации, отработки отказа и восстановления виртуальных машин и физических серверов. Дополнительные сведения о tooAzure отработки отказа или вторичный центр обработки данных."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: pratshar
ms.openlocfilehash: 4f80c44e3f94eaf446bc01a7041d91fe34aa78d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="network-mapping-between-two-azure-regions"></a>Сетевое сопоставление между двумя регионами Azure


В этой статье описывается как toomap Azure виртуальные сети двух регионов Azure друг с другом. Сетевое сопоставление гарантирует, что при создании реплицированной виртуальной машины в целевом hello регион Azure, создается hello виртуальной сети, сопоставленные toovirtual сети hello исходной виртуальной машины.  

## <a name="prerequisites"></a>Предварительные требования
Перед сопоставлением сетей убедитесь, что в исходном и целевом регионе Azure созданы [виртуальные сети Azure](../virtual-network/virtual-networks-overview.md).

## <a name="map-networks"></a>Сопоставление сетей

toomap виртуальной сети Azure в виртуальной сети tooanother одного региона Azure в другую область, последовательно выберите tooSite восстановления инфраструктуры -> Сетевое сопоставление (для виртуальных машин Azure) и создать сопоставление сети.

![Сетевое сопоставление](./media/site-recovery-network-mapping-azure-to-azure/network-mapping1.png)


В hello в приведенном ниже примере виртуальная машина работает в регионе Восточная Азия и выполняется реплицированные tooSoutheast Азии.

Выберите hello исходная и целевая сеть и нажмите кнопку ОК toocreate сетевое сопоставление из tooSoutheast Восточная Азия Азии.

![Сетевое сопоставление](./media/site-recovery-network-mapping-azure-to-azure/network-mapping2.png)


Здравствуйте же самое toocreate сетевое сопоставление из tooEast Азии, Юго-Восточная Азия.  
![Сетевое сопоставление](./media/site-recovery-network-mapping-azure-to-azure/network-mapping3.png)


## <a name="mapping-network-when-enabling-replication"></a>Сетевое сопоставление при включении репликации

Если сетевое сопоставление не выполняется, если выполняется репликация виртуальной машины для hello первый раз формы один регион Azure tooanother, затем можно выбрать целевую сеть как часть hello одного процесса. Site Recovery создает сопоставления сетей из области tootarget области источника и целевой регион toosource области на основе выбора.   

![Сетевое сопоставление](./media/site-recovery-network-mapping-azure-to-azure/network-mapping4.png)

По умолчанию Site Recovery создает сеть в целевой регион hello, идентичные toohello Исходная сеть и путем добавления "-asr" в качестве суффикса имени toohello hello исходную сеть. Щелкните "Настройка", чтобы выбрать созданную ранее сеть.

![Сетевое сопоставление](./media/site-recovery-network-mapping-azure-to-azure/network-mapping5.png)


Если hello сетевое сопоставление уже выполнено, нельзя изменить hello целевой виртуальной сети при включении репликации. toochange, измените существующее сетевое сопоставление.  

![Сетевое сопоставление](./media/site-recovery-network-mapping-azure-to-azure/network-mapping6.png)

![Сетевое сопоставление](./media/site-recovery-network-mapping-azure-to-azure/modify-network-mapping.png)

> [!IMPORTANT]
> При изменении сетевого сопоставления из области 1 tooregion-2, убедитесь, что вы измените сопоставление сети hello из области 2 tooregion-1 также.
>
>


## <a name="subnet-selection"></a>Выбор подсети
Подсеть виртуальной машины hello выбирается на основе имени hello подсети hello hello исходной виртуальной машине. Если подсеть hello одинаковые имена, что и hello исходной виртуальной машины в целевой сети hello, затем, выбирать для hello целевой виртуальной машины. Если подсеть с hello одинаковые имена в целевой сети hello, а затем по алфавиту первая подсеть выбирается как hello целевой подсети. Подсети можно изменить, выбрав tooCompute, а также параметры сети виртуальной машины hello.

![Изменение подсети](./media/site-recovery-network-mapping-azure-to-azure/modify-subnet.png)


## <a name="ip-address"></a>IP-адрес

IP-адрес для каждого сетевого интерфейса hello hello целевой виртуальной машины выбран следующим образом:

### <a name="dhcp"></a>DHCP
Если сетевой интерфейс hello hello исходной виртуальной машине с помощью DHCP, сетевому интерфейсу hello целевая виртуальная машина также задан как DHCP.

### <a name="static-ip"></a>Статический IP-адрес
Если сетевой интерфейс hello hello исходной виртуальной машине использует статический IP-адрес, сетевой интерфейс виртуальной машины hello также устанавливается toouse статический IP-адрес. Статический IP-адрес можно выбрать следующим образом:

#### <a name="same-address-space"></a>Одинаковое пространство адресов

Если подсеть hello источника и целевой подсети hello имеют hello же адресное пространство, то целевой IP-адрес задается то же, что hello IP-адреса сетевого интерфейса hello hello исходной виртуальной машине. Если IP-адрес недоступен, некоторые другие доступный IP-адрес задан как hello целевой IP-адрес.

#### <a name="different-address-space"></a>Разное пространство адресов

Если подсеть источника hello и hello целевой подсети имеют разные адресное пространство, целевой IP-адрес задан как любой доступный IP-адрес в hello целевой подсети.

Hello целевой IP-адрес каждого сетевого интерфейса можно изменить, выбрав tooCompute, а также параметры сети виртуальной машины hello.

## <a name="next-steps"></a>Дальнейшие действия

- Дополнительные сведения о репликации виртуальных машин см. в [этой статье](site-recovery-azure-to-azure-networking-guidance.md).
