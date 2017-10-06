---
title: "Учебник. Интеграция Azure Active Directory с Intralinks | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Intralinks."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 147f2bf9-166b-402e-adc4-4b19dd336883
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 6fa49c932d0c48d4b48e04fe91af9fc86a0c1cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intralinks"></a>Руководство. Интеграция Azure Active Directory с Intralinks

В этом учебнике вы узнаете, как toointegrate Intralinks с Azure Active Directory (Azure AD).

Интеграция с Azure AD Intralinks предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooIntralinks
- Можно включить на пользователей tooautomatically get вошедшего tooIntralinks (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Intralinks требуется hello следующих элементов:

- подписка Azure AD;
- подписка Intralinks с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Intralinks из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-intralinks-from-hello-gallery"></a>Добавление Intralinks из галереи hello
tooconfigure hello интеграции Intralinks в Azure AD, вы должны tooadd Intralinks из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Intralinks из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Intralinks**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. В панели результатов hello выберите **Intralinks**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Intralinks с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Intralinks является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Intralinks должен установить toobe.

В Intralinks, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Intralinks, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя, прошедшего Intralinks](#creating-an-intralinks-test-user)**  -toohave аналог Саймон Britta в Intralinks, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Intralinks.

**tooconfigure Azure AD единого входа с Intralinks, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Intralinks** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_samlbase.png)

3. На hello **URL-адреса и домена Intralinks** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_url.png)

    В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`

    > [!NOTE] 
    > Это значение приведено для справки. Измените значение этого параметра hello фактический URL-адрес входа. Обратитесь к [группа поддержки клиента Intralinks](https://www.intralinks.com/contact-1) tooget это значение. 
 
4. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

6. tooconfigure единого входа на **Intralinks** стороны, необходимо загрузить hello toosend **метаданные в формате XML** [Intralinks поддержки](https://www.intralinks.com/contact-1). Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-an-intralinks-test-user"></a>Создание тестового пользователя Intralinks

В этом разделе описано, как создать пользователя Britta Simon в приложении Intralinks. Можно работать с [Intralinks поддержки](https://www.intralinks.com/contact-1) tooadd hello пользователей на платформе Intralinks hello.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooIntralinks доступа.

![Назначение пользователя][200] 

**tooassign tooIntralinks Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Intralinks**.

    ![Настройка единого входа](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.

### <a name="add-intralinks-via-or-elite-application"></a>Добавление приложения Intralinks VIA или Elite

Использует Intralinks hello же платформой удостоверений единого входа для всех других приложений Intralinks, за исключением возможности хранилища приложения. Поэтому если планируется toouse любого другого приложения Intralinks сначала вы имеете tooconfigure единого входа для одного приложения основной Intralinks, используя описанную выше процедуру hello.

После этого можно выполнить hello ниже процедуры tooadd другое приложение Intralinks в клиенте, который можно использовать этот основного приложения для единого входа. 

>[!NOTE]
>Этот компонент является доступны только клиентам SKU Premium tooAzure AD и недоступно для клиентов Free или Basic SKU.

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]


2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Intralinks**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. На **Intralinks добавить приложение** выполнения hello следующие шаги:

    ![Добавление приложения Intralinks VIA или Elite](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addapp.png)

    а. В **имя** текстового поля, введите соответствующее имя приложения hello, например **элиту Intralinks**.

    b. Нажмите кнопку **Добавить**.

6.  В hello в hello портала Azure **Intralinks** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

7. На hello **единого входа** диалогового окна выберите **режим** как **входа на связанный**.
 
    ![Настройка единого входа](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_linkedsignon.png)

8. Получить hello hello SP инициировано SSO URL-адрес [команды Intralinks](https://www.intralinks.com/contact-1) для hello другого Intralinks приложения и введите его в **Настройка URL-адрес входа** как показано ниже. 
    
     ![Настройка единого входа](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_customappurl.png)
    
     В текстовом поле на URL-адрес входа hello введите URL-адрес hello, используемого приложением Intralinks tooyour toosign на пользователей, используя следующий шаблон hello:
   
    `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`

9. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

10. Назначение toouser приложения hello или групп, как показано в разделе "hello"  **[назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**.

### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки Intralinks плитки в панели доступа hello приветствия, вы должны получить автоматически вошедшего tooyour Intralinks приложения.
Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_203.png

