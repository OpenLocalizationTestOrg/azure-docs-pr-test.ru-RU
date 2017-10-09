---
title: "aaaVariable средств автоматизации Azure | Документы Microsoft"
description: "Ресурсы переменных представлены значения, доступные tooall Runbook и конфигураций DSC в службе автоматизации Azure.  В этой статье подробно описывается hello переменных и как toowork с ними в текстовых и графических разработки."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: b880c15f-46f5-4881-8e98-e034cc5a66ec
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/09/2017
ms.author: magoedte;bwren
ms.openlocfilehash: f9daa49fc1dc883ffb218a9adf26e36df1d6bb27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="variable-assets-in-azure-automation"></a><span data-ttu-id="62f53-104">Средства переменных в службе автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="62f53-104">Variable assets in Azure Automation</span></span>

<span data-ttu-id="62f53-105">Ресурсы переменных представлены значения, доступные tooall Runbook и конфигураций DSC в вашей учетной записи автоматизации.</span><span class="sxs-lookup"><span data-stu-id="62f53-105">Variable assets are values that are available tooall runbooks and DSC configurations in your automation account.</span></span> <span data-ttu-id="62f53-106">Их можно создать, изменить и извлечь из hello портал Azure, Windows PowerShell, а также из runbook или конфигурации DSC.</span><span class="sxs-lookup"><span data-stu-id="62f53-106">They can be created, modified, and retrieved from hello Azure portal, Windows PowerShell, and from within a runbook or DSC configuration.</span></span> <span data-ttu-id="62f53-107">Переменные автоматизации используются для hello следующие сценарии:</span><span class="sxs-lookup"><span data-stu-id="62f53-107">Automation variables are useful for hello following scenarios:</span></span>

- <span data-ttu-id="62f53-108">совместное использование значения несколькими модулями Runbook или конфигурациями DSC;</span><span class="sxs-lookup"><span data-stu-id="62f53-108">Share a value between multiple runbooks or DSC configurations.</span></span>

- <span data-ttu-id="62f53-109">Совместное использование значения несколькими заданиями из hello одного модуля runbook или конфигурации DSC.</span><span class="sxs-lookup"><span data-stu-id="62f53-109">Share a value between multiple jobs from hello same runbook or DSC configuration.</span></span>

- <span data-ttu-id="62f53-110">Управление значением из портала hello или из командной строки Windows PowerShell hello, используемой модулей Runbook или конфигураций DSC, такие как набор общих элементов конфигурации как определенный список имен виртуальных Машин, определенной группы ресурсов, имя домена AD, и т. д.</span><span class="sxs-lookup"><span data-stu-id="62f53-110">Manage a value from hello portal or from hello Windows PowerShell command line that is used by runbooks or DSC configurations, such as a set of common configuration items like specific list of VM names, a specific resource group,  an AD domain name, etc.</span></span>  

<span data-ttu-id="62f53-111">Переменные автоматизации сохраняются так, что они остаются toobe доступен даже при сбое hello runbook или конфигурации DSC.</span><span class="sxs-lookup"><span data-stu-id="62f53-111">Automation variables are persisted so that they continue toobe available even if hello runbook or DSC configuration fails.</span></span>  <span data-ttu-id="62f53-112">Это также позволяет toobe значение, задайте в одном модуле runbook, который затем используется другим или используется hello одного модуля runbook или hello конфигурации DSC очередном запуске.</span><span class="sxs-lookup"><span data-stu-id="62f53-112">This also allows a value toobe set by one runbook that is then used by another, or is used by hello same runbook or DSC configuration hello next time that it is run.</span></span>

