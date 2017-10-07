---
title: "aaaConfigure PowerShell для использования со стеком Azure | Документы Microsoft"
description: "Узнайте, как tooconfigure PowerShell для Azure стека."
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
ms.openlocfilehash: bc40869abe453cef4854daaf11605efd94a66c99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-powershell-for-use-with-azure-stack"></a>Настройка PowerShell для использования с стек Azure 

Данная статья содержит hello действия требуется tooconnect tooan пакет средств разработки Azure стека экземпляра с помощью PowerShell. После подключения можно получить доступ к порталу hello и развертывать ресурсы с помощью PowerShell. Можно использовать hello действия, описанные в этой статье из пакета средств разработки hello или из внешнего клиента на основе Windows, при подключении через виртуальную частную сеть.

В этой статье содержатся подробные инструкции по tooconfigure PowerShell для Azure стека. Тем не менее, если tooquickly установку и настройте PowerShell, можно использовать сценарий hello в hello [приступить к работе с PowerShell](azure-stack-powershell-configure-quickstart.md) раздела. 

## <a name="prerequisites"></a>Предварительные требования
* Установка [модули Azure PowerShell Azure стека совместимой](azure-stack-powershell-install.md).  
* Загрузите hello [toowork необходимые средства с Azure стека](azure-stack-powershell-download.md).  

## <a name="import-hello-connect-powershell-module"></a>Модуль Connect PowerShell hello импорта

После загрузки hello необходимые средства, перейдите в папку toohello загрузить и импортировать hello **Connect** модуля PowerShell. tooimport hello модуля Connect, запустите следующую команду в сеансе PowerShell с повышенными привилегиями hello:

```PowerShell
Set-ExecutionPolicy RemoteSigned
Import-Module .\Connect\AzureStack.Connect.psm1
```

## <a name="configure-hello-powershell-environment"></a>Настройка среды PowerShell hello

tooconfigure среды стека Azure hello следующие:

1. Зарегистрируйте AzureRM среду, которая обращается экземпляр стек Azure с помощью одного из следующих командлетов hello:

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
   
   После зарегистрировались среды AzureRM hello, можно использовать все командлеты AzureRM hello в вашей среде Azure стека. выходные данные Hello Предыдущий командлет hello показан следующий снимок экрана приветствия:

   ![Получение сведений о среде](media/azure-stack-powershell-configure/getenvdetails.png)

2. Установите значение hello GraphEndpointResourceId с помощью одного из следующих командлетов hello:
   
   * **Azure Active Directory (Azure AD)**
   
      * Для hello **облачной среде администрирования**, используйте:
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackAdmin" `
          -GraphAudience "https://graph.windows.net/"
        ```
        
      * Для hello **среды пользователя**, используйте:
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackUser" `
          -GraphAudience "https://graph.windows.net/"
        ```

   * **Службы федерации Active Directory**
   
      * Для hello **облачной среде администрирования**, используйте:
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackAdmin" `
          -GraphAudience "https://graph.local.azurestack.external/" `
          -EnableAdfsAuthentication:$true
        ```
        
      * Для hello **среды пользователя**, используйте:
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackUser" `
          -GraphAudience "https://graph.local.azurestack.external/" `
          -EnableAdfsAuthentication:$true
        ```

3. Получает значение идентификатора GUID hello hello клиента Active Directory, используемые toodeploy стека Azure. Если среду стека Azure развертывается с помощью:  

   * **Azure Active Directory (Azure AD)**
   
      * tooaccess hello **облачной среде администрирования**, используйте:
        ```PowerShell
        $TenantID = Get-AzsDirectoryTenantId `
          -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
          -EnvironmentName "AzureStackAdmin"
        ```

      * tooaccess hello **среды пользователя**, используйте:
        ```PowerShell
        $TenantID = Get-AzsDirectoryTenantId `
          -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
          -EnvironmentName "AzureStackUser"
        ```

   * **Службы федерации Active Directory**
   
      * tooaccess hello **облачной среде администрирования**, используйте:
        ```PowerShell
        $TenantID = Get-AzsDirectoryTenantId `
          -ADFS `
          -EnvironmentName "AzureStackAdmin"
        ```

      * tooaccess hello **среды пользователя**, используйте:
        ```PowerShell 
        $TenantID = Get-AzsDirectoryTenantId `
          -ADFS `
          -EnvironmentName "AzureStackUser" 
        ```

## <a name="sign-in-tooazure-stack"></a>Войдите в tooAzure стека

Войдите в toohello среду стека Azure с помощью одного из следующих двух командлетов hello:

   * toosign в toohello **административный портал**, используйте:
    
       ```PowerShell
       Login-AzureRmAccount `
         -EnvironmentName "AzureStackAdmin" `
         -TenantId $TenantID 
       ```

   * toosign в toohello **пользовательского портала**, используйте:

       ```PowerShell
       Login-AzureRmAccount `
         -EnvironmentName "AzureStackUser" `
         -TenantId $TenantID 
       ```

## <a name="register-resource-providers"></a>Регистрация поставщиков ресурсов

После входа в toohello портал администратора или пользователя, можно выполнять операции с hello зарегистрированных поставщиков ресурсов. По умолчанию все поставщики ресурсов фундаментальные hello регистрируются в hello подписки поставщика по умолчанию (администратор облака hello подписка).

При работе с только что созданного пользователя подписки, при которой не содержит все ресурсы, развертываемые через портал hello, автоматически не зарегистрированы hello поставщиков ресурсов. Следует явно регистрировать hello поставщиков ресурсов с помощью hello следующий скрипт:

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
