---
title: "Среда PowerShell aaaConfigure hello Azure стека оператор | Документы Microsoft"
description: "Узнайте, как tooConfigure hello Azure стека оператор среды PowerShell."
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
ms.openlocfilehash: 1a1e95b95598062f155126b9560934bba4994f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-azure-stack-operators-powershell-environment"></a><span data-ttu-id="270d1-103">Настройка среды PowerShell оператор hello стек Azure</span><span class="sxs-lookup"><span data-stu-id="270d1-103">Configure hello Azure Stack operator's PowerShell environment</span></span>

<span data-ttu-id="270d1-104">Как оператор стек Azure можно настроить пакет средств Azure стека разработки среды PowerShell.</span><span class="sxs-lookup"><span data-stu-id="270d1-104">As an Azure Stack operator, you can configure your Azure Stack Development Kit's PowerShell environment.</span></span> <span data-ttu-id="270d1-105">После настройки, можно использовать PowerShell toomanage стек Azure ресурсов, таких как создание предложений, планы, квот, управление, предупреждения и т. д. Этот раздел является областью toouse оператором hello облачных средах, если требуется tooset копирование PowerShell для среды пользователя hello, относятся только слишком[настройки среды PowerShell hello Azure стека пользователя](azure-stack-powershell-configure-user.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="270d1-105">After you configure, you can use PowerShell toomanage Azure Stack resources such as creating offers, plans, quotas, managing alerts, etc. This topic is scoped toouse with hello cloud operator environments only, if you want tooset up PowerShell for hello user environment, refer too[Configure hello Azure Stack user's PowerShell environment](azure-stack-powershell-configure-user.md) topic.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="270d1-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="270d1-106">Prerequisites</span></span>

<span data-ttu-id="270d1-107">Запустите hello следующие необходимые компоненты из hello [пакет средств разработки](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), или из внешнего клиента Windows в случае [подключен через виртуальную частную сеть](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span><span class="sxs-lookup"><span data-stu-id="270d1-107">Run hello following prerequisites either from hello [development kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span></span> 

* <span data-ttu-id="270d1-108">Установка [модули Azure PowerShell Azure стека совместимой](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="270d1-108">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>  
* <span data-ttu-id="270d1-109">Загрузите hello [toowork необходимые средства с Azure стека](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="270d1-109">Download hello [tools required toowork with Azure Stack](azure-stack-powershell-download.md).</span></span>  

## <a name="configure-hello-operator-environment-and-sign-in-tooazure-stack"></a><span data-ttu-id="270d1-110">Настройка среды оператор hello и вход tooAzure стека</span><span class="sxs-lookup"><span data-stu-id="270d1-110">Configure hello operator environment and sign in tooAzure Stack</span></span>

<span data-ttu-id="270d1-111">В зависимости от типа hello развертывания (Azure AD или AD FS), выполните одну из hello, выполнив сценарий tooconfigure hello Azure стека оператор среды с помощью PowerShell:</span><span class="sxs-lookup"><span data-stu-id="270d1-111">Based on hello type of deployment (Azure AD or AD FS), run one of hello following script tooconfigure hello Azure Stack operator environment with PowerShell:</span></span>

### <a name="azure-active-directory-aad-based-deployments"></a><span data-ttu-id="270d1-112">Azure Active Directory (AAD) на основе развертываний</span><span class="sxs-lookup"><span data-stu-id="270d1-112">Azure Active Directory (AAD) based deployments</span></span>
       
  ```powershell
  # Navigate toohello downloaded folder and import hello **Connect** PowerShell module
  Set-ExecutionPolicy RemoteSigned
  Import-Module .\Connect\AzureStack.Connect.psm1

  # Register an AzureRM environment that targets your Azure Stack instance
  Add-AzureRMEnvironment `
    -Name "AzureStackAdmin" `
    -ArmEndpoint "https://adminmanagement.local.azurestack.external"

  # Set hello GraphEndpointResourceId value
  Set-AzureRmEnvironment `
    -Name "AzureStackAdmin" `
    -GraphAudience "https://graph.windows.net/"

  # Get hello Active Directory tenantId that is used toodeploy Azure Stack
  $TenantID = Get-AzsDirectoryTenantId `
    -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
    -EnvironmentName "AzureStackAdmin"

  # Sign in tooyour environment
  Login-AzureRmAccount `
    -EnvironmentName "AzureStackAdmin" `
    -TenantId $TenantID 
  ```

### <a name="active-directory-federation-services-ad-fs-based-deployments"></a><span data-ttu-id="270d1-113">Службы федерации Active Directory (AD FS) на основе развертываний</span><span class="sxs-lookup"><span data-stu-id="270d1-113">Active Directory Federation Services (AD FS) based deployments</span></span>
         
  ```powershell
  # Navigate toohello downloaded folder and import hello **Connect** PowerShell module
  Set-ExecutionPolicy RemoteSigned
  Import-Module .\Connect\AzureStack.Connect.psm1

  # Register an AzureRM environment that targets your Azure Stack instance
  Add-AzureRMEnvironment `
    -Name "AzureStackAdmin" `
    -ArmEndpoint "https://adminmanagement.local.azurestack.external"

  # Set hello GraphEndpointResourceId value
  Set-AzureRmEnvironment `
    -Name "AzureStackAdmin" `
    -GraphAudience "https://graph.local.azurestack.external/" `
    -EnableAdfsAuthentication:$true

  # Get hello Active Directory tenantId that is used toodeploy Azure Stack     
  $TenantID = Get-AzsDirectoryTenantId `
    -ADFS `
    -EnvironmentName "AzureStackAdmin"

  # Sign in tooyour environment
  Login-AzureRmAccount `
    -EnvironmentName "AzureStackAdmin" `
    -TenantId $TenantID 
  ```

## <a name="test-hello-connectivity"></a><span data-ttu-id="270d1-114">Проверка подключения hello</span><span class="sxs-lookup"><span data-stu-id="270d1-114">Test hello connectivity</span></span>

<span data-ttu-id="270d1-115">Теперь, когда у нас есть все настройки, воспользуемся PowerShell toocreate ресурсов в Azure стека.</span><span class="sxs-lookup"><span data-stu-id="270d1-115">Now that we've got everything set up, let's use PowerShell toocreate resources within Azure Stack.</span></span> <span data-ttu-id="270d1-116">Например можно создать группу ресурсов для приложения и добавить виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="270d1-116">For example, you can create a resource group for an application and add a virtual machine.</span></span> <span data-ttu-id="270d1-117">Hello используется следующая команда toocreate группу ресурсов с именем «MyResourceGroup»:</span><span class="sxs-lookup"><span data-stu-id="270d1-117">Use hello following command toocreate a resource group named "MyResourceGroup":</span></span>

```powershell
New-AzureRmResourceGroup -Name "MyResourceGroup" -Location "Local"
```

## <a name="next-steps"></a><span data-ttu-id="270d1-118">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="270d1-118">Next steps</span></span>
* [<span data-ttu-id="270d1-119">Разработка шаблонов для Azure Stack</span><span class="sxs-lookup"><span data-stu-id="270d1-119">Develop templates for Azure Stack</span></span>](azure-stack-develop-templates.md)
* [<span data-ttu-id="270d1-120">Развертывание шаблонов с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="270d1-120">Deploy templates with PowerShell</span></span>](azure-stack-deploy-template-powershell.md)