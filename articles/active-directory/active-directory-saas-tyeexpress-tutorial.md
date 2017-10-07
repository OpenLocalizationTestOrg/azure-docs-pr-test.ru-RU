---
title: "Руководство по интеграции Azure Active Directory с T&E Express | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и T & E Express."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: B42374E5-2559-4309-8EF2-820BEE7EBB0C
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: jeedes
ms.openlocfilehash: 9a568ace8dbc75fadbf37554996b1b597a813d56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-te-express"></a>Руководство по интеграции Azure Active Directory с T&E Express

В этом учебнике вы узнаете, как toointegrate T & E экспресс-выпуск с Azure Active Directory (Azure AD).

Интеграция с Azure AD T & E Express предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooT & E Express
- Вы можете включить их учетные записи Azure AD пользователи tooautomatically get вошедшего tooT & E Express (Single Sign-On)
- Можно управлять учетными записями в одном централизованном месте - hello портал управления Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с T & E Express необходимо hello следующих элементов:

- подписка Azure AD;
- подписка T&E Express с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не следует использовать рабочую среду при отсутствии необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление T & E Express из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-te-express-from-hello-gallery"></a>Добавление T & E Express из галереи hello
tooconfigure hello интеграции T & E Express в Azure AD, вы должны tooadd T & E Express из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd T & E Express из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портала управления Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".

    ![Приложения][3]

4. Введите в поле поиска hello **T & E Express**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_search.png)

5. В панели результатов hello выберите **T & E Express**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в T&E Express с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в T & E Express является tooa в Azure AD. Другими словами связи между пользователя Azure AD и hello, связанные с пользователем в T & E Express toobe потребностей установлено.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в T & E Express.

tooconfigure и теста Azure AD единого входа с T & E Express, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя T & E Express](#creating-a-te-express-test-user)**  -toohave аналог Саймон Britta в T & E Express, представление связанных toohello Azure AD ей.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал управления Azure hello и настройки единого входа в приложении T & E Express.

**tooconfigure Azure AD единого входа с T & E, экспресс-выпуск выполните следующие шаги hello.**

1. На портале управления Azure hello на hello **T & E Express** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна, как **режим** выберите **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_samlbase.png)

3. На hello **T & E Express доменов и URL-адреса** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_url.png)

    а. В hello **идентификатор** текстовое поле, значение типа hello как:`https://<domain>.tyeexpress.com`

    b. В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`

    > [!NOTE] 
    > Обратите внимание на то, что они не hello реальные значения. У вас tooupdate эти значения с hello фактический идентификатор и ответ URL-адрес. Здесь мы предлагаем вам toouse hello уникальное значение строки в hello идентификатор. Обратитесь к [T & E Express поддержки](http://www.tyeexpress.com/contacto.aspx) tooget эти значения.

5. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.

    ![Настройка единого входа](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_certificate.png) 

6. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_400.png)

8. tooconfigure единого входа на **T & E быстрой** стороне, toohello входа T & E express приложения без SAML единого входа с использованием учетных данных администратора.

9. В разделе hello **администратора** щелкните **домена SAML** tooOpen hello страница "Параметры SAML".

    ![Настройка единого входа](./media/active-directory-saas-tyeexpress-tutorial/tye-SAML.png)

10. Выберите hello **Activar(Activate)** меню **нет** слишком**SI(Yes)**. В hello **метаданные поставщика удостоверений** текстовое поле, вставить hello метаданных XML, что у вас есть donwloaded из портала Azure.

    ![Настройка единого входа](./media/active-directory-saas-tyeexpress-tutorial/tyeAdmin.png)

11. Щелкните hello **Guardar(Save)** кнопку Параметры toosave hello. 


### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя на портале управления Azure hello, вызывается Саймон Britta.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал управления Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_01.png) 

2. Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_02.png) 

3. Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-te-express-test-user"></a>Создание тестового пользователя T&E Express

В порядке tooenable toolog пользователей Azure AD в T & E Express их необходимо подготовить в T & E Express.  
В случае T&E Express подготовка выполняется вручную.

**tooprovision учетных записей пользователей, выполните следующие действия hello:**

1. Войдите в tooyour T & E Express сайт компании в качестве администратора.

2. Под тегом администратора щелкните на главной странице hello tooopen пользователей пользователей.

    ![Добавление сотрудника](./media/active-directory-saas-tyeexpress-tutorial/tye-adminusers.png)

3. На домашней странице приветствия нажмите кнопку  **+**  tooadd hello пользователей.

    ![Добавление сотрудника](./media/active-directory-saas-tyeexpress-tutorial/tye-usershome.png)

4. Введите все обязательные сведения hello, задаваемые в форме hello и щелкните hello сохранить сведения hello toosave кнопки.

    ![Добавление сотрудника](./media/active-directory-saas-tyeexpress-tutorial/tye-usersadd.png)

    ![Добавление сотрудника](./media/active-directory-saas-tyeexpress-tutorial/tye-userssave.png)


### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа, предоставляя свой доступ tooT & E Express.

![Назначение пользователя][200] 

**tooassign tooT Britta Simon & E, экспресс-выпуск выполните следующие шаги hello.**

1. На портале управления Azure hello, открыть представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **T & E Express**.

    ![Настройка единого входа](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello T & E Express плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour T & E Express приложения.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_203.png

