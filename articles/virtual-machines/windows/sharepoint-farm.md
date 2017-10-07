---
title: "aaaCreate ферм серверов SharePoint в Azure | Документы Microsoft"
description: "Быстро создаете новую ферму SharePoint 2013 или SharePoint 2016 в Azure с помощью hello Azure marketplace портала."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 89b124da-019d-4179-86dd-ad418d05a4f2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d71c7177d9b99cf377bab767342508007285b452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-sharepoint-server-farms-using-hello-azure-portal-marketplace"></a><span data-ttu-id="19ad7-103">Создание фермы серверов SharePoint с помощью hello Azure marketplace портала</span><span class="sxs-lookup"><span data-stu-id="19ad7-103">Create SharePoint server farms using hello Azure portal marketplace</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="sharepoint-2013-farms"></a><span data-ttu-id="19ad7-104">Фермы SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="19ad7-104">SharePoint 2013 farms</span></span>
<span data-ttu-id="19ad7-105">С помощью Microsoft Azure marketplace hello портала можно быстро создать предварительно настроенного фермы SharePoint Server 2013.</span><span class="sxs-lookup"><span data-stu-id="19ad7-105">With hello Microsoft Azure portal marketplace, you can quickly create pre-configured SharePoint Server 2013 farms.</span></span> <span data-ttu-id="19ad7-106">Такой подход может сэкономить много времени, когда в среде разработки и тестирования нужна базовая или высокодоступная ферма SharePoint или когда SharePoint Server 2013 рассматривается в качестве решения для совместной работы в рамках организации.</span><span class="sxs-lookup"><span data-stu-id="19ad7-106">This can save you a lot of time when you need a basic or high-availability SharePoint farm for a dev/test environment or if you are evaluating SharePoint Server 2013 as a collaboration solution for your organization.</span></span>

> [!NOTE]
> <span data-ttu-id="19ad7-107">Hello **фермы серверов SharePoint** был удален элемент hello Azure Marketplace hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="19ad7-107">hello **SharePoint Server Farm** item in hello Azure Marketplace of hello Azure portal has been removed.</span></span> <span data-ttu-id="19ad7-108">Он был заменен hello **фермы SharePoint 2013 не - HA** и **высокой ДОСТУПНОСТИ фермы SharePoint 2013** элементов.</span><span class="sxs-lookup"><span data-stu-id="19ad7-108">It has been replaced with hello **SharePoint 2013 non-HA Farm** and **SharePoint 2013 HA Farm** items.</span></span>
>
>

<span data-ttu-id="19ad7-109">Hello основные ферма SharePoint состоит из трех виртуальных машин в этой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="19ad7-109">hello basic SharePoint farm consists of three virtual machines in this configuration.</span></span>

![sharepointfarm](./media/sharepoint-farm/Non-HAFarm.png)

<span data-ttu-id="19ad7-111">Ферму такой конфигурации можно использовать в качестве упрощенной установки для разработки приложений SharePoint или первоначальной оценки SharePoint 2013.</span><span class="sxs-lookup"><span data-stu-id="19ad7-111">You can use this farm configuration for a simplified setup for SharePoint app development or your first-time evaluation of SharePoint 2013.</span></span>

<span data-ttu-id="19ad7-112">toocreate hello основные () SharePoint фермы с тремя серверами:</span><span class="sxs-lookup"><span data-stu-id="19ad7-112">toocreate hello basic (three-server) SharePoint farm:</span></span>

