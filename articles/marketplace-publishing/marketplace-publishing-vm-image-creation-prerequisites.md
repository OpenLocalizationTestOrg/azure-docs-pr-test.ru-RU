---
title: "aaaTechnical предварительные условия для создания образа виртуальной машины для hello Azure Marketplace | Документы Microsoft"
description: "Сведения о требованиях hello для создания и развертывания toohello образ виртуальной машины Azure Marketplace для других toopurchase."
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
ms.openlocfilehash: fcae4d9e052581e3c1dfe7962e6d50ec31040419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="technical-prerequisites-for-creating-a-virtual-machine-image-for-hello-azure-marketplace"></a><span data-ttu-id="30cb6-103">Технические предварительные условия для создания образа виртуальной машины для hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="30cb6-103">Technical prerequisites for creating a virtual machine image for hello Azure Marketplace</span></span>
<span data-ttu-id="30cb6-104">Чтение hello процесса тщательно перед началом и понять, где и почему каждого шага выполняются.</span><span class="sxs-lookup"><span data-stu-id="30cb6-104">Read hello process thoroughly before beginning and understand where and why each step is performed.</span></span> <span data-ttu-id="30cb6-105">Настолько, насколько возможно, вы должны подготовить сведения о компании и другие данные, загрузить необходимые средства и перед началом процесса создания предложения hello создать технические компоненты.</span><span class="sxs-lookup"><span data-stu-id="30cb6-105">As much as possible, you should prepare your company information and other data, download necessary tools, and/or create technical components before beginning hello offer creation process.</span></span> <span data-ttu-id="30cb6-106">Все эти компоненты описаны в данной статье.</span><span class="sxs-lookup"><span data-stu-id="30cb6-106">These items should be clear from reviewing this article.</span></span>  

## <a name="download-needed-tools--applications"></a><span data-ttu-id="30cb6-107">Загрузка необходимых средств и приложений</span><span class="sxs-lookup"><span data-stu-id="30cb6-107">Download needed tools & applications</span></span>
<span data-ttu-id="30cb6-108">Должно быть hello следующих элементов готов до начала процесса hello:</span><span class="sxs-lookup"><span data-stu-id="30cb6-108">You should have hello following items ready before beginning hello process:</span></span>

