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
# <a name="configure-the-azure-stack-users-powershell-environment"></a>Настройка среды PowerShell пользователя стек Azure

Как пользователь с стек Azure можно настроить пакет средств Azure стека разработки среды PowerShell. После настройки, можно использовать PowerShell для управления Azure стека, ресурсы, такие как подписаться на предложения, создания виртуальных машин, развернуть шаблоны Azure Resource Manager и т. д. В этом разделе предназначена для использования с этим пользователем, в средах, если вы хотите настроить PowerShell оператор к облачной среде относятся только к [настройки среды PowerShell оператор стек Azure](azure-stack-powershell-configure-admin.md) раздела. 

## <a name="prerequisites"></a>Предварительные требования 

Выполнить следующие предварительные требования, либо из [пакет средств разработки](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), или из внешнего клиента Windows в случае [подключен через виртуальную частную сеть](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):

* Установка [модули Azure PowerShell Azure стека совместимой](azure-stack-powershell-install.md).  
* Загрузить [инструменты, необходимые для работы с Azure стека](azure-stack-powershell-download.md). 

## <a name="configure-the-user-environment-and-sign-in-to-azure-stack"></a>Настройка среды пользователя и войти в стек Azure

В зависимости от типа развертывания (Azure AD или AD FS), выполните одну из следующий скрипт, чтобы настроить PowerShell для Azure стека:

### <a name="azure-active-directory-aad-based-deployments"></a>Azure Active Directory (AAD) на основе развертываний
       
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

### <a name="active-directory-federation-services-ad-fs-based-deployments"></a>Службы федерации Active Directory (AD FS) на основе развертываний 
          
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

## <a name="register-resource-providers"></a>Регистрация поставщиков ресурсов

При работе на только что созданного пользователя подписку, которая не содержит все ресурсы, развертываемые на портале поставщиков ресурсов не регистрируются автоматически. Следует явно регистрировать их с помощью следующего сценария:

```powershell
foreach($s in (Get-AzureRmSubscription)) {
        Select-AzureRmSubscription -SubscriptionId $s.SubscriptionId | Out-Null
        Write-Progress $($s.SubscriptionId + " : " + $s.SubscriptionName)
Get-AzureRmResourceProvider -ListAvailable | Register-AzureRmResourceProvider -Force
    } 
```

## <a name="test-the-connectivity"></a>Проверка подключения

Теперь, когда у нас есть все настройки, воспользуемся PowerShell для создания ресурсов в Azure стека. Например можно создать группу ресурсов для приложения и добавить виртуальную машину. Создать группу ресурсов с именем «MyResourceGroup», используйте следующую команду:

```powershell
New-AzureRmResourceGroup -Name "MyResourceGroup" -Location "Local"
```

## <a name="next-steps"></a>Дальнейшие действия
* [Разработка шаблонов для Azure Stack](azure-stack-develop-templates.md)
* [Развертывание шаблонов с помощью PowerShell](azure-stack-deploy-template-powershell.md)
