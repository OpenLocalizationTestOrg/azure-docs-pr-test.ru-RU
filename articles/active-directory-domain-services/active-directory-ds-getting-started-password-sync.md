---
title: "Доменные службы Azure Active Directory. Включение синхронизации паролей | Документация Майкрософт"
description: "Приступая к работе с доменными службами Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 5a32a0df-a3ca-4ebe-b980-91f58f8030fc
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: 8e073df9de2996f5ad159dda746881c014ea3d66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a>Включение синхронизации паролей tooAzure доменных служб Active Directory
Выполняя предыдущие задачи, вы включили доменные службы Azure Active Directory для клиента Azure Active Directory (Azure AD). Следующая задача Hello-tooenable синхронизации хэшей учетные данные, необходимые для tooAzure проверки подлинности NT LAN Manager (NTLM) и Kerberos доменные службы AD. После настройки синхронизации учетных данных, пользователи могут входить в управляемый домен toohello со своими корпоративными учетными данными.

этапы Hello отличаются для учетных записей пользователя только для облака учетные записи vs, которые синхронизируются из вашего локального каталога с помощью Azure AD Connect.  Если клиент Azure AD имеет сочетание облако только пользователей и пользователей из локальной AD, необходимо tooperform оба шага.

<br>

> [!div class="op_single_selector"]
> * **Учетные записи пользователей только для облака**: [синхронизации паролей для облачных учетных записей пользователей tooyour управляемого домена](active-directory-ds-getting-started-password-sync.md)
> * **Локальные учетные записи пользователей**: [синхронизировать пароли для учетных записей пользователей, синхронизированных из локальной AD tooyour управляемого домена](active-directory-ds-getting-started-password-sync-synced-tenant.md)
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-cloud-only-user-accounts"></a>Задача 5: Включение пароль tooyour управляемого домена синхронизации учетных записей пользователя только для облака
Пользователи tooauthenticate hello управляемого домена, доменных служб Active Directory Azure требуются учетные данные хэш-коды в формате, который подходит для проверки подлинности NTLM и Kerberos. Azure AD не создавать и хранить хэши учетных данных в формате hello, необходимый для проверки подлинности NTLM или Kerberos, пока не будет включена, Azure доменных служб Active Directory для вашего клиента. Из очевидных соображений безопасности служба Azure AD не хранит пароли в формате открытого текста. Таким образом Azure AD не имеет tooautomatically способом создания этих учетных данных хэш NTLM или Kerberos на основе существующих учетных данных пользователей.

> [!NOTE]
> Если ваша организация использует учетные записи пользователей, пользователей, которым необходим служб домена Active Directory toouse Azure необходимо изменить свои пароли. Учетная запись пользователя только для облака — учетная запись, созданная в Azure AD с помощью hello портал Azure или командлеты Azure AD PowerShell. Такие учетные записи пользователей не синхронизированы из локального каталога.
>
>

Этот процесс изменения пароля приводит hello учетных данных хэш-коды, которые необходимы Azure доменных служб Active Directory для toobe проверки подлинности Kerberos и NTLM, созданные в Azure AD. Либо срок действия можно hello пароли для всех пользователей в hello клиентов, которым требуется служб домена Active Directory Azure toouse или предложите им toochange свои пароли.

### <a name="enable-ntlm-and-kerberos-credential-hash-generation-for-a-cloud-only-user-account"></a>Включение создания хэшей учетных данных NTLM и Kerberos для облачных учетных записей пользователей
Ниже приведены hello указания по созданию tooprovide пользователей, чтобы они могли изменять свои пароли.

1. Go toohello [панели доступа Azure AD](http://myapps.microsoft.com) страницы для вашей организации.

    ![Запуск панели доступа Azure AD hello](./media/active-directory-domain-services-getting-started/access-panel.png)

2. В hello правом верхнем углу щелкните свое имя и выберите **профиль** меню "hello".

    ![Выбор параметра "Профиль"](./media/active-directory-domain-services-getting-started/select-profile.png)

3. На hello **профиль** щелкните **Смена пароля**.

    ![Выбор параметра "Изменение пароля"](./media/active-directory-domain-services-getting-started/user-change-password.png)

   > [!NOTE]
   > Если hello **Смена пароля** параметр не отображается в окне приветствия панели доступа, убедитесь, что ваша организация настроил [управление паролями в Azure AD](../active-directory/active-directory-passwords-getting-started.md).
   >
   >
4. На hello **смены пароля** введите текущий пароль (старая), введите новый пароль и затем подтвердите его.

    ![Создание виртуальной сети для доменных служб Azure AD.](./media/active-directory-domain-services-getting-started/user-change-password2.png)

5. Щелкните **Отправить**.

Через несколько минут после вы изменили свой пароль, новый пароль hello, можно использовать в доменных службах Active Directory Azure. Через несколько дополнительных минут (обычно около 20 в минутах), вы сможете войти в toocomputers, которые присоединены к домену toohello управляемого домена с помощью пароля hello только что изменен.

## <a name="related-content"></a>Похожий контент
* [Как tooupdate свой пароль](../active-directory/active-directory-passwords-update-your-own-password.md)
* [Приступая к работе с компонентами управления паролями](../active-directory/active-directory-passwords-getting-started.md)
* [Включить синхронизацию паролей для клиента tooAzure доменных служб Active Directory для синхронизированных Azure AD](active-directory-ds-getting-started-password-sync-synced-tenant.md)
* [Администрирование управляемого домена доменных служб Azure Active Directory](active-directory-ds-admin-guide-administer-domain.md)
* [К домену Windows виртуальной машины tooan управляемых доменных служб Active Directory Azure](active-directory-ds-admin-guide-join-windows-vm.md)
* [К домену Red Hat Enterprise Linux виртуальной машины tooan управляемых доменных служб Active Directory Azure](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
