---
title: "Параметры aaaRunbook | Документы Microsoft"
description: "Описывает hello параметры конфигурации для модуля runbook в автоматизации Azure и как toochange их с помощью обоих hello портал управления Azure и Windows PowerShell."
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
ms.openlocfilehash: 6f0ef09c148355a351464424c22c33df9300f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-settings"></a><span data-ttu-id="28224-103">Параметры модуля Runbook</span><span class="sxs-lookup"><span data-stu-id="28224-103">Runbook settings</span></span>
<span data-ttu-id="28224-104">Каждый модуль runbook в автоматизации Azure имеется несколько параметров, помочь идентифицировать toobe и toochange его поведение при входе.</span><span class="sxs-lookup"><span data-stu-id="28224-104">Each runbook in Azure Automation has multiple settings that help it toobe identified and toochange its logging behavior.</span></span> <span data-ttu-id="28224-105">Каждый из этих параметров описан ниже следуют процедуры о том, как toomodify их.</span><span class="sxs-lookup"><span data-stu-id="28224-105">Each of these settings is described below followed by procedures on how toomodify them.</span></span>

## <a name="settings"></a><span data-ttu-id="28224-106">данных</span><span class="sxs-lookup"><span data-stu-id="28224-106">Settings</span></span>
### <a name="name-and-description"></a><span data-ttu-id="28224-107">Имя и описание</span><span class="sxs-lookup"><span data-stu-id="28224-107">Name and description</span></span>
<span data-ttu-id="28224-108">Hello имя модуля runbook невозможно изменить после его создания.</span><span class="sxs-lookup"><span data-stu-id="28224-108">You cannot change hello name of a runbook after it has been created.</span></span> <span data-ttu-id="28224-109">Hello описание является необязательным и может быть вверх too512 символов.</span><span class="sxs-lookup"><span data-stu-id="28224-109">hello Description is optional and can be up too512 characters.</span></span>

