---
title: "Руководство по интеграции Azure Active Directory с Panorama9 | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Panorama9."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5e28d7fa-03be-49f3-96c8-b567f1257d44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 548fb6434d920e076db98a0193f8dfdf8a958a91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panorama9"></a>Учебник. Интеграция Azure Active Directory с Panorama9

В этом учебнике вы узнаете, как toointegrate Panorama9 с Azure Active Directory (Azure AD).

Интеграция Panorama9 с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooPanorama9
- Можно включить на пользователей tooautomatically get вошедшего tooPanorama9 (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Panorama9 требуется hello следующих элементов:

- подписка Azure AD;
- Подписка с поддержкой единого входа Panorama9.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Panorama9 из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-panorama9-from-hello-gallery"></a>Добавление Panorama9 из галереи hello
tooconfigure hello интеграции Panorama9 в Azure AD, вы должны tooadd Panorama9 из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Panorama9 из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Panorama9**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_search.png)

5. В панели результатов hello выберите **Panorama9**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе описана настройка и проверка единого входа Azure AD в Panorama9 с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Panorama9 является tooa в Azure AD. Другими словами связи между пользователя Azure AD и hello связанных пользователей в Panorama9 должен установить toobe.

В Panorama9, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Panorama9, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Panorama9](#creating-a-panorama9-test-user)**  -toohave аналог Саймон Britta в Panorama9, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в Panorama9 приложения.

**tooconfigure Azure AD единого входа с Panorama9, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Panorama9** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_samlbase.png)

3. На hello **URL-адреса и домена Panorama9** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес как:`https://dashboard.panorama9.com/saml/access/3262`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`http://www.panorama9.com/saml20/<tenant-name>`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить значения hello фактический URL-адрес входа и идентификатор. Обратитесь к [группа поддержки клиента Panorama9](https://support.panorama9.com) tooget эти значения. 
 
4. На hello **сертификат подписи SAML** раздел, hello копирования **ОТПЕЧАТОК** значение сертификата.

    ![Настройка единого входа](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-panorama9-tutorial/tutorial_general_400.png)

6. На hello **конфигурации Panorama9** щелкните **Настройка Panorama9** tooopen **Настройка входа** окна. Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_configure.png) 

5. В другом окне веб-браузера войдите на сайт Panorama9 своей компании в качестве администратора.

6. Щелкните hello панели инструментов в верхней части hello **управление**, а затем нажмите кнопку **расширения**.
   
   ![Расширения](./media/active-directory-saas-panorama9-tutorial/ic790023.png "Расширения")
7. На hello **расширения** диалоговое окно, нажмите кнопку **Single Sign-On**.
   
   ![Единый вход](./media/active-directory-saas-panorama9-tutorial/ic790024.png "Единый вход")
8. В hello **параметры** выполните следующие шаги hello:
   
   ![Параметры](./media/active-directory-saas-panorama9-tutorial/ic790025.png "Параметры")
   
    а. В **URL-адрес поставщика удостоверений** текстовое значение hello вставить **единого входа URL-адрес службы**, который вы скопировали из портала Azure.
   
    b. В **отпечаток сертификата** текстовое поле, вставить hello **отпечаток** значение сертификат, который вы скопировали из портала Azure.    
         
9. Щелкните **Сохранить**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-panorama9-test-user"></a>Создание тестового пользователя Panorama9

В порядке tooenable toolog пользователей Azure AD в Panorama9 их необходимо подготовить в Panorama9.  

В случае Panorama9 hello Подготовка выполняется вручную.

**tooconfigure подготовки пользователей, выполните следующие шаги hello.**

1. Войдите в tooyour **Panorama9** сайт компании от имени администратора.

2. В меню в верхней части hello hello выберите **управление**, а затем нажмите кнопку **пользователей**.
   
  ![Пользователи](./media/active-directory-saas-panorama9-tutorial/ic790027.png "Пользователи")

3. В hello раздел "пользователи", щелкните  **+**  tooadd нового пользователя.

 ![Пользователи](./media/active-directory-saas-panorama9-tutorial/ic790028.png "Пользователи")

4. Последовательно выберите toohello раздел данных пользователя, типа hello адрес электронной почты действительного пользователя Azure Active Directory требуется tooprovision в hello **электронной почты** текстового поля.

5. Поступать toohello раздел "пользователи", нажмите кнопку **Сохранить**.
   
> [!NOTE]
    > Владелец учетной записи Azure Active Directory Hello получает сообщение электронной почты и соответствует tooconfirm ссылку свою учетную запись, чтобы она стала активной.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooPanorama9 доступа.

![Назначение пользователя][200] 

**tooassign tooPanorama9 Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Panorama9**.

    ![Настройка единого входа](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello Panorama9 плитки в панели доступа hello, вы должны получить автоматически вошедшего tooPanorama9 приложения.
Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_203.png

