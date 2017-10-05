---
title: "Настройка для использования со стеком Azure PowerShell | Документы Microsoft"
description: "Подробные сведения о настройке PowerShell для Azure стека."
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
ms.date: 07/16/2017
ms.author: sngun
ms.openlocfilehash: 3c6fc6af0588ae2e796d50f2d7bfdafaea81e2a1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="configure-powershell-for-use-with-azure-stack"></a>Настройка PowerShell для использования с стек Azure 

В этой статье описаны шаги, необходимые для подключения к экземпляру пакет средств разработки Azure стека с помощью PowerShell. После подключения вы доступ к порталу и развертывать ресурсы с помощью PowerShell. Можно использовать действия, описанные в этой статье из пакета средств разработки, либо от внешнего клиента на основе Windows при подключении через виртуальную частную сеть.

В этой статье содержатся подробные инструкции по настройке PowerShell для Azure стека. Тем не менее, если вы хотите быстро установить и настроить PowerShell, можно использовать сценарий, приведенный в [приступить к работе с PowerShell](azure-stack-powershell-configure-quickstart.md) раздела. 

## <a name="prerequisites"></a>Предварительные требования
* Установка [модули Azure PowerShell Azure стека совместимой](azure-stack-powershell-install.md).  
* Загрузить [инструменты, необходимые для работы с Azure стека](azure-stack-powershell-download.md).  

## <a name="import-the-connect-powershell-module"></a>Импортируйте модуль PowerShell для подключения

После загрузки необходимых средств, перейдите в папку загруженные и импортировать **Connect** модуля PowerShell. Чтобы импортировать модуль Connect, выполните следующую команду в сеансе PowerShell с повышенными привилегиями:

```PowerShell
Set-ExecutionPolicy RemoteSigned
Import-Module .\Connect\AzureStack.Connect.psm1
```

## <a name="configure-the-powershell-environment"></a>Настройка среды PowerShell

Чтобы настроить среду стека Azure, выполните следующее:

1. Зарегистрируйте AzureRM среду, которая обращается экземпляр стек Azure с помощью одного из следующих командлетов:

   * **Облачной среде администрирования**

       ```PowerShell
       Add-AzureRMEnvironment `
         -Name "AzureStackAdmin" `
         -ArmEndpoint "https://adminmanagement.local.azurestack.external"
       ```

   * **Среды пользователя**

       ```PowerShell
       Add-AzureRMEnvironment `
         -Name "AzureStackUser" `
         -ArmEndpoint "https://management.local.azurestack.external" 
       ```
   
   После зарегистрировались AzureRM среды, можно использовать все командлеты AzureRM в вашей среде Azure стека. На следующем снимке экрана показан результат предыдущего выполнения командлета:

   ![Получение сведений о среде](media/azure-stack-powershell-configure/getenvdetails.png)

2. Установите значение GraphEndpointResourceId с помощью одного из следующих командлетов:
   
   * **Azure Active Directory (Azure AD)**
   
      * Для **облачной среде администрирования**, используйте:
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackAdmin" `
          -GraphAudience "https://graph.windows.net/"
        ```
        
      * Для **среды пользователя**, используйте:
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackUser" `
          -GraphAudience "https://graph.windows.net/"
        ```

   * **Службы федерации Active Directory**
   
      * Для **облачной среде администрирования**, используйте:
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackAdmin" `
          -GraphAudience "https://graph.local.azurestack.external/" `
          -EnableAdfsAuthentication:$true
        ```
        
      * Для **среды пользователя**, используйте:
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackUser" `
          -GraphAudience "https://graph.local.azurestack.external/" `
          -EnableAdfsAuthentication:$true
        ```

3. Получите значение идентификатора GUID для клиента Active Directory, который используется для развертывания Azure стека. Если среду стека Azure развертывается с помощью:  

   * **Azure Active Directory (Azure AD)**
   
      * Чтобы получить доступ к **облачной среде администрирования**, используйте:
        ```PowerShell
        $TenantID = Get-AzsDirectoryTenantId `
          -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
          -EnvironmentName "AzureStackAdmin"
        ```

      * Чтобы получить доступ к **среды пользователя**, используйте:
        ```PowerShell
        $TenantID = Get-AzsDirectoryTenantId `
          -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
          -EnvironmentName "AzureStackUser"
        ```

   * **Службы федерации Active Directory**
   
      * Чтобы получить доступ к **облачной среде администрирования**, используйте:
        ```PowerShell
        $TenantID = Get-AzsDirectoryTenantId `
          -ADFS `
          -EnvironmentName "AzureStackAdmin"
        ```

      * Чтобы получить доступ к **среды пользователя**, используйте:
        ```PowerShell 
        $TenantID = Get-AzsDirectoryTenantId `
          -ADFS `
          -EnvironmentName "AzureStackUser" 
        ```

## <a name="sign-in-to-azure-stack"></a>Войдите в стек Azure

Войдите в среду Azure стека с помощью одного из двух следующих командлетов:

   * Для входа в **административный портал**, используйте:
    
       ```PowerShell
       Login-AzureRmAccount `
         -EnvironmentName "AzureStackAdmin" `
         -TenantId $TenantID 
       ```

   * Для входа в **пользовательского портала**, используйте:

       ```PowerShell
       Login-AzureRmAccount `
         -EnvironmentName "AzureStackUser" `
         -TenantId $TenantID 
       ```

## <a name="register-resource-providers"></a>Регистрация поставщиков ресурсов

После входа на портал администратора или пользователя, можно выполнять операции с зарегистрированных поставщиков. По умолчанию все поставщики ресурсов фундаментальные регистрируются в подписки поставщика по умолчанию (администратору облака подписка).

При работе с только что созданного пользователя подписки, при которой не содержит все ресурсы, развертываемые на портале, автоматически не зарегистрированы поставщиков ресурсов. Следует явно регистрировать поставщики ресурсов с помощью следующего сценария:

```powershell

foreach($s in (Get-AzureRmSubscription)) {
        Select-AzureRmSubscription -SubscriptionId $s.SubscriptionId | Out-Null
        Write-Progress $($s.SubscriptionId + " : " + $s.SubscriptionName)
Get-AzureRmResourceProvider -ListAvailable | Register-AzureRmResourceProvider -Force
    } 
```


## <a name="next-steps"></a>Дальнейшие действия
* [Разработка шаблонов для Azure Stack](azure-stack-develop-templates.md)
* [Развертывание шаблонов с помощью PowerShell](azure-stack-deploy-template-powershell.md)
