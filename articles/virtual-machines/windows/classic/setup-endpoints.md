---
title: "aaaSet копирование конечные точки в классической виртуальной Машине Windows | Документы Microsoft"
description: "Узнайте tooset настройке конечных точек для виртуальной Машины Windows в hello Azure классического портала tooallow связи с виртуальной машины Windows в Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 8afc21c2-d3fb-43a3-acce-aa06be448bb6
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: e817076f16d3a245a8d19add7b2f2cf5e3baa17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-classic-windows-virtual-machine-in-azure"></a>Как tooset копирование конечные точки в классической виртуальной машине в Azure
Все виртуальные машины, создаваемые в Azure с помощью hello классической модели развертывания, могут автоматически взаимодействовать через канал частной сети с другими виртуальными машинами в Windows hello одной облачной службе или виртуальной сети. Однако hello Интернет или другими виртуальными сетями компьютеров требуется конечные точки toodirect hello входящего сетевого трафика tooa виртуальной машины. Также доступна версия этой статьи для [виртуальных машин Linux](../../linux/classic/setup-endpoints.md).

> [!IMPORTANT]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.

В hello **диспетчера ресурсов** модель развертывания, настройки конечных точек с помощью **группы безопасности сети (Nsg)**. Дополнительные сведения см. в разделе [разрешить внешний доступ tooyour виртуальной Машины с помощью портала Azure "hello"](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

При создании виртуальной машины Windows в hello портал Azure общие конечные точки, как и для удаленного рабочего стола и удаленного взаимодействия Windows PowerShell обычно создаются автоматически. При создании виртуальной машины hello, либо уже после этого при необходимости можно настроить дополнительные конечные точки.

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a>Дальнейшие действия
* toouse tooset командлет Azure PowerShell копирование конечной точки виртуальной Машины в разделе [Add-AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).
* toouse toomanage командлет Azure PowerShell ACL для конечной точки, в разделе [управление списки управления доступом (ACL) для конечных точек с помощью PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).
* При создании виртуальной машины в модели развертывания диспетчера ресурсов hello Azure PowerShell можно использовать слишком[создавать группы безопасности сети](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) toohello toocontrol трафик виртуальной Машины.
