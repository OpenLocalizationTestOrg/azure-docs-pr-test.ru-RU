---
title: "aaaCreate удостоверением рабочей или учебной в AAD для Linux | Документы Microsoft"
description: "Узнайте, как toocreate использованием рабочей или учебной удостоверения Azure Active Directory toouse с виртуальными машинами Linux."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: b0f86d77-c669-4aa1-a095-c2aa4d9105fe
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/23/2016
ms.author: rasquill
ms.openlocfilehash: 54c3d0b0e89fe1b2d6a9b58a46776fe446ed72b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="creating-a-work-or-school-identity-in-azure-active-directory-toouse-with-linux-vms"></a><span data-ttu-id="da589-103">Создание рабочего или учебного заведения удостоверения в Azure Active Directory toouse с виртуальными машинами Linux</span><span class="sxs-lookup"><span data-stu-id="da589-103">Creating a Work or School identity in Azure Active Directory toouse with Linux VMs</span></span>
<span data-ttu-id="da589-104">Если создать личную учетную запись Azure или иметь личные подписки MSDN и создан hello учетная запись Azure tootake деньги на счете MSDN Azure hello--используется *учетную запись Майкрософт* toocreate удостоверение его.</span><span class="sxs-lookup"><span data-stu-id="da589-104">If you created a personal Azure account or have a personal MSDN subscription and created hello Azure account tootake advantage of hello MSDN Azure credits -- you used a *Microsoft account* identity toocreate it.</span></span> <span data-ttu-id="da589-105">Много замечательных функций Azure — [шаблоны группы ресурсов](../../azure-resource-manager/resource-group-overview.md) один пример — требуется рабочая или учебная учетная запись (удостоверение, под управлением Azure Active Directory) toowork.</span><span class="sxs-lookup"><span data-stu-id="da589-105">Many great features of Azure -- [resource group templates](../../azure-resource-manager/resource-group-overview.md) is one example -- require a work or school account (an identity managed by Azure Active Directory) toowork.</span></span> <span data-ttu-id="da589-106">Можно выполнить hello приведенные ниже инструкции toocreate, так как к счастью, одна из наиболее удобных свойств hello личную учетную запись Azure он поставляется с доменом Azure Active Directory по умолчанию, которые можно использовать toocreate новой рабочей или учебной учетной записи новой работы или учебы Учетная запись, можно использовать с компонентами Azure, которые их используют.</span><span class="sxs-lookup"><span data-stu-id="da589-106">You can follow hello instructions below toocreate a new work or school account because fortunately, one of hello best things about your personal Azure account is that it comes with a default Azure Active Directory domain that you can use toocreate a new work or school account that you can use with Azure features that require it.</span></span>

<span data-ttu-id="da589-107">Однако последние изменения обеспечивает его возможных toomanage подписки с любым типом учетной записи Azure, с помощью hello `azure login` интерактивного входа в систему из описанных [здесь](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="da589-107">However, recent changes make it possible toomanage your subscription with any type of Azure account using hello `azure login` interactive login method described [here](../../xplat-cli-connect.md).</span></span> <span data-ttu-id="da589-108">Вы можете использовать этот механизм, или можно выполнить следующие инструкции hello.</span><span class="sxs-lookup"><span data-stu-id="da589-108">You can either use that mechanism, or you can follow hello instructions that follow.</span></span> <span data-ttu-id="da589-109">Вы также можете [создания рабочей или учебной удостоверения в Azure Active Directory toouse с виртуальными машинами Windows](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="da589-109">You can also [create a work or school identity in Azure Active Directory toouse with Windows VMs](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

[!INCLUDE [virtual-machines-common-create-aad-work-id](../../../includes/virtual-machines-common-create-aad-work-id.md)]

