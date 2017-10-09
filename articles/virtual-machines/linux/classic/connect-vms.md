---
title: "aaaConnect виртуальных машин Linux в облачной службе | Документы Microsoft"
description: "Подключение виртуальных машин Linux, созданных с помощью tooan модели hello классического развертывания Azure облачной службы или виртуальной сети."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 2fd23055-6b34-4ef0-88a8-fc19e32fb3c9
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: cynthn
ms.openlocfilehash: 323baf04390d53ffb2810e24a24d175c08e60cd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-linux-virtual-machines-created-with-hello-classic-deployment-model-with-a-virtual-network-or-cloud-service"></a>Подключение виртуальных машин Linux, созданных с помощью hello классической модели развертывания с помощью виртуальной сети или облачные службы
> [!IMPORTANT]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.

Виртуальные машины Linux, созданных с помощью hello классической модели развертывания они всегда размещаются в облачной службе. Hello облачной службы выступает в роли контейнера и обеспечивает открытый уникальное имя DNS, общедоступный IP-адрес и набор конечных точек tooaccess hello виртуальной машины к hello Интернета. может быть Hello облачной службы в виртуальной сети, но не является обязательным. Вы также можете [подключить виртуальные машины Windows к виртуальной сети или облачной службе](../../windows/classic/connect-vms.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Если облачная служба не находится в виртуальной сети, она называется *автономной* . Hello виртуальные машины в облачной службе автономный взаимодействовать с другими виртуальными машинами с помощью hello открытый DNS-имена других виртуальных машин и hello трафик проходит через Интернет hello. Если облачная служба находится в виртуальной сети виртуальных машин hello в том, что облачная служба может взаимодействовать с всех остальных виртуальных машин в виртуальной сети hello без отправки любой трафик по Интернету hello.

Если поместить виртуальными машинами в hello одной автономной облачной службе, по-прежнему можно использовать балансировку нагрузки и группы доступности. Дополнительные сведения см. в разделе [виртуальные машины с балансировкой нагрузки](../../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) и [Управление доступностью виртуальных машин hello](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Тем не менее нельзя упорядочивать hello виртуальные машины в подсетях или подключить сеть локальной tooyour автономный облачной службы. Ниже приведен пример:

[!INCLUDE [virtual-machines-common-classic-connect-vms](../../../../includes/virtual-machines-common-classic-connect-vms.md)]

## <a name="next-steps"></a>Дальнейшие действия
После создания виртуальной машины, и он имеет смысл слишком[добавьте диск данных](attach-disk.md) , служб и рабочих нагрузок имеют toostore расположение данных.
