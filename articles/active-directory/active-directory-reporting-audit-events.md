---
title: "события отчета об аудите aaaAzure Active Directory | Документы Microsoft"
description: "События, подлежащие аудиту, которые доступны для просмотра и загрузки в Azure Active Directory"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 307eedf7-05bc-448d-a84d-bead5a4c5770
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 4a84cce2be56bde006164abf10ad1e72ca6e99bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-audit-report-events"></a>События отчета аудита Azure Active Directory
*Данная документация является частью hello [Azure Active Directory руководство по отчетам](active-directory-reporting-guide.md).*

Hello отчет об аудите Azure Active Directory позволяет клиентам определить привилегированные действия, которые возникли в своем Azure Active Directory. Привилегированные действия включают повышение изменения (например, Создание роли или сброс пароля), изменение конфигурации политики (например, политики паролей) или toodirectory изменений конфигурации (например, изменения toodomain параметры федерации). Hello отчеты предоставляют запись аудита hello hello событий имени субъекта hello, выполнившего действие hello, hello целевой ресурс влияет изменение hello и hello даты и времени (UTC). Клиенты, могут tooretrieve hello список событий аудита для их Azure Active Directory через hello [портала Azure](https://portal.azure.com/), как описано в [просмотреть журналы аудита](active-directory-reporting-azure-portal.md).

## <a name="list-of-audit-report-events"></a>Список событий отчета аудита
<!--- audit event descriptions should be in hello past tense --->

| События | Описание события |
| --- | --- |
| **Пользовательские события** | |
| Добавить пользователя |Добавить каталог toohello пользователя. |
| Удаление пользователя |Удалить пользователя из каталога hello. |
| Задание свойств лицензии |Задайте свойства hello лицензий для пользователя в каталоге hello. |
| Сброс пароля пользователя |Сброс пароля hello для пользователя в каталоге hello. |
| Смена пароля пользователя |Изменить пароль пользователя в каталоге hello hello. |
| Изменение лицензии пользователя |Изменить назначенные tooa пользователя в каталоге hello hello лицензии. какие лицензии были обновлены, просмотрите hello toosee [обновление пользователя](#update-user-attributes) свойства ниже |
| Обновление пользователя |Обновить пользователя в каталоге hello. [ниже](#update-user-attributes) . |
| Установка принудительной смены пароля пользователя |Свойства hello, требующем toochange пользователя пароль имени входа. |
| Обновление учетных данных пользователя |Пароль пользователя измененные hello |
| **События группы** | |
| Добавление группы |Создать группу в каталоге hello. |
| Обновление группы |Обновить группу в каталоге hello. toosee были обновлены какие свойства группы, ссылаться слишком[аудиту свойства группы](#update-group-attributes) hello ниже в разделе |
| Удаление группы |Удалить группу из каталога hello. |
| CreateGroupSettings |Создание параметров группы. |
| UpdateGroupSettings |Обновление параметров группы. toosee обновлены какие параметры группы, ссылаться слишком[аудиту свойства группы](#update-group-attributes) hello ниже в разделе |
| DeleteGroupSettings |Удаление параметров группы. |
| SetGroupLicense |Настройка лицензии для группы. |
| SetGroupManagedBy |Задать toobe группы управляемых пользователем |
| AddGroupMember |Добавлен элемент toogroup |
| RemoveGroupMember |Удаление участника группы |
| AddGroupOwner |Toogroup добавленного владельцев |
| RemoveGroupOwner |Удаление владельца группы. |
| **События приложения** | |
| Добавление субъекта-службы |Добавить каталог toohello участника службы. |
| Удаление субъекта-службы |Удалить участника службы из каталога hello. |
| Добавление учетных данных субъекта-службы |Участник службы tooa добавленных учетных данных. |
| Удаление учетных данных субъекта-службы |Удалены учетные данные из субъекта-службы. |
| Добавление записи делегирования |Создан [OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) в каталоге hello. |
| Установка записи делегирования |Обновить [OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) в каталоге hello. |
| Удаление записи делегирования |Удалить [OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) в каталоге hello. |
| **События роли** | |
| Добавить tooRole член роли |Добавить роли каталога tooa пользователя. |
| Удаление участника роли из роли |Удален пользователь из роли каталога. |
| AddRoleDefinition |Добавление определения роли. |
| UpdateRoleDefinition |Обновление определения роли. Параметры роли были обновлены, toosee ссылаться слишком[свойства определения роли для аудита](#update-role-definition-attributes) hello ниже в разделе |
| DeleteRoleDefinition |Удаление определения роли. |
| AddRoleAssignmentToRoleDefinition |Добавить определение toorole назначения роли. |
| RemoveRoleAssignmentFromRoleDefinition |Удаление назначения роли из определения роли. |
| AddRoleFromTemplate |Добавление роли на основе шаблона. |
| UpdateRole |Обновление роли. |
| AddRoleScopeMemberToRole |Добавлен элемент области toorole. |
| RemoveRoleScopedMemberFromRole |Удаление участника с заданной областью из роли. |
| **События устройства (все новые события)** | |
| AddDevice |Добавление устройства. |
| UpdateDevice |Обновление устройства. какие свойства устройства были обновлены, toosee ссылаться слишком[свойства устройства Audited](#update-device-attributes) hello ниже в разделе |
| DeleteDevice |Удаление устройства. |
| AddDeviceConfiguration |Добавление конфигурации устройства. |
| UpdateDeviceConfiguration |Обновление конфигурации устройства. какие свойства конфигурации устройства были обновлены, toosee ссылаться слишком[свойства конфигурации устройства Audited](#update-device-configuration-attributes) hello ниже в разделе |
| DeleteDeviceConfiguration |Удаление конфигурации устройства. |
| AddRegisteredOwner |Добавить toodevice зарегистрированного пользователя. |
| AddRegisteredUsers |Добавить toodevice зарегистрированных пользователей. |
| RemoveRegisteredOwner |Удаление зарегистрированного владельца устройства. |
| RemoveRegisteredUsers |Удаление зарегистрированных пользователей устройства. |
| RemoveDeviceCredentials |Удаление учетных данных устройства. |
| **События B2B** | |
| Передан пакет приглашений. |Администратор передал файл, содержащий toobe приглашения отправлено toopartner пользователей. |
| Обработан пакет приглашений. |Файл, содержащий приглашения пользователей toopartner была обработана. |
| Приглашение внешнего пользователя. |Внешний пользователь был приглашенных toohello каталога. |
| Приглашение внешнего пользователя активировано. |Внешний пользователь активирован каталогов toohello приглашения. |
| Добавьте toogroup внешнего пользователя. |Внешний пользователь назначил tooa группу в каталоге hello. |
| Назначьте tooapplication внешнего пользователя. |Внешний пользователь назначил приложения tooan прямой доступ. |
| Создание вирусного клиента. |Новый клиент был создан в Azure AD активации приглашения hello. |
| Создание вирусного пользователя. |Пользователь будет создана в существующий клиент в Azure AD при активации приглашения hello. |
| **Административные единицы (все новые события)** | |
| AddAdministrativeUnit |Добавление административной единицы. |
| UpdateAdministrativeUnit |Обновление административной единицы. toosee, какие свойства административной единицы, были обновлены, см. слишком[аудит администратора свойства устройства](#update-administrative-unit-attributes) hello ниже в разделе |
| DeleteAdministrativeUnit |Удаление административной единицы. |
| AddMemberToAdministrativeUnit |Добавьте модуль tooadministrative член. |
| RemoveMemberFromAdministrativeUnit |Удаление участника из административной единицы. |
| **События каталога** | |
| Добавление партнера toocompany |Добавить каталог toohello партнера. |
| Удаление партнера из компании |Удалить участника из каталога hello. |
| DemotePartner |Изменение типа партнера. |
| Добавление домена toocompany |Добавить каталог toohello домена. |
| Удаление домена из компании |Домен удален из каталога hello. |
| Обновление домена |Обновление домена в каталоге hello. toosee, какие свойства домена были обновлены, см. слишком[свойства домена для аудита](#update-domain-attributes) hello ниже в разделе |
| Установка проверки подлинности домена |Изменить hello домена по умолчанию hello компании. |
| Установка контактных данных компании |Выполнена настройка контактов для компании. Сюда относятся адреса электронной почты для маркетинга, а также технические уведомления о Microsoft Online Services. |
| Установка параметров федерации для домена |Обновленные параметры hello федерации для домена. |
| Проверка домена |Проверенный домен в каталоге hello. |
| Проверка домена с помощью электронной почты |Проверенный домен в каталоге hello, с помощью проверки адреса электронной почты. |
| Установка флага DirSyncEnabled для компании |Задайте для свойства hello, обеспечивающий каталог Azure AD Sync. |
| Установка политики паролей |Установлено ограничение на длину и символы для паролей пользователей. |
| Установка информации о компании |Hello обновленные сведения уровня компании. В разделе hello [Get-MsolCompanyInformation](https://msdn.microsoft.com/library/azure/dn194126.aspx) командлет PowerShell для получения дополнительных сведений. |
| SetCompanyAllowedDataLocation |Задание расположения данных организации. |
| SetCompanyDirSyncEnabled |Установка флага DirSyncEnabled. |
| SetCompanyDirSyncFeature |Установка компонента DirSync. |
| SetCompanyInformation |Настройка информации об организации. |
| SetCompanyMultiNationalEnabled |Включение функции многонациональности для организации. |
| SetDirectoryFeatureOnTenant |Установка поддержки каталога в клиенте. |
| SetTenantLicenseProperties |Задание свойств лицензии клиента. |
| CreateCompanySettings |Создание параметров организации. |
| UpdateCompanySettings |Обновление параметров организации. какие свойства компании были обновлены, toosee ссылаться слишком[аудиту свойства компании](#update-company-attributes) hello ниже в разделе |
| DeleteCompanySettings |Удаление параметров организации. |
| SetAccidentalDeletionThreshold |Задание порогового значения случайного удаления. |
| SetRightsManagementProperties |Установка свойств управления правами. |
| PurgeRightsManagementProperties |Очистка свойств управления правами. |
| UpdateExternalSecrets |Обновление внешних секретов. |
| **События политики (все новые события)** | |
| AddPolicy |Добавление политики. |
| UpdatePolicy |Обновление политики. |
| DeletePolicy |Удаление политики. |
| AddDefaultPolicyApplication |Добавьте tooapplication политики. |
| AddDefaultPolicyServicePrincipal |Добавление участника tooservice политики. |
| RemoveDefaultPolicyApplication |Удаление политики приложения. |
| RemoveDefaultPolicyServicePrincipal |Удаление политики субъекта-службы. |
| RemovePolicyCredentials |Удаление учетных данных политики. |

## <a name="audit-report-retention"></a>Хранение отчетов аудита

Hello самые последние сведения о хранении см. в разделе [политики хранения отчетов Azure Active Directory](active-directory-reporting-retention.md).


Для клиентов, заинтересованных в хранения их события аудита в течение более длительного хранения hello Reporting API может быть используется tooregularly запроса событий аудита в отдельное хранилище данных. В разделе [Приступая к работе с hello Reporting API](active-directory-reporting-api-getting-started.md) подробные сведения.

## <a name="properties-included-with-each-audit-event"></a>Свойства каждого события аудита
| Свойство | Описание |
| --- | --- |
| Дата и время |Hello Дата и время, которые hello событий аудита |
| Субъект |Hello пользователя или участника-службы, выполнившего действие hello |
| Действие |выполненное действие Hello |
| Цель |Hello пользователя или участника-службы, выполняется действие hello |

## <a name="update-user-attributes"></a>Атрибуты события «Обновление пользователя»
событие аудита Hello «обновление пользователя» включает дополнительные сведения о какие атрибуты пользователя были обновлены. Для каждого атрибута оба hello предыдущее значение и новое значение hello включено.

| Атрибут | Описание |
| --- | --- |
| AccountEnabled |Hello пользователь может войти. |
| AssignedLicense |Все лицензии, назначенные toohello пользователя. |
| AssignedPlan |Планы обслуживания, возникающие в результате лицензий hello назначенный пользователь toohello. |
| LicenseAssignmentDetail |Сведения о лицензии назначенный пользователь toohello. Для экземпляра Если был выполнен на основе группы лицензирования, эти права включают hello группу, предоставляются hello лицензии. |
| Мобильные приложения |Hello на мобильный телефон пользователя. |
| OtherMail |Здравствуйте пользователя запасной адрес электронной почты. |
| OtherMobile |Здравствуйте, альтернативный мобильный телефон пользователя. |
| StrongAuthenticationMethod |Список способов проверки подлинности настроен пользователем hello многофакторной проверки подлинности, например код голосовой звонок, SMS или проверки из мобильного приложения. |
| StrongAuthenticationRequirement |Многофакторная проверка подлинности требуется, включена или отключена для этого пользователя. |
| StrongAuthenticationUserDetails |Hello пользователя телефона электронной почты и номера телефонных номеров, альтернативный адрес, используемый для многофакторной проверки подлинности и проверки для сброса пароля. |
| StrongAuthenticationPhoneAppDetail |Приложения phone forof детализации зарегистрированные tooperform 2FA входа |
| TelephoneNumber |номер телефона пользователя Hello. |
| AlternativeSecurityId |Альтернативный идентификатор безопасности для hello объекта. |
| CreationType |Метод создания hello пользователя (либо по приглашениям популярный). |
| InviteTicket |Список билеты приглашения для пользователя hello. |
| InviteReplyUrl |Список URL-адресов tooreply принять приглашение. |
| InviteResources |Приглашен список ресурсов toowhich hello пользователя. |
| LastDirSyncTime |Время последнего hello объекта был обновлен, поскольку синхронизация из заслуживающих доверия hello (клиента или локального) каталога. |
| MSExchRemoteRecipientType |Сопоставляет типы tooMSO получателей. См. слишком https://msdn.microsoft.com/library/microsoft.office.interop.outlook.recipient.type.aspx [MSO типы получателей] для получателей типов |
| PreferredDataLocation |Здравствуйте, предпочтительным хранилищем для hello пользователя, группы, контакта, общих папок или данных на устройстве. |
| ProxyAddresses |Hello адрес, на который распознается объекта получателя Exchange Server в другую почтовую систему. |
| StsRefreshTokensValidFrom |Содержит сведения об отзыве маркера обновления. Все маркеры обновления, выданные до этого времени службой маркеров безопасности, считаются просроченными. |
| UserPrincipalName |Здравствуйте, имя участника-пользователя — это Интернет-входа имя пользователя. |
| UserState |Состояние пользователя: ожидается утверждение, ожидается принятие, принято, ожидается проверка. |
| UserStateChangedOn |Отметка времени последнего изменения tooUserState. Использовать рабочие процессы tootrigger жизненного цикла. |
| UserType |Тип пользователя. Участник (0), гость (1), вирусный пользователь (2). |

## <a name="update-group-attributes"></a>Атрибуты "Обновление группы"
| Атрибут | Описание |
| --- | --- |
| Классификация |Классификация Hello единой группы (HBI, MBI, и т. д.). |
| Описание |Понятное описательное фраз о hello объекта. |
| DisplayName |отображаемое имя Hello объекта |
| DirSyncEnabled |Указывает, происходит ли синхронизация из доверенного каталога (пользовательского, локального). |
| GroupLicenseAssignment |Назначение лицензии группы. |
| GroupType |Тип группы, единая (0). |
| IsMembershipRuleLocked |Указывает, что hello свойство MembershipRule службой управления группами самообслуживания hello и не может быть изменен пользователями. Применимо только toogroups, где GroupType включает GroupType.DynamicMembership |
| IsPublic |Флаг tooindicate, если группа hello открытого и закрытого. |
| LastDirSyncTime |Время последнего hello объекта была обновлена в результате синхронизация из заслуживающих доверия hello (в локальной среде клиента), каталог. |
| Mail |Основной адрес электронной почты. |
| MailEnabled |Указывает, имеет ли эта группа адрес электронной почты. |
| MailNickname |Моникер объекта адресной книги, обычно hello часть его имени электронной почты, предшествующую hello «@» символов. |
| MembershipRule |Строка выражения hello критериев, используемых hello управления группами самообслуживания службы toodetermine, какие члены должны принадлежать к группе toothis. См. также атрибут IsMembershipRuleLocked. Применимо только toogroups которой GroupType включает GroupType.DynamicMembership. |
| MembershipRuleProcessingState |Значение перечисления определены службой управления группами самообслуживания "hello" Определение hello состояние членства обработки для этой группы. Применимо только toogroups которой GroupType включает GroupType.DynamicMembership. |
| ProxyAddresses |Hello адрес, на который распознается объекта получателя Exchange Server в другую почтовую систему. |
| RenewedDateTime |Запись о событии последнего обновления группы с меткой времени. |
| SecurityEnabled |Указывает, является ли членство в группе hello может влияют на решения об авторизации. |
| WellKnownObject |Помечает объект каталога как предварительно определенный набор. |

## <a name="update-device-attributes"></a>Атрибуты "Обновление устройства"
| Атрибут | Описание |
| --- | --- |
| AccountEnabled |Указывает, может ли субъект безопасности выполнять проверку подлинности. |
| CloudAccountEnabled |Указывает, может ли субъект безопасности выполнять проверку подлинности. Написано с InTune, когда устройство hello управляется локально. |
| CloudDeviceOSType |Тип устройства hello на основании hello операционной системы, например Windows RT, iOS. Если задано в облачной службе (например, Windows Intune), этот атрибут становится основным сервером в каталоге hello для DeviceOSType. |
| CloudDeviceOSVersion |Версия ОС hello. Если задано в облачной службе (например, Windows Intune), этот атрибут становится основным сервером в каталоге hello для DeviceOSVersion. |
| CloudDisplayName |Значение атрибута LDAP displayName hello. Если задано в облачной службе (например, Windows Intune), этот атрибут становится основным сервером в каталоге hello displayName. |
| CloudCreated |Указывает, был ли создан объект hello, облачные службы. |
| CompliantUntil |Время, до которого устройство считается соответствующим. |
| DeviceMetadata |Пользовательские метаданные для hello устройства |
| DeviceObjectVersion |Этот атрибут является версия схемы используется tooidentify hello hello устройства. |
| DeviceOSType |Тип устройства hello на основании hello операционной системы, например Windows RT, iOS. Написанное hello службы регистрации и предполагаемого toobe обновлен hello службы управления MDM или STS светло-служба управления. |
| DeviceOSVersion |Версия ОС hello. Написанное hello службы регистрации и предполагаемого toobe обновлен hello службы управления MDM или STS светло-служба управления. |
| DevicePhysicalIds |Многозначный атрибут предназначен toostore идентификаторы hello физического устройства. Сюда могут входить идентификаторы BIOS, TPM-отпечатки, идентификаторы оборудования и т. д. |
| DirSyncEnabled |Указывает, происходит ли синхронизация из доверенного каталога (пользовательского, локального). |
| DisplayName |отображаемое имя Hello объекта |
| IsCompliant |Этот атрибут представляет состояние управления мобильными устройствами используется toomanage hello hello устройства. |
| IsManaged |Этот атрибут используется tooindicate hello устройство управляется службой cloud MDM. |
| LastDirSyncTime |Время последнего hello объекта был обновлен, поскольку синхронизация из заслуживающих доверия hello (в локальной среде клиента), каталог. |

## <a name="update-device-configuration-attributes"></a>Атрибуты Update Device Configuration (Обновление конфигурации устройства)
| Атрибут | Описание |
| --- | --- |
| MaximumRegistrationInactivityPeriod |Hello максимальное количество дней устройство может оставаться неактивным, считался для удаления. |
| RegistrationQuota |Использовать политику toolimit hello количество регистраций устройства, разрешенное для одного пользователя. |

## <a name="update-service-principal-configuration-attributes"></a>Атрибуты Update Service principal Configuration (Обновление конфигурации субъекта-службы)
| Атрибут | Описание |
| --- | --- |
| AccountEnabled |Указывает, может ли субъект безопасности выполнять проверку подлинности. |
| AppPrincipalId |Внешняя определяемая приложением идентификация субъекта безопасности. |
| DisplayName |отображаемое имя Hello объекта |
| ServicePrincipalName |Имя участника-службы, содержащий «имя/authority» где имя задает значение класса приложения и центра содержит по крайней мере имя узла [: порт] или «имя», идентификатор участника службы hello. |

## <a name="update-app-attributes"></a>Атрибуты "Обновление приложения"
| Атрибут | Описание |
| --- | --- |
| AppAddress |набор адресов (перенаправление URL-адреса), назначенных субъекту-службе tooa Hello. |
| AppId |Идентификатор приложения hello приложения |
| AppIdentifierUri |Приложение URI, который идентифицирует приложение hello.  Обычно это URL-адрес приложения hello. |
| AppLogoUrl |Hello URL-адрес для изображения эмблемы приложения hello, хранящихся в CDN. |
| AvailableToOtherTenants |Приложение true hello является многопользовательского приложения (т. е. может использоваться для других клиентов). |
| DisplayName |Hello отображаемое имя для имени приложения |
| Entitlement |Список прав приложения. |
| ExternalUserAccountDelegationsAllowed |Флаг, указывающий, является ли приложение resource доверенным и может ли создать записи делегирования для внешних учетных записей пользователей. |
| GroupMembershipClaims |членство в группе Hello утверждений политики. |
| PublicClient |Значение true, если клиент hello не позволяет хранить секретный (т. е. конфиденциальные клиент в OAuth2.0) |
| RecordConsentConditions |Типы условий согласие, в соответствии с определением hello контракта условия: нет (0), SilentConsentForPartnerManagedApp(1). Это значение будет предоставляться в схеме Graph API hello и может быть только задаваться и изменяться с администраторов заказчика. |
| RequiredResourceAccess |XML-содержимое значения свойства RequiredResourceAccess hello. |
| WebApp |Значение True указывает, что это веб-приложение. |
| WwwHomepage |основной веб-странице приветствия. |

## <a name="update-role-attributes"></a>Атрибуты "Обновить роль"
| Атрибут | Описание |
| --- | --- |
| AppAddress |набор адресов (перенаправление URL-адреса), назначенных субъекту-службе tooa Hello. |
| BelongsToFirstLoginObjectSet |Значение true указывает, что этот объект принадлежит набор toohello входа требуется tooenable объекты первого Здравствуйте, администратор нового клиента. |
| Builtin |Указывает, принадлежит ли система hello hello жизненный цикл объекта. |
| Описание |Понятное описательное фраз о hello объекта. |
| DisplayName |отображаемое имя Hello объекта |
| MailNickname |Моникер объекта адресной книги, обычно hello часть его имени электронной почты, предшествующую hello «@» символов. |
| RoleDisabled |Указывает, следует ли игнорировать роли hello в целях проверки доступа. |
| RoleTemplateId |Идентификатор шаблона роли hello. |
| ServiceInfo |Данные, которые могут использоваться службой MOAC и/или других экземпляров службы инициализации определенной службы (из hello одинаковые или разные типы служб). |
| TaskSetScopeReference |Идентифицирует набор задач и набор областей, связанных с ролью или шаблоном роли. |
| ValidationError |Сведения, опубликованных службой федерации описывает ошибку непереходного, зависящие от службы относительно hello свойства или связь от tooresolve действия администратора объекта. |
| WellKnownObject |Помечает объект каталога как предварительно определенный набор. |

## <a name="update-role-definition-attributes"></a>Атрибуты Update Role definition (Обновление определения роли)
| Атрибут | Описание |
| --- | --- |
| AssignableScopes |Коллекция областей авторизации, которые можно ссылаться при назначении RoleDefinition tooa безопасности участника. |
| DisplayName |отображаемое имя Hello объекта |
| GrantedPermissions |Разрешения, предоставленные в рамках этого определения роли. |

## <a name="update-administrative-unit-attributes"></a>Атрибуты Update Administrative Unit (Обновление административной единицы)
| Атрибут | Описание |
| --- | --- |
| Описание |Это свойство обновляется при изменении описание hello административной единицы. |
| DisplayName |Это свойство обновляется при изменении имени hello административной единицы. |

## <a name="update-company-attributes"></a>Атрибуты Update Company (Обновление компании)
| Атрибут | Описание |
| --- | --- |
| AllowedDataLocation |Расположение, в какие hello компании доступны пользователям toobe подготовлены. |
| AuthorizedServiceInstance |Имена экземпляров службы toowhich плана могут быть развернуты. |
| DirSyncEnabled |Указывает, происходит ли синхронизация из доверенного каталога (пользовательского, локального). |
| DirSyncStatus |Указывает, наступает ли синхронизацию объектов адрес книги в контексте этого клиента из заслуживающих доверия (клиент, в локальной среде) каталога; расширение hello DirSyncEnabled свойств объектов компании. |
| DirSyncFeatures |Бит флаг отслеживания tookeep набора возможностей включенных и отключенных dirsync для клиента hello. |
| DirectoryFeatures |Включенные или отключенные функции синхронизации каталога. |
| DirSyncConfiguration |Содержит все DirSync конфигурации конкретного toohello текущего клиента. |
| DisplayName |отображаемое имя Hello объекта |
| IsMnc |Компания hello слишком» значение true», если набор логический флаг включен для функции hello многонациональной компании. |
| ObjectSettings |Коллекция параметров области применимо toohello hello объекта. |
| PartnerCommerceUrl |URL-адрес toohello партнера коммерческого сайта. |
| PartnerHelpUrl |Узел партнера toohello URL-адрес справки. |
| PartnerSupportEmail |Партнер toohello URL-адрес электронной почты технической поддержки. |
| PartnerSupportTelephone |URL-адрес toohello партнера телефонов поддержки. |
| PartnerSupportUrl |Сайта поддержки партнера toohello URL-адрес. |
| StrongAuthenticationDetails |Сведения, связанные с tooStrongAuthentication. |
| StrongAuthenticationPolicy |Политика строгой проверки подлинности для hello компании. |
| TechnicalNotificationMail |Адрес toonotify технические проблемы с электронной почтой относится tooa компании. |
| TelephoneNumber |Телефонные номера, соответствовать hello E.123 рекомендацией ITU. |
| TenantType |Тип Hello клиента. Если это значение не указано, клиент hello — компании. Возможные значения: MicrosoftSupport (0), SyndicatePartner (1), BreadthPartner (2), BreadthPartnerDelegatedAdmin (3), ResellerPartnerDelegatedAdmin (4), ValueAddedResellerPartnerDelegatedAdmin (5). |
| VerifiedDomain |Набор имен доменов DNS привязан tooa компании. |

## <a name="update-domain-attributes"></a>Атрибуты "Обновление домена"
| Атрибут | Описание |
| --- | --- |
| Возможности |Битовые флаги описания hello возможности домена hello, если таковые имеются. |
| значение по умолчанию |Указывает, является ли домен hello hello значение по умолчанию; Например hello по умолчанию UserPrincipalName суффикс, когда администратор создает нового пользователя в MOAC. |
| Initial |Указывает, является ли домен hello hello первоначальный домен компании hello, выделенного OCP. Начальный домен Hello — уникальный поддомене домена Microsoft Online; e.g.contoso3.microsoftonline.com. |
| LiveType |Тип hello соответствующее Windows Live пространство имен, если таковые имеются. |
| Имя |Идентификатор конечной точки hello. |
| PasswordNotificationWindowDays |Hello число дней до истечения срока действия пароля hello пользователь получает уведомление. |
| PasswordValidityPeriodDays |Здравствуйте, сколько дней пароль действует в течение до его смены. |

Записи аудита — это обязательный элемент управления для многих требований соответствия нормативам. Для клиентов, использующих их нормативным toomeet hello Azure Active Directory аудита отчетов рекомендуется клиента hello отправки копии этой справки с копией hello hello клиента экспортированный отчет аудита, toohelp объяснить hello отчета Подробные сведения. Если Аудитор hello нормативным hello toounderstand, Azure в настоящее время отвечает, прямой hello Аудитор toohello [страницы соответствия](https://azure.microsoft.com/support/trust-center/compliance/) из hello Центр управления безопасностью Microsoft Azure.