<span data-ttu-id="62f53-113">При создании переменной можно указать, что она должна храниться в зашифрованном виде.</span><span class="sxs-lookup"><span data-stu-id="62f53-113">When a variable is created, you can specify that it be stored encrypted.</span></span>  <span data-ttu-id="62f53-114">Если переменная шифруется, она безопасно хранится в службе автоматизации Azure и его значение не удается получить из hello [Get AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx) командлет, который поставляется в составе модуля Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="62f53-114">When a variable is encrypted, it is stored securely in Azure Automation, and its value cannot be retrieved from hello [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx) cmdlet that ships as part of hello Azure PowerShell module.</span></span>  <span data-ttu-id="62f53-115">Hello единственный способ извлечения зашифрованного значения — от hello **Get-AutomationVariable** действие в runbook или конфигурации DSC.</span><span class="sxs-lookup"><span data-stu-id="62f53-115">hello only way that an encrypted value can be retrieved is from hello **Get-AutomationVariable** activity in a runbook or DSC configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="62f53-116">Безопасные средства в службе автоматизации Azure включают учетные данные, сертификаты, подключения и зашифрованные переменные.</span><span class="sxs-lookup"><span data-stu-id="62f53-116">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="62f53-117">Эти ресурсы шифруются и хранятся в hello автоматизации Azure, используя уникальный ключ, который создается для каждой учетной записи автоматизации.</span><span class="sxs-lookup"><span data-stu-id="62f53-117">These assets are encrypted and stored in hello Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="62f53-118">Ключ шифруется главным сертификатом и хранится в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="62f53-118">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="62f53-119">Перед сохранением безопасного ресурса, hello ключ для учетной записи автоматизации hello расшифровывается с помощью шаблона сертификата hello и затем использовать tooencrypt hello активов.</span><span class="sxs-lookup"><span data-stu-id="62f53-119">Before storing a secure asset, hello key for hello automation account is decrypted using hello master certificate and then used tooencrypt hello asset.</span></span>

## <a name="variable-types"></a><span data-ttu-id="62f53-120">Типы переменных</span><span class="sxs-lookup"><span data-stu-id="62f53-120">Variable types</span></span>

<span data-ttu-id="62f53-121">При создании переменной с hello портал Azure, необходимо указать тип данных из раскрывающегося списка hello, hello портале можно было отобразить соответствующий элемент управления для ввода значения переменной hello hello.</span><span class="sxs-lookup"><span data-stu-id="62f53-121">When you create a variable with hello Azure portal, you must specify a data type from hello drop-down list so hello portal can display hello appropriate control for entering hello variable value.</span></span> <span data-ttu-id="62f53-122">переменная Hello не ограниченных toothis данных типа, но необходимо задать переменную hello, с помощью Windows PowerShell, если требуется, чтобы toospecify значение другого типа.</span><span class="sxs-lookup"><span data-stu-id="62f53-122">hello variable is not restricted toothis data type, but you must set hello variable using Windows PowerShell if you want toospecify a value of a different type.</span></span> <span data-ttu-id="62f53-123">При указании **не определен**, а затем hello hello переменной будет иметь значение слишком**$null**, и необходимо задать значение hello с hello [Set-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) командлета или **Set-AutomationVariable** действия.</span><span class="sxs-lookup"><span data-stu-id="62f53-123">If you specify **Not defined**, then hello value of hello variable will be set too**$null**, and you must set hello value with hello [Set-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) cmdlet or **Set-AutomationVariable** activity.</span></span>  <span data-ttu-id="62f53-124">Невозможно создать или изменить hello значение для переменной сложного типа hello портала, но можно указать значение любого типа, с помощью Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="62f53-124">You cannot create or change hello value for a complex variable type in hello portal, but you can provide a value of any type using Windows PowerShell.</span></span> <span data-ttu-id="62f53-125">Сложные типы возвращаются в виде [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).</span><span class="sxs-lookup"><span data-stu-id="62f53-125">Complex types will be returned as a [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).</span></span>

<span data-ttu-id="62f53-126">Можно сохранить несколько значений tooa отдельную переменную, создав массив или хэш-таблицы и сохранить его в переменной toohello.</span><span class="sxs-lookup"><span data-stu-id="62f53-126">You can store multiple values tooa single variable by creating an array or hashtable and saving it toohello variable.</span></span>

