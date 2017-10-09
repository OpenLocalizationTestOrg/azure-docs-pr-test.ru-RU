---
title: "Среда PowerShell aaaConfigure hello Azure стека пользователя | Документы Microsoft"
description: "Настройка среды PowerShell hello Azure стека пользователя"
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
ms.openlocfilehash: 8e7ccea24a1917d349ab06e0abe29f534b47b5d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-azure-stack-users-powershell-environment"></a><span data-ttu-id="158c4-103">Настройка среды PowerShell hello Azure стека пользователя</span><span class="sxs-lookup"><span data-stu-id="158c4-103">Configure hello Azure Stack user's PowerShell environment</span></span>

<span data-ttu-id="158c4-104">Как пользователь с стек Azure можно настроить пакет средств Azure стека разработки среды PowerShell.</span><span class="sxs-lookup"><span data-stu-id="158c4-104">As an Azure Stack user, you can configure your Azure Stack Development Kit's PowerShell environment.</span></span> <span data-ttu-id="158c4-105">После настройки, можно использовать PowerShell toomanage стека Azure ресурсов, таких как подписаться toooffers, создания виртуальных машин, развертывание шаблонов диспетчера ресурсов Azure и т. д. В этом разделе с областью toouse с hello пользовательских сред, следует tooset копирование PowerShell для hello облачной среде оператор обратитесь toohello [настройки среды PowerShell hello Azure стека оператор](azure-stack-powershell-configure-admin.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="158c4-105">After you configure, you can use PowerShell toomanage Azure Stack resources such as subscribe toooffers, create virtual machines, deploy Azure Resource Manager templates,  etc. This topic is scoped toouse with hello user environments only, if you want tooset up PowerShell for hello cloud operator environment, refer toohello [Configure hello Azure Stack operator's PowerShell environment](azure-stack-powershell-configure-admin.md) topic.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="158c4-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="158c4-106">Prerequisites</span></span> 