### <a name="tags"></a><span data-ttu-id="28224-110">Теги</span><span class="sxs-lookup"><span data-stu-id="28224-110">Tags</span></span>
<span data-ttu-id="28224-111">Разрешить теги вы tooassign отдельные слова и фразы toohelp идентификации модуля runbook.</span><span class="sxs-lookup"><span data-stu-id="28224-111">Tags allow you tooassign distinct words and phrases toohelp identify a runbook.</span></span> <span data-ttu-id="28224-112">Например, при отправке runbook toohello [коллекции PowerShell](https://www.powershellgallery.com/), укажите tooidentify теги определенной категории hello runbook должны быть перечислены в.</span><span class="sxs-lookup"><span data-stu-id="28224-112">For example, when you submit a runbook toohello [PowerShell Gallery](https://www.powershellgallery.com/), you specify particular tags tooidentify which categories hello runbook should be listed in.</span></span> <span data-ttu-id="28224-113">Вы можете указать несколько тегов модуля Runbook, разделив их запятой.</span><span class="sxs-lookup"><span data-stu-id="28224-113">You can specify multiple tags for a runbook by separating them with commas.</span></span>

### <a name="logging"></a><span data-ttu-id="28224-114">Ведение журналов</span><span class="sxs-lookup"><span data-stu-id="28224-114">Logging</span></span>
<span data-ttu-id="28224-115">По умолчанию записи Verbose и Progress не записываются toojob журнала.</span><span class="sxs-lookup"><span data-stu-id="28224-115">By default, Verbose and Progress records are not written toojob history.</span></span> <span data-ttu-id="28224-116">Параметры hello для toolog конкретного модуля runbook можно изменить эти записи.</span><span class="sxs-lookup"><span data-stu-id="28224-116">You can change hello settings for a particular runbook toolog these records.</span></span> <span data-ttu-id="28224-117">Дополнительные сведения об этих записях см. в статье [Выходные данные и сообщения Runbook в службе автоматизации Azure](automation-runbook-output-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="28224-117">For more information on these records, see [Runbook Output and Messages](automation-runbook-output-and-messages.md).</span></span>

## <a name="changing-runbook-settings"></a><span data-ttu-id="28224-118">Изменение параметров модуля Runbook</span><span class="sxs-lookup"><span data-stu-id="28224-118">Changing runbook settings</span></span>

### <a name="changing-runbook-settings-with-hello-azure-portal"></a><span data-ttu-id="28224-119">Изменение параметров модуля runbook с hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="28224-119">Changing runbook settings with hello Azure portal</span></span>
<span data-ttu-id="28224-120">Можно изменить параметры модуля Runbook на портал Azure hello из hello **параметры** колонке hello runbook.</span><span class="sxs-lookup"><span data-stu-id="28224-120">You can change settings for a runbook in hello Azure portal from hello **Settings** blade for hello runbook.</span></span>

1. <span data-ttu-id="28224-121">В hello портал Azure, выберите **автоматизации** и нажмите кнопку hello имя учетной записи автоматизации.</span><span class="sxs-lookup"><span data-stu-id="28224-121">In hello Azure portal, select **Automation** and then then click hello name of an automation account.</span></span>
2. <span data-ttu-id="28224-122">Выберите hello **Runbooks** вкладки.</span><span class="sxs-lookup"><span data-stu-id="28224-122">Select hello **Runbooks** tab.</span></span>
3. <span data-ttu-id="28224-123">Щелкните имя runbook hello и являются направленной toohello колонку параметров для модуля runbook hello.</span><span class="sxs-lookup"><span data-stu-id="28224-123">Click hello name of a runbook and you are directed toohello settings blade for hello runbook.</span></span> <span data-ttu-id="28224-124">Здесь можно указать или изменять теги, hello описание runbook, настройте ведение журнала и параметры трассировки и toohelp средства поддержки устранения проблем доступа к.</span><span class="sxs-lookup"><span data-stu-id="28224-124">From here you can specify or modify tags, hello runbook description, configure logging and tracing settings, and access support tools toohelp you solve problems.</span></span>     

### <a name="changing-runbook-settings-with-windows-powershell"></a><span data-ttu-id="28224-125">Изменение параметров модуля Runbook с помощью Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="28224-125">Changing runbook settings with Windows PowerShell</span></span>
<span data-ttu-id="28224-126">Можно использовать hello [AzureRmAutomationRunbook набор](https://msdn.microsoft.com/library/mt603786.aspx) командлет toochange hello параметров модуля runbook.</span><span class="sxs-lookup"><span data-stu-id="28224-126">You can use hello [Set-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx) cmdlet toochange hello settings for a runbook.</span></span> <span data-ttu-id="28224-127">Если вы хотите toospecify несколько тегов, можно либо добавить массив или одной строки с параметром теги toohello значений с разделителями-запятыми.</span><span class="sxs-lookup"><span data-stu-id="28224-127">If you want toospecify multiple tags, you can either provide an array or a single string with comma delimited values toohello Tags parameter.</span></span> <span data-ttu-id="28224-128">Вы можете получить текущие теги hello с hello [Get AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).</span><span class="sxs-lookup"><span data-stu-id="28224-128">You can get hello current tags with hello [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).</span></span>

<span data-ttu-id="28224-129">Привет, следующие примеры команд показывают, как tooset hello свойств для модуля runbook.</span><span class="sxs-lookup"><span data-stu-id="28224-129">hello following sample commands show how tooset hello properties for a runbook.</span></span> <span data-ttu-id="28224-130">В этом примере добавляется три тега toohello существующие теги и указывает, что подробные записи следует вносить в журнал.</span><span class="sxs-lookup"><span data-stu-id="28224-130">This sample adds three tags toohello existing tags and specifies that verbose records should be logged.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $tags = (Get-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName).Tags
    $tags += "Tag1,Tag2,Tag3"
    Set-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName –LogVerbose $true –Tags $tags

## <a name="next-steps"></a><span data-ttu-id="28224-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="28224-131">Next steps</span></span>
* <span data-ttu-id="28224-132">toolearn toocreate и получение выходных данных и сообщения об ошибках из модулей Runbook, в статье [Runbook Output and Messages](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="28224-132">toolearn how toocreate and retrieve output and error messages from runbooks, see [Runbook Output and Messages](automation-runbook-output-and-messages.md)</span></span> 
* <span data-ttu-id="28224-133">toounderstand tooadd runbook, который уже разрабатывался hello сообщества или другой источник или toocreate собственные runbook. в статье [Создание или импорт модуля Runbook](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="28224-133">toounderstand how tooadd a runbook that was already developed by hello community or other source, or toocreate your own runbook see [Creating or Importing a Runbook](automation-creating-importing-runbook.md)</span></span> 

