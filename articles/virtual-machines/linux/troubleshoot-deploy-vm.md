---
title: "aaaTroubleshoot развертывание проблемы виртуальной машины Linux в Azure | Документы Microsoft"
description: "Устранение неполадок при развертывании виртуальных машин Linux в Azure (модель развертывания с помощью Resource Manager)."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: genli
ms.openlocfilehash: d1092ca3d9d51af7510b19c8c9a79e6dda588697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deploying-linux-virtual-machine-issues-in-azure"></a>Устранение неполадок при развертывании виртуальных машин Linux в Azure

tootroubleshoot проблемы развертывания виртуальной машины (VM) в Azure, просмотрите hello [основных проблем](#top-issues) распространенных ошибок и способы их устранения.

Если вам нужна дополнительная помощь в любой момент в этой статье, можно обратиться в hello экспертов Azure на [hello форумы MSDN Azure и переполнения стека](https://azure.microsoft.com/support/forums/). Кроме того, можно зарегистрировать обращение в службу поддержки Azure. Go toohello [сайт поддержки Azure](https://azure.microsoft.com/support/options/) и выберите **получения поддержки**.

## <a name="top-issues"></a>Наиболее важные проблемы
[!INCLUDE [virtual-machines-linux-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

## <a name="hello-cluster-cannot-support-hello-requested-vm-size"></a>не поддерживает кластера Hello hello запрошенный размер виртуальной Машины
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- Повторите запрос hello, с использованием меньшего размера виртуальной Машины.
- Если hello запрошенный размер hello, что виртуальная машина нельзя изменить:
    - Остановите все виртуальные машины hello в наборе доступности hello. Выберите **Группы ресурсов** > имя вашей группы ресурсов > **Ресурсы** > имя вашей группы доступности > **Виртуальные машины** > имя вашей виртуальной машины > **Остановить**.
    - После того как все hello остановка виртуальных машин, создайте hello ВМ hello требуемого размера.
    - Запустить сначала hello новой виртуальной Машины, а затем выберите каждый hello остановлен, виртуальные машины и нажмите кнопку Пуск.


## <a name="hello-cluster-does-not-have-free-resources"></a>Hello кластер не имеет свободных ресурсов
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- Повторите запрос hello позже.
- Если hello новой виртуальной Машины можно указать различные доступности
    - Создайте виртуальную Машину в наборе доступности на другой (в hello одного региона).
    - Добавление новой виртуальной Машины toohello hello одной виртуальной сети.

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a>Как активировать мой ежемесячный кредит для Visual Studio Enterprise (BizSpark)?

tooactivate кредита вашей ежемесячно, см. в этом [статьи](https://azure.microsoft.com/offers/ms-azr-0064p/).

## <a name="why-can-i-not-install-hello-gpu-driver-for-an-ubuntu-nv-vm"></a>Почему не установить драйвер графического Процессора hello для Виртуальной машине Ubuntu NV?

В настоящее время поддержка Linux GPU доступна только на виртуальных машинах Azure серии NC под управлением Ubuntu Server 16.04 LTS. Дополнительные сведения см. в статье [Установка драйверов GPU для виртуальных машин серии N под управлением Linux](n-series-driver-setup.md).

## <a name="my-drivers-are-missing-for-my-linux-n-series-vm"></a>Для моей виртуальной машины Linux серии N отсутствуют драйверы

Драйверы для виртуальных машин под управлением Linux доступны [здесь](n-series-driver-setup.md). 

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a>Не удается найти экземпляр графического процессора (GPU) на виртуальной машине серии N

tootake преимущества возможностей GPU hello Azure N-й серии виртуальных машин под управлением Windows Server 2016 или Windows Server 2012 R2, необходимо установить NVIDIA графические драйверы на каждую виртуальную Машину после развертывания. Сведения об установке драйверов доступны для [виртуальных машин Windows](../windows/n-series-driver-setup.md) и [виртуальных машин Linux](n-series-driver-setup.md).

## <a name="is-n-series-vms-available-in-my-region"></a>Доступны ли виртуальные машины серии N в моем регионе?

Можно проверить доступность hello из hello [продукты, доступные по таблицы region](https://azure.microsoft.com/regions/services)и ценах [здесь](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).

## <a name="i-am-not-able-toosee-vm-size-family-that-i-want-when-resizing-my-vm"></a>Я не семейство может toosee размер виртуальной Машины, которое требуется при изменении размера ВМ.

При запуске виртуальной Машины, это развернутой tooa физического сервера. Hello физические серверы в регионах Azure, группируются в кластеры общих физического оборудования. Изменение размера виртуальной Машины, которая требует hello виртуальная машина перемещена toobe toodifferent аппаратных кластеров отличается в зависимости от того, какая модель развертывания было используется toodeploy hello виртуальной Машины.

- Виртуальные машины, развернутые в классической модели развертывания, hello развертывания облачной службы необходимо удалить и повторного развертывания размер tooa toochange hello виртуальные машины в другую семью размер.

- Виртуальных машин, развернутых в модели развертывания диспетчера ресурсов, необходимо остановить все виртуальные машины в группе перед изменением размера hello любой виртуальной Машины в наборе доступности hello доступности hello.

## <a name="hello-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a>Hello перечисленных размер виртуальной Машины не поддерживается при развертывании в группе доступности.

Выберите размер, который поддерживается в наборе доступности hello кластера. Рекомендуется при создании набора доступности toochoose hello наибольший размер виртуальной Машины, предполагается, что необходимо, а также иметь ее вашего первого развертывания toohello набора доступности.

## <a name="what-linux-distributionsversions-are-supported-on-azure"></a>Какие дистрибутивы или версии Linux поддерживаются в Azure?

Список hello в Linux можно найти на [Azure-Endorsed распределения](endorsed-distros.md).

## <a name="can-i-add-an-existing-classic-vm-tooan-availability-set"></a>Можно добавить существующую группу доступности tooan классической виртуальной Машины

Да. Можно добавить существующие классические ВМ tooa новый или существующий набор доступности. Дополнительные сведения см. [добавить существующую группу доступности виртуальной машины tooan](../windows/classic/configure-availability.md#addmachine).


## <a name="next-steps"></a>Дальнейшие действия
Если вам нужна дополнительная помощь в любой момент в этой статье, можно обратиться в hello экспертов Azure на [hello форумы MSDN Azure и переполнения стека](https://azure.microsoft.com/support/forums/).

Кроме того, можно зарегистрировать обращение в службу поддержки Azure. Go toohello [сайт поддержки Azure](https://azure.microsoft.com/support/options/) и выберите **получения поддержки**.
