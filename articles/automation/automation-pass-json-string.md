---
title: "aaaPass JSON объект runbook службы автоматизации Azure tooan | Документы Microsoft"
description: "Как toopass параметры tooa runbook как объект JSON"
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
ms.openlocfilehash: 8229a16015d549927ead5496c70e9fb391d35498
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="pass-a-json-object-tooan-azure-automation-runbook"></a><span data-ttu-id="9b948-104">Передайте объект JSON tooan модуля runbook службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="9b948-104">Pass a JSON object tooan Azure Automation runbook</span></span>

<span data-ttu-id="9b948-105">Это может быть полезным toostore данных, что runbook tooa toopass в файле JSON.</span><span class="sxs-lookup"><span data-stu-id="9b948-105">It can be useful toostore data that you want toopass tooa runbook in a JSON file.</span></span>
<span data-ttu-id="9b948-106">Например, можно создать файл JSON, содержащий все параметры hello требуется toopass tooa runbook.</span><span class="sxs-lookup"><span data-stu-id="9b948-106">For example, you might create a JSON file that contains all of hello parameters you want toopass tooa runbook.</span></span>
<span data-ttu-id="9b948-107">toodo, имеют tooconvert hello JSON tooa строку и затем преобразовывать hello строка tooa PowerShell перед передачей его содержимое toohello runbook.</span><span class="sxs-lookup"><span data-stu-id="9b948-107">toodo this, you have tooconvert hello JSON tooa string and then convert hello string tooa PowerShell object before passing its contents toohello runbook.</span></span>

