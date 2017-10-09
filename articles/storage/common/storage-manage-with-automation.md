---
title: "aaaManage хранилище Azure с помощью службы автоматизации Azure"
description: "Узнайте, как hello службы автоматизации Azure можно использовать toomanage хранилища Azure в масштабе."
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
ms.openlocfilehash: 5edfba1a9ce1f9c81b5bd0889de19099f3d86fc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-storage-using-azure-automation"></a><span data-ttu-id="0f335-103">Управление хранилищем Azure RemoteApp с помощью службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="0f335-103">Managing Azure Storage using Azure Automation</span></span>
<span data-ttu-id="0f335-104">В этом руководстве приведены toohello службы автоматизации Azure и как можно управления используется toosimplify хранилища Azure BLOB-объектов, таблиц и очередей.</span><span class="sxs-lookup"><span data-stu-id="0f335-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of your Azure Storage blobs, tables, and queues.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="0f335-105">Что такое служба автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="0f335-105">What is Azure Automation?</span></span>
<span data-ttu-id="0f335-106">[Служба автоматизации Azure](https://azure.microsoft.com/services/automation/) — это служба Azure для упрощения управления облаком путем автоматизации процессов.</span><span class="sxs-lookup"><span data-stu-id="0f335-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="0f335-107">С помощью службы автоматизации Azure, длительные, вручную, ошибкам и часто повторяющиеся заданий автоматической tooincrease надежности и эффективности и сократить время toovalue для вашей организации.</span><span class="sxs-lookup"><span data-stu-id="0f335-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability and efficiency, and reduce time toovalue for your organization.</span></span>

<span data-ttu-id="0f335-108">Служба автоматизации Azure обеспечивает механизм выполнения рабочих процессов очень надежное и высокой доступности, которая масштабируется toomeet вашим потребностям по мере роста организации.</span><span class="sxs-lookup"><span data-stu-id="0f335-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="0f335-109">В службе автоматизации Azure процессы можно запустить вручную, в сторонних системах или по расписанию, чтобы все задачи выполнялись в нужное время.</span><span class="sxs-lookup"><span data-stu-id="0f335-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="0f335-110">Снизить операционные издержки и освободить ИТ / автоматический запуск DevOps toofocus сотрудников на работу, которая добавляет ценность для бизнеса, перемещая toobe задачи управления вашей облачной службой автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="0f335-110">Lower operational overhead and free up IT / DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-storage"></a><span data-ttu-id="0f335-111">Как служба автоматизации Azure может помочь управлять хранилищем Azure</span><span class="sxs-lookup"><span data-stu-id="0f335-111">How can Azure Automation help manage Azure Storage?</span></span>
<span data-ttu-id="0f335-112">Хранилище Azure можно управлять в службе автоматизации Azure с помощью командлетов PowerShell hello, которые доступны в [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="0f335-112">Azure Storage can be managed in Azure Automation by using hello PowerShell cmdlets that are available in [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="0f335-113">Служба автоматизации Azure имеет эти доступные командлеты PowerShell хранилища стандартной hello, чтобы вы могли выполнять все BLOB-объекта, таблицы и очереди задач управления в службе hello.</span><span class="sxs-lookup"><span data-stu-id="0f335-113">Azure Automation has these Storage PowerShell cmdlets available out of hello box, so that you can perform all of your blob, table, and queue management tasks within hello service.</span></span> <span data-ttu-id="0f335-114">Также вы можете обеспечить эти командлеты в службе автоматизации Azure с помощью командлетов hello для других служб Azure, tooautomate сложные задачи служб Azure и систем сторонних разработчиков.</span><span class="sxs-lookup"><span data-stu-id="0f335-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="0f335-115">Hello [коллекции модулей runbook службы автоматизации Azure](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) содержит разнообразные продукта team и сообщества runbooks tooget работы автоматизации управления из хранилища Azure, других служб Azure и систем сторонних разработчиков.</span><span class="sxs-lookup"><span data-stu-id="0f335-115">hello [Azure Automation runbook gallery](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contains a variety of product team and community runbooks tooget started automating management of Azure Storage, other Azure services, and 3rd party systems.</span></span> <span data-ttu-id="0f335-116">Коллекция модулей Runbook содержит:</span><span class="sxs-lookup"><span data-stu-id="0f335-116">Gallery runbooks include:</span></span>

* [<span data-ttu-id="0f335-117">Удаление из службы хранилища Azure больших двоичных объектов, которым определенное число дней, с помощью службы автоматизации</span><span class="sxs-lookup"><span data-stu-id="0f335-117">Remove Azure Storage Blobs that are Certain Days Old Using Automation Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Remove-Storage-Blobs-that-aae4b761)
* [<span data-ttu-id="0f335-118">Скачивание большого двоичного объекта из службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="0f335-118">Download a Blob from Azure Storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/a-Blob-from-Azure-Storage-6bc13745)
* [<span data-ttu-id="0f335-119">Архивация всех дисков одной виртуальной машине Azure или всех виртуальных машин в облачной службе</span><span class="sxs-lookup"><span data-stu-id="0f335-119">Backup all disks for a single Azure VM or for all VMs in a Cloud Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Backup-all-disks-for-a-ede940d5)

## <a name="next-steps"></a><span data-ttu-id="0f335-120">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0f335-120">Next Steps</span></span>
<span data-ttu-id="0f335-121">Теперь, когда вы узнали основы hello автоматизации Azure и как его можно использовать toomanage, большие двоичные объекты хранилища Azure, таблиц и очередей, выполните следующие дополнительные сведения об автоматизации Azure toolearn ссылки.</span><span class="sxs-lookup"><span data-stu-id="0f335-121">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure Storage blobs, tables, and queues, follow these links toolearn more about Azure Automation.</span></span>

<span data-ttu-id="0f335-122">В разделе учебника hello автоматизации Azure [Создание или импорт модуля runbook в автоматизации Azure](../../automation/automation-creating-importing-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="0f335-122">See hello Azure Automation tutorial [Creating or importing a runbook in Azure Automation](../../automation/automation-creating-importing-runbook.md).</span></span>

