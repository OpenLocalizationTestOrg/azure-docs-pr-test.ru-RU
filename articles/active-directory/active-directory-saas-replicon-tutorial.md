---
title: "Руководство по интеграции Azure Active Directory с Replicon | Документация Майкрософт"
description: "Узнайте, как toouse Replicon с Azure Active Directory tooenable единого входа, автоматизированной подготовки и многое другое!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 02a62f15-917c-417c-8d80-fe685e3fd601
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 4949eaf959265cfa4f732a2b73317fffe6312a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-replicon"></a>Учебник. Интеграция Azure Active Directory с Replicon
Цель этого учебника Hello — tooshow hello интеграцию Azure и Replicon. Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:

* Действующая подписка на Azure
* Клиент Replicon.

После завершения этого учебника, пользователи hello Azure AD, назначенные tooReplicon будет может toosingle вход в приложение hello на свой корпоративный сайт Replicon (инициированный поставщиком вход службы) или с помощью hello [toohello введение доступа Панель](active-directory-saas-access-panel-introduction.md).

Hello сценарий, описанный в этом руководстве состоит из hello следующие стандартные блоки.

1. Включение hello интеграции приложений для Replicon
2. Настройка единого входа.
3. Настройка подготовки учетных записей пользователей
4. Назначение пользователей

![Сценарий](./media/active-directory-saas-replicon-tutorial/IC777798.png "Сценарий")

## <a name="enable-hello-application-integration-for-replicon"></a>Включить hello интеграции приложений для Replicon
Hello цель этого раздела — toooutline как интеграция приложения hello tooenable для Replicon.

**интеграции приложения hello tooenable для Replicon, выполните следующие шаги hello.**

