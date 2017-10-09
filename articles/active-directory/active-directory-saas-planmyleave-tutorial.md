---
title: "Руководство. Интеграция Azure Active Directory с PlanMyLeave | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и PlanMyLeave."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b0d31cbe-7ae2-488b-9cf3-4927391fa744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: jeedes
ms.openlocfilehash: 44a6782e44ef22fc957544960be1742f9eed6e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-planmyleave"></a>Руководство. Интеграция Azure Active Directory с PlanMyLeave

В этом учебнике вы узнаете, как toointegrate PlanMyLeave с Azure Active Directory (Azure AD).

Интеграция с Azure AD PlanMyLeave предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooPlanMyLeave
- Можно включить на пользователей tooautomatically get вошедшего tooPlanMyLeave (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал управления Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с PlanMyLeave требуется hello следующих элементов:

- подписка Azure AD;
- подписка PlanMyLeave с поддержкой единого входа.


> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.


tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не следует использовать рабочую среду при отсутствии необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление PlanMyLeave из галереи hello
2. Настройка и проверка единого входа в Azure AD


## <a name="adding-planmyleave-from-hello-gallery"></a>Добавление PlanMyLeave из галереи hello
tooconfigure hello интеграции PlanMyLeave в Azure AD, вы должны tooadd PlanMyLeave из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd PlanMyLeave из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портала управления Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".

    ![Приложения][3]

4. Введите в поле поиска hello **PlanMyLeave**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_001.png)

5. В панели результатов hello выберите **PlanMyLeave**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в PlanMyLeave с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в PlanMyLeave является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в PlanMyLeave должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в PlanMyLeave.

tooconfigure и теста Azure AD единого входа с PlanMyLeave, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя PlanMyLeave](#creating-a-planmyleave-test-user)**  -toohave аналог Саймон Britta в PlanMyLeave, представление связанных toohello Azure AD ей.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал управления Azure hello и настройки единого входа в приложении PlanMyLeave.

**tooconfigure Azure AD единого входа с PlanMyLeave, выполните следующие шаги hello.**

1. На портале управления Azure hello на hello **PlanMyLeave** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** странице диалогового окна как **режим** выберите **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_01.png)

3. На hello **URL-адреса и домена PlanMyLeave** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_02.png)

    а. В hello **на URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company-name>.planmyleave.com/Login.aspx`
    
    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company-name>.planmyleave.com`

    > [!NOTE] 
    > Обратите внимание на то, что они не hello реальные значения. У вас есть tooupdate входа эти значения с hello фактический URL-адрес и идентификатор. Обратитесь к [PlanMyLeave поддержки](mailto:support@planmyleave.com) tooget эти значения.

4. На hello **сертификат подписи SAML** щелкните **Создание нового сертификата**.

    ![Настройка единого входа](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_03.png)     

5. На hello **создать новый сертификат** диалоговое окно, щелкните значок календаря hello и выберите **даты истечения срока действия**. Затем нажмите кнопку **Сохранить**.

    ![Настройка единого входа](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_300.png)

6. На hello **сертификат подписи SAML** выберите **активировать новый сертификат** и нажмите кнопку **Сохранить** кнопки.

    ![Настройка единого входа](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_04.png)

7. На всплывающее окно hello **сертификат продолжения** окно, нажмите кнопку **ОК**.

    ![Настройка единого входа](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_400.png)

8. На hello **сертификат подписи SAML** щелкните **сертификата (base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_05.png) 

9. На hello **конфигурации PlanMyLeave** щелкните **Настройка PlanMyLeave** tooopen **Настройка входа** окна.

    ![Настройка единого входа](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_06.png) 

    ![Настройка единого входа](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_07.png)

10. В другом окне веб-браузера войдите в свой клиент PlanMyLeave в качестве администратора.

11. Go слишком**настройки системы**. Затем на hello **Управление безопасностью** щелкните **параметры SAML компании** .

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_002.png) 

12. На hello **параметры SAML** щелкните значок редактора.

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_003.png)

13. На hello **обновления параметры SAML** выполните следующие шаги hello:

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_004.png)

    а.  В hello **URL-адрес входа** текстовое поле, помещение значения hello **SAML единого входа URL-адрес службы** из окна конфигурации приложения Azure AD.

    b.  Откройте в блокноте файл загруженный сертификат, копировать только содержимое hello между hello---Begin Certificate---и---End certificate---его в буфер обмена, а затем вставьте его toohello **сертификат** текстового поля.

    c. Значение»**включаются**«слишком»**Да**».

    d. Щелкните **Сохранить**.



### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя на портале управления Azure hello, вызывается Саймон Britta.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал управления Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_01.png) 

2. Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_02.png) 

3. Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**. 



### <a name="creating-a-planmyleave-test-user"></a>Создание тестового пользователя PlanMyLeave

Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в PlanMyLeave. Приложение PlanMyLeave поддерживает JIT-подготовку. Эта функция включена по умолчанию.

В этом разделе никакие действия с вашей стороны не требуются. Если он еще не существует во время попытки tooaccess PlanMyLeave создается новый пользователь.

> [!NOTE]
> Если требуется toocreate пользователя вручную, необходимо toocontact [PlanMyLeave поддержки](mailto:support@planmyleave.com).



### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления ее tooPlanMyLeave доступа.

![Назначение пользователя][200] 

**tooassign tooPlanMyLeave Britta Simon выполните следующие шаги hello.**

1. На портале управления Azure hello, открыть представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **PlanMyLeave**.

    ![Настройка единого входа](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_50.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    


### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello PlanMyLeave плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour PlanMyLeave приложения.


## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_203.png