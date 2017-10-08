---
title: "элементы aaaThe электронное приглашение hello Azure Active Directory B2B совместной работы | Документы Microsoft"
description: "Шаблон сообщения с приглашением в службу совместной работы Azure Active Directory B2B"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: f4908014d71a63442bbdca2182f54c7a79675a82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="hello-elements-of-hello-b2b-collaboration-invitation-email"></a>элементы Hello hello электронное приглашение B2B совместной работы

Приглашение сообщения электронной почты, которые являются партнерами toobring важнейшей них B2B совместной работы пользователей в Azure AD. Доверие можно использовать их tooincrease hello получателя. Вы можете добавить их и социальных сетей toohello проверки электронной почты, toomake убедиться, что получатель hello, в том числе освоите Выбор hello **приступить к работе** кнопку tooaccept hello приглашения. Это отношение доверия является ключ означает tooreduce трения для управления доступом. И вы хотите искать по электронной почте hello toomake отлично!

![Сообщение с приглашением в службу Azure AD B2B](media/active-directory-b2b-invitation-email/invitation-email.png)

## <a name="explaining-hello-email"></a>Объясняется hello электронной почты
Давайте взглянем на несколько элементов hello электронной почты, чтобы знать, как наиболее toouse их возможности.

### <a name="subject"></a>Субъект
Hello субъекта hello электронной почты следует hello следующий шаблон: приглашаем вас toohello &lt;tenantname&gt; организации

### <a name="from-address"></a>Адрес отправителя
Мы используем LinkedIn шаблон для hello адрес отправителя.  Необходимо очистить, являющийся приглашающего hello и из компании, а также прояснить hello сообщение электронной почты поступает от адрес электронной почты Майкрософт. Формат Hello: &lt;отображаемое имя приглашающего&gt; из &lt;tenantname&gt; (с помощью Microsoft) <invites@microsoft.com&gt;

### <a name="reply-to"></a>Ответить
Hello ответ tooemail задан приглашающего toohello электронной почты, если она доступна, который ответ, электронной почты toohello отправляет приглашающего задней toohello электронной почты.

### <a name="branding"></a>Фирменная символика
сообщения электронной почты от вашего клиента используйте фирменной символики, компании hello приглашения Hello может настройки для вашего клиента. Если требуется, чтобы tootake преимущества этих возможностей [здесь](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) hello. Подробности о том, как tooconfigure его. баннер с логотипом Hello появляется в сообщении электронной почты hello. Выполните hello размер образа и качество инструкции [здесь](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) для получения наилучших результатов. Кроме того, hello компании имя также отображается в tooaction вызов hello.

### <a name="call-tooaction"></a>Вызов tooaction
Здравствуйте, вызов tooaction состоит из двух частей: объясняется, почему hello получатель получил почты hello и какие получателя hello которой запрашивается toodo о нем.
- Здравствуйте, «почему» раздела можно устранить, используя следующий шаблон hello: стали приглашенных tooaccess приложения hello &lt;tenantname&gt; организации

- И hello, раздел «что в ответ на вопрос toodo» обозначается hello наличие hello **начать** кнопки. При добавлении hello получателя без необходимости hello приглашения эта кнопка не отображается.

### <a name="inviters-information"></a>Сведения о приглашающем
Hello приглашающего отображаемое имя включается в сообщении электронной почты hello. И, кроме того, если вы настроили изображение профиля для учетной записи Azure AD, hello приглашение по электронной почте будет содержать этот рисунок также. Оба являются tooincrease предполагаемого получателя достоверности в сообщении электронной почты hello.

Если вы еще не настроили изображение профиля, отображается значок с hello приглашающего инициалы вместо рисунка hello:

  ![Отображение инициалы приглашающего hello](media/active-directory-b2b-invitation-email/inviters-initials.png)

### <a name="body"></a>Текст
текст Hello содержит приветственное сообщение, приглашающего hello составляет или передается через приглашения hello API. Это текстовое поле, поэтому в целях безопасности в нем не обрабатываются HTML-теги.

### <a name="footer-section"></a>Нижний колонтитул
нижний колонтитул Hello содержит фирменной символики компании Майкрософт hello и позволяет получателю hello знать, если было отправлено сообщение hello из псевдонима не отслеживается. Особые случаи:

- приглашающего Hello не использует адрес электронной почты в приглашении аренды hello

  ![Рисунок приглашающего не использует адрес электронной почты в приглашении аренды hello](media/active-directory-b2b-invitation-email/inviter-no-email.png)


- Получатель Hello не требует tooredeem hello приглашения

  ![Если получатель не требует tooredeem приглашения](media/active-directory-b2b-invitation-email/when-recipient-doesnt-redeem.png)


## <a name="next-steps"></a>Дальнейшие действия

Другие статьи о службе совместной работы Azure AD B2B:

* [Что такое предварительная версия службы совместной работы Azure AD B2B?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Как администраторы Azure Active Directory могут добавить пользователей службы совместной работы B2B?](active-directory-b2b-admin-add-users.md)
* [Как информационные работники могут добавить пользователей службы совместной работы B2B в Azure Active Directory?](active-directory-b2b-iw-add-users.md)
* [Активация приглашения службы совместной работы B2B](active-directory-b2b-redemption-experience.md)
* [Руководство по лицензированию службы совместной работы Azure Active Directory B2B](active-directory-b2b-licensing.md)
* [Устранение неполадок службы совместной работы Azure Active Directory B2B](active-directory-b2b-troubleshooting.md)
* [Часто задаваемые вопросы о службе совместной работы Azure Active Directory B2B](active-directory-b2b-faq.md)
* [API службы совместной работы Azure Active Directory B2B и настройка](active-directory-b2b-api.md)
* [Многофакторная идентификация для пользователей службы совместной работы B2B](active-directory-b2b-mfa-instructions.md)
* [Добавление пользователей службы совместной работы B2B без приглашения](active-directory-b2b-add-user-without-invite.md)
* [Указатель статьей по управлению приложениями в Azure Active Directory](active-directory-apps-index.md)
