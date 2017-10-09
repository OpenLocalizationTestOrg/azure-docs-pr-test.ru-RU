---
title: "Руководство по интеграции Azure Active Directory с Thoughtworks Mingle | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Thoughtworks Mingle."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 69d859d9-b7f7-4c42-bc8c-8036138be586
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: c17f8e13d2db3de7d228d9b27128d134f98d6cdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thoughtworks-mingle"></a>Учебник. Интеграция Azure Active Directory с Thoughtworks Mingle

В этом учебнике вы узнаете, как toointegrate Thoughtworks Mingle с Azure Active Directory (Azure AD).

Интеграция Thoughtworks Mingle с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooThoughtworks Mingle
- Можно включить на пользователей tooautomatically get вошедшего tooThoughtworks Mingle (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Thoughtworks Mingle требуется hello следующих элементов:

- подписка Azure AD;
- подписка Thoughtworks Mingle с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Thoughtworks Mingle из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-thoughtworks-mingle-from-hello-gallery"></a>Добавление Thoughtworks Mingle из галереи hello
tooconfigure hello интеграции Thoughtworks Mingle в Azure AD, вы должны tooadd Thoughtworks Mingle из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Thoughtworks Mingle из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Кнопка Hello Azure Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Hello корпоративных приложений колонку][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Кнопка нового приложения Hello][3]

4. Введите в поле поиска hello **Thoughtworks Mingle**выберите **Thoughtworks Mingle** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.

    ![ThoughtWorks Mingle в списке результатов hello](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Thoughtworks Mingle с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Thoughtworks Mingle является tooa в Azure AD. Другими словами связи между пользователя Azure AD и hello связанных пользователей в Thoughtworks Mingle должен установить toobe.

В Thoughtworks Mingle, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Thoughtworks Mingle, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Thoughtworks Mingle](#create-a-thoughtworks-mingle-test-user)**  -toohave аналог Саймон Britta в Thoughtworks Mingle, представление связанных toohello Azure AD пользователя.
4. **[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Thoughtworks Mingle.

**tooconfigure Azure AD единого входа с Thoughtworks Mingle, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Thoughtworks Mingle** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_samlbase.png)

3. На hello **Thoughtworks Mingle доменов и URL-адреса** выполните следующие шаги hello:

    ![Сведения о домене и URL-адресах единого входа для приложения Thoughtworks Mingle](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_url.png)

    В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.mingle.thoughtworks.com`

    > [!NOTE] 
    > значение Hello не является вещественным числом. Значение hello обновления с hello фактический URL-адрес входа. Обратитесь к [Thoughtworks Mingle клиента поддержки](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) tooget значение hello. 
 
4. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_400.png)

6. Войдите в tooyour **Thoughtworks Mingle** сайт компании от имени администратора.

7. Нажмите кнопку hello **администратора** , а затем щелкните **Настройка Единого входа**.
   
    ![Вкладка Admin](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "Настройка единого входа")

8. В hello **Настройка Единого входа** выполните следующие шаги hello:
   
    ![Настройка единого входа](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "Настройка единого входа")
    
    а. файл метаданных tooupload hello, нажмите кнопку **выбрать файл**. 

    b. Нажмите кнопку **Сохранить изменения**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание тестового пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Кнопка "Добавить" Hello](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="create-a-thoughtworks-mingle-test-user"></a>Создание тестового пользователя Thoughtworks Mingle

Для Azure AD пользователи toobe может toosign в они должны быть подготовленных toohello Thoughtworks Mingle приложения с использованием своих имен пользователей Azure Active Directory. В случае Thoughtworks Mingle hello Подготовка выполняется вручную.

**tooconfigure подготовки пользователей, выполните следующие шаги hello.**

1. Войдите в систему tooyour сайт Thoughtworks Mingle компании как администратор.

2. Щелкните **Профиль**.
   
    ![Ваш первый проект](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "Ваш первый проект")

3. Нажмите кнопку hello **администратора** , а затем щелкните **пользователей**.
   
    ![Пользователи](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "Пользователи")

4. Щелкните **Новый пользователь**.
   
    ![Новый пользователь](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "Новый пользователь")

5. На hello **нового пользователя** диалогового окна выполните следующие шаги hello:
   
    ![Диалоговое окно нового пользователя](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "Новый пользователь")  
 
    а. Тип hello **учетное имя**, **отображаемое имя**, **выбранные пароль**, **подтверждение пароля** из допустимых Azure требуется tooprovision учетной записи AD в hello связанные текстовые поля. 

    b. В поле **User type** (Тип пользователя) выберите значение **Full user** (С полным доступом).

    c. Щелкните **Создать этот профиль**.

>[!NOTE]
>Можно использовать любые другие Thoughtworks Mingle пользователя средства создания учетных записей или интерфейсы API, предоставляемые Thoughtworks Mingle tooprovision учетных записей пользователей AAD.
> 

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooThoughtworks Mingle.

![Назначение пользователям ролей hello][200] 

**tooassign Britta Simon tooThoughtworks Mingle, выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Thoughtworks Mingle**.

    ![Hello Thoughtworks Mingle ссылку в списке приложений hello](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Hello ссылку «Пользователи и группы»][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![область назначения, добавьте Hello][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".

При нажатии кнопки hello Thoughtworks Mingle плитки в панели доступа hello, вы должны получить tooyour автоматически подписью в приложении Thoughtworks Mingle.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_203.png

