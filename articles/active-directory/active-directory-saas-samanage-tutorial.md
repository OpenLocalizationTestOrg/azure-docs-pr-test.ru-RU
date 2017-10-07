---
title: "Руководство по интеграции Azure Active Directory с Samanage | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Samanage."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0db4fb0-7eec-48c2-9c7a-beab1ab49bc2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: c8edc29f113b8088438618a731e97c0f4f155b9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-samanage"></a>Руководство. Интеграция Azure Active Directory с Samanage

В этом учебнике вы узнаете, как toointegrate Samanage с Azure Active Directory (Azure AD).

Интеграция Samanage с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooSamanage
- Можно включить на пользователей tooautomatically get вошедшего tooSamanage (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Samanage требуется hello следующих элементов:

- подписка Azure AD;
- подписка Samanage с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Samanage из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-samanage-from-hello-gallery"></a>Добавление Samanage из галереи hello
tooconfigure hello интеграции Samanage в Azure AD, вы должны tooadd Samanage из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Samanage из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Samanage**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_search.png)

5. В панели результатов hello выберите **Samanage**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Samanage с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Samanage является tooa в Azure AD. Другими словами связи между пользователя Azure AD и hello связанных пользователей в Samanage должен установить toobe.

В Samanage, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Samanage, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Samanage](#creating-a-samanage-test-user)**  -toohave аналог Саймон Britta в Samanage, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в Samanage приложения.

**tooconfigure Azure AD единого входа с помощью Samanage, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Samanage** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_samlbase.png)

3. На hello **URL-адреса и домена Samanage** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<Company Name>.samanage.com/saml_login/<Company Name>`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<Company Name>.samanage.com`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновите эти значения с hello фактический URL-адрес входа и идентификатор, который описан далее в учебнике hello. Для получения дополнительных сведений обратитесь к [группе поддержки клиентов Samanage](https://www.samanage.com/support).    
 
4. На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-samanage-tutorial/tutorial_general_400.png)

6. На hello **конфигурации Samanage** щелкните **Настройка Samanage** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода и идентификатор сущности SAML** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_configure.png) 

7. В другом окне веб-браузера войдите на сайт Samanage компании в качестве администратора.

8. Щелкните **Панель мониторинга** и выберите **Настройка** в левой области навигации.
   
    ![Панель мониторинга](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Панель мониторинга")

9. Щелкните **Единый вход**.
   
    ![Единый вход](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "Единый вход")

10. Перейдите в слишком**вход с помощью SAML** выполните следующие шаги hello:
   
    ![Вход с помощью SAML](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "Вход с помощью SAML")
 
    а. Установите флажок **Enable Single Sign-On with SAML**(Включить единый вход с помощью SAML).  
 
    b. В hello **URL-адрес поставщика удостоверений** текстовое значение hello вставить **идентификатор сущности SAML** скопирован из портала Azure.    
 
    c. Подтвердите hello **URL-адрес входа** hello совпадений **на URL-адрес входа** из **URL-адреса и домена Samanage** раздела на портале Azure.
 
    d. В hello **URL-адрес выхода** текстовом поле введите значение hello **URL-адрес выхода** скопирован из портала Azure.
 
    д. В hello **издатель SAML** текстовое поле, URI идентификатора приложения hello тип установить в поставщик удостоверений.
 
    f. Откройте сертификат кодировке base-64 загружен с портала Azure в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **вставьте вашего поставщика удостоверений x.509 ниже сертификат** текстового поля.
 
    ж. Установите флажок **Create users if they do not exist in Samanage**(Создавать пользователей, если они не существуют в Samanage).
 
    h. Нажмите кнопку **Обновить**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
 
### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-samanage-test-user"></a>Создание тестового пользователя в приложении Samanage

Пользователи toolog tooenable Azure AD в tooSamanage, их необходимо подготовить в Samanage.  
В случае hello объекта Samanage Подготовка выполняется вручную.

**tooprovision учетной записи пользователя, выполните следующие шаги hello.**

1. Войдите на корпоративный сайт Samanage в качестве администратора.

2. Щелкните **Dashboard** (Панель мониторинга) и выберите **Setup** (Настройка) в левой области навигации.
   
    ![Настройка](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Настройка")

3. Нажмите кнопку hello **пользователей** вкладка
   
    ![Пользователи](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "Пользователи")

4. Щелкните **Новый пользователь**.
   
    ![Новый пользователь](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "Новый пользователь")

5. Тип hello **имя** и hello **адрес электронной почты** учетной записи Azure Active Directory tooprovision и щелкните **создать пользователя**.
   
    ![Создание пользователя](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "Создание пользователя")
   
   >[!NOTE]
   >Hello владельцем учетной записи Azure Active Directory получит сообщение электронной почты и выполните их учетных записей tooconfirm ссылку, чтобы она стала активной. Можно использовать любые другие Samanage пользователя средства создания учетных записей или API, предоставленные Samanage tooprovision Azure Active Directory учетных записей пользователей.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooSamanage доступа.

![Назначение пользователя][200] 

**tooassign tooSamanage Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Samanage**.

    ![Настройка единого входа](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello Samanage плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Samanage приложения.
Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_203.png

