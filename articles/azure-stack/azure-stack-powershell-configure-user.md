---
title: "Настройка среды PowerShell пользователя стек Azure | Документы Microsoft"
description: "Настройка среды PowerShell пользователя стек Azure"
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
ms.openlocfilehash: dabbd83fb35397f2cf90fac5957d299f0c5d446e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="configure-the-azure-stack-users-powershell-environment"></a><span data-ttu-id="a369d-103">Настройка среды PowerShell пользователя стек Azure</span><span class="sxs-lookup"><span data-stu-id="a369d-103">Configure the Azure Stack user's PowerShell environment</span></span>

<span data-ttu-id="a369d-104">Как пользователь с стек Azure можно настроить пакет средств Azure стека разработки среды PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a369d-104">As an Azure Stack user, you can configure your Azure Stack Development Kit's PowerShell environment.</span></span> <span data-ttu-id="a369d-105">После настройки, можно использовать PowerShell для управления Azure стека, ресурсы, такие как подписаться на предложения, создания виртуальных машин, развернуть шаблоны Azure Resource Manager и т. д. В этом разделе предназначена для использования с этим пользователем, в средах, если вы хотите настроить PowerShell оператор к облачной среде относятся только к [настройки среды PowerShell оператор стек Azure](azure-stack-powershell-configure-admin.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="a369d-105">After you configure, you can use PowerShell to manage Azure Stack resources such as subscribe to offers, create virtual machines, deploy Azure Resource Manager templates,  etc. This topic is scoped to use with the user environments only, if you want to set up PowerShell for the cloud operator environment, refer to the [Configure the Azure Stack operator's PowerShell environment](azure-stack-powershell-configure-admin.md) topic.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a369d-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a369d-106">Prerequisites</span></span> 

