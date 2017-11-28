---
title: "Управление виртуальными машинами с помощью службы автоматизации Azure | Документация Майкрософт"
description: "Способы использования службы автоматизации Azure для управления виртуальными машинами Azure при масштабировании."
services: virtual-machines-windows, automation
documentationcenter: 
author: jodoglevy
manager: timlt
editor: 
ms.assetid: ce49f83a-f409-42ee-af74-a8ea2caa9ae8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2016
ms.author: timlt
ms.openlocfilehash: 15653c5d653ae538bdb66eaf0daee12c35858b45
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-virtual-machines-using-azure-automation"></a><span data-ttu-id="0a620-103">Управление виртуальными машинами Azure с помощью службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="0a620-103">Managing Azure Virtual Machines using Azure Automation</span></span>
<span data-ttu-id="0a620-104">В этом руководстве представлена служба автоматизации Azure и описано, как ее использовать, чтобы упростить управление виртуальными машинами Azure.</span><span class="sxs-lookup"><span data-stu-id="0a620-104">This guide introduces you to the Azure Automation service and how it can be used to simplify managing your Azure virtual machines.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="0a620-105">Что такое служба автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="0a620-105">What is Azure Automation?</span></span>
<span data-ttu-id="0a620-106">[Служба автоматизации Azure](https://azure.microsoft.com/services/automation/) — это служба Azure для упрощения управления облаком путем автоматизации процессов.</span><span class="sxs-lookup"><span data-stu-id="0a620-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="0a620-107">С помощью службы автоматизации Azure можно автоматизировать длительные, выполняемые вручную, ненадежные и часто повторяющиеся задачи для повышения надежности, эффективности и ускорения вывода продукта на рынок.</span><span class="sxs-lookup"><span data-stu-id="0a620-107">By using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated to increase reliability, efficiency, and time-to-value for your organization.</span></span>

<span data-ttu-id="0a620-108">Служба автоматизации Azure предоставляет высоконадежную и высокодоступную подсистему выполнения рабочих процессов с масштабированием в соответствии с требованиями организации по мере ее роста.</span><span class="sxs-lookup"><span data-stu-id="0a620-108">Azure Automation provides a highly reliable and highly available workflow execution engine that scales to meet your needs as your organization grows.</span></span> <span data-ttu-id="0a620-109">В службе автоматизации Azure процессы можно запустить вручную, в сторонних системах или по расписанию, чтобы все задачи выполнялись в нужное время.</span><span class="sxs-lookup"><span data-stu-id="0a620-109">In Azure Automation, processes can be kicked off manually, by third-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="0a620-110">Вы можете уменьшить операционные затраты и освободить сотрудников отделов ИТ и разработки и операций для работы над повышением бизнес-ценности ПО и автоматизации задач управления облаком в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="0a620-110">You can lower operational overhead and free up IT and DevOps staff to focus on work that adds business value by running your cloud management tasks automatically with Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-virtual-machines"></a><span data-ttu-id="0a620-111">Как служба автоматизации Azure может помочь управлять виртуальными машинами Azure</span><span class="sxs-lookup"><span data-stu-id="0a620-111">How can Azure Automation help manage Azure virtual machines?</span></span>
<span data-ttu-id="0a620-112">Виртуальными машинами можно управлять с помощью службы автоматизации Azure, используя [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="0a620-112">Virtual machines can be managed in Azure Automation by using [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="0a620-113">Служба автоматизации Azure включает в себя командлеты PowerShell, позволяющие выполнять все задачи управления виртуальными машинами при помощи этой службы.</span><span class="sxs-lookup"><span data-stu-id="0a620-113">Azure Automation includes the Azure PowerShell cmdlets, so you can perform all of your virtual machine management tasks within the service.</span></span> <span data-ttu-id="0a620-114">Вы также можете связать эти командлеты в службе автоматизации Azure с командлетами для других служб Azure, чтобы автоматизировать сложные задачи в службах Azure и системах сторонних производителей.</span><span class="sxs-lookup"><span data-stu-id="0a620-114">You can also pair the cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and third-party systems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a620-115">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0a620-115">Next steps</span></span>
<span data-ttu-id="0a620-116">Теперь, ознакомившись с основами службы автоматизации Azure и способами ее использования для управления виртуальными машинами, вы можете узнать больше:</span><span class="sxs-lookup"><span data-stu-id="0a620-116">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure virtual machines, learn more:</span></span>

* [<span data-ttu-id="0a620-117">Обзор службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="0a620-117">Azure Automation Overview</span></span>](../../automation/automation-intro.md)
* [<span data-ttu-id="0a620-118">Мой первый Runbook</span><span class="sxs-lookup"><span data-stu-id="0a620-118">My first runbook</span></span>](../../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="0a620-119">План обучения работе со службой автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="0a620-119">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)

