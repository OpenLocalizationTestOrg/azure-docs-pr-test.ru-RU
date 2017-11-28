---
title: "aaaManage управления API Azure, с помощью службы автоматизации Azure"
description: "Узнайте, как hello службы автоматизации Azure можно использовать toomanage управления API Azure."
services: api-management, automation
documentationcenter: 
author: csand-msft
manager: eamono
editor: 
ms.assetid: 2e53c9af-f738-47f8-b1b6-593050a7c51b
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 05b8e3cad786fa701feb88f7b6d9629f16686d15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-api-management-using-azure-automation"></a><span data-ttu-id="20c9a-103">Управление управлением API с помощью службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="20c9a-103">Managing Azure API Management using Azure Automation</span></span>
<span data-ttu-id="20c9a-104">В этом руководстве приведены toohello службы автоматизации Azure и как можно управления используется toosimplify управления API Azure.</span><span class="sxs-lookup"><span data-stu-id="20c9a-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of Azure API Management.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="20c9a-105">Что такое служба автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="20c9a-105">What is Azure Automation?</span></span>
<span data-ttu-id="20c9a-106">[Служба автоматизации Azure](https://azure.microsoft.com/services/automation/) — это служба Azure для упрощения управления облаком путем автоматизации процессов.</span><span class="sxs-lookup"><span data-stu-id="20c9a-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="20c9a-107">С помощью службы автоматизации Azure, вручную, повторяющиеся, длительные и ошибкам задачи могут быть автоматизированные tooincrease надежность, эффективность и toovalue времени для вашей организации.</span><span class="sxs-lookup"><span data-stu-id="20c9a-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="20c9a-108">Служба автоматизации Azure обеспечивает механизм выполнения рабочих процессов высокую степень, высокой доступности, которая масштабируется toomeet вашим потребностям.</span><span class="sxs-lookup"><span data-stu-id="20c9a-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="20c9a-109">В службе автоматизации Azure процессы можно запустить вручную, в сторонних системах или по расписанию, чтобы все задачи выполнялись в нужное время.</span><span class="sxs-lookup"><span data-stu-id="20c9a-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="20c9a-110">Снизить операционные издержки и освободить ИТ и автоматический запуск DevOps toofocus сотрудников на работу, которая добавляет ценность для бизнеса, перемещая toobe задачи управления вашей облачной службой автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="20c9a-110">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-api-management"></a><span data-ttu-id="20c9a-111">Как служба автоматизации Azure помогает управлять управлением API Azure?</span><span class="sxs-lookup"><span data-stu-id="20c9a-111">How can Azure Automation help manage Azure API Management?</span></span>
<span data-ttu-id="20c9a-112">API управления можно управлять в службе автоматизации Azure с помощью hello [командлеты Windows PowerShell для Azure API управления](https://azure.microsoft.com/updates/full-set-of-windows-powershell-cmdlets-for-azure-api-management-api/).</span><span class="sxs-lookup"><span data-stu-id="20c9a-112">API Management can be managed in Azure Automation by using hello [Windows PowerShell cmdlets for Azure API Management API](https://azure.microsoft.com/updates/full-set-of-windows-powershell-cmdlets-for-azure-api-management-api/).</span></span> <span data-ttu-id="20c9a-113">В службе автоматизации Azure можно написать tooperform сценарии рабочего процесса PowerShell многие из задач управления API с помощью командлетов hello.</span><span class="sxs-lookup"><span data-stu-id="20c9a-113">Within Azure Automation you can write PowerShell workflow scripts tooperform many of your API Management tasks using hello cmdlets.</span></span> <span data-ttu-id="20c9a-114">Также вы можете обеспечить эти командлеты в службе автоматизации Azure с помощью командлетов hello для других служб Azure, tooautomate сложные задачи служб Azure и систем сторонних разработчиков.</span><span class="sxs-lookup"><span data-stu-id="20c9a-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="20c9a-115">Ниже приведены некоторые примеры использования управления API с помощью средств службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="20c9a-115">Here are some examples of using API Management with Automation:</span></span>

* [<span data-ttu-id="20c9a-116">Управление API Azure — использование PowerShell для архивации и восстановления</span><span class="sxs-lookup"><span data-stu-id="20c9a-116">Azure API Management – Using PowerShell for backup and restore</span></span>](https://blogs.msdn.microsoft.com/katriend/2015/10/02/azure-api-management-using-powershell-for-backup-and-restore/)

## <a name="next-steps"></a><span data-ttu-id="20c9a-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="20c9a-117">Next Steps</span></span>
<span data-ttu-id="20c9a-118">Теперь, когда вы узнали основы hello автоматизации Azure и как можно использовать toomanage управления API Azure, выполните следующие дополнительные toolearn ссылки.</span><span class="sxs-lookup"><span data-stu-id="20c9a-118">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure API Management, follow these links toolearn more.</span></span>

* <span data-ttu-id="20c9a-119">Hello Azure Automation в разделе [учебник по началу работы](../automation/automation-first-runbook-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="20c9a-119">See hello Azure Automation [getting started tutorial](../automation/automation-first-runbook-graphical.md).</span></span>