<span data-ttu-id="a369d-107">Выполнить следующие предварительные требования, либо из [пакет средств разработки](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), или из внешнего клиента Windows в случае [подключен через виртуальную частную сеть](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span><span class="sxs-lookup"><span data-stu-id="a369d-107">Run the following prerequisites either from the [development kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span></span>

* <span data-ttu-id="a369d-108">Установка [модули Azure PowerShell Azure стека совместимой](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="a369d-108">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>  
* <span data-ttu-id="a369d-109">Загрузить [инструменты, необходимые для работы с Azure стека](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="a369d-109">Download the [tools required to work with Azure Stack](azure-stack-powershell-download.md).</span></span> 

## <a name="configure-the-user-environment-and-sign-in-to-azure-stack"></a><span data-ttu-id="a369d-110">Настройка среды пользователя и войти в стек Azure</span><span class="sxs-lookup"><span data-stu-id="a369d-110">Configure the user environment and sign in to Azure Stack</span></span>

<span data-ttu-id="a369d-111">В зависимости от типа развертывания (Azure AD или AD FS), выполните одну из следующий скрипт, чтобы настроить PowerShell для Azure стека:</span><span class="sxs-lookup"><span data-stu-id="a369d-111">Based on the type of deployment (Azure AD or AD FS), run one of the following script to configure PowerShell for Azure Stack:</span></span>

### <a name="azure-active-directory-aad-based-deployments"></a><span data-ttu-id="a369d-112">Azure Active Directory (AAD) на основе развертываний</span><span class="sxs-lookup"><span data-stu-id="a369d-112">Azure Active Directory (AAD) based deployments</span></span>
       
  ```powershell
  # Navigate to the downloaded folder and import the **Connect** PowerShell module
  Set-ExecutionPolicy RemoteSigned
  Import-Module .\Connect\AzureStack.Connect.psm1

  # Register an AzureRM environment that targets your Azure Stack instance
  Add-AzureRMEnvironment `
    -Name "AzureStackUser" `
    -ArmEndpoint "https://management.local.azurestack.external"

  # Set the GraphEndpointResourceId value
  Set-AzureRmEnvironment `
    -Name "AzureStackUser" `
    -GraphAudience "https://graph.windows.net/"

  # Get the Active Directory tenantId that is used to deploy Azure Stack
  $TenantID = Get-AzsDirectoryTenantId `
    -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
    -EnvironmentName "AzureStackUser"

  # Sign in to your environment
  Login-AzureRmAccount `
    -EnvironmentName "AzureStackUser" `
    -TenantId $TenantID 
   ```

### <a name="active-directory-federation-services-ad-fs-based-deployments"></a><span data-ttu-id="a369d-113">Службы федерации Active Directory (AD FS) на основе развертываний</span><span class="sxs-lookup"><span data-stu-id="a369d-113">Active Directory Federation Services (AD FS) based deployments</span></span> 
          
  ```powershell
  # Navigate to the downloaded folder and import the **Connect** PowerShell module
  Set-ExecutionPolicy RemoteSigned
  Import-Module .\Connect\AzureStack.Connect.psm1

  # Register an AzureRM environment that targets your Azure Stack instance
  Add-AzureRMEnvironment `
    -Name "AzureStackUser" `
    -ArmEndpoint "https://management.local.azurestack.external"

  # Set the GraphEndpointResourceId value
  Set-AzureRmEnvironment `
    -Name "AzureStackUser" `
    -GraphAudience "https://graph.local.azurestack.external/" `
    -EnableAdfsAuthentication:$true

  # Get the Active Directory tenantId that is used to deploy Azure Stack     
  $TenantID = Get-AzsDirectoryTenantId `
    -ADFS `
    -EnvironmentName "AzureStackUser"

  # Sign in to your environment
  Login-AzureRmAccount `
    -EnvironmentName "AzureStackUser" `
    -TenantId $TenantID 
  ```

## <a name="register-resource-providers"></a><span data-ttu-id="a369d-114">Регистрация поставщиков ресурсов</span><span class="sxs-lookup"><span data-stu-id="a369d-114">Register resource providers</span></span>

<span data-ttu-id="a369d-115">При работе на только что созданного пользователя подписку, которая не содержит все ресурсы, развертываемые на портале поставщиков ресурсов не регистрируются автоматически.</span><span class="sxs-lookup"><span data-stu-id="a369d-115">When operating on a newly created user subscription that doesn’t have any resources deployed through the portal, the resource providers aren't automatically registered.</span></span> <span data-ttu-id="a369d-116">Следует явно регистрировать их с помощью следующего сценария:</span><span class="sxs-lookup"><span data-stu-id="a369d-116">You should explicitly register them by using the following script:</span></span>

```powershell
foreach($s in (Get-AzureRmSubscription)) {
        Select-AzureRmSubscription -SubscriptionId $s.SubscriptionId | Out-Null
        Write-Progress $($s.SubscriptionId + " : " + $s.SubscriptionName)
Get-AzureRmResourceProvider -ListAvailable | Register-AzureRmResourceProvider -Force
    } 
```

## <a name="test-the-connectivity"></a><span data-ttu-id="a369d-117">Проверка подключения</span><span class="sxs-lookup"><span data-stu-id="a369d-117">Test the connectivity</span></span>

<span data-ttu-id="a369d-118">Теперь, когда у нас есть все настройки, воспользуемся PowerShell для создания ресурсов в Azure стека.</span><span class="sxs-lookup"><span data-stu-id="a369d-118">Now that we've got everything set up, let's use PowerShell to create resources within Azure Stack.</span></span> <span data-ttu-id="a369d-119">Например можно создать группу ресурсов для приложения и добавить виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="a369d-119">For example, you can create a resource group for an application and add a virtual machine.</span></span> <span data-ttu-id="a369d-120">Создать группу ресурсов с именем «MyResourceGroup», используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a369d-120">Use the following command to create a resource group named "MyResourceGroup":</span></span>

```powershell
New-AzureRmResourceGroup -Name "MyResourceGroup" -Location "Local"
```

## <a name="next-steps"></a><span data-ttu-id="a369d-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a369d-121">Next steps</span></span>
* [<span data-ttu-id="a369d-122">Разработка шаблонов для Azure Stack</span><span class="sxs-lookup"><span data-stu-id="a369d-122">Develop templates for Azure Stack</span></span>](azure-stack-develop-templates.md)
* [<span data-ttu-id="a369d-123">Развертывание шаблонов с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="a369d-123">Deploy templates with PowerShell</span></span>](azure-stack-deploy-template-powershell.md)
