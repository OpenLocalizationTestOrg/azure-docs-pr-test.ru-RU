---
title: "Управление облачными службами Azure с помощью службы автоматизации Azure | Документация Майкрософт"
description: "Способы использования службы автоматизации Azure для управления облачными службами Azure при масштабировании."
services: cloud-services, automation
documentationcenter: 
author: jodoglevy
manager: timlt
editor: 
ms.assetid: 3789810a-2892-4eef-bf29-c781c1b5af48
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2016
ms.author: timlt
ms.openlocfilehash: 6b5acac1b8647c324988c316cd5602b3dba98a1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-cloud-services-using-azure-automation"></a><span data-ttu-id="8e3ce-103">Управление облачными службами Azure с помощью службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="8e3ce-103">Managing Azure Cloud Services using Azure Automation</span></span>
<span data-ttu-id="8e3ce-104">В этом руководстве будет представлена служба автоматизации Azure и способы ее использования для упрощения управления облачными службами Azure.</span><span class="sxs-lookup"><span data-stu-id="8e3ce-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of your Azure cloud services.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="8e3ce-105">Что такое служба автоматизации Azure?</span><span class="sxs-lookup"><span data-stu-id="8e3ce-105">What is Azure Automation?</span></span>
<span data-ttu-id="8e3ce-106">[Служба автоматизации Azure](https://azure.microsoft.com/services/automation/) — это служба Azure для упрощения управления облаком путем автоматизации процессов.</span><span class="sxs-lookup"><span data-stu-id="8e3ce-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="8e3ce-107">С помощью службы автоматизации Azure можно автоматизировать длительные, выполняемые вручную, ненадежные и часто повторяющиеся задачи для повышения надежности, эффективности и ускорения вывода продукта на рынок.</span><span class="sxs-lookup"><span data-stu-id="8e3ce-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="8e3ce-108">Служба автоматизации Azure предоставляет высоконадежную и высокодоступную подсистему выполнения рабочих процессов с масштабированием в соответствии с требованиями организации по мере ее роста.</span><span class="sxs-lookup"><span data-stu-id="8e3ce-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales to meet your needs as your organization grows.</span></span> <span data-ttu-id="8e3ce-109">В службе автоматизации Azure процессы можно запустить вручную, в сторонних системах или по расписанию, чтобы все задачи выполнялись в нужное время.</span><span class="sxs-lookup"><span data-stu-id="8e3ce-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="8e3ce-110">Уменьшите операционные затраты и освободите ИТ-сотрудников и специалистов по разработке и операциям для работы над повышением бизнес-ценности ПО и автоматизации задач управления облаком в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="8e3ce-110">Lower operational overhead and free up IT / DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-cloud-services"></a><span data-ttu-id="8e3ce-111">Как служба автоматизации Azure помогает управлять облачными службами Azure?</span><span class="sxs-lookup"><span data-stu-id="8e3ce-111">How can Azure Automation help manage Azure cloud services?</span></span>
<span data-ttu-id="8e3ce-112">Облачными службами Azure можно управлять в службе автоматизации Azure, используя командлеты PowerShell, доступные в разделе [Инструменты Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="8e3ce-112">Azure cloud services can be managed in Azure Automation by using the PowerShell cmdlets that are available in the [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="8e3ce-113">Служба автоматизации Azure предоставляет командлеты PowerShell облачных служб Azure в готовом виде, чтобы вы могли выполнять все задачи управления облачными службами, не выходя из службы.</span><span class="sxs-lookup"><span data-stu-id="8e3ce-113">Azure Automation has these cloud service PowerShell cmdlets available out of the box, so that you can perform all of your cloud service management tasks within the service.</span></span> <span data-ttu-id="8e3ce-114">Вы также можете связать эти командлеты в службе автоматизации Azure с командлетами для других служб Azure, чтобы автоматизировать сложные задачи в службах Azure и системах сторонних производителей.</span><span class="sxs-lookup"><span data-stu-id="8e3ce-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="8e3ce-115">В некоторых примерах используется служба автоматизации Azure для управления облачными службами Azure, включая следующее:</span><span class="sxs-lookup"><span data-stu-id="8e3ce-115">Some example uses of Azure Automation to manage Azure Cloud Services include:</span></span>

* [<span data-ttu-id="8e3ce-116">непрерывное развертывание облачной службы всякий раз, когда в хранилище BLOB-объектов Azure обновляется CSCFG- или CSPKG-файл;</span><span class="sxs-lookup"><span data-stu-id="8e3ce-116">Continous deployment of a Cloud Service whenever cscfg or cspkg is updated in Azure Blob storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Continuous-Deployment-of-A-eeebf3a6)
* [<span data-ttu-id="8e3ce-117">параллельная перезагрузка экземпляров облачной службы, по одному домену обновления за раз.</span><span class="sxs-lookup"><span data-stu-id="8e3ce-117">Rebooting Cloud Service instances in parallel, one upgrade domain at a time</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Reboot-Cloud-Service-PaaS-b337a06d)

## <a name="next-steps"></a><span data-ttu-id="8e3ce-118">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8e3ce-118">Next Steps</span></span>
<span data-ttu-id="8e3ce-119">Теперь, когда вы познакомились с основами службы автоматизации Azure и способах ее использования для управления облачными службами Azure, пройдите по ссылкам, чтобы получить дополнительные сведения о службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="8e3ce-119">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure cloud services, follow these links to learn more about Azure Automation.</span></span>

* [<span data-ttu-id="8e3ce-120">Обзор службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="8e3ce-120">Azure Automation Overview</span></span>](../automation/automation-intro.md)
* [<span data-ttu-id="8e3ce-121">Мой первый Runbook</span><span class="sxs-lookup"><span data-stu-id="8e3ce-121">My first runbook</span></span>](../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="8e3ce-122">План обучения работе со службой автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="8e3ce-122">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)
