---
title: "aaaAzure AD многоуровневого безопасности пароля | Документы Microsoft"
description: "В этой статье объясняется, как Azure AD применяет надежные пароли и защищает пароли пользователей от киберпреступников."
services: active-directory
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: joflore
ms.openlocfilehash: 10d8b600d9f4c02355b2cd8c5dccf8505aaf210d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="a-multi-tiered-approach-tooazure-ad-password-security"></a>Защита паролем многоуровневый подход tooAzure AD

В этой статье обсуждаются некоторые рекомендации, можно выполнить как пользователь или администратор tooprotect Azure Active Directory (Azure AD) либо учетная запись Майкрософт.

 > [!NOTE]
 > Azure AD администраторы могут сбросить пароли пользователей, с помощью инструкции hello в статье hello [Сброс hello пароля для пользователя в Azure Active Directory](active-directory-users-reset-password-azure-portal.md).
 >
 > Пользователи могут сбросить свой пароль, с помощью инструкции hello в статье hello [справки пользователь забыл свой пароль Azure AD](active-directory-passwords-update-your-own-password.md).
 >

## <a name="password-requirements"></a>Требования к паролю

Azure AD включает hello следующих распространенных простых паролей toosecuring подходов:

* настройка требований к длине пароля;
* настройка требований к сложности пароля;
* регулярная и периодическая смена пароля.

Сведения о в Azure Active Directory сброса пароля см. в разделе hello [Azure AD самостоятельный сброс пароля для ИТ-специалистов hello](active-directory-passwords.md).

## <a name="azure-ad-password-protections"></a>Защита паролей в Azure AD

Azure AD и система учетных записей Майкрософт использовать проверенные отрасли hello подходы tooensure безопасного защиты пользователей и администраторов паролей, включая:

* Динамическая блокировка паролей
* Smart Password Lockout

Сведения об управлении паролями, основаны на текущем исследованиях. в разделе Технический документ hello [пароль руководство](http://aka.ms/passwordguidance).

### <a name="dynamically-banned-passwords"></a>Динамическая блокировка паролей

Azure AD и учетные записи Майкрософт обеспечивают защиту паролей, динамически запрещая все часто используемые пароли. Команда защиты идентификации Azure идентификатор Hello регулярно анализирует списки запрещенных пароль, предотвращая Выбор часто используемые паролей пользователями. Эта служба является доступной tooAzure AD и клиентов службы учетных записей Microsoft hello.

При создании паролей, очень важно для администраторов tooencourage пользователей toochoose пароль фраз, которые содержат уникальное сочетание буквы, цифры, символы или слова. Такой подход помогает скомпрометирован toobe практически невозможно, но упрощает для пользователей tooremember пароли пользователей toomake.

#### <a name="password-breaches"></a>Нарушение безопасности паролей

Корпорация Майкрософт всегда работает один шаг toostay до кибер злоумышленники.

Команда Azure AD Identity Protection Hello постоянно анализирует пароли, которые широко используются. Кибер-также используют злоумышленники аналогичные tooinform стратегии их атаки, такие как построение [радуги таблицы](https://en.wikipedia.org/wiki/Rainbow_table) для взлома хэши паролей.

Корпорация Майкрософт постоянно анализирует [утечки данных](https://www.privacyrights.org/data-breaches) toomaintain список обновляется динамически запрещенное пароль, который обеспечивает заблокированные пароли уязвимы прежде чем они станут реальную угрозы tooAzure AD клиентов. Дополнительные сведения о текущем усилия по безопасности см. в разделе hello [этого отчета](https://www.microsoft.com/security/sir/default.aspx).

### <a name="smart-password-lockout"></a>Smart Password Lockout

Когда Azure AD обнаруживает потенциальные toohack при атаках кибер в пароля пользователя, мы заблокировать учетную запись пользователя hello смарт-блокировка пароль. Azure AD предназначен toodetermine hello рисков, связанных с сеансами конкретного имени входа. Затем с помощью hello самые последние данные безопасности, мы применяем угроз кибер toostop семантику блокировки.

Если пользователь заблокирован из Azure AD, их экран выглядит примерно toohello том, что следует:

  ![Блокировка в Azure AD](./media/active-directory-secure-passwords/locked-out-azuread.png)

Для других учетных записей Майкрософт их экран выглядит примерно toohello том, что следует:

  ![Блокировка учетной записи Майкрософт](./media/active-directory-secure-passwords/locked-out-ms-accounts.png)

Сведения о в Azure Active Directory сброса пароля см. в разделе hello [Azure AD самостоятельный сброс пароля для ИТ-специалистов hello](active-directory-passwords.md).

  >[!NOTE]
  >Если вы являетесь администратором Azure AD, вы можете toouse [Windows Hello](https://www.microsoft.com/windows/windows-hello) tooavoid наличие пользователей создавать традиционные пароли полностью.
  >

## <a name="next-steps"></a>Дальнейшие действия

* [Как tooupdate свой пароль](active-directory-passwords-update-your-own-password.md)
* [Основные принципы управления удостоверениями Azure Hello](fundamentals-identity.md)
* [Приступая к работе с Azure](active-directory-passwords-reporting.md)


