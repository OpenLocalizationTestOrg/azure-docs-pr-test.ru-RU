---
title: "Многопользовательские приложения aaaEnable в стек Azure | Документы Microsoft"
description: "Узнайте, как toosupport нескольких каталогов Azure Active Directory в стек Azure"
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
ms.openlocfilehash: d7e404894a65f6786c42c5c27f76d46f353cb8c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-multi-tenancy-in-azure-stack"></a>Разрешить Многопользовательские приложения в стек Azure

Стек Azure toosupport пользователей из нескольких служб toouse клиентов Azure Active Directory (Azure AD) можно настроить в стек Azure. Например рассмотрим следующие сценарии hello.

 - Есть hello администратора службы из contoso.onmicrosoft.com, где установлена стек Azure.
 - Мария — hello администратор каталога fabrikam.onmicrosoft.com, где расположены гостевых пользователей. 
 - Мэри компании получает служб IaaS и PaaS из вашей организации и требуется tooallow пользователям toosign каталога (fabrikam.onmicrosoft.com) гостевой hello в и использовать ресурсы Azure стека в contoso.onmicrosoft.com.

Это руководство предоставляет hello действия требуются в контексте hello этого сценария tooconfigure Многопользовательские приложения в Azure стека.  В этом сценарии вы и Мария выполните действия tooenable пользователи из компании Fabrikam toosign в и использовать службы из hello развертывания Azure стека в компании Contoso.  

## <a name="before-you-begin"></a>Перед началом работы
Существует несколько tooaccount предварительных требований для перед настройкой Многопользовательские приложения Azure стека:
  
 - Вы Мэри необходимо координировать административные действия между обоих стек Azure установлен в (Contoso) каталог hello и hello каталога гостя (Fabrikam).  
 - Убедитесь, что вы уже [установлен](azure-stack-powershell-install.md) и [настроен](azure-stack-powershell-configure-admin.md) PowerShell для Azure стека.
 - [Загрузить средства стека hello Azure](azure-stack-powershell-download.md)и импортируйте модули hello Connect и удостоверений:

    ````PowerShell
        Import-Module .\Connect\AzureStack.Connect.psm1
        Import-Module .\Identity\AzureStack.Identity.psm1
    ```` 
 - Потребуется Mary [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) доступ к tooAzure стека. 

## <a name="configure-azure-stack-directory"></a>Настроить каталог стек Azure
В этом разделе Настройте стек Azure tooallow входа в систему от клиентов directory Fabrikam Azure AD.

### <a name="onboard-guest-directory-tenant"></a>Встроенный гостевой каталог клиента
Далее, встроенный hello tooAzure клиента каталога гостя (Fabrikam) стека.  Этот шаг позволяет настроить диспетчера ресурсов Azure tooaccept пользователи и участники службы из клиента каталога гостя hello.

````PowerShell
$adminARMEndpoint = "https://adminmanagement.local.azurestack.external"

## Replace hello value below with hello Azure Stack directory
$azureStackDirectoryTenant = "contoso.onmicrosoft.com"

## Replace hello value below with hello guest tenant directory. 
$guestDirectoryTenantToBeOnboarded = "fabrikam.onmicrosoft.com"

Register-AzSGuestDirectoryTenant -AdminResourceManagerEndpoint $adminARMEndpoint `
 -DirectoryTenantName $azureStackDirectoryTenant `
 -GuestDirectoryTenantName $guestDirectoryTenantToBeOnboarded `
 -Location "local"
````



## <a name="configure-guest-directory"></a>Настройка каталога гостя
После выполнения шагов в каталоге Azure стека hello, Мэри необходимо указать согласия tooAzure стека доступ к hello гостевой directory и Azure стеком регистров с каталогом гостевой hello. 

### <a name="registering-azure-stack-with-hello-guest-directory"></a>Регистрация стек Azure directory гостевой hello
После hello гостевой directory администратор предоставил согласие для каталога Azure стека tooaccess Fabrikam, их необходимо зарегистрировать Azure стека клиента каталога компании Fabrikam.

````PowerShell
$tenantARMEndpoint = "https://management.local.azurestack.external"
    
## Replace hello value below with hello guest tenant directory. 
$guestDirectoryTenantName = "fabrikam.onmicrosoft.com"

Register-AzSWithMyDirectoryTenant `
 -TenantResourceManagerEndpoint $tenantARMEndpoint `
 -DirectoryTenantName $guestDirectoryTenantName ` 
 -Verbose 
````
## <a name="direct-users-toosign-in"></a>Предоставить пользователям toosign в
Вы и Мэри после завершения hello действия tooonboard Мэри каталога, Мэри можно направить toosign пользователей Fabrikam в.  Fabrikam пользователей (то есть с суффиксом hello fabrikam.onmicrosoft.com), перейдя по адресу https://portal.local.azurestack.external вход.  

Мария будет направлять все [внешних участников](../active-directory/active-directory-understanding-resource-access.md) в toosign каталога (то есть пользователей в каталог Fabrikam hello без суффикса hello fabrikam.onmicrosoft.com) Fabrikam hello в с помощью https://portal.local.azurestack.external/fabrikam.onmicrosoft.com.  Если они не используют этот URL-адрес, они отправляются tootheir каталог по умолчанию (Fabrikam) и происходит ошибка, о том, что не согласился своему администратору.

## <a name="next-steps"></a>Дальнейшие действия

- [Управление поставщиками делегированные](azure-stack-delegated-provider.md)
- [Основные понятия Azure стека](azure-stack-key-features.md)
