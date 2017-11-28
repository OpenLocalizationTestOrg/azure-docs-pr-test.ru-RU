---
title: "Технические компоненты, необходимые для создания образа виртуальной машины для Azure Marketplace | Документация Майкрософт"
description: "Ознакомьтесь с требованиями по созданию и разработке образа виртуальной машины для Azure Marketplace, предназначенного для продажи."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 63c16966-0304-4b17-a715-368a0a5ccb2c
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: af3e2ad623d8d7bfafe676411f9ae3fbee78aab8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="technical-prerequisites-for-creating-a-virtual-machine-image-for-the-azure-marketplace"></a><span data-ttu-id="1b44a-103">Технические компоненты, необходимые для создания образа виртуальной машины для Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="1b44a-103">Technical prerequisites for creating a virtual machine image for the Azure Marketplace</span></span>
<span data-ttu-id="1b44a-104">Прежде чем начать работу, внимательно прочтите описание и разберитесь, где и зачем выполняется каждый шаг.</span><span class="sxs-lookup"><span data-stu-id="1b44a-104">Read the process thoroughly before beginning and understand where and why each step is performed.</span></span> <span data-ttu-id="1b44a-105">Постарайтесь подготовить максимально подробные сведения о своей компании и другие данные, загрузить необходимые средства и/или создать технические компоненты до того, как начнете создавать предложение.</span><span class="sxs-lookup"><span data-stu-id="1b44a-105">As much as possible, you should prepare your company information and other data, download necessary tools, and/or create technical components before beginning the offer creation process.</span></span> <span data-ttu-id="1b44a-106">Все эти компоненты описаны в данной статье.</span><span class="sxs-lookup"><span data-stu-id="1b44a-106">These items should be clear from reviewing this article.</span></span>  

## <a name="download-needed-tools--applications"></a><span data-ttu-id="1b44a-107">Загрузка необходимых средств и приложений</span><span class="sxs-lookup"><span data-stu-id="1b44a-107">Download needed tools & applications</span></span>
<span data-ttu-id="1b44a-108">К началу работу необходимо подготовить следующее:</span><span class="sxs-lookup"><span data-stu-id="1b44a-108">You should have the following items ready before beginning the process:</span></span>

