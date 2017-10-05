---
title: "Обзор Azure Automation DSC | Документация Майкрософт"
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
ms.openlocfilehash: 468321fa6863d78bc0d179fbe5c2ed6195040d50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-dsc-overview"></a><span data-ttu-id="3c8d0-104">Обзор DSC службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="3c8d0-104">Azure Automation DSC Overview</span></span>

<span data-ttu-id="3c8d0-105">Azure Automation DSC — это служба Azure, которая позволяет создавать и компилировать [конфигурации](https://msdn.microsoft.com/powershell/dsc/configurations) Desired State Configuration (DSC) PowerShell, управлять ими, импортировать [ресурсы DSC](https://msdn.microsoft.com/powershell/dsc/resources), а также назначать конфигурации целевым узлам, и все это в облаке.</span><span class="sxs-lookup"><span data-stu-id="3c8d0-105">Azure Automation DSC is an Azure service that allows you to write, manage, and compile PowerShell Desired State Configuration (DSC) [configurations](https://msdn.microsoft.com/powershell/dsc/configurations), import [DSC Resources](https://msdn.microsoft.com/powershell/dsc/resources), and assign configurations to target nodes, all in the cloud.</span></span>

## <a name="why-use-azure-automation-dsc"></a><span data-ttu-id="3c8d0-106">Преимущества Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="3c8d0-106">Why use Azure Automation DSC</span></span>

<span data-ttu-id="3c8d0-107">Azure Automation DSC обеспечивает ряд преимуществ по сравнению с использованием DSC за пределами Azure.</span><span class="sxs-lookup"><span data-stu-id="3c8d0-107">Azure Automation DSC provides several advantages over using DSC outside of Azure.</span></span>

### <a name="built-in-pull-server"></a><span data-ttu-id="3c8d0-108">Встроенный опрашивающий сервер</span><span class="sxs-lookup"><span data-stu-id="3c8d0-108">Built-in pull server</span></span>

<span data-ttu-id="3c8d0-109">Служба автоматизации Azure предоставляет [опрашивающий сервер DSC](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver), чтобы целевые узлы могли автоматически получать конфигурации, переходить в требуемое состояние и сообщать о готовности.</span><span class="sxs-lookup"><span data-stu-id="3c8d0-109">Azure Automation provides a [DSC pull server](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) so that target nodes automatically receive configurations, conform to the desired state, and report back on their compliance.</span></span>
<span data-ttu-id="3c8d0-110">Встроенный опрашивающий сервер в службе автоматизации Azure избавляет от необходимости устанавливать и обслуживать собственный опрашивающий сервер.</span><span class="sxs-lookup"><span data-stu-id="3c8d0-110">The built-in pull server in Azure Automation eliminates the need to set up and maintain your own pull server.</span></span>
<span data-ttu-id="3c8d0-111">Служба автоматизации Azure может работать с виртуальными и физическими машинами под управлением Windows или Linux, размещенными в облаке или локально.</span><span class="sxs-lookup"><span data-stu-id="3c8d0-111">Azure Automation can target virtual or physical Windows or Linux machines, in the cloud or on-premises.</span></span>

### <a name="management-of-all-your-dsc-artifacts"></a><span data-ttu-id="3c8d0-112">Управление всеми артефактами DSC</span><span class="sxs-lookup"><span data-stu-id="3c8d0-112">Management of all your DSC artifacts</span></span>

<span data-ttu-id="3c8d0-113">Azure Automation DSC обеспечивает тот же слой управления для [Desired State Configuration PowerShell](https://msdn.microsoft.com/powershell/dsc/overview), что и служба автоматизации Azure предлагает для сценариев PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3c8d0-113">Azure Automation DSC brings the same management layer to [PowerShell Desired State Configuration](https://msdn.microsoft.com/powershell/dsc/overview) as Azure Automation offers for PowerShell scripting.</span></span>

<span data-ttu-id="3c8d0-114">Вы можете управлять всеми конфигурациями, ресурсами и целевыми узлами DSC с помощью портала Azure или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3c8d0-114">From the Azure portal, or from PowerShell, you can manage all your DSC configurations, resources, and target nodes.</span></span>

![Снимок экрана колонки службы автоматизации Azure](./media/automation-dsc-overview/azure-automation-blade.png)

### <a name="import-reporting-data-into-log-analytics"></a><span data-ttu-id="3c8d0-116">Импорт данных отчетов в Log Analytics</span><span class="sxs-lookup"><span data-stu-id="3c8d0-116">Import reporting data into Log Analytics</span></span>

<span data-ttu-id="3c8d0-117">Узлы, которые управляются с помощью Azure Automation DSC, отправляют на встроенный опрашивающий сервер подробные отчеты с данными о состоянии.</span><span class="sxs-lookup"><span data-stu-id="3c8d0-117">Nodes that are managed with Azure Automation DSC send detailed reporting status data to the built-in pull server.</span></span>
<span data-ttu-id="3c8d0-118">В Azure Automation DSC можно настроить отправку этих данных в рабочую область Log Analytics в Microsoft Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="3c8d0-118">You can configure Azure Automation DSC to send this data to your Microsoft Operations Management Suite (OMS) Log Analytics workspace.</span></span>
<span data-ttu-id="3c8d0-119">Сведения об отправке данных о состоянии DSC в рабочую область Log Analytics см. в статье [Пересылка данных отчетов Azure Automation DSC в OMS Log Analytics](automation-dsc-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="3c8d0-119">To learn how to send DSC status data to your Log Analytics workspace, see [Forward Azure Automation DSC reporting data to OMS Log Analytics](automation-dsc-diagnostics.md).</span></span>

## <a name="introduction-video"></a><span data-ttu-id="3c8d0-120">Видео: общие сведения</span><span class="sxs-lookup"><span data-stu-id="3c8d0-120">Introduction video</span></span>

<span data-ttu-id="3c8d0-121">Предпочитаете смотреть, а не читать?</span><span class="sxs-lookup"><span data-stu-id="3c8d0-121">Prefer watching to reading?</span></span> <span data-ttu-id="3c8d0-122">Посмотрите следующий видеоролик, выпущенный в мае 2015 г., когда впервые было объявлено о создании службы Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="3c8d0-122">Have a look at the following video from May 2015, when Azure Automation DSC was first announced.</span></span>

>[!NOTE]
><span data-ttu-id="3c8d0-123">Несмотря на то, что основные концепции и жизненный цикл, о которых рассказывается в этом видеоролике, по-прежнему актуальны, с момента записи этого видеоролика Azure Automation DSC сделала большой шаг вперед.</span><span class="sxs-lookup"><span data-stu-id="3c8d0-123">While the concepts and life cycle discussed in this video are correct, Azure Automation DSC has progressed a lot since this video was recorded.</span></span>
><span data-ttu-id="3c8d0-124">Теперь она стала общедоступной, оснащена более функциональным пользовательским интерфейсом на портале Azure и поддерживает множество дополнительных возможностей.</span><span class="sxs-lookup"><span data-stu-id="3c8d0-124">It is now generally available, has a much more extensive UI in the Azure portal, and supports many additional capabilities.</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3467/player]

## <a name="next-steps"></a><span data-ttu-id="3c8d0-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3c8d0-125">Next steps</span></span>

* <span data-ttu-id="3c8d0-126">Сведения о развертывании узлов для управления с помощью Azure Automation DSC см. в статье [Подключение компьютеров для управления с помощью Azure Automation DSC](automation-dsc-onboarding.md).</span><span class="sxs-lookup"><span data-stu-id="3c8d0-126">To learn how to onboard nodes to be managed with Azure Automation DSC, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md)</span></span>
* <span data-ttu-id="3c8d0-127">Чтобы начать работу с Azure Automation DSC, см. статью [Приступая к работе с Azure Automation DSC](automation-dsc-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="3c8d0-127">To get started using Azure Automation DSC, see [Getting started with Azure Automation DSC](automation-dsc-getting-started.md)</span></span>
* <span data-ttu-id="3c8d0-128">Сведения о компиляции конфигураций DSC, которые затем можно назначить целевым узлам, см. в статье [Компиляция конфигураций в Azure Automation DSC](automation-dsc-compile.md).</span><span class="sxs-lookup"><span data-stu-id="3c8d0-128">To learn about compiling DSC configurations so that you can assign them to target nodes, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md)</span></span>
* <span data-ttu-id="3c8d0-129">Справочник по командлетам PowerShell для Azure Automation DSC приводится в статье [Azure​RM.​Automation](/powershell/module/azurerm.automation/#automation).</span><span class="sxs-lookup"><span data-stu-id="3c8d0-129">For PowerShell cmdlet reference for Azure Automation DSC, see [Azure Automation DSC cmdlets](/powershell/module/azurerm.automation/#automation)</span></span>
* <span data-ttu-id="3c8d0-130">Сведения о ценах см. на [странице с ценами на Azure Automation DSC](https://azure.microsoft.com/pricing/details/automation/).</span><span class="sxs-lookup"><span data-stu-id="3c8d0-130">For pricing information, see [Azure Automation DSC pricing](https://azure.microsoft.com/pricing/details/automation/)</span></span>
* <span data-ttu-id="3c8d0-131">Пример использования Azure Automation DSC в конвейере непрерывного развертывания см. в разделе [непрерывного развертывания IaaS виртуальных машин с помощью DSC службы автоматизации Azure и Chocolatey](automation-dsc-cd-chocolatey.md)</span><span class="sxs-lookup"><span data-stu-id="3c8d0-131">To see an example of using Azure Automation DSC in a continuous deployment pipeline, see  [Continuous Deployment to IaaS VMs Using Azure Automation DSC and Chocolatey](automation-dsc-cd-chocolatey.md)</span></span>