1. <span data-ttu-id="19ad7-113">Щелкните [здесь](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/).</span><span class="sxs-lookup"><span data-stu-id="19ad7-113">Click [here](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/).</span></span>
2. <span data-ttu-id="19ad7-114">Щелкните **Развернуть**.</span><span class="sxs-lookup"><span data-stu-id="19ad7-114">Click **Deploy**.</span></span>
3. <span data-ttu-id="19ad7-115">На hello **фермы SharePoint 2013 не - HA** области, нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="19ad7-115">On hello **SharePoint 2013 non-HA Farm** pane, click **Create**.</span></span>
4. <span data-ttu-id="19ad7-116">Укажите параметры на шаги hello hello **создать ферму SharePoint 2013 не - высокой НАДЕЖНОСТИ** , а затем щелкните **создать**.</span><span class="sxs-lookup"><span data-stu-id="19ad7-116">Specify settings on hello steps of hello **Create SharePoint 2013 non-HA Farm** pane, and then click **Create**.</span></span>

<span data-ttu-id="19ad7-117">ферма SharePoint Hello высокого уровня доступности состоит из девяти виртуальные машины в этой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="19ad7-117">hello high-availability SharePoint farm consists of nine virtual machines in this configuration.</span></span>

![sharepointfarm](./media/sharepoint-farm/HAFarm.png)

<span data-ttu-id="19ad7-119">Это более высокие нагрузки клиента фермы конфигурации tootest, высокий уровень доступности hello внешний сайт SharePoint и группы доступности AlwaysOn SQL Server можно использовать для фермы SharePoint.</span><span class="sxs-lookup"><span data-stu-id="19ad7-119">You can use this farm configuration tootest higher client loads, high availability of hello external SharePoint site, and SQL Server AlwaysOn Availability Groups for a SharePoint farm.</span></span> <span data-ttu-id="19ad7-120">Кроме того, такая конфигурация подходит для разработки приложений SharePoint в высокодоступной среде.</span><span class="sxs-lookup"><span data-stu-id="19ad7-120">You can also use this configuration for SharePoint app development in a high-availability environment.</span></span>

<span data-ttu-id="19ad7-121">toocreate hello высокого уровня доступности (9) SharePoint фермы с серверами:</span><span class="sxs-lookup"><span data-stu-id="19ad7-121">toocreate hello high-availability (nine-server) SharePoint farm:</span></span>

1. <span data-ttu-id="19ad7-122">Щелкните [здесь](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/).</span><span class="sxs-lookup"><span data-stu-id="19ad7-122">Click [here](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/).</span></span>
2. <span data-ttu-id="19ad7-123">Щелкните **Развернуть**.</span><span class="sxs-lookup"><span data-stu-id="19ad7-123">Click **Deploy**.</span></span>
3. <span data-ttu-id="19ad7-124">На hello **высокой ДОСТУПНОСТИ фермы SharePoint 2013** области, нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="19ad7-124">On hello **SharePoint 2013 HA Farm** pane, click **Create**.</span></span>
4. <span data-ttu-id="19ad7-125">Укажите параметры на hello семь шагов hello **создания фермы SharePoint 2013 HA** , а затем щелкните **создать**.</span><span class="sxs-lookup"><span data-stu-id="19ad7-125">Specify settings on hello seven steps of hello **Create SharePoint 2013 HA Farm** pane, and then click **Create**.</span></span>

> [!NOTE]
> <span data-ttu-id="19ad7-126">Не удается создать hello **фермы SharePoint 2013 не - HA** или **высокой ДОСТУПНОСТИ фермы SharePoint 2013** с бесплатной пробной версии Azure.</span><span class="sxs-lookup"><span data-stu-id="19ad7-126">You cannot create hello **SharePoint 2013 non-HA Farm** or **SharePoint 2013 HA Farm** with an Azure Free Trial.</span></span>
>
>

<span data-ttu-id="19ad7-127">Hello портал Azure создает оба эти фермы в виртуальной сети только для облака с веб-приложения с выходом в Интернет.</span><span class="sxs-lookup"><span data-stu-id="19ad7-127">hello Azure portal creates both of these farms in a cloud-only virtual network with an Internet-facing web presence.</span></span> <span data-ttu-id="19ad7-128">Имеется не сеть сеть VPN или ExpressRoute подключения задней tooyour организации сетей.</span><span class="sxs-lookup"><span data-stu-id="19ad7-128">There is no site-to-site VPN or ExpressRoute connection back tooyour organization network.</span></span>

