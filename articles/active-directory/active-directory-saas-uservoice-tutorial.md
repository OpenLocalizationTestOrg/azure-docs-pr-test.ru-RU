---
title: "Руководство по интеграции Azure Active Directory с UserVoice | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и UserVoice."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 684a405b-8932-46f6-b43a-4d97a42b6b87
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: 9eade8435ae6c6a3821bbbec9ab7c27ed7ad91ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-uservoice"></a>Руководство по интеграции Azure Active Directory с UserVoice

В этом учебнике вы узнаете, как toointegrate UserVoice с Azure Active Directory (Azure AD).

Интеграция UserVoice с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooUserVoice.
- Можно включить на пользователей tooautomatically get вошедшего tooUserVoice (Single Sign-On) с помощью своих учетных записей Azure AD.
- Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с UserVoice требуется hello следующих элементов:

- подписка Azure AD;
- подписка UserVoice с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление UserVoice из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-uservoice-from-hello-gallery"></a>Добавление UserVoice из галереи hello
tooconfigure hello интеграции UserVoice в Azure AD, вы должны tooadd UserVoice из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd UserVoice из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Кнопка Hello Azure Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Hello корпоративных приложений колонку][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Кнопка нового приложения Hello][3]

4. Введите в поле поиска hello **UserVoice**выберите **UserVoice** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.

    ![UserVoice в списке результатов hello](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе описана настройка и проверка единого входа Azure AD в приложение UserVoice с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователя аналог hello в UserVoice — tooa пользователя в Azure AD. Другими словами связи между пользователя Azure AD и hello связанных пользователей в UserVoice должен установить toobe.

В UserVoice, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с UserVoice, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя UserVoice](#create-a-uservoice-test-user)**  -toohave аналог Саймон Britta в UserVoice, который представляет связанный toohello Azure AD пользователя.
4. **[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении UserVoice.

**Azure AD tooconfigure единого входа с UserVoice, выполните следующие шаги hello.**

1. В hello в hello портала Azure **UserVoice** странице интеграции приложения щелкните **единого входа**.

    ![Ссылка "Настройка единого входа"][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_samlbase.png)

3. На hello **URL-адреса и домена UserVoice** выполните следующие шаги hello:

    ![Сведения о домене и URL-адресах единого входа для приложения UserVoice](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenantname>.UserVoice.com`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenantname>.UserVoice.com`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить значения hello фактический URL-адрес входа и идентификатор. Обратитесь к [группа поддержки клиент UserVoice](https://www.uservoice.com/) tooget эти значения.

4. На hello **сертификат подписи SAML** раздел, hello копирования **ОТПЕЧАТОК** значение сертификата.

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-uservoice-tutorial/tutorial_general_400.png)

6. На hello **конфигурации UserVoice** щелкните **Настройка UserVoice** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Конфигурация UserVoice](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_configure.png) 

7. В другом окне браузера Войдите на сайте компании UserVoice tooyour в качестве администратора.

8. Щелкните hello панели инструментов в верхней части hello **параметры**и выберите **веб-портале** меню "hello".
   
    ![Раздел параметров на стороне приложения](./media/active-directory-saas-uservoice-tutorial/ic777519.png "Параметры")

9. На hello **веб-портале** hello на вкладке **проверки подлинности пользователя** щелкните **изменить** tooopen hello **изменение проверки подлинности пользователей** диалоговое окно страница.
   
    ![Вкладка веб-портала](./media/active-directory-saas-uservoice-tutorial/ic777520.png "Веб-портал")

10. На hello **изменение проверки подлинности пользователей** диалогового окна выполните следующие шаги hello:
   
    ![Изменение проверки подлинности пользователя](./media/active-directory-saas-uservoice-tutorial/ic777521.png "Изменение проверки подлинности пользователя")
   
    а. Выберите **Единый вход (SSO)**.
 
    b. Вставить hello **SAML единого входа URL-адрес службы** значение, которое было скопировано из hello портал Azure в hello **SSO удаленный вход** текстового поля.

    c. Вставить hello **URL-адрес выхода** значение, которое было скопировано из hello портал Azure в hello **textbox удаленный единый выход SSO**.
 
    d. Вставить hello **отпечаток** значение, которое было скопировано из портала Azure в **текущий отпечаток сертификата SHA1** текстового поля.
    
    д. Нажмите кнопку **Сохранить параметры проверки подлинности**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

   ![Создание тестового пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-uservoice-tutorial/create_aaduser_01.png)

2. слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-uservoice-tutorial/create_aaduser_02.png)

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-uservoice-tutorial/create_aaduser_03.png)

4. В hello **пользователя** диалогового окна выполните следующие шаги hello:

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-uservoice-tutorial/create_aaduser_04.png)

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.

    c. Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.

    d. Щелкните **Создать**.
 
### <a name="create-a-uservoice-test-user"></a>Создание тестового пользователя UserVoice

Пользователи toolog tooenable Azure AD в tooUserVoice, их необходимо подготовить в UserVoice. В случае hello объекта UserVoice Подготовка осуществляется вручную.

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a>tooprovision учетной записи пользователя, выполните следующие шаги hello.
1. Войдите в tooyour **UserVoice** клиента.

2. Go слишком**параметры**.
   
    ![Параметры](./media/active-directory-saas-uservoice-tutorial/ic777811.png "Параметры")

3. Выберите пункт **Общие**.

4. Выберите пункт **Агенты и разрешения**.
   
    ![Агенты и разрешения](./media/active-directory-saas-uservoice-tutorial/ic777812.png "Агенты и разрешения")

5. Нажмите кнопку **Добавить администраторов**.
   
    ![Добавление администраторов](./media/active-directory-saas-uservoice-tutorial/ic777813.png "Добавление администраторов")

6. На hello **пригласить администраторов** диалоговое окно, выполните следующие шаги hello:
   
    ![Пригласить администраторов](./media/active-directory-saas-uservoice-tutorial/ic777814.png "Пригласить администраторов")
   
    а. В текстовом поле hello сообщения электронной почты, введите адрес электронной почты hello hello учетной записи tooprovision и нажмите кнопку **добавить**.
   
    b. Нажмите кнопку **Пригласить**.

> [!NOTE]
> Можно использовать любые другие UserVoice пользователя средства создания учетных записей или интерфейсы API, предоставляемые UserVoice tooprovision учетных записей пользователей AAD.

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooUserVoice доступа.

![Назначение пользователям ролей hello][200] 

**tooassign tooUserVoice Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **UserVoice**.

    ![ссылка UserVoice Hello в списке приложений hello](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_app.png)  

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Hello ссылку «Пользователи и группы»][202]

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![область назначения, добавьте Hello][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello UserVoice плитки в панели доступа hello, вы должны получить приложение автоматически вошедшего tooyour UserVoice.
Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_203.png

