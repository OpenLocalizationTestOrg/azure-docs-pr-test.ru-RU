---
title: "безопасность aaaAzure функции, помогающие благодаря управлению | Документы Microsoft"
description: " В этой статье предоставляет обзор функций безопасности Azure core hello, упрощающие управление удостоверениями. Microsoft удостоверениями и доступом решений Справка по управлению ИТ защитить tooapplications доступа и ресурсы между hello корпоративном центре обработки данных и в облаке hello дополнительных уровней проверки, такие как многофакторная проверка подлинности и условное Включение политики доступа. "
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 5aa0a7ac-8f18-4ede-92a1-ae0dfe585e28
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/09/2017
ms.author: terrylan
ms.openlocfilehash: f08e4f6cf2e48e455a16858b7fee08b53d5aa585
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-identity-management-security-overview"></a>Общие сведения о безопасности при управлении удостоверениями в Azure
Microsoft удостоверениями и доступом решений Справка по управлению ИТ защитить tooapplications доступа и ресурсы между hello корпоративном центре обработки данных и в облаке hello дополнительных уровней проверки, такие как многофакторная проверка подлинности и условное Включение политики доступа. Наблюдение за подозрительной активностью с использованием расширенных отчетов, аудита и предупреждений помогает смягчить потенциальные риски безопасности. [Azure Active Directory Premium](../active-directory/active-directory-editions.md) предоставляет toothousands единого входа (SaaS) облачных приложений и приложений tooweb доступ, запустите локально.

Возможность hello преимущества безопасности из Azure Active Directory (AD):

* Создание единого удостоверения для каждого пользователя в пределах гибридной системы, управление этими удостоверениями, а также синхронизация пользователей, групп и устройств.
* Предоставить доступ-tooyour приложений, включая тысяч предварительно интегрированных приложений SaaS
* Возможность безопасного доступа к приложениям с применением Multi-Factor Authentication на основе правил для локальных и облачных приложений.
* Безопасный удаленный доступ подготовки tooon в локальной веб-приложений с помощью прокси приложения Azure AD

Hello цель этой статьи — tooprovide Обзор возможностей безопасности Azure core hello, упрощающие управление удостоверениями. Мы также предоставляем tooarticles ссылками, предоставить подробные сведения о каждой функции, здесь можно получить дополнительные сведения.  

Hello статье основное внимание уделяется hello следующие возможности управления удостоверениями Azure основных компонентов:

* Единый вход
* Обратный прокси-сервер.
* Многофакторная проверка подлинности
* Наблюдение за безопасностью, оповещения и отчеты на основе машинного обучения.
* Управление удостоверениями и доступом клиентов.
* Регистрация устройства
* Управление привилегированными пользователями (PIM)
* Защита идентификации
* Управление гибридными удостоверениями.

## <a name="single-sign-on"></a>Единый вход
Единого входа (SSO) означает может tooaccess все приложения hello и ресурсы, необходимые toodo business вход только один раз, используя учетную запись отдельного пользователя. После входа, доступны все приложения hello, необходимые пользователям, которые не требуется tooauthenticate (например, введите пароль) еще раз.

Во многих организациях для эффективной работы пользователя используются такие приложения SaaS, как Office 365, Box и Salesforce. Исторически tooindividually ИТ персонал необходимости создавать и обновлять учетные записи пользователей в каждом приложении SaaS, а пользователи имели tooremember пароль для каждого приложения SaaS.

Azure AD расширяет в локальной среде Active Directory в облако hello Включение toouse пользователей основная учетная запись организации toonot только вход tootheir присоединенных к домену устройства и ресурсы компании, но также все hello и веб-приложений SaaS требуется для их задания.

Не только пользователи не имеют toomanage несколько наборов имена пользователей и пароли, доступ к приложению может быть автоматически подготовленные или отмены подготовки на основе группами в организации и их состояние в качестве сотрудника. Azure AD представляет безопасности и элементы управления доступом, позволяющие вы toocentrally управлять доступом пользователей к приложениям SaaS.

Подробнее.

* [Общие сведения о едином входе](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](../active-directory/active-directory-appssoaccess-whatis.md)
* [Интеграция единого входа Azure Active Directory с приложениями SaaS](../active-directory/active-directory-sso-integrate-saas-apps.md)

