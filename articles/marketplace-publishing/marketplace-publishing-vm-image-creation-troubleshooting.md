---
title: "Как устранить распространенные неполадки, возникающие в процессе создания виртуального жесткого диска | Документация Майкрософт"
description: "Ответы на распространенные вопросы об устранении неполадок, а также о проблемах, возникающих в процессе создания виртуального жесткого диска."
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: 
editor: 
ms.assetid: e39563d8-8646-4cb7-b078-8b10ac35b494
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 09/26/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: c4e88a9fbb15dd90d619b159ae1065dfacc1907f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-troubleshoot-common-issues-encountered-during-vhd-creation"></a><span data-ttu-id="38f36-103">Как устранить распространенные неполадки, возникающие в процессе создания виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="38f36-103">How to troubleshoot common issues encountered during VHD creation</span></span>
<span data-ttu-id="38f36-104">Сведения, приведенные в этой статье, помогут издателям и соадминистраторам решить проблемы, возникающие в процессе публикации решений lkz виртуальных машин или управления ими.</span><span class="sxs-lookup"><span data-stu-id="38f36-104">This article is provided to help an Azure Marketplace publisher and/or co-administrator that may experience an issue or have common questions while publishing or managing their virtual machine solution(s).</span></span>

1. <span data-ttu-id="38f36-105">Как изменить имя узла?</span><span class="sxs-lookup"><span data-stu-id="38f36-105">How do I change the name of the host?</span></span>
   
    <span data-ttu-id="38f36-106">После создания виртуальной машины имя узла изменить невозможно.</span><span class="sxs-lookup"><span data-stu-id="38f36-106">Once VM is created, users can’t update the name of the host.</span></span>
2. <span data-ttu-id="38f36-107">Как сбросить службу удаленного рабочего стола или ее пароль для входа в систему?</span><span class="sxs-lookup"><span data-stu-id="38f36-107">How to reset the Remote Desktop service or its login password?</span></span>
   
   * [<span data-ttu-id="38f36-108">Справочные материалы для виртуальной машины Windows</span><span class="sxs-lookup"><span data-stu-id="38f36-108">Reference for Windows VM</span></span>](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-reset-rdp/)
   * [<span data-ttu-id="38f36-109">Справочные материалы для виртуальной машины Linux</span><span class="sxs-lookup"><span data-stu-id="38f36-109">Reference for Linux VM</span></span>](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)
3. <span data-ttu-id="38f36-110">Как создать сертификаты SSH?</span><span class="sxs-lookup"><span data-stu-id="38f36-110">How to generate new ssh certificates?</span></span>
   
   <span data-ttu-id="38f36-111">Перейдите по этой ссылке: [https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/).</span><span class="sxs-lookup"><span data-stu-id="38f36-111">Please refer to the link: [https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)</span></span>
4. <span data-ttu-id="38f36-112">Как настроить открытый сертификат VPN?</span><span class="sxs-lookup"><span data-stu-id="38f36-112">How to configure an open VPN certificate?</span></span>
   
   <span data-ttu-id="38f36-113">Перейдите по этой ссылке: [https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/](https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/).</span><span class="sxs-lookup"><span data-stu-id="38f36-113">Please refer to the link: [https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/](https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/)</span></span>
5. <span data-ttu-id="38f36-114">Каковы условия предоставления поддержки для ПО Microsoft Server, запущенного в среде виртуальной машины Microsoft Azure (инфраструктура как услуга)?</span><span class="sxs-lookup"><span data-stu-id="38f36-114">What is the support policy for running Microsoft server software in the Microsoft Azure virtual machine environment (infrastructure-as-a-service)?</span></span>
   
   <span data-ttu-id="38f36-115">Перейдите по этой ссылке: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672).</span><span class="sxs-lookup"><span data-stu-id="38f36-115">Please refer to the link: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)</span></span>
6. <span data-ttu-id="38f36-116">Имеют ли виртуальные машины какой-либо уникальный идентификатор?</span><span class="sxs-lookup"><span data-stu-id="38f36-116">Do Virtual Machines have any unique identifier?</span></span>
   
   <span data-ttu-id="38f36-117">В каждой виртуальной машине Azure зашифрован уникальный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="38f36-117">Azure encodes Azure VM Unique ID in every VM.</span></span> <span data-ttu-id="38f36-118">Дополнительные сведения см. в блоге и документации.</span><span class="sxs-lookup"><span data-stu-id="38f36-118">See details in this blog and documentation.</span></span>
7. <span data-ttu-id="38f36-119">Как выполняется управление расширением пользовательских скриптов при запуске виртуальной машины?</span><span class="sxs-lookup"><span data-stu-id="38f36-119">In a VM how can I manage the custom script extension in the startup task?</span></span>
   
   <span data-ttu-id="38f36-120">Перейдите по этой ссылке: [https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/).</span><span class="sxs-lookup"><span data-stu-id="38f36-120">Please refer to the link: [https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/)</span></span>
8. <span data-ttu-id="38f36-121">Как создать виртуальную машину на портале Azure, используя виртуальный жесткий диск, загруженный в хранилище класса Premium?</span><span class="sxs-lookup"><span data-stu-id="38f36-121">How to create a VM from the Azure portal using the VHD that is uploaded to premium storage?</span></span>
   
   <span data-ttu-id="38f36-122">В настоящее время эта функция не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="38f36-122">We do not support this feature yet.</span></span>
9. <span data-ttu-id="38f36-123">Поддерживаются ли 32-разрядные приложения в Azure Marketplace?</span><span class="sxs-lookup"><span data-stu-id="38f36-123">Is a 32-bit app supported in the Azure Marketplace?</span></span>
   
   <span data-ttu-id="38f36-124">Сведения о политике поддержки см. здесь: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672).</span><span class="sxs-lookup"><span data-stu-id="38f36-124">Please refer to the link for details on the support policy: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)</span></span>
10. <span data-ttu-id="38f36-125">Каждый раз при попытке создать образ виртуальных жестких дисков в PowerShell отображается следующее сообщение об ошибке: "VHD уже зарегистрирован в репозитории образов как ресурс".</span><span class="sxs-lookup"><span data-stu-id="38f36-125">Every time I am trying to create an image from my VHDs, I get the error “.VHD is already registered with image repository as the resource” in PowerShell.</span></span> <span data-ttu-id="38f36-126">Я не создавал образы раньше, и в Azure отсутствует образ с таким именем.</span><span class="sxs-lookup"><span data-stu-id="38f36-126">I did not create any image before nor did I find any image with this name in Azure.</span></span> <span data-ttu-id="38f36-127">Как решить эту проблему?</span><span class="sxs-lookup"><span data-stu-id="38f36-127">How do I resolve this?</span></span>
    
    <span data-ttu-id="38f36-128">Это обычно происходит, если пользователь подготовил виртуальную машину из виртуального жесткого диска, который заблокирован.</span><span class="sxs-lookup"><span data-stu-id="38f36-128">This usually happen if the user provisioned a VM from this VHD and there is a lock on that VHD.</span></span> <span data-ttu-id="38f36-129">Проверьте, не использовался ли этот виртуальный жесткий диск для выделения виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="38f36-129">Please check that there is no VM allocated from this VHD.</span></span> <span data-ttu-id="38f36-130">Если эта ошибка по-прежнему возникает, отправьте запрос в службу поддержки на портале публикации или перейдите по ссылке (дополнительные сведения см. в ответе на 11 вопрос).</span><span class="sxs-lookup"><span data-stu-id="38f36-130">If the error still persist , then please raise a support ticket using this link or from the Publishing portal regarding this (details are given in the answer of question 11).</span></span>