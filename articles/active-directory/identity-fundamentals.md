---
title: "aaaFundamentals диспетчера удостоверений Azure | Документы Microsoft"
description: 
keywords: 
author: jeffgilb
manager: femila
ms.reviewr: jsnow
ms.author: jeffgilb
ms.date: 7/5/2017
ms.topic: article
ms.prod: 
ms.service: azure
ms.technology: 
ms.assetid: 
ms.custom: it-pro
ms.openlocfilehash: a9710b8e543cdbb2f78ea9e3f83b183e1983b31d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="fundamentals-of-azure-identity-management"></a>Основы управления удостоверениями Azure
Как больше и больше цифровых ресурсам компании живете за пределами корпоративной сети hello в облаке hello и на устройствах, отлично облачной идентификацией и доступом решением по управлению важнейшим фактором. Облачные удостоверения стали hello лучшим способом toomaintain управления over и видимость, как и когда пользователи получить доступ к корпоративным приложениям и данным.

Корпорация Майкрософт защита облачных удостоверений для более десяти лет и теперь с [Azure Active Directory (AD)](https://docs.microsoft.com/azure/active-directory/active-directory-editions), эти же системы защиты, доступных tooyou. С помощью Azure AD корпоративные администраторы могут легко обеспечить подотчетность пользователей и администраторов, а также повысить безопасность и контроль до невиданного уровня.

Azure AD Premium — облачной идентификацией и доступом решение для управления с возможностями надежную защиту, позволяющий одно удостоверение безопасности для всех приложений, защиты идентификации (улучшена за счет hello [безопасности аналитики Microsoft graph](https://www.microsoft.com/en-us/security/intelligence)) и управление привилегированными пользователями. Не просто еще одно мониторинга или отчетов средства Azure AD Premium можно защиты учетных записей пользователей в режиме реального времени и разрешить вы toocreate доступ риска, адаптивной политики tooprotect данных вашей организации.

Ниже представлено короткое видео с краткими сведениями о защите удостоверений и управлении ими в Azure AD.
<iframe width="560" height="315" src="https://www.youtube.com/embed/9LGIJ2-FKIM" frameborder="0" allowfullscreen></iframe>

Корпорация Майкрософт не только предоставляет удостоверение, которое принимает везде, но также набор tooautomate средств защиты и управления ими ИТ вашей организации. Даже после появления hello облачных вычислений, по-прежнему требовать toomanage и управлять ИТ-задач, как службы технической поддержки вызывает tooreset пароли пользователей группа пользователей, управление и запросов приложений. Усложнения дополнительные действия, сотрудники находятся теперь перевод toowork их личных устройствах и с помощью доступны приложениям SaaS. Таким образом, контроль над приложениями пользователей в корпоративных центрах обработки данных и на общедоступных облачных платформах представляет собой нетривиальную задачу.

[!INCLUDE [identity](../../includes/azure-ad-licenses.md)]

## <a name="connect-on-premises-active-directory-with-azure-ad-and-office-365"></a>Подключение локальной службы Active Directory к Azure AD и Office 365
Организациям, которые сделаны больших вложений в локальной среде Active Directory можно расширить toohello этих вложений в облако путем интеграции с Azure AD в своих локальных каталогов [гибридное Управление удостоверениями](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview). Это поможет повысить продуктивность работы пользователей, так как они получают общее удостоверение для доступа к ресурсам независимо от своего местоположения. Пользователей и организаций могут использовать единый вход (SSO) tooaccess оба локальных ресурсов и облачных служб, таких как Office 365.

[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) — единственное средство hello, необходимо сделать интеграции hello tooget. Azure AD Connect предоставляет возможности toosupport должен синхронизацию удостоверений и заменяет старые версии средств интеграции удостоверений, таких как DirSync и Azure AD Sync. В Azure AD Connect управление удостоверениями и синхронизация локальной среды и Azure AD обеспечивается за счет следующих операций и компонентов:

- Синхронизация. Cлужбы синхронизации отвечают за создание пользователей, групп и других объектов. Он также отвечает за убедиться, что сведения об удостоверении для локальных пользователей и групп них совпадающие hello облака. Обратная запись пароля также может быть включена tookeep локальных каталогов синхронизирован, когда пользователь обновляет свой пароль в Azure AD.
- AD FS - федерация — дополнительные возможности, предоставляемые Azure AD Connect, который можно использовать tooconfigure в гибридной среде с помощью локальной инфраструктуры AD FS. Федерации может использоваться организаций tooaddress сложных развертываний, таких как единый вход, принудительного применения политики входа в AD и смарт-карты или сторонних производителей многофакторной проверки Подлинности.
- Наблюдение за работоспособностью - [Azure AD Connect Health](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health) могут предоставлять надежные мониторинга и предоставление центрального расположения в hello Azure портала tooview это действие.

## <a name="increase-productivity-and-reduce-helpdesk-costs-with-self-service-and-single-sign-on-experiences"></a>Повышение производительности и снижение затрат на службу поддержки за счет самообслуживания и единого входа

Сотрудники, повысить производительность при наличии у них один tooremember имя пользователя и пароль и согласованный с каждого устройства. Они также сэкономить время, когда они могут выполнять самообслуживания задачи, такие как [Сброс забытого пароля](https://docs.microsoft.com/azure/active-directory/active-directory-passwords) или запрос доступа tooan приложения без ожидания помощь службы поддержки hello.

Azure AD [расширяет локальной Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) в облаке hello Включение пользователей toouse записью основной организации для своих устройств, присоединенных к домену, ресурсам компании и все hello веб-приложений и приложений SaaS они требуется toouse tooget свою работу. В дополнение к этому toonot наличие tooremember несколько наборов имена пользователей и пароли, доступ пользователей приложения можно также автоматически подготовлены (или отмены подготовки) на основании их членства в группах организации и их состояние как сотрудники. И управления, доступ для приложений, коллекции или собственные локальных приложений, которые были разработаны и опубликованных через hello [прокси приложения Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started).

## <a name="manage-and-control-access-toocorporate-resources"></a>Управлять и контролировать доступ к ресурсам toocorporate
Microsoft удостоверениями и доступом решений Справка по управлению ИТ защитить tooapplications доступа и ресурсы между hello корпоративном центре обработки данных и в облаке hello, такие как включение дополнительных уровней проверки [многофакторной проверки подлинности](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next) и [политики условного доступа](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal). Наблюдение за подозрительной активностью с использованием расширенных отчетов, аудита и предупреждений помогает смягчить потенциальные риски безопасности.

Политики условного доступа в Azure AD Premium дает, hello администратора предприятия, hello возможность toocreate на основе политик правил доступа для любого Azure AD подключен приложения (приложений SaaS, пользовательские приложения, выполняющиеся в веб-приложения hello облаке или локально). Azure AD оценивает эти политики в режиме реального времени и применяет их каждый раз, когда пользователь пытается tooaccess приложения. Политики защиты идентификации Azure позволяют tooautomatically выполните действие при обнаружении подозрительной активности. Эти операции могут включать блокирует доступ toousers с высоким риском, включение многофакторной проверки подлинности и сброс паролей пользователей, если он будет выглядеть учетные данные были скомпрометированы.


## <a name="azure-active-directory-privileged-identity-management"></a>Управление привилегированными удостоверениями в Azure Active Directory

[Управление привилегированными пользователями](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-getting-started), входящий в состав hello Azure Active Directory Premium P2 предложения, дает toodiscover, ограничения и отслеживать административных учетных записей и их tooresources доступа в Azure Active Directory и другие Microsoft online services. Он также позволяет администрировать административный доступ по требованию в течение hello точное время, необходимое.

Управление привилегированными пользователями можно принудительно задать права администратора по требованию, чтобы администраторы могли запрашивать многофакторной проверкой подлинности, временные повышение свои права доступа для предварительно настроенных периодов времени до учетные записи вернуть обычный tooa Состояние пользователя.

## <a name="benefits-of-azure-identity"></a>Преимущества удостоверения Azure

Управление удостоверениями Azure предоставляет следующие возможности:

-   Создание единого удостоверения для каждого пользователя в пределах всей системы, управление этими удостоверениями, а также синхронизация пользователей, групп и устройств с помощью [Azure Active Directory Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).

-   Указать tooyour приложений, включая тысяч предварительно интегрированных приложений SaaS единого входа для доступа или безопасного удаленного доступа tooon локальные приложения SaaS, с помощью hello [прокси приложения Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started).

-   Возможность безопасного доступа к приложениям с применением [Многофакторной идентификации](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next) на основе правил для локальных и облачных приложений.

-   Повысить производительность труда пользователей с [самостоятельный сброс пароля](https://docs.microsoft.com/azure/active-directory/active-directory-passwords)и группы, так и приложения с помощью hello запросов доступа [MyApps портала](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-user-help).

-   Воспользоваться преимуществами hello [высокого уровня доступности и надежности](https://docs.microsoft.com/azure/architecture/resiliency/high-availability-azure-applications) элемента по всему миру, корпоративного уровня, Облачное решение управления удостоверениями и доступом.

## <a name="next-steps"></a>Дальнейшие действия
[Узнайте о решениях Azure для управления удостоверениями](https://docs.microsoft.com/azure/active-directory/understand-azure-identity-solutions)