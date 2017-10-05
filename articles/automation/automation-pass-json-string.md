---
title: "Передача объекта JSON в модуль runbook службы автоматизации Azure | Документация Майкрософт"
description: "Как передать параметры в runbook в виде объекта JSON"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: "powershell, runbook, json, служба автоматизации azure"
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 06/15/2017
ms.author: eslesar
ms.openlocfilehash: eac0e95a46731b9d396ea0590e629d61ca6a7d70
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="pass-a-json-object-to-an-azure-automation-runbook"></a><span data-ttu-id="98c78-104">Передача объекта JSON в модуль runbook службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="98c78-104">Pass a JSON object to an Azure Automation runbook</span></span>

<span data-ttu-id="98c78-105">Иногда может быть полезным хранить данные, которые необходимо передать в модуль runbook, в файле JSON.</span><span class="sxs-lookup"><span data-stu-id="98c78-105">It can be useful to store data that you want to pass to a runbook in a JSON file.</span></span>
<span data-ttu-id="98c78-106">Например, можно создать файл JSON, который содержит все параметры, которые необходимо передать в модуль runbook.</span><span class="sxs-lookup"><span data-stu-id="98c78-106">For example, you might create a JSON file that contains all of the parameters you want to pass to a runbook.</span></span>
<span data-ttu-id="98c78-107">Чтобы сделать это, необходимо преобразовать файл JSON в строку, а затем преобразовать строку в объект PowerShell перед передачей содержимого файла в модуль runbook.</span><span class="sxs-lookup"><span data-stu-id="98c78-107">To do this, you have to convert the JSON to a string and then convert the string to a PowerShell object before passing its contents to the runbook.</span></span>

