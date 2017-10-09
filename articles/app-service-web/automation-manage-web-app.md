---
title: "aaaManage веб-приложения Azure с помощью службы автоматизации Azure | Документы Microsoft"
description: "Узнайте, как hello службы автоматизации Azure можно использовать toomanage веб-приложения Azure."
services: app-service\web, automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: c960a44f-f941-401d-afba-a4bc0f0394eb
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: magoedte
ms.openlocfilehash: 6d80351a2927f26753cfbaead6e1c0c3c94e86e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-web-app-using-azure-automation"></a><span data-ttu-id="b2d28-103">Управление веб-приложением Azure с помощью службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="b2d28-103">Managing Azure Web App using Azure Automation</span></span>
<span data-ttu-id="b2d28-104">В этом руководстве приведены toohello службы автоматизации Azure и как можно использовать toosimplify управление веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="b2d28-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of Azure Web App.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="b2d28-105">Что такое служба автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="b2d28-105">What is Azure Automation?</span></span>
<span data-ttu-id="b2d28-106">[Служба автоматизации Azure](../automation/automation-intro.md) — это служба Azure для упрощения управления облаком путем автоматизации процессов.</span><span class="sxs-lookup"><span data-stu-id="b2d28-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="b2d28-107">С помощью службы автоматизации Azure, вручную, повторяющиеся, длительные и ошибкам задачи могут быть автоматизированные tooincrease надежность, эффективность и toovalue времени для вашей организации.</span><span class="sxs-lookup"><span data-stu-id="b2d28-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="b2d28-108">Служба автоматизации Azure обеспечивает механизм выполнения рабочих процессов высокую степень, высокой доступности, которая масштабируется toomeet вашим потребностям.</span><span class="sxs-lookup"><span data-stu-id="b2d28-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="b2d28-109">В службе автоматизации Azure процессы можно запустить вручную, в сторонних системах или по расписанию, чтобы все задачи выполнялись в нужное время.</span><span class="sxs-lookup"><span data-stu-id="b2d28-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="b2d28-110">Снизить операционные издержки и освободить ИТ и автоматический запуск DevOps toofocus сотрудников на работу, которая добавляет ценность для бизнеса, перемещая toobe задачи управления вашей облачной службой автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="b2d28-110">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-web-app"></a><span data-ttu-id="b2d28-111">Как служба автоматизации Azure помогает управлять веб-приложением Azure?</span><span class="sxs-lookup"><span data-stu-id="b2d28-111">How can Azure Automation help manage Azure Web App?</span></span>
<span data-ttu-id="b2d28-112">Можно управлять веб-приложения в службе автоматизации Azure с помощью командлетов PowerShell hello, которые доступны в hello [модули Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="b2d28-112">Web App can be managed in Azure Automation by using hello PowerShell cmdlets that are available in hello [Azure PowerShell modules](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="b2d28-113">Вы можете [установить эти командлеты PowerShell веб приложения в службе автоматизации Azure](https://azure.microsoft.com/blog/announcing-azure-resource-manager-support-azure-automation-runbooks/), после чего можно выполнять все задачи управления веб-приложения в службе hello.</span><span class="sxs-lookup"><span data-stu-id="b2d28-113">You can [install these Web App PowerShell cmdlets in Azure Automation](https://azure.microsoft.com/blog/announcing-azure-resource-manager-support-azure-automation-runbooks/), so that you can perform all of your Web App management tasks within hello service.</span></span> <span data-ttu-id="b2d28-114">Также вы можете обеспечить эти командлеты в службе автоматизации Azure с помощью командлетов hello для других служб Azure tooautomate сложных задач служб Azure и систем сторонних разработчиков.</span><span class="sxs-lookup"><span data-stu-id="b2d28-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="b2d28-115">Ниже приведены некоторые примеры управления службами приложений с помощью средств службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="b2d28-115">Here are some examples of managing App Services with Automation:</span></span>

* [<span data-ttu-id="b2d28-116">Скрипты для управления веб-приложениями</span><span class="sxs-lookup"><span data-stu-id="b2d28-116">Scripts for managing Web Apps</span></span>](https://azure.microsoft.com/documentation/scripts/)

## <a name="next-steps"></a><span data-ttu-id="b2d28-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b2d28-117">Next steps</span></span>
<span data-ttu-id="b2d28-118">Теперь, когда вы узнали основы hello автоматизации Azure и как можно использовать toomanage веб-приложения Azure, выполните следующие дополнительные сведения об автоматизации Azure toolearn ссылки.</span><span class="sxs-lookup"><span data-stu-id="b2d28-118">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure Web App, follow these links toolearn more about Azure Automation.</span></span>

* <span data-ttu-id="b2d28-119">Hello Azure Automation в разделе [учебник по началу работы](../automation/automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="b2d28-119">See hello Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span></span>

