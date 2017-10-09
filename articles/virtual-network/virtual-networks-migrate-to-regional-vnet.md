---
title: "aaaMigrate виртуальной сети Azure (классические) из области территориальная группа tooa | Документы Microsoft"
description: "Узнайте, как toomigrate виртуальной сети (классической) из территориальной группы tooa области."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 84febcb9-bb8b-4e79-ab91-865ad9de41cb
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: e3a5c0f21e748912e29e2e8d03f4295720e63637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-a-virtual-network-classic-from-an-affinity-group-tooa-region"></a><span data-ttu-id="3982e-103">Миграция виртуальной сети (классические) из области tooa территориальная группа</span><span class="sxs-lookup"><span data-stu-id="3982e-103">Migrate a virtual network (classic) from an affinity group tooa region</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3982e-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3982e-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="3982e-105">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="3982e-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="3982e-106">Корпорация Майкрософт рекомендует наиболее новые развертывания модели развертывания диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="3982e-106">Microsoft recommends that most new deployments use hello Resource Manager deployment model.</span></span>

<span data-ttu-id="3982e-107">Территориальные группы убедитесь, что ресурсы создана в одной территориальной группе физически размещенные на серверах, которые находятся рядом друг с другом, включение toocommunicate эти ресурсы быстрее hello.</span><span class="sxs-lookup"><span data-stu-id="3982e-107">Affinity groups ensure that resources created within hello same affinity group are physically hosted by servers that are close together, enabling these resources toocommunicate quicker.</span></span> <span data-ttu-id="3982e-108">В прошлом hello Территориальные группы требовались для создания виртуальных сетей (классические).</span><span class="sxs-lookup"><span data-stu-id="3982e-108">In hello past, affinity groups were a requirement for creating virtual networks (classic).</span></span> <span data-ttu-id="3982e-109">В это время служба диспетчера сети hello, управляет виртуальными сетями (классические) могла работать только в набор физических серверов или единице масштабирования.</span><span class="sxs-lookup"><span data-stu-id="3982e-109">At that time, hello network manager service that managed virtual networks (classic) could only work within a set of physical servers or scale unit.</span></span> <span data-ttu-id="3982e-110">Архитектурные усовершенствования расширили область hello tooa области сетевого управления.</span><span class="sxs-lookup"><span data-stu-id="3982e-110">Architectural improvements have increased hello scope of network management tooa region.</span></span>

<span data-ttu-id="3982e-111">В результате этих усовершенствований необходимость в наличии территориальных групп для виртуальных сетей (классических) отпала.</span><span class="sxs-lookup"><span data-stu-id="3982e-111">As a result of these architectural improvements, affinity groups are no longer recommended, or required for virtual networks (classic).</span></span> <span data-ttu-id="3982e-112">Hello использование территориальных групп для виртуальных сетей (классические) заменяется областей.</span><span class="sxs-lookup"><span data-stu-id="3982e-112">hello use of affinity groups for virtual networks (classic) is replaced by regions.</span></span> <span data-ttu-id="3982e-113">Классические виртуальные сети, связанные с регионами, называются региональными.</span><span class="sxs-lookup"><span data-stu-id="3982e-113">Virtual networks (classic) that are associated with regions are called regional virtual networks.</span></span>

<span data-ttu-id="3982e-114">Территориальные группы не рекомендуется использовать вообще.</span><span class="sxs-lookup"><span data-stu-id="3982e-114">We recommend that you don't use affinity groups in general.</span></span> <span data-ttu-id="3982e-115">Помимо требований виртуальной сети hello Территориальные группы было также важно toouse tooensure ресурсы, такие как вычислений (классические) и хранилища (классические), были помещены рядом друг с другом.</span><span class="sxs-lookup"><span data-stu-id="3982e-115">Aside from hello virtual network requirement, affinity groups were also important toouse tooensure resources, such as compute (classic) and storage (classic), were placed near each other.</span></span> <span data-ttu-id="3982e-116">Однако с текущей архитектурой сети Azure hello, эти требования к размещению более не нужны.</span><span class="sxs-lookup"><span data-stu-id="3982e-116">However, with hello current Azure network architecture, these placement requirements are no longer necessary.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3982e-117">Хотя по-прежнему технически возможно toocreate виртуальной сети, которая связана с группой сходства, нет без веских причин toodo таким образом.</span><span class="sxs-lookup"><span data-stu-id="3982e-117">Although it is still technically possible toocreate a virtual network that is associated with an affinity group, there is no compelling reason toodo so.</span></span> <span data-ttu-id="3982e-118">Многие возможности виртуальных сетей, в частности группы безопасности сети, доступны только при использовании региональной виртуальной сети и недоступны для виртуальных сетей, связанных с территориальными группами.</span><span class="sxs-lookup"><span data-stu-id="3982e-118">Many virtual network features, such as network security groups, are only available when using a regional virtual network, and are not available for virtual networks that are associated with affinity groups.</span></span>
> 
> 

## <a name="edit-hello-network-configuration-file"></a><span data-ttu-id="3982e-119">Изменение файла конфигурации сети hello</span><span class="sxs-lookup"><span data-stu-id="3982e-119">Edit hello network configuration file</span></span>

