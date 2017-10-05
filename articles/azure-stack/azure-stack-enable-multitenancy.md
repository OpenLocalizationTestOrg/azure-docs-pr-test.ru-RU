---
title: "Разрешить Многопользовательские приложения в Azure стек | Документы Microsoft"
description: "Узнайте, как для поддержки нескольких каталогов Azure Active Directory в стек Azure"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: helaw
ms.openlocfilehash: ed1d9d20c06ea0478a439775020fd35941b3d640
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="enable-multi-tenancy-in-azure-stack"></a>Разрешить Многопользовательские приложения в стек Azure

Вы можете настроить стек Azure для поддержки пользователей из нескольких клиентов Azure Active Directory (Azure AD) для использования служб в Azure стека. Например рассмотрим следующий сценарий:

 - Вы являетесь администратором службы из contoso.onmicrosoft.com, установленным Azure стека.
 - Мэри является администратором каталога fabrikam.onmicrosoft.com, где расположены гостевых пользователей. 
 - Мэри компании получает служб IaaS и PaaS из компании и необходимо разрешить пользователям из каталога гостя (fabrikam.onmicrosoft.com) войти и использовать ресурсы Azure стека в contoso.onmicrosoft.com.

Здесь приведены шаги, в контексте этого сценария для настройки Многопользовательские приложения Azure стека.  В этом случае вы и Мэри необходимо выполнить действия, чтобы разрешить пользователям из компании Fabrikam, выполнить вход и использовать службы из развертывания Azure стека в компании Contoso.  

## <a name="before-you-begin"></a>Перед началом работы
Существует несколько необходимых компонентов для учета перед настройкой Многопользовательские приложения Azure стека:
  
 - Вы и Мэри необходимо координировать административные действия в каталог, который в (Contoso), устанавливается стек Azure и каталог гостя (Fabrikam).  
 - Убедитесь, что вы уже [установлен](azure-stack-powershell-install.md) и [настроен](azure-stack-powershell-configure-admin.md) PowerShell для Azure стека.
 - [Загрузите средства Azure стека](azure-stack-powershell-download.md)и импортируйте модули Connect и удостоверений:

    ````PowerShell
        Import-Module .\Connect\AzureStack.Connect.psm1
        Import-Module .\Identity\AzureStack.Identity.psm1
    ```` 
 - Потребуется Mary [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) доступ к Azure стека. 

## <a name="configure-azure-stack-directory"></a>Настроить каталог стек Azure
В этом разделе Настройте стек Azure позволяет войти в систему от клиентов directory Fabrikam Azure AD.

### <a name="onboard-guest-directory-tenant"></a>Встроенный гостевой каталог клиента
Далее, встроенный клиент каталога гостя (Fabrikam) в стек Azure.  Этот шаг позволяет настроить Azure Resource Manager для принятия пользователи и участники службы из клиента каталога гостя.

````PowerShell
$adminARMEndpoint = "https://adminmanagement.local.azurestack.external"

## Replace the value below with the Azure Stack directory
$azureStackDirectoryTenant = "contoso.onmicrosoft.com"

## Replace the value below with the guest tenant directory. 
$guestDirectoryTenantToBeOnboarded = "fabrikam.onmicrosoft.com"

Register-AzSGuestDirectoryTenant -AdminResourceManagerEndpoint $adminARMEndpoint `
 -DirectoryTenantName $azureStackDirectoryTenant `
 -GuestDirectoryTenantName $guestDirectoryTenantToBeOnboarded `
 -Location "local"
````



## <a name="configure-guest-directory"></a>Настройка каталога гостя
После выполнения шагов в каталоге Azure стека, Мэри необходимо дать согласие на доступ к каталогу гостевой стек Azure и Azure стеком регистров с каталогом гостевой. 

### <a name="registering-azure-stack-with-the-guest-directory"></a>Регистрация в каталоге гостевой стек Azure
После гостевой directory администратор предоставил разрешения для стека Azure для доступа к каталогу компании Fabrikam, их необходимо зарегистрировать Azure стека клиента каталога компании Fabrikam.

````PowerShell
$tenantARMEndpoint = "https://management.local.azurestack.external"
    
## Replace the value below with the guest tenant directory. 
$guestDirectoryTenantName = "fabrikam.onmicrosoft.com"

Register-AzSWithMyDirectoryTenant `
 -TenantResourceManagerEndpoint $tenantARMEndpoint `
 -DirectoryTenantName $guestDirectoryTenantName ` 
 -Verbose 
````
## <a name="direct-users-to-sign-in"></a>Предоставить пользователям вход
Теперь, когда вы и Мэри шаги по встроенным Мэри каталог, Мэри могут направлять пользователей Fabrikam вход.  Вход пользователей Fabrikam (то есть, пользователи с суффиксом fabrikam.onmicrosoft.com), перейдя по адресу https://portal.local.azurestack.external.  

Мария будет направлять все [внешних участников](../active-directory/active-directory-understanding-resource-access.md) в каталоге компании Fabrikam (то есть, пользователи в каталоге Fabrikam без суффикса fabrikam.onmicrosoft.com) выполнить вход с использованием https://portal.local.azurestack.external/fabrikam.onmicrosoft.com.  Если они не используют этот URL-адрес, они отправляются их каталог по умолчанию (Fabrikam) и происходит ошибка, о том, что не согласился своему администратору.

## <a name="next-steps"></a>Дальнейшие действия

- [Управление поставщиками делегированные](azure-stack-delegated-provider.md)
- [Основные понятия Azure стека](azure-stack-key-features.md)
