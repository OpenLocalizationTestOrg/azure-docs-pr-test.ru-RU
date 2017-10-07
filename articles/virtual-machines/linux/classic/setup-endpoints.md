---
title: "aaaSet копирование конечные точки в классической виртуальной Машины Linux | Документы Microsoft"
description: "Узнайте tooset настройке конечных точек для виртуальной Машины Linux в hello Azure классического портала tooallow связи с виртуальной машины Linux в Azure"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f3749738-1109-4a1d-8635-40e4bd220e91
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: 1c959d10dd1e20228fa4a20e1cc0205c1d12f185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-linux-classic-virtual-machine-in-azure"></a>Как tooset копирование конечные точки в классической виртуальной машины Linux в Azure
Все виртуальные машины Linux, созданных в Azure с помощью hello классической модели развертывания могут автоматически взаимодействовать через канал частной сети с другими виртуальными машинами в hello, же облака службы или виртуальной сети. Однако hello Интернет или другими виртуальными сетями компьютеров требуется конечные точки toodirect hello входящего сетевого трафика tooa виртуальной машины. Также доступна версия этой статьи для [виртуальных машин Windows](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

> [!IMPORTANT]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.

В hello **диспетчера ресурсов** модель развертывания, настройки конечных точек с помощью **группы безопасности сети (Nsg)**. Дополнительные сведения см. в статье [Открытие портов и конечных точек](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

При создании виртуальной машины Linux в hello портал Azure конечной точки для Secure Shell (SSH) обычно создается автоматически. При создании виртуальной машины hello, либо уже после этого при необходимости можно настроить дополнительные конечные точки.

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a>Дальнейшие действия
* Можно также создать конечную точку виртуальной Машины с помощью hello [интерфейса командной строки Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2). Запустите hello **конечную точку виртуальной машины Windows azure, создайте** команды.
* При создании виртуальной машины в модели развертывания диспетчера ресурсов hello hello Azure CLI в режим диспетчера ресурсов можно использовать слишком[создавать группы безопасности сети](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) toohello toocontrol трафик виртуальной Машины.