1. <span data-ttu-id="3982e-120">Экспортируйте файл конфигурации сети hello.</span><span class="sxs-lookup"><span data-stu-id="3982e-120">Export hello network configuration file.</span></span> <span data-ttu-id="3982e-121">toolearn как текстовый файл с помощью PowerShell или hello Azure командной строки (CLI) 1.0, tooexport конфигурации сети в разделе [настройки виртуальной сети, с помощью файла конфигурации сети](virtual-networks-using-network-configuration-file.md#export).</span><span class="sxs-lookup"><span data-stu-id="3982e-121">toolearn how tooexport a network configuration file using PowerShell or hello Azure command-line interface (CLI) 1.0, see [Configure a virtual network using a network configuration file](virtual-networks-using-network-configuration-file.md#export).</span></span>
2. <span data-ttu-id="3982e-122">Изменение файла конфигурации сети hello, заменив **AffinityGroup** с **расположение**.</span><span class="sxs-lookup"><span data-stu-id="3982e-122">Edit hello network configuration file, replacing **AffinityGroup** with **Location**.</span></span> <span data-ttu-id="3982e-123">В качестве значения параметра **Location** следует указать [регион](https://azure.microsoft.com/regions) Azure.</span><span class="sxs-lookup"><span data-stu-id="3982e-123">You specify an Azure [region](https://azure.microsoft.com/regions) for **Location**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="3982e-124">Hello **расположение** — hello область, указанная для hello территориальную группу, которая связана с виртуальной сети (классические).</span><span class="sxs-lookup"><span data-stu-id="3982e-124">hello **Location** is hello region that you specified for hello affinity group that is associated with your virtual network (classic).</span></span> <span data-ttu-id="3982e-125">Например, если виртуальной сети (классические) связан с территориальной группой, расположенной на Западе США при выполнении миграции вашей **расположение** должен указывать tooWest США.</span><span class="sxs-lookup"><span data-stu-id="3982e-125">For example, if your virtual network (classic) is associated with an affinity group that is located in West US, when you migrate, your **Location** must point tooWest US.</span></span> 
   > 
   > 
   
    <span data-ttu-id="3982e-126">Измените hello следующие строки в файле конфигурации сети, заменив значения hello собственные.</span><span class="sxs-lookup"><span data-stu-id="3982e-126">Edit hello following lines in your network configuration file, replacing hello values with your own:</span></span> 
   
    <span data-ttu-id="3982e-127">**Старое значение:** \<VirtualNetworkSitename="VNetUSWest" AffinityGroup="VNetDemoAG"\>.</span><span class="sxs-lookup"><span data-stu-id="3982e-127">**Old value:** \<VirtualNetworkSitename="VNetUSWest" AffinityGroup="VNetDemoAG"\></span></span> 
   
    <span data-ttu-id="3982e-128">**Новое значение:** \<VirtualNetworkSitename="VNetUSWest" Location="West US"\>.</span><span class="sxs-lookup"><span data-stu-id="3982e-128">**New value:** \<VirtualNetworkSitename="VNetUSWest" Location="West US"\></span></span>
3. <span data-ttu-id="3982e-129">Сохранить изменения и [импорта](virtual-networks-using-network-configuration-file.md#import) hello tooAzure конфигурации сети.</span><span class="sxs-lookup"><span data-stu-id="3982e-129">Save your changes and [import](virtual-networks-using-network-configuration-file.md#import) hello network configuration tooAzure.</span></span>

> [!NOTE]
> <span data-ttu-id="3982e-130">Этот вид миграции не вызывает простоев tooyour служб.</span><span class="sxs-lookup"><span data-stu-id="3982e-130">This migration does NOT cause any downtime tooyour services.</span></span>
> 
> 

## <a name="what-toodo-if-you-have-a-vm-classic-in-an-affinity-group"></a><span data-ttu-id="3982e-131">Какие toodo при наличии виртуальной Машины (классические) в территориальной группе</span><span class="sxs-lookup"><span data-stu-id="3982e-131">What toodo if you have a VM (classic) in an affinity group</span></span>
<span data-ttu-id="3982e-132">Виртуальные машины (классические), которые в настоящее время в территориальной группе не обязательно toobe удалены из hello территориальную группу.</span><span class="sxs-lookup"><span data-stu-id="3982e-132">VMs (classic) that are currently in an affinity group do not need toobe removed from hello affinity group.</span></span> <span data-ttu-id="3982e-133">После развертывания виртуальной Машины это развернутой tooa одну единицу масштабирования.</span><span class="sxs-lookup"><span data-stu-id="3982e-133">Once a VM is deployed, it is deployed tooa single scale unit.</span></span> <span data-ttu-id="3982e-134">Территориальные группы могут ограничить hello набор доступных размеров ВМ для нового развертывания виртуальной Машины, но не были ограничены существующей виртуальной Машине, развернутой toohello набор виртуальных Машин размеров, доступных в единице масштабирования hello, в какие hello развертывания ВМ.</span><span class="sxs-lookup"><span data-stu-id="3982e-134">Affinity groups can restrict hello set of available VM sizes for a new VM deployment, but any existing VM that is deployed is already restricted toohello set of VM sizes available in hello scale unit in which hello VM is deployed.</span></span> <span data-ttu-id="3982e-135">Поскольку hello виртуальная машина уже развернут tooa единица масштабирования, удаление виртуальной Машины из территориальной группы не оказывает влияния на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="3982e-135">Because hello VM is already deployed tooa scale unit, removing a VM from an affinity group has no effect on hello VM.</span></span>
