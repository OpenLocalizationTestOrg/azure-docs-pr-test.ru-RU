---
title: "Учебник. Интеграция Azure Active Directory с Cisco Webex | Документация Майкрософт"
description: "Узнайте, как toouse Cisco Webex с Azure Active Directory tooenable единого входа, автоматизированной подготовки и многое другое!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 26704ca7-13ed-4261-bf24-fd6252e2072b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 9fc11e58a7acaa6fbfb32eeccbfbf85984950e67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-webex"></a>Руководство. Интеграция Azure Active Directory с Cisco Webex
Цель этого учебника Hello — tooshow hello интеграцию Azure с Cisco Webex.  
Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:

* Действующая подписка на Azure
* Клиент Cisco Webex

После завершения этого учебника, Здравствуйте, пользователи Azure AD, назначенные tooCisco будет Webex может toosingle входа в приложение hello на корпоративном сайте Cisco Webex (инициированный поставщиком вход службы) или с помощью hello [toohello введение Получить доступ к панели](active-directory-saas-access-panel-introduction.md).

Hello сценарий, описанный в этом руководстве состоит из hello следующие стандартные блоки.

* Включение интеграции приложений hello для Cisco Webex
* Настройка единого входа.
* Настройка подготовки учетных записей пользователей
* Назначение пользователей

