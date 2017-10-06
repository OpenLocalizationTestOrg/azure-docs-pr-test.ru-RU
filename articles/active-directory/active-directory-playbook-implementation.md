---
title: "aaaAzure реализации репертуара подтверждения концепции Active Directory | Документы Microsoft"
description: "Ознакомление со сценариями управления удостоверениями и доступом и их реализация"
services: active-directory
keywords: "azure active directory, сборник тренировочных заданий, подтверждение концепции, PoC"
documentationcenter: 
author: dstefanMSFT
manager: asuthar
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/12/2017
ms.author: dstefan
ms.openlocfilehash: 4d61f1432d5f1c15cd88fda4824cf1c1de64c712
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-implementation"></a>Сборник тренировочных заданий по подтверждению концепции для Azure Active Directory. Реализация

## <a name="foundation---syncing-ad-tooazure-ad"></a>Foundation - синхронизации AD tooAzure AD 

Гибридное удостоверение — hello foundation для большинства hello корпоративных клиентов, которые уже имеют локального каталога. Hello цель — toointentionally тратить как меньше времени как значение hello возможных tooshow hello фактическое удостоверениями и доступом сценариев. 

| Сценарий | Стандартные блоки| 
| --- | --- |  
| [Расширение локальных удостоверений toohello облака](#extending-your-on-premises-identity-to-the-cloud) | [Синхронизация каталога. Синхронизация хэша паролей](active-directory-playbook-building-blocks.md#directory-synchronization---password-hash-sync-phs---new-installation) <br/>**Примечание.** Если у вас есть DirSync/ADSync или более ранние версии Azure AD Connect, этот шаг является необязательным. Для некоторых сценариев в этом руководстве может потребоваться более поздняя версия Azure AD Connect.  <br/>[Фирменная символика](active-directory-playbook-building-blocks.md#branding) | 
| [Назначение лицензий Azure AD с помощью групп](#assigning-azure-ad-licenses-using-groups) | [Групповое лицензирование](active-directory-playbook-building-blocks.md#group-based-licensing). |


### <a name="extending-your-on-premises-identity-toohello-cloud"></a>Расширение локальных удостоверений toohello облака 

1. Боб является администратором Active Directory hello в Contoso. Он возвращает удостоверение tooenable hello требование как служба для группы пользователей. После выполнения мастера Azure AD Connect hello удостоверения пользователей целевой hello доступны в облаке hello. 
2. Боб запрашивает Susie, один из пользователей целевой hello, tooaccess hello панели доступа Azure Active Directory и убедитесь, что она проверяет подлинность. Лилия видит страницу входа с фирменной символикой и пустую панель доступа, где можно включить последующий доступ к приложению.

### <a name="assigning-azure-ad-licenses-using-groups"></a>Назначение лицензий Azure AD с помощью групп 

1. Боб — hello глобальный администратор Azure AD и хочет tooallocate лицензии Azure AD tooa определенного набора пользователей как часть начальной внедрения hello Azure AD.
2. Боб создает группу для hello пилотных пользователей. 
3. Боб назначает hello лицензий toohello группы
4. В рамках своих обязанностей Susie, один из hello информационные работники, добавляется toohello группы безопасности
5. Через некоторое время Susie имеет доступ toohello Azure AD premium лицензирования. Это позволит несколько сценариев проверки Концепции hello позже.

## <a name="theme---lots-of-apps-one-identity"></a>Тема: большое количество приложений, одно удостоверение

| Сценарий | Стандартные блоки| 
| --- | --- |  
| [Интеграция приложений SaaS: федеративный единый вход](#integrate-saas-applications---federated-sso) | [Настройка федеративного единого входа SaaS](active-directory-playbook-building-blocks.md#saas-federated-sso-configuration) <br/>[Группы — делегированное владение](active-directory-playbook-building-blocks.md#groups---delegated-ownership) |
| [Интеграция приложений SaaS: единый вход с помощью пароля](#integrate-saas-applications---password-sso) | [Настройка единого входа SaaS с помощью пароля](active-directory-playbook-building-blocks.md#saas-password-sso-configuration) |
| [Единый вход и события жизненного цикла удостоверений](#sso-and-identity-lifecycle-events) | [SaaS и жизненный цикл удостоверений](active-directory-playbook-building-blocks.md#saas-and-identity-lifecycle). |
| [Защита учетных записей доступа tooShared](#secure-access-to-shared-accounts) | [Настройка общих учетных записей SaaS](active-directory-playbook-building-blocks.md#saas-shared-accounts-configuration). |
| [Безопасность удаленного доступа tooOn локальных приложений](#secure-remote-access-to-on-premises-applications) | [Настройка прокси приложения](active-directory-playbook-building-blocks.md#app-proxy-configuration). |
| [Синхронизация удостоверений LDAP tooAzure AD](#synchronize-ldap-identities-to-azure-ad) |  [Настройка универсального соединителя LDAP](active-directory-playbook-building-blocks.md#generic-ldap-connector-configuration). |

### <a name="integrate-saas-applications---federated-sso"></a>Интеграция приложений SaaS: федеративный единый вход 

1. Боб — hello глобальный администратор Azure AD и получает запрос от tootheir hello маркетинга отдел tooenable доступа экземпляра ServiceNow. Боб находит пошаговый учебник hello в документации по Azure AD и следующий за ним и делегаты hello назначение tooKevin приложения toohello пользователей, head hello отдела маркетинга. 
2. Кевин вошел в систему как владелец hello ServiceNow прав и назначает Susie toohello приложения. Также Кирилл отмечает, что профиль Лилии в ServiceNow был создан автоматически.
3. Susie является сотрудник отдела маркетинга hello. Она входит в tooazure AD и выполняет поиск всех приложений SaaS ему назначается tooin myapps портала. После этого она легко возвращает tooServiceNow доступа.
4. Hello отдела маркетинга хочет tooaudit, кто обращается к ServiceNow. Артем загружает отчет о действиях и отправляет его Кириллу по электронной почте.  

### <a name="sso-and-identity-lifecycle-events"></a>Единый вход и события жизненного цикла удостоверений

1. Susie принимает отпуск, и с корпоративной политикой hello локальной учетной записи AD является временной отключено. Susie не могут войти в tooAzure AD и поэтому недоступны для ServiceNow. 
2. Susie делает боковое перемещения из маркетингового tooSales. Кирилл из ServiceNow отменяет доступ для нее. Susie входит myapps hello azure ad, и она больше не видит hello ServiceNow плитки. Через 10 минут Кирилл подтверждает, что учетная запись Лилии была отключена с помощью консоли управления ServiceNow.

### <a name="integrate-saas-applications---password-sso"></a>Интеграция приложений SaaS: единый вход с помощью пароля

1. Алексей настраивает доступа tooAtlassian HipChat. HipChat имеет tooSusie SSO на ОСНОВЕ пароля, интеграции и предоставление доступа
2. Susie журналы портала myapps toohello и видит hello toodownload ссылку расширения обозревателя Azure AD IE, которое она загружает
3. При этом она получает запрос на ввод своих учетных данных для HipChat — имени пользователя и пароля. Это одноразовая операция, и после ее завершения, она должна tooHipChat доступа
4. Спустя несколько дней Лилия открывает портал MyApps и снова щелкает HipChat. В этот раз она получает прозрачный доступ.
5. Кевин владельцу приложения hello HipChat, хочет tooaudit, кто обращается к приложения hello. Артем загружает отчет аудита и отправляет его Кириллу по электронной почте. 

### <a name="secure-access-tooshared-accounts"></a>Защита учетных записей доступа tooShared 

1. Боб представляет дескриптор Twitter hello общей задачей является toosecure сотрудники отдела продаж hello. Он добавляет Twitter как приложение единого входа и присваивает его группа безопасности toohello hello Группа продаж. Он был задан hello учетные данные общего toohello учетная запись, и он предоставляет в системе hello. 
2. Совместное использование учетных данных Twitter больше не является доверенным, из-за toomultiple людей, с ним. Боб включает автоматическую смену пароля hello Twitter.
3. Susie член группы продаж hello входит портал myapps toohello и видит hello toodownload ссылку расширение обозревателя Azure AD IE. Она устанавливает его.
4. После нажатия кнопки, она получить прямой доступ к tooTwitter. Она не знает пароль hello.
5. Арнольд также является частью группы менеджеров по продажам hello. У него есть возможности Susie в шагах 3-4 hello
6. отдел продаж Hello хочет tooaudit, кто обращается к Twitter. Артем загружает отчет о действиях и отправляет его Кириллу по электронной почте. 

### <a name="secure-remote-access-tooon-premises-applications"></a>Безопасность удаленного доступа tooOn локальных приложений

1. Боб, hello Azure AD глобального администратора, оказался несколько запросов на tooaccess сотрудников tooenable несколько полезных локальных ресурсов, таких как приложения hello расходы, при удаленной работе. Он выполняет hello [документации прокси-сервера приложения](active-directory-application-proxy-enable.md) tooinstall соединителя и опубликовать расходы как приложение прокси приложения. 
2. Боб hello внешний расходы приложения URL-адрес совместно Susie, одного из сотрудников hello, которым необходим удаленный доступ. Она обращается к связи hello и после проверки подлинности для AAD, она является расходы приложение может tooaccess hello и продолжить toobe производительность при удаленном подключении. 
3. Боб затем продолжается hello toopublish дополнительных локальных приложений с помощью того же процесса и предоставления доступа toousers при необходимости. Он добавляет условного доступа и многофакторной проверки подлинности для hello более важных приложений, он публикует, tooensure дополнительную безопасность.

### <a name="synchronize-ldap-identities-tooazure-ad"></a>Синхронизация удостоверений LDAP tooAzure AD

1. У организации Артема сложная инфраструктура удостоверений. Большинство пользователей hello, сохраняются в Windows Server Active Directory домена службы (ADDS). Некоторыми из них управляет система отдела кадров внутри служб облегченного доступа к каталогам Active Directory (ADLDS).
2. Боб назначены для включения приложений tooSaaS доступ для всех пользователей (также они отсутствуют в ADDS).
3. Боб настраивает данные toopull универсальный соединитель LDAP из ADLDS в Azure AD Connect.
4. Боб создает правила синхронизации, чтобы пользователи LDAP заполняются в метавселенной и tooAzure AD
5. Лилия, являясь пользователем LDAP, входит в свое приложение SaaS с помощью синхронизированной идентификации.



> [!IMPORTANT] 
> Для использования этой расширенной конфигурации необходимо прежде ознакомиться с FIM/MIM. Дополнительные сведения о ее использовании в рабочей среде см. на странице [запросов на поддержку](https://support.microsoft.com/premier).



## <a name="theme---increase-your-security"></a>Тема: повышение уровня безопасности 

| Сценарий | Стандартные блоки| 
| --- | --- |  
| [Безопасный доступ к учетной записи администратора](#secure-administrator-account-access) | [Подтверждение многофакторной проверки подлинности в Azure с помощью телефонных звонков](active-directory-playbook-building-blocks.md#azure-multi-factor-authentication-with-phone-calls) |
| [Безопасный доступ к приложениям](#secure-access-to-applications) | [Условный доступ к приложениям SaaS](active-directory-playbook-building-blocks.md#mfa-conditional-access-for-saas-applications) |
| [Включение JIT-администрирования](#enable-just-in-time-jit-administration) | [Управление привилегированными пользователями](active-directory-playbook-building-blocks.md#privileged-identity-management-pim) |
| [Защита удостоверений в зависимости от рисков](#protect-identities-based-on-risk) | [Обнаружение событий риска](active-directory-playbook-building-blocks.md#discovering-risk-events) <br/>[Развертывание политик риска при входе в систему](active-directory-playbook-building-blocks.md#deploying-sign-in-risk-policies) |
| [Проверка подлинности без использования паролей с помощью сертификатов](#authenticate-without-passwords-using-certificate-based-authentication) | [Настройка проверки подлинности на основе сертификата](active-directory-playbook-building-blocks.md#configuring-certificate-based-authentication)

### <a name="secure-administrator-account-access"></a>Безопасный доступ к учетной записи администратора

1. Боб — hello глобальный администратор Azure AD. Он определил Стюарт как администратором службы hello. 
2. Боб настраивает учетную запись Стюарт tooalways требуют уровня безопасности hello tooimprove многофакторной проверки Подлинности
3. Стюарт ведет журнал toohello портал Azure и уведомления, что он должен tooregister его входа hello toocontinue номера телефона
4. Последующих входов в систему из Стюарт теперь защищены с помощью многофакторной проверки подлинности, и теперь он получает tooverify телефонный звонок свою подлинность.

### <a name="secure-access-tooapplications"></a>Tooapplications безопасный доступ

1. Кевин является владельцем бизнеса hello ServiceNow. Hello компании предполагает toologin этих пользователей с многофакторной проверки Подлинности при доступе к внешней корпоративной сети hello.
2. Боб, нашей глобальный администратор Azure AD, добавляет условного доступа политики toohello ServiceNow приложения tooenable многофакторной проверки Подлинности для внешнего доступа
3. Susie наш информационный работник входит Мои приложения портала и нажимает плитку ServiceNow hello. Теперь Лилия сталкивается с многофакторной проверкой подлинности.

### <a name="enable-just-in-time-jit-administration"></a>Включение JIT-администрирования

1. Артем и Виктор являются глобальными администраторами Azure AD. Они хотят tooenable JIT доступа toohello управления ролями и также tookeep записи во время использования hello hello привилегированным ролей.
2. Боб включает PIM в клиенте Azure AD hello и становится администратором безопасности hello. Он изменяет себе и членство в роли глобального администратора Стюарт с постоянными tooeligible.
3. Боб и Stuart теперь требуется активация роли через портал Azure hello перед выполнения изменяет tooAzure AD конфигурации. 

### <a name="protect-identities-based-on-risk"></a>Защита удостоверений в зависимости от рисков 

1. Лилия, информационный сотрудник, пытается выполнить вход с помощью Tor Browser. 
2. Виктор проверяет мониторинга hello Azure AD identity protection и видит Susie в имени входа с анонимных IP-адреса. Группа безопасности Hello требуется toochallenge таких обращается к пользователям с многофакторной проверки Подлинности
3. Боб включает политику защиты идентификации Azure AD toochallenge многофакторной проверки Подлинности для событий, средним или высоким риском
4. Проходит некоторое время и Лилия снова выполняет вход с помощью Tor Browser. На этот раз она увидит hello многофакторной проверки Подлинности запроса

### <a name="authenticate-without-passwords-using-certificate-based-authentication"></a>Проверка подлинности без использования паролей с помощью сертификатов

1. Артем является глобальным администратором финансового учреждения, в котором запрещено использование паролей в качестве фактора проверки подлинности для приложений.
2. Артем включает и принудительно применяет проверку подлинности сертификата в ADFS и Azure AD.
3. Susie во время доступа к приложению на запрос с использованием сертификата tooauthenticate

## <a name="theme---scale-with-self-service"></a>Тема: самостоятельное масштабирование

| Сценарий | Стандартные блоки| 
| --- | --- |  
| [Самостоятельный сброс пароля](#self-service-password-reset) | [Самостоятельный сброс пароля](active-directory-playbook-building-blocks.md#self-service-password-reset). |
| [SELF tooApplications доступ к службе](#self-service-access-to-applications) | [SELF tooApplications доступ к службе](active-directory-playbook-building-blocks.md#self-service-access-to-application-management) |

### <a name="self-service-password-reset"></a>Самостоятельный сброс пароля 

1. Боб является hello Azure AD глобального администратора и включает автоматическое управление паролями службы tooa подмножество пользователей, включая Susie. 
2. Susie ведет журнал toomyapps портала и см. в разделе tooregister сообщение своей сведения о безопасности для события сброса пароля в будущем.
3. Через несколько дней Лилия забывает пароль и сбрасывает его с помощью портала Azure AD.

### <a name="self-service-access-tooapplications"></a>SELF tooApplications доступ к службе 

1. Кевин является владельцем бизнеса hello ServiceNow. Он хочет пользователи слишком «зарегистрироваться» для его по требованию, вместо добавления их все за один раз
2. Боб, нашей глобальный администратор Azure AD, изменяет tooenable приложения hello ServiceNow запросы самообслуживания
3. Susie наш информационный работник входит Мои приложения портала и щелчки кнопку «Добавить дополнительные приложения» hello и увидеть ServiceNow является одним из рекомендуется приложения hello. Затем она переходит назад toomy приложения портала и приложение hello-ServiceNow.

[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]