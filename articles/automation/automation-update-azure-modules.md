---
title: "Обновление модулей Azure в службе автоматизации Azure | Документация Майкрософт"
description: "В этой статье описывается, как можно обновить общие модули Azure PowerShell, предоставленные по умолчанию в службе автоматизации Azure."
services: automation
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/13/2017
ms.author: magoedte
ms.openlocfilehash: ed8c97b642d406a05817ec6c67f31a1b4bce93b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-update-azure-powershell-modules-in-azure-automation"></a><span data-ttu-id="ed3c8-103">Как обновить модули Azure PowerShell в службе автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="ed3c8-103">How to update Azure PowerShell modules in Azure Automation</span></span>

<span data-ttu-id="ed3c8-104">Наиболее распространенные модули Azure PowerShell приведены в каждой учетной записи автоматизации по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ed3c8-104">The most common Azure PowerShell modules are provided by default in each Automation account.</span></span>  <span data-ttu-id="ed3c8-105">Группа разработчиков Azure регулярно обновляет модули Azure, поэтому в учетной записи службы автоматизации мы предоставляем способ обновления модулей в учетной записи, когда на портале доступны новые версии.</span><span class="sxs-lookup"><span data-stu-id="ed3c8-105">The Azure team updates the Azure modules regularly, so in the Automation account we provide a way for you to update the modules in the account when new versions are available from the portal.</span></span>  

<span data-ttu-id="ed3c8-106">Так как модули регулярно обновляются специалистами группы продуктов, то изменения могут затронуть и входящие в них командлеты, что может негативно повлиять на работу модулей Runbook. Это зависит от типа изменения. Например, возможно переименование параметра или полное прекращение поддержки одного из командлетов.</span><span class="sxs-lookup"><span data-stu-id="ed3c8-106">Because modules are updated regularly by the product group, changes can occur with the  included cmdlets, which may negatively impact your runbooks depending on the type of change, such as renaming a parameter or deprecating a cmdlet entirely.</span></span> <span data-ttu-id="ed3c8-107">Чтобы избежать негативного влияния на модули Runbook и автоматизируемые ими процессы, настоятельно рекомендуется выполнить предварительное тестирование и проверку.</span><span class="sxs-lookup"><span data-stu-id="ed3c8-107">To avoid impacting your runbooks and the processes they automate, it is strongly recommended that you test and validate before proceeding.</span></span>  <span data-ttu-id="ed3c8-108">Если у вас нет выделенной учетной записи службы автоматизации, предназначенной для этой цели, то рекомендуется ее создать, чтобы протестировать различные сценарии и перестановки в процессе разработки модулей Runbook, а также повторяющиеся изменения, такие как обновления модулей PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ed3c8-108">If you do not have a dedicated Automation account intended for this purpose, consider creating one so that you can test many different scenarios and permutations during the development of your runbooks, in addition to iterative changes such as updating the PowerShell modules.</span></span>  <span data-ttu-id="ed3c8-109">После проверки результатов и применения необходимых изменений можно перейти к процессу переноса измененных модулей Runbook и выполнить описанное ниже обновление в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="ed3c8-109">After the results are validated and you have applied any changes required, proceed with coordinating the migration of any runbooks that required modification and perform the update as described below in production.</span></span>     

## <a name="updating-azure-modules"></a><span data-ttu-id="ed3c8-110">Обновление модулей Azure</span><span class="sxs-lookup"><span data-stu-id="ed3c8-110">Updating Azure Modules</span></span>

