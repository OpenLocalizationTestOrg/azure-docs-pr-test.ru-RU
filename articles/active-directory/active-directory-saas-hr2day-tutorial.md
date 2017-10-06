---
title: "Учебник. Интеграция Azure Active Directory с HR2day by Merces | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и HR2day по Merces."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 853d08c9-27b1-48d4-b8e7-3705140eb67f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: 257233767e1fddbaf115878cb0455acf61b2f5f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hr2day-by-merces"></a>Руководство. Интеграция Azure Active Directory с HR2day от Merces

В этом учебнике вы узнаете, как toointegrate HR2day по Merces с Azure Active Directory (Azure AD).

Интеграция с Azure AD HR2day по Merces предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooHR2day по Merces.
- Можно включить пользователей tooautomatically получить подписан в tooHR2day Merces с их учетными записями Azure AD.
- Вы можете управлять учетными записями в одном централизованном месте--hello портал Azure.

Дополнительные сведения об интеграции приложений SaaS с Azure AD см. в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с HR2day по Merces требуется hello следующих элементов:

- подписка Azure AD;
- подписка HR2day от Merces с поддержкой единого входа.

> [!NOTE]
> Не рекомендуется с помощью рабочей среды tootest hello шаги в этом учебнике.

tootest hello шаги в этом учебнике, придерживайтесь следующих рекомендаций:

