---
title: "доступ локального tooon aaaConditional приложения - Azure AD | Документы Microsoft"
description: "Описание способа tooset условного доступа для приложений публикации toobe доступны удаленно с помощью прокси приложения Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 2e97722b-eb4e-4078-b607-9fed210d8a0f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 7bed25dd4ba17941e77d8c4b2b9ba4edcf0cf597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-conditional-access-in-azure-ad-application-proxy"></a>Работа с условным доступом в прокси приложения Azure AD

>[!NOTE]
>Эта статья относится toohello классический портал Azure, который выводится из эксплуатации. Мы рекомендуем использовать hello [портал Azure](https://portal.azure.com). В hello портал Azure для приложений, прокси-сервер приложения hello и те же возможности условного доступа как и любые другие приложения SaaS. toolearn Дополнительные сведения о условного доступа в разделе [приступить к работе с помощью условного доступа в Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).

Можно настроить доступ tooapplications условного доступа toogrant правила публикуются с использованием прокси приложения. Это позволяет:

* требовать многофакторную идентификацию для каждого приложения;
* требовать многофакторную идентификацию только в том случае, если пользователи не находятся на работе;
* Блокировать доступ приложения hello, если они не на работе пользователей

Эти правила могут быть применен tooall пользователей и групп, или только toospecific пользователей и групп. По умолчанию применяется правило hello tooall пользователей, имеющих доступ toohello приложения. Однако hello правило также может быть ограниченным toousers, которые являются членами определенной группы безопасности.  

Правила доступа оцениваются, когда пользователь обращается к федеративному приложению, использующему OAuth 2.0, OpenID Connect, SAML или WS-Federation. Кроме того правила доступа оцениваются с OAuth 2.0 и OpenID Connect, когда токен обновления используется tooacquire маркер доступа.

## <a name="conditional-access-prerequisites"></a>Необходимые условия для включения условного доступа
* Подписки tooAzure Active Directory Premium
* Федеративный или управляемый клиент Azure Active Directory.
* Федеративным клиентам требуется многофакторная идентификация (MFA)  
    ![Настройка правил доступа: требование многофакторной идентификации](./media/active-directory-application-proxy-conditional-access/application-proxy-conditional-access.png)

## <a name="configure-per-application-multi-factor-authentication"></a>Настройка многофакторной идентификации для каждого приложения
1. Войдите как администратор в hello классический портал Azure.
2. Перейдите в каталог tooActive и выберите hello каталог, в котором нужно tooenable прокси-сервера приложения.
3. Нажмите кнопку **приложений** и прокрутите вниз toohello **правила доступа** раздела. раздел правил доступа Hello отображается только для приложений, опубликованных с помощью прокси-сервера приложений, использующих федеративную проверку подлинности.
4. Включить правило hello, выбрав **включить правила доступа** слишком**на**.
5. Укажите hello пользователей и групп toowhom приветствия применяются правила. Используйте hello **добавить группу** кнопку tooselect одну или несколько групп, применяется правило доступа toowhich hello. Это диалоговое окно также можно использовать tooremove выбранные группы.  При выбранной tooapply toogroups правила hello hello правила доступа применяются только к пользователям, принадлежащим tooone из указанного hello групп безопасности.  

   * Проверьте группы безопасности tooexplicitly исключения из правила hello **за исключением** и укажите одну или несколько групп. Пользователи, являющиеся членами группы в hello, за исключением списка не требуется tooperform многофакторной проверки подлинности.  
   * Если пользователь был настроен с помощью функции многофакторной проверки подлинности пользователя hello, этот параметр имеет приоритет над hello правил многофакторной проверки подлинности приложения. Пользователь, который был настроен для многофакторной проверки подлинности пользователя является необходимые tooperform многофакторной проверки подлинности, даже если он был исключен из правил многофакторной проверки подлинности приложения hello. Узнайте больше о [многофакторной идентификации и пользовательских параметрах](../multi-factor-authentication/multi-factor-authentication.md).
6. Выберите правило доступа hello, требуется tooset:

   * **Требовать многофакторную проверку подлинности**: пользователи, применяются правила доступа toowhom являются многофакторной проверки подлинности требуется toocomplete прежде, чем доступ к hello приложения toowhich hello правило применяется.
   * **Требовать многофакторную проверку подлинности, если не на работе**: пользователей, приложение hello tooaccess из надежных IP-адрес не будет обязательным tooperform многофакторной проверки подлинности. Hello доверенные диапазоны IP-адресов можно настроить на странице параметров многофакторной проверки подлинности hello.
   * **Блокировать доступ, если не на работе**: пользователей, приложение hello tooaccess за пределами корпоративной сети не будет возможности tooaccess приложения hello.

## <a name="configuring-mfa-for-federation-services"></a>Настройка многофакторной проверки подлинности для служб федерации
Для федеративных клиентов многофакторная проверка подлинности (MFA) может быть выполнена с Azure Active Directory или hello локального сервера AD FS. По умолчанию многофакторная идентификация выполняется на любой странице, размещенной в Azure Active Directory. tooconfigure многофакторной проверки Подлинности в локальной среде выполнения Windows PowerShell и используйте hello – SupportsMFA свойство tooset hello модуля Azure AD.

Hello следующем примере показано, как tooenable локальной многофакторной проверки Подлинности с помощью hello [командлет Set-MsolDomainFederationSettings](https://msdn.microsoft.com/library/azure/dn194088.aspx) на приветствия клиента contoso.com:`Set-MsolDomainFederationSettings -DomainName contoso.com -SupportsMFA $true `

В дополнение toosetting этот флаг hello экземпляра федеративного клиента AD FS должен быть настроен tooperform многофакторной проверки подлинности. Следуйте инструкциям hello [развертывания Microsoft Azure многофакторной проверки подлинности в локальной](../multi-factor-authentication/multi-factor-authentication-get-started-server.md).

## <a name="see-also"></a>См. также
* [Работа с приложениями, поддерживающими утверждения](active-directory-application-proxy-claims-aware-apps.md)
* [Опубликуйте приложения с помощью прокси-сервера приложений.](active-directory-application-proxy-publish.md)
* [Включение единого входа](active-directory-application-proxy-sso-using-kcd.md)
* [Публикация приложений с помощью доменного имени](active-directory-application-proxy-custom-domains.md)

Для получения hello последние новости и обновления, посетите hello [блога прокси приложения](http://blogs.technet.com/b/applicationproxyblog/)