<span data-ttu-id="62f53-127">Здесь представлены Hello список типов переменных автоматизации:</span><span class="sxs-lookup"><span data-stu-id="62f53-127">hello following are a list of variable types available in Automation:</span></span>

* <span data-ttu-id="62f53-128">Строка</span><span class="sxs-lookup"><span data-stu-id="62f53-128">String</span></span>
* <span data-ttu-id="62f53-129">Целое число </span><span class="sxs-lookup"><span data-stu-id="62f53-129">Integer</span></span>
* <span data-ttu-id="62f53-130">DateTime</span><span class="sxs-lookup"><span data-stu-id="62f53-130">DateTime</span></span>
* <span data-ttu-id="62f53-131">Логический</span><span class="sxs-lookup"><span data-stu-id="62f53-131">Boolean</span></span>
* <span data-ttu-id="62f53-132">Null</span><span class="sxs-lookup"><span data-stu-id="62f53-132">Null</span></span>

## <a name="cmdlets-and-workflow-activities"></a><span data-ttu-id="62f53-133">Командлеты и рабочие процессы</span><span class="sxs-lookup"><span data-stu-id="62f53-133">Cmdlets and workflow activities</span></span>

<span data-ttu-id="62f53-134">командлеты Hello в следующей таблице hello, используемые toocreate и управления переменными службы автоматизации с помощью Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="62f53-134">hello cmdlets in hello following table are used toocreate and manage Automation variables with Windows PowerShell.</span></span> <span data-ttu-id="62f53-135">Они поставляются как часть hello [модуля Azure PowerShell](../powershell-install-configure.md) доступный для использования в Runbook автоматизации и конфигурации DSC.</span><span class="sxs-lookup"><span data-stu-id="62f53-135">They ship as part of hello [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configuration.</span></span>

|<span data-ttu-id="62f53-136">Командлеты</span><span class="sxs-lookup"><span data-stu-id="62f53-136">Cmdlets</span></span>|<span data-ttu-id="62f53-137">Описание</span><span class="sxs-lookup"><span data-stu-id="62f53-137">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="62f53-138">Get-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="62f53-138">Get-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603849.aspx)|<span data-ttu-id="62f53-139">Извлекает значение hello существующей переменной.</span><span class="sxs-lookup"><span data-stu-id="62f53-139">Retrieves hello value of an existing variable.</span></span>|
|[<span data-ttu-id="62f53-140">New-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="62f53-140">New-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603613.aspx)|<span data-ttu-id="62f53-141">Создает новую переменную и устанавливает ее значение.</span><span class="sxs-lookup"><span data-stu-id="62f53-141">Creates a new variable and sets its value.</span></span>|
|[<span data-ttu-id="62f53-142">Remove-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="62f53-142">Remove-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt619354.aspx)|<span data-ttu-id="62f53-143">Удаляет существующую переменную.</span><span class="sxs-lookup"><span data-stu-id="62f53-143">Removes an existing variable.</span></span>|
|[<span data-ttu-id="62f53-144">Set-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="62f53-144">Set-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603601.aspx)|<span data-ttu-id="62f53-145">Задает значение hello для существующей переменной.</span><span class="sxs-lookup"><span data-stu-id="62f53-145">Sets hello value for an existing variable.</span></span>|

<span data-ttu-id="62f53-146">действия рабочего процесса Hello в следующей таблице hello, используемые tooaccess переменные автоматизации в модуле runbook.</span><span class="sxs-lookup"><span data-stu-id="62f53-146">hello workflow activities in hello following table are used tooaccess Automation variables in a runbook.</span></span> <span data-ttu-id="62f53-147">Они доступны только для использования в конфигурации DSC или runbook и поставляются в составе модуля Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="62f53-147">They are only available for use in a runbook or DSC configuration, and do not ship as part of hello Azure PowerShell module.</span></span>

