---
title: "aaaHow Azure подписки связаны с Azure Active Directory | Документы Microsoft"
description: "Вход tooMicrosoft Azure и проблем, например hello связь между подпиской Azure и Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: bc4773c2-bc4a-4d21-9264-2267065f0aea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/24/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 4f831cfb972efec57083fcaa63adb43fde7b2faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-subscriptions-are-associated-with-azure-active-directory"></a>Связь между подписками Azure и службой Azure Active Directory
В этой статье представлены сведения о hello отношения между подпиской Azure и Azure Active Directory (Azure AD) и как tooadd существующий каталог Azure AD tooyour подписки.

## <a name="your-azure-subscriptions-relationship-tooazure-ad"></a>TooAzure связи подписки Azure AD
Ваша подписка Azure имеет отношение доверия с Azure AD, это означает, что она доверяет hello каталог tooauthenticate пользователей, служб и устройств. Несколько подписок могут доверять hello же каталоге, но каждая подписка доверяет только одному каталогу. 

Hello отношения доверия между подпиской и каталогом не похожи hello связь с с другими ресурсами в Azure (веб-сайтов, баз данных и т. д.). Если действие подписки истечет, доступ к toohello также останавливает другие ресурсы, связанные с подпиской hello. Наряду с каталогом Azure AD в Azure, вы можете связать другую подписку с этим каталогом и управлять hello каталог, используя новую подписку hello.

![Схема: как подписки связаны с каталогом](./media/active-directory-how-subscriptions-associated-directory/WAAD_OrgAccountSubscription.png)

Все пользователи относятся к единому домашнему каталогу, который проверяет их подлинность. Они также могут быть гостями в других каталогах. В Azure AD можно просмотреть каталоги hello которых учетная запись пользователя является элемент или гостя.

## <a name="azure-ad-and-cloud-service-subscriptions"></a>Azure AD и подписки на облачные службы
Azure AD обеспечивает hello core каталогами и удостоверениями возможности управления большинства облачных служб Майкрософт, включая:

* Таблицы Azure
* Microsoft Office 365
* Microsoft Dynamics CRM Online
* Microsoft Intune

При регистрации для любой из этих облачных служб Майкрософт, вы получаете hello бесплатной службой Azure AD. Если вы хотите tooadd есть каталог Azure AD tooan дополнительные подписки Azure, должны быть подписаны с учетной записью Майкрософт. Если вход tooAzure с помощью рабочей или учебной учетной записи, невозможно добавить существующий каталог tooan подписки Azure, поскольку вашей рабочей или учебной учетной записи не может пройти проверку подлинности непосредственно Azure. 

## <a name="tooadd-an-existing-subscription-tooyour-azure-ad-directory"></a>tooadd существующий каталог Azure AD tooyour подписки
Необходимо войти с учетной записью, которая существует в текущем каталоге обоих hello, с которой hello связана подписка, и в каталоге hello требуется tooadd его. 

1. Войдите в toohello [центр учетных записей Azure](https://account.windowsazure.com/Home/Index) под учетной записью, hello учетной записи администратора подписки hello, владелец которой требуется tootransfer.
2. Убедитесь, hello пользователя, который вы хотите владельца подписки hello toobe находится в каталоге hello целевые.
3. Щелкните **Перенос подписки**.
4. Укажите получателя hello. Hello получатель автоматически получает сообщение электронной почты со ссылкой приемки.
5. Получатель Hello щелкает ссылку hello и следует инструкциям hello, введя свои реквизиты. После успешного завершения получателя hello передается hello подписки. 
6. изменить каталог по умолчанию Hello hello подписки toohello directory hello пользователя находится в.


## <a name="suggestions-toomanage-both-a-subscription-and-a-directory"></a>Предложения toomanage каталог и подписка
Hello административные роли подписки Azure управляют ресурсами, привязанными toohello подписки Azure. В этом разделе описываются отличия hello подписки Azure Администраторы и Администраторы каталогов Azure AD. Административные роли и другие предложения по их использованию подпиской описаны в toomanage [назначение ролей администратора в Azure Active Directory](active-directory-assign-admin-roles.md).

По умолчанию назначаются роли администратора службы hello при регистрации. Если другие пользователи должны toosign в и получать доступ к службам с помощью hello одной подписке, их можно добавить дополнительных администраторов. 

Azure AD предоставляет ряд различных directory hello toomanage административные роли и компоненты, связанные с идентификаторами. Например hello глобального администратора каталога Добавление пользователей и групп toohello каталог или требовать многофакторную проверку подлинности для пользователей. Роль глобального администратора toohello назначен пользователь, создающий каталог, и они могут назначать административные роли пользователей tooother. Роли администраторов Azure AD также используются другими службами, например Office 365 и Microsoft Intune. 

Администраторы подписки Azure и администраторы каталога Azure AD — это две разные роли. 
* Администраторы подписки Azure могут управлять ресурсами в Azure и можно использовать Azure AD в hello портал Azure (поскольку hello Azure самого портала — это ресурс Azure). 
* Администраторы каталогов можно управлять свойствами только в каталоге Azure AD hello.

Пользователю можно назначить обе эти роли, но это не обязательно. Глобального администратора каталога невозможно назначить в качестве администратора службы или соадминистратора подписки Azure или наоборот. Не является администратором подписки hello, hello пользователя может войти в toohello портал Azure, но не может управлять hello каталоги для этой подписки на портале hello. Тем не менее этот пользователь может управлять с помощью других средств, таких как Azure AD PowerShell или Центр администрирования Office 365 hello.

## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения о toolearn toochange администраторов для подписки Azure. в статье [передачи владения tooanother учетную запись подписки Azure](../billing/billing-subscription-transfer.md)
* toolearn Дополнительные сведения о как осуществляется доступ к ресурсам в Microsoft Azure в разделе [основные сведения о доступе к ресурсам в Azure](active-directory-understanding-resource-access.md)
* Дополнительные сведения о том, как tooassign роли в Azure AD в разделе [назначение ролей администратора в Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)

<!--Image references-->
[1]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_PassThruAuth.png
[2]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_OrgAccountSubscription.png
[3]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_SignInDisambiguation.PNG
