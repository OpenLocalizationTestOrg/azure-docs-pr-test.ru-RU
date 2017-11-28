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
# <a name="troubleshoot-allocation-failures-when-you-create-restart-or-resize-linux-vms-in-azure"></a><span data-ttu-id="965b1-103">Устранение ошибок выделения ресурсов при создании, перезагрузке или изменении размера виртуальных машин Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="965b1-103">Troubleshoot allocation failures when you create, restart, or resize Linux VMs in Azure</span></span>
<span data-ttu-id="965b1-104">После создания виртуальной Машины, перезапустите остановлена (освобождена) виртуальных машин или изменить размер виртуальной Машины Microsoft Azure выделяет вычислительные ресурсы tooyour подписки.</span><span class="sxs-lookup"><span data-stu-id="965b1-104">When you create a VM, restart stopped (deallocated) VMs, or resize a VM, Microsoft Azure allocates compute resources tooyour subscription.</span></span> <span data-ttu-id="965b1-105">Иногда может получать ошибки, при выполнении этих операций — даже в том случае, прежде чем достигнет hello ограничения подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="965b1-105">You may occasionally receive errors when performing these operations -- even before you reach hello Azure subscription limits.</span></span> <span data-ttu-id="965b1-106">В этой статье объясняется причины hello некоторых распространенных ошибок выделения hello и предлагает возможные исправления.</span><span class="sxs-lookup"><span data-stu-id="965b1-106">This article explains hello causes of some of hello common allocation failures and suggests possible remediation.</span></span> <span data-ttu-id="965b1-107">Hello сведения также можно использовать при планировании развертывания hello служб.</span><span class="sxs-lookup"><span data-stu-id="965b1-107">hello information may also be useful when you plan hello deployment of your services.</span></span> <span data-ttu-id="965b1-108">Вы также можете [устранить ошибки выделения ресурсов при создании, перезапуске или изменении размера виртуальных машин Windows в Azure](../windows/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="965b1-108">You can also [troubleshoot allocation failures when you create, restart, or resize Windows VMs in Azure](../windows/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-allocation-failure](../../../includes/virtual-machines-common-allocation-failure.md)]

