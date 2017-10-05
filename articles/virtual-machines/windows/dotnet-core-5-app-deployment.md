---
title: "Автоматизация развертывания приложений с помощью расширений виртуальной машины | Документация Майкрософт"
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
ms.openlocfilehash: f2996eef71b39c6240fac5484854f72d3e657d0f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="5f55f-103">Развертывание приложений с использованием шаблонов Azure Resource Manager для виртуальных машин Windows</span><span class="sxs-lookup"><span data-stu-id="5f55f-103">Application deployment with Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="5f55f-104">Как только все инфраструктурные требования Azure будут определены и на их основе будет создан шаблон развертывания, можно приступать фактическому развертыванию приложения.</span><span class="sxs-lookup"><span data-stu-id="5f55f-104">Once all Azure infrastructural requirements have been identified and translated into a deployment template, the actual application deployment needs to be addressed.</span></span> <span data-ttu-id="5f55f-105">Развертывание приложения в данном случае сводится к установке фактических двоичных файлов приложения в ресурсы Azure.</span><span class="sxs-lookup"><span data-stu-id="5f55f-105">Application deployment here is referring to installing the actual application binaries onto Azure resources.</span></span> <span data-ttu-id="5f55f-106">Чтобы развернуть приложение магазина музыки, на каждой виртуальной машине необходимо установить и настроить .NET Core и IIS.</span><span class="sxs-lookup"><span data-stu-id="5f55f-106">For the Music Store sample, .Net Core and IIS need to be installed and configured on each virtual machine.</span></span> <span data-ttu-id="5f55f-107">Вам потребуется установить двоичные файлы магазина музыки на виртуальную машину и предварительно создать базу данных музыкального магазина.</span><span class="sxs-lookup"><span data-stu-id="5f55f-107">The Music Store binaries need to be installed onto the virtual machine, and the Music Store database pre-created.</span></span>

<span data-ttu-id="5f55f-108">В этом документе описана автоматизация развертывания и настройки приложений на виртуальных машинах Azure с помощью расширений виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5f55f-108">This document details how Virtual Machine extensions can automate application deployment and configuration to Azure virtual machines.</span></span> <span data-ttu-id="5f55f-109">Здесь будут описаны все зависимости и уникальные настройки.</span><span class="sxs-lookup"><span data-stu-id="5f55f-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="5f55f-110">Чтобы оптимизировать процесс, заранее разверните экземпляр решения в подписке Azure, а затем установите шаблон Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5f55f-110">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="5f55f-111">Полный шаблон можно найти [здесь](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="5f55f-111">The complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="configuration-script"></a><span data-ttu-id="5f55f-112">Скрипт настройки</span><span class="sxs-lookup"><span data-stu-id="5f55f-112">Configuration script</span></span>
<span data-ttu-id="5f55f-113">Расширения виртуальных машин — это специальные программы, которые выполняются на виртуальных машинах для автоматизации настройки.</span><span class="sxs-lookup"><span data-stu-id="5f55f-113">Virtual Machine extensions are specialized programs that execute against virtual machines to provide configuration automation.</span></span> <span data-ttu-id="5f55f-114">Расширения используются в различных целях, например для автоматизации антивирусных программ, настройки ведения журнала и конфигурации Docker.</span><span class="sxs-lookup"><span data-stu-id="5f55f-114">Extensions are available for many specific purposes such as anti-virus, logging configuration, and Docker configuration.</span></span> <span data-ttu-id="5f55f-115">Расширение пользовательских скриптов можно использовать для запуска любого скрипта на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="5f55f-115">The Custom Script extension can be used to run any script against a virtual machine.</span></span> <span data-ttu-id="5f55f-116">В примере магазина музыки расширение пользовательских скриптов используется для настройки виртуальных машинах Windows и установки приложения магазина музыки.</span><span class="sxs-lookup"><span data-stu-id="5f55f-116">With the Music Store sample, it is up to the custom script extension to configure the Windows virtual machines and install the Music Store application.</span></span>

<span data-ttu-id="5f55f-117">Прежде чем перейти к подробному описанию того, как расширения виртуальных машин объявляются в шаблоне Azure Resource Manager, изучите выполняющийся скрипт.</span><span class="sxs-lookup"><span data-stu-id="5f55f-117">Before detailing how virtual machine extensions are declared in an Azure Resource Manager template, examine the script that is run.</span></span> <span data-ttu-id="5f55f-118">Он настраивает виртуальную машину Windows для размещения приложения магазина музыки.</span><span class="sxs-lookup"><span data-stu-id="5f55f-118">This script configures the Windows virtual machine to host the Music Store application.</span></span> <span data-ttu-id="5f55f-119">Во время выполнения скрипт устанавливает все необходимое программное обеспечение, устанавливает приложение магазина музыки из системы управления версиями и выполняет подготовку базы данных.</span><span class="sxs-lookup"><span data-stu-id="5f55f-119">When run, the script installs all needed software, install the Music store application from source control, and prepare the database.</span></span> 

> <span data-ttu-id="5f55f-120">Этот пример предназначен только для демонстрации.</span><span class="sxs-lookup"><span data-stu-id="5f55f-120">This sample is for demonstration purposes.</span></span>

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

