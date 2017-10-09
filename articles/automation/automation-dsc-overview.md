---
title: "Общие сведения о DSC автоматизации aaaAzure | Документы Microsoft"
description: "Обзор DSC службы автоматизации Azure, условий использования и известных проблем"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: "PowerShell DSC, настройка требуемого состояния, PowerShell DSC для Azure"
ms.assetid: fd40cb68-c1a6-48c3-bba2-710b607d1555
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 06/15/2017
ms.author: eslesar
ms.openlocfilehash: 5b8e5104c7b5bed848c015ac26a8b7d1f5b24de9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-dsc-overview"></a><span data-ttu-id="7b4bf-104">Обзор DSC службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="7b4bf-104">Azure Automation DSC Overview</span></span>

<span data-ttu-id="7b4bf-105">Azure Automation DSC — это служба Azure, который позволяет вам toowrite, управления и компиляции конфигурации требуемого состояния (DSC) PowerShell [конфигурации](https://msdn.microsoft.com/powershell/dsc/configurations), Импорт [ресурсов DSC](https://msdn.microsoft.com/powershell/dsc/resources)и назначение узлы tootarget конфигураций в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="7b4bf-105">Azure Automation DSC is an Azure service that allows you toowrite, manage, and compile PowerShell Desired State Configuration (DSC) [configurations](https://msdn.microsoft.com/powershell/dsc/configurations), import [DSC Resources](https://msdn.microsoft.com/powershell/dsc/resources), and assign configurations tootarget nodes, all in hello cloud.</span></span>

## <a name="why-use-azure-automation-dsc"></a><span data-ttu-id="7b4bf-106">Преимущества Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="7b4bf-106">Why use Azure Automation DSC</span></span>

<span data-ttu-id="7b4bf-107">Azure Automation DSC обеспечивает ряд преимуществ по сравнению с использованием DSC за пределами Azure.</span><span class="sxs-lookup"><span data-stu-id="7b4bf-107">Azure Automation DSC provides several advantages over using DSC outside of Azure.</span></span>

### <a name="built-in-pull-server"></a><span data-ttu-id="7b4bf-108">Встроенный опрашивающий сервер</span><span class="sxs-lookup"><span data-stu-id="7b4bf-108">Built-in pull server</span></span>

<span data-ttu-id="7b4bf-109">Служба автоматизации Azure обеспечивает [опрашивающего сервера DSC](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) , чтобы целевые узлы автоматически получать конфигураций, соответствуют toohello требуемого состояния и выдавать отчеты об их соответствии.</span><span class="sxs-lookup"><span data-stu-id="7b4bf-109">Azure Automation provides a [DSC pull server](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) so that target nodes automatically receive configurations, conform toohello desired state, and report back on their compliance.</span></span>
<span data-ttu-id="7b4bf-110">Hello встроенных опрашивающего сервера в службе автоматизации Azure устраняет необходимость tooset hello вверх и ведение опрашивающего сервера.</span><span class="sxs-lookup"><span data-stu-id="7b4bf-110">hello built-in pull server in Azure Automation eliminates hello need tooset up and maintain your own pull server.</span></span>
<span data-ttu-id="7b4bf-111">Служба автоматизации Azure можно выбрать целевую виртуальных или физических Windows или Linux машин, в облаке hello или локальной.</span><span class="sxs-lookup"><span data-stu-id="7b4bf-111">Azure Automation can target virtual or physical Windows or Linux machines, in hello cloud or on-premises.</span></span>

### <a name="management-of-all-your-dsc-artifacts"></a><span data-ttu-id="7b4bf-112">Управление всеми артефактами DSC</span><span class="sxs-lookup"><span data-stu-id="7b4bf-112">Management of all your DSC artifacts</span></span>

<span data-ttu-id="7b4bf-113">Переводит Azure Automation DSC hello же уровень управления слишком[настройки требуемого состояния PowerShell](https://msdn.microsoft.com/powershell/dsc/overview) как автоматизации Azure предоставляет для создания сценариев PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7b4bf-113">Azure Automation DSC brings hello same management layer too[PowerShell Desired State Configuration](https://msdn.microsoft.com/powershell/dsc/overview) as Azure Automation offers for PowerShell scripting.</span></span>

<span data-ttu-id="7b4bf-114">Из hello портал Azure или из PowerShell можно управлять все вашей DSC конфигураций, ресурсов и целевой узлы.</span><span class="sxs-lookup"><span data-stu-id="7b4bf-114">From hello Azure portal, or from PowerShell, you can manage all your DSC configurations, resources, and target nodes.</span></span>

![Снимок экрана: колонка hello автоматизации Azure](./media/automation-dsc-overview/azure-automation-blade.png)

### <a name="import-reporting-data-into-log-analytics"></a><span data-ttu-id="7b4bf-116">Импорт данных отчетов в Log Analytics</span><span class="sxs-lookup"><span data-stu-id="7b4bf-116">Import reporting data into Log Analytics</span></span>

<span data-ttu-id="7b4bf-117">Узлы, которые управляются с помощью DSC службы автоматизации Azure отправить подробное состояние данных toohello Встроенные запросу сервера отчетов.</span><span class="sxs-lookup"><span data-stu-id="7b4bf-117">Nodes that are managed with Azure Automation DSC send detailed reporting status data toohello built-in pull server.</span></span>
<span data-ttu-id="7b4bf-118">Эта рабочая область данных tooyour анализа журналов Microsoft Operations Management Suite (OMS) можно настроить toosend DSC службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="7b4bf-118">You can configure Azure Automation DSC toosend this data tooyour Microsoft Operations Management Suite (OMS) Log Analytics workspace.</span></span>
<span data-ttu-id="7b4bf-119">tooyour данных состояния toosend DSC рабочей областью аналитики журналов, в статье toolearn [вперед DSC службы автоматизации Azure reporting tooOMS данных аналитики журналов](automation-dsc-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="7b4bf-119">toolearn how toosend DSC status data tooyour Log Analytics workspace, see [Forward Azure Automation DSC reporting data tooOMS Log Analytics](automation-dsc-diagnostics.md).</span></span>

## <a name="introduction-video"></a><span data-ttu-id="7b4bf-120">Видео: общие сведения</span><span class="sxs-lookup"><span data-stu-id="7b4bf-120">Introduction video</span></span>

<span data-ttu-id="7b4bf-121">Предпочитаете просмотра tooreading?</span><span class="sxs-lookup"><span data-stu-id="7b4bf-121">Prefer watching tooreading?</span></span> <span data-ttu-id="7b4bf-122">Рассмотрим следующие видео от мая 2015 г., при первом объявлении Azure Automation DSC hello.</span><span class="sxs-lookup"><span data-stu-id="7b4bf-122">Have a look at hello following video from May 2015, when Azure Automation DSC was first announced.</span></span>

>[!NOTE]
><span data-ttu-id="7b4bf-123">Хотя правильность hello основные понятия и жизненный цикл, рассматриваемые в этом видео, Azure Automation DSC изменилась во многом так, как это видео было записано.</span><span class="sxs-lookup"><span data-stu-id="7b4bf-123">While hello concepts and life cycle discussed in this video are correct, Azure Automation DSC has progressed a lot since this video was recorded.</span></span>
><span data-ttu-id="7b4bf-124">Теперь стал общедоступным, имеет гораздо более сложные пользовательский Интерфейс в hello портал Azure и поддерживает множество дополнительных возможностей.</span><span class="sxs-lookup"><span data-stu-id="7b4bf-124">It is now generally available, has a much more extensive UI in hello Azure portal, and supports many additional capabilities.</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3467/player]

## <a name="next-steps"></a><span data-ttu-id="7b4bf-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7b4bf-125">Next steps</span></span>

* <span data-ttu-id="7b4bf-126">toolearn toobe tooonboard узлов управляются с помощью Azure Automation DSC. в разделе [адаптации машин для управления с помощью DSC службы автоматизации Azure](automation-dsc-onboarding.md)</span><span class="sxs-lookup"><span data-stu-id="7b4bf-126">toolearn how tooonboard nodes toobe managed with Azure Automation DSC, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md)</span></span>
* <span data-ttu-id="7b4bf-127">tooget к работе с Azure Automation DSC. в разделе [Приступая к работе с Azure Automation DSC](automation-dsc-getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="7b4bf-127">tooget started using Azure Automation DSC, see [Getting started with Azure Automation DSC](automation-dsc-getting-started.md)</span></span>
* <span data-ttu-id="7b4bf-128">разделе toolearn о компиляции конфигурации DSC, в котором можно задать их узлы tootarget [компиляции конфигурации в DSC службы автоматизации Azure](automation-dsc-compile.md)</span><span class="sxs-lookup"><span data-stu-id="7b4bf-128">toolearn about compiling DSC configurations so that you can assign them tootarget nodes, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md)</span></span>
* <span data-ttu-id="7b4bf-129">Справочник по командлетам PowerShell для Azure Automation DSC приводится в статье [Azure​RM.​Automation](/powershell/module/azurerm.automation/#automation).</span><span class="sxs-lookup"><span data-stu-id="7b4bf-129">For PowerShell cmdlet reference for Azure Automation DSC, see [Azure Automation DSC cmdlets](/powershell/module/azurerm.automation/#automation)</span></span>
* <span data-ttu-id="7b4bf-130">Сведения о ценах см. на [странице с ценами на Azure Automation DSC](https://azure.microsoft.com/pricing/details/automation/).</span><span class="sxs-lookup"><span data-stu-id="7b4bf-130">For pricing information, see [Azure Automation DSC pricing](https://azure.microsoft.com/pricing/details/automation/)</span></span>
* <span data-ttu-id="7b4bf-131">см. пример использования в конвейере непрерывного развертывания Azure Automation DSC toosee [tooIaaS непрерывного развертывания виртуальных машин с помощью DSC службы автоматизации Azure и Chocolatey](automation-dsc-cd-chocolatey.md)</span><span class="sxs-lookup"><span data-stu-id="7b4bf-131">toosee an example of using Azure Automation DSC in a continuous deployment pipeline, see  [Continuous Deployment tooIaaS VMs Using Azure Automation DSC and Chocolatey](automation-dsc-cd-chocolatey.md)</span></span>
