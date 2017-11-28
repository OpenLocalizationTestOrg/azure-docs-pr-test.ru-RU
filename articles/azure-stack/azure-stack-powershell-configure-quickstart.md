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
# <a name="get-up-and-running-with-powershell-in-azure-stack"></a><span data-ttu-id="56c08-103">Приступить к работе с PowerShell в стек Azure</span><span class="sxs-lookup"><span data-stu-id="56c08-103">Get up and running with PowerShell in Azure Stack</span></span>

<span data-ttu-id="56c08-104">Эта статья является быстро приступить к установке и настройке среды Azure стека с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="56c08-104">This article is a quick start to install and configure Azure Stack environment with PowerShell.</span></span> <span data-ttu-id="56c08-105">Этот сценарий, приведенный в этой статье, ограничиваются по **стека Azure оператор** только.</span><span class="sxs-lookup"><span data-stu-id="56c08-105">This script provided in this article is scoped to by the **Azure Stack operator** only.</span></span>

<span data-ttu-id="56c08-106">Эта статья содержит в сжатом действия, описанные в [установите PowerShell]( azure-stack-powershell-install.md), [загрузить набор средств]( azure-stack-powershell-download.md), [настройки среды PowerShell оператор стек Azure]( azure-stack-powershell-configure-admin.md)статей.</span><span class="sxs-lookup"><span data-stu-id="56c08-106">This article is a condensed version of the steps described in the [Install PowerShell]( azure-stack-powershell-install.md), [Download tools]( azure-stack-powershell-download.md), [Configure the Azure Stack operator's PowerShell environment]( azure-stack-powershell-configure-admin.md) articles.</span></span> <span data-ttu-id="56c08-107">С помощью скриптов в этом разделе, можно настроить PowerShell для Azure стека сред, развернутых с помощью служб федерации Active Directory или Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="56c08-107">By using the scripts in this topic, you can set up PowerShell for Azure Stack environments that are deployed with Azure Active Directory or Active Directory Federation Services.</span></span>  


## <a name="set-up-powershell-for-aad-based-deployments"></a><span data-ttu-id="56c08-108">Настроить PowerShell для развертывания на основе AAD</span><span class="sxs-lookup"><span data-stu-id="56c08-108">Set up PowerShell for AAD based deployments</span></span>

<span data-ttu-id="56c08-109">Войдите в ваш пакет средств разработки Azure стека или внешнего клиента на основе Windows при подключении через виртуальную частную сеть.</span><span class="sxs-lookup"><span data-stu-id="56c08-109">Sign in to your Azure Stack Development Kit, or a Windows-based external client if you are connected through VPN.</span></span> <span data-ttu-id="56c08-110">Откройте сеанс интегрированной среды Сценариев PowerShell с повышенными привилегиями и выполните следующий сценарий:</span><span class="sxs-lookup"><span data-stu-id="56c08-110">Open an elevated PowerShell ISE session and run the following script:</span></span>

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

## <a name="set-up-powershell-for-ad-fs-based-deployments"></a><span data-ttu-id="56c08-111">Настроить PowerShell для развертывания на основе AD FS</span><span class="sxs-lookup"><span data-stu-id="56c08-111">Set up PowerShell for AD FS based deployments</span></span> 

<span data-ttu-id="56c08-112">Войдите в ваш пакет средств разработки Azure стека или внешнего клиента на основе Windows при подключении через виртуальную частную сеть.</span><span class="sxs-lookup"><span data-stu-id="56c08-112">Sign in to your Azure Stack Development Kit, or a Windows-based external client if you are connected through VPN.</span></span> <span data-ttu-id="56c08-113">Откройте сеанс интегрированной среды Сценариев PowerShell с повышенными привилегиями и выполните следующий сценарий:</span><span class="sxs-lookup"><span data-stu-id="56c08-113">Open an elevated PowerShell ISE session and run the following script:</span></span>

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

## <a name="test-the-connectivity"></a><span data-ttu-id="56c08-114">Проверка подключения</span><span class="sxs-lookup"><span data-stu-id="56c08-114">Test the connectivity</span></span>

<span data-ttu-id="56c08-115">Настройки PowerShell, создав группу ресурсов можно протестировать конфигурацию:</span><span class="sxs-lookup"><span data-stu-id="56c08-115">Now that you’ve configured PowerShell, you can test the configuration by creating a resource group:</span></span>

```powershell
New-AzureRMResourceGroup -Name "ContosoVMRG" -Location Local
```

<span data-ttu-id="56c08-116">При создании группы ресурсов, выходные данные командлета имеет состояние подготовки, имеющим значение «Успешно».</span><span class="sxs-lookup"><span data-stu-id="56c08-116">When the resource group is created, the cmdlet output has the Provisioning state property set to "Succeeded."</span></span>

## <a name="next-steps"></a><span data-ttu-id="56c08-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="56c08-117">Next steps</span></span>

* [<span data-ttu-id="56c08-118">Установка и настройка CLI</span><span class="sxs-lookup"><span data-stu-id="56c08-118">Install and configure CLI</span></span>](azure-stack-connect-cli.md)

* [<span data-ttu-id="56c08-119">Шаблоны разработки</span><span class="sxs-lookup"><span data-stu-id="56c08-119">Develop templates</span></span>](azure-stack-develop-templates.md)