* <span data-ttu-id="1b44a-109">в зависимости от целевой операционной системы установите [командлеты Azure PowerShell](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WindowsAzurePowershellGet.3f.3f.3fnew.appids) или [программу командной строки Linux](https://go.microsoft.com/fwlink/?LinkId=253472&clcid=0x409) со страницы [Загрузки](https://azure.microsoft.com/downloads/);</span><span class="sxs-lookup"><span data-stu-id="1b44a-109">Depending on which operating system you are targeting, install the [Azure PowerShell cmdlets](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WindowsAzurePowershellGet.3f.3f.3fnew.appids) or [Linux command-line interface tool](https://go.microsoft.com/fwlink/?LinkId=253472&clcid=0x409) from the [Azure Downloads](https://azure.microsoft.com/downloads/) page.</span></span>
* <span data-ttu-id="1b44a-110">установите Azure Storage Explorer из CodePlex;</span><span class="sxs-lookup"><span data-stu-id="1b44a-110">Install Azure Storage Explorer from CodePlex.</span></span>
* <span data-ttu-id="1b44a-111">скачайте и установите средство проверки сертификации для Azure Certified:</span><span class="sxs-lookup"><span data-stu-id="1b44a-111">Download and install the Certification Test Tool for Azure Certified:</span></span>
  * <span data-ttu-id="1b44a-112">[http://go.microsoft.com/fwlink/?LinkID=526913](http://go.microsoft.com/fwlink/?LinkID=526913).</span><span class="sxs-lookup"><span data-stu-id="1b44a-112">[http://go.microsoft.com/fwlink/?LinkID=526913](http://go.microsoft.com/fwlink/?LinkID=526913).</span></span> <span data-ttu-id="1b44a-113">Для запуска инструмента сертификации потребуется компьютер под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="1b44a-113">You need a Windows-based computer to run the certification tool.</span></span> <span data-ttu-id="1b44a-114">Если у вас нет такого компьютера, запустите средство сертификации на виртуальной машине Windows в Azure.</span><span class="sxs-lookup"><span data-stu-id="1b44a-114">If you do not have a Windows-based computer available, you can run the tool using a Windows-based VM in Azure.</span></span>

## <a name="platforms-supported"></a><span data-ttu-id="1b44a-115">Поддерживаемые платформы</span><span class="sxs-lookup"><span data-stu-id="1b44a-115">Platforms supported</span></span>
<span data-ttu-id="1b44a-116">Виртуальные машины Azure можно разрабатывать на базе Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="1b44a-116">You can develop Azure-based VMs on Windows or Linux.</span></span> <span data-ttu-id="1b44a-117">На некоторых этапах публикации, например при создании виртуального жесткого диска (VHD), совместимого с Azure, используемые инструменты и выполняемые действия зависят от операционной системы.</span><span class="sxs-lookup"><span data-stu-id="1b44a-117">Some elements of the publishing process--such as creating an Azure-compatible virtual hard disk (VHD)--use different tools and steps depending on which operating system you are using:</span></span>  

* <span data-ttu-id="1b44a-118">При использовании операционной системы Linux см. раздел "Создание виртуального жесткого диска, совместимого с Azure (для Linux)" [руководства по публикации образов виртуальных машин](marketplace-publishing-vm-image-creation.md).</span><span class="sxs-lookup"><span data-stu-id="1b44a-118">If you are using Linux, refer to the “Create an Azure-compatible VHD (Linux-based)” section of the [Virtual machine image publishing guide](marketplace-publishing-vm-image-creation.md).</span></span>
* <span data-ttu-id="1b44a-119">При использовании операционной системы Windows см. раздел "Создание виртуального жесткого диска, совместимого с Azure (на основе Windows)" [руководства по публикации образов виртуальных машин](marketplace-publishing-vm-image-creation.md).</span><span class="sxs-lookup"><span data-stu-id="1b44a-119">If you are using Windows, refer to the “Create an Azure-compatible VHD (Windows-based)” section of the [Virtual machine image publishing guide](marketplace-publishing-vm-image-creation.md).</span></span>

> [!NOTE]
> <span data-ttu-id="1b44a-120">Доступ к компьютеру под управлением Windows необходим для:</span><span class="sxs-lookup"><span data-stu-id="1b44a-120">You need access to a Windows-based machine to:</span></span>
> 
> * <span data-ttu-id="1b44a-121">запуска инструмента проверки сертификации;</span><span class="sxs-lookup"><span data-stu-id="1b44a-121">Run the certification validation tool.</span></span>
> * <span data-ttu-id="1b44a-122">создания подписанного URL-адреса VHD для передачи сертификации VHD.</span><span class="sxs-lookup"><span data-stu-id="1b44a-122">Create the VHD shared access signature URL for the VHD certification submission.</span></span>
> 
> 

## <a name="develop-your-vhd"></a><span data-ttu-id="1b44a-123">Разработка VHD</span><span class="sxs-lookup"><span data-stu-id="1b44a-123">Develop your VHD</span></span>
<span data-ttu-id="1b44a-124">Диски VHD Azure можно разрабатывать в облаке или локально.</span><span class="sxs-lookup"><span data-stu-id="1b44a-124">You can develop Azure VHDs in the cloud or on-premises:</span></span>

* <span data-ttu-id="1b44a-125">Разработка в облаке означает, что все этапы разработки выполняются удаленно на VHD, который находится в Azure.</span><span class="sxs-lookup"><span data-stu-id="1b44a-125">Cloud-based development means all development steps are performed remotely on a VHD resident on Azure.</span></span>
* <span data-ttu-id="1b44a-126">Для локальной разработки VHD необходимо загрузить и разработать в локальной инфраструктуре.</span><span class="sxs-lookup"><span data-stu-id="1b44a-126">On-premises development requires downloading a VHD and developing it using on-premises infrastructure.</span></span> <span data-ttu-id="1b44a-127">Такой вариант возможен, но не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="1b44a-127">Although this is possible, we do not recommend it.</span></span> <span data-ttu-id="1b44a-128">Обратите внимание на то, что локальная разработка для Windows и SQL требует соответствующих локальных лицензионных ключей.</span><span class="sxs-lookup"><span data-stu-id="1b44a-128">Note that developing for Windows or SQL on-premises requires you to have the relevant on-premises license keys.</span></span> <span data-ttu-id="1b44a-129">Невозможно добавить или установить SQL Server после создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="1b44a-129">You cannot include or install SQL Server after creating a VM.</span></span> <span data-ttu-id="1b44a-130">Кроме того, в вашем предложении должен использоваться утвержденный образ SQL с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="1b44a-130">You must also base your offer on an approved SQL image from the Azure portal.</span></span> <span data-ttu-id="1b44a-131">При выборе локальной разработки некоторые действия нужно будет выполнить не так, как при разработке в облаке.</span><span class="sxs-lookup"><span data-stu-id="1b44a-131">If you decide to develop on-premises, you must perform some steps differently than if you were developing in the cloud.</span></span> <span data-ttu-id="1b44a-132">Соответствующие сведения см. в статье [Локальная разработка образа виртуальной машины для Azure Marketplace](marketplace-publishing-vm-image-creation-on-premise.md).</span><span class="sxs-lookup"><span data-stu-id="1b44a-132">You can find relevant information in [Create an on-premises VM image](marketplace-publishing-vm-image-creation-on-premise.md).</span></span>

[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
