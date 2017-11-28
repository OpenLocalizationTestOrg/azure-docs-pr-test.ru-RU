---
title: "aaaUsing SAP на виртуальных машинах Linux | Документы Microsoft"
description: "Узнайте об использовании SAP на виртуальных машинах в Microsoft Azure."
services: virtual-machines-linux,virtual-network,storage
documentationcenter: saponazure
author: MSSedusch
manager: timlt
editor: 
tags: azure-service-management
keywords: 
ms.assetid: f9cd93dc-71ad-48a4-8778-4e48aec484a6
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: campaign-page
ms.tgt_pltfrm: vm-linux
ms.workload: na
ms.date: 10/04/2016
ms.author: sedusch
ms.openlocfilehash: a805cdecb515239057e185a92bf5c4d4e707f72f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-sap-on-linux-virtual-machines-in-azure"></a><span data-ttu-id="3a6d8-103">Использование SAP в виртуальных машинах Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="3a6d8-103">Using SAP on Linux virtual machines in Azure</span></span>
<span data-ttu-id="3a6d8-104">Облачные вычисления — это широко используемый термин, который приобретает все большее значение в пределах hello ИТ-индустрии, от малых компаний вверх toolarge транснациональных корпораций.</span><span class="sxs-lookup"><span data-stu-id="3a6d8-104">Cloud Computing is a widely used term which is gaining more and more importance within hello IT industry, from small companies up toolarge and multinational corporations.</span></span> <span data-ttu-id="3a6d8-105">Microsoft Azure — hello платформа облачных служб Майкрософт, которая предлагает широкий спектр новых возможностей.</span><span class="sxs-lookup"><span data-stu-id="3a6d8-105">Microsoft Azure is hello Cloud Services Platform from Microsoft which offers a wide spectrum of new possibilities.</span></span> <span data-ttu-id="3a6d8-106">Теперь заказчики могут toorapidly подготовки и Отмена подготовки приложений как облачных служб, так, чтобы они не только tootechnical или бюджетные ограничения.</span><span class="sxs-lookup"><span data-stu-id="3a6d8-106">Now customers are able toorapidly provision and de-provision applications as Cloud-Services, so they are not limited tootechnical or budgeting restrictions.</span></span> <span data-ttu-id="3a6d8-107">Вместо того чтобы тратить время и бюджет на аппаратную инфраструктуру, компании могут сосредоточить внимание на приложения hello, бизнес-процессов и его преимущества для клиентов и пользователей.</span><span class="sxs-lookup"><span data-stu-id="3a6d8-107">Instead of investing time and budget into hardware infrastructure, companies can focus on hello application, business processes and its benefits for customers and users.</span></span>

<span data-ttu-id="3a6d8-108">Корпорация Майкрософт предоставляет виртуальные машины Microsoft Azure как комплексную платформу "инфраструктура как услуга" (IaaS).</span><span class="sxs-lookup"><span data-stu-id="3a6d8-108">With Microsoft Azure virtual machines, Microsoft offers a comprehensive Infrastructure as a Service (IaaS) platform.</span></span> <span data-ttu-id="3a6d8-109">Виртуальные машины Azure (IaaS) поддерживают приложения на основе SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="3a6d8-109">SAP NetWeaver based applications are supported on Azure Virtual Machines (IaaS).</span></span> <span data-ttu-id="3a6d8-110">технические документы Hello ниже описывают, как tooplan и реализуйте SAP NetWeaver приложения, основанные на виртуальных машинах Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="3a6d8-110">hello whitepapers below describe how tooplan and implement SAP NetWeaver based applications on Windows virtual machines in Azure.</span></span> <span data-ttu-id="3a6d8-111">Приложения на основе SAP NetWeaver можно также реализовать на [виртуальных машинах Windows](../../windows/classic/sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3a6d8-111">You can also implement SAP NetWeaver based applications on [Windows virtual machines](../../windows/classic/sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-sap-get-started](../../../../includes/virtual-machines-common-classic-sap-get-started.md)]

## <a name="sap-netweaver-on-azure-suse-linux-virtual-machines"></a><span data-ttu-id="3a6d8-112">SAP NetWeaver на виртуальных машинах Azure под управлением SUSE Linux</span><span class="sxs-lookup"><span data-stu-id="3a6d8-112">SAP NetWeaver on Azure SUSE Linux Virtual Machines</span></span>
<span data-ttu-id="3a6d8-113">Заголовок: aaaTesting SAP NetWeaver в ВМ Microsoft Azure SUSE Linux</span><span class="sxs-lookup"><span data-stu-id="3a6d8-113">title: aaaTesting SAP NetWeaver on Microsoft Azure SUSE Linux VMs</span></span>

<span data-ttu-id="3a6d8-114">Содержание. На данный момент времени официальной поддержки SAP для запуска SAP NetWeaver на виртуальных машинах Azure под управлением Linux нет.</span><span class="sxs-lookup"><span data-stu-id="3a6d8-114">Summary: There is no official SAP support for running SAP NetWeaver on Azure Linux VMs at this point in time.</span></span> <span data-ttu-id="3a6d8-115">Тем не менее клиентов может потребоваться toodo некоторые тестирования или рассмотрите возможность toorun систем SAP демонстрации или обучения на виртуальных машинах Linux Azure при условии, что нет необходимости связи со службой поддержки SAP.</span><span class="sxs-lookup"><span data-stu-id="3a6d8-115">Nevertheless customers might want toodo some testing or might consider toorun SAP demo or training systems on Azure Linux VMs as long as there is no need for contacting SAP support.</span></span> <span data-ttu-id="3a6d8-116">В этой статье помогут настройку виртуальных машин Linux SUSE Azure для выполнения SAP и предоставляет некоторые основные ссылки в порядке tooavoid типичные потенциальные проблемы.</span><span class="sxs-lookup"><span data-stu-id="3a6d8-116">This article should help setting up Azure SUSE Linux VMs for running SAP and gives some basic hints in order tooavoid common potential pitfalls.</span></span>

<span data-ttu-id="3a6d8-117">Последнее обновление: декабрь 2015 г.</span><span class="sxs-lookup"><span data-stu-id="3a6d8-117">Updated: December 2015</span></span>

[<span data-ttu-id="3a6d8-118">Эту статью можно найти здесь</span><span class="sxs-lookup"><span data-stu-id="3a6d8-118">This article can be found here</span></span>](../../virtual-machines-linux-sap-on-suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

