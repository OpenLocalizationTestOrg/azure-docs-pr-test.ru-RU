---
title: "Управление веб-приложением Azure с помощью службы автоматизации Azure | Документация Майкрософт"
description: "Дополнительные сведения об использовании службы автоматизации Azure для управления веб-приложением Azure."
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
ms.openlocfilehash: a96332346747114620ee6ebd2a2d0c4417d4a213
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="managing-azure-web-app-using-azure-automation"></a><span data-ttu-id="1e562-103">Управление веб-приложением Azure с помощью службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="1e562-103">Managing Azure Web App using Azure Automation</span></span>
<span data-ttu-id="1e562-104">В этом руководстве представлена служба автоматизации Azure и способы ее использования для упрощения управления веб-приложением Azure.</span><span class="sxs-lookup"><span data-stu-id="1e562-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of Azure Web App.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="1e562-105">Что такое служба автоматизации Azure?</span><span class="sxs-lookup"><span data-stu-id="1e562-105">What is Azure Automation?</span></span>
<span data-ttu-id="1e562-106">[Служба автоматизации Azure](../automation/automation-intro.md) — это служба Azure для упрощения управления облаком путем автоматизации процессов.</span><span class="sxs-lookup"><span data-stu-id="1e562-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="1e562-107">С помощью службы автоматизации Azure повторяющиеся задачи, которые выполняются вручную, требуют много времени и подвержены ошибкам, можно автоматизировать для повышения надежности, эффективности и экономии времени в вашей организации.</span><span class="sxs-lookup"><span data-stu-id="1e562-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="1e562-108">Служба автоматизации Azure предоставляет высоконадежную и высокодоступную подсистему выполнения рабочих процессов, которая масштабируется в соответствии с вашими задачами.</span><span class="sxs-lookup"><span data-stu-id="1e562-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales to meet your needs.</span></span> <span data-ttu-id="1e562-109">В службе автоматизации Azure процессы можно запустить вручную, в сторонних системах или по расписанию, чтобы все задачи выполнялись в нужное время.</span><span class="sxs-lookup"><span data-stu-id="1e562-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="1e562-110">Уменьшите операционные затраты и освободите ИТ-сотрудников и специалистов по разработке и операциям для работы над повышением бизнес-ценности ПО и автоматизации задач управления облаком в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="1e562-110">Reduce operational overhead and free up IT and DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-web-app"></a><span data-ttu-id="1e562-111">Как служба автоматизации Azure помогает управлять веб-приложением Azure?</span><span class="sxs-lookup"><span data-stu-id="1e562-111">How can Azure Automation help manage Azure Web App?</span></span>
<span data-ttu-id="1e562-112">Веб-приложением Azure можно управлять в службе автоматизации Azure, используя командлеты PowerShell, указанные в статье [Установка и настройка Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="1e562-112">Web App can be managed in Azure Automation by using the PowerShell cmdlets that are available in the [Azure PowerShell modules](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="1e562-113">Эти [командлеты PowerShell можно установить в службе автоматизации Azure](https://azure.microsoft.com/blog/announcing-azure-resource-manager-support-azure-automation-runbooks/), чтобы выполнять все задачи управления веб-приложением, не выходя из службы.</span><span class="sxs-lookup"><span data-stu-id="1e562-113">You can [install these Web App PowerShell cmdlets in Azure Automation](https://azure.microsoft.com/blog/announcing-azure-resource-manager-support-azure-automation-runbooks/), so that you can perform all of your Web App management tasks within the service.</span></span> <span data-ttu-id="1e562-114">Кроме того, вы можете сопоставить эти командлеты в службе автоматизации Azure с командлетами для других служб Azure для автоматизации сложных задач в службах Azure и сторонних системах.</span><span class="sxs-lookup"><span data-stu-id="1e562-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="1e562-115">Ниже приведены некоторые примеры управления службами приложений с помощью средств службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="1e562-115">Here are some examples of managing App Services with Automation:</span></span>

* [<span data-ttu-id="1e562-116">Скрипты для управления веб-приложениями</span><span class="sxs-lookup"><span data-stu-id="1e562-116">Scripts for managing Web Apps</span></span>](https://azure.microsoft.com/documentation/scripts/)

## <a name="next-steps"></a><span data-ttu-id="1e562-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1e562-117">Next steps</span></span>
<span data-ttu-id="1e562-118">Теперь после знакомства с основами службы автоматизации Azure и способах ее использования для управления веб-приложением Azure пройдите по ссылкам, чтобы получить дополнительные сведения о службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="1e562-118">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure Web App, follow these links to learn more about Azure Automation.</span></span>

* <span data-ttu-id="1e562-119">Изучите [руководство по началу работы](../automation/automation-first-runbook-graphical.md) со службой автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="1e562-119">See the Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span></span>

