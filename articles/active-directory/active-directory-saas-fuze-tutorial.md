---
title: "Руководство по интеграции Azure Active Directory с Fuze | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Fuze."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9780b4bf-1fd1-48c1-9ceb-f750225ae08a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: d0ea8c6456824e348301ed8bf1f5e00f4bfa8121
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fuze"></a>Руководство по интеграции Azure Active Directory с Fuze

В этом учебнике вы узнаете, как toointegrate Fuze с Azure Active Directory (Azure AD).

Интеграция с Azure AD Fuze предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooFuze
- Можно включить на пользователей tooautomatically get вошедшего tooFuze (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал управления Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Fuze требуется hello следующих элементов:

- подписка Azure AD;
- подписка Fuze с поддержкой единого входа.


> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.


tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не следует использовать рабочую среду при отсутствии необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Fuze из галереи hello
2. Настройка и проверка единого входа в Azure AD


## <a name="adding-fuze-from-hello-gallery"></a>Добавление Fuze из галереи hello
tooconfigure hello интеграции Fuze в Azure AD, вы должны tooadd Fuze из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Fuze из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портала управления Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".

    ![Приложения][3]

4. Введите в поле поиска hello **Fuze**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_000.png)

5. В панели результатов hello выберите **Fuze**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в приложение Fuze с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Fuze является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Fuze должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Fuze.

tooconfigure и теста Azure AD единого входа с Fuze, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Fuze](#creating-a-fuze-test-user)**  -toohave аналог Саймон Britta в Fuze, представление связанных toohello Azure AD ей.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал управления Azure hello и настройки единого входа в приложении Fuze.

**tooconfigure Azure AD единого входа с Fuze, выполните следующие шаги hello.**

1. На портале управления Azure hello на hello **Fuze** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна, как **режим** выберите **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_01.png)

3. На hello **URL-адреса и домена Fuze** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_020.png)
    
    В hello **URL-адрес входа** текстовом поле введите URL-адрес hello вход как:`https://www.thinkingphones.com/jetspeed/portal/`

4.  Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-fuze-tutorial/tutorial_general_400.png)

5. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.

    ![Настройка единого входа](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_05.png) 

6. tooconfigure единого входа на **Fuze** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[Fuze поддержки](https://www.fuze.com/support). Они будут устанавливается в порядке toohave hello правильно настроенной на обеих сторонах соединения единого входа SAML.


### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя на портале управления Azure hello, вызывается Саймон Britta.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал управления Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-fuze-tutorial/create_aaduser_01.png) 

2. Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-fuze-tutorial/create_aaduser_02.png) 

3. Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-fuze-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-fuze-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**. 


### <a name="creating-a-fuze-test-user"></a>Создание тестового пользователя Fuze

Приложение Fuze поддерживает JIT-подготовку пользователей, поэтому при входе пользователи будут создаваться автоматически. Для получения дополнительных пояснений, обратитесь в [службу поддержки](https://www.fuze.com/support) Fuze.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления ее tooFuze доступа.

![Назначение пользователя][200] 

**tooassign tooFuze Britta Simon выполните следующие шаги hello.**

1. На портале управления Azure hello, открыть представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Fuze**.

    ![Настройка единого входа](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_50.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    

### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello Fuze плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Fuze приложения.


## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_203.png