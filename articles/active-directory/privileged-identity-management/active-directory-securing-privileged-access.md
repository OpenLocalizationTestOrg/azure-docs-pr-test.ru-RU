---
title: "aaaSecuring привилегированный доступ в Azure AD | Документы Microsoft"
description: "Раздел, посвященный hello подходы для обеспечения безопасности привилегированным доступом для Azure, Azure Active Directory и Microsoft Online Services."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: mwahl
ms.assetid: 235a0ce9-1daf-4433-8f65-9c6afcd64d08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: kgremban
ms.custom: pim
ms.openlocfilehash: 694835dc5c41640673dbd996d44b0d1f217220de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="securing-privileged-access-in-azure-ad"></a>Защита привилегированного доступа в Azure AD
Обеспечение безопасности привилегированным доступом — критически важный первый шаг toohelp защиту корпоративных активов в современных организациях. Привилегированные учетные записи — это учетные записи, которые администрируют ИТ-системы и управляют ими. Злоумышленники кибер предназначены для этих учетных записей toogain доступа tooan организации данных и систем. toosecure привилегированный доступ, необходимо изолировать hello учетных записей и системами hello риск того, что отображается tooa злонамеренный пользователь.

Все больше пользователей начинают tooget привилегированный доступ с помощью облачных служб. Это могут быть глобальные администраторы Office 365, администраторы подписок Azure и пользователи, имеющие административный доступ на виртуальных машинах или в приложениях SaaS.

Корпорация Майкрософт рекомендует придерживаться следующего плана: [Защита привилегированного доступа](https://technet.microsoft.com/library/mt631194.aspx).

Клиенты, использующие Azure Active Directory, Office 365 или другие службы и приложения Майкрософт, могут использовать эти принципы независимо от того, где осуществляются управление учетными записями пользователей и аутентификация — в Active Directory или в Azure Active Directory. Hello следующих разделах содержатся дополнительные сведения о защите привилегированного доступа toosupport возможности Azure AD.

## <a name="azure-multi-factor-authentication"></a>Многофакторная идентификация Microsoft Azure;
tooincrease hello безопасности проверки подлинности администратора, должна требовать двухшаговую проверку перед предоставлением прав. Двухшаговая проверка — метод проверки того, кто именно требует использования hello не только имя пользователя и пароль. Он предоставляет дополнительный уровень безопасности toouser входа и транзакций.

Azure Multi-factor Authentication (MFA) — решения проверки двухэтапный корпорации Майкрософт, который помогает защитить access toodata и приложения удовлетворением спроса на простой процесс входа в. Она обеспечивает строгую аутентификацию с помощью ряда простых параметров проверки, включая:

- телефонные звонки;
- текстовые сообщения;
- уведомления для мобильных приложений;
- коды проверки для мобильных приложений.
- OATH-токены сторонних производителей.

Общие сведения о том, как работает Azure Multi-factor Authentication см. следующие видео hello.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]

Дополнительные сведения см. в записи блога [MFA for Office 365 and MFA for Azure](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/) (MFA для Office 365 и Azure).

## <a name="time-bound-privileges"></a>Временное ограничение привилегий
В некоторых организациях может оказаться, что пользователей с высоким уровнем привилегий оказалось слишком много. Пользователь могли быть добавлены toohello роли для определенного действия, например toosign службы, но не часто впоследствии использовать эти привилегии.

время выдержки hello toolower привилегий и повысить эффективность работы в их использования, ограничения пользователей tooonly перевода на свои права доступа «по требованию» (JIT), когда им нужен tooperform задачи. Для Azure Active Directory и Microsoft Online Services можно использовать [управление привилегированными пользователями (PIM) в Azure AD](http://aka.ms/AzurePIM).

![Панель мониторинга PIM][2]

## <a name="attack-detection"></a>Обнаружение атак
[Служба защиты идентификации Azure Active Directory](../active-directory-identityprotection.md) предоставляет единое представление для просмотра сведений обо всех представляющих риск событиях и возможных уязвимостях, которые могут повлиять на учетные записи вашей организации. На основе событий риска защиты идентификации вычисляет уровень риска для каждого пользователя, позволяя tooconfigure риск политики на основе защиты tooautomatically hello удостоверения вашей организации. Эти политики, а также другие элементы управления условного доступа, предоставляемые Azure Active Directory и EMS, можно автоматически блокировать пользователя hello или оптимизации, включая сброс пароля и принудительного применения многофакторной проверки подлинности.

![защиту идентификации Azure AD][3]

## <a name="conditional-access"></a>Условный доступ
С помощью элемента управления условного доступа Azure Active Directory проверяет hello определенных условий, выбранного для проверки подлинности пользователя, прежде чем разрешить доступ tooan приложения. Если эти условия выполнены, hello пользователя с проверкой подлинности и доступа toohello приложение, которому разрешен.

![Настройка правил условного доступа с использованием многофакторной проверки подлинности][4]

## <a name="related-articles"></a>Связанные статьи
* Включение [многофакторной идентификации Azure](../../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)
* Включение [Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-configure.md)
* Включение [защиты идентификации Azure AD](../active-directory-identityprotection.md)
* Включение [элементов управления условным доступом](../active-directory-conditional-access.md)

Дополнительные сведения о построении стратегия целиком разделе hello «обязанности клиента и стратегия» hello [Microsoft Cloud Security для архитекторов Enterprise](http://aka.ms/securecustomer) документа. Дополнительные сведения о привлечения tooassist службы Microsoft с любым из следующих разделов, обратитесь к представителю корпорации Майкрософт или посетите наш [кибербезопасности решений страницы](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx).

<!--Image references-->
[1]: ../media/active-directory-privileged-identity-management-configure/Search_PIM.png
[2]: ../media/active-directory-privileged-identity-management-configure/PIM_Dash.png
[3]: ../media/active-directory-identityprotection/29.png
[4]: ../media/active-directory-conditional-access/conditionalaccess-saas-apps.png
