---
title: "Параметры Runbook | Документация Майкрософт"
description: "Описываются параметры конфигурации для модуля Runbook службы автоматизации Azure и то, как изменить их с помощью портала управления Azure и Windows PowerShell."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: a726f20c-a952-48b8-88ee-36d76aa3ac61
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/11/2016
ms.author: bwren
ms.openlocfilehash: 20ecbc270e61d234e026e6ba2634c7aad63b3355
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="runbook-settings"></a><span data-ttu-id="cae32-103">Параметры модуля Runbook</span><span class="sxs-lookup"><span data-stu-id="cae32-103">Runbook settings</span></span>
<span data-ttu-id="cae32-104">Каждый модуль Runbook в службе автоматизации Azure имеет несколько параметров, которые помогут определить его и изменить его поведение при ведении журнала.</span><span class="sxs-lookup"><span data-stu-id="cae32-104">Each runbook in Azure Automation has multiple settings that help it to be identified and to change its logging behavior.</span></span> <span data-ttu-id="cae32-105">Каждый из этих параметров описан ниже, рядом с ним приводятся пояснения об изменении его значения.</span><span class="sxs-lookup"><span data-stu-id="cae32-105">Each of these settings is described below followed by procedures on how to modify them.</span></span>

## <a name="settings"></a><span data-ttu-id="cae32-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="cae32-106">Settings</span></span>
### <a name="name-and-description"></a><span data-ttu-id="cae32-107">Имя и описание</span><span class="sxs-lookup"><span data-stu-id="cae32-107">Name and description</span></span>
<span data-ttu-id="cae32-108">Имя модуля Runbook нельзя изменить после его создания.</span><span class="sxs-lookup"><span data-stu-id="cae32-108">You cannot change the name of a runbook after it has been created.</span></span> <span data-ttu-id="cae32-109">Описание не обязательно и может содержать до 512 символов.</span><span class="sxs-lookup"><span data-stu-id="cae32-109">The Description is optional and can be up to 512 characters.</span></span>

