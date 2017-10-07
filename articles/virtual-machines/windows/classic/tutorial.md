---
title: "aaaCreate виртуальной Машины в hello портал Azure | Документы Microsoft"
description: "Создание виртуальной машины Windows в hello портал Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1871f823-ebd7-4eff-9a22-8e2411555595
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 3848a3d06a7ce377633db78ea385826ed40f94fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-running-windows-in-hello-azure-portal"></a>Создание виртуальной машины под управлением Windows в hello портал Azure
> [!div class="op_single_selector"]
> * [Портал Azure](tutorial.md)
> * [PowerShell: классическое развертывание](create-powershell.md)
>
>

<br>

> [!IMPORTANT]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов. Узнайте, каким образом слишком[выполните следующие действия, с помощью модели развертывания диспетчера ресурсов hello](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) с помощью hello **портал Azure**.

В этом учебнике показано как toocreate Azure виртуальной машины (VM) под управлением Windows в hello портал Azure. Мы будем использовать образ Windows Server в качестве примера, но это только один из hello многие образы Azure предлагает. Обратите внимание, что доступные образы зависят от подписки. Например изображения рабочего стола Windows может быть доступен tooMSDN подписчиков.

В этом разделе показано, как toouse hello **мониторинга** в hello Azure tooselect портала и затем создать виртуальную машину hello.

Можно также создавать виртуальные машины с помощью [собственных образов](createupload-vhd.md). toolearn об этом и других методов, в разделе [toocreate различными способами виртуальной машины Windows](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

<!-- 02/27/2017 Video removed as it was based on hello classic portal. -->

## <a id="createvirtualmachine"></a>Создание hello виртуальной машины
[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

## <a name="next-steps"></a>Дальнейшие действия
* Узнайте, каким образом слишком[создания виртуальной Машины с помощью модели развертывания диспетчера ресурсов hello](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) в hello портал Azure.
* Войдите в систему виртуальной машины toohello. Инструкции см. в разделе [вход tooa виртуальной машины под управлением Windows Server](connect-logon.md).
* Присоедините диск данных toostore. Можно присоединять пустые диски и диски с данными. Инструкции см. в разделе hello [присоединения данных диска tooa Windows виртуальную машину, созданную с помощью hello классической модели развертывания](attach-disk.md).