> [!NOTE]
> <span data-ttu-id="19ad7-129">При создании hello основные или фермах SharePoint высокого уровня доступности с помощью hello портал Azure, нельзя указать существующую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="19ad7-129">When you create hello basic or high-availability SharePoint farms using hello Azure portal, you cannot specify an existing resource group.</span></span> <span data-ttu-id="19ad7-130">toowork обойти это ограничение, создайте эти ферм с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="19ad7-130">toowork around this limitation, create these farms with Azure PowerShell.</span></span> <span data-ttu-id="19ad7-131">Дополнительные сведения см. в разделе [Создание ферм разработки и тестирования SharePoint 2013 с помощью Azure PowerShell](https://technet.microsoft.com/library/mt743093.aspx#powershell).</span><span class="sxs-lookup"><span data-stu-id="19ad7-131">For more information, see [Create SharePoint 2013 dev/test farms with Azure PowerShell](https://technet.microsoft.com/library/mt743093.aspx#powershell).</span></span>
>
>

## <a name="sharepoint-2016-farms"></a><span data-ttu-id="19ad7-132">Фермы SharePoint 2016</span><span class="sxs-lookup"><span data-stu-id="19ad7-132">SharePoint 2016 farms</span></span>
<span data-ttu-id="19ad7-133">В разделе [в этой статье](https://technet.microsoft.com/library/mt723354.aspx) hello инструкции toobuild hello после одного сервера SharePoint Server 2016 фермы.</span><span class="sxs-lookup"><span data-stu-id="19ad7-133">See [this article](https://technet.microsoft.com/library/mt723354.aspx) for hello instructions toobuild hello following single-server SharePoint Server 2016 farm.</span></span>

![sharepointfarm](./media/sharepoint-farm/SP2016Farm.png)

## <a name="managing-hello-sharepoint-farms"></a><span data-ttu-id="19ad7-135">Управление фермами hello</span><span class="sxs-lookup"><span data-stu-id="19ad7-135">Managing hello SharePoint farms</span></span>
<span data-ttu-id="19ad7-136">Администрирование серверов hello этих ферм через подключения удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="19ad7-136">You can administer hello servers of these farms through Remote Desktop connections.</span></span> <span data-ttu-id="19ad7-137">Дополнительные сведения см. в разделе [входа на виртуальную машину toohello](quick-create-portal.md#connect-to-virtual-machine).</span><span class="sxs-lookup"><span data-stu-id="19ad7-137">For more information, see [Log on toohello virtual machine](quick-create-portal.md#connect-to-virtual-machine).</span></span>

<span data-ttu-id="19ad7-138">С сайта центра администрирования SharePoint hello можно настроить узлы, приложения SharePoint и другие функциональные возможности.</span><span class="sxs-lookup"><span data-stu-id="19ad7-138">From hello Central Administration SharePoint site, you can configure My sites, SharePoint applications, and other functionality.</span></span> <span data-ttu-id="19ad7-139">Дополнительные сведения см. в статье [Настройка SharePoint 2013](http://technet.microsoft.com/library/ee836142.aspx).</span><span class="sxs-lookup"><span data-stu-id="19ad7-139">For more information, see [Configure SharePoint](http://technet.microsoft.com/library/ee836142.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="19ad7-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="19ad7-140">Next steps</span></span>
* <span data-ttu-id="19ad7-141">Ознакомьтесь с дополнительными [конфигурациями SharePoint](https://technet.microsoft.com/library/dn635309.aspx) в службах инфраструктуры Azure.</span><span class="sxs-lookup"><span data-stu-id="19ad7-141">Discover additional [SharePoint configurations](https://technet.microsoft.com/library/dn635309.aspx) in Azure infrastructure services.</span></span>