<span data-ttu-id="98c78-108">В этом примере мы создадим сценарий PowerShell, который вызывает [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) для запуска модуля runbook PowerShell, передавая содержимое файла JSON в runbook.</span><span class="sxs-lookup"><span data-stu-id="98c78-108">In this example, we'll create a PowerShell script that calls [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) to start a PowerShell runbook, passing the contents of the JSON to the runbook.</span></span>
<span data-ttu-id="98c78-109">Модуль runbook PowerShell запускает виртуальную машину Azure, получая параметры для нее из переданного файла JSON.</span><span class="sxs-lookup"><span data-stu-id="98c78-109">The PowerShell runbook starts an Azure VM, getting the parameters for the VM from the JSON that was passed in.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98c78-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="98c78-110">Prerequisites</span></span>
<span data-ttu-id="98c78-111">Для работы с этим учебником требуется:</span><span class="sxs-lookup"><span data-stu-id="98c78-111">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="98c78-112">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="98c78-112">Azure subscription.</span></span> <span data-ttu-id="98c78-113">Если у вас ее нет, [активируйте преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) или <a href="/pricing/free-account/" target="_blank">[зарегистрируйте бесплатную учетную запись](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="98c78-113">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or <a href="/pricing/free-account/" target="_blank">[sign up for a free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="98c78-114">[Учетная запись службы автоматизации](automation-sec-configure-azure-runas-account.md) , чтобы хранить модуль Runbook и выполнять проверку подлинности ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="98c78-114">[Automation account](automation-sec-configure-azure-runas-account.md) to hold the runbook and authenticate to Azure resources.</span></span>  <span data-ttu-id="98c78-115">Эта учетная запись должна иметь разрешение на запуск и остановку виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="98c78-115">This account must have permission to start and stop the virtual machine.</span></span>
* <span data-ttu-id="98c78-116">Виртуальная машина Azure.</span><span class="sxs-lookup"><span data-stu-id="98c78-116">An Azure virtual machine.</span></span> <span data-ttu-id="98c78-117">Это не должна быть рабочая виртуальная машина, так как в процессе изучения этого руководства ее нужно будет остановить и запустить заново.</span><span class="sxs-lookup"><span data-stu-id="98c78-117">We stop and start this machine so it should not be a production VM.</span></span>
* <span data-ttu-id="98c78-118">Azure PowerShell, установленный на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="98c78-118">Azure Powershell installed on a local machine.</span></span> <span data-ttu-id="98c78-119">Дополнительные сведения о получении Azure PowerShell см. в статье [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) (Установка и настройка Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="98c78-119">See [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) for information about how to get Azure PowerShell.</span></span>

## <a name="create-the-json-file"></a><span data-ttu-id="98c78-120">Создание файла JSON</span><span class="sxs-lookup"><span data-stu-id="98c78-120">Create the JSON file</span></span>

<span data-ttu-id="98c78-121">Введите следующий текст в текстовый файл и сохраните его как `test.json` в любом месте на своем локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="98c78-121">Type the following test in a text file, and save it as `test.json` somewhere on your local computer.</span></span>

```json
{
   "VmName" : "TestVM",
   "ResourceGroup" : "AzureAutomationTest"
}
```

## <a name="create-the-runbook"></a><span data-ttu-id="98c78-122">Создание модуля runbook</span><span class="sxs-lookup"><span data-stu-id="98c78-122">Create the runbook</span></span>

<span data-ttu-id="98c78-123">Создайте новый модуль runbook PowerShell с именем Test-Json в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="98c78-123">Create a new PowerShell runbook named "Test-Json" in Azure Automation.</span></span>
<span data-ttu-id="98c78-124">Дополнительные сведения о создании модуля runbook в PowerShell см. в статье [Мой первый модуль Runbook PowerShell](automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="98c78-124">To learn how to create a new PowerShell runbook, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span></span>

<span data-ttu-id="98c78-125">Чтобы принять данные JSON, модуль runbook должен принять объект в качестве входного параметра.</span><span class="sxs-lookup"><span data-stu-id="98c78-125">To accept the JSON data, the runbook must take an object as an input parameter.</span></span>

<span data-ttu-id="98c78-126">Модуль runbook может использовать свойства, определенные в JSON.</span><span class="sxs-lookup"><span data-stu-id="98c78-126">The runbook can then use the properties defined in the JSON.</span></span>

```powershell
Param(
     [parameter(Mandatory=$true)]
     [object]$json
)

# Connect to Azure account   
$Conn = Get-AutomationConnection -Name AzureRunAsConnection
Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint

# Convert object to actual JSON
$json = $json | ConvertFrom-Json

# Use the values from the JSON object as the parameters for your command
Start-AzureRmVM -Name $json.VMName -ResourceGroupName $json.ResourceGroup
 ```

 <span data-ttu-id="98c78-127">Сохраните и опубликуйте этот модуль runbook в учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="98c78-127">Save and publish this runbook in your Automation account.</span></span>

## <a name="call-the-runbook-from-powershell"></a><span data-ttu-id="98c78-128">Вызов модуля runbook из PowerShell</span><span class="sxs-lookup"><span data-stu-id="98c78-128">Call the runbook from PowerShell</span></span>

<span data-ttu-id="98c78-129">Теперь можно вызвать модуль runbook с локального компьютера с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="98c78-129">Now you can call the runbook from your local machine by using Azure PowerShell.</span></span>
<span data-ttu-id="98c78-130">Выполните следующие команды PowerShell:</span><span class="sxs-lookup"><span data-stu-id="98c78-130">Run the following PowerShell commands:</span></span>

1. <span data-ttu-id="98c78-131">Войдите в Azure:</span><span class="sxs-lookup"><span data-stu-id="98c78-131">Log in to Azure:</span></span>
   ```powershell
   Login-AzureRmAccount
   ```
    <span data-ttu-id="98c78-132">Вам будет предложено ввести учетные данные Azure.</span><span class="sxs-lookup"><span data-stu-id="98c78-132">You are prompted to enter your Azure credentials.</span></span>
1. <span data-ttu-id="98c78-133">Получите содержимое файла JSON и преобразуйте его в строку:</span><span class="sxs-lookup"><span data-stu-id="98c78-133">Get the contents of the JSON file and convert it to a string:</span></span>
    ```powershell
    $json =  (Get-content -path 'JsonPath\test.json' -Raw) | Out-string
    ```
    <span data-ttu-id="98c78-134">`JsonPath` — это путь, по которому был сохранен файл JSON.</span><span class="sxs-lookup"><span data-stu-id="98c78-134">`JsonPath` is the path where you saved the JSON file.</span></span>
1. <span data-ttu-id="98c78-135">Преобразуйте содержимое строки `$json` в объект PowerShell:</span><span class="sxs-lookup"><span data-stu-id="98c78-135">Convert the string contents of `$json` to a PowerShell object:</span></span>
   ```powershell
   $JsonParams = @{"json"=$json}
   ```
1. <span data-ttu-id="98c78-136">Создайте хэш-таблицу для параметров команды `Start-AzureRmAutomstionRunbook`:</span><span class="sxs-lookup"><span data-stu-id="98c78-136">Create a hashtable for the parameters for `Start-AzureRmAutomstionRunbook`:</span></span>
   ```powershell
   $RBParams = @{
        AutomationAccountName = 'AATest'
        ResourceGroupName = 'RGTest'
        Name = 'Test-Json'
        Parameters = $JsonParams
   }
   ```
   <span data-ttu-id="98c78-137">Обратите внимание, что вы задаете значение `Parameters` объекту PowerShell, который содержит значения из файла JSON.</span><span class="sxs-lookup"><span data-stu-id="98c78-137">Notice that you are setting the value of `Parameters` to the PowerShell object that contains the values from the JSON file.</span></span> 
1. <span data-ttu-id="98c78-138">Запуск модуля runbook</span><span class="sxs-lookup"><span data-stu-id="98c78-138">Start the runbook</span></span>
   ```powershell
   $job = Start-AzureRmAutomationRunbook @RBParams
   ```

<span data-ttu-id="98c78-139">Модуль runbook использует значения из файла JSON для запуска виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="98c78-139">The runbook uses the values from the JSON file to start a VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98c78-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="98c78-140">Next steps</span></span>

* <span data-ttu-id="98c78-141">Дополнительные сведения о редактировании модулей Runbook PowerShell и рабочих процессов PowerShell с помощью текстового редактора см. в статье [Изменение текстовых модулей Runbook в службе автоматизации Azure](automation-edit-textual-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="98c78-141">To learn more about editing PowerShell and PowerShell Workflow runbooks with a textual editor, see [Editing textual runbooks in Azure Automation](automation-edit-textual-runbook.md)</span></span> 
* <span data-ttu-id="98c78-142">Дополнительные сведения о создании и импорте модулей runbook см. в статье [Создание или импорт модуля Runbook в службе автоматизации Azure](automation-creating-importing-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="98c78-142">To learn more about creating and importing runbooks, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md)</span></span>


