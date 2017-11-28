---
title: "Ресурсы-контейнеры переменных в службе автоматизации Azure | Документация Майкрософт"
description: "Ресурсы-контейнеры переменных — это значения, которые доступны для всех модулей Runbook и конфигураций DSC в службе автоматизации Azure.  В статье подробно рассматриваются переменные и работа с ними как в текстовых, так и в графических модулях."
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
ms.openlocfilehash: dc00e1e5fa8df5cb55e7e2672137d1df44133773
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="variable-assets-in-azure-automation"></a><span data-ttu-id="5fc70-104">Средства переменных в службе автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="5fc70-104">Variable assets in Azure Automation</span></span>

<span data-ttu-id="5fc70-105">Ресурсы-контейнеры переменных — это значения, которые доступны для всех модулей Runbook и конфигураций DSC в учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="5fc70-105">Variable assets are values that are available to all runbooks and DSC configurations in your automation account.</span></span> <span data-ttu-id="5fc70-106">Средства можно создавать, изменять или получать с помощью портала Azure, Windows PowerShell, из модуля Runbook или конфигурации DSC.</span><span class="sxs-lookup"><span data-stu-id="5fc70-106">They can be created, modified, and retrieved from the Azure portal, Windows PowerShell, and from within a runbook or DSC configuration.</span></span> <span data-ttu-id="5fc70-107">Переменные автоматизации полезны в следующих случаях:</span><span class="sxs-lookup"><span data-stu-id="5fc70-107">Automation variables are useful for the following scenarios:</span></span>

- <span data-ttu-id="5fc70-108">совместное использование значения несколькими модулями Runbook или конфигурациями DSC;</span><span class="sxs-lookup"><span data-stu-id="5fc70-108">Share a value between multiple runbooks or DSC configurations.</span></span>

- <span data-ttu-id="5fc70-109">совместное использование значения несколькими заданиями из одного модуля Runbook или конфигурации DSC;</span><span class="sxs-lookup"><span data-stu-id="5fc70-109">Share a value between multiple jobs from the same runbook or DSC configuration.</span></span>

- <span data-ttu-id="5fc70-110">управление значением из портала или из командной строки Windows PowerShell, используемой модулями Runbook или конфигурациями DSC; это может быть набор типичных элементов конфигурации, такой как список имен виртуальных машин, определенная группа ресурсов, доменное имя AD и т. д.</span><span class="sxs-lookup"><span data-stu-id="5fc70-110">Manage a value from the portal or from the Windows PowerShell command line that is used by runbooks or DSC configurations, such as a set of common configuration items like specific list of VM names, a specific resource group,  an AD domain name, etc.</span></span>  

<span data-ttu-id="5fc70-111">Переменные службы автоматизации сохраняются, чтобы они были доступными после сбоя модуля Runbook или конфигурации DSC.</span><span class="sxs-lookup"><span data-stu-id="5fc70-111">Automation variables are persisted so that they continue to be available even if the runbook or DSC configuration fails.</span></span>  <span data-ttu-id="5fc70-112">Это также позволяет модулю Runbook задать значение, которое может быть использовано другим модулем или этим же модулем либо конфигурацией DSC при следующем запуске.</span><span class="sxs-lookup"><span data-stu-id="5fc70-112">This also allows a value to be set by one runbook that is then used by another, or is used by the same runbook or DSC configuration the next time that it is run.</span></span>

