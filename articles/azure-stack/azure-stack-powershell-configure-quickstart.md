---
title: "aaaInstall и настроить PowerShell для Azure стека краткое руководство | Документы Microsoft"
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
ms.openlocfilehash: bb0bed983a09e32dbaaa39159b1d6d8bae7ea690
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-up-and-running-with-powershell-in-azure-stack"></a><span data-ttu-id="36d60-103">Приступить к работе с PowerShell в стек Azure</span><span class="sxs-lookup"><span data-stu-id="36d60-103">Get up and running with PowerShell in Azure Stack</span></span>

<span data-ttu-id="36d60-104">Эта статья является tooinstall быстрого запуска и настройки среды Azure стека с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="36d60-104">This article is a quick start tooinstall and configure Azure Stack environment with PowerShell.</span></span> <span data-ttu-id="36d60-105">Этот сценарий, приведенный в этой статье — hello области tooby **стека Azure оператор** только.</span><span class="sxs-lookup"><span data-stu-id="36d60-105">This script provided in this article is scoped tooby hello **Azure Stack operator** only.</span></span>

<span data-ttu-id="36d60-106">Эта статья содержит в сжатом hello действия, описанные в hello [установите PowerShell]( azure-stack-powershell-install.md), [загрузить набор средств]( azure-stack-powershell-download.md), [настройки среды PowerShell hello Azure стека оператор]( azure-stack-powershell-configure-admin.md) статей.</span><span class="sxs-lookup"><span data-stu-id="36d60-106">This article is a condensed version of hello steps described in hello [Install PowerShell]( azure-stack-powershell-install.md), [Download tools]( azure-stack-powershell-download.md), [Configure hello Azure Stack operator's PowerShell environment]( azure-stack-powershell-configure-admin.md) articles.</span></span> <span data-ttu-id="36d60-107">С помощью скриптов hello в этом разделе, можно настроить PowerShell для Azure стека сред, развернутых с помощью служб федерации Active Directory или Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="36d60-107">By using hello scripts in this topic, you can set up PowerShell for Azure Stack environments that are deployed with Azure Active Directory or Active Directory Federation Services.</span></span>  


## <a name="set-up-powershell-for-aad-based-deployments"></a><span data-ttu-id="36d60-108">Настроить PowerShell для развертывания на основе AAD</span><span class="sxs-lookup"><span data-stu-id="36d60-108">Set up PowerShell for AAD based deployments</span></span>

<span data-ttu-id="36d60-109">Войдите в tooyour пакет средств разработки Azure стека или внешнего клиента на основе Windows, при подключении через виртуальную частную сеть.</span><span class="sxs-lookup"><span data-stu-id="36d60-109">Sign in tooyour Azure Stack Development Kit, or a Windows-based external client if you are connected through VPN.</span></span> <span data-ttu-id="36d60-110">Откройте сеанс интегрированной среды Сценариев PowerShell с повышенными привилегиями и выполните hello следующий скрипт:</span><span class="sxs-lookup"><span data-stu-id="36d60-110">Open an elevated PowerShell ISE session and run hello following script:</span></span>

```powershell
# Specify Azure Active Directory tenant name
$TenantName = "<mydirectory>.onmicrosoft.com"

# Set hello module repository and hello execution policy
Set-PSRepository `
  -Name "PSGallery" `
  -InstallationPolicy Trusted

Set-ExecutionPolicy RemoteSigned `
  -force

# Uninstall any existing Azure PowerShell modules. toouninstall, close all hello active PowerShell sessions and run hello following command:
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

# Download Azure Stack tools from GitHub and import hello connect module
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

# Configure hello cloud administrator’s PowerShell environment.
Add-AzureRMEnvironment `
  -Name "AzureStackAdmin" `
  -ArmEndpoint "https://adminmanagement.local.azurestack.external"

Set-AzureRmEnvironment `
  -Name "AzureStackAdmin" `
  -GraphAudience "https://graph.windows.net/"

$TenantID = Get-AzsDirectoryTenantId `
  -AADTenantName $TenantName `
  -EnvironmentName AzureStackAdmin

# Sign-in toohello administrative portal.
Login-AzureRmAccount `
  -EnvironmentName "AzureStackAdmin" `
  -TenantId $TenantID 

```

## <a name="set-up-powershell-for-ad-fs-based-deployments"></a><span data-ttu-id="36d60-111">Настроить PowerShell для развертывания на основе AD FS</span><span class="sxs-lookup"><span data-stu-id="36d60-111">Set up PowerShell for AD FS based deployments</span></span> 

<span data-ttu-id="36d60-112">Войдите в tooyour пакет средств разработки Azure стека или внешнего клиента на основе Windows, при подключении через виртуальную частную сеть.</span><span class="sxs-lookup"><span data-stu-id="36d60-112">Sign in tooyour Azure Stack Development Kit, or a Windows-based external client if you are connected through VPN.</span></span> <span data-ttu-id="36d60-113">Откройте сеанс интегрированной среды Сценариев PowerShell с повышенными привилегиями и выполните hello следующий скрипт:</span><span class="sxs-lookup"><span data-stu-id="36d60-113">Open an elevated PowerShell ISE session and run hello following script:</span></span>

```powershell

# Set hello module repository and hello execution policy
Set-PSRepository `
  -Name "PSGallery" `
  -InstallationPolicy Trusted

Set-ExecutionPolicy RemoteSigned `
  -force

# Uninstall any existing Azure PowerShell modules. toouninstall, close all hello active PowerShell sessions and run hello following command:
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

# Download Azure Stack tools from GitHub and import hello connect module
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

# Configure hello cloud administrator’s PowerShell environment.
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

# Sign-in toohello administrative portal.
Login-AzureRmAccount `
  -EnvironmentName "AzureStackAdmin" `
  -TenantId $TenantID 

```

## <a name="test-hello-connectivity"></a><span data-ttu-id="36d60-114">Проверка подключения hello</span><span class="sxs-lookup"><span data-stu-id="36d60-114">Test hello connectivity</span></span>

<span data-ttu-id="36d60-115">Настройки PowerShell можно проверить конфигурацию hello, создание группы ресурсов:</span><span class="sxs-lookup"><span data-stu-id="36d60-115">Now that you’ve configured PowerShell, you can test hello configuration by creating a resource group:</span></span>

```powershell
New-AzureRMResourceGroup -Name "ContosoVMRG" -Location Local
```

<span data-ttu-id="36d60-116">При создании группы ресурсов hello выходные данные командлета hello hello подготовки состояние свойство имеет значение слишком «успешно выполнено.»</span><span class="sxs-lookup"><span data-stu-id="36d60-116">When hello resource group is created, hello cmdlet output has hello Provisioning state property set too"Succeeded."</span></span>

## <a name="next-steps"></a><span data-ttu-id="36d60-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="36d60-117">Next steps</span></span>

* [<span data-ttu-id="36d60-118">Установка и настройка CLI</span><span class="sxs-lookup"><span data-stu-id="36d60-118">Install and configure CLI</span></span>](azure-stack-connect-cli.md)

* [<span data-ttu-id="36d60-119">Шаблоны разработки</span><span class="sxs-lookup"><span data-stu-id="36d60-119">Develop templates</span></span>](azure-stack-develop-templates.md)







