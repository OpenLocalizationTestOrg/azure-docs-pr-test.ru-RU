---
title: "Руководство по интеграции Azure Active Directory с TOPdesk — Secure | Документация Майкрософт"
description: "Узнайте, как toouse TOPdesk - Secure с Azure Active Directory tooenable единого входа, автоматизированной подготовки и многое другое!."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 8e149d2d-7849-48ec-9993-31f4ade5fdb4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 10fe420d1691c2845b89c779486ffd6fcd736432
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---secure"></a>Учебник. Интеграция Azure Active Directory с TOPdesk — Secure
Цель этого учебника Hello tooshow hello интеграцию Azure и TOPdesk - Secure.  
Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:

* Действующая подписка на Azure
* Подписка TOPdesk — Secure с поддержкой единого входа.

Изучив этот учебник, пользователи Azure AD hello назначенные tooTOPdesk - безопасный будет быть может toosingle входа в приложение hello в версию TOPdesk - сайте компании безопасной (инициированный поставщиком вход службы) или с помощью hello [введение Панель доступа toohello](active-directory-saas-access-panel-introduction.md).

Hello сценарий, описанный в этом руководстве состоит из hello следующие стандартные блоки.

1. Включение интеграции приложений hello для безопасной версии TOPdesk
2. Настройка единого входа
3. Настройка подготовки учетных записей пользователей
4. Назначение пользователей

