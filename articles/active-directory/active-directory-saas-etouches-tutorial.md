---
title: "Руководство по интеграции Azure Active Directory с etouches | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и etouches."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 76cccaa8-859c-4c16-9d1d-8a6496fc7520
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 5f3ff7550e660b0fc52612140ca55061504b5edd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-etouches"></a>Руководство. Интеграция Azure Active Directory с etouches

В этом учебнике вы узнаете, как etouches toointegrate с Azure Active Directory (Azure AD).

Интеграция с Azure AD etouches предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooetouches
- Можно включить на пользователей tooautomatically get вошедшего tooetouches (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с etouches требуется hello следующих элементов:

- подписка Azure AD;
- подписка etouches с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление etouches из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-etouches-from-hello-gallery"></a>Добавление etouches из галереи hello
tooconfigure hello интеграции etouches в Azure AD, вы должны etouches tooadd из списка tooyour коллекции hello управляемых приложений SaaS.

**etouches tooadd из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Кнопка Hello Azure Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Hello корпоративных приложений колонку][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Кнопка нового приложения Hello][3]

4. Введите в поле поиска hello **etouches**выберите **etouches** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.

    ![etouches в списке результатов hello](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в etouches с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в etouches является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в etouches должен установить toobe.

В etouches, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с etouches, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя, прошедшего etouches](#create-an-etouches-test-user)**  -toohave аналог Саймон Britta в etouches, который представляет связанный toohello Azure AD пользователя.
4. **[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении etouches.

**tooconfigure Azure AD единого входа с etouches, выполните следующие шаги hello.**

1. В hello в hello портала Azure **etouches** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_samlbase.png)

3. На hello **etouches URL-адреса и домена** выполните следующие шаги hello:

    ![Сведения о домене и URL-адресах единого входа для приложения etouches](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://www.eiseverywhere.com/<instance name>`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить значение hello hello фактическое вход URL-адрес и идентификатор, который описан далее в учебнике hello.
    > 

4. etouches приложение ожидает утверждения SAML hello в определенном формате. Настройка следующих утверждений для этого приложения hello. Вы можете управлять hello значения этих атрибутов из hello **атрибут пользователя** приложения hello. пример Hello следующий снимок экрана для этого. 

    ![Атрибут пользователя](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_attribute.png) 

5. В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна, Настройка атрибутов токена SAML, как показано на рисунке hello и выполните следующие шаги hello:
    
    | Имя атрибута | Значение атрибута |
    | ------------------- | -------------------- |
    | Email | user.mail |    
    
    а. Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.

    ![Добавление атрибута](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_04.png)

    ![Диалоговое окно добавления атрибута](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_05.png)

    b. В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.

    c. Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.
    
    d. Нажмите кнопку **ОК**. 

6. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_certificate.png) 

7. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-etouches-tutorial/tutorial_general_400.png)

8. tooget единого входа, настроенному для вашего приложения, выполните следующие шаги в приложении etouches hello hello. 

    ![Настройка etouches](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_06.png) 

    а. Имя входа слишком**etouches** приложения с помощью hello права администратора.
   
    b. Go toohello **SAML** конфигурации.

    c. В hello **Общие параметры** статьи, откройте загруженный сертификат из портала Azure в блокноте, hello копирования содержимого и вставьте его в текстовое поле метаданных hello поставщика Удостоверений. 

    d. Щелкните hello **сохранить & остаться** кнопки.
  
    д. Щелкните hello **обновление метаданных** кнопку в hello раздел метаданных SAML. 

    f. Это приведет к открытию страницы hello и выполнить единый вход. Один раз hello единого входа работает, а затем можно настроить имя пользователя hello.

    ж. В поле имя пользователя hello выбрать hello **emailaddress** как показано в приведенном ниже рисунке hello. 

    h. Копировать hello **идентификатор сущности SP** значение и вставьте его в hello **идентификатор** текстовое поле находится в **etouches URL-адреса и домена** раздела на портале Azure.

    i. Копировать hello **URL-адрес единого входа и ACS** значение и вставьте его в hello **URL-адрес входа** текстовое поле находится в **etouches URL-адреса и домена** раздела на портале Azure.
   
> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание тестового пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-etouches-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-etouches-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Кнопка "Добавить" Hello](./media/active-directory-saas-etouches-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-etouches-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="create-an-etouches-test-user"></a>Создание тестового пользователя etouches

В этом разделе описано, как создать пользователя Britta Simon в приложении etouches. Работать с [etouches клиента поддержки](https://www.etouches.com/event-software/support/customer-support/) tooadd hello пользователей на платформе etouches hello.

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooetouches доступа.

![Назначение пользователям ролей hello][200] 

**tooassign tooetouches Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **etouches**.

    ![ссылка etouches Hello в списке приложений hello](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Hello ссылку «Пользователи и группы»][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![область назначения, добавьте Hello][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа


Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".

При нажатии кнопки etouches плитки в панели доступа hello приветствия, вы должны получить автоматически вошедшего tooyour etouches приложения.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_203.png

