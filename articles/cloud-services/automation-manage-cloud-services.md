---
title: "aaaManage облачных служб Azure с помощью службы автоматизации Azure | Документы Microsoft"
description: "Узнайте, как hello службы автоматизации Azure можно использовать toomanage облачных служб Azure в масштабе."
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
ms.openlocfilehash: 8e920fb94955466bfec71cc332444f5f0ee497a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-cloud-services-using-azure-automation"></a><span data-ttu-id="6ed20-103">Управление облачными службами Azure с помощью службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="6ed20-103">Managing Azure Cloud Services using Azure Automation</span></span>
<span data-ttu-id="6ed20-104">В этом руководстве приведены toohello службы автоматизации Azure и как можно использовать toosimplify управление облачных служб Azure.</span><span class="sxs-lookup"><span data-stu-id="6ed20-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of your Azure cloud services.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="6ed20-105">Что такое служба автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="6ed20-105">What is Azure Automation?</span></span>
<span data-ttu-id="6ed20-106">[Служба автоматизации Azure](https://azure.microsoft.com/services/automation/) — это служба Azure для упрощения управления облаком путем автоматизации процессов.</span><span class="sxs-lookup"><span data-stu-id="6ed20-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="6ed20-107">С помощью службы автоматизации Azure, длительные, вручную, ошибкам и часто повторяющиеся задачи может быть автоматизированные tooincrease надежность, эффективность и toovalue времени для вашей организации.</span><span class="sxs-lookup"><span data-stu-id="6ed20-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="6ed20-108">Служба автоматизации Azure обеспечивает механизм выполнения рабочих процессов очень надежное и высокой доступности, которая масштабируется toomeet вашим потребностям по мере роста организации.</span><span class="sxs-lookup"><span data-stu-id="6ed20-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="6ed20-109">В службе автоматизации Azure процессы можно запустить вручную, в сторонних системах или по расписанию, чтобы все задачи выполнялись в нужное время.</span><span class="sxs-lookup"><span data-stu-id="6ed20-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="6ed20-110">Снизить операционные издержки и освободить ИТ / автоматический запуск DevOps toofocus сотрудников на работу, которая добавляет ценность для бизнеса, перемещая toobe задачи управления вашей облачной службой автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="6ed20-110">Lower operational overhead and free up IT / DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-cloud-services"></a><span data-ttu-id="6ed20-111">Как служба автоматизации Azure помогает управлять облачными службами Azure?</span><span class="sxs-lookup"><span data-stu-id="6ed20-111">How can Azure Automation help manage Azure cloud services?</span></span>
<span data-ttu-id="6ed20-112">Облачных служб Azure можно управлять в службе автоматизации Azure с помощью командлетов PowerShell hello, которые доступны в hello [средства Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="6ed20-112">Azure cloud services can be managed in Azure Automation by using hello PowerShell cmdlets that are available in hello [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="6ed20-113">Служба автоматизации Azure имеет эти облачные службы командлетов PowerShell, доступных стандартной hello, что позволяет выполнять все задачи управления облачной службы в службе hello.</span><span class="sxs-lookup"><span data-stu-id="6ed20-113">Azure Automation has these cloud service PowerShell cmdlets available out of hello box, so that you can perform all of your cloud service management tasks within hello service.</span></span> <span data-ttu-id="6ed20-114">Также вы можете обеспечить эти командлеты в службе автоматизации Azure с помощью командлетов hello для других служб Azure, tooautomate сложные задачи служб Azure и систем сторонних разработчиков.</span><span class="sxs-lookup"><span data-stu-id="6ed20-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="6ed20-115">Некоторые примеры использования toomanage автоматизации Azure, облачных служб Azure относятся:</span><span class="sxs-lookup"><span data-stu-id="6ed20-115">Some example uses of Azure Automation toomanage Azure Cloud Services include:</span></span>

* [<span data-ttu-id="6ed20-116">непрерывное развертывание облачной службы всякий раз, когда в хранилище BLOB-объектов Azure обновляется CSCFG- или CSPKG-файл;</span><span class="sxs-lookup"><span data-stu-id="6ed20-116">Continous deployment of a Cloud Service whenever cscfg or cspkg is updated in Azure Blob storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Continuous-Deployment-of-A-eeebf3a6)
* [<span data-ttu-id="6ed20-117">параллельная перезагрузка экземпляров облачной службы, по одному домену обновления за раз.</span><span class="sxs-lookup"><span data-stu-id="6ed20-117">Rebooting Cloud Service instances in parallel, one upgrade domain at a time</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Reboot-Cloud-Service-PaaS-b337a06d)

## <a name="next-steps"></a><span data-ttu-id="6ed20-118">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6ed20-118">Next Steps</span></span>
<span data-ttu-id="6ed20-119">Теперь, когда вы узнали основы hello автоматизации Azure и как можно использовать toomanage облачных служб Azure, выполните следующие дополнительные сведения об автоматизации Azure toolearn ссылки.</span><span class="sxs-lookup"><span data-stu-id="6ed20-119">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure cloud services, follow these links toolearn more about Azure Automation.</span></span>

* [<span data-ttu-id="6ed20-120">Обзор службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="6ed20-120">Azure Automation Overview</span></span>](../automation/automation-intro.md)
* [<span data-ttu-id="6ed20-121">Мой первый Runbook</span><span class="sxs-lookup"><span data-stu-id="6ed20-121">My first runbook</span></span>](../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="6ed20-122">План обучения работе со службой автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="6ed20-122">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)