![Сценарий](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Сценарий")

## <a name="enabling-hello-application-integration-for-topdesk---secure"></a>Включение интеграции приложений hello для безопасной версии TOPdesk
Hello цель этого раздела — toooutline как интеграции приложения hello tooenable для безопасной версии TOPdesk.

### <a name="tooenable-hello-application-integration-for-topdesk---secure-perform-hello-following-steps"></a>tooenable hello приложения интеграции для версии TOPdesk — безопасный, выполните следующие шаги hello.
1. В hello классический портал Azure, hello левой области навигации, выберите **Active Directory**.
   
    ![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")

2. Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.

3. Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.
   
    ![Приложения](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "Приложения")

4. Нажмите кнопку **добавить** hello нижней части страницы приветствия.
   
    ![Добавление приложения](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Добавление приложения")

5. На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.
   
    ![Добавление приложения из коллекции](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Добавление приложения из коллекции")

6. В hello **поле поиска**, тип **безопасной версии TOPdesk**.
   
    ![Коллекция приложений](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "Коллекция приложений")

7. В области результатов hello выберите **безопасной версии TOPdesk**и нажмите кнопку **завершить** tooadd приложения hello.
   
    ![TOPdesk — Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk — Secure")

## <a name="configuring-single-sign-on"></a>Настройка единого входа
Hello цель этого раздела — toooutline как tooTOPdesk tooauthenticate пользователей tooenable - защитить с помощью учетной записи в Azure AD, используя федерацию основании hello протокола SAML.  
Настройка единого входа для безопасной версии TOPdesk требуется tooupload файл значка логотипа. файл значка hello tooget, поддержки topdesk контактов hello.

### <a name="tooconfigure-single-sign-on-perform-hello-following-steps"></a>tooconfigure единого входа, выполните следующие шаги hello:
1. Войдите на tooyour **безопасной версии TOPdesk** сайт компании от имени администратора.
2. В hello **TOPdesk** меню, нажмите кнопку **параметры**.
   
    ![Параметры](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Параметры")

3. Щелкните **Параметры входа**.
   
    ![Параметры входа](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Параметры входа")

4. Разверните hello **параметры входа** меню, а затем нажмите **Общие**.
   
    ![Общие](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "Общие")

5. В hello **Secure** раздел hello **входа SAML** конфигурации выполните следующие шаги hello:
   
    ![Технические параметры](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "Технические параметры")
   
    а. Нажмите кнопку **загрузки** toodownload hello общедоступный файл метаданных, а затем сохраните его локально на компьютере.
   
    b. Откройте файл метаданных hello, а затем найдите hello **AssertionConsumerService** узла.
    
    ![Служба обработчика утверждений](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Служба обработчика утверждений")
   
    c. Копировать hello **AssertionConsumerService** значение.  
      
    > [!NOTE]
    > Будет необходимо hello значение в hello **настроить URL-адрес приложения** далее в этом учебнике.
    > 
    > 

6. В другом окне веб-браузера войдите на **классический портал Azure** в качестве администратора.

7. На hello **безопасной версии TOPdesk** странице интеграции приложения щелкните **настроить единый вход** tooopen hello ** Настройка единого входа ** диалогового окна.
   
    ![Настройка единого входа](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Настройка единого входа")

8. На hello **как как toosign пользователей на tooTOPdesk - Secure** выберите **Microsoft Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.
   
    ![Настройка единого входа](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Настройка единого входа")

9. На hello **настроить URL-адрес приложения** выполните следующие шаги hello:
   
    ![Настройка URL-адреса приложения](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "Настройка URL-адреса приложения")
   
    а. В hello **TOPdesk - Secure на URL-адрес входа** textbox hello введите URL-адрес, используемый вашей toosign пользователей в вашей безопасную версию TOPdesk (например: «*https://qssolutions.topdesk.net*»).
   
    b. В hello **TOPdesk — общедоступный URL-адрес ответа** текстовое поле, вставить hello **TOPdesk - Secure URL-адрес AssertionConsumerService** (например: «*https://qssolutions.topdesk.net/tas/public/login/saml*")
   
    c. Щелкните **Далее**.

10. На hello **настройки единого входа в безопасную версию TOPdesk** страницы, toodownload файл метаданных, нажмите кнопку **загрузить метаданные**, а затем сохраните файл hello на локальном компьютере.
    
    ![Настройка единого входа](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Настройка единого входа")

11. toocreate файлом сертификата, выполните следующие шаги hello.
    
    ![Сертификат](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "Сертификат")
    
    а. Откройте hello скачанный файл метаданных.
    b. Разверните hello **RoleDescriptor** узла, имеющего **xsi: Type** из **fed: ApplicationServiceType**.
    c. Скопируйте значение hello hello **X509Certificate** узла.
    d. Сохранить hello копируются **X509Certificate** значение на локальном компьютере в файле.

12. В версии TOPdesk - Secure корпоративный сайт в hello **TOPdesk** меню, нажмите кнопку **параметры**.
    
    ![Параметры](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Параметры")

13. Щелкните **Параметры входа**.
    
    ![Параметры входа](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Параметры входа")

14. Разверните hello **параметры входа** меню, а затем нажмите **Общие**.
    
    ![Общие](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "Общие")

15. В hello **открытый** щелкните **добавить**.
    
    ![Добавление](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Добавление")

16. На hello **помощник по настройке SAML** диалогового окна выполните следующие шаги hello:
    
    ![Помощник по настройке SAML](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "Помощник по настройке SAML")
    
    а. tooupload метаданные загруженного файла в разделе **метаданные федерации**, нажмите кнопку **Обзор**.

    b. файл сертификата, в разделе tooupload **сертификат (RSA)**, нажмите кнопку **Обзор**.

    c. Файл эмблемы hello tooupload, полученного от поддержки topdesk hello в разделе **значок логотипа**, нажмите кнопку **Обзор**.

    d. В hello **атрибут имени пользователя** введите **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.

    д. В hello **отображаемое имя** текстовом поле введите имя для конфигурации.

    f. Щелкните **Сохранить**.

17. На hello классический портал Azure, выберите Подтверждение настройки единого входа hello и нажмите кнопку **завершить** tooclose hello **Настройка единого входа** диалогового окна.
    
    ![Настройка единого входа](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Настройка единого входа")

## <a name="configuring-user-provisioning"></a>Настройка подготовки учетных записей пользователей
В порядке tooenable Azure AD пользователи toolog в версии TOPdesk - уровень безопасности, их необходимо подготовить в безопасной версии TOPdesk.  
В случае TOPdesk - hello безопасный, Подготовка выполняется вручную.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure подготовки пользователей, выполните следующие шаги hello.
1. Войдите на tooyour **безопасной версии TOPdesk** сайт компании от имени администратора.
2. В меню в верхней части hello hello выберите **TOPdesk \> New \> файлы поддержки \> оператор**.
   
    ![Оператор](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Оператор")

3. На hello **оператор New** диалоговое окно, выполните следующие шаги hello:
   
    ![Новый оператор](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "Новый оператор")
   
    а. Щелкните вкладку Общие hello.
   
    b. В hello **Фамилия** текстового поля из hello **Общие** раздел, имя последнего типа hello действительной учетной записи Azure Active Directory требуется tooprovision.
   
    c. Выберите **сайта** для учетной записи hello в hello **расположение** раздела.
   
    d. В hello **имя входа** текстового поля из hello **учетные данные TOPdesk** введите имя входа для пользователя.
   
    д. Щелкните **Сохранить**.

> [!NOTE]
> Можно использовать любые другие версии TOPdesk - учетная запись безопасности пользователя, инструменты для создания или API-интерфейсы, предоставляемые версией TOPdesk - Secure tooprovision учетных записей пользователей AAD.
> 
> 

## <a name="assigning-users"></a>Назначение пользователей
tootest конфигурацию, необходимо toogrant hello Azure AD пользователей с помощью tooit доступ вашего приложения путем назначения им tooallow.

### <a name="tooassign-users-tootopdesk---secure-perform-hello-following-steps"></a>tooTOPdesk пользователи tooassign - безопасной, выполните следующие шаги hello.
1. В hello классический портал Azure создайте тестовую учетную запись.
2. На hello ** безопасной версии TOPdesk ** странице интеграции приложения щелкните **назначить пользователей**.
   
    ![Назначение пользователей](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "Назначение пользователей")

3. Выберите тестового пользователя, нажмите кнопку **назначить**, а затем нажмите кнопку **Да** tooconfirm назначения.
   
    ![Да](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Да")

Tootest параметры единого входа, откройте панель доступа hello. Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