<span data-ttu-id="158c4-107">Запустите hello следующие необходимые компоненты из hello [пакет средств разработки](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), или из внешнего клиента Windows в случае [подключен через виртуальную частную сеть](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span><span class="sxs-lookup"><span data-stu-id="158c4-107">Run hello following prerequisites either from hello [development kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span></span>

* <span data-ttu-id="158c4-108">Установка [модули Azure PowerShell Azure стека совместимой](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="158c4-108">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>  
* <span data-ttu-id="158c4-109">Загрузите hello [toowork необходимые средства с Azure стека](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="158c4-109">Download hello [tools required toowork with Azure Stack](azure-stack-powershell-download.md).</span></span> 

## <a name="configure-hello-user-environment-and-sign-in-tooazure-stack"></a><span data-ttu-id="158c4-110">Настройка среды пользователя hello и вход tooAzure стека</span><span class="sxs-lookup"><span data-stu-id="158c4-110">Configure hello user environment and sign in tooAzure Stack</span></span>

<span data-ttu-id="158c4-111">В зависимости от типа развертывания (Azure AD или AD FS), выполните одну из следующих tooconfigure сценария PowerShell для Azure стека hello hello:</span><span class="sxs-lookup"><span data-stu-id="158c4-111">Based on hello type of deployment (Azure AD or AD FS), run one of hello following script tooconfigure PowerShell for Azure Stack:</span></span>

### <a name="azure-active-directory-aad-based-deployments"></a><span data-ttu-id="158c4-112">Azure Active Directory (AAD) на основе развертываний</span><span class="sxs-lookup"><span data-stu-id="158c4-112">Azure Active Directory (AAD) based deployments</span></span>
       
  ```powershell
  # Navigate toohello downloaded folder and import hello **Connect** PowerShell module
  Set-ExecutionPolicy RemoteSigned
  Import-Module .\Connect\AzureStack.Connect.psm1

  # Register an AzureRM environment that targets your Azure Stack instance
  Add-AzureRMEnvironment `
    -Name "AzureStackUser" `
    -ArmEndpoint "https://management.local.azurestack.external"

  # Set hello GraphEndpointResourceId value
  Set-AzureRmEnvironment `
    -Name "AzureStackUser" `
    -GraphAudience "https://graph.windows.net/"

  # Get hello Active Directory tenantId that is used toodeploy Azure Stack
  $TenantID = Get-AzsDirectoryTenantId `
    -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
    -EnvironmentName "AzureStackUser"

  # Sign in tooyour environment
  Login-AzureRmAccount `
    -EnvironmentName "AzureStackUser" `
    -TenantId $TenantID 
   ```

### <a name="active-directory-federation-services-ad-fs-based-deployments"></a><span data-ttu-id="158c4-113">Службы федерации Active Directory (AD FS) на основе развертываний</span><span class="sxs-lookup"><span data-stu-id="158c4-113">Active Directory Federation Services (AD FS) based deployments</span></span> 
          
  ```powershell
  # Navigate toohello downloaded folder and import hello **Connect** PowerShell module
  Set-ExecutionPolicy RemoteSigned
  Import-Module .\Connect\AzureStack.Connect.psm1

  # Register an AzureRM environment that targets your Azure Stack instance
  Add-AzureRMEnvironment `
    -Name "AzureStackUser" `
    -ArmEndpoint "https://management.local.azurestack.external"

  # Set hello GraphEndpointResourceId value
  Set-AzureRmEnvironment `
    -Name "AzureStackUser" `
    -GraphAudience "https://graph.local.azurestack.external/" `
    -EnableAdfsAuthentication:$true

  # Get hello Active Directory tenantId that is used toodeploy Azure Stack     
  $TenantID = Get-AzsDirectoryTenantId `
    -ADFS `
    -EnvironmentName "AzureStackUser"

  # Sign in tooyour environment
  Login-AzureRmAccount `
    -EnvironmentName "AzureStackUser" `
    -TenantId $TenantID 
  ```

## <a name="register-resource-providers"></a><span data-ttu-id="158c4-114">Регистрация поставщиков ресурсов</span><span class="sxs-lookup"><span data-stu-id="158c4-114">Register resource providers</span></span>

<span data-ttu-id="158c4-115">При работе на только что созданного пользователя подписку, которая не содержит все ресурсы, развертываемые через портал hello поставщиков ресурсов hello не регистрируются автоматически.</span><span class="sxs-lookup"><span data-stu-id="158c4-115">When operating on a newly created user subscription that doesn’t have any resources deployed through hello portal, hello resource providers aren't automatically registered.</span></span> <span data-ttu-id="158c4-116">Следует явным образом их необходимо зарегистрировать с помощью hello следующий скрипт:</span><span class="sxs-lookup"><span data-stu-id="158c4-116">You should explicitly register them by using hello following script:</span></span>

```powershell
foreach($s in (Get-AzureRmSubscription)) {
        Select-AzureRmSubscription -SubscriptionId $s.SubscriptionId | Out-Null
        Write-Progress $($s.SubscriptionId + " : " + $s.SubscriptionName)
Get-AzureRmResourceProvider -ListAvailable | Register-AzureRmResourceProvider -Force
    } 
```

## <a name="test-hello-connectivity"></a><span data-ttu-id="158c4-117">Проверка подключения hello</span><span class="sxs-lookup"><span data-stu-id="158c4-117">Test hello connectivity</span></span>

<span data-ttu-id="158c4-118">Теперь, когда у нас есть все настройки, воспользуемся PowerShell toocreate ресурсов в Azure стека.</span><span class="sxs-lookup"><span data-stu-id="158c4-118">Now that we've got everything set up, let's use PowerShell toocreate resources within Azure Stack.</span></span> <span data-ttu-id="158c4-119">Например можно создать группу ресурсов для приложения и добавить виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="158c4-119">For example, you can create a resource group for an application and add a virtual machine.</span></span> <span data-ttu-id="158c4-120">Hello используется следующая команда toocreate группу ресурсов с именем «MyResourceGroup»:</span><span class="sxs-lookup"><span data-stu-id="158c4-120">Use hello following command toocreate a resource group named "MyResourceGroup":</span></span>

```powershell
New-AzureRmResourceGroup -Name "MyResourceGroup" -Location "Local"
```

## <a name="next-steps"></a><span data-ttu-id="158c4-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="158c4-121">Next steps</span></span>
* [<span data-ttu-id="158c4-122">Разработка шаблонов для Azure Stack</span><span class="sxs-lookup"><span data-stu-id="158c4-122">Develop templates for Azure Stack</span></span>](azure-stack-develop-templates.md)
* [<span data-ttu-id="158c4-123">Развертывание шаблонов с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="158c4-123">Deploy templates with PowerShell</span></span>](azure-stack-deploy-template-powershell.md)
