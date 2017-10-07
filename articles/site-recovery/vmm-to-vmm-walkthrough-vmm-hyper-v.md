---
title: "aaaSet VMM и Hyper-V для репликации tooa вторичного сайта с помощью Azure Site Recovery | Документы Microsoft"
description: "Описывает способ tooset серверы System Center VMM и узлы Hyper-V для репликации tooa вторичный сайт VMM."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d0389e3b-3737-496c-bda6-77152264dd98
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 677bf6d38328ccc425e3b0f056d03159a52da428
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-set-up-vmm-and-hyper-v-for-hyper-v-vm-replication-tooa-secondary-site"></a>Шаг 4: Настройка VMM и Hyper-V для виртуальных Машин Hyper-V репликации tooa вторичного сайта 

После подготовки для работы в сети настраивать серверы диспетчера виртуальных машин System Center (VMM) и узлы Hyper-V для Hyper-V виртуальной машины (VM) репликации tooa вторичного сайта с помощью [Azure Site Recovery](site-recovery-overview.md) в hello портал Azure. 

После считывания в этой статье, отправлять любые комментарии, внизу hello, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="prepare-vmm-servers"></a>Подготовка серверов VMM 

tooprepare для развертывания:


1. Убедитесь, что серверы VMM соответствовать hello [требованиям](site-recovery-support-matrix-to-sec-site.md#on-premises-servers), и [необходимые условия для развертывания](vmm-to-vmm-walkthrough-prerequisites.md).
2. Убедитесь, что серверы VMM подключенных toohello Интернет и доступа toothese URL-адресов.
    
    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
    - Если правила брандмауэра на основе адресов IP, убедитесь, что они позволяют tooAzure связи.
    - Разрешить hello [диапазоны IP-адресов центра обработки данных Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)и hello порта HTTPS (443).
    - Разрешить диапазоны IP-адресов для hello регион Azure, подписки и Запад США (используется для контроля доступа и удостоверений).
3. Убедитесь, что сервер VMM hello [подготовлен для сетевого сопоставления](vmm-to-vmm-walkthrough-network.md#prepare-for-network-mapping)


## <a name="prepare-hyper-v-hostsclusters"></a>Подготовка узлов и кластеров Hyper-V

1. Убедитесь, что узлы Hyper-V и кластеры соответствовать hello [требованиям](site-recovery-support-matrix-to-sec-site.md#on-premises-servers), и [необходимые условия для развертывания](vmm-to-vmm-walkthrough-prerequisites.md).
2. Проверьте требования hello для [виртуальных машин Hyper-V](site-recovery-support-matrix-to-sec-site.md#support-for-replicated-machine-os-versions)
3. Проверьте требования к [сети](site-recovery-support-matrix-to-sec-site.md#network-configuration) и [хранилищу](site-recovery-support-matrix-to-sec-site.md#storage).
4. Убедитесь, что узлы Hyper-V подключенных toohello Интернет и доступа toothese URL-адресов.
    
    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
    - Если правила брандмауэра на основе адресов IP, убедитесь, что они позволяют tooAzure связи.
    - Разрешить hello [диапазоны IP-адресов центра обработки данных Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)и hello порта HTTPS (443).
    - Разрешить диапазоны IP-адресов для hello регион Azure, подписки и Запад США (используется для контроля доступа и удостоверений).

## <a name="prepare-for-single-server-deployment"></a>Подготовка к развертыванию одного сервера


Если имеется только один сервер VMM, можно выполнять репликацию виртуальных машин в узлах Hyper-V в облаке VMM hello слишком[Azure](hyper-v-site-walkthrough-overview.md) или tooa получателя VMM облака, как описано в этом документе. Рекомендуется hello первый вариант, поскольку репликация между облаками не прозрачную.

Если вы хотите tooreplicate между облаками, можно реплицировать с одним автономным сервером VMM или с одного сервера VMM, развернутых в кластере Windows растяжением

### <a name="replicate-with-a-standalone-vmm-server"></a>Репликация с использованием изолированного сервера VMM

В этом сценарии развертывания одного сервера VMM hello в качестве виртуальной машины в первичном сайте hello и реплицировать этой виртуальной Машины tooa вторичный сайт с помощью Site Recovery и реплики Hyper-V.

1. **Настройте VMM на виртуальной машине Hyper-V**. Мы советуем использовать совместное размещение hello экземпляр SQL Server, используемый VMM на hello одной виртуальной Машины. Это экономит время, что только одна виртуальная машина имеет toobe создан. Если требуется toouse удаленный экземпляр SQL Server и возникновении сбоя, необходимо toorecover этот экземпляр перед восстановлением VMM.
2. **Убедитесь, сервер VMM hello имеет по крайней мере два облака, настроенные**. Одно облако содержит виртуальные машины должны tooreplicate и hello другие облачные будет использоваться в качестве дополнительного расположения hello приветствия. Здравствуйте облако, содержащее hello виртуальных машин требуется должны соответствовать tooprotect [необходимых компонентов](#prerequisites).
3. Настройте Site Recovery, как описано в этой статье. Создать и зарегистрировать сервер VMM hello в хранилище, настройте политику репликации и включить репликацию. Hello исходного и конечного имен VMM будет hello же. Указывайте, что начальная репликация выполняется по сети hello.
4. При настройке сетевого сопоставления можно сопоставить hello сети виртуальной Машины для сети виртуальной Машины toohello hello основное облако для hello вторичное облако.
5. В консоли диспетчера Hyper-V hello включения реплики Hyper-V на узле Hyper-V hello, содержащий hello виртуальной Машины VMM и включить репликацию на hello виртуальной Машины. Убедитесь, что не добавляйте tooclouds виртуальной машины VMM hello, защищенные Site Recovery, tooensure, что параметры реплики Hyper-V не переопределено Site Recovery.
6. При создании планов восстановления для отработки отказа, используемого hello один сервер VMM для источника и целевых.
7. Отработка отказа и восстановление при полном сбое выполняются следующим образом.

   1. Запустите незапланированную отработку отказа в консоли диспетчера Hyper-V hello в hello вторичного сайта, toofail через hello основной виртуальной Машины VMM toohello вторичного сайта.
   2. Убедитесь, что приветствия виртуальной Машины VMM работает и работает и в хранилище hello запустите toofail внеплановой отработки отказа на виртуальных машинах hello из первичного toosecondary облаков. Зафиксируйте hello перехода на другой ресурс и выберите альтернативную точку восстановления, если это необходимо.
   3. Завершении hello внеплановой отработки отказа, все ресурсы может осуществляться снова hello основного сайта.
   4. При доступности, в консоли диспетчера Hyper-V hello hello вторичном сайте первичного сайта hello включите обратную репликацию для виртуальной Машины VMM hello. Запустится репликации для виртуальной Машины hello из вторичного tooprimary.
   5. Выполните Плановую отработку отказа в консоли диспетчера Hyper-V hello hello вторичном сайте, toofail через hello виртуальной Машины VMM toohello первичного сайта. Зафиксируйте hello перехода на другой ресурс. Затем включите обратную репликацию, hello виртуальной Машины VMM еще раз реплицируется из источника toosecondary.
   6. В хранилище служб восстановления hello включите обратную репликацию для hello нагрузок виртуальных машин, копируя их из вторичного tooprimary toostart.
   7. В hello хранилище служб восстановления, выполните Плановую отработку отказа toofail назад hello рабочей нагрузки виртуальных машин toohello первичного сайта. Зафиксировать hello отработки отказа toocomplete его. Затем включите обратную репликацию toostart репликации hello рабочей нагрузки виртуальных машин с основного toosecondary.

### <a name="replicate-with-a-stretched-vmm-cluster"></a>Репликация с использованием растянутого кластера VMM

Вместо развертывания автономного сервера VMM, как виртуальная машина, реплицируемые tooa вторичного сайта, то сможете VMM высокой надежности, развертывая ее в качестве виртуальной Машины в отказоустойчивом кластере Windows. Это позволяет обеспечить устойчивость рабочих нагрузок и защиту от сбоев оборудования. toodeploy с hello сайта восстановления виртуальной Машины VMM следует развернуть в кластере stretch географически узлами. toodo это:

1. Установка VMM на виртуальной машине в отказоустойчивом кластере Windows и выберите hello параметр toorun hello сервер высокой надежности во время установки.
2. экземпляр SQL Server Hello, которое используется диспетчером VMM должны реплицироваться с группами доступности SQL Server AlwaysOn, таким образом, что реплика базы данных hello в hello вторичного сайта.
3. Следуйте инструкциям hello в этой статье toocreate хранилище, зарегистрируйте сервер hello и настройки защиты. Необходимо tooregister каждый сервер VMM в hello кластер в hello в хранилище служб восстановления. toodo это, установите hello поставщик на активном узле и зарегистрируйте сервер VMM hello. Затем установите hello поставщика на другие узлы.
4. При возникновении сбоя сервера VMM hello и соответствующей базой данных SQL Server при сбое и обращаться из hello вторичного сайта.



## <a name="next-steps"></a>Дальнейшие действия

Go слишком[шаг 5: Настройка хранилища](vmm-to-vmm-walkthrough-create-vault.md).