<span data-ttu-id="5fc70-113">При создании переменной можно указать, что она должна храниться в зашифрованном виде.</span><span class="sxs-lookup"><span data-stu-id="5fc70-113">When a variable is created, you can specify that it be stored encrypted.</span></span>  <span data-ttu-id="5fc70-114">Если переменная зашифрована, она безопасно хранится в службе автоматизации Azure и ее значение не может быть получено с помощью командлета [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx), который входит в модуль Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5fc70-114">When a variable is encrypted, it is stored securely in Azure Automation, and its value cannot be retrieved from the [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx) cmdlet that ships as part of the Azure PowerShell module.</span></span>  <span data-ttu-id="5fc70-115">Единственный способ получить зашифрованное значение — использовать действие **Get-AutomationVariable** в модуле Runbook или конфигурации DSC.</span><span class="sxs-lookup"><span data-stu-id="5fc70-115">The only way that an encrypted value can be retrieved is from the **Get-AutomationVariable** activity in a runbook or DSC configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="5fc70-116">Безопасные средства в службе автоматизации Azure включают учетные данные, сертификаты, подключения и зашифрованные переменные.</span><span class="sxs-lookup"><span data-stu-id="5fc70-116">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="5fc70-117">Эти ресурсы шифруются и хранятся в службе автоматизации Azure с помощью уникального ключа, который создается для каждой учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="5fc70-117">These assets are encrypted and stored in the Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="5fc70-118">Ключ шифруется главным сертификатом и хранится в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="5fc70-118">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="5fc70-119">Прежде чем сохранять безопасное средство, ключ учетной записи в службе автоматизации дешифруется с помощью главного сертификата и используется для шифрования средства.</span><span class="sxs-lookup"><span data-stu-id="5fc70-119">Before storing a secure asset, the key for the automation account is decrypted using the master certificate and then used to encrypt the asset.</span></span>

## <a name="variable-types"></a><span data-ttu-id="5fc70-120">Типы переменных</span><span class="sxs-lookup"><span data-stu-id="5fc70-120">Variable types</span></span>

<span data-ttu-id="5fc70-121">При создании переменной с помощью портала Azure выберите тип данных из раскрывающегося списка, чтобы портал мог вывести соответствующий элемент управления для ввода значения переменной.</span><span class="sxs-lookup"><span data-stu-id="5fc70-121">When you create a variable with the Azure portal, you must specify a data type from the drop-down list so the portal can display the appropriate control for entering the variable value.</span></span> <span data-ttu-id="5fc70-122">Переменная не ограничивается этим типом данных, однако следует задать значение с помощью Windows PowerShell, если значение должно иметь другой тип.</span><span class="sxs-lookup"><span data-stu-id="5fc70-122">The variable is not restricted to this data type, but you must set the variable using Windows PowerShell if you want to specify a value of a different type.</span></span> <span data-ttu-id="5fc70-123">Если указать **Не задан**, то переменная получит значение **$null**, и значение необходимо указать с помощью командлета [Set-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) или с помощью действия **Set-AutomationVariable**.</span><span class="sxs-lookup"><span data-stu-id="5fc70-123">If you specify **Not defined**, then the value of the variable will be set to **$null**, and you must set the value with the [Set-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) cmdlet or **Set-AutomationVariable** activity.</span></span>  <span data-ttu-id="5fc70-124">Невозможно создать или изменить значение для переменной сложного типа на портале, но можно указать значение любого типа с помощью Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5fc70-124">You cannot create or change the value for a complex variable type in the portal, but you can provide a value of any type using Windows PowerShell.</span></span> <span data-ttu-id="5fc70-125">Сложные типы возвращаются в виде [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).</span><span class="sxs-lookup"><span data-stu-id="5fc70-125">Complex types will be returned as a [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).</span></span>

<span data-ttu-id="5fc70-126">Можно сохранить несколько значений в отдельной переменной, создав массив или хэш-таблицу и сохранив ее в переменную.</span><span class="sxs-lookup"><span data-stu-id="5fc70-126">You can store multiple values to a single variable by creating an array or hashtable and saving it to the variable.</span></span>

<span data-ttu-id="5fc70-127">Ниже перечислены типы переменных, которые доступны в службе автоматизации.</span><span class="sxs-lookup"><span data-stu-id="5fc70-127">The following are a list of variable types available in Automation:</span></span>

