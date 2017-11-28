---
title: "aaaAutomating развертывания приложений с помощью расширения виртуальных машин | Документы Microsoft"
description: "Руководство по .NET Core для виртуальных машин Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 79c91304-6c1b-4354-a185-fecc129b139d
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6d52537fbd4e935f19d3864def11484f519f8598
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="57bd8-103">Развертывание приложений с использованием шаблонов Azure Resource Manager для виртуальных машин Windows</span><span class="sxs-lookup"><span data-stu-id="57bd8-103">Application deployment with Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="57bd8-104">После выявления и преобразовать в шаблон развертывания все требования для Azure инфраструктурных развертывания приложения hello должен обращаться toobe.</span><span class="sxs-lookup"><span data-stu-id="57bd8-104">Once all Azure infrastructural requirements have been identified and translated into a deployment template, hello actual application deployment needs toobe addressed.</span></span> <span data-ttu-id="57bd8-105">Развертывание приложения в данном ссылается двоичные файлы приложения hello tooinstalling на ресурсах Azure.</span><span class="sxs-lookup"><span data-stu-id="57bd8-105">Application deployment here is referring tooinstalling hello actual application binaries onto Azure resources.</span></span> <span data-ttu-id="57bd8-106">Образец hello Music Store, .net Core и IIS должны toobe устанавливается и настраивается на каждой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="57bd8-106">For hello Music Store sample, .Net Core and IIS need toobe installed and configured on each virtual machine.</span></span> <span data-ttu-id="57bd8-107">предварительно создать Hello Music Store двоичные файлы должны toobe установлена на виртуальной машине hello и hello Music Store базы данных.</span><span class="sxs-lookup"><span data-stu-id="57bd8-107">hello Music Store binaries need toobe installed onto hello virtual machine, and hello Music Store database pre-created.</span></span>

<span data-ttu-id="57bd8-108">В этом документе описаны как расширения виртуальных машин можно автоматизировать приложения развертывание и настройку tooAzure виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="57bd8-108">This document details how Virtual Machine extensions can automate application deployment and configuration tooAzure virtual machines.</span></span> <span data-ttu-id="57bd8-109">Здесь будут описаны все зависимости и уникальные настройки.</span><span class="sxs-lookup"><span data-stu-id="57bd8-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="57bd8-110">Для получения наилучших результатов hello предварительно разверните экземпляр tooyour решения hello подписки Azure, работают вместе с hello шаблона диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="57bd8-110">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="57bd8-111">Полный шаблон Hello можно найти здесь — [музыка хранилища развертывания в Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="57bd8-111">hello complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="configuration-script"></a><span data-ttu-id="57bd8-112">Скрипт настройки</span><span class="sxs-lookup"><span data-stu-id="57bd8-112">Configuration script</span></span>
<span data-ttu-id="57bd8-113">Расширения виртуальных машин — это специализированные программы, применяемыми автоматизации конфигурации tooprovide виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="57bd8-113">Virtual Machine extensions are specialized programs that execute against virtual machines tooprovide configuration automation.</span></span> <span data-ttu-id="57bd8-114">Расширения используются в различных целях, например для автоматизации антивирусных программ, настройки ведения журнала и конфигурации Docker.</span><span class="sxs-lookup"><span data-stu-id="57bd8-114">Extensions are available for many specific purposes such as anti-virus, logging configuration, and Docker configuration.</span></span> <span data-ttu-id="57bd8-115">Hello расширение пользовательского скрипта можно использовать toorun любой скрипт от виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="57bd8-115">hello Custom Script extension can be used toorun any script against a virtual machine.</span></span> <span data-ttu-id="57bd8-116">Образец hello Music Store он работает toohello пользовательского скрипта расширения tooconfigure hello виртуальных машинах и установить приложение Music Store hello.</span><span class="sxs-lookup"><span data-stu-id="57bd8-116">With hello Music Store sample, it is up toohello custom script extension tooconfigure hello Windows virtual machines and install hello Music Store application.</span></span>

<span data-ttu-id="57bd8-117">Перед с подробным описанием объявлены как расширения виртуальных машин в шаблон диспетчера ресурсов Azure, изучите hello скрипт, который выполняется.</span><span class="sxs-lookup"><span data-stu-id="57bd8-117">Before detailing how virtual machine extensions are declared in an Azure Resource Manager template, examine hello script that is run.</span></span> <span data-ttu-id="57bd8-118">Этот скрипт настраивает toohost виртуальной машины Windows hello hello приложение Music Store.</span><span class="sxs-lookup"><span data-stu-id="57bd8-118">This script configures hello Windows virtual machine toohost hello Music Store application.</span></span> <span data-ttu-id="57bd8-119">При запуске hello скрипт устанавливает все необходимое программное обеспечение, установить приложение магазина музыка hello из системы управления версиями и подготовки hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="57bd8-119">When run, hello script installs all needed software, install hello Music store application from source control, and prepare hello database.</span></span> 

