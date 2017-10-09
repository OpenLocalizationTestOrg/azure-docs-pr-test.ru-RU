---
title: "развертывание Windows виртуальной машины проблемы в Azure aaaTroubleshoot | Документы Microsoft"
description: "Устранение неполадок при развертывании виртуальных машин Windows в Azure (модель развертывания с помощью Resource Manager)."
services: virtual-machines-windows
documentationcenter: 
author: genlin
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
ms.openlocfilehash: 30de25827c050cc266761cfc14548bcc64237dac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deploying-windows-virtual-machine-issues-in-azure"></a>Устранение неполадок при развертывании виртуальных машин Windows в Azure

tootroubleshoot проблемы развертывания виртуальной машины (VM) в Azure, просмотрите hello [основных проблем](#top-issues) распространенных ошибок и способы их устранения.

Если вам нужна дополнительная помощь в любой момент в этой статье, можно обратиться в hello экспертов Azure на [hello форумы MSDN Azure и переполнения стека](https://azure.microsoft.com/support/forums/). Кроме того, можно зарегистрировать обращение в службу поддержки Azure. Go toohello [сайт поддержки Azure](https://azure.microsoft.com/support/options/) и выберите **получения поддержки**.

## <a name="top-issues"></a>Наиболее важные проблемы
[!INCLUDE [virtual-machines-windows-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-windows-troubleshoot-deploy-vm-top.md)]

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

## <a name="how-can-i-use-and-deploy-a-windows-client-image-into-azure"></a>Как использовать и развернуть образ клиента Windows в Azure?

В сценариях разработки и тестирования Azure можно использовать Windows 7, Windows 8 или Windows 10, если у вас есть соответствующая подписка Visual Studio (прежнее название — MSDN). Это [статьи](client-images.md) контуров hello требования для запуска клиента Windows в Azure, а также способы использования hello образов коллекции Azure.

## <a name="how-can-i-deploy-a-virtual-machine-using-hello-hybrid-use-benefit-hub"></a>Развертывание виртуальной машины при помощи hello преимущество использования гибридной (КОНЦЕНТРАТОР)

Существует несколько способов toodeploy Windows виртуальных машин с hello преимущество использования гибридной Azure.

Для подписки с соглашением Enterprise:

•   можно развернуть виртуальные машины на основе специальных образов из Marketplace, предварительно настроенных для применения программы преимуществ гибридного использования Azure.

Для соглашения Enterprise:

•   можно передать настраиваемую виртуальную машину и развернуть ее с помощью шаблона Resource Manager или Azure PowerShell.

Дополнительные сведения см. в разделе hello следующие ресурсы:

 - [Обзор программы преимуществ гибридного использования Azure](https://azure.microsoft.com/pricing/hybrid-use-benefit/)

 - [Скачиваемый файл с часто задаваемыми вопросами](http://download.microsoft.com/download/4/2/1/4211AC94-D607-4A45-B472-4B30EDF437DE/Windows_Server_Azure_Hybrid_Use_FAQ_EN_US.pdf)

 - [Преимущества гибридного использования Azure для сервера Windows Server и клиента Windows](hybrid-use-benefit-licensing.md)

 - [Как использовать hello гибридного использовать преимущества Azure](https://blogs.msdn.microsoft.com/azureedu/2016/04/13/how-can-i-use-the-hybrid-use-benefit-in-azure)

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a>Как активировать мой ежемесячный кредит для Visual Studio Enterprise (BizSpark)?

tooactivate кредита вашей ежемесячно, см. в этом [статьи](https://azure.microsoft.com/offers/ms-azr-0064p/).

## <a name="how-tooadd-enterprise-devtest-toomy-enterprise-agreement-ea-tooget-access-toowindow-client-images"></a>Как tooadd Enterprise разработки и тестирования toomy Enterprise Agreement (EA) tooget доступ к tooWindow образов клиента?

предложить Hello возможность toocreate подписки, основанные на hello Enterprise разработки и тестирования является ограниченным tooAccount владельцев, которые были присвоены разрешения toodo так администратором предприятия. Hello владелец учетной записи создает подписки через портал учетных записей Azure hello и затем следует добавить действующими подписками Visual Studio в список администраторов. Чтобы они смогут управлять и использовать ресурсы hello, необходимые для разработки и тестирования. Дополнительные сведения см. в статье [Разработка и тестирование Enterprise](https://azure.microsoft.com/offers/ms-azr-0148p/).

## <a name="my-drivers-are-missing-for-my-windows-n-series-vm"></a>Для моей виртуальной машины Windows серии N отсутствуют драйверы

Драйверы для виртуальных машин под управлением Windows доступны [здесь](n-series-driver-setup.md).

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a>Не удается найти экземпляр графического процессора (GPU) на виртуальной машине серии N

tootake преимущества возможностей GPU hello Azure N-й серии виртуальных машин под управлением Windows Server 2016 или Windows Server 2012 R2, необходимо установить NVIDIA графические драйверы на каждую виртуальную Машину после развертывания. Сведения об установке драйверов доступны для [виртуальных машин Windows](n-series-driver-setup.md) и [виртуальных машин Linux](../linux/n-series-driver-setup.md).

## <a name="are-client-images-supported-for-n-series"></a>Поддерживаются ли образы клиентов для серии N?

В настоящее время Azure поддерживает образы клиентов только на виртуальных машинах серии N под управлением операционных систем Windows Server и Linux.

## <a name="is-n-series-vms-available-in-my-region"></a>Доступны ли виртуальные машины серии N в моем регионе?

Можно проверить доступность hello из hello [продукты, доступные по таблицы region](https://azure.microsoft.com/regions/services)и ценах [здесь](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).

## <a name="what-client-images-can-i-use-and-deploy-in-azure-and-how-tooi-get-them"></a>Какие клиентские образы можно ли использовать и развертывать в Azure, а также как получить tooI их?

В сценариях разработки и тестирования Azure можно использовать Windows 7, Windows 8 или Windows 10 при условии, что у вас есть соответствующая подписка Visual Studio (прежнее название — MSDN). 

- Образы Windows 10 можно получить из коллекции Azure hello в [предлагает подходящие для разработки и тестирования](client-images.md#eligible-offers). 
- Visual Studio, использующих любого типа предложения можно также [адекватно подготовки и создания](prepare-for-upload-vhd-image.md) 64-разрядный образ Windows 7, Windows 8 или Windows 10 и затем [отправить tooAzure](upload-generalized-managed.md). Использование Hello остается ограниченной toodev и тестирования с действующими подписками Visual Studio.

Это [статьи](client-images.md) контуров hello требования для запуска клиента Windows Azure и использование hello образов коллекции Azure.

## <a name="i-am-not-able-toosee-vm-size-family-that-i-want-when-resizing-my-vm"></a>Я не семейство может toosee размер виртуальной Машины, которое требуется при изменении размера ВМ.

При запуске виртуальной Машины, это развернутой tooa физического сервера. Hello физические серверы в регионах Azure, группируются в кластеры общих физического оборудования. Изменение размера виртуальной Машины, которая требует hello виртуальная машина перемещена toobe toodifferent аппаратных кластеров отличается в зависимости от того, какая модель развертывания было используется toodeploy hello виртуальной Машины.

- Виртуальные машины, развернутые в классической модели развертывания, hello развертывания облачной службы необходимо удалить и повторного развертывания размер tooa toochange hello виртуальные машины в другую семью размер.

- Виртуальных машин, развернутых в модели развертывания диспетчера ресурсов, необходимо остановить все виртуальные машины в группе перед изменением размера hello любой виртуальной Машины в наборе доступности hello доступности hello.

## <a name="hello-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a>Hello перечисленных размер виртуальной Машины не поддерживается при развертывании в группе доступности.

Выберите размер, который поддерживается в наборе доступности hello кластера. Рекомендуется при создании набора доступности toochoose hello наибольший размер виртуальной Машины, предполагается, что необходимо, а также иметь ее вашего первого развертывания toohello набора доступности.

## <a name="can-i-add-an-existing-classic-vm-tooan-availability-set"></a>Можно добавить существующую группу доступности tooan классической виртуальной Машины

Да. Можно добавить существующие классические ВМ tooa новый или существующий набор доступности. Дополнительные сведения см. [добавить существующую группу доступности виртуальной машины tooan](classic/configure-availability.md#addmachine).


## <a name="next-steps"></a>Дальнейшие действия
Если вам нужна дополнительная помощь в любой момент в этой статье, можно обратиться в hello экспертов Azure на [hello форумы MSDN Azure и переполнения стека](https://azure.microsoft.com/support/forums/).

Кроме того, можно зарегистрировать обращение в службу поддержки Azure. Go toohello [сайт поддержки Azure](https://azure.microsoft.com/support/options/) и выберите **получения поддержки**.
