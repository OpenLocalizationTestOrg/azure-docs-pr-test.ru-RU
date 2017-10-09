---
title: "aaaUpdate Azure модули в службе автоматизации Azure | Документы Microsoft"
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
ms.openlocfilehash: afa404a643349f044e55be2280e435b575049dec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-azure-powershell-modules-in-azure-automation"></a><span data-ttu-id="a6585-103">Как tooupdate модули Azure PowerShell в службе автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="a6585-103">How tooupdate Azure PowerShell modules in Azure Automation</span></span>

<span data-ttu-id="a6585-104">наиболее распространенные модули Azure PowerShell Hello предоставляются по умолчанию в каждой учетной записи автоматизации.</span><span class="sxs-lookup"><span data-stu-id="a6585-104">hello most common Azure PowerShell modules are provided by default in each Automation account.</span></span>  <span data-ttu-id="a6585-105">Hello Azure команды обновления регулярно hello модули Azure, в учетной записи автоматизации hello мы предоставляют вы tooupdate hello модули в учетной записи hello Если доступны новые версии с портала hello.</span><span class="sxs-lookup"><span data-stu-id="a6585-105">hello Azure team updates hello Azure modules regularly, so in hello Automation account we provide a way for you tooupdate hello modules in hello account when new versions are available from hello portal.</span></span>  

<span data-ttu-id="a6585-106">Так как модули регулярно обновляются по группе продуктов hello, изменения могут происходить с помощью командлетов hello включены, что может отрицательно повлиять на модули Runbook в зависимости от типа hello изменения, например переименование параметра или полностью исключения устаревшего командлета.</span><span class="sxs-lookup"><span data-stu-id="a6585-106">Because modules are updated regularly by hello product group, changes can occur with hello  included cmdlets, which may negatively impact your runbooks depending on hello type of change, such as renaming a parameter or deprecating a cmdlet entirely.</span></span> <span data-ttu-id="a6585-107">модули Runbook и hello, влияющие на tooavoid процессов они автоматизации, тестирования и проверки перед продолжением настоятельно рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="a6585-107">tooavoid impacting your runbooks and hello processes they automate, it is strongly recommended that you test and validate before proceeding.</span></span>  <span data-ttu-id="a6585-108">Если выделенной учетной записи автоматизации, предназначенные для этой цели нет, рекомендуется создать один, благодаря чему можно протестировать различных сценариях и перестановок во время разработки hello из модулей Runbook, в добавление tooiterative изменения, такие как обновление hello Модули PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a6585-108">If you do not have a dedicated Automation account intended for this purpose, consider creating one so that you can test many different scenarios and permutations during hello development of your runbooks, in addition tooiterative changes such as updating hello PowerShell modules.</span></span>  <span data-ttu-id="a6585-109">После проверки результатов hello и применены необходимые изменения, продолжить согласование hello миграции все модули Runbook, необходимые изменения и выполнить обновление hello, как описано ниже в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="a6585-109">After hello results are validated and you have applied any changes required, proceed with coordinating hello migration of any runbooks that required modification and perform hello update as described below in production.</span></span>     

## <a name="updating-azure-modules"></a><span data-ttu-id="a6585-110">Обновление модулей Azure</span><span class="sxs-lookup"><span data-stu-id="a6585-110">Updating Azure Modules</span></span>

