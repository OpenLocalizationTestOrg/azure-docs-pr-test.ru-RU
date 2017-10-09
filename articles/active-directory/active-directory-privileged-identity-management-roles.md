---
title: "aaaRoles в Azure AD Privileged Identity Management | Документы Microsoft"
description: "Узнайте, какие роли используются для привилегированных удостоверений с hello расширение управления привилегированными пользователями Azure."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: ac812ccc-cf4e-4ac2-b981-69598056c9ed
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017;oldportal;it-pro;
ms.openlocfilehash: dc58d005489e3b51b3b3dbea4bf35bd795dbdfb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="different-administrative-role-in-azure-active-directory-pim"></a>Различные административные роли в Azure Active Directory PIM
<!-- **PLACEHOLDER: Need description of how this works. Azure PIM uses roles from MSODS objects.**-->

Можно назначить пользователей в вашей организации toodifferent административных ролей в Azure AD. Эти назначения ролей контролировать, какие задачи, такие как добавление или удаление пользователей либо изменить параметры службы, hello пользователи могли tooperform на Azure AD, Office 365 и других служб Microsoft Online Services и подключенных приложений.  

> [!IMPORTANT]
> Корпорация Майкрософт рекомендует управлять Azure AD, используя hello [Центр администрирования Azure AD](https://aad.portal.azure.com) в hello портал Azure, вместо использования hello классический портал Azure, в этой статье.

Глобальный администратор может обновлять которой пользователи являются **окончательно** назначены tooroles в Azure AD, с помощью командлетов PowerShell, таких как `Add-MsolRoleMember` и `Remove-MsolRoleMember`, или с помощью классического портала hello, как описано в [ Назначение ролей администратора в Azure Active Directory](active-directory-assign-admin-roles.md).

Служба управления привилегированными пользователями (PIM) Azure AD управляет политиками привилегированного доступа для пользователей в Azure AD. PIM назначает tooone пользователей или несколько ролей в Azure AD, и кто-то можно назначить toobe без возможности восстановления в роль hello, или, доступные для роли hello. При пользователя без возможности восстановления назначена роль tooa или активирует назначение ролей на соответствующих, а затем их можно управлять с помощью назначения ролей, tootheir разрешения hello Azure Active Directory, Office 365 и другие приложения.

Нет никаких различий в hello доступа, предоставленный toosomeone с постоянным и назначение ролей на право. Hello отличается только что некоторые пользователи не требуется такой доступ все время hello. Они сделаны подлежащие hello роли и его можно включить и отключить каждый раз, когда они должны.

## <a name="roles-managed-in-pim"></a>Роли, которыми можно управлять в PIM
Управление привилегированными пользователями позволяет назначить роли администратора пользователей toocommon, включая:

* **Глобальный администратор** (известно также как администратор компании) имеет доступ tooall административных функций. В организации может быть несколько глобальных администраторов. Hello пользователь, зарегистрировавшийся toopurchase Office 365 автоматически становится глобальным администратором.
* **Администратор привилегированных ролей** управляет привилегированными пользователями в Azure AD и обновляет назначения ролей для других пользователей.  
* **Администратор выставления счетов** совершает покупки, управляет подписками и обращениями в службу поддержки, а также отслеживает работоспособность службы.
* **Администратор паролей** сбрасывает пароли, управляет запросами на обслуживание и отслеживает работоспособность службы. Администраторам пароль, не ограниченной tooresetting паролей для пользователей.
* **Администратор службы** управляет запросами на обслуживание и отслеживает работоспособность службы.
  
  > [!NOTE]
  > При использовании Office 365, перед назначением пользователя tooa роли администратора службы hello, сначала назначьте административные разрешения пользователя hello tooa службы, такие как Exchange Online.
  > 
  > 
* **Администратор управления пользователями** сбрасывает пароли, отслеживает работоспособность службы и управляет учетными записями пользователей, группами пользователей и запросами на обслуживание. Здравствуйте, администратор управления пользователя не может удалить глобального администратора, создавать другие роли администратора или сбрасывать пароли для выставления счетов, глобальных и администраторам службы.
* **Администратор Exchange** имеет административный доступ tooExchange сети через Центр администрирования Exchange hello (EAC) и можно выполнить почти любую задачу в Exchange Online.
* **Администратор SharePoint** имеет административный доступ tooSharePoint сети через Центр администрирования SharePoint Online hello и могут выполнять практически любые задачи в SharePoint Online.
* **Скайп для администратора предприятия** имеет tooSkype административного доступа для бизнеса через hello Скайп для бизнеса центра администрирования и можно выполнить почти любую задачу в Скайп для бизнеса Online.

Дополнительные сведения см. в статье [Назначение ролей администратора в Azure Active Directory](active-directory-assign-admin-roles.md) и [Назначение ролей администратора в Office 365](https://support.office.com/article/Assigning-admin-roles-in-Office-365-eac4d046-1afd-4f1a-85fc-8219c79e1504).

<!--**PLACEHOLDER: hello above article may not be hello one we want since PIM gets roles from places other that Office 365**-->


В PIM, вы можете [назначить эти роли пользователей tooa](active-directory-privileged-identity-management-how-to-add-role-to-user.md) , позволяющую hello пользователя [Активация роли hello при необходимости](active-directory-privileged-identity-management-how-to-activate-role.md).

Если требуется другой toomanage доступа пользователя в PIM, hello роли, которые требуется PIM toohave пользователя hello описаны далее в toogive [как toogive доступ к tooPIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).

<!-- ## hello PIM Security Administrator Role **PLACEHOLDER: Need description of hello Security Administrator role.**-->

## <a name="roles-not-managed-in-pim"></a>Роли, которыми нельзя управлять в PIM
Роли в Exchange Online или SharePoint Online, за исключением упомянутых выше, не представлены в Azure AD и поэтому не отображаются в PIM. Дополнительные сведения об изменении детализированных назначений ролей в этих службах Office 365 см. в статье [Роли администраторов в Office 365](https://support.office.com/article/Permissions-in-Office-365-da585eea-f576-4f55-a1e0-87090b6aaa9d).

Подписки Azure и группы ресурсов также не представлены в Azure AD. toomanage Azure подписки, в разделе [как tooadd или изменение роли администратора Azure](../billing/billing-add-change-azure-subscription-administrator.md) и Дополнительные сведения о Azure RBAC см. в разделе [контроля доступа](role-based-access-control-configure.md).

<!--**hello above links might be replaced by ones that are from within this documentation repository **-->


## <a name="user-roles-and-signing-in"></a>Роли пользователей и вход в систему
Для некоторых службы и приложения Майкрософт, назначение роли tooa пользователя не может быть достаточно tooenable toobe этого пользователя администратором.

Доступ toohello классический портал Azure требует hello пользователь быть администратором служб или соадминистратора в подписку Azure, даже если hello пользователю не требуется toomanage hello подписок Azure.  Например toomanage параметры конфигурации для Azure AD в классический портал hello, пользователь должен быть глобальным администратором в Azure AD и соадминистратор подписки, на подписку Azure.  toolearn tooadd пользователей tooAzure подписки, в статье [как tooadd или изменение роли администратора Azure](../billing/billing-add-change-azure-subscription-administrator.md).

TooMicrosoft доступа к интерактивным службам может потребоваться hello пользователей также необходимо назначить лицензию прежде, чем они смогут открыть портал hello службы или выполнять административные задачи.

## <a name="assign-a-license-tooa-user-in-azure-ad"></a>Назначение лицензии пользователя tooa в Azure AD
1. Войдите в toohello [классический портал Azure](http://manage.windowsazure.com) с учетной записью глобального администратора или учетной записи соадминистратора.
2. Выберите **все элементы** hello в главном меню.
3. Выберите каталог hello toowork с и что лицензии связанной с ним.
4. Выберите **Лицензии**. Появится список доступных лицензий Hello.
5. Выберите план лицензирования hello, содержащий hello лицензий, которые должны toodistribute.
6. Выберите **Назначить пользователей**.
7. Выберите hello пользователя, что требуется лицензия tooassign для.
8. Нажмите кнопку hello **назначить** кнопки.  Hello пользователь теперь может войти в tooAzure.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Дальнейшие действия
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

