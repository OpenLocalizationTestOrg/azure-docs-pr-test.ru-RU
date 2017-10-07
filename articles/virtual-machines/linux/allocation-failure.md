---
title: "aaaTroubleshooting ВМ Linux ошибок выделения | Документы Microsoft"
description: "Устраните ошибки выделения ресурсов при создании, перезагрузке или изменении размера виртуальных машин Linux в Azure."
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue,azure-resourece-manager,azure-service-management
ms.assetid: 1ef41144-6dd6-4a56-b180-9d8b3d05eae7
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2016
ms.author: cjiang
ms.openlocfilehash: 502fbb406b0b4acf086c2586795f69a44cc1a004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-allocation-failures-when-you-create-restart-or-resize-linux-vms-in-azure"></a>Устранение ошибок выделения ресурсов при создании, перезагрузке или изменении размера виртуальных машин Linux в Azure
После создания виртуальной Машины, перезапустите остановлена (освобождена) виртуальных машин или изменить размер виртуальной Машины Microsoft Azure выделяет вычислительные ресурсы tooyour подписки. Иногда может получать ошибки, при выполнении этих операций — даже в том случае, прежде чем достигнет hello ограничения подписки Azure. В этой статье объясняется причины hello некоторых распространенных ошибок выделения hello и предлагает возможные исправления. Hello сведения также можно использовать при планировании развертывания hello служб. Вы также можете [устранить ошибки выделения ресурсов при создании, перезапуске или изменении размера виртуальных машин Windows в Azure](../windows/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

[!INCLUDE [virtual-machines-common-allocation-failure](../../../includes/virtual-machines-common-allocation-failure.md)]