![Сценарий](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Сценарий")

## <a name="enable-hello-application-integration-for-cisco-webex"></a>Включить hello интеграции приложений для Cisco Webex
Hello цель этого раздела — toooutline как интеграция приложения hello tooenable для Cisco Webex.

**Интеграция приложения hello tooenable для Cisco Webex, выполните hello следующие шаги.**

1. В hello классический портал Azure, hello левой области навигации, выберите **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")
2. Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.
3. Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.
   
   ![Приложения](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "Приложения")
4. Нажмите кнопку **добавить** hello нижней части страницы приветствия.
   
   ![Добавление приложения](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Добавление приложения")
5. На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.
   
   ![Добавление приложения из коллекции](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Добавление приложения из коллекции")
6. В hello **поле поиска**, тип **Cisco Webex**.
   
   ![Коллекция приложений](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Коллекция приложений")
7. В области результатов hello выберите **Cisco Webex**и нажмите кнопку **завершить** tooadd приложения hello.
   
   ![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")
   
## <a name="configure-single-sign-on"></a>Настройка единого входа

Цель этого раздела Hello — toooutline, каким образом пользователи tooenable tooauthenticate tooCisco Webex с помощью учетной записи в Azure AD, используя федерацию на основе hello SAML протокола.  

В рамках этой процедуры не toocreate требуется файл сертификата в кодировке base-64. Если вы не знакомы с этой процедурой, см. раздел [как tooconvert двоичные данные сертификата в текстовый файл](http://youtu.be/PlgrzUZ-Y1o)

**tooconfigure единого входа, выполните следующие шаги hello:**

1. В классический портал Azure, на hello hello **Cisco Webex** странице интеграции приложения щелкните **настроить единый вход** tooopen hello **Настройка единого входа** диалогового окна.
   
   ![Настройка единого входа](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Настройка единого входа")
2. На hello **предпочитаемый как toosign пользователей на tooCisco Webex** выберите **Microsoft Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.
   
   ![Настройка единого входа](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Настройка единого входа")
3. На hello **настроить URL-адрес приложения** страницы, выполните следующие шаги hello и нажмите кнопку **Далее**.
   
   ![Настройка URL-адреса приложения](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "Настройка URL-адреса приложения")   
   1. В hello **проигрывать на URL-адрес** текстовом поле введите URL-адрес клиента Cisco Webex (например: *http://contoso.webex.com*).
   2. В hello **URL-адрес ответа Cisco Webex** введите ваш **URL-адрес Cisco Webex AssertionConsumerService** (например: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company* ).
4. На hello **настройки единого входа в Cisco Webex** страницы, toodownload свой сертификат, нажмите кнопку **загрузки сертификата**, а затем сохраните файл сертификата hello на вашем компьютере.
   
   ![Настройка единого входа](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Настройка единого входа")
5. В другом окне веб-браузера войдите на свой корпоративный веб-сайт Cisco Webex в качестве администратора.
6. В меню в верхней части hello hello выберите **Администрирование сайта**.
   
   ![Администрирование сайта](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Администрирование сайта")
7. В hello **Управление сайтом** щелкните **Настройка единого входа**.
   
   ![Настройка единого входа](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "Настройка единого входа")
8. В hello раздел федеративного единого входа веб-конфигурации выполните следующие шаги hello.
   
   ![Настройка федеративного единого входа](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Настройка федеративного единого входа")  
   1. Из hello **протокол федерации** выберите **SAML 2.0**.
   2. Создайте файл **в кодировке Base-64** из скачанного сертификата.  
    >[!TIP]
    >Дополнительные сведения см. в разделе [как tooconvert двоичные данные сертификата в текстовый файл](http://youtu.be/PlgrzUZ-Y1o)
    >  
   3. Откройте сертификат в кодировке base-64 в блокноте, а затем hello копирования содержимого его.
   4. Нажмите **Импорт метаданных SAML**и вставьте сертификат в кодировке Base-64.
   5. В классический портал Azure, на hello hello **настройки единого входа в Cisco Webex** странице диалогового окна, hello копирования **URL-адрес издателя** значение, а затем вставьте его в hello **издатель для SAML (ИД IdP)** текстового поля.
   6. В классический портал Azure, на hello hello **настройки единого входа в Cisco Webex** странице диалогового окна, hello копирования **URL-адрес удаленного входа** значение, а затем вставьте его в hello **входа службы единого входа клиента URL-адрес** текстового поля.
   7. Из hello **формата идентификатора имени** выберите **адрес электронной почты**.
   8. В hello **AuthnContextClassRef** введите **urn: oasis: имена: tc: SAML:2.0:ac:classes:Password**.
   9. В классический портал Azure, на hello hello **настройки единого входа в Cisco Webex** странице диалогового окна, hello копирования **URL-адрес удаленного выхода** значение, а затем вставьте его в hello **выхода службы единого входа клиента URL-адрес** текстового поля.
   10. Нажмите кнопку **Обновить**.
9. В классический портал Azure, на hello hello **настройки единого входа в Cisco Webex** странице диалогового окна выберите Подтверждение настройки единого входа hello и нажмите кнопку **завершить**.
   
   ![Настройка единого входа](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Настройка единого входа")
   
## <a name="configure-user-provisioning"></a>Настроить подготовку учетных записей пользователей

В порядке tooenable toolog пользователей Azure AD в Cisco Webex их необходимо подготовить в Cisco Webex.  

* В случае hello Cisco Webex Подготовка выполняется вручную.

**tooprovision учетных записей пользователей, выполните следующие действия hello:**

1. Войдите в tooyour **Cisco Webex** клиента.
2. Go слишком**Управление пользователями \> добавить пользователя**.
   
   ![Добавление пользователей](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Добавление пользователей")
3. На hello раздел добавить пользователя выполните hello следующие шаги.
   
   ![Добавление пользователя](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Добавление пользователя")   
   1. Для параметра **Тип учетной записи** выберите значение **Узел**.
   2. Введите сведения hello существующего пользователя Azure AD в следующие текстовые поля hello: **имя и фамилию пользователя**, **имя пользователя**, **электронной почты**, **пароля**, **Подтверждение пароля**.
   3. Щелкните **Добавить**.

>[!NOTE]
>Можно использовать любые другие Cisco Webex пользователя средства создания учетных записей или интерфейсы API, предоставляемые Cisco Webex tooprovision учетных записей пользователей AAD. 
> 

## <a name="assign-users"></a>Назначить пользователей
tootest конфигурацию, необходимо toogrant hello Azure AD пользователей с помощью tooit доступ вашего приложения путем назначения им tooallow.

**Пользователи tooassign tooCisco Webex, выполните hello следующие шаги.**

1. В hello классический портал Azure создайте тестовую учетную запись.
2. На hello **Cisco Webex** странице интеграции приложения щелкните **назначить пользователей**.
   
   ![Назначение пользователей](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "Назначение пользователей")
3. Выберите тестового пользователя, нажмите кнопку **назначить**, а затем нажмите кнопку **Да** tooconfirm назначения.
   
   ![Да](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Да")

Tootest параметры единого входа, откройте панель доступа hello. Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