## <a name="vm-script-extension"></a><span data-ttu-id="5f55f-121">Расширение скриптов виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="5f55f-121">VM Script Extension</span></span>
<span data-ttu-id="5f55f-122">Расширения ВМ можно запустить на виртуальной машине во время сборки, включив ресурс расширения в шаблон Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5f55f-122">VM Extensions can be run against a virtual machine at build time by including the extension resource in the Azure Resource Manager template.</span></span> <span data-ttu-id="5f55f-123">Чтобы добавить расширение, можно использовать мастер добавления ресурсов в Visual Studio или вставить в шаблон развертывания правильно определенный объект JSON.</span><span class="sxs-lookup"><span data-stu-id="5f55f-123">The extension can be added with the Visual Studio Add Resource wizard, or by inserting valid JSON into the template.</span></span> <span data-ttu-id="5f55f-124">Ресурс расширения скрипта вложен в ресурс виртуальной машины. Это можно увидеть в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="5f55f-124">The Script Extension resource is nested inside the Virtual Machine resource; this can be seen in the following example.</span></span>

<span data-ttu-id="5f55f-125">Щелкните эту ссылку, чтобы увидеть пример JSON в шаблоне Resource Manager: [расширение скрипта виртуальной машины](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339).</span><span class="sxs-lookup"><span data-stu-id="5f55f-125">Follow this link to see the JSON sample within the Resource Manager template – [VM Script Extension](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339).</span></span> 

<span data-ttu-id="5f55f-126">Обратите внимание, что в объекте JSON, приведенном ниже, скрипт хранится в GitHub.</span><span class="sxs-lookup"><span data-stu-id="5f55f-126">Notice in the below JSON that the script is stored in GitHub.</span></span> <span data-ttu-id="5f55f-127">Этот скрипт также может храниться в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="5f55f-127">This script could also be stored in Azure Blob storage.</span></span> <span data-ttu-id="5f55f-128">Кроме того, шаблоны Azure Resource Manager позволяют создать строку выполнения скрипта так, чтобы значения параметров шаблона можно было использовать в качестве параметров для выполнения скрипта.</span><span class="sxs-lookup"><span data-stu-id="5f55f-128">Also, Azure Resource Manager templates allow the script execution string to be constructed such that template parameters values can be used as parameters for script execution.</span></span> <span data-ttu-id="5f55f-129">В этом случае данные указываются при развертывании шаблонов, и эти значения затем можно использовать при выполнении скрипта.</span><span class="sxs-lookup"><span data-stu-id="5f55f-129">In this case data is provided when deploying the templates, and these values can then be used when executing the script.</span></span>

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

<span data-ttu-id="5f55f-130">Как упоминалось выше, пользовательские сценарии можно также сохранять в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="5f55f-130">As mentioned above, it is also possible to store your custom scripts in Azure Blob storage.</span></span> <span data-ttu-id="5f55f-131">Существуют два варианта хранения ресурсов сценария в хранилище BLOB-объектов. Можно сделать контейнер и сценарий общедоступными и применить подход, описанный выше. Можно также хранить сценарий в частном хранилище BLOB-объектов, что потребует указать storageAccountName и storageAccountKey в определении ресурсов CustomScriptExtension.</span><span class="sxs-lookup"><span data-stu-id="5f55f-131">There are two options for storing the script resources in blob storage; either make the container/script public and follow the same approach as above, or it can also be kept in private blob storage which requires you to provide the storageAccountName and storageAccountKey to the CustomScriptExtension resource definition.</span></span>

<span data-ttu-id="5f55f-132">В приведенном ниже примере мы пошли дальше.</span><span class="sxs-lookup"><span data-stu-id="5f55f-132">In the example below we have gone a step further.</span></span> <span data-ttu-id="5f55f-133">Хотя во время развертывания можно предоставить имя учетной записи хранения и ключ в качестве параметра или переменной, в шаблонах Resource Manager доступна функция `listKeys`, которая может программно получить ключ учетной записи хранения и вставить его в шаблон во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="5f55f-133">While it is possible to provide the storage account name and key as a parameter or variable during deployment, Resource Manager templates provide the `listKeys` function that can obtain the storage account key programmatically and insert it in to the template for you at deployment time.</span></span>

<span data-ttu-id="5f55f-134">В приведенном ниже примере определения ресурса CustomScriptExtension пользовательский сценарий уже передан в учетную запись хранения Azure `mystorageaccount9999`, которая существует в группе ресурсов `mysa999rgname`.</span><span class="sxs-lookup"><span data-stu-id="5f55f-134">In the example CustomScriptExtension resource definition below, our custom script has already been uploaded to an Azure storage account called `mystorageaccount9999` which exists in another Resource Group called `mysa999rgname`.</span></span> <span data-ttu-id="5f55f-135">При развертывании шаблона, содержащего этот ресурс, функция `listKeys` программно получает ключ учетной записи хранения `mystorageaccount9999` в группе ресурсов `mysa999rgname` и вставляет его в шаблон.</span><span class="sxs-lookup"><span data-stu-id="5f55f-135">When we deploy a template containing this resource, the `listKeys` function programmatically obtains the storage account key for the storage account `mystorageaccount9999` in the Resource Group `mysa999rgname` and inserts it in to the template for us.</span></span>

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

<span data-ttu-id="5f55f-136">Основным преимуществом такого подхода является то, что он не требует изменять шаблон или параметры развертывания в случае изменения ключа учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="5f55f-136">The main benefit of this approach is that it does not require you to change your template or deployment parameters in the event of the storage account key changing.</span></span>

<span data-ttu-id="5f55f-137">Дополнительные сведения об использовании пользовательского расширения сценария см. в статье [Использование расширения пользовательских сценариев для виртуальных машин Linux с шаблонами Azure Resource Manager](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5f55f-137">For more information on using the custom script extension, see [Custom script extensions with Resource Manager templates](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-step"></a><span data-ttu-id="5f55f-138">Дальнейшее действие</span><span class="sxs-lookup"><span data-stu-id="5f55f-138">Next Step</span></span>
<hr>

[<span data-ttu-id="5f55f-139">Ознакомьтесь с другими шаблонами Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5f55f-139">Explore More Azure Resource Manager Templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