> <span data-ttu-id="57bd8-120">Этот пример предназначен только для демонстрации.</span><span class="sxs-lookup"><span data-stu-id="57bd8-120">This sample is for demonstration purposes.</span></span>

```PowerShell
<#
    .SYNOPSIS
        Downloads and configures .Net Core Music Store application sample across IIS and Azure SQL DB.
#>

Param (
    [string]$user,
    [string]$password,
    [string]$sqlserver
)

# Firewall
netsh advfirewall firewall add rule name="http" dir=in action=allow protocol=TCP localport=80

# Folders
New-Item -ItemType Directory c:\temp
New-Item -ItemType Directory c:\music

# Install iis
Install-WindowsFeature web-server -IncludeManagementTools

# Install dot.net core sdk
Invoke-WebRequest http://go.microsoft.com/fwlink/?LinkID=615460 -outfile c:\temp\vc_redistx64.exe
Start-Process c:\temp\vc_redistx64.exe -ArgumentList '/quiet' -Wait
Invoke-WebRequest https://go.microsoft.com/fwlink/?LinkID=809122 -outfile c:\temp\DotNetCore.1.0.0-SDK.Preview2-x64.exe
Start-Process c:\temp\DotNetCore.1.0.0-SDK.Preview2-x64.exe -ArgumentList '/quiet' -Wait
Invoke-WebRequest https://go.microsoft.com/fwlink/?LinkId=817246 -outfile c:\temp\DotNetCore.WindowsHosting.exe
Start-Process c:\temp\DotNetCore.WindowsHosting.exe -ArgumentList '/quiet' -Wait

# Download music app
Invoke-WebRequest  https://github.com/Microsoft/dotnet-core-sample-templates/raw/master/dotnet-core-music-windows/music-app/music-store-azure-demo-pub.zip -OutFile c:\temp\musicstore.zip
Expand-Archive C:\temp\musicstore.zip c:\music

# Azure SQL connection sting in environment variable
[Environment]::SetEnvironmentVariable("Data:DefaultConnection:ConnectionString", "Server=$sqlserver;Database=MusicStore;Integrated Security=False;User Id=$user;Password=$password;MultipleActiveResultSets=True;Connect Timeout=30",[EnvironmentVariableTarget]::Machine)

# Pre-create database
$env:Data:DefaultConnection:ConnectionString = "Server=$sqlserver;Database=MusicStore;Integrated Security=False;User Id=$user;Password=$password;MultipleActiveResultSets=True;Connect Timeout=30"
Start-Process 'C:\Program Files\dotnet\dotnet.exe' -ArgumentList 'c:\music\MusicStore.dll'

# Configure iis
Remove-WebSite -Name "Default Web Site"
Set-ItemProperty IIS:\AppPools\DefaultAppPool\ managedRuntimeVersion ""
New-Website -Name "MusicStore" -Port 80 -PhysicalPath C:\music\ -ApplicationPool DefaultAppPool
& iisreset
```

## <a name="vm-script-extension"></a><span data-ttu-id="57bd8-121">Расширение скриптов виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="57bd8-121">VM Script Extension</span></span>
<span data-ttu-id="57bd8-122">Расширения ВМ может выполняться от виртуальной машины во время сборки, включая расширения ресурсов hello в hello шаблона диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="57bd8-122">VM Extensions can be run against a virtual machine at build time by including hello extension resource in hello Azure Resource Manager template.</span></span> <span data-ttu-id="57bd8-123">Hello расширения можно добавить с помощью мастера добавления ресурсов Visual Studio hello, или путем вставки допустимых данных JSON в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="57bd8-123">hello extension can be added with hello Visual Studio Add Resource wizard, or by inserting valid JSON into hello template.</span></span> <span data-ttu-id="57bd8-124">Hello расширение сценария ресурса вложен в hello ресурса виртуальной машины; Это можно заметить в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="57bd8-124">hello Script Extension resource is nested inside hello Virtual Machine resource; this can be seen in hello following example.</span></span>

<span data-ttu-id="57bd8-125">Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [расширение ВМ сценария](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339).</span><span class="sxs-lookup"><span data-stu-id="57bd8-125">Follow this link toosee hello JSON sample within hello Resource Manager template – [VM Script Extension](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339).</span></span> 

