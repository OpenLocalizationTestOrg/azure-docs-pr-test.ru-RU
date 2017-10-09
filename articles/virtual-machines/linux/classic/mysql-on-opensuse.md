---
title: "aaaInstall MySQL на Виртуальной машине OpenSUSE | Документы Microsoft"
description: "Узнайте, tooinstall MySQL на машине OpenSUSE Linux VMirtual в Azure."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1594e10e-c314-455a-9efb-a89441de364b
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/19/2016
ms.author: cynthn
ms.openlocfilehash: 8f96d29f29cb9c466dd7fdaf92b378783fdaacd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-mysql-on-a-virtual-machine-running-opensuse-linux-in-azure"></a><span data-ttu-id="e670f-103">Установка MySQL на виртуальной машине под управлением OpenSUSE Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="e670f-103">Install MySQL on a virtual machine running OpenSUSE Linux in Azure</span></span>
<span data-ttu-id="e670f-104">[MySQL][MySQL] является популярной базой данных SQL с открытым кодом.</span><span class="sxs-lookup"><span data-stu-id="e670f-104">[MySQL][MySQL] is a popular, open-source SQL database.</span></span> <span data-ttu-id="e670f-105">В этом учебнике показано как toocreate виртуальной машины с ОС OpenSUSE Linux, затем установите MySQL.</span><span class="sxs-lookup"><span data-stu-id="e670f-105">This tutorial shows you how toocreate a virtual machine running OpenSUSE Linux, then install MySQL.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="e670f-106">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e670f-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e670f-107">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="e670f-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="e670f-108">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e670f-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<br>

## <a name="create-a-virtual-machine-running-opensuse-linux"></a><span data-ttu-id="e670f-109">Создание виртуальной машины под управлением OpenSUSE Linux</span><span class="sxs-lookup"><span data-stu-id="e670f-109">Create a virtual machine running OpenSUSE Linux</span></span>
[!INCLUDE [create-and-configure-opensuse-vm-in-portal](../../../../includes/create-and-configure-opensuse-vm-in-portal.md)]

## <a name="install-and-run-mysql-on-hello-virtual-machine"></a><span data-ttu-id="e670f-110">Установить и запустить на виртуальной машине hello MySQL</span><span class="sxs-lookup"><span data-stu-id="e670f-110">Install and run MySQL on hello virtual machine</span></span>
[!INCLUDE [install-and-run-mysql-on-opensuse-vm](../../../../includes/install-and-run-mysql-on-opensuse-vm.md)]

## <a name="next-steps"></a><span data-ttu-id="e670f-111">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e670f-111">Next steps</span></span>
<span data-ttu-id="e670f-112">Дополнительные сведения о MySQL см. в разделе hello [документация по MySQL][MySQLDocs].</span><span class="sxs-lookup"><span data-stu-id="e670f-112">For details about MySQL, see hello [MySQL Documentation][MySQLDocs].</span></span>

[MySQLDocs]:http://dev.mysql.com/doc/index-topic.html
[MySQL]:http://www.mysql.com