* <span data-ttu-id="5fc70-128">Строка</span><span class="sxs-lookup"><span data-stu-id="5fc70-128">String</span></span>
* <span data-ttu-id="5fc70-129">Целое число </span><span class="sxs-lookup"><span data-stu-id="5fc70-129">Integer</span></span>
* <span data-ttu-id="5fc70-130">DateTime</span><span class="sxs-lookup"><span data-stu-id="5fc70-130">DateTime</span></span>
* <span data-ttu-id="5fc70-131">Логический</span><span class="sxs-lookup"><span data-stu-id="5fc70-131">Boolean</span></span>
* <span data-ttu-id="5fc70-132">Null</span><span class="sxs-lookup"><span data-stu-id="5fc70-132">Null</span></span>

## <a name="cmdlets-and-workflow-activities"></a><span data-ttu-id="5fc70-133">Командлеты и рабочие процессы</span><span class="sxs-lookup"><span data-stu-id="5fc70-133">Cmdlets and workflow activities</span></span>

<span data-ttu-id="5fc70-134">Командлеты, представленные в следующей таблице, используются для создания переменных и управления ими с помощью Windows PowerShell в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="5fc70-134">The cmdlets in the following table are used to create and manage Automation variables with Windows PowerShell.</span></span> <span data-ttu-id="5fc70-135">Они входят в состав [модуля Azure PowerShell](../powershell-install-configure.md) , доступного в модулях Runbook и конфигурации DSC службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="5fc70-135">They ship as part of the [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configuration.</span></span>

|<span data-ttu-id="5fc70-136">Командлеты</span><span class="sxs-lookup"><span data-stu-id="5fc70-136">Cmdlets</span></span>|<span data-ttu-id="5fc70-137">Описание</span><span class="sxs-lookup"><span data-stu-id="5fc70-137">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="5fc70-138">Get-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="5fc70-138">Get-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603849.aspx)|<span data-ttu-id="5fc70-139">Получает значение существующей переменной.</span><span class="sxs-lookup"><span data-stu-id="5fc70-139">Retrieves the value of an existing variable.</span></span>|
|[<span data-ttu-id="5fc70-140">New-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="5fc70-140">New-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603613.aspx)|<span data-ttu-id="5fc70-141">Создает новую переменную и устанавливает ее значение.</span><span class="sxs-lookup"><span data-stu-id="5fc70-141">Creates a new variable and sets its value.</span></span>|
|[<span data-ttu-id="5fc70-142">Remove-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="5fc70-142">Remove-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt619354.aspx)|<span data-ttu-id="5fc70-143">Удаляет существующую переменную.</span><span class="sxs-lookup"><span data-stu-id="5fc70-143">Removes an existing variable.</span></span>|
|[<span data-ttu-id="5fc70-144">Set-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="5fc70-144">Set-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603601.aspx)|<span data-ttu-id="5fc70-145">Получает значение существующей переменной.</span><span class="sxs-lookup"><span data-stu-id="5fc70-145">Sets the value for an existing variable.</span></span>|

<span data-ttu-id="5fc70-146">Действия рабочего процесса в следующей таблице используются для доступа к переменным автоматизации в модуле Runbook.</span><span class="sxs-lookup"><span data-stu-id="5fc70-146">The workflow activities in the following table are used to access Automation variables in a runbook.</span></span> <span data-ttu-id="5fc70-147">Они доступны для использования в модуле Runbook или конфигурации DSC и не поставляются вместе с модулем Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5fc70-147">They are only available for use in a runbook or DSC configuration, and do not ship as part of the Azure PowerShell module.</span></span>

