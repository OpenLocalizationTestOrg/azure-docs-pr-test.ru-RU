---
title: "Руководство по интеграции Azure Active Directory с Optimizely | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Optimizely."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28ef03e1-9aad-4301-af97-d94e853edc74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 868aefae27ca155d2963f3dcfcd79bbb564b48ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-optimizely"></a>Учебник. Интеграция Azure Active Directory с Optimizely

В этом учебнике вы узнаете, как toointegrate Optimizely с Azure Active Directory (Azure AD).

Интеграция с Azure AD Optimizely предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooOptimizely
- Можно включить на пользователей tooautomatically get вошедшего tooOptimizely (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Optimizely требуется hello следующих элементов:

- подписка Azure AD;
- подписка Optimizely с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Optimizely из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-optimizely-from-hello-gallery"></a>Добавление Optimizely из галереи hello
tooconfigure hello интеграции Optimizely в Azure AD, вы должны tooadd Optimizely из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Optimizely из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Optimizely**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_search.png)

5. В панели результатов hello выберите **Optimizely**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Optimizely с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Optimizely является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Optimizely должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Optimizely.

tooconfigure и теста Azure AD единого входа с Optimizely, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя, прошедшего Optimizely](#creating-an-optimizely-test-user)**  -toohave аналог Саймон Britta в Optimizely, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Optimizely.

**tooconfigure Azure AD единого входа с Optimizely, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Optimizely** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_samlbase.png)

3. На hello **URL-адреса и домена Optimizely** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://app.optimizely.net/<instance name>`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`urn:auth0:optimizely:contoso`

    > [!NOTE] 
    > Эти значения не являются реальными hello. Значение hello будут обновлены hello фактический URL-адрес входа и идентификатор, который описан далее в учебнике hello. 

4. На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-optimizely-tutorial/tutorial_general_400.png)

6. На hello **конфигурации Optimizely** щелкните **Настройка Optimizely** tooopen **Настройка входа** окна. Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_configure.png) 

7. tooconfigure единого входа на **Optimizely** стороны, обратитесь к менеджеру по продажам Optimizely и обеспечения загружаются hello **сертификата (Base64)**, и **SAML единого входа URL-адрес службы** . 

8. В сообщении электронной почты tooyour ответ Optimizely предоставляет приветствия на URL-адрес входа (SSO, инициированные SP) и hello значения идентификатора (идентификатор сущности поставщика службы).

    а. Копировать hello **инициируемая SP URL-адрес единого входа** предоставляемого Optimizely и вставить в hello **на URL-адрес входа** текстовое поле в **URL-адреса и домена Optimizely** раздела на портале Azure 

    b. Копировать hello **идентификатор сущности поставщика службы** предоставляемого Optimizely и вставить в hello **идентификатор** текстовое поле в **URL-адреса и домена Optimizely** раздела на портале Azure 

9. В другом окне браузера, tooyour входа Optimizely приложения.

10. Нажмите кнопку, можно ввести имя учетной записи в предложении top hello правом углу и затем **параметры учетной записи**.
   
    ![Единый вход в Azure AD](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_09.png)

11. Во вкладке "учетная запись" hello, установите флажок "hello" **Включить единый вход** в области единого входа в hello **Обзор** раздела.
   
    ![Единый вход в Azure AD](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_10.png)
    
12. Нажмите кнопку **Сохранить**

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из Саймон Britta.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-an-optimizely-test-user"></a>Создание тестового пользователя Optimizely

В этом разделе описано, как создать пользователя Britta Simon в приложении Optimizely.

1. На домашней странице приветствия установите **участники совместной работы** вкладки.

2. tooadd новый проект toohello участника совместной работы, нажмите кнопку **нового участника совместной работы**.
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_10.png)

3. Введите адрес электронной почты hello и назначить ему роль. Нажмите кнопку **Пригласить**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_11.png)

4. Он получит приглашение по электронной почте. С помощью адреса электронной почты hello, они имеют toolog tooOptimizely.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooOptimizely доступа.

![Назначение пользователя][200] 

**tooassign tooOptimizely Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Optimizely**.

    ![Настройка единого входа](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello Optimizely плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Optimizely приложения. 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_203.png