|<span data-ttu-id="62f53-148">Действия рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="62f53-148">Workflow Activities</span></span>|<span data-ttu-id="62f53-149">Описание</span><span class="sxs-lookup"><span data-stu-id="62f53-149">Description</span></span>|
|:---|:---|
|<span data-ttu-id="62f53-150">Get-AutomationVariable</span><span class="sxs-lookup"><span data-stu-id="62f53-150">Get-AutomationVariable</span></span>|<span data-ttu-id="62f53-151">Извлекает значение hello существующей переменной.</span><span class="sxs-lookup"><span data-stu-id="62f53-151">Retrieves hello value of an existing variable.</span></span>|
|<span data-ttu-id="62f53-152">Set-AutomationVariable</span><span class="sxs-lookup"><span data-stu-id="62f53-152">Set-AutomationVariable</span></span>|<span data-ttu-id="62f53-153">Задает значение hello для существующей переменной.</span><span class="sxs-lookup"><span data-stu-id="62f53-153">Sets hello value for an existing variable.</span></span>|

> [!NOTE] 
> <span data-ttu-id="62f53-154">Следует избегать использования переменных в hello – имя параметра **Get-AutomationVariable** в runbook или конфигурации DSC, поскольку это может усложнить обнаружение зависимостей между модулями Runbook или конфигурации DSC и автоматизации переменные во время разработки.</span><span class="sxs-lookup"><span data-stu-id="62f53-154">You should avoid using variables in hello –Name parameter of **Get-AutomationVariable**  in a runbook or DSC configuration since this can complicate discovering dependencies between runbooks or DSC configuration, and Automation variables at design time.</span></span>

## <a name="creating-a-new-automation-variable"></a><span data-ttu-id="62f53-155">Создание новой переменной автоматизации</span><span class="sxs-lookup"><span data-stu-id="62f53-155">Creating a new Automation variable</span></span>

### <a name="toocreate-a-new-variable-with-hello-azure-portal"></a><span data-ttu-id="62f53-156">toocreate новую переменную с hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="62f53-156">toocreate a new variable with hello Azure portal</span></span>

1. <span data-ttu-id="62f53-157">Из учетной записи автоматизации, нажмите кнопку hello **активы** плитку и затем на hello **активы** колонке выберите **переменных**.</span><span class="sxs-lookup"><span data-stu-id="62f53-157">From your Automation account, click hello **Assets** tile and then on hello **Assets** blade, select **Variables**.</span></span>
2. <span data-ttu-id="62f53-158">На hello **переменных** плитки, выберите **добавить переменную**.</span><span class="sxs-lookup"><span data-stu-id="62f53-158">On hello **Variables** tile, select **Add a variable**.</span></span>
3. <span data-ttu-id="62f53-159">Настройте параметры hello на hello **новой переменной** колонку и нажмите кнопку **создать** сохранить новую переменную hello.</span><span class="sxs-lookup"><span data-stu-id="62f53-159">Complete hello options on hello **New Variable** blade and click **Create** save hello new variable.</span></span>

### <a name="toocreate-a-new-variable-with-windows-powershell"></a><span data-ttu-id="62f53-160">toocreate новую переменную с помощью Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="62f53-160">toocreate a new variable with Windows PowerShell</span></span>

<span data-ttu-id="62f53-161">Hello [New AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) создает новую переменную и задает ее начальное значение.</span><span class="sxs-lookup"><span data-stu-id="62f53-161">hello [New-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) cmdlet creates a new variable and sets its initial value.</span></span> <span data-ttu-id="62f53-162">Можно извлечь при помощи значение hello [Get AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx).</span><span class="sxs-lookup"><span data-stu-id="62f53-162">You can retrieve hello value using [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx).</span></span> <span data-ttu-id="62f53-163">Если hello значение простого типа, то возвращается того же типа.</span><span class="sxs-lookup"><span data-stu-id="62f53-163">If hello value is a simple type, then that same type is returned.</span></span> <span data-ttu-id="62f53-164">Если это сложный тип, возвращается **PSCustomObject** .</span><span class="sxs-lookup"><span data-stu-id="62f53-164">If it’s a complex type, then a **PSCustomObject** is returned.</span></span>

