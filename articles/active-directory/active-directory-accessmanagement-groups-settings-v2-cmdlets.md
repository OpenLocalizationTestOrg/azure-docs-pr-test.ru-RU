---
title: "Примеры aaaPowerShell для управления группами в Azure Active Directory | Документы Microsoft"
description: "На этой странице представлены примеры toohelp PowerShell Управление группами в Azure Active Directory"
keywords: "Azure AD, Azure Active Directory, PowerShell, группы, управление группами"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7a5023dc-2727-4c25-8254-b531fc3244ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: rodejo
ms.openlocfilehash: ba049babc436e99a290f20899b3a87bcfa811d9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-version-2-cmdlets-for-group-management"></a>Командлеты Azure Active Directory версии 2 для управления группами
> [!div class="op_single_selector"]
> * [Портал Azure](active-directory-groups-create-azure-portal.md)
> * [Классический портал Azure](active-directory-accessmanagement-manage-groups.md)
> * [PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

Эта статья содержит примеры использования toouse PowerShell toomanage групп в Azure Active Directory (Azure AD).  Он также рассказывается, как настроить tooget с hello модуля Azure AD PowerShell. Во-первых, необходимо [загрузки модуля Azure AD PowerShell hello](https://www.powershellgallery.com/packages/AzureAD/).

## <a name="installing-hello-azure-ad-powershell-module"></a>Установка модуля Azure AD PowerShell hello
hello tooinstall модуля Azure AD PowerShell, используйте hello, следующие команды:

    PS C:\Windows\system32> install-module azuread

tooverify, hello модуля был установлен, выполните следующую команду hello.

    PS C:\Windows\system32> get-module azuread

    ModuleType Version      Name                                ExportedCommands
    ---------- ---------    ----                                ----------------
    Binary     2.0.0.115    azuread                      {Add-AzureADAdministrati...}

Теперь можно запустить с помощью командлетов hello в модуле hello. Полное описание командлетов hello в модуле hello Azure AD, можно найти toohello online справочную документацию по [Azure Active Directory PowerShell версии 2](/powershell/azure/install-adv2?view=azureadps-2.0).

## <a name="connecting-toohello-directory"></a>Подключение toohello directory
Прежде чем приступить к управлению группами с помощью командлетов Azure AD PowerShell, необходимо подключить каталог toohello сеанса PowerShell, требуется toomanage. Hello используйте следующую команду:

    PS C:\Windows\system32> Connect-AzureAD

Hello командлет предложит hello учетных данных вы хотите toouse tooaccess вашего каталога. В этом примере мы используем karen@drumkit.onmicrosoft.com tooaccess hello демонстрации каталога. Hello командлет возвращает подтверждение tooshow hello сеанс был подключен успешно tooyour каталога:

    Account                       Environment Tenant
    -------                       ----------- ------
    Karen@drumkit.onmicrosoft.com AzureCloud  85b5ff1e-0402-400c-9e3c-0f…

Теперь можно запустить с помощью командлетов toomanage hello AzureAD групп в каталоге.

## <a name="retrieving-groups"></a>Получение сведений о группах
существующие группы tooretrieve из каталога, используемого hello командлет Get-AzureADGroups. tooretrieve всех групп в каталоге hello, используйте командлет hello без параметров.

    PS C:\Windows\system32> get-azureadgroup

Hello командлет возвращает все группы в подключенном каталоге hello.

Можно использовать tooretrieve параметра - objectID hello определенной группы, для которого задаются objectID hello группы:

    PS C:\Windows\system32> get-azureadgroup -ObjectId e29bae11-4ac0-450c-bc37-6dae8f3da61b

командлет Hello теперь возвращает objectID которого соответствует значению hello параметра hello введенный группы hello:

    DeletionTimeStamp            :
    ObjectId                     : e29bae11-4ac0-450c-bc37-6dae8f3da61b
    ObjectType                   : Group
    Description                  :
    DirSyncEnabled               :
    DisplayName                  : Pacific NW Support
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 9bb4139b-60a1-434a-8c0d-7c1f8eee2df9
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

Можно выполнить поиск конкретной группы с помощью hello - параметр фильтра. Этот параметр принимает предложение фильтра ODATA и возвращает все группы, соответствующие фильтру hello, как следующий пример hello:

    PS C:\Windows\system32> Get-AzureADGroup -Filter "DisplayName eq 'Intune Administrators'"


    DeletionTimeStamp            :
    ObjectId                     : 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df
    ObjectType                   : Group
    Description                  : Intune Administrators
    DirSyncEnabled               :
    DisplayName                  : Intune Administrators
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 4dd067a0-6515-4f23-968a-cc2ffc2eff5c
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

> [!NOTE] 
> командлеты AzureAD PowerShell Hello реализовать hello стандартных запросов OData. Дополнительные сведения см. в разделе **$filter** в [параметры запросов системы OData, с помощью конечной точки OData hello](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).

## <a name="creating-groups"></a>Создание групп
toocreate новую группу в вашем каталоге, используйте командлет New-AzureADGroup hello. Этот командлет создает новую группу безопасности с именем Marketing:

    PS C:\Windows\system32> New-AzureADGroup -Description "Marketing" -DisplayName "Marketing" -MailEnabled $false -SecurityEnabled $true -MailNickName "Marketing"

## <a name="updating-groups"></a>Обновление групп
tooupdate существующую группу, с помощью командлета Set AzureADGroup hello. В этом примере происходит изменение hello свойство DisplayName hello группы «Администраторы Intune». Во-первых мы поиск hello группы, с помощью командлета Get-AzureADGroup hello и фильтрация с помощью атрибут DisplayName hello:

    PS C:\Windows\system32> Get-AzureADGroup -Filter "DisplayName eq 'Intune Administrators'"


    DeletionTimeStamp            :
    ObjectId                     : 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df
    ObjectType                   : Group
    Description                  : Intune Administrators
    DirSyncEnabled               :
    DisplayName                  : Intune Administrators
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 4dd067a0-6515-4f23-968a-cc2ffc2eff5c
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

Далее мы происходит изменение hello описание toohello новое значение свойства «Администраторы устройств Intune»:

    PS C:\Windows\system32> Set-AzureADGroup -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -Description "Intune Device Administrators"

Теперь если мы найти группы hello мы увидим hello описание свойства является обновленные tooreflect hello новое значение:

    PS C:\Windows\system32> Get-AzureADGroup -Filter "DisplayName eq 'Intune Administrators'"


    DeletionTimeStamp            :
    ObjectId                     : 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df
    ObjectType                   : Group
    Description                  : Intune Device Administrators
    DirSyncEnabled               :
    DisplayName                  : Intune Administrators
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 4dd067a0-6515-4f23-968a-cc2ffc2eff5c
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

## <a name="deleting-groups"></a>Удаление групп
toodelete групп из каталога, используйте командлет Remove-AzureADGroup hello следующим образом:

    PS C:\Windows\system32> Remove-AzureADGroup -ObjectId b11ca53e-07cc-455d-9a89-1fe3ab24566b

## <a name="managing-members-of-groups"></a>Управление членами групп
При необходимости tooadd новую группу tooa членов с помощью командлета Add AzureADGroupMember hello. Эта команда добавляет членом группы администраторов Intune toohello члена, которые были использованы в предыдущем примере hello:

    PS C:\Windows\system32> Add-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

Hello параметра - ObjectId — hello ObjectID можем tooadd членом группы toowhich hello и hello - RefObjectId — hello ObjectID пользователя hello мы хотим tooadd как toohello элементов групп.

tooget hello существующие члены группы, используйте командлет Get-AzureADGroupMember hello, как показано в примере:

    PS C:\Windows\system32> Get-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          72cd4bbd-2594-40a2-935c-016f3cfeeeea User
                          8120cc36-64b4-4080-a9e8-23aa98e8b34f User

tooremove hello мы ранее добавлен член группы toohello, используйте командлет Remove-AzureADGroupMember hello, как показано ниже:

    PS C:\Windows\system32> Remove-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -MemberId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

tooverify hello группы участие пользователя, с помощью командлета Select AzureADGroupIdsUserIsMemberOf hello. Этот командлет принимает в качестве своих параметров hello ObjectId hello пользователя для членства в группах какие toocheck hello и список групп для hello какие toocheck членства. Hello список групп необходимо, предоставляемых в виде переменной сложного типа «Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck» hello, поэтому сначала необходимо создать переменную с этим типом.

    PS C:\Windows\system32> $g = new-object Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck

Далее мы введите значения для toocheck groupIds hello в атрибуте hello «GroupIds» этой переменной комплексного:

    PS C:\Windows\system32> $g.GroupIds = "b11ca53e-07cc-455d-9a89-1fe3ab24566b", "31f1ff6c-d48c-4f8a-b2e1-abca7fd399df"

Теперь если мы хотим toocheck hello членства в группах пользователя с 72cd4bbd-2594-40a2-935c-016f3cfeeeea ObjectID для всех групп hello в $g, следует использовать:

    PS C:\Windows\system32> Select-AzureADGroupIdsUserIsMemberOf -ObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea -GroupIdsForMembershipCheck $g

    OdataMetadata                                                                                                 Value
    -------------                                                                                                  -----
    https://graph.windows.net/85b5ff1e-0402-400c-9e3c-0f9e965325d1/$metadata#Collection(Edm.String)             {31f1ff6c-d48c-4f8a-b2e1-abca7fd399df}


Hello возвращаемое значение списка групп, членом которых является этот пользователь. Вы также можете применять этот метод toocheck контакты, группы или субъекты-службы членства, заданному списку групп, с помощью Select-AzureADGroupIdsContactIsMemberOf Select AzureADGroupIdsGroupIsMemberOf или Выберите AzureADGroupIdsServicePrincipalIsMemberOf

## <a name="managing-owners-of-groups"></a>Управление владельцами групп
Группа tooa владельцев tooadd, используйте командлет Add-AzureADGroupOwner hello:

    PS C:\Windows\system32> Add-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

Hello параметра - ObjectId — hello ObjectID toowhich группы hello можем tooadd владельца и hello - RefObjectId — hello ObjectID пользователя hello мы хотим tooadd в качестве владельца группы hello.

tooretrieve hello владельцев группы, используйте командлет Get-AzureADGroupOwner hello:

    PS C:\Windows\system32> Get-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

Hello командлет возвращает список владельцев для указанной группы hello hello.

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          e831b3fd-77c9-49c7-9fca-de43e109ef67 User

Tooremove владельца из группы, используйте командлет Remove-AzureADGroupOwner hello:

    PS C:\Windows\system32> remove-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -OwnerId e831b3fd-77c9-49c7-9fca-de43e109ef67

## <a name="reserved-aliases"></a>Зарезервированные псевдонимы 
При создании группы определенные конечные точки позволяют toospecify конечного пользователя hello toobe mailNickname или псевдонима, используется в качестве части адреса электронной почты hello hello группы. Группы с hello следующие псевдонимы привилегированным электронной почты могут создаваться только глобальный администратор Azure AD. 
  
* abuse 
* admin 
* administrator 
* hostmaster 
* majordomo 
* postmaster 
* root 
* secure 
* security 
* ssl-admin 
* webmaster 

## <a name="next-steps"></a>Дальнейшие действия
Дополнительную документацию по PowerShell Azure Active Directory см. в разделе [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0) (Командлеты Azure Active Directory).

* [Управление tooresources доступ с помощью групп Azure Active Directory](active-directory-manage-groups.md)
* [Интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md)
