---
title: "Управление хранилищем ключей Azure с помощью службы автоматизации Azure | Документация Майкрософт"
description: "Сведения об использовании службы автоматизации Azure для управления хранилищем ключей Azure."
services: Key-Vault, automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 4e780762-19b6-4ca6-b894-ebb44c538f35
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: magoedte;csand
ms.openlocfilehash: dee39662472fe54776b591977f2b1ecb39d15b00
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-key-vault-using-azure-automation"></a><span data-ttu-id="23e8e-103">Управление хранилищем ключей Azure с помощью службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="23e8e-103">Managing Azure Key Vault using Azure Automation</span></span>
<span data-ttu-id="23e8e-104">В этом руководстве будет представлена служба автоматизации Azure и показано, как ее использовать для упрощения управления ключами и секретами в хранилище ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="23e8e-104">This guide will introduce you to the Azure Automation service and how it can be used to simplify management of your keys and secrets in Azure Key Vault.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="23e8e-105">Что такое служба автоматизации Azure?</span><span class="sxs-lookup"><span data-stu-id="23e8e-105">What is Azure Automation?</span></span>
<span data-ttu-id="23e8e-106">[Служба автоматизации Azure](../automation/automation-intro.md) — это служба Azure, которая упрощает управление облаком благодаря автоматизации процессов и настройке требуемого состояния.</span><span class="sxs-lookup"><span data-stu-id="23e8e-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation and desired state configuration.</span></span> <span data-ttu-id="23e8e-107">С помощью службы автоматизации Azure повторяющиеся задачи, которые выполняются вручную, требуют много времени и подвержены ошибкам, можно автоматизировать для повышения надежности, эффективности и экономии времени в вашей организации.</span><span class="sxs-lookup"><span data-stu-id="23e8e-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="23e8e-108">Служба автоматизации Azure предоставляет высоконадежную и высокодоступную подсистему выполнения рабочих процессов, которая масштабируется в соответствии с вашими задачами.</span><span class="sxs-lookup"><span data-stu-id="23e8e-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales to meet your needs.</span></span> <span data-ttu-id="23e8e-109">В службе автоматизации Azure процессы можно запустить вручную, в сторонних системах или по расписанию, чтобы все задачи выполнялись в нужное время.</span><span class="sxs-lookup"><span data-stu-id="23e8e-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="23e8e-110">Уменьшите операционные затраты и освободите ИТ-сотрудников и DevOps для работы над повышением бизнес-ценности ПО и автоматизации задач управления облаком в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="23e8e-110">Reduce operational overhead and free up IT and DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-key-vault"></a><span data-ttu-id="23e8e-111">Как служба автоматизации Azure помогает управлять хранилищем ключей Azure?</span><span class="sxs-lookup"><span data-stu-id="23e8e-111">How can Azure Automation help manage Azure Key Vault?</span></span>
<span data-ttu-id="23e8e-112">Хранилищем ключей можно управлять в службе автоматизации Azure с помощью [командлетов хранилища ключей AzureRM](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) и [командлетов классического хранилища ключей Azure](https://msdn.microsoft.com/library/azure/dn868052.aspx).</span><span class="sxs-lookup"><span data-stu-id="23e8e-112">Key Vault can be managed in Azure Automation by using the [AzureRM Key Vault cmdlets](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) and [Azure Classic Key Vault cmdlets](https://msdn.microsoft.com/library/azure/dn868052.aspx).</span></span> <span data-ttu-id="23e8e-113">Модуль Azure для управления классическим хранилищем ключей автоматически доступен в службе автоматизации Azure, и вы можете импортировать [модуль AzureRM-KeyVault](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) в службу автоматизации Azure. Это позволит выполнять многие задачи управления хранилищем ключей в службе.</span><span class="sxs-lookup"><span data-stu-id="23e8e-113">The Azure module for managing classic Key Vault is available automatically in Azure Automation, and you can import the [AzureRM-KeyVault module](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) into Azure Automation, so that you can perform many of your Key Vault management tasks within the service.</span></span> <span data-ttu-id="23e8e-114">Вы также можете связать эти командлеты в службе автоматизации Azure с командлетами для других служб Azure, чтобы автоматизировать сложные задачи в службах Azure и системах сторонних производителей.</span><span class="sxs-lookup"><span data-stu-id="23e8e-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="23e8e-115">С помощью командлетов хранилища ключей Azure можно выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="23e8e-115">With the Azure Key Vault cmdlets you can perform these tasks among others:</span></span> 

* <span data-ttu-id="23e8e-116">создавать и настраивать хранилище ключей;</span><span class="sxs-lookup"><span data-stu-id="23e8e-116">Create and configure a key vault</span></span>
* <span data-ttu-id="23e8e-117">создавать или импортировать ключи;</span><span class="sxs-lookup"><span data-stu-id="23e8e-117">Create or import a key</span></span>
* <span data-ttu-id="23e8e-118">создавать или обновлять секреты;</span><span class="sxs-lookup"><span data-stu-id="23e8e-118">Create or update a secret</span></span>
* <span data-ttu-id="23e8e-119">обновлять атрибуты ключей;</span><span class="sxs-lookup"><span data-stu-id="23e8e-119">Update attributes of a key</span></span>
* <span data-ttu-id="23e8e-120">получать ключи или секреты;</span><span class="sxs-lookup"><span data-stu-id="23e8e-120">Get a key or secret</span></span>
* <span data-ttu-id="23e8e-121">удалять ключи или секреты.</span><span class="sxs-lookup"><span data-stu-id="23e8e-121">Delete a key or secret</span></span>

<span data-ttu-id="23e8e-122">Вот несколько примеров использования PowerShell для управления хранилищем ключей.</span><span class="sxs-lookup"><span data-stu-id="23e8e-122">Here are some examples of using PowerShell to manage Key Vault:</span></span>  

* [<span data-ttu-id="23e8e-123">Azure Key Vault - Step by Step (Хранилище ключей Azure: шаг за шагом)</span><span class="sxs-lookup"><span data-stu-id="23e8e-123">Azure Key Vault - Step by Step</span></span>](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step)
* [<span data-ttu-id="23e8e-124">Setting Up and Configuring an Azure Key Vault (Установка и настройка хранилища ключей Azure)</span><span class="sxs-lookup"><span data-stu-id="23e8e-124">Setting Up and Configuring an Azure Key Vault</span></span>](https://www.simple-talk.com/cloud/platform-as-a-service/setting-up-and-configuring-an-azure-key-vault)

## <a name="next-steps"></a><span data-ttu-id="23e8e-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="23e8e-125">Next steps</span></span>
<span data-ttu-id="23e8e-126">Теперь, когда вы познакомились с основами службы автоматизации Azure и способами ее использования для управления хранилищем ключей Azure, пройдите по ссылкам, чтобы получить дополнительные сведения о службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="23e8e-126">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure Key Vault, follow these links to learn more about Azure Automation.</span></span>

* <span data-ttu-id="23e8e-127">Изучите [руководство по началу работы](../automation/automation-first-runbook-graphical.md)со службой автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="23e8e-127">See the Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md).</span></span>
* <span data-ttu-id="23e8e-128">Изучите раздел [Скрипты PowerShell хранилища ключей Azure](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).</span><span class="sxs-lookup"><span data-stu-id="23e8e-128">See the [Azure Key Vault PowerShell scripts](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).</span></span>