|<span data-ttu-id="5fc70-148">Действия рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="5fc70-148">Workflow Activities</span></span>|<span data-ttu-id="5fc70-149">Описание</span><span class="sxs-lookup"><span data-stu-id="5fc70-149">Description</span></span>|
|:---|:---|
|<span data-ttu-id="5fc70-150">Get-AutomationVariable</span><span class="sxs-lookup"><span data-stu-id="5fc70-150">Get-AutomationVariable</span></span>|<span data-ttu-id="5fc70-151">Получает значение существующей переменной.</span><span class="sxs-lookup"><span data-stu-id="5fc70-151">Retrieves the value of an existing variable.</span></span>|
|<span data-ttu-id="5fc70-152">Set-AutomationVariable</span><span class="sxs-lookup"><span data-stu-id="5fc70-152">Set-AutomationVariable</span></span>|<span data-ttu-id="5fc70-153">Получает значение существующей переменной.</span><span class="sxs-lookup"><span data-stu-id="5fc70-153">Sets the value for an existing variable.</span></span>|

> [!NOTE] 
> <span data-ttu-id="5fc70-154">Не следует использовать переменные в параметре –Name действия **Get-AutomationVariable** в модуле Runbook или конфигурации DSC, поскольку это усложняет определение зависимостей между модулями Runbook или конфигурацией DSC и переменными службы автоматизации во время разработки.</span><span class="sxs-lookup"><span data-stu-id="5fc70-154">You should avoid using variables in the –Name parameter of **Get-AutomationVariable**  in a runbook or DSC configuration since this can complicate discovering dependencies between runbooks or DSC configuration, and Automation variables at design time.</span></span>

## <a name="creating-a-new-automation-variable"></a><span data-ttu-id="5fc70-155">Создание новой переменной автоматизации</span><span class="sxs-lookup"><span data-stu-id="5fc70-155">Creating a new Automation variable</span></span>

### <a name="to-create-a-new-variable-with-the-azure-portal"></a><span data-ttu-id="5fc70-156">Создание новой переменной на портале Azure</span><span class="sxs-lookup"><span data-stu-id="5fc70-156">To create a new variable with the Azure portal</span></span>

1. <span data-ttu-id="5fc70-157">В учетной записи службы автоматизации щелкните плитку **Ресурсы**, а затем в колонке **Ресурсы** выберите **Переменные**.</span><span class="sxs-lookup"><span data-stu-id="5fc70-157">From your Automation account, click the **Assets** tile and then on the **Assets** blade, select **Variables**.</span></span>
2. <span data-ttu-id="5fc70-158">На плитке **Переменные** выберите **Добавить переменную**.</span><span class="sxs-lookup"><span data-stu-id="5fc70-158">On the **Variables** tile, select **Add a variable**.</span></span>
3. <span data-ttu-id="5fc70-159">Укажите параметры в колонке **Новая переменная** и нажмите кнопку **Создать**, чтобы сохранить новую переменную.</span><span class="sxs-lookup"><span data-stu-id="5fc70-159">Complete the options on the **New Variable** blade and click **Create** save the new variable.</span></span>

### <a name="to-create-a-new-variable-with-windows-powershell"></a><span data-ttu-id="5fc70-160">Создание переменной с помощью Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="5fc70-160">To create a new variable with Windows PowerShell</span></span>

<span data-ttu-id="5fc70-161">Командлет [New-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) создает переменную и задает ее исходное значение.</span><span class="sxs-lookup"><span data-stu-id="5fc70-161">The [New-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) cmdlet creates a new variable and sets its initial value.</span></span> <span data-ttu-id="5fc70-162">Значение можно получить с помощью [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx).</span><span class="sxs-lookup"><span data-stu-id="5fc70-162">You can retrieve the value using [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx).</span></span> <span data-ttu-id="5fc70-163">Если значение простого типа, возвращается тот же тип.</span><span class="sxs-lookup"><span data-stu-id="5fc70-163">If the value is a simple type, then that same type is returned.</span></span> <span data-ttu-id="5fc70-164">Если это сложный тип, возвращается **PSCustomObject** .</span><span class="sxs-lookup"><span data-stu-id="5fc70-164">If it’s a complex type, then a **PSCustomObject** is returned.</span></span>