<span data-ttu-id="57bd8-126">Обратите внимание на hello ниже JSON, hello сценарий хранится в GitHub.</span><span class="sxs-lookup"><span data-stu-id="57bd8-126">Notice in hello below JSON that hello script is stored in GitHub.</span></span> <span data-ttu-id="57bd8-127">Этот скрипт также может храниться в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="57bd8-127">This script could also be stored in Azure Blob storage.</span></span> <span data-ttu-id="57bd8-128">Кроме того шаблоны Azure Resource Manager разрешить hello сценария выполнения строки toobe составить таким образом, что значения параметров шаблона, которая может использоваться в качестве параметров для выполнения скриптов.</span><span class="sxs-lookup"><span data-stu-id="57bd8-128">Also, Azure Resource Manager templates allow hello script execution string toobe constructed such that template parameters values can be used as parameters for script execution.</span></span> <span data-ttu-id="57bd8-129">В этом случае данные предоставляются в развертывание шаблонов hello, и эти значения можно затем использовать при выполнении сценария hello.</span><span class="sxs-lookup"><span data-stu-id="57bd8-129">In this case data is provided when deploying hello templates, and these values can then be used when executing hello script.</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
  }
}
```

<span data-ttu-id="57bd8-130">Как упоминалось выше, это также возможно toostore пользовательских скриптов в хранилище больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="57bd8-130">As mentioned above, it is also possible toostore your custom scripts in Azure Blob storage.</span></span> <span data-ttu-id="57bd8-131">Существует два варианта для хранения ресурсов сценария hello в хранилище больших двоичных объектов; сделать hello открытого контейнера файлов и сценариев и следуйте hello подход таким же, как описано выше, или также могут храниться в хранилище закрытый большой двоичный объект, требующий tooprovide hello storageAccountName и storageAccountKey toohello CustomScriptExtension определения ресурса.</span><span class="sxs-lookup"><span data-stu-id="57bd8-131">There are two options for storing hello script resources in blob storage; either make hello container/script public and follow hello same approach as above, or it can also be kept in private blob storage which requires you tooprovide hello storageAccountName and storageAccountKey toohello CustomScriptExtension resource definition.</span></span>

<span data-ttu-id="57bd8-132">В приведенном ниже примере hello мы вышли шаг дальнейшей.</span><span class="sxs-lookup"><span data-stu-id="57bd8-132">In hello example below we have gone a step further.</span></span> <span data-ttu-id="57bd8-133">Это имя учетной записи хранения возможных tooprovide hello и ключ как имя параметра или переменной во время развертывания, шаблоны диспетчера ресурсов предоставляют hello `listKeys` функции, можно получить учетную запись хранения hello программного ключа и вставьте его в toohello шаблон автоматически во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="57bd8-133">While it is possible tooprovide hello storage account name and key as a parameter or variable during deployment, Resource Manager templates provide hello `listKeys` function that can obtain hello storage account key programmatically and insert it in toohello template for you at deployment time.</span></span>

<span data-ttu-id="57bd8-134">В примере hello, CustomScriptExtension определения ресурсов ниже, наш пользовательский скрипт уже был загруженного tooan именем учетной записи хранилища Azure `mystorageaccount9999` которого существует в другой группе ресурсов с именем `mysa999rgname`.</span><span class="sxs-lookup"><span data-stu-id="57bd8-134">In hello example CustomScriptExtension resource definition below, our custom script has already been uploaded tooan Azure storage account called `mystorageaccount9999` which exists in another Resource Group called `mysa999rgname`.</span></span> <span data-ttu-id="57bd8-135">При развертывании шаблона, содержащего этот ресурс, hello `listKeys` функция программным образом получает hello ключ учетной записи хранилища для учетной записи хранения hello `mystorageaccount9999` в hello группы ресурсов `mysa999rgname` и вставляет его в шаблон toohello нам.</span><span class="sxs-lookup"><span data-stu-id="57bd8-135">When we deploy a template containing this resource, hello `listKeys` function programmatically obtains hello storage account key for hello storage account `mystorageaccount9999` in hello Resource Group `mysa999rgname` and inserts it in toohello template for us.</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.7",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://mystorageaccount9999.blob.core.windows.net/container/configure-music-app.ps1"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]",
      "storageAccountName": "mystorageaccount9999",
      "storageAccountKey": "[listKeys(resourceId('mysa999rgname','Microsoft.Storage/storageAccounts', mystorageaccount9999), '2015-06-15').key1]"
    }
  }
}
```

<span data-ttu-id="57bd8-136">Hello основным преимуществом такого подхода является не требуется, вы toochange шаблон или параметры развертывания для события hello hello изменение ключа учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="57bd8-136">hello main benefit of this approach is that it does not require you toochange your template or deployment parameters in hello event of hello storage account key changing.</span></span>

<span data-ttu-id="57bd8-137">Дополнительные сведения об использовании расширения пользовательского скрипта hello см. в разделе [пользовательских расширений сценария с помощью шаблонов диспетчера ресурсов](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="57bd8-137">For more information on using hello custom script extension, see [Custom script extensions with Resource Manager templates](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-step"></a><span data-ttu-id="57bd8-138">Дальнейшее действие</span><span class="sxs-lookup"><span data-stu-id="57bd8-138">Next Step</span></span>
<hr>

[<span data-ttu-id="57bd8-139">Ознакомьтесь с другими шаблонами Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="57bd8-139">Explore More Azure Resource Manager Templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

