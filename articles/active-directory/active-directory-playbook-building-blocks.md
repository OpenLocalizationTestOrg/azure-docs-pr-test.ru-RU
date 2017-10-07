---
title: "aaaAzure подтверждения концепции репертуара стандартных блоков в Active Directory | Документы Microsoft"
description: "Ознакомление со сценариями управления удостоверениями и доступом и их реализация"
services: active-directory
keywords: "azure active directory, сборник тренировочных заданий, подтверждение концепции, PoC"
documentationcenter: 
author: dstefanMSFT
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: dstefan
ms.openlocfilehash: e54148330a123baf27d7e0f73469ff2a24c0efcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-building-blocks"></a>Сборник тренировочных заданий по подтверждению концепции для Azure Active Directory: стандартные блоки

## <a name="catalog-of-roles"></a>Каталог ролей

| Роль | Описание | Обязанности по подтверждению концепции |
| --- | --- | --- |
| **Группа по архитектуре удостоверений и разработке** | В эту группу, обычно является hello один, разрабатывает решения hello, реализующий прототипов, дисков утверждения и наконец передает toooperations | Они обеспечивают средах hello и являются hello из них вычисление hello различных сценариев с точки зрения управляемости hello |
| **Группа по работе с локальными удостоверениями** | Управляет hello другим удостоверением источников локальной: леса Active Directory, каталогов LDAP, HR систем и поставщиков федерации удостоверений. | Предоставить доступ к ресурсам локальной tooon необходимые для hello сценарии проверки концепции.<br/>Этих сотрудников следует вовлекать в работу как можно меньше.|
| **Технические владельцы приложений** | Технические владельцев hello разных облачных приложений и служб, которые будут интегрированы с Azure AD | Предоставляют сведения о приложениях SaaS (потенциальные экземпляры для тестирования). |
| **Глобальный администратор Azure AD** | Управляет конфигурацией hello Azure AD | Укажите учетные данные службы синхронизации tooconfigure hello. Обычно hello группы архитектура идентификаторов во время проверки концепции, но отдельные операции на этапе hello|
| **Группа баз данных** | Владельцами инфраструктура hello базы данных | Предоставить доступ tooSQL среду (служб федерации Active Directory или Azure AD Connect) для конкретного сценария подготовительные действия.<br/>Этих сотрудников следует вовлекать в работу как можно меньше. |
| **Группа по сетям** | Владельцы hello сетевой инфраструктуры | Укажите необходимый уровень доступа на уровне сети hello hello синхронизации серверов tooproperly hello источниками данных и облачных служб (правила брандмауэра, открытых портов, правила IPSec и т. д.) |
| **Группа безопасности:** | Определяет стратегию безопасности hello, анализирует отчеты из различных источников и распространяется на результаты. | Предоставляет целевые сценарии по оценке безопасности. |

## <a name="common-prerequisites-for-all-building-blocks"></a>Общие предварительные требования для всех стандартных блоков

Ниже приведены некоторые предварительные требования по любому подтверждению концепции для Azure AD Premium.