<span data-ttu-id="62f53-165">Hello следующем образце команд Показать как toocreate переменную типа string и возвращать его значение.</span><span class="sxs-lookup"><span data-stu-id="62f53-165">hello following sample commands show how toocreate a variable of type string and then return its value.</span></span>

    New-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" 
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable' `
    –Encrypted $false –Value 'My String'
    $string = (Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable').Value

<span data-ttu-id="62f53-166">Hello следующем образце команд Показать как toocreate переменной с помощью сложного типа, а затем возвращают ее свойства.</span><span class="sxs-lookup"><span data-stu-id="62f53-166">hello following sample commands show how toocreate a variable with a complex type and then return its properties.</span></span> <span data-ttu-id="62f53-167">В данном случае используется объект виртуальной машины из **Get-AzureRmVm**.</span><span class="sxs-lookup"><span data-stu-id="62f53-167">In this case, a virtual machine object from **Get-AzureRmVm** is used.</span></span>

    $vm = Get-AzureRmVm -ResourceGroupName "ResourceGroup01" –Name "VM01"
    New-AzureRmAutomationVariable –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable" –Encrypted $false –Value $vm
    
    $vmValue = (Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable").Value
    $vmName = $vmValue.Name
    $vmIpAddress = $vmValue.IpAddress



## <a name="using-a-variable-in-a-runbook-or-dsc-configuration"></a><span data-ttu-id="62f53-168">Использование переменной в модуле Runbook или конфигурации DSC</span><span class="sxs-lookup"><span data-stu-id="62f53-168">Using a variable in a runbook or DSC configuration</span></span>

<span data-ttu-id="62f53-169">Используйте hello **Set-AutomationVariable** действия tooset hello значение переменной службы автоматизации в runbook или конфигурации DSC и hello **Get-AutomationVariable** tooretrieve его.</span><span class="sxs-lookup"><span data-stu-id="62f53-169">Use hello **Set-AutomationVariable** activity tooset hello value of an Automation variable in a runbook or DSC configuration, and hello **Get-AutomationVariable** tooretrieve it.</span></span>  <span data-ttu-id="62f53-170">Не следует использовать hello **Set-AzureAutomationVariable** или **Get-AzureAutomationVariable** командлетов в runbook или конфигурации DSC, так как они менее эффективным, чем hello действий рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="62f53-170">You shouldn't use hello **Set-AzureAutomationVariable** or  **Get-AzureAutomationVariable** cmdlets in a runbook or DSC configuration since they are less efficient than hello workflow activities.</span></span>  <span data-ttu-id="62f53-171">Также не удается получить значение hello безопасного переменных с **Get-AzureAutomationVariable**.</span><span class="sxs-lookup"><span data-stu-id="62f53-171">You also cannot retrieve hello value of secure variables with **Get-AzureAutomationVariable**.</span></span>  <span data-ttu-id="62f53-172">Здравствуйте только способом toocreate новой переменной из модуля runbook или конфигурации DSC — toouse hello [New-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx) командлета.</span><span class="sxs-lookup"><span data-stu-id="62f53-172">hello only way toocreate a new variable from within a runbook or DSC configuration is toouse hello [New-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx)  cmdlet.</span></span>


### <a name="textual-runbook-samples"></a><span data-ttu-id="62f53-173">Текстовые примеры модуля Runbook</span><span class="sxs-lookup"><span data-stu-id="62f53-173">Textual runbook samples</span></span>

#### <a name="setting-and-retrieving-a-simple-value-from-a-variable"></a><span data-ttu-id="62f53-174">Установка и получение простого значения из переменной</span><span class="sxs-lookup"><span data-stu-id="62f53-174">Setting and retrieving a simple value from a variable</span></span>

<span data-ttu-id="62f53-175">Hello следующем образце команд Показать как tooset и вернуть переменную в текстовой runbook.</span><span class="sxs-lookup"><span data-stu-id="62f53-175">hello following sample commands show how tooset and retrieve a variable in a textual runbook.</span></span> <span data-ttu-id="62f53-176">В примере предполагается, что целочисленные переменные *NumberOfIterations* и *NumberOfRunnings* и строковая переменная *SampleMessage* уже созданы.</span><span class="sxs-lookup"><span data-stu-id="62f53-176">In this sample, it is assumed that variables of type integer named *NumberOfIterations* and *NumberOfRunnings* and a variable of type string named *SampleMessage* have already been created.</span></span>

    $NumberOfIterations = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfIterations'
    $NumberOfRunnings = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfRunnings'
    $SampleMessage = Get-AutomationVariable -Name 'SampleMessage'
    
    Write-Output "Runbook has been run $NumberOfRunnings times."
    
    for ($i = 1; $i -le $NumberOfIterations; $i++) {
       Write-Output "$i`: $SampleMessage"
    }
    Set-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" –Name NumberOfRunnings –Value ($NumberOfRunnings += 1)

#### <a name="setting-and-retrieving-a-complex-object-in-a-variable"></a><span data-ttu-id="62f53-177">Задание и получение сложного объекта в переменной</span><span class="sxs-lookup"><span data-stu-id="62f53-177">Setting and retrieving a complex object in a variable</span></span>

<span data-ttu-id="62f53-178">Hello следующем образце кода показано, как tooupdate переменной с помощью сложного значения в текстовое runbook.</span><span class="sxs-lookup"><span data-stu-id="62f53-178">hello following sample code shows how tooupdate a variable with a complex value in a textual runbook.</span></span> <span data-ttu-id="62f53-179">В этом примере извлекается виртуальная машина Azure с **Get-AzureVM** и сохраненные tooan существующей переменной службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="62f53-179">In this sample, an Azure virtual machine is retrieved with **Get-AzureVM** and saved tooan existing Automation variable.</span></span>  <span data-ttu-id="62f53-180">Как указано в разделе [Типы переменных](#variable-types), значение сохраняется в виде PSCustomObject.</span><span class="sxs-lookup"><span data-stu-id="62f53-180">As explained in [Variable types](#variable-types), this is stored as a PSCustomObject.</span></span>

    $vm = Get-AzureVM -ServiceName "MyVM" -Name "MyVM"
    Set-AutomationVariable -Name "MyComplexVariable" -Value $vm


<span data-ttu-id="62f53-181">В hello после кода hello значение извлекается из hello переменной и используется toostart hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="62f53-181">In hello following code, hello value is retrieved from hello variable and used toostart hello virtual machine.</span></span>

    $vmObject = Get-AutomationVariable -Name "MyComplexVariable"
    if ($vmObject.PowerState -eq 'Stopped') {
       Start-AzureVM -ServiceName $vmObject.ServiceName -Name $vmObject.Name
    }


#### <a name="setting-and-retrieving-a-collection-in-a-variable"></a><span data-ttu-id="62f53-182">Задание и получение коллекции в переменной</span><span class="sxs-lookup"><span data-stu-id="62f53-182">Setting and retrieving a collection in a variable</span></span>

<span data-ttu-id="62f53-183">Hello следующем образце кода показано, как toouse переменную с коллекцией сложных значений в текстовых runbook.</span><span class="sxs-lookup"><span data-stu-id="62f53-183">hello following sample code shows how toouse a variable with a collection of complex values in a textual runbook.</span></span> <span data-ttu-id="62f53-184">В этом образце несколько виртуальных машин Azure, извлекаются с помощью **Get-AzureVM** и сохраненные tooan существующей переменной службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="62f53-184">In this sample, multiple Azure virtual machines are retrieved with **Get-AzureVM** and saved tooan existing Automation variable.</span></span>  <span data-ttu-id="62f53-185">Как указано в разделе [Типы переменных](#variable-types), значение сохраняется в виде коллекции PSCustomObject.</span><span class="sxs-lookup"><span data-stu-id="62f53-185">As explained in [Variable types](#variable-types), this is stored as a collection of PSCustomObjects.</span></span>

    $vms = Get-AzureVM | Where -FilterScript {$_.Name -match "my"}     
    Set-AutomationVariable -Name 'MyComplexVariable' -Value $vms

<span data-ttu-id="62f53-186">В hello после кода hello коллекции извлекается из переменной hello и toostart каждой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="62f53-186">In hello following code, hello collection is retrieved from hello variable and used toostart each virtual machine.</span></span>

    $vmValues = Get-AutomationVariable -Name "MyComplexVariable"
    ForEach ($vmValue in $vmValues)
    {
       if ($vmValue.PowerState -eq 'Stopped') {
          Start-AzureVM -ServiceName $vmValue.ServiceName -Name $vmValue.Name
       }
    }


### <a name="graphical-runbook-samples"></a><span data-ttu-id="62f53-187">Графические примеры для модуля Runbook</span><span class="sxs-lookup"><span data-stu-id="62f53-187">Graphical runbook samples</span></span>

<span data-ttu-id="62f53-188">В графический runbook, добавлении hello **Get-AutomationVariable** или **Set-AutomationVariable** , щелкнув правой кнопкой мыши на переменную hello в области библиотеки hello hello графического редактора и выбрав hello действие.</span><span class="sxs-lookup"><span data-stu-id="62f53-188">In a graphical runbook, you add hello **Get-AutomationVariable** or **Set-AutomationVariable** by right-clicking on hello variable in hello Library pane of hello graphical editor and selecting hello activity you want.</span></span>

![Добавление переменной toocanvas](media/automation-variables/runbook-variable-add-canvas.png)

#### <a name="setting-values-in-a-variable"></a><span data-ttu-id="62f53-190">Задание значений в переменной</span><span class="sxs-lookup"><span data-stu-id="62f53-190">Setting values in a variable</span></span>
<span data-ttu-id="62f53-191">Hello ниже приведен пример действия tooupdate переменную с простым значением в графический runbook.</span><span class="sxs-lookup"><span data-stu-id="62f53-191">hello following image shows sample activities tooupdate a variable with a simple value in a graphical runbook.</span></span> <span data-ttu-id="62f53-192">В этом примере извлекается одной виртуальной машины Azure с **Get AzureRmVM** и имя компьютера hello сохраняется tooan существующей переменной службы автоматизации с типом String.</span><span class="sxs-lookup"><span data-stu-id="62f53-192">In this sample, a single Azure virtual machine is retrieved with **Get-AzureRmVM** and hello computer name is saved tooan existing Automation variable with a type of String.</span></span>  <span data-ttu-id="62f53-193">Неважно, будет ли hello [ссылка относится конвейера или последовательность](automation-graphical-authoring-intro.md#links-and-workflow) так, как только ожидается, что один объект в выходных данных hello.</span><span class="sxs-lookup"><span data-stu-id="62f53-193">It doesn't matter whether hello [link is a pipeline or sequence](automation-graphical-authoring-intro.md#links-and-workflow) since we only expect a single object in hello output.</span></span>

![Задание простой переменной](media/automation-variables/runbook-set-simple-variable.png)

## <a name="next-steps"></a><span data-ttu-id="62f53-195">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="62f53-195">Next Steps</span></span>

* <span data-ttu-id="62f53-196">toolearn Дополнительные сведения о соединении действий вместе в графический разработки, в разделе [ссылки в графический разработки](automation-graphical-authoring-intro.md#links-and-workflow)</span><span class="sxs-lookup"><span data-stu-id="62f53-196">toolearn more about connecting activities together in graphical authoring, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow)</span></span>
* <span data-ttu-id="62f53-197">tooget к работе с графический Runbook в разделе [Мой первый графический runbook](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="62f53-197">tooget started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span> 

