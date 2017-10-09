---
title: "aaaManage Azure RemoteApp с помощью службы автоматизации Azure | Документы Microsoft"
description: "Узнайте, как hello службы автоматизации Azure можно использовать toomanage Azure RemoteApp."
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
ms.openlocfilehash: a4cb23e292c797256e971acb3b363b025f140f16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-remoteapp-using-azure-automation"></a><span data-ttu-id="0be35-103">Управление удаленными приложениями Azure RemoteApp с помощью службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="0be35-103">Managing Azure RemoteApp using Azure Automation</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0be35-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="0be35-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="0be35-105">Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="0be35-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="0be35-106">В этом руководстве приведены toohello службы автоматизации Azure и как можно использовать toosimplify управление Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="0be35-106">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of Azure RemoteApp.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="0be35-107">Что такое служба автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="0be35-107">What is Azure Automation?</span></span>
<span data-ttu-id="0be35-108">[Служба автоматизации Azure](../automation/automation-intro.md) — это служба Azure для упрощения управления облаком путем автоматизации процессов.</span><span class="sxs-lookup"><span data-stu-id="0be35-108">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="0be35-109">С помощью службы автоматизации Azure, может быть вручную часто повторяется, длительные задачи и ошибкам автоматических tooincrease надежность, эффективность и toovalue времени для вашей организации.</span><span class="sxs-lookup"><span data-stu-id="0be35-109">Using Azure Automation, manual, frequently-repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="0be35-110">Служба автоматизации Azure обеспечивает механизм выполнения рабочих процессов высокую степень, высокой доступности, которая масштабируется toomeet вашим потребностям.</span><span class="sxs-lookup"><span data-stu-id="0be35-110">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="0be35-111">В службе автоматизации Azure процессы можно запустить вручную, в сторонних системах или по расписанию, чтобы все задачи выполнялись в нужное время.</span><span class="sxs-lookup"><span data-stu-id="0be35-111">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="0be35-112">Снизить операционные издержки и освободить ИТ и автоматический запуск DevOps toofocus сотрудников на работу, которая добавляет ценность для бизнеса, перемещая toobe задачи управления вашей облачной службой автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="0be35-112">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-remoteapp"></a><span data-ttu-id="0be35-113">Как служба автоматизации Azure может помочь управлять удаленными приложениями Azure</span><span class="sxs-lookup"><span data-stu-id="0be35-113">How can Azure Automation help manage Azure RemoteApp?</span></span>
<span data-ttu-id="0be35-114">RemoteApp можно управлять в службе автоматизации Azure с помощью командлетов PowerShell hello, которые доступны в hello [средства Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="0be35-114">RemoteApp can be managed in Azure Automation by using hello PowerShell cmdlets that are available in hello [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="0be35-115">Служба автоматизации Azure имеет этих командлетов RemoteApp PowerShell, доступных стандартной hello, что позволяет выполнять все задачи управления RemoteApp в службе hello.</span><span class="sxs-lookup"><span data-stu-id="0be35-115">Azure Automation has these RemoteApp PowerShell cmdlets available out of hello box, so that you can perform all of your RemoteApp management tasks within hello service.</span></span> <span data-ttu-id="0be35-116">Также вы можете обеспечить эти командлеты в службе автоматизации Azure с помощью командлетов hello для других служб Azure, tooautomate сложные задачи служб Azure и систем сторонних разработчиков.</span><span class="sxs-lookup"><span data-stu-id="0be35-116">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0be35-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0be35-117">Next steps</span></span>
<span data-ttu-id="0be35-118">Теперь, когда вы узнали основы hello автоматизации Azure и как можно использовать toomanage Azure RemoteApp, выполните следующие дополнительные сведения об автоматизации Azure toolearn ссылки.</span><span class="sxs-lookup"><span data-stu-id="0be35-118">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure RemoteApp, follow these links toolearn more about Azure Automation.</span></span>

* <span data-ttu-id="0be35-119">Hello Azure Automation в разделе [учебник по началу работы](../automation/automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="0be35-119">See hello Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span></span>