| Предварительные требования | Ресурсы |
| --- | --- |
| Определен клиент Azure AD с действительной подпиской Azure | [Как клиент tooget Azure Active Directory](active-directory-howto-tenant.md)<br/>**Примечание:** при наличии среды с Azure AD Premium лицензий ноль cap подписки можно получить, перейдя по toohttps://aka.ms/accessaad <br/>Дополнительные сведения: https://blogs.technet.microsoft.com/enterprisemobility/2016/02/26/azure-ad-mailbag-azure-subscriptions-and-azure-ad-2/ и https://technet.microsoft.com/library/dn832618.aspx. |
| Домены определены и проверены | [Добавить tooAzure имя пользовательского домена Active Directory](active-directory-domains-add-azure-portal.md)<br/>**Примечание:** некоторых рабочих нагрузок, таких как Power BI может подготовлены клиента azure AD в hello рассматриваются. toocheck, если в заданном домене клиента связанного tooa переход toohttps://login.microsoftonline.com/ {domain}/v2.0/.well-known/openid-configuration. Если вы получаете успешный ответ, то hello домена уже назначен tooa клиента и перехватить могут быть необходимы. В этом случае за дальнейшими указаниями обратитесь в корпорацию Майкрософт. Дополнительные сведения о параметрах слиянию компании hello в: [возможности самообслуживания при регистрации в Azure?](active-directory-self-service-signup.md) |
| Включена пробная версия EMS или Azure AD Premium | [Бесплатная пробная версия Azure Active Directory Premium на один месяц](https://azure.microsoft.com/trial/get-started-active-directory/) |
| Назначены лицензии Azure AD Premium или EMS tooPoC пользователей | [Самостоятельное лицензирование и лицензирование пользователей в Azure Active Directory](active-directory-licensing-get-started-azure-portal.md) |
| Учетные данные глобального администратора Azure AD | [Назначение ролей администратора в Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md) |
| Необязательно, но настоятельно рекомендуется: параллельная лабораторная среда в качестве резерва | [Необходимые условия для Azure AD Connect](./connect/active-directory-aadconnect-prerequisites.md) |

## <a name="directory-synchronization---password-hash-sync-phs---new-installation"></a>Синхронизация каталога. Синхронизация хэша паролей (PHS): новая установка

Приблизительное время tooComplete: один час для менее 1000 пользователей проверки концепции

### <a name="pre-requisites"></a>Предварительные требования

| Предварительные требования | Ресурсы |
| --- | --- |
| TooRun сервера Azure AD Connect | [Необходимые условия для Azure AD Connect](./connect/active-directory-aadconnect-prerequisites.md) |
| Целевые Пользователи подтверждения Концепции, в hello одном домене и часть группы безопасности и Подразделения | [Выборочная установка Azure AD Connect](./connect/active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) |
| Azure AD подключения возможности, необходимые для проверки Концепции идентифицируются hello | [Подключение Active Directory к Azure Active Directory — настройка функций синхронизации](./connect/active-directory-aadconnect.md#configure-sync-features) |
| Наличие необходимых учетных данных для локальных и облачных сред  | [Azure AD Connect: учетные записи и разрешения](./connect/active-directory-aadconnect-accounts-permissions.md) |

### <a name="steps"></a>Действия

| Шаг | Ресурсы |
| --- | --- |
| Загрузить последнюю версию Azure AD Connect hello | [Скачивание Microsoft Azure Active Directory Connect](https://www.microsoft.com/download/details.aspx?id=47594) |
| Установить Azure AD Connect с простейший способ hello: Express <br/>1. Фильтрация toohello целевого Подразделение toominimize hello цикла синхронизации времени<br/>2. Выберите целевой группы пользователей в локальной группе hello.<br/>3. Развертывание необходимые по hello прочих тем подтверждения Концепции функции hello | [Azure AD Connect: выборочная установка. Фильтрация домена и подразделения](./connect/active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) <br/>[Azure AD Connect: выборочная установка. Фильтрация на основе групп](./connect/active-directory-aadconnect-get-started-custom.md#sync-filtering-based-on-groups)<br/>[Azure AD Connect: интеграция локальных удостоверений с Azure Active Directory. Настройка функции синхронизации](./connect/active-directory-aadconnect.md#configure-sync-features) |
| Откройте hello Azure AD Connect пользовательского интерфейса и увидеть выполнение hello профили завершенного (импорта, синхронизации и экспорт) | [Синхронизация Azure AD Connect: планировщик](./connect/active-directory-aadconnectsync-feature-scheduler.md) |
| Откройте hello [портала управления Azure AD](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/), перейдите в колонку toohello «Все пользователи», добавьте столбец «Источник» и убедитесь, что пользователи hello отображаются, надлежащим образом помечен как поступающие от «Windows Server AD» | [Портал управления Azure AD](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) |

### <a name="considerations"></a>Рекомендации

1. Просмотрите рекомендации по безопасности hello синхронизация хэшей паролей [здесь](./connect/active-directory-aadconnectsync-implement-password-synchronization.md).  Если синхронизация хэшей паролей для пользователей пилотного производства неприемлемо окончательно, следует выбрать hello следующие варианты:
   * Создайте тестовых пользователей в домене производственного hello. Следите за тем, чтобы не синхронизировать никакие другие учетные записи.
   * Переместить tooan UAT среды
2.  Если вы хотите toopursue федерации, стоит toounderstand hello затраты, связанные федеративных решений с локальным поставщиком удостоверений за пределами hello подтверждения Концепции и поиске измерения, от hello преимущества:
    * Он находится в критическом пути hello, у вас есть toodesign для обеспечения высокой доступности
    * Он является локальной службы, необходимо toocapacity плана
    * Он является локальной службы, необходимо toomonitor/Ведение/patch

Дополнительные сведения: [Сведения об удостоверении Office 365 и Azure Active Directory — федеративное удостоверение](https://support.office.com/article/Understanding-Office-365-identity-and-Azure-Active-Directory-06a189e7-5ec6-4af2-94bf-a22ea225a7a9#bk_federated)

## <a name="branding"></a>Фирменная символика

Приблизительное время tooComplete: 15 минут

### <a name="pre-requisites"></a>Предварительные требования

| Предварительные требования | Ресурсы |
| --- | --- |
| Активы (изображений, эмблемы, и т. д.); Для наиболее подходящей визуализацией следует убедиться, что активы hello имеют hello, рекомендуется использовать размеры. | [Добавить корпоративную фирменную символику tooyour на странице входа в Azure Active Directory hello](active-directory-branding-custom-signon-azure-portal.md) |
| Необязательно: Если hello среде имеется сервер служб федерации Active Directory, доступ к toohello сервера toocustomize веб-темы | [Настройка входа для пользователя AD FS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/ad-fs-user-sign-in-customization) |
| Имя входа для конечных пользователей взаимодействие с клиентом компьютер tooperform |  |
| Необязательно: Мобильные устройства toovalidate качества |  |

### <a name="steps"></a>Действия

| Шаг | Ресурсы |
| --- | --- |
| Go tooAzure AD портал управления | [Портал управления Azure AD — фирменная символика организации](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/LoginTenantBranding) |
| Передать активы приветствия для страницы входа hello (героя эмблемы, эмблемы, метки, и т. д.). При необходимости выровняйте при наличии AD FS hello же средств со страницы входа служб федерации Active Directory | [Добавить корпоративную фирменную символику tooyour входа и панели доступа: настраиваемые элементы](active-directory-add-company-branding.md) |
| Подождите несколько минут для hello toofully изменения вступят в силу |  |
| Войдите с hello toohttps://myapps.microsoft.com учетных данных пользователя подтверждения Концепции |  |
| Подтвердите hello внешний вид и поведение в браузере | [Добавить корпоративную фирменную символику tooyour входа и панели доступа](active-directory-add-company-branding.md) |
| При необходимости подтвердите hello внешний вид и поведение в других устройствах |  |

### <a name="considerations"></a>Рекомендации

Если hello старого внешний вид и поведение остается после настройки hello очистить кэш клиента hello браузера и повторите операцию hello.

## <a name="group-based-licensing"></a>Групповое лицензирование

Приблизительное время tooComplete: 10 минут

### <a name="pre-requisites"></a>Предварительные требования

| Предварительные требования | Ресурсы |
| --- | --- |
| Все пользователи подтверждения концепции входят в состав группы безопасности (облачной или локальной) | [Создание группы и добавление в нее пользователей в Azure Active Directory](active-directory-groups-create-azure-portal.md) |

### <a name="steps"></a>Действия

| Шаг | Ресурсы |
| --- | --- |
| Перейдите в колонку toolicenses на портале управления Azure AD | [Портал управления Azure AD: лицензирование](https://portal.azure.com/#blade/Microsoft_AAD_IAM/LicensesMenuBlade/Products) |
| Назначьте группу безопасности toohello hello лицензий с пользователями подтверждения Концепции. | [Назначьте лицензии tooa группу пользователей в Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md) |

### <a name="considerations"></a>Рекомендации

В случае проблем с, go слишком[сценарии, ограничения и известные проблемы при использовании групп toomanage лицензирования в Azure Active Directory](active-directory-licensing-group-advanced.md)

## <a name="saas-federated-sso-configuration"></a>Настройка федеративного единого входа SaaS

Приблизительное время tooComplete: 60 минут

### <a name="pre-requisites"></a>Предварительные требования

| Предварительные требования | Ресурсы |
| --- | --- |
| Тестовая среда для hello доступные приложения SaaS. В этом руководстве в качестве примера мы используем ServiceNow.<br/>Мы настоятельно рекомендуем toouse повышение эффективности toominimize тестового экземпляра о перемещении существующего качества данных и сопоставления. | Go toohttps://developer.servicenow.com/app.do#! / home toostart hello процесс получения экземпляра теста |
| Консоль управления ServiceNow toohello доступа администратора | [Руководство: интеграция Azure Active Directory с ServiceNow](active-directory-saas-servicenow-tutorial.md) |
| Целевой набор пользователей tooassign hello приложению. Рекомендуется использовать группы безопасности, содержащей пользователей подтверждения концепции hello. <br/>Если создание hello группы не может быть выполнено, затем назначьте пользователей hello toodirectly toohello приложение для проверки концепции hello | [Назначить пользователю или группе tooan приложений в Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |

### <a name="steps"></a>Действия

| Шаг | Ресурсы |
| --- | --- |
| Совместное использование субъекты учебника tooall hello из документации Майкрософт  | [Руководство: интеграция Azure Active Directory с ServiceNow](active-directory-saas-servicenow-tutorial.md) |
| Задать рабочей встречи и следуйте hello шагах учебника с каждый субъект. | [Руководство: интеграция Azure Active Directory с ServiceNow](active-directory-saas-servicenow-tutorial.md) |
| Назначьте группы toohello приложения hello, указанных в hello предварительные требования. Если hello подтверждения Концепции условного доступа в области hello, можно позже, вернитесь и добавить многофакторную проверку Подлинности и пр. <br/>Обратите внимание, что это будет срабатывать hello процесс подготовки (если настроено) |  [Назначить пользователю или группе tooan приложений в Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) <br/>[Создание группы и добавление в нее пользователей в Azure Active Directory](active-directory-groups-create-azure-portal.md) |
| Использование tooadd портала управления Azure AD ServiceNow приложения из коллекции| [Портал управления Azure AD: корпоративные приложения](https://portal.azure.com/#blade/Microsoft_AAD_IAM/StartboardApplicationsMenuBlade/Overview) <br/>[Новые возможности управления корпоративными приложениями в Azure Active Directory](active-directory-enterprise-apps-whats-new-azure-portal.md) |
| В колонке "Единый вход" приложения ServiceNow включите параметр "SAML-based Sign-on" (Вход на основе SAML). |  |
| Укажите в полях "URL-адрес для входа" и "Идентификатор" URL-адрес ServiceNow.<br/>Флажок "hello"слишком «активировать новый сертификат»<br/>и сохраните параметры. |  |
| Откройте колонку «Настройка ServiceNow» hello нижней части панели tooview hello пользовательские инструкции tooconfigure ServiceNow |  |
| Следуйте инструкциям tooconfigure ServiceNow |  |
| В колонке "Подготовка" приложения ServiceNow включите автоматическую подготовку. | [Управление учетной записью пользователя, подготовки для корпоративных приложений в новый портал Azure hello](active-directory-enterprise-apps-manage-provisioning.md) |
| Подождите несколько минут, пока подготовка закончится.  Это время, в hello можно проверить на hello, подготовки отчетов |  |
| Войдите в toohttps://myapps.microsoft.com/ в качестве тестового пользователя, имеющего доступ | [Что такое hello панель доступа?](active-directory-saas-access-panel-introduction.md) |
| Щелкните плитку приложения hello, только что созданный hello. Подтвердите доступ. |  |
| При необходимости можно проверять отчеты об использовании приложения hello. Обратите внимание, что имеется некоторая задержка, поэтому требуется toowait трафик hello toosee время в отчетах hello. | [Отчеты действия при входе в портал Azure Active Directory hello: использование управляемых приложений](active-directory-reporting-activity-sign-ins.md#usage-of-managed-applications)<br/>[Политики хранения отчетов Azure Active Directory](active-directory-reporting-retention.md) |

### <a name="considerations"></a>Рекомендации

1. Выше [учебника](active-directory-saas-servicenow-tutorial.md) ссылается интерфейс управления tooold Azure AD. Однако подтверждение концепции основано на интерфейсе [быстрого запуска](active-directory-enterprise-apps-whats-new-azure-portal.md#quick-start-get-going-with-your-new-application-right-away).
2. Если отсутствует целевое приложение hello в галерее hello, можно использовать, «Принеси свое приложение». Дополнительные сведения: [Новые возможности управления корпоративными приложениями в Azure Active Directory. Добавление пользовательских приложений из одного расположения](active-directory-enterprise-apps-whats-new-azure-portal.md#add-custom-applications-from-one-place)

## <a name="saas-password-sso-configuration"></a>Настройка единого входа SaaS с помощью пароля

Приблизительное время tooComplete: 15 минут

### <a name="pre-requisites"></a>Предварительные требования

| Предварительные требования | Ресурсы |
| --- | --- |
| Тестовая среда для приложений SaaS. Примером единого входа с паролем является HipChat и Twitter. Для любого другого приложения необходимо hello точный URL-адрес страницы приветствия с формы входа в html. | [Twitter в Microsoft Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/aad.twitter)<br/>[HipChat в Microsoft Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/aad.hipchat) |
| Тестовые учетные записи для приложения hello. | [Регистрация в Twitter](https://twitter.com/signup?lang=en)<br/>[Бесплатная регистрация: HipChat](https://www.hipchat.com/sign_up) |
| Целевой набор пользователей tooassign hello приложению. Рекомендуется использовать безопасности группы содержится hello пользователи. | [Назначить пользователю или группе tooan приложений в Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |
| Локальный администратор доступа tooa компьютера toodeploy hello расширение панели доступа для Internet Explorer, Chrome или Firefox | [Расширение "Панель доступа" для Internet Explorer](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[Расширение "Панель доступа" для Chrome](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[Расширение "Панель доступа" для Firefox](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |

### <a name="steps"></a>Действия

| Шаг | Ресурсы |
| --- | --- |
| Установка расширения браузера hello | [Расширение "Панель доступа" для Internet Explorer](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[Расширение "Панель доступа" для Chrome](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[Расширение "Панель доступа" для Firefox](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |
| Настройте приложение из коллекции. | [Новые возможности управления для корпоративных приложений в Azure Active Directory: hello коллекцию новых и усовершенствованных приложений](active-directory-enterprise-apps-whats-new-azure-portal.md#improvements-to-the-azure-active-directory-application-gallery) |
| Настройте единый вход с паролем. | [Управление единым входом для корпоративных приложений в новый портал Azure hello: паролю вход](active-directory-enterprise-apps-manage-sso.md#password-based-sign-on) |
| Назначьте группы toohello приложения hello, указанных в hello предварительные требования | [Назначить пользователю или группе tooan приложений в Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |
| Войдите в toohttps://myapps.microsoft.com/ в качестве тестового пользователя, имеющего доступ |  |
| Щелкните плитку приложения hello, только что созданный hello. | [Что такое hello панель доступа?: SSO на основе пароля без предоставления идентификатора](active-directory-saas-access-panel-introduction.md#password-based-sso-without-identity-provisioning) |
| Укажите учетные данные приложения hello | [Что такое hello панель доступа?: SSO на основе пароля без предоставления идентификатора](active-directory-saas-access-panel-introduction.md#password-based-sso-without-identity-provisioning) |
| Закройте браузер hello и повторите hello входа. Этот раз у пользователя hello должно открыться приложение toohello легкий доступ. |  |
| При необходимости можно проверять отчеты об использовании приложения hello. Обратите внимание, что имеется некоторая задержка, поэтому требуется toowait трафик hello toosee время в отчетах hello. | [Отчеты действия при входе в портал Azure Active Directory hello: использование управляемых приложений](active-directory-reporting-activity-sign-ins.md#usage-of-managed-applications)<br/>[Политики хранения отчетов Azure Active Directory](active-directory-reporting-retention.md) |

### <a name="considerations"></a>Рекомендации

Если отсутствует целевое приложение hello в галерее hello, можно использовать, «Принеси свое приложение». Дополнительные сведения: [Новые возможности управления корпоративными приложениями в Azure Active Directory. Добавление пользовательских приложений из одного расположения](active-directory-enterprise-apps-whats-new-azure-portal.md#add-custom-applications-from-one-place)

 Имейте в виду hello следующие требования:
   * Приложение должно иметь известный URL-адрес входа.
   * Hello на странице входа должен содержать HTML-формы с одной несколько текстовых полей, расширения обозревателя hello можно автоматического заполнения. На минимальное hello она должна содержать имя пользователя и пароль.

## <a name="saas-shared-accounts-configuration"></a>Настройка общих учетных записей SaaS.

Приблизительное время tooComplete: 30 минут

### <a name="pre-requisites"></a>Предварительные требования

| Предварительные требования | Ресурсы |
| --- | --- |
| Здравствуйте, список целевых приложений и hello точное вход URL-адреса заранее. Например, можно использовать Twitter. | [Twitter в Microsoft Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/aad.twitter)<br/>[Регистрация в Twitter](https://twitter.com/signup?lang=en) |
| Общие учетные данные для этого приложения SaaS. | [Совместное использование учетных записей с помощью Azure AD](active-directory-sharing-accounts.md)<br/>[Автоматическая смена паролей Azure AD для Facebook, Twitter и LinkedIn перешла на этап предварительной версии! — блог по Enterprise Mobility + Security] (https://blogs.technet.microsoft.com/enterprisemobility/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview/) |
| Здравствуйте, учетные данные для по крайней мере двух участников команды, которые получат доступ к одной учетной записи. Они должны входить в группу безопасности. | [Назначить пользователю или группе tooan приложений в Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |
| Локальный администратор доступа tooa компьютера toodeploy hello расширение панели доступа для Internet Explorer, Chrome или Firefox | [Расширение "Панель доступа" для Internet Explorer](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[Расширение "Панель доступа" для Chrome](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[Расширение "Панель доступа" для Firefox](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |

### <a name="steps"></a>Действия

| Шаг | Ресурсы |
| --- | --- |
| Установка расширения браузера hello | [Расширение "Панель доступа" для Internet Explorer](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[Расширение "Панель доступа" для Chrome](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[Расширение "Панель доступа" для Firefox](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |
| Настройте приложение из коллекции. | [Новые возможности управления для корпоративных приложений в Azure Active Directory: hello коллекцию новых и усовершенствованных приложений](active-directory-enterprise-apps-whats-new-azure-portal.md#improvements-to-the-azure-active-directory-application-gallery) |
| Настройте единый вход с паролем. | [Управление единым входом для корпоративных приложений в новый портал Azure hello: паролю вход](active-directory-enterprise-apps-manage-sso.md#password-based-sign-on) |
| Назначьте группы toohello приложения hello, указанных в hello предварительные условия, при назначении их учетные данные | [Назначить пользователю или группе tooan приложений в Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |
| Выполните вход в качестве разных пользователей, доступ приложения в качестве hello **же общим учетной записи.**  |  |
| При необходимости можно проверять отчеты об использовании приложения hello. Обратите внимание, что имеется некоторая задержка, поэтому требуется toowait трафик hello toosee время в отчетах hello. | [Отчеты действия при входе в портал Azure Active Directory hello: использование управляемых приложений](active-directory-reporting-activity-sign-ins.md#usage-of-managed-applications)<br/>[Политики хранения отчетов Azure Active Directory](active-directory-reporting-retention.md) |


### <a name="considerations"></a>Рекомендации

Если отсутствует целевое приложение hello в галерее hello, можно использовать, «Принеси свое приложение». Дополнительные сведения: [Новые возможности управления корпоративными приложениями в Azure Active Directory. Добавление пользовательских приложений из одного расположения](active-directory-enterprise-apps-whats-new-azure-portal.md#add-custom-applications-from-one-place)

 Имейте в виду hello следующие требования:
   * Приложение должно иметь известный URL-адрес входа.
   * Hello на странице входа должен содержать HTML-формы с одной несколько текстовых полей, расширения обозревателя hello можно автоматического заполнения. На минимальное hello она должна содержать имя пользователя и пароль.

## <a name="app-proxy-configuration"></a>Настройка прокси приложения

Приблизительное время tooComplete: 20 минут

### <a name="pre-requisites"></a>Предварительные требования

| Предварительные требования | Ресурсы |
| --- | --- |
| Подписка на Microsoft Azure AD Basic или Premium, а также каталог Azure AD, для которого вы являетесь глобальным администратором. | [Выпуски Azure Active Directory](active-directory-editions.md) |
| Веб-приложения размещенного в локальной среде, желательно tooconfigure для удаленного доступа |  |
| Сервер под управлением Windows Server 2012 R2 или Windows 8.1 или более поздней версии, на котором можно установить соединитель прокси приложения hello | [Сведения о соединителях прокси приложения Azure AD](application-proxy-understand-connectors.md) |
| Если в пути hello установлен брандмауэр, убедитесь, что он открыт, что приветствия соединителя можно сделать HTTPS (TCP) запрашивает toohello прокси приложения | [Включите прокси приложения в hello Azure portal: предварительные требования прокси приложения](active-directory-application-proxy-enable.md#application-proxy-prerequisites) |
| Если ваша организация использует прокси-сервер toohello tooconnect серверов Интернета, take, рассмотрим блог hello post рабочий с существующие локальный прокси-серверы для получения подробной информации по tooconfigure их | [Работа с имеющимися локальными прокси-серверами](application-proxy-working-with-proxy-servers.md) |


### <a name="steps"></a>Действия

| Шаг | Ресурсы |
| --- | --- |
| Установите соединитель на сервере hello | [Включите прокси приложения в hello Azure portal: Установка и регистрация hello соединителя](active-directory-application-proxy-enable.md#install-and-register-a-connector) |
| Публикация приложения hello в локальной среде в Azure AD, как приложение прокси приложения | [Публикация приложений с помощью прокси приложения Azure AD](application-proxy-publish-azure-portal.md) |
| Назначьте тестовых пользователей. | [Публикация приложений с помощью прокси приложения Azure AD: добавление тестового пользователя](application-proxy-publish-azure-portal.md#add-a-test-user) |
| При необходимости настройте процедуру единого входа для пользователей. | [Реализация единого входа с помощью прокси приложения Azure AD](application-proxy-sso-azure-portal.md) |
| Тестовое приложение при входе в портал tooMyApps как назначенный пользователь | https://myapps.microsoft.com |

### <a name="considerations"></a>Рекомендации

1. Во время рекомендуется размещение соединителя hello в своей корпоративной сети, существуют случаи, когда вы увидите более высокую производительность, поместив его в облаке hello. Дополнительные сведения: [Аспекты топологии сети при использовании прокси приложения Azure Active Directory](application-proxy-network-topology-considerations.md).
2. Дополнительные сведения о безопасности и том, как получить решение для безопасного удаленного доступа, поддерживая только исходящие подключения, см. в статье [Вопросы безопасности при удаленном доступе к приложениям через прокси приложения Azure AD](application-proxy-security-considerations.md).

## <a name="generic-ldap-connector-configuration"></a>Настройка универсального соединителя LDAP

Приблизительное время tooComplete: 60 минут

> [!IMPORTANT]
> Для использования этой расширенной конфигурации нужно сначала ознакомиться с FIM/MIM. Дополнительные сведения о ее использовании в рабочей среде можно получить в [службе поддержки Premier](https://support.microsoft.com/premier).

### <a name="pre-requisites"></a>Предварительные требования

| Предварительные требования | Ресурсы |
| --- | --- |
| Установленная и настроенная среда Azure AD Connect. | Стандартный блок: [Синхронизация каталога. Синхронизация хэша паролей](#directory-synchronization--password-hash-sync-phs--new-installation) |
| Соответствующий требованиям экземпляр ADLDS. | [Технический справочник универсальный соединитель LDAP: Общие сведения о hello универсальный соединитель LDAP](./connect/active-directory-aadconnectsync-connector-genericldap.md#overview-of-the-generic-ldap-connector) |
| Список рабочих нагрузок, используемых пользователями, а также связанные с этими нагрузками атрибуты. | [Синхронизация Azure AD Connect: атрибуты, синхронизированные tooAzure Active Directory](./connect/active-directory-aadconnectsync-attributes-synchronized.md) |


### <a name="steps"></a>Действия

| Шаг | Ресурсы |
| --- | --- |
| Добавьте универсальный соединитель LDAP. | [Технический справочник по универсальному соединителю LDAP: создание нового соединителя](./connect/active-directory-aadconnectsync-connector-genericldap.md#create-a-new-connector) |
| Создайте профили выполнения для созданного соединителя (полный импорт, разностный импорт, полная синхронизация, разностная синхронизация, экспорт). | [Создание профиля выполнения для агента управления](https://technet.microsoft.com/library/jj590219(v=ws.10).aspx)<br/> [Использование соединителей с hello Azure AD Connect Sync Service Manager](./connect/active-directory-aadconnectsync-service-manager-ui-connectors.md)|
| Запустите профиль полного импорта и убедитесь, что в пространстве соединителя есть объекты. | [Поиск объекта пространства соединителя](https://technet.microsoft.com/library/jj590287(v=ws.10).aspx)<br/>[Использование соединителей с hello Azure AD Connect Sync Service Manager: поиска пространства соединителя](./connect/active-directory-aadconnectsync-service-manager-ui-connectors.md#search-connector-space) |
| Создайте правила синхронизации, чтобы объекты в метавселенной имели подходящие атрибуты для рабочих нагрузок. | [Синхронизация Azure AD Connect: советы и рекомендации по изменению конфигурации по умолчанию hello: изменяет правила tooSynchronization](./connect/active-directory-aadconnectsync-best-practices-changing-default-configuration.md#changes-to-synchronization-rules)<br/>[Служба синхронизации Azure AD Connect: общие сведения о декларативной подготовке](./connect/active-directory-aadconnectsync-understanding-declarative-provisioning.md)<br/>[Служба синхронизации Azure AD Connect: общие сведения о выражениях декларативной подготовки](./connect/active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) |
| Запустите полный цикл синхронизации. | [Синхронизация Azure AD Connect: планировщика: запустить планировщик hello](./connect/active-directory-aadconnectsync-feature-scheduler.md#start-the-scheduler) |
| При возникновении проблем выполните устранение неполадок. | [Устранение неполадок объект, который не выполняют синхронизацию tooAzure AD](./connect/active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) |
| Убедитесь, что LDAP пользователь может войти и доступ к приложению hello | https://myapps.microsoft.com |

### <a name="considerations"></a>Рекомендации

> [!IMPORTANT]
> Для использования этой расширенной конфигурации нужно сначала ознакомиться с FIM/MIM. Дополнительные сведения о ее использовании в рабочей среде можно получить в [службе поддержки Premier](https://support.microsoft.com/premier).

## <a name="groups---delegated-ownership"></a>Группы — делегированное владение.

Приблизительное время tooComplete: 10 минут

### <a name="pre-requisites"></a>Предварительные требования

| Предварительные требования | Ресурсы |
| --- | --- |
| Приложение SaaS (федеративный единый вход или единый вход с паролем) уже настроено. | Стандартный блок: [Настройка федеративного единого входа SaaS](#saas-federated-sso-configuration) |
| Определяется группа облака, назначенная toohello приложения access в #1 | Стандартный блок: [Настройка федеративного единого входа SaaS](#saas-federated-sso-configuration) <br/>[Создание группы и добавление в нее пользователей в Azure Active Directory](active-directory-groups-create-azure-portal.md) |
| Нет учетных данных для владельца группы hello | [Управление tooresources доступ с помощью групп Azure Active Directory](active-directory-manage-groups.md) |
| Учетные данные для доступа к приложений hello hello сведения работника обнаружена | [Что такое hello панель доступа?](active-directory-saas-access-panel-introduction.md) |


### <a name="steps"></a>Действия

| Шаг | Ресурсы |
| --- | --- |
| Определять hello группы, которой предоставлены toohello приложения access и настраивать hello владельцем данной группы| [Управление параметрами hello группы в Azure Active Directory](active-directory-groups-settings-azure-portal.md) |
| Войдите в систему как владелец группы hello см. в разделе членство в группе hello в группы на вкладке панели доступа | [Страница управления группами Azure Active Directory](https://account.activedirectory.windowsazure.com/r/#/groups) |
| Добавить hello информационный работник, вы хотите tootest |  |
| Войдите в систему как hello информационный работник Подтвердите, что доступен плитки приветствия | [Что такое hello панель доступа?](active-directory-saas-access-panel-introduction.md) |

### <a name="considerations"></a>Рекомендации

Если приложения hello подготовки включена, может потребоваться toowait через несколько минут для подготовки toocomplete перед обращением к приложения hello hello информационный работник hello.

## <a name="saas-and-identity-lifecycle"></a>SaaS и жизненный цикл удостоверений

### <a name="pre-requisites"></a>Предварительные требования

| Предварительные требования | Ресурсы |
| --- | --- |
| Приложение SaaS (федеративный единый вход или единый вход с паролем) уже настроено. | Стандартный блок: [Настройка федеративного единого входа SaaS](#saas-federated-sso-configuration) |
| Определяется группа облака, назначенная toohello приложения access в #1 | Стандартный блок: [Настройка федеративного единого входа SaaS](#saas-federated-sso-configuration) <br/>[Создание группы и добавление в нее пользователей в Azure Active Directory](active-directory-groups-create-azure-portal.md) |
| Учетные данные для доступа к приложений hello hello сведения работника обнаружена | [Что такое hello панель доступа?](active-directory-saas-access-panel-introduction.md) |


### <a name="steps"></a>Действия

| Шаг | Ресурсы |
| --- | --- |
| Удалите слишком назначен пользователь hello из приложения hello hello группы| [Управление участниками групп в клиенте Azure Active Directory](active-directory-groups-members-azure-portal.md) |
| Подождите несколько минут, пока отзыв закончится. | [Автоматическая подготовка пользователей для приложения SaaS в Azure AD: как работает автоматическая подготовка](active-directory-saas-app-provisioning.md#how-does-automated-provisioning-work) |
| В сеансе отдельный браузер войдите в систему как hello информационный работник toomy приложений портал и убедитесь, что она отсутствует | http://myapps.microsoft.com |


### <a name="considerations"></a>Рекомендации

Экстраполируйте tooleavers сценарий проверки концепции hello и/или сценарии отпуске. Если пользователь hello возвращает отключен в локальном AD или удалены, больше не toolog способом в toohello приложения SaaS.

## <a name="self-service-access-tooapplication-management"></a>SELF tooApplication доступ к службе управления

Приблизительное время tooComplete: 10 минут

### <a name="pre-requisites"></a>Предварительные требования

| Предварительные требования | Ресурсы |
| --- | --- |
| Идентификация пользователей подтверждения Концепции, которые будут запрашивать доступ toohello приложения, в рамках группы безопасности hello | Стандартный блок: [Настройка федеративного единого входа SaaS](#saas-federated-sso-configuration) |
| Целевое приложение развернуто. | Стандартный блок: [Настройка федеративного единого входа SaaS](#saas-federated-sso-configuration) |

### <a name="steps"></a>Действия

| Шаг | Ресурсы |
| --- | --- |
| Перейдите в колонку tooEnterprise приложений на портале управления Azure AD | [Портал управления Azure AD: корпоративные приложения](https://portal.azure.com/#blade/Microsoft_AAD_IAM/StartboardApplicationsMenuBlade/AllApps/menuId/) |
| Настройте самообслуживание для приложения из предварительных требований. | [Новые возможности управления корпоративными приложениями в Azure Active Directory: настройка самостоятельного доступа к приложениям](active-directory-enterprise-apps-whats-new-azure-portal.md#configure-self-service-application-access) |
| Войдите в систему как hello информационный работник toomy приложений портал | http://myapps.microsoft.com |
| Обратите внимание, «+ добавить приложение» кнопку на op страницы приветствия. Использовать приложение toohello tooget доступа |  |

### <a name="considerations"></a>Рекомендации

Выбранный приложения Hello возможно подготовки требования, поэтому будет немедленно toohello приложения может привести к некоторые ошибки. Если выбрана приложения hello поддерживает подготовку с помощью azure ad и он настроен, его можно использовать как возможность tooshow hello весь поток работа end tooend. . В разделе hello стандартный блок для [SaaS федеративного единого входа конфигурации](#saas-federated-sso-configuration) Дополнительные рекомендации

## <a name="self-service-password-reset"></a>Самостоятельный сброс пароля

Приблизительное время tooComplete: 15 минут

### <a name="pre-requisites"></a>Предварительные требования

| Предварительные требования | Ресурсы |
| --- | --- |
| Включите самостоятельное управление паролями в клиенте. | [Сброс паролей Azure Active Directory для ИТ-администраторов](active-directory-passwords.md) |
| Включите пароль toomanage обратной записи паролей из локальной. Обратите внимание, что для этого требуются определенные версии Azure AD Connect. | [Необходимые условия для обратной записи паролей](active-directory-passwords-writeback.md) |
| Определите hello подтверждения концепции пользователей, которые будут использовать эту функцию и убедитесь, что они являются членами группы безопасности. Hello пользователи должны иметь возможность hello демонстрационные toofully не являющихся администраторами | [Настройка: Управление паролями Azure AD: сброс toopassword ограничение доступа](active-directory-passwords-writeback.md) |


### <a name="steps"></a>Действия

| Шаг | Ресурсы |
| --- | --- |
| Перейдите tooAzure AD портал управления: сброса пароля | [Портал управления Azure AD: сброс пароля](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/PasswordReset) |
| Определите, какая политика сброса пароля hello. Для целей проверки Концепции можно использовать телефонного звонка и вопросов и ответов. Рекомендуется toobe tooenable регистрации, необходимые для входа в панель tooaccess |  |
| Выйдите из системы и войдите в качестве информационного работника. |  |
| Предоставьте hello данных самостоятельного сброса пароля, как настроить для каждого шага 2 | http://aka.ms/ssprsetup |
| Закрыть hello браузера |  |
| Начинать процесс входа в систему hello hello информационный работник, который использовался в шаге 4 |  |
| Сброс пароля hello | [Изменение своего пароля: сброс пароля](active-directory-passwords-update-your-own-password.md) |
| Выполните вход с использованием нового пароля tooAzure AD, а также tooon локальных ресурсов |  |

### <a name="considerations"></a>Рекомендации

1. Если обновление hello Azure AD Connect будет toocause трения, рассмотреть возможность его использования для облачных учетных записях или сделать его Демонстрация отдельной среде
2. Hello Администраторы имеют разные политики и Здравствуйте, администратор с помощью учетной записи tooreset hello пароль может taint hello подтверждения концепции и ввести в заблуждение. Убедитесь, что применяется операций сброса обычной пользовательской учетной записи tootest hello


## <a name="azure-multi-factor-authentication-with-phone-calls"></a>Многофакторная идентификация в Azure с помощью телефонных звонков

Приблизительное время tooComplete: 10 минут

### <a name="pre-requisites"></a>Предварительные требования

| Предварительные требования | Ресурсы |
| --- | --- |
| Удостоверение пользователей подтверждения концепции, которые будут использовать Многофакторную идентификацию.  |  |
| Телефон с хорошим приемом для прохождения Многофакторной идентификации.  | [Что такое Многофакторная идентификация Azure?](../multi-factor-authentication/multi-factor-authentication.md) |

### <a name="steps"></a>Действия

| Шаг | Ресурсы |
| --- | --- |
| Перейдите в слишком колонка «Пользователи и группы» на портале управления Azure AD | [Портал управления Azure AD: пользователи и группы](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/Overview/menuId/) |
| Выберите колонку "Все пользователи". |  |
| В верхней части кнопки «Многофакторная проверка подлинности» выберите hello | Прямой URL-адрес для портала Многофакторной идентификации Azure: https://aka.ms/mfaportal |
| В параметрах «User» hello выберите пользователей подтверждения концепции hello и позволяющие им многофакторной проверки подлинности. | [Состояние пользователей в службе Многофакторной идентификации Azure](../multi-factor-authentication/multi-factor-authentication-get-started-user-states.md) |
| Войдите в систему как пользователь подтверждения концепции hello и руководства по процессу hello дополнительная защита  |  |

### <a name="considerations"></a>Рекомендации

1. Hello подтверждения концепции шагов в этот стандартный блок явного задания многофакторной проверки Подлинности для пользователя все имена входа. Существуют и другие средства, такие как условный доступ и защита идентификации, включающие Многофакторную идентификацию в более специализированных сценариях. Это будет что-нибудь tooconsider при переходе от tooproduction подтверждения Концепции.
2. шаги проверки концепции Hello в этот стандартный блок явным образом используете телефонные звонки как hello метод многофакторной проверки Подлинности для expedience. При переходе от tooproduction проверки Концепции, мы рекомендуем использовать приложения, такие как hello [проверки подлинности Microsoft](../multi-factor-authentication/end-user/microsoft-authenticator-app-how-to.md) как ваш второй фактор, когда это возможно.
Дополнительные сведения: [черновик специальной публикации NIST 800-63B](https://pages.nist.gov/800-63-3/sp800-63b.html)

## <a name="mfa-conditional-access-for-saas-applications"></a>Условный доступ MFA к приложениям SaaS

Приблизительное время tooComplete: 10 минут

### <a name="pre-requisites"></a>Предварительные требования

| Предварительные требования | Ресурсы |
| --- | --- |
| Поиск подтверждения концепции пользователей tootarget hello политики. Эти пользователи должны иметь в политике безопасности группы tooscope hello условным доступом | [Настройка федеративного единого входа SaaS](#saas-federated-sso-configuration). |
| Приложение SaaS уже настроено. |  |
| Подтверждения концепции пользователям уже назначены toohello приложения |  |
| Доступны пользователя подтверждения Концепции toohello учетные данные |  |
| Пользователь подтверждения концепции зарегистрирован для Многофакторной идентификации. Используется телефон с хорошим приемом. | http://aka.ms/ssprsetup |
| Устройство hello внутренней сети. IP-адрес в диапазоне внутреннего адреса hello | Узнайте свой IP-адрес: https://www.bing.com/search?q=what%27s+my+ip |
| Устройство в hello внешней сети (может быть телефон с помощью hello оператора мобильной сети) |  |

### <a name="steps"></a>Действия

| Шаг | Ресурсы |
| --- | --- |
| Go tooAzure AD портал управления: колонке условного доступа | [Портал управления Azure AD: условный доступ](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/Policies) |
| Создайте политику условного доступа:<br/>— Нацельтесь на пользователей подтверждения концепции в разделе "Пользователи и группы".<br/>— Нацельтесь на приложение подтверждения концепции в разделе "Облачные приложения".<br/>— Нацельтесь на все расположения, кроме надежных, в разделе "Условия" -> "Расположения". **Примечание.** Надежные IP-адреса настраиваются на [портале Многофакторной идентификации](https://account.activedirectory.windowsazure.com/UserManagement/MfaSettings.aspx).<br/>— Запросите Многофакторную идентификацию в разделе "Предоставление". | [Начало работы с условным доступом в Azure Active Directory: настройка политики](active-directory-conditional-access-azure-portal-get-started.md#policy-configuration-steps) |
| Обратитесь к приложению из корпоративной сети. | [Начало работы с условным доступом в Azure Active Directory: hello Политика тестирования](active-directory-conditional-access-azure-portal-get-started.md#testing-the-policy) |
| Обратитесь к приложению из общедоступной сети. | [Начало работы с условным доступом в Azure Active Directory: hello Политика тестирования](active-directory-conditional-access-azure-portal-get-started.md#testing-the-policy) |

### <a name="considerations"></a>Рекомендации

Если вы используете федерации, можно использовать hello локального поставщика удостоверений (IdP) toocommunicate hello внутри или за пределами корпоративной сети состояние с утверждениями. Этот метод можно использовать без toomanage hello список IP-адресов, которые может быть сложной tooassess и управления ими в крупных организациях. В этой программе установки требуется учетная запись для сценария hello «network перемещаемых» (вход пользователя в из внутренней сети hello и во время зарегистрированного в системе коммутаторы местах, например в кофейне) и убедитесь, что вы понимаете последствия hello. Дополнительные сведения: [Защита облачных ресурсов с помощью Многофакторной идентификации Azure и AD FS. Доверенные IP-адреса для федеративных пользователей](../multi-factor-authentication/multi-factor-authentication-get-started-adfs-cloud.md#trusted-ips-for-federated-users)

## <a name="privileged-identity-management-pim"></a>Управление привилегированными пользователями (PIM)

Приблизительное время tooComplete: 15 минут

### <a name="pre-requisites"></a>Предварительные требования

| Предварительные требования | Ресурсы |
| --- | --- |
| Определите hello глобального администратора, который будет входить в состав hello подтверждения Концепции для PIM | [Приступая к использованию Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md) |
| Определите hello глобального администратора, который должен стать hello администратор безопасности | [Приступая к использованию Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)<br/> [Различные административные роли в Azure Active Directory PIM](active-directory-privileged-identity-management-roles.md) |
| Необязательно: Убедитесь, что если глобальным администраторам hello установили электронной почты доступ к tooexercise уведомления по электронной почте в PIM | [Что такое Azure AD Privileged Identity Management?: настроить параметры активации роли hello](active-directory-privileged-identity-management-configure.md#configure-the-role-activation-settings)


### <a name="steps"></a>Действия

| Шаг | Ресурсы |
| --- | --- |
| Toohttps://portal.azure.com входа как глобальный администратор (GA) и колонки PIM hello начальной загрузки. Hello глобального администратора, который выполняет этот шаг запускается от имени администратора безопасности hello.  Назовем этот субъект GA1. | [С помощью мастера безопасности hello в Azure AD Privileged Identity Management](active-directory-privileged-identity-management-security-wizard.md) |
| Определите hello глобального администратора и перемещать их из постоянного tooeligible. Это должен быть отдельный администратора из hello, что используется на шаге 1 для ясности. Назовем этот субъект GA2. | [Azure AD Privileged Identity Management: Как tooadd или удалить роль пользователя](active-directory-privileged-identity-management-how-to-add-role-to-user.md)<br/>[Что такое Azure AD Privileged Identity Management?: настроить параметры активации роли hello](active-directory-privileged-identity-management-configure.md#configure-the-role-activation-settings)  |
| Теперь войдите в систему как GA2 toohttps://portal.azure.com и попробуйте изменить «Параметры пользователя». Обратите внимание, что некоторые параметры будут недоступны. | |
| В новой вкладке в hello того же сеанса как шаг 3, теперь toohttps://portal.azure.com и навигацию добавить колонку toohello hello PIM мониторинга. | [Как tooactivate и деактивация роли в Azure AD Privileged Identity Management: Добавление приложения hello Privileged Identity Management](active-directory-privileged-identity-management-how-to-activate-role.md#add-the-privileged-identity-management-application) |
| Роль глобального администратора toohello активации запроса | [Как tooactivate и деактивация роли в Azure AD Privileged Identity Management: Активация роли](active-directory-privileged-identity-management-how-to-activate-role.md#activate-a-role) |
| Обратите внимание, что если GA2 никогда не регистрировался для Многофакторной идентификации, потребуется выполнить такую регистрацию. |  |
| Вернитесь к предыдущему окну toohello исходную вкладку на шаге 3 и нажмите кнопку обновления hello в браузере hello. Обратите внимание, что теперь toochange доступа «Параметры пользователя» | |
| При необходимости Если глобальные Администраторы имеют по электронной почте включена, можно проверить GA1 и GA2 элемента папки "Входящие" и разделе hello уведомление об активации роли hello |  |
| Проверьте наличие в журнале аудита hello 8 и обратите внимание, что отображается отчет hello tooconfirm повышение hello GA2. | [Что такое Azure AD Privileged Identity Management: просмотр активности роли](active-directory-privileged-identity-management-configure.md#review-role-activity) |

### <a name="considerations"></a>Рекомендации

Эта возможность является частью Azure AD Premium P2 и/или EMS E5.

## <a name="discovering-risk-events"></a>Обнаружение событий риска

Приблизительное время tooComplete: 20 минут

### <a name="pre-requisites"></a>Предварительные требования

| Предварительные требования | Ресурсы |
| --- | --- |
| Устройство с установленным браузером Tor. | [Скачайте браузер Tor](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| Имя входа пользователя toodo доступа tooPOC hello | [Тренировочное задание по защите идентификации Azure Active Directory](active-directory-identityprotection-playbook.md) |

### <a name="steps"></a>Действия

| Шаг | Ресурсы |
| --- | --- |
| Откройте браузер Tor. | [Скачайте браузер Tor](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| Войдите в toohttps://myapps.microsoft.com с hello учетной записи пользователя для проверки Концепции | [Тренировочное задание по защите идентификации Azure Active Directory: моделирование событий риска](active-directory-identityprotection-playbook.md#simulating-risk-events) |
| Подождите 5–7 минут. |  |
| Войдите в систему как toohttps://portal.azure.com глобального администратора и откройте колонку защиты идентификации hello | https://aka.ms/aadipgetstarted |
| Откройте hello риска — колонка событий. Вы должны увидеть запись в разделе "Попытки входа с анонимных IP-адресов".  | [Тренировочное задание по защите идентификации Azure Active Directory: моделирование событий риска](active-directory-identityprotection-playbook.md#simulating-risk-events) |

### <a name="considerations"></a>Рекомендации

Эта возможность является частью Azure AD Premium P2 и/или EMS E5.

## <a name="deploying-sign-in-risk-policies"></a>Развертывание политик риска при входе в систему

Приблизительное время tooComplete: 10 минут

### <a name="pre-requisites"></a>Предварительные требования

| Предварительные требования | Ресурсы |
| --- | --- |
| Устройство с установленным браузером Tor. | [Скачайте браузер Tor](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| Права доступа, что журнал hello toodo пользователя подтверждения Концепции при тестировании |  |
| Пользователь подтверждения концепции зарегистрирован для Многофакторной идентификации. Убедитесь, что toouse телефон с хорошей приема | Стандартный блок: [Многофакторная идентификация в Azure с помощью телефонных звонков](#azure-multi-factor-authentication-with-phone-calls) |


### <a name="steps"></a>Действия

| Шаг | Ресурсы |
| --- | --- |
| Войдите в систему как toohttps://portal.azure.com глобального администратора и откройте колонку защиты идентификации hello | https://aka.ms/aadipgetstarted |
| Включите политику риска для входа:<br/>— Назначено: пользователь подтверждения концепции<br/>— Условия: риск входа средний или выше (вход из анонимного расположения относится к среднему уровню риска)<br/>— Элементы управления: требовать Многофакторную идентификацию | [Тренировочное задание по защите идентификации Azure Active Directory: риск при входе](active-directory-identityprotection-playbook.md#sign-in-risk) |
| Откройте браузер Tor. | [Скачайте браузер Tor](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| Войдите в toohttps://myapps.microsoft.com с hello учетной записи пользователя для проверки концепции |  |
| Обратите внимание hello многофакторной проверки Подлинности запроса | [Процедуры входа с защитой идентификации Azure AD: восстановление входа, представлявшего риск](active-directory-identityprotection-flows.md#risky-sign-in-recovery)

### <a name="considerations"></a>Рекомендации

Эта возможность является частью Azure AD Premium P2 и (или) EMS E5. Дополнительные сведения о событиях риска посетите toolearn: [событий риска Azure Active Directory](active-directory-reporting-risk-events.md)

## <a name="configuring-certificate-based-authentication"></a>Настройка проверки подлинности на основе сертификата

Приблизительное время toocomplete: 20 минут

### <a name="pre-requisites"></a>Предварительные требования

| Предварительные требования | Ресурсы |
| --- | --- |
| Устройство с подготовленным сертификатом пользователя (Windows, iOS или Android) из корпоративной PKI. | [Развертывание сертификатов пользователей](https://msdn.microsoft.com/library/cc770857.aspx) |
| Домен Azure AD в федерации с ADFS. | [Azure AD Connect и федерация](./connect/active-directory-aadconnectfed-whatis.md)<br/>[Обзор служб сертификатов Active Directory](https://technet.microsoft.com/library/hh831740.aspx)|
| Для устройств iOS требуется установленное приложение Microsoft Authenticator. | [Приступая к работе с приложением для проверки подлинности Microsoft hello](../multi-factor-authentication/end-user/microsoft-authenticator-app-how-to.md) |

### <a name="steps"></a>Действия

| Шаг | Ресурсы |
| --- | --- |
| Включите параметр "Проверка подлинности сертификата" в службах ADFS. | [Настройка политик проверки подлинности: tooconfigure основной проверки подлинности глобально в Windows Server 2012 R2](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-authentication-policies#to-configure-primary-authentication-globally-in-windows-server-2012-r2) |
| Необязательно: включите проверку подлинности на основе сертификата в Azure AD для клиентов Exchange Active Sync. | [Приступая к работе с аутентификацией на основе сертификата в Azure Active Directory](active-directory-certificate-based-authentication-get-started.md) |
| Перейдите в панель tooAccess и проверку подлинности с помощью сертификата пользователя | https://myapps.microsoft.com |

### <a name="considerations"></a>Рекомендации

Дополнительные сведения о предупреждениях при выполнении этого развертывания посетите toolearn: [служб федерации Active Directory: сертификат проверки подлинности в Azure AD & Office 365](https://blogs.msdn.microsoft.com/samueld/2016/07/19/adfs-certauth-aad-o365/)



> [!NOTE]
> Владение сертификатом пользователя нужно защитить. Это можно сделать, управляя устройствами или используя ПИН-код (для смарт-карт).



[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]
