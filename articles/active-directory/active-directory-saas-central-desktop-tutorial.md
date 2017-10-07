---
title: "Руководство. Интеграция Azure Active Directory с Central Desktop | Документация Майкрософт"
description: "Узнайте, как toouse Central Desktop с Azure Active Directory tooenable единого входа, автоматизированной подготовки и многое другое!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: b805d485-93db-49b4-807a-18d446c7090e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 93036ae801c446ce476288c00579931ba10a843b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-central-desktop"></a>Учебник. Интеграция Azure Active Directory с Central Desktop
Цель этого учебника Hello — tooshow hello интеграцию Azure и Central Desktop. Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:

* Действующая подписка на Azure
* Подписка с поддержкой единого входа в Central Desktop/клиент Central Desktop

Hello сценарий, описанный в этом руководстве состоит из hello следующие стандартные блоки.

* Включение интеграции приложений hello для Central Desktop
* Настройка единого входа.
* Настройка подготовки учетных записей пользователей
* Назначение пользователей

![Сценарий](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "Сценарий")

## <a name="enable-hello-application-integration-for-central-desktop"></a>Включить hello интеграции приложений для Central Desktop
Hello цель этого раздела — toooutline как интеграции приложения hello tooenable для Central Desktop.

**Интеграция приложения hello tooenable для Central Desktop выполните hello следующие шаги.**

1. В hello классический портал Azure, hello левой области навигации, выберите **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")
2. Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.
3. Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.
   
   ![Приложения](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "Приложения")
4. Нажмите кнопку **добавить** hello нижней части страницы приветствия.
   
   ![Добавление приложения](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "Добавление приложения")
5. На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.
   
   ![Добавление приложения из коллекции](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "Добавление приложения из коллекции")
6. В hello **поле поиска**, тип **Central Desktop**.
   
   ![Коллекция приложений](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "Коллекция приложений")
