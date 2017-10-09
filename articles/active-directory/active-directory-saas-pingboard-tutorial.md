---
title: "Руководство по интеграции Azure Active Directory с Pingboard | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Pingboard."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 0a916b1f9ef32d8124aa11284d2115bb4fc0bbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pingboard"></a>Руководство по интеграции Azure Active Directory с Pingboard

В этом учебнике вы узнаете, как toointegrate Pingboard с Azure Active Directory (Azure AD).

Интеграция с Azure AD Pingboard предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooPingboard
- Можно включить на пользователей tooautomatically get вошедшего tooPingboard (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал управления Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Pingboard требуется hello следующих элементов:

- подписка Azure AD;
- подписка Pingboard с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не следует использовать рабочую среду при отсутствии необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Pingboard из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-pingboard-from-hello-gallery"></a>Добавление Pingboard из галереи hello
tooconfigure hello интеграции Pingboard в Azure AD, вы должны tooadd Pingboard из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Pingboard из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портала управления Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".

    ![Приложения][3]

4. Введите в поле поиска hello **Pingboard**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_search.png)

5. В панели результатов hello выберите **Pingboard**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в приложение Pingboard с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Pingboard является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Pingboard должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Pingboard.

tooconfigure и теста Azure AD единого входа с Pingboard, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Pingboard](#creating-a-pingboard-test-user)**  -toohave аналог Саймон Britta в Pingboard, представление связанных toohello Azure AD ей.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал управления Azure hello и настройки единого входа в приложении Pingboard.

**tooconfigure Azure AD единого входа с Pingboard, выполните следующие шаги hello.**

1. На портале управления Azure hello на hello **Pingboard** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна, как **режим** выберите **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_samlbase.png)

3. На hello **Pingboard доменов и URL-адреса** выполните hello, выполните действия, при желании tooconfigure приложения hello в **IDP** инициировал режим:

    ![Настройка единого входа](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_url.png)

    а. В hello **идентификатор** текстовое поле, значение типа hello как:`http://<entity-id>.pingboard.com/sp`

    b. В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<entity-id>.pingboard.com/auth/saml/consume`

    > [!NOTE] 
    > Обратите внимание на то, что они не hello реальные значения. У вас tooupdate эти значения с hello фактический идентификатор и ответ URL-адрес. Здесь мы предлагаем вам toouse hello уникальное значение строки в hello идентификатор. Обратитесь к [группа поддержки клиента Pingboard](https://support.pingboard.com/) tooget эти значения. 

4. Проверьте **Показывать дополнительные параметры URL-адреса**, если нужно, чтобы приложение hello tooconfigure в **SP** инициировал режим:

    ![Настройка единого входа](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_sp_initiated01.png)

    а. В hello **URL-адрес входа** текстовое поле, значение типа hello как:`http://<sub-domain>.pingboard.com/sign_in`
     
5. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.

    ![Настройка единого входа](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_certificate.png) 

6. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-pingboard-tutorial/tutorial_general_400.png)

7. tooconfigure единого входа на стороне Pingboard, откройте новое окно браузера и войдите в tooyour Pingboard учетной записи. Tooset администратора Pingboard копирование единый вход должен быть на.

8. Hello верхней строке меню выберите **приложений > интеграции**

    ![Настройка единого входа](./media/active-directory-saas-pingboard-tutorial/Pingboard_integration.png)

9.  На hello **интеграции** найдите hello **«Azure Active Directory»** плитки и щелкните его.

    ![Настройка единого входа](./media/active-directory-saas-pingboard-tutorial/Pingboard_aad.png)

10. В hello модальное далее щелкните **«Настройка»**

    ![Настройка единого входа](./media/active-directory-saas-pingboard-tutorial/Pingboard_configure.png)

11. На странице hello можно заметить «интеграция единого входа Azure включения.». Откройте hello загружен файл метаданных XML в Блокнот и вставьте hello, содержимого в **метаданные поставщика Удостоверений**.

    ![Настройка единого входа](./media/active-directory-saas-pingboard-tutorial/Pingboard_sso_configure.png)

12. файл Hello будет проверяться, и если все работает правильно, будет включен единый вход

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя на портале управления Azure hello, вызывается Саймон Britta.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал управления Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_01.png) 

2. Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_02.png) 

3. Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-pingboard-test-user"></a>Создание тестового пользователя Pingboard

В порядке tooenable toolog пользователей Azure AD в Pingboard их необходимо подготовить в Pingboard.  
В случае Pingboard hello Подготовка выполняется вручную.

**tooprovision учетных записей пользователей, выполните следующие действия hello:**

1. Войдите в систему tooyour Pingboard сайт компании как администратор.

2. Нажмите кнопку **Add Employee** (Добавить сотрудника) на странице **Directory** (Каталог).

    ![Добавление сотрудника](./media/active-directory-saas-pingboard-tutorial/create_testuser_add.png)

3. На hello **«Добавить сотрудника»** диалогового окна выполните следующие шаги hello.

    ![Приглашение пользователей](./media/active-directory-saas-pingboard-tutorial/create_testuser_name.png)

    а. В hello **полное имя** textbox hello полное имя типа Саймон Britta.

    b. В hello **электронной почты** текстовом поле введите адрес электронной почты hello Саймон Britta учетной записи.

    c. В hello **должность** текстового поля, типа hello должности Саймон Britta.

    d. В hello **расположение** раскрывающийся список, выберите hello расположение Саймон Britta.
    
    д. Щелкните **Добавить**.   

4. Экран подтверждения запустится tooconfirm hello Добавление пользователя.
    
    ![Подтверждение](./media/active-directory-saas-pingboard-tutorial/create_testuser_confirm.png)
        
    > [!NOTE]
    > Hello владельцем учетной записи Azure Active Directory получит сообщение электронной почты и выполните их учетных записей tooconfirm ссылку, чтобы она стала активной.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления ее tooPingboard доступа.

![Назначение пользователя][200] 

**tooassign tooPingboard Britta Simon выполните следующие шаги hello.**

1. На портале управления Azure hello, открыть представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Pingboard**.

    ![Настройка единого входа](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello Pingboard плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Pingboard приложения.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_203.png
