---
title: "aaaManage виртуальных машин с помощью службы автоматизации Azure | Документы Microsoft"
description: "Узнайте, как hello службы автоматизации Azure можно использовать toomanage виртуальных машин Azure в масштабе."
services: virtual-machines-windows, automation
documentationcenter: 
author: jodoglevy
manager: timlt
editor: 
ms.assetid: ce49f83a-f409-42ee-af74-a8ea2caa9ae8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2016
ms.author: timlt
ms.openlocfilehash: bfe7b3a51b6e82bd7cd5b0a83df7226476ed4f36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-virtual-machines-using-azure-automation"></a><span data-ttu-id="6c1b5-103">Управление виртуальными машинами Azure с помощью службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="6c1b5-103">Managing Azure Virtual Machines using Azure Automation</span></span>
<span data-ttu-id="6c1b5-104">В этом руководстве описаны toohello службы автоматизации Azure и как они могут использоваться toosimplify управление виртуальных машин Azure.</span><span class="sxs-lookup"><span data-stu-id="6c1b5-104">This guide introduces you toohello Azure Automation service and how it can be used toosimplify managing your Azure virtual machines.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="6c1b5-105">Что такое служба автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="6c1b5-105">What is Azure Automation?</span></span>
<span data-ttu-id="6c1b5-106">[Служба автоматизации Azure](https://azure.microsoft.com/services/automation/) — это служба Azure для упрощения управления облаком путем автоматизации процессов.</span><span class="sxs-lookup"><span data-stu-id="6c1b5-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="6c1b5-107">С помощью службы автоматизации Azure, длительные, вручную, ошибкам и часто повторяющиеся задачи может быть автоматизированные tooincrease надежность, эффективность и времени значение для вашей организации.</span><span class="sxs-lookup"><span data-stu-id="6c1b5-107">By using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability, efficiency, and time-to-value for your organization.</span></span>

<span data-ttu-id="6c1b5-108">Служба автоматизации Azure обеспечивает механизм выполнения рабочих процессов высокую степень доступности и высокой доступности, которая масштабируется toomeet вашим потребностям по мере роста организации.</span><span class="sxs-lookup"><span data-stu-id="6c1b5-108">Azure Automation provides a highly reliable and highly available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="6c1b5-109">В службе автоматизации Azure процессы можно запустить вручную, в сторонних системах или по расписанию, чтобы все задачи выполнялись в нужное время.</span><span class="sxs-lookup"><span data-stu-id="6c1b5-109">In Azure Automation, processes can be kicked off manually, by third-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="6c1b5-110">Можно снизить операционные издержки и освободить ИТ DevOps персонал toofocus на работу, которая добавляет ценность для бизнеса, запустив свое облако задачи управления автоматически в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="6c1b5-110">You can lower operational overhead and free up IT and DevOps staff toofocus on work that adds business value by running your cloud management tasks automatically with Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-virtual-machines"></a><span data-ttu-id="6c1b5-111">Как служба автоматизации Azure может помочь управлять виртуальными машинами Azure</span><span class="sxs-lookup"><span data-stu-id="6c1b5-111">How can Azure Automation help manage Azure virtual machines?</span></span>
<span data-ttu-id="6c1b5-112">Виртуальными машинами можно управлять с помощью службы автоматизации Azure, используя [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="6c1b5-112">Virtual machines can be managed in Azure Automation by using [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="6c1b5-113">Служба автоматизации Azure включает командлеты Azure PowerShell hello, чтобы выполнить все задачи управления виртуальной машины в службе hello.</span><span class="sxs-lookup"><span data-stu-id="6c1b5-113">Azure Automation includes hello Azure PowerShell cmdlets, so you can perform all of your virtual machine management tasks within hello service.</span></span> <span data-ttu-id="6c1b5-114">Также вы можете обеспечить командлеты hello в службе автоматизации Azure с помощью командлетов hello для других служб Azure, tooautomate сложные задачи для служб Azure и систем сторонних разработчиков.</span><span class="sxs-lookup"><span data-stu-id="6c1b5-114">You can also pair hello cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and third-party systems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c1b5-115">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6c1b5-115">Next steps</span></span>
<span data-ttu-id="6c1b5-116">Теперь, когда вы узнали основы hello автоматизации Azure и как можно использовать toomanage виртуальных машинах Azure, Дополнительные сведения:</span><span class="sxs-lookup"><span data-stu-id="6c1b5-116">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure virtual machines, learn more:</span></span>

* [<span data-ttu-id="6c1b5-117">Обзор службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="6c1b5-117">Azure Automation Overview</span></span>](../../automation/automation-intro.md)
* [<span data-ttu-id="6c1b5-118">Мой первый Runbook</span><span class="sxs-lookup"><span data-stu-id="6c1b5-118">My first runbook</span></span>](../../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="6c1b5-119">План обучения работе со службой автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="6c1b5-119">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)

