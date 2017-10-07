---
title: "Учебник. Интеграция Azure Active Directory с Coupa | Документация Майкрософт"
description: "Узнайте, как toouse Coupa с Azure Active Directory tooenable единого входа, автоматизированной подготовки и многое другое!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 47f27746-9057-4b9c-991e-3abf77710f73
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 87e98573718d27d408c886466a374a987f58faa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-coupa"></a>Руководство. Интеграция Azure Active Directory с Coupa
Цель этого учебника Hello — tooshow hello интеграцию Azure и Coupa.  
Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:

* Действующая подписка на Azure
* Подписка Coupa с поддержкой единого входа

После завершения этого учебника, пользователи hello Azure AD, назначенные tooCoupa будут может toosingle входа в приложение hello hello [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

Hello сценарий, описанный в этом руководстве состоит из hello следующие стандартные блоки.

* Включение hello интеграции приложений для Coupa
* Настройка единого входа
* Настройка подготовки учетных записей пользователей
* Назначение пользователей

![Сценарий](./media/active-directory-saas-coupa-tutorial/IC791897.png "Сценарий")

## <a name="enable-hello-application-integration-for-coupa"></a>Включить hello интеграции приложений для Coupa
Hello цель этого раздела — toooutline как интеграции приложения hello tooenable для Coupa.

**интеграции приложения hello tooenable для Coupa, выполните следующие шаги hello.**

1. В hello классический портал Azure, hello левой области навигации, выберите **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")
2. Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.
3. Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.
   
   ![Приложения](./media/active-directory-saas-coupa-tutorial/IC700994.png "Приложения")
4. Нажмите кнопку **добавить** hello нижней части страницы приветствия.
   
   ![Добавление приложения](./media/active-directory-saas-coupa-tutorial/IC749321.png "Добавление приложения")
5. На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.
   
   ![Добавление приложения из коллекции](./media/active-directory-saas-coupa-tutorial/IC749322.png "Добавление приложения из коллекции")
6. В hello **поле поиска**, тип **Coupa**.
   
   ![Коллекция приложений](./media/active-directory-saas-coupa-tutorial/IC791898.png "Коллекция приложений")
7. В области результатов hello выберите **Coupa**и нажмите кнопку **завершить** tooadd приложения hello.
   
   ![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")
   
## <a name="configure-single-sign-on"></a>Настройка единого входа

Цель этого раздела Hello — toooutline как tooCoupa tooauthenticate tooenable пользователей с учетной записью в Azure AD, используя федерацию на основе hello SAML протокола.  

Настройка единого входа для Coupa требуется tooretrieve значение отпечатка из сертификата. Если вы не знакомы с этой процедурой, см. раздел [как tooretrieve значение отпечатка сертификата](http://youtu.be/YKQF266SAxI).

**tooconfigure единого входа, выполните следующие шаги hello:**

1. Войдите на tooyour сайт Coupa компании от имени администратора.
2. Go слишком**установки \> управления безопасностью**.
   
   ![Средства управления безопасностью](./media/active-directory-saas-coupa-tutorial/IC791900.png "Средства управления безопасностью")
3. toodownload hello Coupa метаданных файла tooyour компьютера, нажмите кнопку **загрузить и импортировать метаданные SP**.
   
   ![Метаданные Coupa SP](./media/active-directory-saas-coupa-tutorial/IC791901.png "Метаданные Coupa SP")
4. В другом окне браузера Войдите на классический портал Azure toohello.
5. На hello **Coupa** странице интеграции приложения щелкните **настроить единый вход** tooopen hello **Настройка единого входа** диалогового окна.
   
   ![Настройка единого входа](./media/active-directory-saas-coupa-tutorial/IC791902.png "Настройка единого входа")
6. На hello **предпочитаемый как toosign пользователей на tooCoupa** выберите **Microsoft Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.
   
   ![Настройка единого входа](./media/active-directory-saas-coupa-tutorial/IC791903.png "Настройка единого входа")
7. На hello **настроить URL-адрес приложения** выполните следующие шаги hello:
   
   ![Настройка URL-адреса приложения](./media/active-directory-saas-coupa-tutorial/IC791904.png "Настройка URL-адреса приложения")   
   1. В hello **на URL-адрес входа** текстовом поле введите URL-адрес, используемый вашей toosign пользователей на tooyour приложение Coupa (например: «*http://company.Coupa.com*»).
   2. Откройте скачанный файл метаданных Coupa и скопируйте hello **AssertionConsumerService index/URL**.
   3. В hello **URL-адрес ответа Coupa** текстовое поле, вставить hello **AssertionConsumerService index/URL** значение.
   4. Щелкните **Далее**.
8. На hello **настройки единого входа в Coupa** страницы, toodownload файл метаданных, нажмите кнопку **загрузить метаданные**, а затем сохраните файл hello на локальном компьютере.
   
   ![Настройка единого входа](./media/active-directory-saas-coupa-tutorial/IC791905.png "Настройка единого входа")
9. На сайте Coupa компании hello перейдите слишком**установки \> управления безопасностью**.
   
   ![Средства управления безопасностью](./media/active-directory-saas-coupa-tutorial/IC791900.png "Средства управления безопасностью")
10. В hello **вход с использованием учетных данных Coupa** выполните следующие шаги hello:  

   ![Вход с использованием учетных данных Coupa](./media/active-directory-saas-coupa-tutorial/IC791906.png "Вход с использованием учетных данных Coupa") 
   1. Выберите **Вход с помощью SAML**.
   2. Нажмите кнопку **Обзор** tooupload скачанный файл метаданных Azure Active.
   3. Щелкните **Сохранить**.
11. На hello классический портал Azure, выберите Подтверждение настройки единого входа hello и нажмите кнопку **завершить** tooclose hello **Настройка единого входа** диалогового окна.
    
   ![Настройка единого входа](./media/active-directory-saas-coupa-tutorial/IC791907.png "Настройка единого входа")
    
## <a name="configure-user-provisioning"></a>Настроить подготовку учетных записей пользователей

В порядке tooenable toolog пользователей Azure AD в Coupa их необходимо подготовить в Coupa.  

* В случае hello объекта Coupa Подготовка выполняется вручную.

**tooconfigure подготовки пользователей, выполните следующие шаги hello.**

1. Войдите в tooyour **Coupa** сайт компании от имени администратора.
2. В меню в верхней части hello hello выберите **установки**и нажмите кнопку **пользователей**.
   
   ![Пользователи](./media/active-directory-saas-coupa-tutorial/IC791908.png "Пользователи")
3. Щелкните **Создать**.
   
   ![Создание пользователей](./media/active-directory-saas-coupa-tutorial/IC791909.png "Создание пользователей")
4. В hello **создать пользователя** выполните следующие шаги hello:
   
   ![Сведения о пользователе](./media/active-directory-saas-coupa-tutorial/IC791910.png "Сведения о пользователе")
   
   1. Тип hello **входа**, **имя**, **Фамилия**, **идентификатор-**, **электронной почты** атрибуты допустимую учетную запись Azure Active Directory, требуется tooprovision в hello связанные текстовые поля.
   2. Щелкните **Создать**.   
   >[!NOTE]
   >Владелец учетной записи Hello Azure Active Directory получит сообщение электронной почты с учетной записью hello tooconfirm ссылку, чтобы она стала активной. 
   > 

>[!NOTE]
>Можно использовать любые другие Coupa пользователя средства создания учетных записей или интерфейсы API, предоставляемые Coupa tooprovision учетных записей пользователей AAD. 
> 

## <a name="assign-users"></a>Назначить пользователей
tootest конфигурацию, необходимо toogrant hello Azure AD пользователей с помощью tooit доступ вашего приложения путем назначения им tooallow.

**tooCoupa tooassign пользователей, выполните следующие шаги hello:**

1. В hello классический портал Azure создайте тестовую учетную запись.
2. На hello ** Coupa ** странице интеграции приложения щелкните **назначить пользователей**.
   
   ![Назначение пользователей](./media/active-directory-saas-coupa-tutorial/IC791911.png "Назначение пользователей")
3. Выберите тестового пользователя, нажмите кнопку **назначить**, а затем нажмите кнопку **Да** tooconfirm назначения.
   
   ![Да](./media/active-directory-saas-coupa-tutorial/IC767830.png "Да")

Tootest параметры единого входа, откройте панель доступа hello. Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

