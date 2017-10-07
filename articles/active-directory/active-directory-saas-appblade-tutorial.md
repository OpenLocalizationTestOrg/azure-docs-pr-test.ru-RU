---
title: "Руководство. Интеграция Azure Active Directory с AppBlade | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и AppBlade."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3360d7aa-6518-4f99-88bd-b7f7258183e8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 06f3d8fcee97945c867bca6f3aebe15ecef04617
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-appblade"></a>Руководство. Интеграция Azure Active Directory с AppBlade

В этом учебнике вы узнаете, как toointegrate AppBlade с Azure Active Directory (Azure AD).

Интеграция с Azure AD AppBlade предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooAppBlade
- Можно включить на пользователей tooautomatically get вошедшего tooAppBlade (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с AppBlade требуется hello следующих элементов:

- подписка Azure AD;
- подписка AppBlade с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление AppBlade из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-appblade-from-hello-gallery"></a>Добавление AppBlade из галереи hello
tooconfigure hello интеграции AppBlade в Azure AD, вы должны tooadd AppBlade из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd AppBlade из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **AppBlade**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_search.png)

5. В панели результатов hello выберите **AppBlade**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в приложение AppBlade с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в AppBlade является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в AppBlade должен установить toobe.

В AppBlade, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с AppBlade, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя, прошедшего AppBlade](#creating-an-appblade-test-user)**  -toohave аналог Саймон Britta в AppBlade, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении AppBlade.

**tooconfigure Azure AD единого входа с AppBlade, выполните следующие шаги hello.**

1. В hello в hello портала Azure **AppBlade** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_samlbase.png)

3. На hello **URL-адреса и домена AppBlade** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_url.png)

    В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.appblade.com/saml/<tenantid>`

    > [!NOTE] 
    > Это значение приведено для справки. Значение hello обновления с hello фактический URL-адрес входа. Обратитесь к [группа поддержки клиента AppBlade](mailto:support@appblade.com) tooget значение hello. 
 
4. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-appblade-tutorial/tutorial_general_400.png)

6. tooconfigure единого входа на **AppBlade** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[AppBlade поддержки](mailto:support@appblade.com). Кроме того, попросите их tooconfigure hello **URL-адрес издателя единого входа** как `https://appblade.com/saml`. Этот параметр является обязательным для toowork.


> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
 
### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-appblade-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-appblade-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-appblade-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-appblade-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-an-appblade-test-user"></a>Создание тестового пользователя AppBlade

Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в AppBlade. Приложение AppBlade поддерживает JIT-подготовку. Эта функция включена по умолчанию. **Убедитесь, что ваше доменное имя настроено в AppBlade для подготовки пользователей. После этого только hello в время подготовки пользователей работает.**

Если пользователь hello имеет адрес электронной почты, заканчивая hello домена, настроенного с AppBlade для вашей учетной записи, то hello пользователя автоматически соединит как член с уровнем разрешений hello, указываемые hello учетной записи, которая является одной из «Basic» (basic пользователя, которому можно установить только приложения), «Участник» (пользователь, который можно отправить новых версий приложения и управления проектами) или «Administrator» (учетная запись toohello права полного администратора). Обычно один бы выбрать Basic и затем продвинуть пользователей вручную через имя входа администратора (AppBlade должен tooconfigure либо имя входа администратора на основе электронной почты заранее или повысить пользователя от имени клиента hello после входа в систему).

В этом разделе никакие действия с вашей стороны не требуются. Новый пользователь создается во время попытки tooaccess AppBlade, если он еще не существует. 

> [!NOTE]
> Если требуется toocreate пользователя вручную, необходимо toocontact hello [AppBlade поддержки](mailto:support@appblade.com).

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooAppBlade доступа.

![Назначение пользователя][200] 

**tooassign tooAppBlade Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **AppBlade**.

    ![Настройка единого входа](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".  
При нажатии кнопки hello AppBlade плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour AppBlade приложения. 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_203.png