1. <span data-ttu-id="ed3c8-111">В колонке"Модули" вашей учетной записи службы автоматизации есть параметр под названием **Update Azure Modules** (Обновление модулей Azure).</span><span class="sxs-lookup"><span data-stu-id="ed3c8-111">In the Modules blade of your Automation account there is an option called **Update Azure Modules**.</span></span>  <span data-ttu-id="ed3c8-112">Он всегда включен.</span><span class="sxs-lookup"><span data-stu-id="ed3c8-112">It is always enabled.</span></span><br><br> <span data-ttu-id="ed3c8-113">![Параметр Update Azure Modules (Обновление модулей Azure) в колонке "Модули"](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span><span class="sxs-lookup"><span data-stu-id="ed3c8-113">![Update Azure Modules option in Modules blade](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span></span>

2. <span data-ttu-id="ed3c8-114">Щелкните **Update Azure Modules** (Обновление модулей Azure), после чего появится уведомление с запросом о продолжении.</span><span class="sxs-lookup"><span data-stu-id="ed3c8-114">Click **Update Azure Modules** and you will be presented with a confirmation notification that asks you if you want to continue.</span></span><br><br> <span data-ttu-id="ed3c8-115">![Уведомление об обновлении модулей Azure](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span><span class="sxs-lookup"><span data-stu-id="ed3c8-115">![Update Azure Modules notification](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span></span>

3. <span data-ttu-id="ed3c8-116">Щелкните **Да**, чтобы начать процесс обновления модулей.</span><span class="sxs-lookup"><span data-stu-id="ed3c8-116">Click **Yes** and the module update process will begin.</span></span>  <span data-ttu-id="ed3c8-117">Процесс обновления следующих модулей занимает около 15–20 минут:</span><span class="sxs-lookup"><span data-stu-id="ed3c8-117">The update process takes about 15-20 minutes to update the following modules:</span></span>

  * <span data-ttu-id="ed3c8-118">Таблицы Azure</span><span class="sxs-lookup"><span data-stu-id="ed3c8-118">Azure</span></span>
  * <span data-ttu-id="ed3c8-119">Azure.Storage;</span><span class="sxs-lookup"><span data-stu-id="ed3c8-119">Azure.Storage</span></span>
  * <span data-ttu-id="ed3c8-120">AzureRm.Automation;</span><span class="sxs-lookup"><span data-stu-id="ed3c8-120">AzureRm.Automation</span></span>
  * <span data-ttu-id="ed3c8-121">AzureRm.Compute;</span><span class="sxs-lookup"><span data-stu-id="ed3c8-121">AzureRm.Compute</span></span>
  * <span data-ttu-id="ed3c8-122">AzureRm.Profile;</span><span class="sxs-lookup"><span data-stu-id="ed3c8-122">AzureRm.Profile</span></span>
  * <span data-ttu-id="ed3c8-123">AzureRm.Resources;</span><span class="sxs-lookup"><span data-stu-id="ed3c8-123">AzureRm.Resources</span></span>
  * <span data-ttu-id="ed3c8-124">AzureRm.Sql;</span><span class="sxs-lookup"><span data-stu-id="ed3c8-124">AzureRm.Sql</span></span>
  * <span data-ttu-id="ed3c8-125">AzureRm.Storage.</span><span class="sxs-lookup"><span data-stu-id="ed3c8-125">AzureRm.Storage</span></span>

    <span data-ttu-id="ed3c8-126">Если модули уже обновлены, процесс будет завершен через несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="ed3c8-126">If the modules are already up to date, then the process will complete in a few seconds.</span></span>  <span data-ttu-id="ed3c8-127">После завершения процесса обновления вы получите уведомление.</span><span class="sxs-lookup"><span data-stu-id="ed3c8-127">When the update process completes you will be notified.</span></span><br><br> ![Состояние обновления Update Azure Modules (Обновление модулей Azure)](media/automation-update-azure-modules/automation-update-azure-modules-updatestatus.png)

> [!NOTE]
> <span data-ttu-id="ed3c8-129">При запуске нового запланированного задания служба автоматизации Azure будет использовать модули последней версии в вашей учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="ed3c8-129">Azure Automation will use the latest modules in your Automation account when a new scheduled job is run.</span></span>    

<span data-ttu-id="ed3c8-130">При использовании командлетов из этих модулей Azure PowerShell в модулях runbook для управления ресурсами Azure этот процесс обновления необходимо выполнять примерно каждый месяц, чтобы гарантировать наличие последних модулей.</span><span class="sxs-lookup"><span data-stu-id="ed3c8-130">If you use cmdlets from these Azure PowerShell modules in your runbooks to manage Azure resources, then you will want to perform this update process every month or so to assure that you have the latest modules.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed3c8-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ed3c8-131">Next steps</span></span>

* <span data-ttu-id="ed3c8-132">Дополнительные сведения о модулях интеграции и создании настраиваемых модулей для дальнейшей интеграции службы автоматизации с другими системами, службами и решениями см. в статье [Модули интеграции службы автоматизации Azure](automation-integration-modules.md).</span><span class="sxs-lookup"><span data-stu-id="ed3c8-132">To learn more about Integration Modules and how to create custom modules to further integrate Automation with other systems, services, or solutions, see [Integration Modules](automation-integration-modules.md).</span></span>

* <span data-ttu-id="ed3c8-133">Рассмотрите возможность интеграции системы управления версиями с помощью [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) или [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md), чтобы централизованно управлять выпусками своих модулей Runbook службы автоматизации и набором конфигураций.</span><span class="sxs-lookup"><span data-stu-id="ed3c8-133">Consider source control integration using [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) or [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) to centrally manage and control releases of your Automation runbook and configuration portfolio.</span></span>  