1. <span data-ttu-id="a6585-111">В модулях hello колонке вашей учетной записи автоматизации, существует вариант называется **модули Azure обновления**.</span><span class="sxs-lookup"><span data-stu-id="a6585-111">In hello Modules blade of your Automation account there is an option called **Update Azure Modules**.</span></span>  <span data-ttu-id="a6585-112">Он всегда включен.</span><span class="sxs-lookup"><span data-stu-id="a6585-112">It is always enabled.</span></span><br><br> <span data-ttu-id="a6585-113">![Параметр Update Azure Modules (Обновление модулей Azure) в колонке "Модули"](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span><span class="sxs-lookup"><span data-stu-id="a6585-113">![Update Azure Modules option in Modules blade](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span></span>

2. <span data-ttu-id="a6585-114">Нажмите кнопку **модули Azure обновления** и появляется подтверждение уведомление с вопросом, следует ли toocontinue.</span><span class="sxs-lookup"><span data-stu-id="a6585-114">Click **Update Azure Modules** and you will be presented with a confirmation notification that asks you if you want toocontinue.</span></span><br><br> <span data-ttu-id="a6585-115">![Уведомление об обновлении модулей Azure](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span><span class="sxs-lookup"><span data-stu-id="a6585-115">![Update Azure Modules notification](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span></span>

3. <span data-ttu-id="a6585-116">Нажмите кнопку **Да** и начнется процесс обновления модуля hello.</span><span class="sxs-lookup"><span data-stu-id="a6585-116">Click **Yes** and hello module update process will begin.</span></span>  <span data-ttu-id="a6585-117">процесс обновления Hello занимает около 15-20 минут tooupdate hello следующие модули:</span><span class="sxs-lookup"><span data-stu-id="a6585-117">hello update process takes about 15-20 minutes tooupdate hello following modules:</span></span>

  * <span data-ttu-id="a6585-118">Таблицы Azure</span><span class="sxs-lookup"><span data-stu-id="a6585-118">Azure</span></span>
  * <span data-ttu-id="a6585-119">Azure.Storage;</span><span class="sxs-lookup"><span data-stu-id="a6585-119">Azure.Storage</span></span>
  * <span data-ttu-id="a6585-120">AzureRm.Automation;</span><span class="sxs-lookup"><span data-stu-id="a6585-120">AzureRm.Automation</span></span>
  * <span data-ttu-id="a6585-121">AzureRm.Compute;</span><span class="sxs-lookup"><span data-stu-id="a6585-121">AzureRm.Compute</span></span>
  * <span data-ttu-id="a6585-122">AzureRm.Profile;</span><span class="sxs-lookup"><span data-stu-id="a6585-122">AzureRm.Profile</span></span>
  * <span data-ttu-id="a6585-123">AzureRm.Resources;</span><span class="sxs-lookup"><span data-stu-id="a6585-123">AzureRm.Resources</span></span>
  * <span data-ttu-id="a6585-124">AzureRm.Sql;</span><span class="sxs-lookup"><span data-stu-id="a6585-124">AzureRm.Sql</span></span>
  * <span data-ttu-id="a6585-125">AzureRm.Storage.</span><span class="sxs-lookup"><span data-stu-id="a6585-125">AzureRm.Storage</span></span>

    <span data-ttu-id="a6585-126">Модули hello, копирование toodate, процесс hello будет завершен через несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="a6585-126">If hello modules are already up toodate, then hello process will complete in a few seconds.</span></span>  <span data-ttu-id="a6585-127">После завершения процесса обновления hello вы получите уведомление.</span><span class="sxs-lookup"><span data-stu-id="a6585-127">When hello update process completes you will be notified.</span></span><br><br> ![Состояние обновления Update Azure Modules (Обновление модулей Azure)](media/automation-update-azure-modules/automation-update-azure-modules-updatestatus.png)

> [!NOTE]
> <span data-ttu-id="a6585-129">Службы автоматизации Azure будет использовать последнюю модули hello в вашей учетной записи автоматизации при запуске нового запланированного задания.</span><span class="sxs-lookup"><span data-stu-id="a6585-129">Azure Automation will use hello latest modules in your Automation account when a new scheduled job is run.</span></span>    

<span data-ttu-id="a6585-130">При использовании командлетов из этих модулей Azure PowerShell в вашей toomanage модулей Runbook Azure ресурсов, то обычно tooperform этот процесс обновления каждый месяц или т tooassure, у вас есть hello последних модулей.</span><span class="sxs-lookup"><span data-stu-id="a6585-130">If you use cmdlets from these Azure PowerShell modules in your runbooks toomanage Azure resources, then you will want tooperform this update process every month or so tooassure that you have hello latest modules.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6585-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a6585-131">Next steps</span></span>

* <span data-ttu-id="a6585-132">toolearn Дополнительные сведения о модулях интеграции и как пользовательские модули toofurther toocreate интегрировать автоматизации с других систем, служб и решений, в разделе [модули интеграции](automation-integration-modules.md).</span><span class="sxs-lookup"><span data-stu-id="a6585-132">toolearn more about Integration Modules and how toocreate custom modules toofurther integrate Automation with other systems, services, or solutions, see [Integration Modules](automation-integration-modules.md).</span></span>

* <span data-ttu-id="a6585-133">Рассмотрите возможность использования интеграции управления источника [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) или [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) toocentrally управления и контроля версий портфеля автоматизации runbook и конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a6585-133">Consider source control integration using [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) or [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) toocentrally manage and control releases of your Automation runbook and configuration portfolio.</span></span>  
