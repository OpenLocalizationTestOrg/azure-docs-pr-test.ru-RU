---
title: "aaaCreate полное доменное имя для виртуальной Машины Windows в hello портал Azure | Документы Microsoft"
description: "Узнайте, как toocreate полное доменное имя или полное доменное имя, для диспетчера ресурсов на основе виртуальной машины в hello портал Azure."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a2ae5887-76df-485e-ae19-0efd96df8600
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 67c817ec97073803e513bc41ebde67b75ced565e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-qualified-domain-name-in-hello-azure-portal-for-a-windows-vm"></a>Создание полного доменного имени в hello портал Azure для виртуальной Машины Windows.

При создании виртуальной машины (VM) в hello [портал Azure](https://portal.azure.com), открытому ресурсу IP для hello виртуальной машины создается автоматически. Можно использовать этот IP адрес tooremotely доступа hello виртуальной Машины. Несмотря на то, что портал hello не приводит к созданию [полного доменного имени](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), или полное доменное имя, его можно создать после hello виртуальной Машины. В этой статье демонстрируется toocreate hello действия DNS-имя или полное доменное имя.

## <a name="create-a-fqdn"></a>Создание полного доменного имени
Для работы с руководством требуется виртуальная машина. При необходимости вы можете [создания виртуальной Машины на портале hello](quick-create-portal.md) или [с помощью Azure PowerShell](quick-create-powershell.md). Когда виртуальная машина будет готова, выполните следующие действия:

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

Теперь можно удаленно подключиться toohello виртуальную Машину с помощью этого DNS-имя как для протокола удаленного рабочего стола (RDP).

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда у виртуальной машины имеется общедоступный IP-адрес и DNS-имя, можно развернуть общие программные платформы или службы, такие как IIS, SQL или SharePoint.

Изучите дополнительные сведения об [использовании Resource Manager](../../azure-resource-manager/resource-group-overview.md), чтобы получить советы по созданию развертываний Azure.