## <a name="reverse-proxy"></a>Обратный прокси-сервер.
Прокси приложения Azure AD позволяет публиковать локальных приложений, таких как [SharePoint](https://support.office.com/article/What-is-SharePoint-97b915e6-651b-43b2-827d-fb25777f446f?ui=en-US&rs=en-US&ad=US) сайтов, [Outlook Web App](https://technet.microsoft.com/library/jj657718.aspx), и [IIS](http://www.iis.net/)-приложений в частной сети на основе и обеспечивает безопасный доступ toousers вне сети. Приложение прокси-сервер предоставляет удаленный доступ и единого входа (SSO) для многих типов в локальной веб-приложения с hello тысячам приложений SaaS, поддерживающие Azure AD. Сотрудники могут войти на tooyour приложения из дома на свои собственные устройства и проверки подлинности с помощью облачных прокси.

Подробнее.

* [Включение прокси приложения Azure AD](../active-directory/active-directory-application-proxy-enable.md)
* [Публикация приложений с помощью прокси приложения Azure AD](../active-directory/active-directory-application-proxy-publish.md)
* [Единый вход с помощью прокси приложения](../active-directory/active-directory-application-proxy-sso-using-kcd.md)
* [Работа с условным доступом](../active-directory/active-directory-application-proxy-conditional-access.md)

## <a name="multi-factor-authentication"></a>Многофакторная проверка подлинности
Azure Multi-factor authentication (MFA) — это метод проверки подлинности, который требует использования hello более одного метода проверки и добавляет важный второй уровень безопасности toouser входов и транзакций. Многофакторной проверки Подлинности помогает toodata защиты доступа и приложений удовлетворением спроса на простой процесс входа в систему. Она обеспечивает строгую проверку подлинности разными способами — с помощью телефонного звонка, текстового сообщения, уведомления в мобильном приложении, кода подтверждения или OAuth-маркеров сторонних поставщиков.

Подробнее.

* [Многофакторная проверка подлинности](https://azure.microsoft.com/documentation/services/multi-factor-authentication/)
* [Что такое Azure Multi-factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)
* [Принципы работы службы Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-how-it-works.md)

## <a name="security-monitoring-alerts-and-machine-learning-based-reports"></a>Наблюдение за безопасностью, оповещения и отчеты на основе машинного обучения.
Мониторинг безопасности и оповещения, а также отчеты на базе машинного обучения, которые позволяют определить несогласованные схемы доступа, помогают защитить бизнес-процессы. Можно использовать доступа Azure Active Directory и видимость toogain отчеты об использовании hello целостности и безопасности каталога вашей организации. С этой информацией администратор каталога может лучше определить, где могут возникнуть риски безопасности, чтобы их можно создать соответствующий план toomitigate этих рисков.

В hello классический портал Azure отчеты упорядочены по hello следующих способов:

* Отчеты об аномалиях — содержат события, было найдено toobe аномальных попыток входа. Наша цель — toomake вам о таких событиях и дают разработчикам возможности toomake toobe определение о подозрительных событие.
* Отчеты о встроенных приложениях: предоставляют подробную информацию об использовании облачных приложений в вашей организации. Azure Active Directory обеспечивает интеграцию с множеством облачных приложений.
* Отчеты об ошибках — указывают ошибки, которые могут возникать при подготовке учетных записей tooexternal приложений.
* Отчеты о пользователях: предоставляют данные об использовании устройств и событиях входа для конкретного пользователя.
* Журналы действий — содержат записи всех аудированных событий в пределах hello последние 24 часа, последние 7 дней или последние 30 дней и изменения действия группы и действиях по сбросу и регистрации паролей.

Подробнее.

* [Просмотр отчетов о доступе и использовании](../active-directory/active-directory-view-access-usage-reports.md)
* [Приступая к работе со средством создания отчетов Azure Active Directory](../active-directory/active-directory-reporting-getting-started.md)
* [Руководство по отчетам Azure Active Directory](../active-directory/active-directory-reporting-guide.md)

## <a name="consumer-identity-and-access-management"></a>Управление удостоверениями и доступом клиентов.
Azure Active Directory B2C — служба управления высокой надежности, глобальных идентификаторов для приложений, ориентированных на потребителей, масштабируемая toohundreds миллионов идентификаторов. Служба интегрируется с мобильными и веб-платформами. Потребителей могут входить на tooall приложений с помощью настраиваемых интерфейсов с помощью свои существующие учетные записи социальных сетей или путем создания новых учетных данных.

В прошлом hello разработчикам приложений, желавшим toosign вверх и вход пользователей в свои приложения будет записан свой собственный код. И они бы использовали локальных баз данных и систем toostore имена пользователей и пароли. Azure Active Directory B2C предлагает организации лучше способом toointegrate потребителя удостоверений в приложения с помощью hello безопасную, основанную на стандартах платформу и большой набор расширяемый политик.

Azure Active Directory B2C позволяет клиентам регистрироваться в приложениях с использованием существующих учетных записей в социальных сетях (Facebook, Google, Amazon, LinkedIn). Кроме того, пользователи могут создавать новые учетные данные (электронный адрес и пароль или имя пользователя и пароль).

Подробнее.

* [Что такое Azure Active Directory B2C?](https://azure.microsoft.com/services/active-directory-b2c/)
* [Azure Active Directory B2C (предварительная версия): регистрация и вход пользователей в приложения](../active-directory-b2c/active-directory-b2c-overview.md)
* [Предварительная версия Azure Active Directory B2C: типы приложений](../active-directory-b2c/active-directory-b2c-apps.md)

## <a name="device-registration"></a>Регистрация устройства
Регистрации устройств в Azure AD является основой hello для устройств под управлением [условного доступа](../active-directory/active-directory-conditional-access-device-registration-overview.md) сценариев. При регистрации устройства регистрации устройств Azure Active Directory предоставляет hello устройства с использованием идентификатора, используемые tooauthenticate hello устройства при входе пользователя hello. Hello проверку подлинности устройства и атрибуты hello hello устройства, затем можно используется tooenforce политик условного доступа для приложений, размещенных в облаке hello и в локальной среде.

В сочетании с мобильными устройствами (MDM) управления например Intune, атрибуты устройства hello в Azure Active Directory обновляются с дополнительными сведениями об устройстве hello. Это позволяет вам toocreate правила условного доступа, которые осуществляют доступ к устройствам toomeet стандартов безопасности и соответствия требованиям.

Подробнее.

* [Знакомство с регистрацией устройств в Azure Active Directory](../active-directory/active-directory-conditional-access-device-registration-overview.md)
* [Автоматическая регистрация в Azure Active Directory присоединенных к домену устройств Windows](../active-directory/active-directory-conditional-access-automatic-device-registration.md)
* [Настройка автоматической регистрации присоединенных к домену устройств Windows в Azure Active Directory](../active-directory/active-directory-conditional-access-automatic-device-registration-setup.md)

## <a name="privileged-identity-management"></a>Управление привилегированными пользователями (PIM)
Active Directory (AD) Управление привилегированными пользователями Azure позволяет управлять, управление и мониторинг привилегированных удостоверений и доступа tooresources в Azure AD, а также другие Microsoft online services, например Office 365 или Microsoft Intune.

Иногда пользователи должны toocarry привилегированных операций в ресурсы Azure или Office 365 или другими приложениями SaaS. Это часто означает организации имеют toogive их постоянной привилегированным доступом в Azure AD. При этом возрастает угроза безопасности ресурсов, размещенных в облаке, поскольку организация не может эффективно отслеживать действия пользователей с привилегиями администраторов. Кроме того, скомпрометированная учетная запись с привилегированным доступом может повлиять на общую безопасность облака. Azure AD Privileged Identity Management помогает tooresolve этот риск.

Управление привилегированными пользователями Azure AD позволяет:

* видеть, какие пользователи являются администраторами Azure AD;
* Включить по запросу «по требованию» tooMicrosoft административный доступ веб-служб, таких как Office 365 и Intune
* получать отчеты по данным журнала доступа администраторов и изменениям в назначениях администраторов;
* Получать оповещения о доступа tooa привилегированной роли

Подробнее.

* [Azure AD Privileged Identity Management](../active-directory/active-directory-privileged-identity-management-configure.md)
* [Роли в службе управления привилегированными пользователями Azure AD](../active-directory/active-directory-privileged-identity-management-roles.md)
* [Azure AD Privileged Identity Management: Как tooadd или удалить роль пользователя](../active-directory/active-directory-privileged-identity-management-how-to-add-role-to-user.md)

## <a name="identity-protection"></a>Защита идентификации
Служба защиты идентификации Azure AD — это служба безопасности, которая предоставляет согласованное представление всех событий риска и возможных уязвимостей, которые могут влиять на корпоративные удостоверения. Защита идентификации использует встроенные возможности Azure Active Directory по обнаружению аномалий (они доступны в отчетах Azure AD об аномальных действиях) и включает новые типы событий риска, которые позволяют обнаруживать аномалии в реальном времени.

Подробнее.

* [Защита идентификации Azure Active Directory.](../active-directory/active-directory-identityprotection.md)
* [Channel 9: Azure AD and Identity Show: Identity Protection Preview (Канал 9. Azure Active Directory и идентификация. Предварительная версия защиты идентификации)](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

## <a name="hybrid-identity-management"></a>Управление гибридными удостоверениями.
Корпорации Майкрософт подход tooidentity диапазонов локальной и облачной hello, создание единого пользовательского удостоверения для проверки подлинности и авторизации tooall ресурсов, независимо от расположения.

Подробнее.

* [Hybrid identity white paper](http://download.microsoft.com/download/D/B/A/DBA9E313-B833-48EE-998A-240AA799A8AB/Hybrid_Identity_White_Paper.pdf)
* [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/)
* [Блог группы разработчиков Active Directory](https://blogs.technet.microsoft.com/ad/)
