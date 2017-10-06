---
title: "Руководство по интеграции Azure Active Directory с порталом управления облачными службами для Microsoft Azure | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и портал управления облако Microsoft Azure."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4ea9f47c-25ca-42b0-a878-9e7aa6f34973
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 9596826e3dc1289b95009bf01ec8b86f823ef345
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cloud-management-portal-for-microsoft-azure"></a>Учебник. Интеграция Azure Active Directory с порталом управления облачными службами для Microsoft Azure

В этом учебнике вы узнаете, как toointegrate облака портал управления для Microsoft Azure в Azure Active Directory (Azure AD).

Интеграция с Azure AD портал управления облако Microsoft Azure предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooCloud портал управления для Microsoft Azure
- Ваш пользователей tooautomatically get вошедшего tooCloud портал управления для Microsoft Azure (Single Sign-On) можно включить с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с портала управления облака для Microsoft Azure требуется hello следующих элементов:

- подписка Azure AD;
- подписка портала управления облачными службами для Microsoft Azure с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление облака портал управления для Microsoft Azure из коллекции hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-cloud-management-portal-for-microsoft-azure-from-hello-gallery"></a>Добавление облака портал управления для Microsoft Azure из коллекции hello
tooconfigure hello интеграции облака портал управления для Microsoft Azure в Azure AD, необходимо tooadd облака портал управления для Microsoft Azure из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd облака портал управления для Microsoft Azure из коллекции hello выполните hello следующие шаги.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **облака портал управления для Microsoft Azure**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_search.png)

5. В панели результатов hello выберите **облака портал управления для Microsoft Azure**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описывается настройка и проверка единого входа Azure AD на портале управления облачными службами в Microsoft Azure с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в облаке портал управления для Microsoft Azure является tooa в Azure AD. Другими словами связи между пользователя Azure AD и hello связанных пользователей на портале управления облака для Microsoft Azure должна установить toobe.

На портале управления облака для Microsoft Azure, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и выполнить проверку Azure AD единого входа с помощью портала управления облако Microsoft Azure, необходимы следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание облака портал управления для тестового пользователя Microsoft Azure](#creating-a-cloud-management-portal-for-microsoft-azure-test-user)**  -toohave аналог Саймон Britta на портале управления облака для Microsoft Azure, которая является представлением связанного toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в портал управления облачные приложения Microsoft Azure.

**tooconfigure Azure AD единого входа с помощью портала управления облака для Microsoft Azure выполните следующие шаги hello.**

1. В hello в hello портала Azure **облака портал управления для Microsoft Azure** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_samlbase.png)

3. На hello **портала управления Cloud домена Microsoft Azure и URL-адреса** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_url.png)

    а. В hello **URL-адрес входа** текстовое поле, введите URL-адрес, используя hello следующие шаблоны: 
    
    | |
    |--|
    | `https://portal.newsignature.com/<instancename>` |   
    | `https://portal.igcm.com/<instancename>` |
    
    b. В hello **идентификатор** текстовое поле, введите URL-адрес, используя hello следующие шаблоны: 
    
    | |
    |--|
    | `https://<subdomain>.igcm.com` |
    | `https://<subdomain>.newsignature.com` |

    c. В hello **URL-адрес ответа** текстовое поле, введите URL-адрес, используя hello следующие шаблоны: 
    
    | |
    |--|
    | `https://<subdomain>.igcm.com/<instancename>` |
    | `https://<subdomain>.newsignature.com` |
    | `https://<subdomain>.newsignature.com/<instancename>` |

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновите эти значения с hello фактический URL-адрес входа, идентификатор и ответ URL-адрес. Обратитесь к [облака портал управления для поддержки клиент Microsoft Azure](mailto:jczernuszka@newsignature.com) tooget эти значения. 
 
4. На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-newsignature-tutorial/tutorial_general_400.png)

6. На hello **облака портал управления для Microsoft Azure конфигурации** щелкните **Настройка облака портал управления Microsoft Azure** tooopen **Настройкавхода**окна. Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_configure.png) 

7. tooconfigure единого входа на **облака портал управления для Microsoft Azure** стороны, необходимо загрузить hello toosend **сертификат**, **URL-адрес выхода**, **SAML единого входа URL-адрес службы** и **идентификатор сущности SAML** слишком[облака портал управления для поддержки Microsoft Azure](mailto:jczernuszka@newsignature.com). Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-cloud-management-portal-for-microsoft-azure-test-user"></a>Создание тестового пользователя портала управления облачными службами для Microsoft Azure

Цель этого раздела Hello — toocreate пользователя с именем Britta Simon на портале управления облака для Microsoft Azure. Можно работать с [облака портал управления для поддержки Microsoft Azure](mailto:jczernuszka@newsignature.com) tooadd пользователей hello в hello портала управления Cloud для учетной записи Microsoft Azure.


### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooCloud портал управления для Microsoft Azure.

![Назначение пользователя][200] 

**tooassign tooCloud Britta Simon портал управления для Microsoft Azure, выполните hello следующие шаги.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **облака портал управления для Microsoft Azure**.

    ![Настройка единого входа](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".
При нажатии кнопки hello облака портал управления для Microsoft Azure плитки в панели доступа hello, вы должны получить tooyour автоматически подписан на портал управления облака для приложения Microsoft Azure.

Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_203.png

