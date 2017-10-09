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
# <a name="configure-hello-azure-stack-users-powershell-environment"></a>Настройка среды PowerShell hello Azure стека пользователя

Как пользователь с стек Azure можно настроить пакет средств Azure стека разработки среды PowerShell. После настройки, можно использовать PowerShell toomanage стека Azure ресурсов, таких как подписаться toooffers, создания виртуальных машин, развертывание шаблонов диспетчера ресурсов Azure и т. д. В этом разделе с областью toouse с hello пользовательских сред, следует tooset копирование PowerShell для hello облачной среде оператор обратитесь toohello [настройки среды PowerShell hello Azure стека оператор](azure-stack-powershell-configure-admin.md) раздела. 

## <a name="prerequisites"></a>Предварительные требования 

Запустите hello следующие необходимые компоненты из hello [пакет средств разработки](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), или из внешнего клиента Windows в случае [подключен через виртуальную частную сеть](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):

* Установка [модули Azure PowerShell Azure стека совместимой](azure-stack-powershell-install.md).  
* Загрузите hello [toowork необходимые средства с Azure стека](azure-stack-powershell-download.md). 

## <a name="configure-hello-user-environment-and-sign-in-tooazure-stack"></a>Настройка среды пользователя hello и вход tooAzure стека

В зависимости от типа развертывания (Azure AD или AD FS), выполните одну из следующих tooconfigure сценария PowerShell для Azure стека hello hello:

### <a name="azure-active-directory-aad-based-deployments"></a>Azure Active Directory (AAD) на основе развертываний
       
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

### <a name="active-directory-federation-services-ad-fs-based-deployments"></a>Службы федерации Active Directory (AD FS) на основе развертываний 
          
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

## <a name="register-resource-providers"></a>Регистрация поставщиков ресурсов

При работе на только что созданного пользователя подписку, которая не содержит все ресурсы, развертываемые через портал hello поставщиков ресурсов hello не регистрируются автоматически. Следует явным образом их необходимо зарегистрировать с помощью hello следующий скрипт:

```powershell
foreach($s in (Get-AzureRmSubscription)) {
        Select-AzureRmSubscription -SubscriptionId $s.SubscriptionId | Out-Null
        Write-Progress $($s.SubscriptionId + " : " + $s.SubscriptionName)
Get-AzureRmResourceProvider -ListAvailable | Register-AzureRmResourceProvider -Force
    } 
```

## <a name="test-hello-connectivity"></a>Проверка подключения hello

Теперь, когда у нас есть все настройки, воспользуемся PowerShell toocreate ресурсов в Azure стека. Например можно создать группу ресурсов для приложения и добавить виртуальную машину. Hello используется следующая команда toocreate группу ресурсов с именем «MyResourceGroup»:

```powershell
New-AzureRmResourceGroup -Name "MyResourceGroup" -Location "Local"
```

## <a name="next-steps"></a>Дальнейшие действия
* [Разработка шаблонов для Azure Stack](azure-stack-develop-templates.md)
* [Развертывание шаблонов с помощью PowerShell](azure-stack-deploy-template-powershell.md)