- Не используйте рабочую среду без необходимости.
- Получите [бесплатную пробную версию Azure AD на 1 месяц](https://azure.microsoft.com/pricing/free-trial/), если у вас еще ее нет.  

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. сценарий Hello, описанные здесь состоит из двух основных компонентов.

1. Добавление HR2day по Merces из галереи hello.
2. Настройка и проверка единого входа Azure AD.

## <a name="add-hr2day-by-merces-from-hello-gallery"></a>Добавление HR2day по Merces из коллекции hello
tooconfigure интеграция HR2day по Merces hello в Azure AD, добавить HR2day по Merces из hello коллекции tooyour список управляемых приложений SaaS.

**tooadd HR2day по Merces из галереи hello, hello выполните следующие шаги:**

1. В hello [портал Azure](https://portal.azure.com), на левой панели навигации hello, выберите hello **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Go слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd нового приложения, выберите hello **новое приложение** кнопку в верхней части hello диалогового окна «hello».

    ![Приложения][3]

4. Введите в поле поиска hello **HR2day по Merces**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_search.png)

5. Hello панели результатов выберите **HR2day по Merces**, а затем выберите hello **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в HR2day от Merces с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow кто hello пользователем аналога в HR2day по Merces tooa пользователя в Azure AD. Другими словами необходимо tooestablish связь между пользователя Azure AD и связанных пользователей hello в HR2day по Merces.

Присвойте hello в HR2day по Merces **имя пользователя** в Azure AD слишком **имя пользователя** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с HR2day по Merces, требуются следующие стандартные блоки hello toocomplete:

1. [Настройка Azure AD единого входа](#configuring-azure-ad-single-sign-on): включить эту функцию на toouse пользователей.
2. [Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user) требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.
3. [Создание HR2day пользователем теста Merces](#creating-an-hr2day-by-merces-test-user): создание аналог Саймон Britta в HR2day по Merces, представление связанных toohello Azure AD пользователя.
4. [Назначить hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user): Включение Саймон Britta toouse Azure AD единого входа.
5. [Тестирование единого входа](#testing-single-sign-on): Проверьте, работает ли конфигурация hello.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в вашей HR2day Merces приложением.

**tooconfigure Azure AD единого входа с HR2day по Merces, выполните следующие шаги hello.**

1. В hello в hello портала Azure **HR2day по Merces** странице интеграции приложений выберите **единого входа**.

    ![Настройка единого входа][4]

2. tooenable единого входа, в hello **единого входа** выберите **режим** как **входа на базе SAML**.
 
    ![Настройка единого входа](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_samlbase.png)

3. В hello **HR2day Merces доменом и URL-адреса** примите hello следующие шаги:

    ![Настройка единого входа](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_url.png)

    а. В hello **URL-адрес входа** введите URL-адрес, используя следующий шаблон hello: `https://<tenantname>.force.com/<instancename>`.

    b. В hello **идентификатор** введите URL-адрес, используя следующий шаблон hello: `https://hr2day.force.com/<companyname>`.

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновите эти значения с hello фактический URL-адрес входа и идентификатором. Обратитесь в службу hello [HR2day группой поддержки клиента Merces](mailto:servicedesk@merces.nl) tooget эти значения. 
 


4. На hello **сертификат подписи SAML** выберите **Certificate(Base64)**, а затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_certificate.png) 

5. В этом разделе описываются как tooHR2day tooauthenticate tooenable пользователей по Merces с учетной записью в Azure AD. Они это сделать с помощью федерации на основании hello протокола SAML.

    Ваш HR2day приложением Merces ожидает утверждения SAML hello в определенном формате, требующей маркера SAML tooyour сопоставления настраиваемого атрибута tooadd. Следующий снимок экрана приветствия показан пример этого. 

    ![Настройка единого входа](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_00.png)
    
    > [!NOTE] 
    Перед настройкой hello утверждения SAML, необходимо обратиться к hello [HR2day группой поддержки клиента Merces](mailto:servicedesk@merces.nl) и запросить значение hello hello уникальный идентификатор атрибута для вашего клиента. Необходимо, чтобы это значение toocomplete hello действия, описанные в следующем разделе hello. 

6. В hello **единого входа** диалогового окна hello **атрибуты пользователя** статьи, настройте атрибутов токена SAML hello, как показано в hello после изображения. Затем выполните следующие шаги hello.
    
      | Имя атрибута    |   Значение атрибута |  
    | ------------------- | -------------------- |    
    | ATTR_LOGINCLAIM | join([mail],"102938475Z","@" |
    
      а. tooopen hello **Добавление атрибута** диалогового окна выберите **добавить атрибут**.

    ![Настройка единого входа](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_04.png)

    ![Настройка единого входа](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_05.png)

    b. В hello **имя** введите **ATTR_LOGINCLAIM**.

    c. Из hello **значение** выберите **Join()**.

    d. Из hello **String1** выберите **user.mail**.

    д. Для **String2**, введите уникальный идентификатор hello, предоставляемая HR2day команды.

    f. В hello **разделителя** введите  **@** .
    
    ж. Нажмите кнопку **ОК**.

7. Выберите hello **Сохранить** кнопки.

    ![Настройка единого входа](./media/active-directory-saas-hr2day-tutorial/tutorial_general_400.png)

8. В hello **HR2day конфигурацией Merces** выберите **Настройка HR2day по Merces** tooopen hello **Настройка входа** окна. Копировать hello **URL-адрес выхода**, **идентификатор сущности SAML**, и **SAML единого входа URL-адрес службы** из hello **краткий справочник** раздела.

    ![Настройка единого входа](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_configure.png) 

9. tooconfigure единого входа для вашего приложения, обратитесь в службу hello [HR2day группой поддержки клиента Merces](mailTo:servicedesk@merces.nl). Присоединение загружаются hello **Certificate(Base64)** файл tooyour электронной почты. Также предоставляют hello **URL-адрес выхода**, **идентификатор сущности SAML**, и **SAML единого входа URL-адрес службы** , чтобы они могут быть настроены для интеграции единого входа.

    > [!NOTE]
    >Назовите toohello Merces команды, которые требуется такая интеграция hello набор с шаблоном hello toobe идентификатор сущности **https://hr2day.force.com/INSTANCENAME**.

    > [!TIP]
    >Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения с hello **Active Directory** > **корпоративных приложений** раздел, выберите hello **Single Sign-On** вкладки. Hello доступа внедряются документации с помощью hello **конфигурации** раздела внизу hello. Вы можете прочитать больше о документации embedded hello в hello [Azure AD внедренных документации]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, hello выполните следующие шаги:**

1. В hello **портал Azure**, на левой панели навигации hello, выберите hello **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп**и выберите **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** выберите **добавить** в верхней части hello диалогового окна «hello».
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_03.png) 

4. В hello **пользователя** диалоговом hello выполните следующие шаги:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** поле, тип hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль**и запишите пароль hello.

    d. Нажмите кнопку **Создать**.
 
### <a name="create-an-hr2day-by-merces-test-user"></a>Создание тестового пользователя HR2day от Merces

Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в HR2day по Merces. Пользователи tooadd hello в учетной записи hello HR2day, работать с hello [HR2day группой поддержки клиента Merces](mailto:servicedesk@merces.nl). 

> [!NOTE]
> Если вам требуется toocreate пользователя вручную, обратитесь в службу hello [HR2day группой поддержки клиента Merces](mailto:servicedesk@merces.nl).

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления ее tooHR2day доступ по Merces.

![Назначение пользователя][200] 

**tooassign tooHR2day Britta Simon по Merces hello выполните следующие шаги:**

1. В hello Azure приложений портала, откройте hello просмотра, перейдите в представление каталога toohello, а затем перейдите слишком**корпоративных приложений**. Затем выберите **Все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **HR2day по Merces**.

    ![Настройка единого входа](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_app.png) 

3. Выберите в меню hello слева hello, **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Выберите hello **добавить** кнопки. Затем в hello **добавить назначение** выберите **пользователей и групп**.

    ![Назначение пользователя][203]

5. В hello **пользователей и групп** диалогового окна hello **пользователей** выберите **Britta Simon**.

6. Нажмите кнопку hello **выберите** кнопки.

7. В hello **добавить назначение** выберите **назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

Hello цель этого раздела — tootest конфигурации Azure AD единого входа с помощью hello панели доступа.  

При выборе hello HR2day путем Merces плитки в панели доступа hello вы автоматически получите вход в tooyour HR2day Merces приложением.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников о том, как tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_203.png

