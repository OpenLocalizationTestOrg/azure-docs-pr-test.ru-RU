---
title: "в классической виртуальной Машине Linux с помощью aaaCreate hello Azure CLI 1.0 | Документы Microsoft"
description: "Узнайте, как toocreate виртуальной машины Linux с использованием hello Azure CLI 1.0 hello классической модели развертывания"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: f8071a2e-ed91-4f77-87d9-519a37e5364f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 5c3c54e5d1444a79e8e609c76d04a3a621c8d03f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-classic-linux-vm-with-hello-azure-cli-10"></a><span data-ttu-id="f439d-103">Как tooCreate в классической виртуальной Машины Linux с hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="f439d-103">How tooCreate a Classic Linux VM with hello Azure CLI 1.0</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="f439d-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f439d-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f439d-105">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="f439d-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="f439d-106">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f439d-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="f439d-107">Hello диспетчера ресурсов версию в разделе [здесь](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f439d-107">For hello Resource Manager version, see [here](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="f439d-108">В этом разделе описывается, как toocreate виртуальной машины (VM) Linux с использованием hello Azure CLI 1.0 hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="f439d-108">This topic describes how toocreate a Linux virtual machine (VM) with hello Azure CLI 1.0 using hello Classic deployment model.</span></span> <span data-ttu-id="f439d-109">Мы используем образа Linux из доступных hello **ИЗОБРАЖЕНИЯ** в Azure.</span><span class="sxs-lookup"><span data-stu-id="f439d-109">We use a Linux image from hello available **IMAGES** on Azure.</span></span> <span data-ttu-id="f439d-110">команды, Hello Azure CLI 1.0 дают hello следующие варианты конфигурации, в частности:</span><span class="sxs-lookup"><span data-stu-id="f439d-110">hello Azure CLI 1.0 commands give hello following configuration choices, among others:</span></span>

* <span data-ttu-id="f439d-111">Подключение hello ВМ tooa виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="f439d-111">Connecting hello VM tooa virtual network</span></span>
* <span data-ttu-id="f439d-112">Добавление hello tooan существующие облачная служба виртуальных Машин</span><span class="sxs-lookup"><span data-stu-id="f439d-112">Adding hello VM tooan existing cloud service</span></span>
* <span data-ttu-id="f439d-113">Добавление hello tooan существующего хранилища учетную запись виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="f439d-113">Adding hello VM tooan existing storage account</span></span>
* <span data-ttu-id="f439d-114">Добавление группы доступности tooan Виртуальной hello или расположение</span><span class="sxs-lookup"><span data-stu-id="f439d-114">Adding hello VM tooan availability set or location</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f439d-115">Если вы хотите toouse вашей виртуальной Машины виртуальной сети, для подключения tooit напрямую по имени узла или набор подключений между организациями, убедитесь, что при создании виртуальной Машины hello, укажите hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="f439d-115">If you want your VM toouse a virtual network so you can connect tooit directly by hostname or set up cross-premises connections, make sure you specify hello virtual network when you create hello VM.</span></span> <span data-ttu-id="f439d-116">Виртуальная машина может быть настроенный toojoin виртуальной сети только при создании виртуальной Машины hello.</span><span class="sxs-lookup"><span data-stu-id="f439d-116">A VM can be configured toojoin a virtual network only when you create hello VM.</span></span> <span data-ttu-id="f439d-117">Дополнительную информацию о виртуальных сетях см. в разделе [Обзор виртуальных сетей Azure](http://go.microsoft.com/fwlink/p/?LinkID=294063).</span><span class="sxs-lookup"><span data-stu-id="f439d-117">For details on virtual networks, see [Azure Virtual Network Overview](http://go.microsoft.com/fwlink/p/?LinkID=294063).</span></span>
> 
> 

## <a name="how-toocreate-a-linux-vm-using-hello-classic-deployment-model"></a><span data-ttu-id="f439d-118">Как toocreate в виртуальной Машине Linux с помощью hello классической модели развертывания</span><span class="sxs-lookup"><span data-stu-id="f439d-118">How toocreate a Linux VM using hello Classic deployment model</span></span>
[!INCLUDE [virtual-machines-create-LinuxVM](../../../../includes/virtual-machines-create-linuxvm.md)]

