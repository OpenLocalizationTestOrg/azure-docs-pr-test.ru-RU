---
title: "Управление службой Azure RemoteApp с помощью службы автоматизации Azure | Документация Майкрософт"
description: "Способы использования службы автоматизации Azure для управления удаленными приложениями Azure RemoteApp."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 589f01ef-f9c1-4e7b-a040-1b46862d3544
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: magoedte;csand
ms.openlocfilehash: 59ac11f153c0bd74a1106400dbbf5790968b657c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-remoteapp-using-azure-automation"></a><span data-ttu-id="98595-103">Управление удаленными приложениями Azure RemoteApp с помощью службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="98595-103">Managing Azure RemoteApp using Azure Automation</span></span>
> [!IMPORTANT]
> <span data-ttu-id="98595-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="98595-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="98595-105">Дополнительные сведения см. в [объявлении](https://go.microsoft.com/fwlink/?linkid=821148).</span><span class="sxs-lookup"><span data-stu-id="98595-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="98595-106">В этом руководстве представлена служба автоматизации Azure и описано, как ее использовать, чтобы упростить управление удаленными приложениями Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="98595-106">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of Azure RemoteApp.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="98595-107">Что такое служба автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="98595-107">What is Azure Automation?</span></span>
<span data-ttu-id="98595-108">[Служба автоматизации Azure](../automation/automation-intro.md) — это служба Azure для упрощения управления облаком путем автоматизации процессов.</span><span class="sxs-lookup"><span data-stu-id="98595-108">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="98595-109">С помощью службы автоматизации Azure часто повторяющиеся задачи, которые выполняются вручную, требуют много времени и подвержены ошибкам, можно автоматизировать для повышения надежности, эффективности и экономии времени в вашей организации.</span><span class="sxs-lookup"><span data-stu-id="98595-109">Using Azure Automation, manual, frequently-repeated, long-running, and error-prone tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="98595-110">Служба автоматизации Azure предоставляет высоконадежную и высокодоступную подсистему выполнения рабочих процессов, которая масштабируется в соответствии с вашими задачами.</span><span class="sxs-lookup"><span data-stu-id="98595-110">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales to meet your needs.</span></span> <span data-ttu-id="98595-111">В службе автоматизации Azure процессы можно запустить вручную, в сторонних системах или по расписанию, чтобы все задачи выполнялись в нужное время.</span><span class="sxs-lookup"><span data-stu-id="98595-111">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="98595-112">Уменьшите операционные затраты и освободите ИТ-сотрудников и DevOps для работы над повышением бизнес-ценности ПО и автоматизации задач управления облаком в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="98595-112">Reduce operational overhead and free up IT and DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-remoteapp"></a><span data-ttu-id="98595-113">Как служба автоматизации Azure может помочь управлять удаленными приложениями Azure</span><span class="sxs-lookup"><span data-stu-id="98595-113">How can Azure Automation help manage Azure RemoteApp?</span></span>
<span data-ttu-id="98595-114">Служба автоматизации Azure может управлять удаленными приложениями RemoteApp с помощью командлетов PowerShell, которые доступны в [средствах Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="98595-114">RemoteApp can be managed in Azure Automation by using the PowerShell cmdlets that are available in the [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="98595-115">В службе автоматизации Azure эти командлеты PowerShell для удаленных приложений RemoteApp уже сразу доступны, поэтому все задачи управления RemoteApp можно выполнять из службы.</span><span class="sxs-lookup"><span data-stu-id="98595-115">Azure Automation has these RemoteApp PowerShell cmdlets available out of the box, so that you can perform all of your RemoteApp management tasks within the service.</span></span> <span data-ttu-id="98595-116">Вы также можете связать эти командлеты в службе автоматизации Azure с командлетами для других служб Azure, чтобы автоматизировать сложные задачи в службах Azure и системах сторонних производителей.</span><span class="sxs-lookup"><span data-stu-id="98595-116">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98595-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="98595-117">Next steps</span></span>
<span data-ttu-id="98595-118">Теперь, когда вы познакомились с основами службы автоматизации Azure и способами ее использования для управления удаленными приложениями Azure, пройдите по ссылкам, чтобы получить дополнительные сведения о службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="98595-118">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure RemoteApp, follow these links to learn more about Azure Automation.</span></span>

* <span data-ttu-id="98595-119">Изучите [руководство по началу работы](../automation/automation-first-runbook-graphical.md) со службой автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="98595-119">See the Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span></span>

