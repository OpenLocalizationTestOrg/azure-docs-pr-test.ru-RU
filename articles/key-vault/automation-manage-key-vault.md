---
title: "Хранилище ключей Azure, с помощью службы автоматизации Azure aaaManage | Документы Microsoft"
description: "Узнайте, как hello службы автоматизации Azure можно использовать toomanage хранилище ключей Azure."
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
ms.openlocfilehash: 7f46ecc1206a96e8aeb1d086285461cb5b205472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-key-vault-using-azure-automation"></a><span data-ttu-id="5620b-103">Управление хранилищем ключей Azure с помощью службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="5620b-103">Managing Azure Key Vault using Azure Automation</span></span>
<span data-ttu-id="5620b-104">В этом руководстве приведены toohello службы автоматизации Azure и как можно использовать toosimplify управление ключи и секретные данные в хранилище ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="5620b-104">This guide will introduce you toohello Azure Automation service and how it can be used toosimplify management of your keys and secrets in Azure Key Vault.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="5620b-105">Что такое служба автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="5620b-105">What is Azure Automation?</span></span>
<span data-ttu-id="5620b-106">[Служба автоматизации Azure](../automation/automation-intro.md) — это служба Azure, которая упрощает управление облаком благодаря автоматизации процессов и настройке требуемого состояния.</span><span class="sxs-lookup"><span data-stu-id="5620b-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation and desired state configuration.</span></span> <span data-ttu-id="5620b-107">С помощью службы автоматизации Azure, вручную, повторяющиеся, длительные и ошибкам задачи могут быть автоматизированные tooincrease надежность, эффективность и toovalue времени для вашей организации.</span><span class="sxs-lookup"><span data-stu-id="5620b-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="5620b-108">Служба автоматизации Azure обеспечивает механизм выполнения рабочих процессов высокую степень, высокой доступности, которая масштабируется toomeet вашим потребностям.</span><span class="sxs-lookup"><span data-stu-id="5620b-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="5620b-109">В службе автоматизации Azure процессы можно запустить вручную, в сторонних системах или по расписанию, чтобы все задачи выполнялись в нужное время.</span><span class="sxs-lookup"><span data-stu-id="5620b-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="5620b-110">Снизить операционные издержки и освободить ИТ и автоматический запуск DevOps toofocus сотрудников на работу, которая добавляет ценность для бизнеса, перемещая toobe задачи управления вашей облачной службой автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="5620b-110">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-key-vault"></a><span data-ttu-id="5620b-111">Как служба автоматизации Azure помогает управлять хранилищем ключей Azure?</span><span class="sxs-lookup"><span data-stu-id="5620b-111">How can Azure Automation help manage Azure Key Vault?</span></span>
<span data-ttu-id="5620b-112">Хранилище ключей можно управлять в службе автоматизации Azure с помощью hello [командлетам хранилища ключей AzureRM](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) и [командлеты классический хранилище ключей Azure](https://msdn.microsoft.com/library/azure/dn868052.aspx).</span><span class="sxs-lookup"><span data-stu-id="5620b-112">Key Vault can be managed in Azure Automation by using hello [AzureRM Key Vault cmdlets](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) and [Azure Classic Key Vault cmdlets](https://msdn.microsoft.com/library/azure/dn868052.aspx).</span></span> <span data-ttu-id="5620b-113">Здравствуйте модуль Azure для управления классический хранилище ключей доступны автоматически в службе автоматизации Azure, а также импортировать hello [модуль AzureRM KeyVault](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) в службу автоматизации Azure, что позволяет выполнять многие управления хранилищем ключей задачи в рамках службы hello.</span><span class="sxs-lookup"><span data-stu-id="5620b-113">hello Azure module for managing classic Key Vault is available automatically in Azure Automation, and you can import hello [AzureRM-KeyVault module](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) into Azure Automation, so that you can perform many of your Key Vault management tasks within hello service.</span></span> <span data-ttu-id="5620b-114">Также вы можете обеспечить эти командлеты в службе автоматизации Azure с помощью командлетов hello для других служб Azure, tooautomate сложные задачи служб Azure и систем сторонних разработчиков.</span><span class="sxs-lookup"><span data-stu-id="5620b-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="5620b-115">Эти задачи, среди прочего можно выполнять с hello командлетам хранилища ключей Azure:</span><span class="sxs-lookup"><span data-stu-id="5620b-115">With hello Azure Key Vault cmdlets you can perform these tasks among others:</span></span> 

* <span data-ttu-id="5620b-116">создавать и настраивать хранилище ключей;</span><span class="sxs-lookup"><span data-stu-id="5620b-116">Create and configure a key vault</span></span>
* <span data-ttu-id="5620b-117">создавать или импортировать ключи;</span><span class="sxs-lookup"><span data-stu-id="5620b-117">Create or import a key</span></span>
* <span data-ttu-id="5620b-118">создавать или обновлять секреты;</span><span class="sxs-lookup"><span data-stu-id="5620b-118">Create or update a secret</span></span>
* <span data-ttu-id="5620b-119">обновлять атрибуты ключей;</span><span class="sxs-lookup"><span data-stu-id="5620b-119">Update attributes of a key</span></span>
* <span data-ttu-id="5620b-120">получать ключи или секреты;</span><span class="sxs-lookup"><span data-stu-id="5620b-120">Get a key or secret</span></span>
* <span data-ttu-id="5620b-121">удалять ключи или секреты.</span><span class="sxs-lookup"><span data-stu-id="5620b-121">Delete a key or secret</span></span>

<span data-ttu-id="5620b-122">Ниже приведены несколько примеров использования PowerShell toomanage хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="5620b-122">Here are some examples of using PowerShell toomanage Key Vault:</span></span>  

* [<span data-ttu-id="5620b-123">Azure Key Vault - Step by Step (Хранилище ключей Azure: шаг за шагом)</span><span class="sxs-lookup"><span data-stu-id="5620b-123">Azure Key Vault - Step by Step</span></span>](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step)
* [<span data-ttu-id="5620b-124">Setting Up and Configuring an Azure Key Vault (Установка и настройка хранилища ключей Azure)</span><span class="sxs-lookup"><span data-stu-id="5620b-124">Setting Up and Configuring an Azure Key Vault</span></span>](https://www.simple-talk.com/cloud/platform-as-a-service/setting-up-and-configuring-an-azure-key-vault)

## <a name="next-steps"></a><span data-ttu-id="5620b-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5620b-125">Next steps</span></span>
<span data-ttu-id="5620b-126">Теперь, когда вы узнали основы hello автоматизации Azure и как можно использовать toomanage хранилище ключей Azure, выполните следующие дополнительные сведения об автоматизации Azure toolearn ссылки.</span><span class="sxs-lookup"><span data-stu-id="5620b-126">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure Key Vault, follow these links toolearn more about Azure Automation.</span></span>

* <span data-ttu-id="5620b-127">Hello Azure Automation в разделе [учебник по началу работы](../automation/automation-first-runbook-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="5620b-127">See hello Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md).</span></span>
* <span data-ttu-id="5620b-128">В разделе hello [сценариев PowerShell хранилище ключей Azure](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).</span><span class="sxs-lookup"><span data-stu-id="5620b-128">See hello [Azure Key Vault PowerShell scripts](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).</span></span>

