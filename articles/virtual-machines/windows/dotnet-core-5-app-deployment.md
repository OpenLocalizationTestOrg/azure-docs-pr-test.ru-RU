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
# <a name="application-deployment-with-azure-resource-manager-templates-for-windows-vms"></a>Развертывание приложений с использованием шаблонов Azure Resource Manager для виртуальных машин Windows

После выявления и преобразовать в шаблон развертывания все требования для Azure инфраструктурных развертывания приложения hello должен обращаться toobe. Развертывание приложения в данном ссылается двоичные файлы приложения hello tooinstalling на ресурсах Azure. Образец hello Music Store, .net Core и IIS должны toobe устанавливается и настраивается на каждой виртуальной машине. предварительно создать Hello Music Store двоичные файлы должны toobe установлена на виртуальной машине hello и hello Music Store базы данных.

В этом документе описаны как расширения виртуальных машин можно автоматизировать приложения развертывание и настройку tooAzure виртуальных машин. Здесь будут описаны все зависимости и уникальные настройки. Для получения наилучших результатов hello предварительно разверните экземпляр tooyour решения hello подписки Azure, работают вместе с hello шаблона диспетчера ресурсов Azure. Полный шаблон Hello можно найти здесь — [музыка хранилища развертывания в Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="configuration-script"></a>Скрипт настройки
Расширения виртуальных машин — это специализированные программы, применяемыми автоматизации конфигурации tooprovide виртуальных машин. Расширения используются в различных целях, например для автоматизации антивирусных программ, настройки ведения журнала и конфигурации Docker. Hello расширение пользовательского скрипта можно использовать toorun любой скрипт от виртуальной машины. Образец hello Music Store он работает toohello пользовательского скрипта расширения tooconfigure hello виртуальных машинах и установить приложение Music Store hello.

Перед с подробным описанием объявлены как расширения виртуальных машин в шаблон диспетчера ресурсов Azure, изучите hello скрипт, который выполняется. Этот скрипт настраивает toohost виртуальной машины Windows hello hello приложение Music Store. При запуске hello скрипт устанавливает все необходимое программное обеспечение, установить приложение магазина музыка hello из системы управления версиями и подготовки hello базы данных. 

> Этот пример предназначен только для демонстрации.

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

## <a name="vm-script-extension"></a>Расширение скриптов виртуальной машины
Расширения ВМ может выполняться от виртуальной машины во время сборки, включая расширения ресурсов hello в hello шаблона диспетчера ресурсов Azure. Hello расширения можно добавить с помощью мастера добавления ресурсов Visual Studio hello, или путем вставки допустимых данных JSON в шаблоне hello. Hello расширение сценария ресурса вложен в hello ресурса виртуальной машины; Это можно заметить в следующий пример hello.

Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [расширение ВМ сценария](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339). 

Обратите внимание на hello ниже JSON, hello сценарий хранится в GitHub. Этот скрипт также может храниться в хранилище BLOB-объектов Azure. Кроме того шаблоны Azure Resource Manager разрешить hello сценария выполнения строки toobe составить таким образом, что значения параметров шаблона, которая может использоваться в качестве параметров для выполнения скриптов. В этом случае данные предоставляются в развертывание шаблонов hello, и эти значения можно затем использовать при выполнении сценария hello.

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

Как упоминалось выше, это также возможно toostore пользовательских скриптов в хранилище больших двоичных объектов Azure. Существует два варианта для хранения ресурсов сценария hello в хранилище больших двоичных объектов; сделать hello открытого контейнера файлов и сценариев и следуйте hello подход таким же, как описано выше, или также могут храниться в хранилище закрытый большой двоичный объект, требующий tooprovide hello storageAccountName и storageAccountKey toohello CustomScriptExtension определения ресурса.

В приведенном ниже примере hello мы вышли шаг дальнейшей. Это имя учетной записи хранения возможных tooprovide hello и ключ как имя параметра или переменной во время развертывания, шаблоны диспетчера ресурсов предоставляют hello `listKeys` функции, можно получить учетную запись хранения hello программного ключа и вставьте его в toohello шаблон автоматически во время развертывания.

В примере hello, CustomScriptExtension определения ресурсов ниже, наш пользовательский скрипт уже был загруженного tooan именем учетной записи хранилища Azure `mystorageaccount9999` которого существует в другой группе ресурсов с именем `mysa999rgname`. При развертывании шаблона, содержащего этот ресурс, hello `listKeys` функция программным образом получает hello ключ учетной записи хранилища для учетной записи хранения hello `mystorageaccount9999` в hello группы ресурсов `mysa999rgname` и вставляет его в шаблон toohello нам.

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

Hello основным преимуществом такого подхода является не требуется, вы toochange шаблон или параметры развертывания для события hello hello изменение ключа учетной записи хранилища.

Дополнительные сведения об использовании расширения пользовательского скрипта hello см. в разделе [пользовательских расширений сценария с помощью шаблонов диспетчера ресурсов](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="next-step"></a>Дальнейшее действие
<hr>

[Ознакомьтесь с другими шаблонами Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates)

