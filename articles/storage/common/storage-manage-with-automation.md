---
title: "Управление хранилищем Azure RemoteApp с помощью службы автоматизации Azure"
description: "Способы использования службы автоматизации Azure для управления хранилищем Azure при масштабировании."
services: storage, automation
documentationcenter: 
author: jodoglevy
manager: eamono
editor: 
ms.assetid: bac41c39-1d95-46aa-a481-ec17bbb21b40
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: eamono
ms.openlocfilehash: 4649e42a628307e15f8b067503e4e8e13f16f1af
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="managing-azure-storage-using-azure-automation"></a><span data-ttu-id="6124e-103">Управление хранилищем Azure RemoteApp с помощью службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="6124e-103">Managing Azure Storage using Azure Automation</span></span>
<span data-ttu-id="6124e-104">В этом руководстве представлена служба автоматизации Azure и описано, как ее использовать, чтобы упростить управление BLOB-объектами, таблицами и запросами хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="6124e-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of your Azure Storage blobs, tables, and queues.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="6124e-105">Что такое служба автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="6124e-105">What is Azure Automation?</span></span>
<span data-ttu-id="6124e-106">[Служба автоматизации Azure](https://azure.microsoft.com/services/automation/) — это служба Azure для упрощения управления облаком путем автоматизации процессов.</span><span class="sxs-lookup"><span data-stu-id="6124e-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="6124e-107">С помощью службы автоматизации Azure можно автоматизировать длительные, выполняемые вручную, ненадежные и часто повторяющиеся задачи, чтобы повысить надежность и эффективность, а также ускорить окупаемость инвестиций вашей организации.</span><span class="sxs-lookup"><span data-stu-id="6124e-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated to increase reliability and efficiency, and reduce time to value for your organization.</span></span>

<span data-ttu-id="6124e-108">Служба автоматизации Azure предоставляет высоконадежную и высокодоступную подсистему выполнения рабочих процессов с масштабированием в соответствии с требованиями организации по мере ее роста.</span><span class="sxs-lookup"><span data-stu-id="6124e-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales to meet your needs as your organization grows.</span></span> <span data-ttu-id="6124e-109">В службе автоматизации Azure процессы можно запустить вручную, в сторонних системах или по расписанию, чтобы все задачи выполнялись в нужное время.</span><span class="sxs-lookup"><span data-stu-id="6124e-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="6124e-110">Уменьшите операционные затраты и освободите ИТ-сотрудников и специалистов по разработке и операциям для работы над повышением бизнес-ценности ПО и автоматизации задач управления облаком в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="6124e-110">Lower operational overhead and free up IT / DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-storage"></a><span data-ttu-id="6124e-111">Как служба автоматизации Azure может помочь управлять хранилищем Azure</span><span class="sxs-lookup"><span data-stu-id="6124e-111">How can Azure Automation help manage Azure Storage?</span></span>
<span data-ttu-id="6124e-112">Службой хранилища Azure можно управлять в службе автоматизации Azure с помощью командлетов PowerShell, которые доступны в [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="6124e-112">Azure Storage can be managed in Azure Automation by using the PowerShell cmdlets that are available in [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="6124e-113">В службе автоматизации Azure эти командлеты PowerShell уже сразу доступны, поэтому все задачи управления BLOB-объектами, таблицами и запросами можно выполнять из службы.</span><span class="sxs-lookup"><span data-stu-id="6124e-113">Azure Automation has these Storage PowerShell cmdlets available out of the box, so that you can perform all of your blob, table, and queue management tasks within the service.</span></span> <span data-ttu-id="6124e-114">Вы также можете связать эти командлеты в службе автоматизации Azure с командлетами для других служб Azure, чтобы автоматизировать сложные задачи в службах Azure и системах сторонних производителей.</span><span class="sxs-lookup"><span data-stu-id="6124e-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="6124e-115">[Коллекция модулей Runbook службы автоматизации Azure](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) содержит модули Runbook различных групп разработки продуктов и сообществ, позволяющие начать работу по автоматизации управления хранилищем Azure, другими службами Azure, а также системами сторонних производителей.</span><span class="sxs-lookup"><span data-stu-id="6124e-115">The [Azure Automation runbook gallery](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contains a variety of product team and community runbooks to get started automating management of Azure Storage, other Azure services, and 3rd party systems.</span></span> <span data-ttu-id="6124e-116">Коллекция модулей Runbook содержит:</span><span class="sxs-lookup"><span data-stu-id="6124e-116">Gallery runbooks include:</span></span>

* [<span data-ttu-id="6124e-117">Удаление из службы хранилища Azure больших двоичных объектов, которым определенное число дней, с помощью службы автоматизации</span><span class="sxs-lookup"><span data-stu-id="6124e-117">Remove Azure Storage Blobs that are Certain Days Old Using Automation Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Remove-Storage-Blobs-that-aae4b761)
* [<span data-ttu-id="6124e-118">Скачивание большого двоичного объекта из службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="6124e-118">Download a Blob from Azure Storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/a-Blob-from-Azure-Storage-6bc13745)
* [<span data-ttu-id="6124e-119">Архивация всех дисков одной виртуальной машине Azure или всех виртуальных машин в облачной службе</span><span class="sxs-lookup"><span data-stu-id="6124e-119">Backup all disks for a single Azure VM or for all VMs in a Cloud Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Backup-all-disks-for-a-ede940d5)

## <a name="next-steps"></a><span data-ttu-id="6124e-120">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6124e-120">Next Steps</span></span>
<span data-ttu-id="6124e-121">Теперь, когда вы познакомились с основами службы автоматизации Azure и способами ее использования для управления BLOB-объектами, таблицами и запроса хранилища Azure, пройдите по ссылкам, чтобы получить дополнительные сведения о службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="6124e-121">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure Storage blobs, tables, and queues, follow these links to learn more about Azure Automation.</span></span>

<span data-ttu-id="6124e-122">См. руководство [Создание или импорт модуля Runbook в службе автоматизации Azure](../../automation/automation-creating-importing-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="6124e-122">See the Azure Automation tutorial [Creating or importing a runbook in Azure Automation](../../automation/automation-creating-importing-runbook.md).</span></span>

