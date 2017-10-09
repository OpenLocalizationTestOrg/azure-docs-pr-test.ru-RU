---
title: "Работа по сети для репликации Hyper-V (без System Center VMM) tooAzure с Azure Site Recovery aaaPlan | Документы Microsoft"
description: "В этой статье описывается сети, планирование, необходимое при репликации виртуальных машин Hyper-V (без VMM) tooAzure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5ca12254-975d-48e8-a84d-422825dac9b2
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: a35de72b53ca921a7b9bfca00a0edcb9416d5aa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-plan-networking-for-hyper-v-tooazure-replication"></a>Шаг 4: Планирование сети для репликации tooAzure Hyper-V

Это статье кратко рассматриваются вопросы планирования при репликации локальных tooAzure виртуальных машин Hyper-V (без System Center VMM), с помощью hello сети [Azure Site Recovery](site-recovery-overview.md) службы.

Отправлять все комментарии hello нижней части этой статьи, или задать вопросы в hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="connecting-tooreplica-vms-after-failover"></a>Подключение tooreplica виртуальных машин после отработки отказа

При планировании репликации и стратегия отработки отказа, является одним из ключевых вопроса hello как toohello tooconnect виртуальной Машины Azure после отработки отказа. При разработке сетевой стратегии для виртуальных машин реплик Azure существует несколько вариантов:

- **Другой IP-адрес**: можно выбрать toouse диапазоном IP-адресов для сети виртуальной Машины Azure реплицированных hello. В этот сценарий hello виртуальная машина получит новый IP-адрес после отработки отказа и требуется обновление DNS. [Дополнительные сведения](site-recovery-test-failover-vmm-to-vmm.md#prepare-the-infrastructure-for-test-failover)
- **Один IP-адрес**: может потребоваться toouse hello же диапазон IP-адресов, что, в основной в локальной сети, для hello сети Azure после отработки отказа.  Сохранение hello одинаковые IP-адреса упрощает hello восстановления за счет уменьшения проблемы, связанные с сети после отработки отказа. Тем не менее при выполнении репликации tooAzure, необходимо будет tooupdate маршруты с нового расположения hello hello IP-адресов после отработки отказа.


## <a name="retain-ip-addresses"></a>Использование тех же IP-адресов

Site Recovery предоставляет hello возможность tooretain фиксированных IP-адресов при отработке отказа tooAzure с отработки отказа в подсети.

При отработке отказа в подсети отдельно взятая подсеть присутствует на сайте 1 или 2, но никогда на обоих сайтах одновременно. В порядке toomaintain hello пространство IP-адресов в событии hello перехода на другой ресурс программным образом упорядочить для hello маршрутизатора инфраструктуры toomove из одного узла tooanother hello подсетей. Во время отработки отказа hello подсетей для перемещения hello связанные защищенных виртуальных машин. Основным недостатком Hello: в случае сбоя hello иметь toomove hello всей подсети.


### <a name="failover-example"></a>Пример отработки отказа

Давайте рассмотрим пример tooAzure перехода на другой ресурс.

- Вымышленная компания, банк Woodgrove, имеет локальную инфраструктуру, в которой размещены ее бизнес-приложения. Ее мобильные приложения размещены в Azure.
- Связь между виртуальными машинами банка Woodgrove в Azure и локальных серверов обеспечивается соединение сеть сеть (VPN) между hello локальной сети edge и hello виртуальной сети Azure.
- Это VPN означает, что hello компании виртуальной сети в Azure в виде расширения их в локальной сети.
- Woodgrove хочет toouse Site Recovery tooreplicate локальных рабочих нагрузок tooAzure.
 - Woodgrove имеет toodeal с приложениями и конфигурации, которые зависят от жестко IP-адресов и поэтому tooretain IP-адреса для своих приложений после отработки отказа tooAzure.
 - Woodgrove назначил IP-адреса из диапазона 172.16.1.0/24, 172.16.2.0/24 tooits ресурсов в Azure.


Для банка Woodgrove toobe может tooreplicate tooAzure его виртуальные машины во время сохранения hello IP-адресов Вот какие hello компании toodo:

1. Создайте виртуальную сеть Azure. Расширение hello в локальной сети, необходимо, чтобы приложения могут выполнять отработку отказа без проблем.
2. Azure позволяет вам tooadd сеть сеть VPN-подключение, кроме toopoint сеть toohello виртуальных сетей, созданные в Azure.
3. При настройке подключения hello сайт сайт, в hello Azure сети, может осуществлять маршрутизацию трафика toohello локально (локальная сеть) только в том случае, если диапазон IP-адресов hello отличается от диапазона IP-адресов hello в локальной среде.
    - Это связано с тем, что Azure не поддерживает растянутые подсети. Поэтому при наличии подсети 192.168.1.0/24 локальной 192.168.1.0/24 локальной сети нельзя добавить в hello сети Azure.
    - Ожидается, так как Azure не знает, что отсутствуют активные ВМ в подсети hello и подсети hello создается только для аварийного восстановления.
    - toobe может toocorrectly маршрутизацию сетевого трафика за пределами Azure hello подсетей в сети hello и hello локальной сети должен конфликтуют.

![Перед выполнением отработки отказа подсети](./media/hyper-v-site-walkthrough-network/network-design7.png)

### <a name="before-failover"></a>Перед выполнением отработки отказа

1. Создайте дополнительную сеть (например, сеть восстановления). Это сеть hello в которой отработку отказа виртуальных машин были созданы.
2. tooensure, hello IP-адрес для виртуальной Машины сохраняется после отработки отказа, в свойствах виртуальной Машины hello > **Настройка**, укажите hello же IP-адресов, hello виртуальной Машины используется локальная и нажмите кнопку **Сохранить**.
3. При переключении hello ВМ Azure Site Recovery будет назначать hello, предоставляемые tooit IP адрес.

    ![Свойства сети](./media/hyper-v-site-walkthrough-network/network-design8.png)

4. После отработки отказа триггер срабатывает и hello виртуальные машины создаются в Azure с hello требуется IP-адрес, можно подключиться при помощи сети toohello [Vnet tooVnet vonnection](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md). Это действие можно выполнить с помощью сценария.
5. Маршруты необходимо соответствующим образом изменены, toobe tooreflect tooAzure теперь перемещен, 192.168.1.0/24.

    ![После выполнения отработки отказа подсети](./media/hyper-v-site-walkthrough-network/network-design9.png)

### <a name="after-failover"></a>После выполнения отработки отказа

Если у вас нет сети Azure, как показано на рисунке выше, то после отработки отказа можно создать VPN-подключение типа "сеть — сеть" между основным сайтом и Azure.

## <a name="change-ip-addresses"></a>Изменение IP-адресов

Это [блога](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) объясняет, как tooset копирование hello Azure сетевой инфраструктуры, когда нет необходимости использовать tooretain IP адресов после перехода на другой ресурс. Он начинается с описание приложения, осуществляет как tooset сеть в локальной, так и в Azure и заканчиваются сведения о выполнении переход на другой ресурс.  

## <a name="next-steps"></a>Дальнейшие действия

Go слишком[шаг 5: Подготовка Azure](hyper-v-site-walkthrough-prepare-azure.md)