* <span data-ttu-id="30cb6-109">В зависимости от операционной системы в качестве цели, установка hello [командлетов Azure PowerShell](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WindowsAzurePowershellGet.3f.3f.3fnew.appids) или [средство командной строки Linux](https://go.microsoft.com/fwlink/?LinkId=253472&clcid=0x409) из hello [загрузки Azure](https://azure.microsoft.com/downloads/) страница.</span><span class="sxs-lookup"><span data-stu-id="30cb6-109">Depending on which operating system you are targeting, install hello [Azure PowerShell cmdlets](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WindowsAzurePowershellGet.3f.3f.3fnew.appids) or [Linux command-line interface tool](https://go.microsoft.com/fwlink/?LinkId=253472&clcid=0x409) from hello [Azure Downloads](https://azure.microsoft.com/downloads/) page.</span></span>
* <span data-ttu-id="30cb6-110">установите Azure Storage Explorer из CodePlex;</span><span class="sxs-lookup"><span data-stu-id="30cb6-110">Install Azure Storage Explorer from CodePlex.</span></span>
* <span data-ttu-id="30cb6-111">Загрузите и установите hello средство тестирования сертификации для Azure Certified.</span><span class="sxs-lookup"><span data-stu-id="30cb6-111">Download and install hello Certification Test Tool for Azure Certified:</span></span>
  * <span data-ttu-id="30cb6-112">[http://go.microsoft.com/fwlink/?LinkID=526913](http://go.microsoft.com/fwlink/?LinkID=526913).</span><span class="sxs-lookup"><span data-stu-id="30cb6-112">[http://go.microsoft.com/fwlink/?LinkID=526913](http://go.microsoft.com/fwlink/?LinkID=526913).</span></span> <span data-ttu-id="30cb6-113">Необходимо, чтобы средство сертификации hello toorun компьютер под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="30cb6-113">You need a Windows-based computer toorun hello certification tool.</span></span> <span data-ttu-id="30cb6-114">Если нет доступных компьютере под управлением Windows, можно запустить средство hello, используя виртуальную Машину под управлением Windows в Azure.</span><span class="sxs-lookup"><span data-stu-id="30cb6-114">If you do not have a Windows-based computer available, you can run hello tool using a Windows-based VM in Azure.</span></span>

## <a name="platforms-supported"></a><span data-ttu-id="30cb6-115">Поддерживаемые платформы</span><span class="sxs-lookup"><span data-stu-id="30cb6-115">Platforms supported</span></span>
<span data-ttu-id="30cb6-116">Виртуальные машины Azure можно разрабатывать на базе Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="30cb6-116">You can develop Azure-based VMs on Windows or Linux.</span></span> <span data-ttu-id="30cb6-117">Некоторые элементы hello процесса, таких как создание совместимое Azure виртуального жесткого диска (VHD) — используйте различные средства и шаги в зависимости от операционной системы с помощью публикации:</span><span class="sxs-lookup"><span data-stu-id="30cb6-117">Some elements of hello publishing process--such as creating an Azure-compatible virtual hard disk (VHD)--use different tools and steps depending on which operating system you are using:</span></span>  

* <span data-ttu-id="30cb6-118">При использовании Linux см. раздел «Создание с совместимостью Azure виртуального жесткого диска (на основе Linux)» toohello hello [руководство по публикации образ виртуальной машины](marketplace-publishing-vm-image-creation.md).</span><span class="sxs-lookup"><span data-stu-id="30cb6-118">If you are using Linux, refer toohello “Create an Azure-compatible VHD (Linux-based)” section of hello [Virtual machine image publishing guide](marketplace-publishing-vm-image-creation.md).</span></span>
* <span data-ttu-id="30cb6-119">Если вы используете Windows, см. раздел «Создание с совместимостью Azure виртуального жесткого диска (на основе Windows)» toohello hello [руководство по публикации образ виртуальной машины](marketplace-publishing-vm-image-creation.md).</span><span class="sxs-lookup"><span data-stu-id="30cb6-119">If you are using Windows, refer toohello “Create an Azure-compatible VHD (Windows-based)” section of hello [Virtual machine image publishing guide](marketplace-publishing-vm-image-creation.md).</span></span>

> [!NOTE]
> <span data-ttu-id="30cb6-120">Требуется доступ к tooa машину под управлением Windows, чтобы:</span><span class="sxs-lookup"><span data-stu-id="30cb6-120">You need access tooa Windows-based machine to:</span></span>
> 
> * <span data-ttu-id="30cb6-121">Запустите средство проверки сертификации hello.</span><span class="sxs-lookup"><span data-stu-id="30cb6-121">Run hello certification validation tool.</span></span>
> * <span data-ttu-id="30cb6-122">Создайте hello общего виртуального жесткого диска подписанный URL для hello сертификации отправки виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="30cb6-122">Create hello VHD shared access signature URL for hello VHD certification submission.</span></span>
> 
> 

## <a name="develop-your-vhd"></a><span data-ttu-id="30cb6-123">Разработка VHD</span><span class="sxs-lookup"><span data-stu-id="30cb6-123">Develop your VHD</span></span>
<span data-ttu-id="30cb6-124">Можно разрабатывать VHD Azure в облаке hello или в локальной среде:</span><span class="sxs-lookup"><span data-stu-id="30cb6-124">You can develop Azure VHDs in hello cloud or on-premises:</span></span>

* <span data-ttu-id="30cb6-125">Разработка в облаке означает, что все этапы разработки выполняются удаленно на VHD, который находится в Azure.</span><span class="sxs-lookup"><span data-stu-id="30cb6-125">Cloud-based development means all development steps are performed remotely on a VHD resident on Azure.</span></span>
* <span data-ttu-id="30cb6-126">Для локальной разработки VHD необходимо загрузить и разработать в локальной инфраструктуре.</span><span class="sxs-lookup"><span data-stu-id="30cb6-126">On-premises development requires downloading a VHD and developing it using on-premises infrastructure.</span></span> <span data-ttu-id="30cb6-127">Такой вариант возможен, но не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="30cb6-127">Although this is possible, we do not recommend it.</span></span> <span data-ttu-id="30cb6-128">Обратите внимание, что разработка для Windows или SQL в локальной требуется вы toohave hello соответствующих локальных лицензионных ключей.</span><span class="sxs-lookup"><span data-stu-id="30cb6-128">Note that developing for Windows or SQL on-premises requires you toohave hello relevant on-premises license keys.</span></span> <span data-ttu-id="30cb6-129">Невозможно добавить или установить SQL Server после создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="30cb6-129">You cannot include or install SQL Server after creating a VM.</span></span> <span data-ttu-id="30cb6-130">Ваше предложение необходимо основать на изображении утвержденных SQL из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="30cb6-130">You must also base your offer on an approved SQL image from hello Azure portal.</span></span> <span data-ttu-id="30cb6-131">Если вы решите toodevelop в локальной среде, необходимо выполнить некоторые действия не так, как если вы разрабатывали в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="30cb6-131">If you decide toodevelop on-premises, you must perform some steps differently than if you were developing in hello cloud.</span></span> <span data-ttu-id="30cb6-132">Соответствующие сведения см. в статье [Локальная разработка образа виртуальной машины для Azure Marketplace](marketplace-publishing-vm-image-creation-on-premise.md).</span><span class="sxs-lookup"><span data-stu-id="30cb6-132">You can find relevant information in [Create an on-premises VM image](marketplace-publishing-vm-image-creation-on-premise.md).</span></span>

[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