7. В области результатов hello выберите **Central Desktop**и нажмите кнопку **завершить** tooadd приложения hello.
   
   ![Central Desktop](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")
   
## <a name="configure-single-sign-on"></a>Настройка единого входа

Цель этого раздела Hello — toooutline, каким образом пользователи tooenable tooauthenticate tooCentral рабочего стола с помощью учетной записи в Azure AD, используя федерацию на основе hello SAML протокола.

В рамках этой процедуры, необходимые tooupload клиента tooyour Central Desktop сертификат в кодировке base-64.  
Если вы не знакомы с этой процедурой, см. раздел [как tooconvert двоичные данные сертификата в текстовый файл](http://youtu.be/PlgrzUZ-Y1o).

**tooconfigure единого входа, выполните следующие шаги hello:**

1. В классический портал Azure, на hello hello **Central Desktop** странице интеграции приложения щелкните **настроить единый вход** tooopen hello ** Настройка единого входа ** диалогового окна.
   
   ![Настройка единого входа](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "Настройка единого входа")
2. На hello **предпочитаемый как toosign пользователей на tooCentral рабочего стола** выберите **Microsoft Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.
   
   ![Настройка единого входа](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "Настройка единого входа")
3. На hello **настроить URL-адрес приложения** страницы, выполните следующие шаги hello и нажмите кнопку **Далее**: 
   
   1. В hello **рабочий стол входа в URL-адрес центра** в текстовое поле введите hello URL-адрес клиента Central Desktop (например: *http://contoso.centraldesktop.com*).
   2. Hello URL-адрес ответа центра рабочего стола введите текстовое поле URL-адрес центра Desktop AssertionConsumerService (например: https://contoso.centraldesktop.com/saml2-assertion.php).
   
   >[!NOTE]
   >Hello значение можно получить из метаданных central desktop hello (например: *http://contoso.centraldesktop.com*).
   >  
   
   ![Настройка URL-адреса приложения](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "Настройка URL-адреса приложения")
4. На hello **настроить единый вход в Central Desktop** страницы, toodownload свой сертификат, нажмите кнопку **загрузки сертификата**, а затем сохраните файл сертификата hello на компьютере.
   
  ![Настройка единого входа](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "Настройка единого входа")
5. Войдите в tooyour **Central Desktop** клиента.
6. Go слишком**параметры**, нажмите кнопку **Дополнительно**, а затем нажмите кнопку **единого входа**.
   
  ![Настройка — Дополнительно](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Настройка — Дополнительно")
7. На hello **настройки единого входа** выполните следующие шаги hello:
   
  ![Параметры единого входа](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Параметры единого входа")
   
  1. Установите флажок **Разрешить единый вход SAML версии 2**.
  2. В классический портал Azure, на hello hello **настроить единый вход в Central Desktop** страницы, копировать hello **URL-адрес издателя** значение, а затем вставьте его в hello **URL-адрес SSO** текстового поля.
  3. В классический портал Azure, на hello hello **настроить единый вход в Central Desktop** страницы, копировать hello **URL-адрес удаленного входа** значение, а затем вставьте его в hello **URL-адрес входа SSO**текстового поля.
  4. В классический портал Azure, на hello hello **настроить единый вход в Central Desktop** страницы, копировать hello **URL-адрес службы единого выхода** значение, а затем вставьте его в hello **URL-адрес выхода SSO** текстового поля.
8. В hello **метод проверки подписи сообщения** выполните следующие шаги hello:
   
   ![Метод проверки подписей в сообщениях](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "Метод проверки подписей в сообщениях")
   
  1. Выберите **Сертификат**.
  2. Из hello **сертификат SSO** выберите **RSH SHA256**.
  3. Создайте текстовый файл из сертификата загружен hello, hello копирования содержимого hello текстового файла, а затем вставьте его в hello **сертификат SSO** поля.  
     >[!TIP]
     >Дополнительные сведения см. в разделе [как tooconvert двоичные данные сертификата в текстовый файл](http://youtu.be/PlgrzUZ-Y1o)
      >  
   4. Выберите **отображать страницу входа tooyour SAMLv2 ссылку**.
9. Нажмите кнопку **Обновить**.
10. На hello классический портал Azure, выберите Подтверждение настройки единого входа hello и нажмите кнопку **завершить** tooclose hello **Настройка единого входа** диалогового окна.
    
    ![Настройка единого входа](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "Настройка единого входа")
    
## <a name="configure-user-provisioning"></a>Настроить подготовку учетных записей пользователей

Для AAD пользователей toobe может toosign в они должны быть подготовленных toohello приложении Central Desktop. В этом разделе описывается, как учетные записи пользователей toocreate AAD в Central Desktop.

**tooCentral учетных записей пользователя tooprovision рабочего стола:**
1. Войдите в систему tooyour клиента Central Desktop.
2. Go слишком**людей \> внутренние члены**.
3. Нажмите кнопку **Добавить внутренних участников**.
   
  ![Люди](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "Люди")
4. В hello **электронной почты адрес новых членов** текстовом поле введите учетную запись AAD tooprovision и нажмите кнопку **Далее**.
   
  ![Адреса электронной почты новых участников](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "Адреса электронной почты новых участников")
5. Нажмите кнопку **Добавить внутренних участников**.
   
  ![Добавление внутренних участников](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "Добавление внутренних участников")
   
   >[!NOTE]
   >Hello пользователей, которые были добавлены получит сообщение электронной почты, включающий ссылку для подтверждения они необходима учетная запись hello tooactivate tooclick.
   > 

>[!NOTE]
>Можно использовать любые другие Central Desktop пользователя средства создания учетных записей или интерфейсы API, предоставляемые Central Desktop tooprovision учетных записей пользователей AAD
>  

## <a name="assign-users"></a>Назначить пользователей
tootest конфигурацию, необходимо toogrant hello Azure AD пользователей с помощью tooit доступ вашего приложения путем назначения им tooallow.

**Пользователи tooassign tooCentral рабочего стола, выполните hello следующие шаги.**

1. В hello классический портал Azure создайте тестовую учетную запись.
2. На hello **Central Desktop** странице интеграции приложения щелкните **назначить пользователей**.
   
   ![Назначение пользователей](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "Назначение пользователей")
3. Выберите тестового пользователя, нажмите кнопку **назначить**, а затем нажмите кнопку **Да** tooconfirm назначения.
   
   ![Да](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Да")

Tootest параметры единого входа, откройте панель доступа hello. Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

