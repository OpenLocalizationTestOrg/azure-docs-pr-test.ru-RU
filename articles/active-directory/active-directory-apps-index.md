---
title: "aaaArticle индекс для управления приложениями в Azure Active Directory | Microsoft Azure"
description: "Узнайте, как toocustomize hello срок действия сертификатов федерации, а также как toorenew сертификатов, которые скоро истекает."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 5321b8e4-2afa-4dfe-8d53-4add7abb5ec8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.openlocfilehash: f8a584baa94dc50e279899074f50160978256559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="article-index-for-application-management-in-azure-active-directory"></a>Указатель статей по управлению приложениями в Azure Active Directory
Эта страница содержит полный список каждого документа, запись о hello различные функции, связанные с приложением в Azure Active Directory (Azure AD).

Нет области Основные функции tooeach краткое описание, а также рекомендации по какой tooread статьи, в зависимости от того, какую информацию вы ищете.

## <a name="overview-articles"></a>Обзор статей
в следующей статье Hello подходят отправная точка для тех, кто просто краткое описание функций управления приложениями в Azure AD.

| Путеводитель по статьям |  |
|:---:| --- |
| Введение toohello приложения управления проблемы, которые решает Azure AD |[Управление приложениями с помощью Azure Active Directory (AD)](active-directory-enable-sso-scenario.md) |
| Обзор hello различные функции в Azure AD, связанные с tooenabling единого входа, определять, кто имеет доступ к tooapps и как пользователям запускать приложения |[Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md) |
| Рассмотрим hello различные этапы при установке приложения в Azure AD |[Интеграция Azure Active Directory с приложениями](active-directory-integrating-applications-getting-started.md)<br /><br />[Включение единого входа tooSaaS приложений](active-directory-sso-integrate-saas-apps.md)<br /><br />[Управление доступом tooApps](active-directory-managing-access-to-apps.md) |
| Технические сведения о представлении приложений в Azure AD |[Как и почему приложения добавляются tooAzure AD](active-directory-how-applications-are-added.md) |

## <a name="troubleshooting-articles"></a>Статьи по устранению неполадок
Этот раздел предоставляет быстрый доступ руководства по устранению неполадок toorelevant. Дополнительные сведения о каждой функциональной области находятся на hello оставшейся части этой страницы.

