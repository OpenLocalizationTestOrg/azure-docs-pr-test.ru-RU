---
title: "Установите и настройте PowerShell для Azure стека краткое руководство | Документы Microsoft"
description: "Дополнительные сведения об установке и настройке PowerShell для Azure стека."
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: sngun
ms.openlocfilehash: d0fc07f20937d4867c59930b13f6aed4aa37f98d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="get-up-and-running-with-powershell-in-azure-stack"></a>Приступить к работе с PowerShell в стек Azure

Эта статья является быстро приступить к установке и настройке среды Azure стека с помощью PowerShell. Этот сценарий, приведенный в этой статье, ограничиваются по **стека Azure оператор** только.

Эта статья содержит в сжатом действия, описанные в [установите PowerShell]( azure-stack-powershell-install.md), [загрузить набор средств]( azure-stack-powershell-download.md), [настройки среды PowerShell оператор стек Azure]( azure-stack-powershell-configure-admin.md)статей. С помощью скриптов в этом разделе, можно настроить PowerShell для Azure стека сред, развернутых с помощью служб федерации Active Directory или Azure Active Directory.  


## <a name="set-up-powershell-for-aad-based-deployments"></a>Настроить PowerShell для развертывания на основе AAD

Войдите в ваш пакет средств разработки Azure стека или внешнего клиента на основе Windows при подключении через виртуальную частную сеть. Откройте сеанс интегрированной среды Сценариев PowerShell с повышенными привилегиями и выполните следующий сценарий:

```powershell
# Specify Azure Active Directory tenant name
$TenantName = "<mydirectory>.onmicrosoft.com"

# Set the module repository and the execution policy
Set-PSRepository `
  -Name "PSGallery" `
  -InstallationPolicy Trusted

Set-ExecutionPolicy RemoteSigned `
  -force

# Uninstall any existing Azure PowerShell modules. To uninstall, close all the active PowerShell sessions and run the following command:
Get-Module -ListAvailable | `
  where-Object {$_.Name -like “Azure*”} | `
  Uninstall-Module

# Install PowerShell for Azure Stack
Install-Module `
  -Name AzureRm.BootStrapper `
  -Force

Use-AzureRmProfile `
  -Profile 2017-03-09-profile `
  -Force

Install-Module `
  -Name AzureStack `
  -RequiredVersion 1.2.10 `
  -Force 

# Download Azure Stack tools from GitHub and import the connect module
cd \

invoke-webrequest `
  https://github.com/Azure/AzureStack-Tools/archive/master.zip `
  -OutFile master.zip

expand-archive master.zip `
  -DestinationPath . `
  -Force

cd AzureStack-Tools-master

Import-Module `
  .\Connect\AzureStack.Connect.psm1

# Configure the cloud administrator’s PowerShell environment.
Add-AzureRMEnvironment `
  -Name "AzureStackAdmin" `
  -ArmEndpoint "https://adminmanagement.local.azurestack.external"

Set-AzureRmEnvironment `
  -Name "AzureStackAdmin" `
  -GraphAudience "https://graph.windows.net/"

$TenantID = Get-AzsDirectoryTenantId `
  -AADTenantName $TenantName `
  -EnvironmentName AzureStackAdmin

# Sign-in to the administrative portal.
Login-AzureRmAccount `
  -EnvironmentName "AzureStackAdmin" `
  -TenantId $TenantID 

```

## <a name="set-up-powershell-for-ad-fs-based-deployments"></a>Настроить PowerShell для развертывания на основе AD FS 

Войдите в ваш пакет средств разработки Azure стека или внешнего клиента на основе Windows при подключении через виртуальную частную сеть. Откройте сеанс интегрированной среды Сценариев PowerShell с повышенными привилегиями и выполните следующий сценарий:

```powershell

# Set the module repository and the execution policy
Set-PSRepository `
  -Name "PSGallery" `
  -InstallationPolicy Trusted

Set-ExecutionPolicy RemoteSigned `
  -force

# Uninstall any existing Azure PowerShell modules. To uninstall, close all the active PowerShell sessions and run the following command:
Get-Module -ListAvailable | `
  where-Object {$_.Name -like “Azure*”} | `
  Uninstall-Module

# Install PowerShell for Azure Stack
Install-Module `
  -Name AzureRm.BootStrapper `
  -Force

Use-AzureRmProfile `
  -Profile 2017-03-09-profile `
  -Force

Install-Module `
  -Name AzureStack `
  -RequiredVersion 1.2.10 `
  -Force 

# Download Azure Stack tools from GitHub and import the connect module
cd \

invoke-webrequest `
  https://github.com/Azure/AzureStack-Tools/archive/master.zip `
  -OutFile master.zip

expand-archive master.zip `
  -DestinationPath . `
  -Force

cd AzureStack-Tools-master

Import-Module `
  .\Connect\AzureStack.Connect.psm1

# Configure the cloud administrator’s PowerShell environment.
Add-AzureRMEnvironment `
  -Name "AzureStackAdmin" `
  -ArmEndpoint "https://adminmanagement.local.azurestack.external"

Set-AzureRmEnvironment `
  -Name "AzureStackAdmin" `
  -GraphAudience "https://graph.local.azurestack.external/" `
  -EnableAdfsAuthentication:$true

$TenantID = Get-AzsDirectoryTenantId `
  -ADFS `
  -EnvironmentName "AzureStackAdmin"

# Sign-in to the administrative portal.
Login-AzureRmAccount `
  -EnvironmentName "AzureStackAdmin" `
  -TenantId $TenantID 

```

## <a name="test-the-connectivity"></a>Проверка подключения

Настройки PowerShell, создав группу ресурсов можно протестировать конфигурацию:

```powershell
New-AzureRMResourceGroup -Name "ContosoVMRG" -Location Local
```

При создании группы ресурсов, выходные данные командлета имеет состояние подготовки, имеющим значение «Успешно».

## <a name="next-steps"></a>Дальнейшие действия

* [Установка и настройка CLI](azure-stack-connect-cli.md)

* [Шаблоны разработки](azure-stack-develop-templates.md)