1. В hello классический портал Azure, hello левой области навигации, выберите **Active Directory**.
   
    ![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")
2. Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.
3. Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.
   
    ![Приложения](./media/active-directory-saas-replicon-tutorial/IC700994.png "Приложения")
4. Нажмите кнопку **добавить** hello нижней части страницы приветствия.
   
    ![Добавление приложения](./media/active-directory-saas-replicon-tutorial/IC749321.png "Добавление приложения")
5. На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.
   
    ![Добавление приложения из коллекции](./media/active-directory-saas-replicon-tutorial/IC749322.png "Добавление приложения из коллекции")
6. В hello **поле поиска**, тип **Replicon**.
   
    ![Коллекция приложений](./media/active-directory-saas-replicon-tutorial/IC777799.png "Коллекция приложений")
7. В области результатов hello выберите **Replicon**и нажмите кнопку **завершить** tooadd приложения hello.
   
    ![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")
   
## <a name="configure-single-sign-on"></a>Настройка единого входа

Цель этого раздела Hello — toooutline как tooReplicon tooauthenticate tooenable пользователей с учетной записью в Azure AD, используя федерацию на основе hello SAML протокола.

**tooconfigure единого входа, выполните следующие шаги hello:**

1. В классический портал Azure, на hello hello **Replicon** странице интеграции приложения щелкните **настроить единый вход** tooopen hello **Настройка единого входа** диалогового окна.
   
    ![Настройка единого входа](./media/active-directory-saas-replicon-tutorial/IC777801.png "Настройка единого входа")
2. На hello **предпочитаемый как toosign пользователей на tooReplicon** выберите **Microsoft Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.
   
    ![Настройка единого входа](./media/active-directory-saas-replicon-tutorial/IC777802.png "Настройка единого входа")
3. На hello **настроить URL-адрес приложения** выполните следующие шаги hello:
   
    ![Настройка URL-адреса приложения](./media/active-directory-saas-replicon-tutorial/IC777803.png "Настройка URL-адреса приложения")
  1. В hello **Replicon на URL-адрес входа** текстовом поле введите URL-адрес клиента Replicon (например: *https://na2.replicon.com/company/saml2/sp-sso/post*).
  2. В hello **URL-адрес ответа Replicon** текстовом поле введите ваш Replicon **AssertionConsumerService** URL-адрес (например: *https://global.replicon.com/! / saml2 или компании или единого входа и после*).  
      
     >[!NOTE]
     >Hello URL-адрес можно получить из метаданных Replicon hello по адресу: **https://global.replicon.com/! /saml2/\<YourCompanyKey\>**.
     > 
     > 
 
  3. Щелкните **Далее**.

4. На hello **настройки единого входа в Replicon** страницы, toodownload метаданные, нажмите кнопку **загрузить метаданные**, а затем сохраните метаданные hello на вашем компьютере.
   
    ![Настройка единого входа](./media/active-directory-saas-replicon-tutorial/IC777804.png "Настройка единого входа")
5. В другом окне веб-браузера войдите на сайт Replicon своей компании в качестве администратора.

6. tooconfigure SAML 2.0, выполните следующие шаги hello.
   
    ![Включение аутентификации SAML](./media/active-directory-saas-replicon-tutorial/IC777805.png "Включение аутентификации SAML")
  
  1. toodisplay hello **EnableSAML Authentication2** диалоговое окно, добавьте следующие tooyour URL-адрес после ключа вашей компании hello: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**  
    * Hello ниже показан hello схема hello полный URL-адреса:  
   **https://na2.replicon.com/\<ключ_вашей_орагнизации\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**
   2. Нажмите кнопку hello  **+**  tooexpand hello **v20Configuration** раздела.
   3. Нажмите кнопку hello  **+**  tooexpand hello **metaDataConfiguration** раздела.
   4. Нажмите кнопку **выбрать файл**, tooselect XML-файл метаданных поставщика удостоверений и нажмите кнопку **отправить**.

7. На hello классический портал Azure, выберите Подтверждение настройки единого входа hello и нажмите кнопку **завершить** tooclose hello **Настройка единого входа** диалогового окна.
   
    ![Настройка единого входа](./media/active-directory-saas-replicon-tutorial/IC778418.png "Настройка единого входа")
   
## <a name="configure-user-provisioning"></a>Настроить подготовку учетных записей пользователей

В порядке tooenable toolog пользователей Azure AD в Replicon их необходимо подготовить в Replicon.  

В случае Replicon hello Подготовка выполняется вручную.

**tooconfigure подготовки пользователей, выполните следующие шаги hello.**

1. В окне веб-браузера войдите на сайт Replicon своей компании в качестве администратора.
2. Go слишком**администрирования \> пользователей**.
   
    ![Пользователи](./media/active-directory-saas-replicon-tutorial/IC777806.png "Пользователи")
3. Нажмите кнопку **+ Добавить пользователя**.
   
    ![Добавление пользователя](./media/active-directory-saas-replicon-tutorial/IC777807.png "Добавление пользователя")
4. В hello **профиля пользователя** выполните следующие шаги hello:
   
    ![Профиль пользователя](./media/active-directory-saas-replicon-tutorial/IC777808.png "Профиль пользователя")
   
  1. В hello **имя входа** текстового поля, типа hello Azure AD адрес электронной почты пользователя hello Azure AD будет tooprovision.
  2. Для параметра **Authentication Type** (Тип аутентификации) выберите значение **SSO** (Единый вход).
  3. В hello **отдел** текстовом поле введите отдел пользователя hello.
  4. Для параметра **Employee Type** (Тип сотрудника) выберите значение **Administrator** (Администратор).
  5. Нажмите кнопку **Сохранить профиль пользователя**.

>[!NOTE]
>Можно использовать любые другие Replicon пользователя средства создания учетных записей или интерфейсы API, предоставляемые Replicon tooprovision учетных записей пользователей AAD.
> 
> 

## <a name="assign-users"></a>Назначить пользователей
tootest конфигурацию, необходимо toogrant hello Azure AD пользователей с помощью tooit доступ вашего приложения путем назначения им tooallow.

**tooReplicon tooassign пользователей, выполните следующие шаги hello:**

1. В hello классический портал Azure создайте тестовую учетную запись.

2. На hello **Replicon** странице интеграции приложения щелкните **назначить пользователей**.
   
    ![Назначение пользователей](./media/active-directory-saas-replicon-tutorial/IC777809.png "Назначение пользователей")

3. Выберите тестового пользователя, нажмите кнопку **назначить**, а затем нажмите кнопку **Да** tooconfirm назначения.
   
    ![Да](./media/active-directory-saas-replicon-tutorial/IC767830.png "Да")

Tootest параметры единого входа, откройте панель доступа hello. Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

