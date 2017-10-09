---
title: "Следующий прыжок aaaFind с Azure сети наблюдателя следующего прыжка - портал Azure | Документы Microsoft"
description: "В этой статье описывается, как можно найти какие hello тип следующего прыжка — и IP-адрес, с помощью следующего прыжка hello портал Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 7b459dcf-4077-424e-a774-f7bfa34c5975
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b64a2a5275c15aa8bdb10601de4ae1504a9ab551
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-hello-portal"></a>Узнать, какой тип следующего прыжка hello является использование возможностей следующего прыжка hello в Наблюдатель сети Azure с помощью портала hello

> [!div class="op_single_selector"]
> - [Портал Azure](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [Интерфейс командной строки 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-next-hop-cli.md)
> - [Azure REST API](network-watcher-check-next-hop-rest.md)

Следующий прыжок является компонентом Наблюдатель сети, который предоставляет возможность hello получить тип следующего прыжка hello и IP-адрес, на основе указанной виртуальной машины. Эта функция полезна при определении Если пакетов, отправляемых виртуальная машина проходит через шлюз, Интернет или назначения tooits tooget виртуальных сетей.

## <a name="before-you-begin"></a>Перед началом работы

Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети. сценарий Hello также предполагается, что группа ресурсов с действительной виртуальной машиной существует toobe используется.

## <a name="scenario"></a>Сценарий

Hello сценарии, описанные в данной статье используется следующего прыжка toofind тип следующего прыжка hello и IP-адрес для ресурса. Посетите toolearn Дополнительные сведения о следующего прыжка [следующего прыжка Обзор](network-watcher-next-hop-overview.md).

Вам предстоит:

* Получение следующего прыжка hello из виртуальной машины.

## <a name="get-next-hop"></a>Получение следующего прыжка

### <a name="step-1"></a>Шаг 1

Перейдите tooyour Наблюдатель сети ресурс в hello портал Azure.

### <a name="step-2"></a>Шаг 2

Нажмите кнопку **следующего прыжка** в области навигации hello hello выберите виртуальную машину и сетевого интерфейса, введите hello исходного и конечного IP и нажмите кнопку hello **следующего прыжка** кнопки.

> [!NOTE]
> Следующий прыжок требуется что toorun распределения ресурсов виртуальной Машины hello.

![Обзор получения следующего прыжка][1]

### <a name="step-3"></a>Шаг 3.

После завершения задачи hello приведены результаты hello. Здравствуйте, IP-адрес и тип следующего прыжка hello устройство, отображается. Hello следующей таблице показаны доступные возвращенные значения hello в портал hello.

**Типы следующего прыжка**

* Интернет
* VirtualAppliance
* VirtualNetworkGateway
* VnetLocal
* HyperNetGateway
* VnetPeering
* None

Если настраиваемый маршрут был используется tooroute этот трафик hello определяемых пользователем маршрутов (UDR) также отображаются с результатами hello.

![Получение результатов следующего прыжка][2]

## <a name="next-steps"></a>Дальнейшие действия

Узнайте, как tooreview параметров группы безопасности сети программным способом, посетив [NSG аудита и Наблюдатель сети](network-watcher-nsg-auditing-powershell.md)

[1]: ./media/network-watcher-check-next-hop-portal/figure1.png
[2]: ./media/network-watcher-check-next-hop-portal/figure2.png














