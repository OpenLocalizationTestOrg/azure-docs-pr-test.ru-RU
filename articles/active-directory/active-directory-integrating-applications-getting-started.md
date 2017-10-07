---
title: "aaaGet запущена интеграция Azure AD с приложениями | Документы Microsoft"
description: "Эта статья представляет собой вводное руководство по интеграции Azure Active Directory (AD) с локальными приложениями и облачными приложениями."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: db6d210d-c970-49e9-bd20-36d984bcd1c3
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.openlocfilehash: 5a7a851e8418083fee72ab58477a9cab75d0d4bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-azure-active-directory-with-applications-getting-started-guide"></a>Руководство по интеграции Azure Active Directory с приложениями
## <a name="overview"></a>Обзор
Этот раздел является предполагаемым toogive вы план интеграция приложений с Azure Active Directory (AD). Каждый из приведенных ниже разделах hello содержать краткую сводку более подробные статьи и позволяют определить, какие части данного руководства по началу работы, соответствующие tooyou.  Переходить по ссылкам hello для более подробного изучения на каждый субъект.

## <a name="before-you-begin-take-inventory"></a>Инвентаризация перед началом работы
Прежде чем приступить к toointegrating приложений с Azure AD, где используется и где требуется toogo это важные tooknow.  Hello следующие вопросы, предполагаемого toohelp, которую вы думаете о проекта интеграции приложения Azure AD.

### <a name="application-inventory"></a>Инвентаризация приложений
* Где находятся все ваши приложения? Кто ими владеет?
* Какой тип проверки подлинности требуется для приложений?
* Лиц, которые должны получать доступ к приложениям toowhich?
* Вы хотите, чтобы toodeploy новое приложение?
  * Вы создадите его локально и развернете в экземпляре службы вычислений Azure?
  * Вы будете использовать доступное в hello коллекции приложений Azure?

### <a name="user-and-group-inventory"></a>Инвентаризация пользователей и групп
* Где находятся учетные записи пользователей?
  * Локальная служба Active Directory
  * Azure AD
  * в отдельной базе данных приложений, владельцем которой вы являетесь;
  * в несанкционированных приложениях;
  * Все выше hello
* Какие разрешения и роли в настоящее время назначены пользователям? Нужна tooreview свой доступ, или вы уверены, что назначение доступа и роли пользователя подходят теперь?
* В вашем локальном каталоге Active Directory уже созданы группы?
  * Как эти группы упорядочены?
  * Которые являются членами группы hello?
  * Какие назначения разрешений и ролей hello групп в настоящее время у?
* Потребуется ли tooclean копирование баз данных пользователя или группу перед интеграции?  (Это чрезвычайно важный вопрос, ведь результат напрямую зависит от исходного состояния.)

### <a name="access-management-inventory"></a>Инвентаризация управления доступом
* Как вы в настоящее время управлять tooapplications доступ пользователя? Требуется ли, toochange?  Определены ли другие способы доступа toomanage, такие как с [RBAC](role-based-access-control-configure.md) например?
* Зачем toowhat доступа?

Может быть нет tooall hello ответы из этих вопросов заранее, но это неважно.  Это руководство поможет вам ответить на некоторые из этих вопросов и принять обоснованные решения.

## <a name="prerequisites"></a>Предварительные требования
* Подписка Azure и каталог Azure Active Directory.  Если у вас еще нет подписки Azure, вы можете получить бесплатную пробную версию Azure на 30 дней. [Просто попробуйте!](https://azure.microsoft.com/trial/get-started-active-directory/)

## <a name="application-integration-with-azure-ad"></a>Интеграция приложений с Azure AD
### <a name="finding-unsanctioned-cloud-applications-with-cloud-app-discovery"></a>Поиск несанкционированных облачных приложений с Cloud App Discovery
Как было сказано выше, могут обнаружиться приложения, которые до сих пор были вне поля зрения вашей организации.  В рамках процесса инвентаризации hello это возможных toofind санкционировано облачных приложений. См. статью [Поиск неуправляемых облачных приложений с помощью Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).

### <a name="authentication-types"></a>Типы проверки подлинности
Каждое приложение может иметь разные требования к проверке подлинности. С помощью Azure AD сертификаты подписи можно использовать с приложениями, использующими SAML 2.0, WS-Federation или протоколы подключения OpenID, а также единый вход с паролем. Дополнительные сведения о типах аутентификации в приложениях для использования с Azure AD см. в статье [Управление сертификатами для федеративного единого входа в Azure Active Directory](active-directory-sso-certs.md) и разделе [Единый вход на основе пароля](active-directory-appssoaccess-whatis.md).

### <a name="enabling-sso-with-azure-ad-app-proxy"></a>Включение единого входа с помощью прокси приложений Azure AD
С помощью прокси приложения Microsoft Azure AD вы можете предоставить доступ tooapplications безопасно, расположенный в частной сети из любого места и с любого устройства. После установки в своей среде соединителя прокси-сервера приложения его можно легко настроить с Azure AD.

### <a name="integrating-applications-with-azure-ad"></a>Интеграция приложений с Azure AD
Hello ниже статьях рассматриваются различные способы hello приложения интеграции с Azure AD и предоставляют некоторые рекомендации.

* [Определить, какие toouse Active Directory](active-directory-administer.md)
* [С помощью приложения из коллекции Azure приложения hello](active-directory-appssoaccess-whatis.md)
* [Список учебников по интеграции приложений SaaS с Azure Active Directory.](active-directory-saas-tutorial-list.md)

## <a name="managing-access-tooapplications"></a>Управление доступом tooapplications
Hello следующих статьях представлено описание способов управления tooapplications доступ, как только они интегрированы с Azure AD с помощью соединителей Azure AD и Azure AD.

* [Управление tooapps доступ с помощью Azure AD](active-directory-managing-access-to-apps.md)
* [Автоматическая подготовка пользователей и ее отзыв для приложений SaaS в Azure Active Directory.](active-directory-saas-app-provisioning.md)
* [Назначение пользователей tooan приложения](active-directory-applications-guiding-developers-assigning-users.md)
* [Назначение группы tooan приложения](active-directory-applications-guiding-developers-assigning-groups.md)
* [Совместное использование учетных записей.](active-directory-sharing-accounts.md)

## <a name="integrating-custom-applications"></a>Интеграция пользовательских приложений
Если вы пишете приложение на новое и разработчики tooassist благодаря использованию power hello Azure AD, см. раздел [Guiding разработчики](active-directory-applications-guiding-developers-for-lob-applications.md).

Если tooadd вашего пользовательского приложения toohello коллекции приложений Azure, см. [«Принеси свое приложение» с конфигурацией самообслуживания Azure AD SAML](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx).

## <a name="see-also"></a>См. также
* [Указатель статьей по управлению приложениями в Azure Active Directory](active-directory-apps-index.md)