| Область функций |  |
|:---:| --- |
| Федеративный единый вход |[Отладка единого входа на основе SAML в приложения в Azure Active Directory](active-directory-saml-debugging.md) |
| Единый вход на основе пароля |[Устранение неполадок hello расширение панели доступа для Internet Explorer](active-directory-saas-ie-troubleshooting.md) |
| Прокси приложения |[Устранение неполадок прокси-сервера приложений](active-directory-application-proxy-troubleshoot.md) |
| Единый вход между локальным AD и Azure AD |[Устранение неполадок синхронизации паролей](connect/active-directory-aadconnectsync-implement-password-synchronization.md#troubleshoot-password-synchronization)<br /><br />[Устранение неполадок обратной записи паролей](active-directory-passwords-troubleshoot.md#troubleshoot-password-writeback) |
| Динамическое членство в группах |[Устранение неполадок динамического членства в группах](active-directory-accessmanagement-troubleshooting.md) |

## <a name="single-sign-on-sso"></a>Единый вход (SSO)
### <a name="federated-single-sign-on-sign-into-many-apps-using-one-identity"></a>Федеративный единый вход: вход в несколько приложений с помощью одного удостоверения
Единый вход позволяет пользователям tooaccess различных приложений и служб, используя только один набор учетных данных. Федеративный единый вход — это один из методов единого входа. Пользователю, открывающему toosign в федеративной приложения получат перенаправленный tootheir организации официальным страницы входа подготовки к просмотру в Azure Active Directory и затем последовательно перенаправленный задней toohello приложения после успешной проверки подлинности.

| Путеводитель по статьям |  |
|:---:| --- |
| Введение toofederation и другие виды единого входа |[Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md) |
| Тысячи приложений SaaS, предварительно интегрированных с Azure AD, для которых можно с легкостью настроить единый вход |[Приступая к работе с коллекцией приложений Azure AD hello](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery)<br /><br />[Полный список предварительно интегрированных приложений, поддерживающих федерацию](http://aka.ms/aadfederatedapps)<br /><br />[Как приложения tooAdd toohello коллекции приложений Azure AD.](active-directory-app-gallery-listing.md) |
| Более 150 приложения учебники по как tooconfigure единый вход для приложений, таких как [Salesforce](active-directory-saas-salesforce-tutorial.md), [ServiceNow](active-directory-saas-servicenow-tutorial.md), [Google Apps](active-directory-saas-google-apps-tutorial.md), [Workday](active-directory-saas-workday-tutorial.md)и многое другое |[Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md) |
| Как установить и настроить конфигурацию единого входа toomanually |[Как tooConfigure tooApps федеративного единого входа, не входящих в коллекцию приложений Azure Active Directory hello](active-directory-saas-custom-apps.md)<br /><br />[Как tooCustomize утверждений, выданных в hello токена SAML для Pre-Integrated приложений](active-directory-saml-claims-customization.md) |
| Поиск и устранение неисправностей для федеративных приложений, использующих протокол SAML hello |[Устранение неполадок единого входа на основе SAML](active-directory-saml-debugging.md) |
| Как tooconfigure срок действия сертификата ваше приложение и как toorenew сертификатов |[Управление сертификатами для федеративного единого входа в Azure Active Directory](active-directory-sso-certs.md) |

Федеративного единого входа для всех версий Azure AD для копирования tooten приложений на пользователя. [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) поддерживает неограниченное количество приложений. Если ваша организация имеет [Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/) или [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/), то вы можете [используйте группы приложений toofederated для доступа к tooassign](#managing-access-to-applications).

### <a name="password-based-single-sign-on-account-sharing-and-sso-for-non-federated-apps"></a>Единый вход на основе пароля: совместное использование учетных записей и единый вход для нефедеративных приложений
tooenable единого входа tooapplications, не поддерживающих федерацию, Azure AD предлагает пароль возможности управления, которые можно безопасно хранить пароли tooSaaS приложений и автоматически вход пользователей в эти приложения. Используя эти функции, можно с легкостью задать необходимые учетные данные для новых учетных записей и совместно с другими использовать общие учетные записи. Пользователи не должны обязательно tooknow hello учетные данные toohello учетные записи, которые они ей предоставляется доступ к.

| Путеводитель по статьям |  |
|:---:| --- |
| Works SSO введение паролю toohow и краткий технический обзор |[Единый вход на основе пароля](active-directory-appssoaccess-whatis.md#password-based-single-sign-on) |
| Список связанных tooaccount сценарии hello совместного использования и как решаются эти проблемы с помощью Azure AD |[Совместное использование учетных записей в Azure AD](active-directory-sharing-accounts.md) |
| Автоматически измените пароль hello для определенных приложений через определенные интервалы |[Automated Password Rollover (preview) (Автоматическая смена пароля (предварительная версия))](https://blogs.technet.microsoft.com/enterprisemobility/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview/) |
| Развертывание и устранение неполадок руководства по версии Internet Explorer hello hello расширение управления пароля Azure AD |[Как tooDeploy hello расширение панели доступа для Internet Explorer с помощью групповой политики](active-directory-saas-ie-group-policy.md)<br /><br />[Устранение неполадок hello расширение панели доступа для Internet Explorer](active-directory-saas-ie-troubleshooting.md) |

Основанный на пароле единого входа для всех версий Azure AD для копирования tooten приложений на пользователя. [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) поддерживает неограниченное количество приложений. Если ваша организация имеет [Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/) или [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/), то вы можете [использования групп доступа tooapplications tooassign](#managing-access-to-applications). Автоматическая смена пароля — это функция [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) .

### <a name="app-proxy-single-sign-on-and-remote-access-tooon-premises-applications"></a>Прокси-сервер приложения: Единого входа и удаленный доступ tooon локальные приложения
При наличии приложений в частной сети, для которых требуются toobe доступ пользователей и устройств, находящихся за пределами сети hello, можно использовать приложения toothose безопасного удаленного доступа tooenable прокси приложения Azure AD.

| Путеводитель по статьям |  |
|:---:| --- |
| Общие сведения о прокси приложения Azure AD и принципах его работы |[Предоставление безопасного удаленного доступа tooon локальные приложения](active-directory-application-proxy-get-started.md) |
| Учебники по tooconfigure прокси приложения и как toopublish своего первого приложения |[Как tooSet копирование прокси приложения Azure AD](active-directory-application-proxy-enable.md)<br /><br />[Как установить tooSilently hello соединитель прокси приложения](active-directory-application-proxy-silent-installation.md)<br /><br />[Как tooPublish приложений с помощью прокси приложения](active-directory-application-proxy-publish.md)<br /><br />[Как tooUse собственные имя домена по умолчанию](active-directory-application-proxy-custom-domains.md) |
| Как tooenable единого входа и условного доступа для приложений, опубликованных с помощью прокси приложения |[Единый вход с помощью прокси приложения](active-directory-application-proxy-sso-using-kcd.md)<br /><br />[Работа с условным доступом](active-directory-application-proxy-conditional-access.md) |
| Рекомендации о том, как toouse прокси приложения для hello следующие сценарии |[Как tooSupport приложения собственного клиента](active-directory-application-proxy-native-client.md)<br /><br />[Как tooSupport приложений с поддержкой утверждений](active-directory-application-proxy-claims-aware-apps.md)<br /><br />[Каким образом tooSupport приложений опубликован на отдельные сети и расположения](active-directory-application-proxy-connectors.md) |
| Руководство по устранению неполадок прокси приложения |[Устранение неполадок прокси-сервера приложений](active-directory-application-proxy-troubleshoot.md) |

Прокси приложения — для всех версий Azure AD для копирования tooten приложений на пользователя. [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) поддерживает неограниченное количество приложений. Если ваша организация имеет [Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/) или [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/), то вы можете [использования групп доступа tooapplications tooassign](#managing-access-to-applications).

Также могут быть интересны [доменные службы Azure AD](../active-directory-domain-services/active-directory-ds-overview.md), что позволяет toomigrate tooAzure приложений вашей локальной удовлетворением hello удостоверения по-прежнему требуется этих приложений.

### <a name="enabling-single-sign-on-between-azure-ad-and-on-premises-ad"></a>Включение единого входа между Azure AD и локальной службой AD
Если ваша организация хранит Active Directory Windows Server на локальном компьютере вместе с Azure Active Directory в облаке hello, то необходимо будет tooenable единого входа между двумя этими системами. Azure AD Connect (hello программы, которая объединяет эти две системы друг с другом) предоставляет несколько параметров для настройки единого входа: создать федерацию со служб федерации Active Directory или другого поставщика федерации, или включить синхронизацию паролей.

| Путеводитель по статьям |  |
|:---:| --- |
| Общие сведения о hello единого входа для параметров, предусмотренных в Azure AD Connect, а также сведения об управлении гибридными средами |[Параметры входа в Azure AD Connect](active-directory-aadconnect-user-signin.md) |
| Общие рекомендации по управлению средами с помощью локальной службы Active Directory и Azure Active Directory |[Рекомендации по разработке архитектуры гибридной идентификации в Azure AD](active-directory-hybrid-identity-design-considerations-overview.md)<br /><br />[Интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md) |
| Рекомендации по работе с синхронизацией паролей tooenable единого входа |[Реализация синхронизации паролей с помощью Azure AD Connect](active-directory-aadconnectsync-implement-password-synchronization.md)<br /><br />[Устранение неполадок синхронизации паролей](https://support.microsoft.com/en-us/kb/2855271) |
| Рекомендации по использованию tooenable обратной записи паролей единого входа |[Приступая к работе с компонентами управления паролями](active-directory-passwords-getting-started.md)<br /><br />[Устранение неполадок с обратной записью паролей](active-directory-passwords-troubleshoot.md#troubleshoot-password-writeback) |
| Рекомендации по использованию сторонних производителей идентификаторов поставщиков tooenable единого входа |[Список совместимых сторонних идентификаторов поставщиков возможность использования tooEnable единого входа](https://aka.ms/ssoproviders) |
| Как пользователи Windows 10 можно использовать преимущества hello единым входом через присоединения Azure AD |[Расширение возможностей облака tooWindows 10 устройствами с помощью присоединения Azure Active Directory](active-directory-azureadjoin-overview.md) |

Azure AD Connect доступно для [всех выпусков Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/). Функция самостоятельного сброса пароля Azure AD поддерживается в выпусках [Azure AD уровня "Базовый"](https://azure.microsoft.com/pricing/details/active-directory/) и [Azure AD уровня "Премиум"](https://azure.microsoft.com/pricing/details/active-directory/). Tooon обратной записи паролей в локальной AD — [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) компонентов.

### <a name="conditional-access-enforce-additional-security-requirements-for-high-risk-apps"></a>Условный доступ: принудительное выполнение дополнительных требований к безопасности для приложений с высоким уровнем риска
После настройки-tooyour приложениям и ресурсам, можно затем дальнейшей защитить уязвимых приложений путем применения специальные требования по безопасности для каждого приложения toothat входа. Например можно использовать toodemand Azure AD, что все конкретного приложения tooa доступа всегда требовать многофакторную проверку подлинности, независимо от того, является ли приложение innately поддерживает эту функцию. Другой распространенный пример условного доступа является доверенного toorequire обеспечить пользователями подключенных toohello организации сети в порядке tooaccess конфиденциальности приложения.

| Путеводитель по статьям |  |
|:---:| --- |
| Введение toohello условного доступа предоставляет через Azure AD, Office 365 и Intune |[Управление рисками с помощью условного доступа](active-directory-conditional-access.md) |
| Как tooenable условный доступ к hello следующие типы ресурсов |[Условный доступ к приложениям SaaS](active-directory-conditional-access-azuread-connected-apps.md)<br /><br />[Условный доступ к службам Office 365](active-directory-conditional-access-device-policies.md)<br /><br />[Условный доступ к локальным приложениям](active-directory-conditional-access.md)<br /><br />[Работа с условным доступом](active-directory-application-proxy-conditional-access.md) |

| Tooregister устройствами с помощью Azure Active Directory на очередность использования tooenable политики условного доступа на основе устройств | [Общие сведения о регистрации устройств Azure Active Directory](active-directory-conditional-access-device-registration-overview.md)<br /><br />[Как tooEnable Автоматическая регистрация устройства для устройства Windows, присоединенные к домену](active-directory-conditional-access-automatic-device-registration.md)<br />— [Действия для устройств Windows 8.1](active-directory-conditional-access-automatic-device-registration-setup.md)<br />— [Действия для устройств Windows 7](active-directory-conditional-access-automatic-device-registration-setup.md) |

| Как toouse hello приложение для проверки подлинности Microsoft для двухшаговой проверки | [Проверки подлинности Майкрософт](../multi-factor-authentication/end-user/microsoft-authenticator-app-how-to.md) |

Условный доступ — это функция [Azure AD уровня "Премиум"](https://azure.microsoft.com/pricing/details/active-directory/) .

## <a name="apps--azure-ad"></a>Приложения и Azure AD
### <a name="cloud-app-discovery-find-which-saas-apps-are-being-used-in-your-organization"></a>Cloud App Discovery: поиск приложений SaaS, используемых в вашей организации
Cloud App Discovery помогает ИТ-отделы узнать, какие приложения SaaS используются в организации hello. Его можно измерение использования приложений и популярности, так что он может определить, какие приложения будут выполняться эффективнее hello наиболее сборщику переведена в режим в группе управления ИТ и интегрированы с Azure AD.

| Путеводитель по статьям |  |
|:---:| --- |
| Общие сведения о принципах работы Cloud App Discovery |[Поиск несанкционированных облачных приложений с Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md) |
| Подробно изучить, как она работает с tooquestions ответы на конфиденциальность |[Вопросы безопасности и конфиденциальности Cloud App Discovery](active-directory-cloudappdiscovery-security-and-privacy-considerations.md) |
| Часто задаваемые вопросы |[FAQ for Cloud App Discovery (Часто задаваемые вопросы о Cloud App Discovery)](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx) |
| Руководства по развертыванию Cloud App Discovery |[Руководство по развертыванию групповой политики](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)<br /><br />[Руководство по развертыванию System Center](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)<br /><br />[Параметры реестра Cloud App Discovery для прокси-служб](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md) |
| журнал агента Cloud App Discovery toohello обновления изменений Hello |[Change log (Журнал изменений)](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx) |

Cloud App Discovery — это функция [Azure AD уровня "Премиум"](https://azure.microsoft.com/pricing/details/active-directory/) .

### <a name="automatically-provision-and-deprovision-user-accounts-in-saas-apps"></a>Автоматическая подготовка учетных записей пользователей и ее отзыв в приложениях SaaS
Автоматизация создания hello, обслуживание и удаление удостоверения пользователей для приложений SaaS, таких как Dropbox, Salesforce, ServiceNow и многое другое. Соответствует и синхронизацию существующих удостоверений между Azure AD и SaaS приложениях и управления доступом, автоматически отключив учетные записи, когда пользователи покидают организацию hello.

| Путеводитель по статьям |  |
|:---:| --- |
| Дополнительные сведения о работе и найти ответы на вопросы toocommon |[Автоматизировать подготовку пользователей & отзыва tooSaaS приложений](active-directory-saas-app-provisioning.md) |
| Настройка способов сопоставления сведений между Azure AD и приложением SaaS |[Настройка сопоставлений атрибутов](active-directory-saas-customizing-attribute-mappings.md)<br><br>[Запись выражений для сопоставления атрибутов](active-directory-saas-writing-expressions-for-attribute-mappings.md) |
| Как tooenable автоматической подготовки tooany приложения, поддерживающего протокол SCIM hello |[Настройка автоматической подготовки пользователей tooany SCIM-Enabled приложения](active-directory-scim-provisioning.md) |
| Как tooreport на и устранение неполадок подготовки пользователей. |[Отчеты об автоматической подготовке пользователей](active-directory-saas-provisioning-reporting.md)<br><br>[Уведомления о подготовке](active-directory-saas-account-provisioning-notifications.md)<br><br>[Устранение неполадок при подготовке пользователей](active-directory-application-provisioning-content-map.md) |
| Ограничение, получающему подготовленных tooan приложения на основе значений их атрибутов |[Подготовка приложений на основе атрибутов с использованием фильтров области](active-directory-saas-scoping-filters.md) |

Автоматическая подготовка пользователей доступен для всех выпусков Azure AD для копирования tooten приложений на пользователя. [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) поддерживает неограниченное количество приложений. Если ваша организация имеет [Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/) или [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/), а затем вы можете [использовать toomanage групп получить подготовить пользователей, которые](#managing-access-to-applications).

### <a name="building-applications-that-integrate-with-azure-ad"></a>Создание приложений, которые интегрируются с Azure AD
Если вашей организации разработку и обслуживание бизнес-приложений (LoB), или если вы разработчик приложения с клиентами, которые используют Azure Active Directory, hello следующие учебники помогут интеграция приложений с Azure AD.

| Путеводитель по статьям |  |
|:---:| --- |
| Рекомендации для ИТ-специалистов и разработчиков приложений по интеграции приложений с Azure AD |[Hello ИТ-специалиста руководства по разработке приложений для Azure AD](active-directory-applications-guiding-developers-for-lob-applications.md)<br /><br />[Hello в руководстве разработчика для Azure Active Directory](active-directory-developers-guide.md) |
| Как добавить tooapplication поставщиков их приложений toohello коллекции приложений Azure AD. |[Перечисление приложения в коллекции приложений Azure Active Directory hello](active-directory-app-gallery-listing.md) |
| Как toomanage доступ к toodeveloped приложений, использующих Azure Active Directory |[Как tooEnable назначение пользователя для разработки приложений](active-directory-applications-guiding-developers-requiring-user-assignment.md)<br /><br />[Назначение пользователей tooyour приложения](active-directory-applications-guiding-developers-assigning-users.md)<br /><br />[Назначение группы tooyour приложения](active-directory-applications-guiding-developers-assigning-groups.md) |

При разработке приложений потребительском, можно получить с помощью [Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/) , чтобы не нужно toodevelop собственные toomanage системы удостоверений пользователей. [Подробнее](../active-directory-b2c/active-directory-b2c-overview.md).

## <a name="managing-access-tooapplications"></a>Управление доступом tooApplications
### <a name="using-groups-and-self-service-toomanage-who-has-access-toowhich-apps"></a>Использование групп и toomanage самообслуживания, кто имеет доступ toowhich приложений
toohelp вы управляете, имеющих доступ к ресурсам toowhich, Azure Active Directory позволяет tooset назначения и разрешения в масштабе, с помощью групп. ИТ может tooenable возможностей самообслуживания, чтобы пользователи могли запрашивать разрешение, просто нужным для них.

| Путеводитель по статьям |  |
|:---:| --- |
| Обзор функций управления доступом Azure AD |[Введение tooManaging tooApps доступа](active-directory-managing-access-to-apps.md)<br /><br />[Как работает управление доступом в Azure AD](active-directory-manage-groups.md)<br /><br />[Как tooManage группы tooUse tooSaaS доступ приложений](active-directory-accessmanagement-group-saasapps.md) |
| Включение самостоятельного управления приложениями и группами |[Самостоятельное управление приложениями](active-directory-self-service-application-access.md)<br /><br />[Настройка Azure Active Directory для управления самостоятельным доступом к приложениям](active-directory-accessmanagement-self-service-group-management.md) |
| Указания по настройке групп в Azure AD |[Как tooCreate групп безопасности](active-directory-accessmanagement-manage-groups.md)<br /><br />[Как tooDesignate владельцами группы](active-directory-accessmanagement-managing-group-owners.md)<br /><br />[Как tooUse hello «все пользователи» группы](active-directory-accessmanagement-dedicated-groups.md) |
| Используйте динамические группы tooautomatically заполнения членства в группе с помощью правила членства, основанное на атрибутах |[Динамическое членство в группах: расширенные правила](active-directory-accessmanagement-groups-with-advanced-rules.md)<br /><br />[Устранение неполадок динамического членства в группах](active-directory-accessmanagement-troubleshooting.md) |

Управление доступом к приложениям на основе групп поддерживается в [Azure AD уровня "Базовый"](https://azure.microsoft.com/pricing/details/active-directory/) и [Azure AD уровня "Премиум"](https://azure.microsoft.com/pricing/details/active-directory/). Самостоятельное управление группами и приложениями, а также динамические группы — это функции [Azure AD уровня "Премиум"](https://azure.microsoft.com/pricing/details/active-directory/) .

### <a name="b2b-collaboration-enable-partner-access-tooapplications"></a>Совместная работа B2B: Включить tooapplications доступа партнера
Если вашего бизнеса имеет партнерские отношения с другими компаниями, скорее всего, необходимо toomanage партнера tooyour доступа к корпоративным приложениям. Azure Active Directory B2B совместной работы обеспечивает простой и безопасный способ tooshare приложений с партнерами.

| Путеводитель по статьям |  |
|:---:| --- |
| Общие сведения о различных функциях Azure AD, с помощью которых можно управлять внешними пользователями, такими как партнеры, клиенты и т. д. |[Сравнение возможностей управления внешними удостоверениями с помощью Azure Active Directory](active-directory-b2b-compare-external-identities.md) |
| Введение tooB2B совместной работы и как tooget запущена |[Простая и надежная облачная интеграция партнеров с Azure AD](active-directory-b2b-what-is-azure-ad-b2b.md)<br /><br />[Служба Azure Active Directory B2B Collaboration](active-directory-b2b-collaboration-overview.md) |
| Подробно изучить совместной работы Azure AD B2B и как toouse его |[Принципы работы службы совместной работы B2B](active-directory-b2b-how-it-works.md)<br /><br />[Текущие ограничения службы совместной работы Azure AD B2B](active-directory-b2b-current-limitations.md)<br /><br />[Подробное пошаговое руководство по использованию службы совместной работы Azure Active Directory (Azure AD) B2B](active-directory-b2b-detailed-walkthrough.md) |
| Справочные статьи, содержащие технические сведения о том, как работает служба совместной работы Azure AD B2B |[Формат CSV-файла для добавления пользователей партнера](active-directory-b2b-references-csv-file-format.md)<br /><br />[Атрибуты пользователя, затронутые службой совместной работы Azure AD B2B](active-directory-b2b-references-external-user-object-attribute-changes.md)<br /><br />[Формат внешнего пользовательского токена для предварительной версии службы Azure Active Directory B2B Collaboration](active-directory-b2b-references-external-user-token-format.md) |

Служба совместной работы B2B в настоящее время доступна для [всех выпусков Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).

### <a name="access-panel-a-portal-for-accessing-apps-and-self-service-features"></a>Панель доступа: портал для доступа к приложениям и функциям самообслуживания
Hello панели доступа Azure AD является где конечным пользователям можно запустить их приложения и доступа hello функций самообслуживания, позволяющие им toomanage своих приложений и членства в группах. В дополнение к этому toohello панели доступа, другие параметры для доступа к приложениям с поддержкой единого входа включаются в расположенном ниже списке hello.

| Путеводитель по статьям |  |
|:---:| --- |
| Сравнение hello различных функций, доступных для развертывания приложений-toousers |[Развертывание tooUsers интегрированные приложения Azure AD](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users) |
| Обзор hello панели доступа и его мобильных эквивалентные MyApps. |[Введение tooAccess панели и MyApps.](active-directory-saas-access-panel-introduction.md)<br />— [iOS](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8)<br />— [Android](https://play.google.com/store/apps/details?id=com.microsoft.myapps) |
| Как приложения Azure AD tooaccess из hello веб-сайте Office 365 |[С помощью hello средство запуска приложений Office 365](https://support.office.com/en-us/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a) |
| Как приложения Azure AD tooaccess из hello мобильное приложение Intune Managed Browser |[Управление доступом в Интернет с помощью политик управляемого браузера в Microsoft Intune](https://technet.microsoft.com/en-us/library/dn878029.aspx)<br />— [iOS](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8)<br />— [Android](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser) |
| Как приложения Azure AD tooaccess tooinitiate прямые ссылки единого входа |[Получение приложений tooYour прямые ссылки входа](active-directory-appssoaccess-whatis.md#direct-sign-on-links-for-federated-password-based-or-existing-apps) |

Панель доступа доступна для [всех выпусков Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).

### <a name="reports-easily-audit-app-access-changes-and-monitor-sign-ins-tooapps"></a>Отчеты о легко проводить аудит изменения доступа приложения и контролировать tooapps входа в систему
Azure Active Directory предоставляет несколько отчетов и оповещений toohelp отслеживать tooapplications доступа вашей организации. Можно получать оповещения для приложений tooyour аномальных попыток входа в систему, и вы можете отслеживать, когда и почему изменено приложение tooan доступа пользователей.

| Путеводитель по статьям |  |
|:---:| --- |
| Общие сведения о функции создания отчетов в Azure Active Directory hello |[Приступая к работе со средством создания отчетов Azure Active Directory](active-directory-reporting-getting-started.md) |
| Как hello toomonitor входа и применения приложений пользователей |[Просмотр отчетов о доступе и использовании](active-directory-view-access-usage-reports.md) |
| Отслеживать изменения, внесенные toowho можно получить доступ к конкретному приложению |[События отчета аудита Azure Active Directory](active-directory-reporting-audit-events.md) |
| Экспорт данных hello этих средств tooyour предпочтительные отчеты с помощью hello Reporting API |[Приступая к работе с API отчетов Azure AD "hello"](active-directory-reporting-api-getting-started.md) |

какие отчеты входят в состав различных выпусках Azure Active Directory, toosee [щелкните здесь](active-directory-view-access-usage-reports.md).

## <a name="see-also"></a>См. также
[Что такое Microsoft Azure Active Directory](active-directory-whatis.md)

[Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/)

[Доменные службы Azure Active Directory](https://azure.microsoft.com/services/active-directory-ds/)

[Azure Multi-Factor Authentication](https://azure.microsoft.com/services/multi-factor-authentication/)