<span data-ttu-id="5fc70-165">Приведенные ниже примеры команд демонстрируют создание переменной строкового типа и возврат ее значения.</span><span class="sxs-lookup"><span data-stu-id="5fc70-165">The following sample commands show how to create a variable of type string and then return its value.</span></span>

    New-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" 
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable' `
    –Encrypted $false –Value 'My String'
    $string = (Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable').Value

<span data-ttu-id="5fc70-166">Приведенные ниже примеры команд демонстрируют создание переменной сложного типа и возврат ее свойств.</span><span class="sxs-lookup"><span data-stu-id="5fc70-166">The following sample commands show how to create a variable with a complex type and then return its properties.</span></span> <span data-ttu-id="5fc70-167">В данном случае используется объект виртуальной машины из **Get-AzureRmVm**.</span><span class="sxs-lookup"><span data-stu-id="5fc70-167">In this case, a virtual machine object from **Get-AzureRmVm** is used.</span></span>

    $vm = Get-AzureRmVm -ResourceGroupName "ResourceGroup01" –Name "VM01"
    New-AzureRmAutomationVariable –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable" –Encrypted $false –Value $vm
    
    $vmValue = (Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable").Value
    $vmName = $vmValue.Name
    $vmIpAddress = $vmValue.IpAddress



## <a name="using-a-variable-in-a-runbook-or-dsc-configuration"></a><span data-ttu-id="5fc70-168">Использование переменной в модуле Runbook или конфигурации DSC</span><span class="sxs-lookup"><span data-stu-id="5fc70-168">Using a variable in a runbook or DSC configuration</span></span>

<span data-ttu-id="5fc70-169">Используйте действие **Set-AutomationVariable**, чтобы задать значение переменной службы автоматизации в модуле Runbook, и действие **Get-AutomationVariable**, чтобы получить его.</span><span class="sxs-lookup"><span data-stu-id="5fc70-169">Use the **Set-AutomationVariable** activity to set the value of an Automation variable in a runbook or DSC configuration, and the **Get-AutomationVariable** to retrieve it.</span></span>  <span data-ttu-id="5fc70-170">Не следует использовать командлеты **Set-AzureAutomationVariable** и **Get-AzureAutomationVariable** в модуле Runbook или конфигурации DSC, поскольку они менее эффективны, чем действия рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="5fc70-170">You shouldn't use the **Set-AzureAutomationVariable** or  **Get-AzureAutomationVariable** cmdlets in a runbook or DSC configuration since they are less efficient than the workflow activities.</span></span>  <span data-ttu-id="5fc70-171">Также с помощью **Get-AzureAutomationVariable**нельзя получить значение безопасных переменных.</span><span class="sxs-lookup"><span data-stu-id="5fc70-171">You also cannot retrieve the value of secure variables with **Get-AzureAutomationVariable**.</span></span>  <span data-ttu-id="5fc70-172">Единственный способ создать переменную из модуля Runbook или конфигурации DSC — использовать командлет [New-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx).</span><span class="sxs-lookup"><span data-stu-id="5fc70-172">The only way to create a new variable from within a runbook or DSC configuration is to use the [New-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx)  cmdlet.</span></span>


### <a name="textual-runbook-samples"></a><span data-ttu-id="5fc70-173">Текстовые примеры модуля Runbook</span><span class="sxs-lookup"><span data-stu-id="5fc70-173">Textual runbook samples</span></span>

#### <a name="setting-and-retrieving-a-simple-value-from-a-variable"></a><span data-ttu-id="5fc70-174">Установка и получение простого значения из переменной</span><span class="sxs-lookup"><span data-stu-id="5fc70-174">Setting and retrieving a simple value from a variable</span></span>

<span data-ttu-id="5fc70-175">Приведенные ниже примеры команд демонстрируют задание и получение переменной в текстовом модуле Runbook.</span><span class="sxs-lookup"><span data-stu-id="5fc70-175">The following sample commands show how to set and retrieve a variable in a textual runbook.</span></span> <span data-ttu-id="5fc70-176">В примере предполагается, что целочисленные переменные *NumberOfIterations* и *NumberOfRunnings* и строковая переменная *SampleMessage* уже созданы.</span><span class="sxs-lookup"><span data-stu-id="5fc70-176">In this sample, it is assumed that variables of type integer named *NumberOfIterations* and *NumberOfRunnings* and a variable of type string named *SampleMessage* have already been created.</span></span>

    $NumberOfIterations = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfIterations'
    $NumberOfRunnings = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfRunnings'
    $SampleMessage = Get-AutomationVariable -Name 'SampleMessage'
    
    Write-Output "Runbook has been run $NumberOfRunnings times."
    
    for ($i = 1; $i -le $NumberOfIterations; $i++) {
       Write-Output "$i`: $SampleMessage"
    }
    Set-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" –Name NumberOfRunnings –Value ($NumberOfRunnings += 1)

#### <a name="setting-and-retrieving-a-complex-object-in-a-variable"></a><span data-ttu-id="5fc70-177">Задание и получение сложного объекта в переменной</span><span class="sxs-lookup"><span data-stu-id="5fc70-177">Setting and retrieving a complex object in a variable</span></span>

<span data-ttu-id="5fc70-178">В следующем примере кода показано, как добавить в переменную сложное значение в текстовом модуле Runbook.</span><span class="sxs-lookup"><span data-stu-id="5fc70-178">The following sample code shows how to update a variable with a complex value in a textual runbook.</span></span> <span data-ttu-id="5fc70-179">В этом примере виртуальная машина Azure вызывается с помощью команды **Get-AzureVM** и сохраняется в существующую переменную автоматизации.</span><span class="sxs-lookup"><span data-stu-id="5fc70-179">In this sample, an Azure virtual machine is retrieved with **Get-AzureVM** and saved to an existing Automation variable.</span></span>  <span data-ttu-id="5fc70-180">Как указано в разделе [Типы переменных](#variable-types), значение сохраняется в виде PSCustomObject.</span><span class="sxs-lookup"><span data-stu-id="5fc70-180">As explained in [Variable types](#variable-types), this is stored as a PSCustomObject.</span></span>

    $vm = Get-AzureVM -ServiceName "MyVM" -Name "MyVM"
    Set-AutomationVariable -Name "MyComplexVariable" -Value $vm


<span data-ttu-id="5fc70-181">В следующем коде значение возвращается из переменной и используется для запуска виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="5fc70-181">In the following code, the value is retrieved from the variable and used to start the virtual machine.</span></span>

    $vmObject = Get-AutomationVariable -Name "MyComplexVariable"
    if ($vmObject.PowerState -eq 'Stopped') {
       Start-AzureVM -ServiceName $vmObject.ServiceName -Name $vmObject.Name
    }


#### <a name="setting-and-retrieving-a-collection-in-a-variable"></a><span data-ttu-id="5fc70-182">Задание и получение коллекции в переменной</span><span class="sxs-lookup"><span data-stu-id="5fc70-182">Setting and retrieving a collection in a variable</span></span>

<span data-ttu-id="5fc70-183">В следующем примере кода показано, как использовать переменную с набором сложных значений в текстовом модуле Runbook.</span><span class="sxs-lookup"><span data-stu-id="5fc70-183">The following sample code shows how to use a variable with a collection of complex values in a textual runbook.</span></span> <span data-ttu-id="5fc70-184">В этом примере имена нескольких виртуальных машин Azure возвращаются с помощью команды **Get-AzureVM** и затем сохраняются в существующую переменную автоматизации.</span><span class="sxs-lookup"><span data-stu-id="5fc70-184">In this sample, multiple Azure virtual machines are retrieved with **Get-AzureVM** and saved to an existing Automation variable.</span></span>  <span data-ttu-id="5fc70-185">Как указано в разделе [Типы переменных](#variable-types), значение сохраняется в виде коллекции PSCustomObject.</span><span class="sxs-lookup"><span data-stu-id="5fc70-185">As explained in [Variable types](#variable-types), this is stored as a collection of PSCustomObjects.</span></span>

    $vms = Get-AzureVM | Where -FilterScript {$_.Name -match "my"}     
    Set-AutomationVariable -Name 'MyComplexVariable' -Value $vms

<span data-ttu-id="5fc70-186">В следующем коде коллекция значений возвращается из переменной и используется для запуска виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="5fc70-186">In the following code, the collection is retrieved from the variable and used to start each virtual machine.</span></span>

    $vmValues = Get-AutomationVariable -Name "MyComplexVariable"
    ForEach ($vmValue in $vmValues)
    {
       if ($vmValue.PowerState -eq 'Stopped') {
          Start-AzureVM -ServiceName $vmValue.ServiceName -Name $vmValue.Name
       }
    }


### <a name="graphical-runbook-samples"></a><span data-ttu-id="5fc70-187">Графические примеры для модуля Runbook</span><span class="sxs-lookup"><span data-stu-id="5fc70-187">Graphical runbook samples</span></span>

<span data-ttu-id="5fc70-188">Чтобы добавить команды **Get-AutomationVariable** и **Set-AutomationVariable** в графическом модуле Runbook, щелкните правой кнопкой мыши переменную в области библиотеки графического редактора и выберите необходимый процесс.</span><span class="sxs-lookup"><span data-stu-id="5fc70-188">In a graphical runbook, you add the **Get-AutomationVariable** or **Set-AutomationVariable** by right-clicking on the variable in the Library pane of the graphical editor and selecting the activity you want.</span></span>

![Добавление переменной в полотно](media/automation-variables/runbook-variable-add-canvas.png)

#### <a name="setting-values-in-a-variable"></a><span data-ttu-id="5fc70-190">Задание значений в переменной</span><span class="sxs-lookup"><span data-stu-id="5fc70-190">Setting values in a variable</span></span>
<span data-ttu-id="5fc70-191">На следующем рисунке приведен пример добавления в переменную простого значения в графическом модуле Runbook.</span><span class="sxs-lookup"><span data-stu-id="5fc70-191">The following image shows sample activities to update a variable with a simple value in a graphical runbook.</span></span> <span data-ttu-id="5fc70-192">В этом примере имя одной виртуальной машины Azure возвращается с помощью команды **Get-AzureRmVM**, а имя компьютера сохраняется в существующую переменную службы автоматизации строкового типа.</span><span class="sxs-lookup"><span data-stu-id="5fc70-192">In this sample, a single Azure virtual machine is retrieved with **Get-AzureRmVM** and the computer name is saved to an existing Automation variable with a type of String.</span></span>  <span data-ttu-id="5fc70-193">Не имеет значения, [является ли ссылка конвейером или последовательностью](automation-graphical-authoring-intro.md#links-and-workflow) , так как ожидается только одно значение в выводе.</span><span class="sxs-lookup"><span data-stu-id="5fc70-193">It doesn't matter whether the [link is a pipeline or sequence](automation-graphical-authoring-intro.md#links-and-workflow) since we only expect a single object in the output.</span></span>

![Задание простой переменной](media/automation-variables/runbook-set-simple-variable.png)

## <a name="next-steps"></a><span data-ttu-id="5fc70-195">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5fc70-195">Next Steps</span></span>

* <span data-ttu-id="5fc70-196">Дополнительные сведения о соединении действий в графической разработке см. в разделе [Использование связей при создании графических модулей](automation-graphical-authoring-intro.md#links-and-workflow).</span><span class="sxs-lookup"><span data-stu-id="5fc70-196">To learn more about connecting activities together in graphical authoring, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow)</span></span>
* <span data-ttu-id="5fc70-197">Чтобы начать работу с графическими модулями Runbook, см. инструкции в статье [Первый графический Runbook](automation-first-runbook-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="5fc70-197">To get started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span> 

