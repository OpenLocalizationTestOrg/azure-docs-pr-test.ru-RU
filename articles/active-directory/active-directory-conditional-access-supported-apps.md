---
title: "aaaApplications и браузеры, использующие правила условного доступа в Azure Active Directory | Документы Microsoft"
description: "С помощью элемента управления условного доступа Azure Active Directory проверяет для конкретных условий при проверке подлинности пользователя hello и tooallow доступ к приложениям."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 62349fba-3cc0-4ab5-babe-372b3389eff6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: ca20853bb9f4b22d0b88ddd2f051d658e0d88cf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="applications-and-browsers-that-use-conditional-access-rules-in-azure-active-directory"></a>Приложения и браузеры, использующие правила условного доступа в Azure Active Directory

Правила условного доступа поддерживаются в приложениях, подключенных к Azure Active Directory (Azure AD), предварительно интегрированных федеративных приложениях, предоставляемых по модели "Программное обеспечение как услуга" (SaaS), приложениях, использующих единый вход (SSO) с паролем, в бизнес-приложениях, а также в приложениях, использующих прокси-сервер приложений Azure AD. Подробный список приложений с поддержкой условного доступа см. в разделе [Службы, включаемые с условным доступом](active-directory-conditional-access-technical-reference.md). Условный доступ поддерживается в мобильных и классических приложениях, в которых используется современная проверка подлинности. В этой статье описан принцип работы условного доступа в мобильных и классических приложениях.

Современная проверка подлинности выполняется на странице входа Azure AD в приложение. Войдя на эту страницу, пользователь получает запрос на выполнение многофакторной идентификации. Будет выведено сообщение, если пользователь hello доступ будет заблокирован. Современная проверка подлинности является обязательным для hello tooauthenticate устройства в Azure AD, чтобы политики условного доступа на основе устройств.

Это важные tooknow приложения, которые можно использовать правила условного доступа и действия, которые могут потребоваться tootake toosecure другие точки входа приложения hello.

## <a name="applications-that-use-modern-authentication"></a>Приложения, использующие современную проверку подлинности
> [!NOTE]
> Если в Azure AD и Office 365 используется аналогичная политика условного доступа, необходимо настроить обе политики. Это будет применена, например, tooconditional политик доступа для Exchange Online или SharePoint Online.
>
>

Hello следующие приложения поддерживают условный доступ для Office 365 и другие приложения Azure AD-подключенной службы:


| Целевая служба| Платформа| Приложение |
| --- | --- | --- |
| Все службы приложения "Мои приложения"| Android и iOS| MFA и политика расположения для приложений Политики на основе устройств не поддерживаются.|
| Удаленная служба приложений Azure| Windows 10, Windows 8.1, Windows 7, iOS, Android и Mac OS X| Azure RemoteApp|
| Dynamics CRM| Windows 10, Windows 8.1, Windows 7, iOS и Android| Приложение Dynamics CRM|
| Microsoft Teams| Windows 10, Windows 8.1, Windows 7, iOS, Android и Mac OS X| Microsoft Teams Services — контролируют все службы, которые поддерживают Microsoft Teams, и все их клиентские приложения: для Windows Desktop, MAC OS X, iOS, Android, WP, а также веб-клиент.|
| Office 365 Exchange Online| Windows 10| Приложения "Почта", "Календарь" и "Люди", Outlook 2016, Outlook 2013 (с современной проверкой подлинности), Skype для бизнеса (с современной проверкой подлинности)|
| Office 365 Exchange Online| Windows 8.1, Windows 7| Outlook 2016, Outlook 2013 (с современной проверкой подлинности), Skype для бизнеса (с современной проверкой подлинности)|
| Office 365 Exchange Online| iOS| Приложение Outlook Mobile|
| Office 365 Exchange Online| Mac OS X| Outlook 2016 (Office для macOS)|
| Office 365 SharePoint Online| Windows 10| Приложения Office 2016, Office универсальных приложений Office 2013 (с современной проверкой подлинности), OneDrive синхронизации клиента (см. [заметки](https://support.office.com/en-US/article/Azure-Active-Directory-conditional-access-with-the-OneDrive-sync-client-on-Windows-028d73d7-4b86-4ee0-8fb7-9a209434b04e)), поддержки групп Office, запланированных для будущих hello, поддержки приложений SharePoint запланировано в будущем hello|
| Office 365 SharePoint Online| Windows 8.1, Windows 7| Приложения Office 2016, Office 2013 (с современной проверкой подлинности), клиент синхронизации OneDrive (см. [заметки](https://support.office.com/en-US/article/Azure-Active-Directory-conditional-access-with-the-OneDrive-sync-client-on-Windows-028d73d7-4b86-4ee0-8fb7-9a209434b04e))|
| Office 365 SharePoint Online| iOS, Android| Мобильные приложения Office|
| Office 365 SharePoint Online| Mac OS X| Office 2016 для macOS (только Word, Excel, PowerPoint, OneNote). OneDrive для бизнеса поддержки, запланированных для будущих hello|
| Office 365 Yammer| Windows 10, iOS, Android| Приложение Office Yammer|
| Служба PowerBI| Windows 10, Windows 8.1, Windows 7 и iOS.| Приложение PowerBI. приложение Hello Power BI для Android в настоящее время не поддерживает условного доступа на основе устройств.|
| Visual Studio Team Services| Windows 10, Windows 8.1, Windows 7, iOS и Android| Приложение Visual Studio Team Services|








## <a name="applications-that-do-not-use-modern-authentication"></a>Приложения, не использующие современную проверку подлинности
В настоящее время необходимо использовать другие tooapps доступа tooblock методы, не использующих современную проверку подлинности. Это связано с тем, что при условном доступе правила доступа не применяются к приложениям, не использующим современную проверку подлинности. Это в первую очередь касается доступа к Exchange и SharePoint. В предыдущих версиях этих приложений используются более старые протоколы контроля доступа.

### <a name="control-access-in-office-365-sharepoint-online"></a>Управление доступом в Office 365 SharePoint Online
Прежних версий протоколов для доступа к SharePoint можно отключить с помощью командлета Set SPOTenant hello. Используйте этот командлет tooprevent клиентов Office, использующие протоколы проверки подлинности несовременных доступ к ресурсам SharePoint Online.

**Пример команды**: `Set-SPOTenant -LegacyAuthProtocolsEnabled $false`

### <a name="control-access-in-office-365-exchange-online"></a>Управление доступом в Office 365 Exchange Online
В Exchange существуют две основные категории протоколов. Просмотрите hello следующие параметры, а затем выберите hello политики, которая подходит для вашей организации.

* **Exchange ActiveSync.** По умолчанию политики условного доступа для многофакторной идентификации и расположения не применяются к Exchange ActiveSync. Необходимо службы toothese tooprotect доступа путем настройки политики Exchange ActiveSync напрямую или с помощью блокирования Exchange ActiveSync с помощью служб федерации Active Directory (AD FS) правила.
* **Устаревшие протоколы.** Устаревшие протоколы можно заблокировать с помощью служб федерации Active Directory. Это блокирует клиентов Office tooolder доступа, например Office 2013 без включить современную проверку подлинности и более ранних версиях Office.

### <a name="use-ad-fs-tooblock-legacy-protocol"></a>Использовать устаревший протокол tooblock AD FS
Можно использовать следующий пример выдачи авторизации правила tooblock устаревший протокол доступа на уровне hello AD FS hello. Выберите одну из двух распространенных конфигураций.

#### <a name="option-1-allow-exchange-activesync-and-allow-legacy-apps-but-only-on-hello-intranet"></a>Вариант 1: Разрешить Exchange ActiveSync и разрешить приложений прежних версий, но только в интрасети hello
Применяя следующие три правила toohello hello AD FS, проверяющая сторона отношения доверия для Microsoft Office 365 Identity Platform трафика Exchange ActiveSync и браузера и современные способы проверки подлинности трафика, имеют доступ. Устаревшие приложения изолированы от hello экстрасети.

##### <a name="rule-1"></a>Правило 1
    @RuleName = "Allow all intranet traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "true"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

##### <a name="rule-2"></a>Правило 2
    @RuleName = "Allow Exchange ActiveSync"
    c1:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value == "Microsoft.Exchange.ActiveSync"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

##### <a name="rule-3"></a>Правило 3
    @RuleName = "Allow extranet browser and browser dialog traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

#### <a name="option-2-allow-exchange-activesync-and-block-legacy-apps"></a>Вариант 2. Разрешить Exchange ActiveSync и блокировать устаревшие приложения.
Применяя следующие три правила toohello hello AD FS, проверяющая сторона отношения доверия для Microsoft Office 365 Identity Platform трафика Exchange ActiveSync и браузера и современные способы проверки подлинности трафика, имеют доступ. Доступ устаревших приложений из любого расположения будет заблокирован.

##### <a name="rule-1"></a>Правило 1
    @RuleName = "Allow all intranet traffic only for browser and modern authentication clients"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "true"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


##### <a name="rule-2"></a>Правило 2
    @RuleName = "Allow Exchange ActiveSync"
    c1:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value == "Microsoft.Exchange.ActiveSync"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


##### <a name="rule-3"></a>Правило 3
    @RuleName = "Allow extranet browser and browser dialog traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


## <a name="supported-browsers-for-device-based-policies"></a>Поддерживаемые браузеры для политик на основе устройств 

Только вы можете получить доступ для устройств на основе политик, проверьте соответствие устройства и присоединения к домену при Azure AD можно идентифицировать и проверять подлинность устройств hello. Во время большинство проверки, такие как расположение и рабочих многофакторной проверки Подлинности для большинства устройств и браузеров устройства с политиками версии hello операционной системы и браузеры, перечисленные ниже. Доступ будет заблокирован на неподдерживаемые браузеры или hello операционных систем для пользователей, если период политики устройств. 

| ОС                     | Браузеры                 | Поддержка     |
| :--                    | :--                      | :-:         |
| Windows 10                 | IE, Edge                 | ![Проверка][1] |
| Windows 10                 | Chrome                   | Предварительный просмотр     |
| Windows 8, Windows 8.1            | Internet Explorer, Chrome               | ![Проверка][1] |
| Windows 7                  | Internet Explorer, Chrome               | ![Проверка][1] |
| iOS                    | Safari                   | ![Проверка][1] |
| Android                | Chrome                   | ![Проверка][1] |
| Windows Phone          | IE, Edge                 | ![Проверка][1] |
| Windows Server 2016    | IE, Edge                 | ![Проверка][1] |
| Windows Server 2016    | Chrome                   | Скоро |
| Windows Server 2012 R2 | Internet Explorer, Chrome               | ![Проверка][1] |
| Windows Server 2008 R2 | Internet Explorer, Chrome               | ![Проверка][1] |
| MacOS                 | Safari                   | ![Проверка][1] |
| MacOS                 | Chrome                   | Скоро |

> [!NOTE]
> Для поддержки Chrome, необходимо использовать создатели центра обновления Windows 10 и расширение hello установки найдено [здесь](https://chrome.google.com/webstore/detail/windows-10-accounts/ppnbnpeolgkicgegkbkbjmhlideopiji).
>
>

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения см. в разделе [Условный доступ в Azure Active Directory](active-directory-conditional-access.md).




<!--Image references-->
[1]: ./media/active-directory-conditional-access-supported-apps/ic195031.png