<span data-ttu-id="9b948-108">В этом примере мы создадим сценария PowerShell, который вызывает [начала AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart runbook PowerShell, передавая hello содержимого hello JSON toohello runbook.</span><span class="sxs-lookup"><span data-stu-id="9b948-108">In this example, we'll create a PowerShell script that calls [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart a PowerShell runbook, passing hello contents of hello JSON toohello runbook.</span></span>
<span data-ttu-id="9b948-109">Виртуальной машине Azure, получения параметров hello для hello виртуальной Машины из hello JSON, который был передан в запуске Hello PowerShell runbook.</span><span class="sxs-lookup"><span data-stu-id="9b948-109">hello PowerShell runbook starts an Azure VM, getting hello parameters for hello VM from hello JSON that was passed in.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b948-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9b948-110">Prerequisites</span></span>
<span data-ttu-id="9b948-111">toocomplete этого учебника требуется hello следующие:</span><span class="sxs-lookup"><span data-stu-id="9b948-111">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="9b948-112">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="9b948-112">Azure subscription.</span></span> <span data-ttu-id="9b948-113">Если у вас ее нет, [активируйте преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) или <a href="/pricing/free-account/" target="_blank">[зарегистрируйте бесплатную учетную запись](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="9b948-113">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or <a href="/pricing/free-account/" target="_blank">[sign up for a free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="9b948-114">[Учетная запись службы автоматизации](automation-sec-configure-azure-runas-account.md) toohold hello runbook и проверить подлинность tooAzure ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9b948-114">[Automation account](automation-sec-configure-azure-runas-account.md) toohold hello runbook and authenticate tooAzure resources.</span></span>  <span data-ttu-id="9b948-115">Этой учетной записи необходимо разрешение toostart и остановить виртуальную машину hello.</span><span class="sxs-lookup"><span data-stu-id="9b948-115">This account must have permission toostart and stop hello virtual machine.</span></span>
* <span data-ttu-id="9b948-116">Виртуальная машина Azure.</span><span class="sxs-lookup"><span data-stu-id="9b948-116">An Azure virtual machine.</span></span> <span data-ttu-id="9b948-117">Это не должна быть рабочая виртуальная машина, так как в процессе изучения этого руководства ее нужно будет остановить и запустить заново.</span><span class="sxs-lookup"><span data-stu-id="9b948-117">We stop and start this machine so it should not be a production VM.</span></span>
* <span data-ttu-id="9b948-118">Azure PowerShell, установленный на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="9b948-118">Azure Powershell installed on a local machine.</span></span> <span data-ttu-id="9b948-119">В разделе [Установка и настройка Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) сведения о том, как tooget Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9b948-119">See [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) for information about how tooget Azure PowerShell.</span></span>

## <a name="create-hello-json-file"></a><span data-ttu-id="9b948-120">Создать файл JSON hello</span><span class="sxs-lookup"><span data-stu-id="9b948-120">Create hello JSON file</span></span>

<span data-ttu-id="9b948-121">Введите следующее hello тестирования в текстовый файл и сохраните его как `test.json` где-либо на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="9b948-121">Type hello following test in a text file, and save it as `test.json` somewhere on your local computer.</span></span>

```json
{
   "VmName" : "TestVM",
   "ResourceGroup" : "AzureAutomationTest"
}
```

## <a name="create-hello-runbook"></a><span data-ttu-id="9b948-122">Создание hello runbook</span><span class="sxs-lookup"><span data-stu-id="9b948-122">Create hello runbook</span></span>

<span data-ttu-id="9b948-123">Создайте новый модуль runbook PowerShell с именем Test-Json в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="9b948-123">Create a new PowerShell runbook named "Test-Json" in Azure Automation.</span></span>
<span data-ttu-id="9b948-124">toocreate новый модуль runbook PowerShell в статье toolearn [Мой первый runbook PowerShell](automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="9b948-124">toolearn how toocreate a new PowerShell runbook, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span></span>

<span data-ttu-id="9b948-125">данные JSON tooaccept hello, hello runbook должен получить объект в качестве входного параметра.</span><span class="sxs-lookup"><span data-stu-id="9b948-125">tooaccept hello JSON data, hello runbook must take an object as an input parameter.</span></span>

<span data-ttu-id="9b948-126">Hello runbook можно использовать свойства hello, определенные в hello JSON.</span><span class="sxs-lookup"><span data-stu-id="9b948-126">hello runbook can then use hello properties defined in hello JSON.</span></span>

```powershell
Param(
     [parameter(Mandatory=$true)]
     [object]$json
)

# Connect tooAzure account   
$Conn = Get-AutomationConnection -Name AzureRunAsConnection
Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint

# Convert object tooactual JSON
$json = $json | ConvertFrom-Json

# Use hello values from hello JSON object as hello parameters for your command
Start-AzureRmVM -Name $json.VMName -ResourceGroupName $json.ResourceGroup
 ```

 <span data-ttu-id="9b948-127">Сохраните и опубликуйте этот модуль runbook в учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="9b948-127">Save and publish this runbook in your Automation account.</span></span>

## <a name="call-hello-runbook-from-powershell"></a><span data-ttu-id="9b948-128">Вызов hello runbook из PowerShell</span><span class="sxs-lookup"><span data-stu-id="9b948-128">Call hello runbook from PowerShell</span></span>

<span data-ttu-id="9b948-129">Теперь можно вызвать hello runbook с локального компьютера с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9b948-129">Now you can call hello runbook from your local machine by using Azure PowerShell.</span></span>
<span data-ttu-id="9b948-130">Выполните следующие команды PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="9b948-130">Run hello following PowerShell commands:</span></span>

1. <span data-ttu-id="9b948-131">Вход tooAzure:</span><span class="sxs-lookup"><span data-stu-id="9b948-131">Log in tooAzure:</span></span>
   ```powershell
   Login-AzureRmAccount
   ```
    <span data-ttu-id="9b948-132">Вы являются tooenter запрашиваемые учетные данные Azure.</span><span class="sxs-lookup"><span data-stu-id="9b948-132">You are prompted tooenter your Azure credentials.</span></span>
1. <span data-ttu-id="9b948-133">Получение содержимого hello hello JSON-файл и преобразовать его в строку tooa:</span><span class="sxs-lookup"><span data-stu-id="9b948-133">Get hello contents of hello JSON file and convert it tooa string:</span></span>
    ```powershell
    $json =  (Get-content -path 'JsonPath\test.json' -Raw) | Out-string
    ```
    <span data-ttu-id="9b948-134">`JsonPath`— путь hello, где был сохранен файл JSON hello.</span><span class="sxs-lookup"><span data-stu-id="9b948-134">`JsonPath` is hello path where you saved hello JSON file.</span></span>
1. <span data-ttu-id="9b948-135">Преобразовать содержимое строки hello `$json` tooa объект PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9b948-135">Convert hello string contents of `$json` tooa PowerShell object:</span></span>
   ```powershell
   $JsonParams = @{"json"=$json}
   ```
1. <span data-ttu-id="9b948-136">Создать хэш-таблицу для параметров hello `Start-AzureRmAutomstionRunbook`:</span><span class="sxs-lookup"><span data-stu-id="9b948-136">Create a hashtable for hello parameters for `Start-AzureRmAutomstionRunbook`:</span></span>
   ```powershell
   $RBParams = @{
        AutomationAccountName = 'AATest'
        ResourceGroupName = 'RGTest'
        Name = 'Test-Json'
        Parameters = $JsonParams
   }
   ```
   <span data-ttu-id="9b948-137">Обратите внимание, что вы задаете значение hello `Parameters` toohello объект PowerShell, содержащий значения hello из файла JSON hello.</span><span class="sxs-lookup"><span data-stu-id="9b948-137">Notice that you are setting hello value of `Parameters` toohello PowerShell object that contains hello values from hello JSON file.</span></span> 
1. <span data-ttu-id="9b948-138">Запустить hello runbook</span><span class="sxs-lookup"><span data-stu-id="9b948-138">Start hello runbook</span></span>
   ```powershell
   $job = Start-AzureRmAutomationRunbook @RBParams
   ```

<span data-ttu-id="9b948-139">Hello runbook используются значения hello из toostart файла JSON hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="9b948-139">hello runbook uses hello values from hello JSON file toostart a VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b948-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9b948-140">Next steps</span></span>

* <span data-ttu-id="9b948-141">toolearn Дополнительные сведения о редактирования модулей Runbook PowerShell и рабочий процесс PowerShell с помощью текстового редактора в разделе [редактирования текстовое Runbook в автоматизации Azure](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="9b948-141">toolearn more about editing PowerShell and PowerShell Workflow runbooks with a textual editor, see [Editing textual runbooks in Azure Automation](automation-edit-textual-runbook.md)</span></span> 
* <span data-ttu-id="9b948-142">в разделе toolearn Дополнительные сведения о создании и импорт модулей Runbook, [Создание или импорт модуля runbook в автоматизации Azure](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="9b948-142">toolearn more about creating and importing runbooks, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md)</span></span>


