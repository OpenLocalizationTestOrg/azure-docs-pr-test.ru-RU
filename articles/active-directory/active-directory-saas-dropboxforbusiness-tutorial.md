---
title: "Руководство по интеграции Azure Active Directory с Dropbox for Business | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Dropbox для бизнеса."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 63502412-758b-4b46-a580-0e8e130791a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 3f33a43ca8fbd60486d7a400ae8246af768376ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-dropbox-for-business"></a>Руководство. Интеграция Azure Active Directory с Dropbox for Business

В этом учебнике вы узнаете, как toointegrate Dropbox для бизнеса с помощью Azure Active Directory (Azure AD).

Интеграция Dropbox для бизнеса с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooDropbox для бизнеса
- Вы можете включить вашей пользователей tooautomatically get вошедшего tooDropbox для бизнеса (Single Sign-On) учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Dropbox для бизнеса требуется hello следующих элементов:

- подписка Azure AD;
- подписка Dropbox for Business с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление из галереи hello Dropbox для бизнеса
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-dropbox-for-business-from-hello-gallery"></a>Добавление из галереи hello Dropbox для бизнеса
интеграции hello tooconfigure Dropbox для бизнеса в Azure AD, необходимо tooadd Dropbox для бизнеса из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Dropbox для бизнеса из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. Нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна "hello".

    ![Приложения][3]

4. Введите в поле поиска hello **Dropbox для бизнеса**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_search.png)

5. В панели результатов hello выберите **Dropbox для бизнеса**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Dropbox for Business с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow какой пользователь hello аналога в Dropbox для бизнеса — tooa пользователя в Azure AD. Другими словами связи между hello связанных пользователей в Dropbox для бизнеса и пользователя Azure AD должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Dropbox для бизнеса.

tooconfigure и теста Azure AD единого входа с Dropbox для бизнеса, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание Dropbox для бизнеса тестового пользователя](#creating-a-dropbox-for-business-test-user)**  -toohave аналог Саймон Britta в Dropbox для бизнеса, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе Azure AD единым входом в портал Azure hello включить и настроить единый вход в Dropbox для бизнес-приложений.

**Azure AD tooconfigure единого входа с Dropbox для бизнеса, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Dropbox для бизнеса** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_samlbase.png)

3. На hello **Dropbox для бизнеса домена и URL-адреса** выполните следующие шаги hello:

    а. Войдите на tooyour Dropbox для бизнеса. 
   
    ![Настройка единого входа](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "Настройка единого входа")
   
    b. Hello hello левой панели навигации щелкните **консоли администрирования**. 
   
    ![Настройка единого входа](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "Настройка единого входа")
   
    c. На hello **консоли администрирования**, нажмите кнопку **проверки подлинности** hello левой панели навигации. 
   
    ![Настройка единого входа](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "Настройка единого входа")
   
    d. В hello **единого входа** выберите **Включить единый вход**, а затем нажмите кнопку **дополнительные** tooexpand в этом разделе.  
   
    ![Настройка единого входа](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "Настройка единого входа")
   
    д. Скопируйте URL-адрес hello рядом слишком**пользователи могут войти, введя свой адрес электронной почты или переходить непосредственно к**. 
    
    ![Настройка единого входа](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769513.png)
    
    f. На портал Azure, в hello hello **URL-адрес входа** в текстовое поле URL-адрес для вставки hello.

    ![Настройка единого входа](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_url.png)

     В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://www.dropbox.com/sso/<id>`

    > [!NOTE] 
    > Это значение приведено для примера. Обновите значение hello с hello фактический URL-адрес входа получить из их раздела единого входа. Обратитесь к [Dropbox для бизнеса клиента поддержки](https://www.dropbox.com/business/contact) tooget это значение. 
 
4. На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_400.png)

6. На hello **Dropbox для бизнеса конфигурации** щелкните **настроить Dropbox для бизнеса** tooopen **Настройка входа** окна. Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_configure.png) 

7. tooconfigure единого входа на **Dropbox для бизнеса** стороны, перейдите на клиенте Dropbox для бизнеса, в hello **единого входа** раздел hello **проверки подлинности** страницы, выполните следующие шаги hello. 
   
    ![Настройка единого входа](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "Настройка единого входа")
   
    а. Установите флажок **Обязательно**.
   
    b. В hello в hello портала Azure **Настройка входа** окна, hello копирования **SAML единого входа URL-адрес службы** значение, а затем вставьте его в hello **URL-адрес входа** текстового поля.

    c. Нажмите кнопку **изменить сертификат**, а затем найдите tooyour **файл сертификата в кодировке Base64**.

    d. Нажмите кнопку **сохранить изменения** toocomplete hello конфигурации на клиенте DropBox для бизнеса.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_01.png) 

2.  hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_02.png) 

3. Вверху hello hello диалоговое окно, нажмите кнопку **добавить** tooopen hello **пользователя** диалогового окна.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-dropbox-for-business-test-user"></a>Создание тестового пользователя Dropbox for Business

В этом разделе вы создадите в Dropbox for Business пользователя с именем Britta Simon. Приложение Dropbox for Business поддерживает JIT-подготовку. Эта функция включена по умолчанию.

В этом разделе никакие действия с вашей стороны не требуются. Если пользователь еще не существует в Dropbox для бизнеса, создается новый, при попытке tooaccess Dropbox для бизнеса.

>[!Note]
>При необходимости пользователь вручную, обратитесь к toocreate [Dropbox для бизнеса клиента поддержки](https://www.dropbox.com/business/contact) 

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooDropbox для бизнеса.

![Назначение пользователя][200] 

**tooassign tooDropbox Britta Simon для бизнеса, выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Dropbox для бизнеса**.

    ![Настройка единого входа](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello Dropbox для бизнеса плитки в панели доступа hello, вы должны получить страницу входа для Dropbox для бизнес-приложений.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Руководство по настройке Google Apps для автоматической подготовки пользователей](active-directory-saas-dropboxforbusiness-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_203.png

