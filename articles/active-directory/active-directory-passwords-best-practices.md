---
title: "Развертывание функции Azure AD SSPR | Документация Майкрософт"
description: "Советы для успешного развертывания функции самостоятельного сброса пароля в Azure AD"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: f8cd7e68-2c8e-4f30-b326-b22b16de9787
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 73d31679b38ff009a767335adaebc49fbc5a75b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="roll-out-password-reset-for-users"></a>Развертывание функции сброса паролей для пользователей

Большинство пользователей выполните hello описанных ниже tooensure smooth развертывания SSPR функциональных возможностей.

1. [Включите сброс паролей в каталоге.](active-directory-passwords-getting-started.md)
2. [Настройте локальные разрешения AD для обратной записи паролей.](active-directory-passwords-how-it-works.md#active-directory-permissions)
3. [Настройка обратной записи паролей](active-directory-passwords-writeback.md#configuring-password-writeback) tooyour локального каталога резервного toowrite пароли из Azure AD
4. [Назначьте и проверьте необходимые лицензии.](active-directory-passwords-licensing.md)
5. Если требуется, чтобы tooroll постепенно, что можно при необходимости предел сброса пароля tooa группы пользователей tooroll функцией hello медленно со временем. toodo задать hello **Self пароль сбросить включена служба** переключиться из **все** слишком**группы** и выберите tooenable группы безопасности для сброса пароля. Hello члены этой группы имеют toothem лицензии и является хорошим способом tooenable [группы на основе лицензирования](active-directory-passwords-licensing.md#enable-group-or-user-based-licensing).
6. Заполнение hello минимальный набор [данные проверки подлинности](active-directory-passwords-data.md), на основании политики.
7. Обучение пользователей как toouse SSPR, отправляя их инструкции tooshow их как tooregister и как tooreset.
    > [!NOTE]
    > Тестируйте SSPR с использованием учетной записи пользователя, а не администратора, так как Майкрософт имеет строгие требования к проверке подлинности учетных записей Azure типа "администратор". Дополнительные сведения о политике паролей администратора hello см. наш [глубокое погружение в статье](active-directory-passwords-how-it-works.md).

8. Можно выбрать tooenforce регистрации в любой момент и требуется tooreconfirm пользователей после определенного периода времени, данные проверки подлинности. Если вы не хотите вашей tooregister toohave пользователей, вы можете [развертывание сброс пароля без необходимости регистрации конечных пользователей](active-directory-passwords-data.md).
9. Со временем, просмотрите пользователей, регистрация и использование просмотрев hello [отчетов, предоставляемые Azure AD](active-directory-passwords-reporting.md).

## <a name="email-based-rollout"></a>Развертывание по электронной почте

Многие клиенты найти кампании по электронной почте, с инструкциями простой toouse является hello простым способом tooget пользователей toouse SSPR. [Мы создали три простых электронных сообщений, которые можно использовать в качестве шаблонов toohelp в развертывания.](https://onedrive.live.com/?authkey=%21AD5ZP%2D8RyJ2Cc6M&id=A0B59A91C740AB16%2125063&cid=A0B59A91C740AB16)

* **Ожидается в ближайшее время** используется в неделях hello или дней до развертывания toolet пользователи знают, что-нибудь требуется toodo toobe шаблон электронной почты.
* **Теперь доступны** шаблона используется toobe hello день запуска toodrive пользователей tooregister электронной почты и подтвердите свои данные проверки подлинности, чтобы они могли использовать SSPR, когда это необходимо.
* **Регистрация напоминание** шаблон для нескольких дней tooweeks по электронной почте после развертывания tooremind пользователей tooregister и подтвердить свои данные проверки подлинности.

## <a name="creating-your-own-password-portal"></a>Создание собственного портала паролей

Наших клиентов больше выберите toohost веб-страницы и создать запись DNS, такие как https://passwords.contoso.com корневой каталог. Они заполнения эту страницу сброса паролей ссылки toohello Azure AD, регистрации, порталов изменение паролей и других сведений, относящихся к организации для сброса пароля. Во всех сообщениях электронной почты или листовки отправлены, затем можно включить фирменной символикой, запоминающимися, URL-адрес, что пользователи могут перейти toowhen, они должны toouse hello служб.

* Портал сброса пароля: https://passwordreset.microsoftonline.com/
* Портал регистрации для сброса пароля: http://aka.ms/ssprsetup
* Портал изменения пароля: https://account.activedirectory.windowsazure.com/ChangePassword.aspx

## <a name="using-enforced-registration"></a>Принудительная регистрация

Если требуется вашей tooregister пользователей для сброса пароля можно принудительно tooregister при входе с помощью Azure AD. Этот параметр можно включить из вашего каталога **сброса пароля** колонки, включив hello **tooRegister требуют пользователей при входе в** параметр hello **регистрации** на вкладке.

Администраторы могут потребовать toore регистрацию пользователей после определенного периода времени путем установки hello **число дней, прежде чем пользователи задаваемые tooreconfirm данные проверки подлинности** от 0 до 730 дней.

После включения этого параметра, пользователи, входящие увидят сообщение, информирующее о том, их администратор требует tooverify данные проверки подлинности.

## <a name="populate-authentication-data"></a>Заполнение данных для проверки подлинности

Если вы [заполнения данными проверки подлинности для пользователей](active-directory-passwords-data.md), пользователям не требуется tooregister для сброса пароля, чтобы могли toouse SSPR, а затем. При условии, что пользователи имеют hello данные аутентификации, отвечающий вы определили политику сброса паролей hello, они могут tooreset свои пароли.

## <a name="disabling-self-service-password-reset"></a>Выключение самостоятельного сброса пароля

Отключение самостоятельного сброса пароля является просто открыть клиент Azure AD и происходит слишком**сброса пароля**, **свойства**и выбрав **никто не** под ** Самостоятельный сброс пароля включен**

## <a name="next-steps"></a>Дальнейшие действия

Привет, следующие ссылки предоставляют дополнительную информацию об пароль с помощью Azure AD

* [**Быстрое начало работы с самостоятельным сбросом пароля в Azure AD**](active-directory-passwords-getting-started.md). Запуск и выполнение службы самостоятельного управления паролями Azure AD. 
* [**Licensing requirements for Azure AD self-service password reset**](active-directory-passwords-licensing.md) (Требования к лицензированию самостоятельного сброса пароля в Azure AD). Сведения о настройке лицензирования Azure AD.
* [**Данные** ](active-directory-passwords-data.md) — понять hello данные, которые не требуется и как она используется для управления паролями
* [**Настройка** ](active-directory-passwords-customize.md) -настроить hello внешний вид и поведение hello SSPR взаимодействие с вашей компании.
* [**Политики и ограничения для паролей в Azure Active Directory**](active-directory-passwords-policy.md). Общие сведения и информация об установке политик паролей Azure AD.
* [**Обзор компонента обратной записи паролей**](active-directory-passwords-writeback.md). Как работает функция обратной записи паролей с вашим локальным каталогом.
* [**Reporting options for Azure AD password management**](active-directory-passwords-reporting.md) (Параметры отчетов для управления паролями Azure AD). Определяйте, кто и когда использовал функцию SSPR.
* [**Технические глубокое погружение** ](active-directory-passwords-how-it-works.md) -перейдите за занавесом toounderstand hello принцип работы
* [**Вопросы и ответы об управлении паролями**](active-directory-passwords-faq.md). Как? Почему? Что? Где? Кто? Когда? -Ответы tooquestions требуется, чтобы tooask
* [**Устранение неполадок** ](active-directory-passwords-troubleshoot.md) -Узнайте, как tooresolve распространенные проблемы, мы увидим с SSPR