### <a name="tags"></a><span data-ttu-id="cae32-110">Теги</span><span class="sxs-lookup"><span data-stu-id="cae32-110">Tags</span></span>
<span data-ttu-id="cae32-111">Теги позволяют назначать отдельные слова и фразы для идентификации модуля Runbook.</span><span class="sxs-lookup"><span data-stu-id="cae32-111">Tags allow you to assign distinct words and phrases to help identify a runbook.</span></span> <span data-ttu-id="cae32-112">Например, при отправке модуля Runbook в [коллекцию PowerShell](https://www.powershellgallery.com/) можно указать определенные теги для идентификации категорий, к которым должен относиться модуль Runbook.</span><span class="sxs-lookup"><span data-stu-id="cae32-112">For example, when you submit a runbook to the [PowerShell Gallery](https://www.powershellgallery.com/), you specify particular tags to identify which categories the runbook should be listed in.</span></span> <span data-ttu-id="cae32-113">Вы можете указать несколько тегов модуля Runbook, разделив их запятой.</span><span class="sxs-lookup"><span data-stu-id="cae32-113">You can specify multiple tags for a runbook by separating them with commas.</span></span>

### <a name="logging"></a><span data-ttu-id="cae32-114">Ведение журналов</span><span class="sxs-lookup"><span data-stu-id="cae32-114">Logging</span></span>
<span data-ttu-id="cae32-115">По умолчанию записи Verbose и Progress не записываются в журнал заданий.</span><span class="sxs-lookup"><span data-stu-id="cae32-115">By default, Verbose and Progress records are not written to job history.</span></span> <span data-ttu-id="cae32-116">Вы можете изменить параметры для определенного модуля Runbook, чтобы записывать эти записи.</span><span class="sxs-lookup"><span data-stu-id="cae32-116">You can change the settings for a particular runbook to log these records.</span></span> <span data-ttu-id="cae32-117">Дополнительные сведения об этих записях см. в статье [Выходные данные и сообщения Runbook в службе автоматизации Azure](automation-runbook-output-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="cae32-117">For more information on these records, see [Runbook Output and Messages](automation-runbook-output-and-messages.md).</span></span>

## <a name="changing-runbook-settings"></a><span data-ttu-id="cae32-118">Изменение параметров модуля Runbook</span><span class="sxs-lookup"><span data-stu-id="cae32-118">Changing runbook settings</span></span>

### <a name="changing-runbook-settings-with-the-azure-portal"></a><span data-ttu-id="cae32-119">Изменение параметров модуля Runbook с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="cae32-119">Changing runbook settings with the Azure portal</span></span>
<span data-ttu-id="cae32-120">Параметры модуля Runbook можно изменить на портале Azure в колонке **Параметры** модуля Runbook.</span><span class="sxs-lookup"><span data-stu-id="cae32-120">You can change settings for a runbook in the Azure portal from the **Settings** blade for the runbook.</span></span>

1. <span data-ttu-id="cae32-121">На портале Azure щелкните **Служба автоматизации** и затем имя учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="cae32-121">In the Azure portal, select **Automation** and then then click the name of an automation account.</span></span>
2. <span data-ttu-id="cae32-122">Выберите вкладку **Модули Runbook** .</span><span class="sxs-lookup"><span data-stu-id="cae32-122">Select the **Runbooks** tab.</span></span>
3. <span data-ttu-id="cae32-123">Щелкните имя модуля Runbook. Откроется колонка "Параметры" выбранного модуля.</span><span class="sxs-lookup"><span data-stu-id="cae32-123">Click the name of a runbook and you are directed to the settings blade for the runbook.</span></span> <span data-ttu-id="cae32-124">В ней вы можете указать или изменить теги, ввести описание модуля Runbook, настроить параметры ведения журнала и трассировки, а также получить доступ к средствам поддержки, которые помогут устранить возникшие проблемы.</span><span class="sxs-lookup"><span data-stu-id="cae32-124">From here you can specify or modify tags, the runbook description, configure logging and tracing settings, and access support tools to help you solve problems.</span></span>     

### <a name="changing-runbook-settings-with-windows-powershell"></a><span data-ttu-id="cae32-125">Изменение параметров модуля Runbook с помощью Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="cae32-125">Changing runbook settings with Windows PowerShell</span></span>
<span data-ttu-id="cae32-126">Для изменения параметров модуля Runbook можно воспользоваться командлетом [Set-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx).</span><span class="sxs-lookup"><span data-stu-id="cae32-126">You can use the [Set-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx) cmdlet to change the settings for a runbook.</span></span> <span data-ttu-id="cae32-127">Если вы хотите указать несколько тегов, вы можете предоставить массив или единую строку со значениями, разделенными запятыми, в параметр Tags.</span><span class="sxs-lookup"><span data-stu-id="cae32-127">If you want to specify multiple tags, you can either provide an array or a single string with comma delimited values to the Tags parameter.</span></span> <span data-ttu-id="cae32-128">С помощью командлета [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx) можно получить текущие теги.</span><span class="sxs-lookup"><span data-stu-id="cae32-128">You can get the current tags with the [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).</span></span>

<span data-ttu-id="cae32-129">Приведенные образцы команд показывают, как установить свойства для модуля Runbook.</span><span class="sxs-lookup"><span data-stu-id="cae32-129">The following sample commands show how to set the properties for a runbook.</span></span> <span data-ttu-id="cae32-130">В этом примере к существующим тегам добавляются три тега и указывается, что необходимо вести запись подробных записей.</span><span class="sxs-lookup"><span data-stu-id="cae32-130">This sample adds three tags to the existing tags and specifies that verbose records should be logged.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $tags = (Get-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName).Tags
    $tags += "Tag1,Tag2,Tag3"
    Set-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName –LogVerbose $true –Tags $tags

## <a name="next-steps"></a><span data-ttu-id="cae32-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cae32-131">Next steps</span></span>
* <span data-ttu-id="cae32-132">Чтобы узнать, как создавать и извлекать выходные данные и сообщения об ошибках из модулей Runbook, ознакомьтесь со статьей [Выходные данные и сообщения Runbook в службе автоматизации Azure](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="cae32-132">To learn how to create and retrieve output and error messages from runbooks, see [Runbook Output and Messages](automation-runbook-output-and-messages.md)</span></span> 
* <span data-ttu-id="cae32-133">Сведения о добавлении модуля Runbook, который уже был разработан сообществом или взят из другого источника, а также сведения о создании собственного модуля Runbook см. в статье [Создание или импорт модуля Runbook](automation-creating-importing-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="cae32-133">To understand how to add a runbook that was already developed by the community or other source, or to create your own runbook see [Creating or Importing a Runbook](automation-creating-importing-runbook.md)</span></span> 

