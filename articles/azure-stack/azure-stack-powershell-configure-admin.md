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
# <a name="configure-hello-azure-stack-operators-powershell-environment"></a>Настройка среды PowerShell оператор hello стек Azure

Как оператор стек Azure можно настроить пакет средств Azure стека разработки среды PowerShell. После настройки, можно использовать PowerShell toomanage стек Azure ресурсов, таких как создание предложений, планы, квот, управление, предупреждения и т. д. Этот раздел является областью toouse оператором hello облачных средах, если требуется tooset копирование PowerShell для среды пользователя hello, относятся только слишком[настройки среды PowerShell hello Azure стека пользователя](azure-stack-powershell-configure-user.md) раздела. 

## <a name="prerequisites"></a>Предварительные требования

Запустите hello следующие необходимые компоненты из hello [пакет средств разработки](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), или из внешнего клиента Windows в случае [подключен через виртуальную частную сеть](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn): 

* Установка [модули Azure PowerShell Azure стека совместимой](azure-stack-powershell-install.md).  
* Загрузите hello [toowork необходимые средства с Azure стека](azure-stack-powershell-download.md).  

## <a name="configure-hello-operator-environment-and-sign-in-tooazure-stack"></a>Настройка среды оператор hello и вход tooAzure стека

В зависимости от типа hello развертывания (Azure AD или AD FS), выполните одну из hello, выполнив сценарий tooconfigure hello Azure стека оператор среды с помощью PowerShell:

### <a name="azure-active-directory-aad-based-deployments"></a>Azure Active Directory (AAD) на основе развертываний
       
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

### <a name="active-directory-federation-services-ad-fs-based-deployments"></a>Службы федерации Active Directory (AD FS) на основе развертываний
         
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

## <a name="test-hello-connectivity"></a>Проверка подключения hello

Теперь, когда у нас есть все настройки, воспользуемся PowerShell toocreate ресурсов в Azure стека. Например можно создать группу ресурсов для приложения и добавить виртуальную машину. Hello используется следующая команда toocreate группу ресурсов с именем «MyResourceGroup»:

```powershell
New-AzureRmResourceGroup -Name "MyResourceGroup" -Location "Local"
```

## <a name="next-steps"></a>Дальнейшие действия
* [Разработка шаблонов для Azure Stack](azure-stack-develop-templates.md)
* [Развертывание шаблонов с помощью PowerShell](azure-stack-deploy-template-powershell.md)