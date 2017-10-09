---
title: "Руководство по интеграции Azure Active Directory с BlueJeans | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и BlueJeans."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dfc634fd-1b55-4ba8-94a8-b8288429b6a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: jeedes
ms.openlocfilehash: 67613303a9f854afbf4619418cc1607d329caf94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bluejeans"></a>Руководство по интеграции Azure Active Directory с BlueJeans

В этом учебнике вы узнаете, как toointegrate BlueJeans с Azure Active Directory (Azure AD).

Интеграция BlueJeans с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooBlueJeans
- Можно включить на пользователей tooautomatically get вошедшего tooBlueJeans (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с BlueJeans требуется hello следующих элементов:

- подписка Azure AD;
- подписка BlueJeans с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление BlueJeans из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-bluejeans-from-hello-gallery"></a>Добавление BlueJeans из галереи hello
tooconfigure hello интеграции BlueJeans в Azure AD, вы должны tooadd BlueJeans из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd BlueJeans из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **BlueJeans**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_search.png)

5. В панели результатов hello выберите **BlueJeans**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в BlueJeans с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в BlueJeans является tooa в Azure AD. Другими словами связи между пользователя Azure AD и hello связанных пользователей в BlueJeans должен установить toobe.

В BlueJeans, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с BlueJeans, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя BlueJeans](#creating-a-bluejeans-test-user)**  -toohave аналог Саймон Britta в BlueJeans, представление связанных toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в BlueJeans приложения.

**tooconfigure Azure AD единого входа с BlueJeans, выполните следующие шаги hello.**

1. В hello в hello портала Azure **BlueJeans** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_samlbase.png)

3. На hello **URL-адреса и домена BlueJeans** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.BlueJeans.com`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.BlueJeans.com`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить значения hello фактический URL-адрес входа и идентификатор. Обратитесь к [группа поддержки клиента BlueJeans](https://support.bluejeans.com/contact) tooget эти значения. 
 
4. На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-bluejeans-tutorial/tutorial_general_400.png)

6. На hello **конфигурации BlueJeans** щелкните **Настройка BlueJeans** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода, URL-адрес изменения пароля и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_configure.png) 

7. В другом окне браузера, войдите в tooyour **BlueJeans** сайт компании от имени администратора.

8. Go слишком**АДМИНИСТРАТОРА \> параметры группы \> безопасности**.
   
   ![Администратор](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "Администратор")

9. В hello **безопасности** выполните следующие шаги hello:
   
   ![Единый вход SAML](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "Единый вход SAML")   
   
   а. Выберите параметр **SAML Single Sign On**(Единый вход SAML).
  
   b. Установите флажок **Enable automatic provisioning**(Включить автоматическую подготовку).

10. Продолжите и hello следующие шаги:

    ![Путь к сертификату](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "Путь к сертификату")
    
    а. Нажмите кнопку **выбрать файл**и затем передайте сертификат загружаются hello.
   
    b. Вставить **SAML единого входа URL-адрес службы** в hello **URL-адрес входа** текстового поля.
   
    c. Вставить **URL-адрес изменения пароля** в hello **URL-адрес изменения пароля** текстового поля.
   
    d. Вставить **URL-адрес выхода** в hello **URL-адрес выхода** текстового поля.

11. Продолжите и hello следующие шаги:
    
    ![Сохранение изменений](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "Сохранение изменений")
    
    а. В hello **идентификатор пользователя** введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.
   
    b. В hello **электронной почты** введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.
   
    c. Нажмите кнопку **Сохранить изменения**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-bluejeans-test-user"></a>Создание тестового пользователя BlueJeans

Пользователи toolog tooenable Azure AD в tooBlueJeans, их необходимо подготовить в BlueJeans.  

В случае BlueJeans подготовка выполняется вручную.

**tooprovision учетных записей пользователей, выполните следующие действия hello:**

1. Войдите в tooyour **BlueJeans** сайт компании от имени администратора.

2. Go слишком**АДМИНИСТРАТОРА \> Управление пользователями \> добавить пользователя**.
   
   ![Администратор](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "Администратор")
   
   >[!IMPORTANT]
   >Hello **добавить пользователя** вкладка доступна, только если в hello **вкладка "Безопасность"**, **включить автоматическую подготовку** снят. 
   
3. В hello **добавить пользователя** выполните следующие шаги hello:

    ![Добавление пользователя](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "Добавление пользователя")
    
    а. Введите значение **имя пользователя BlueJeans**, **адрес электронной почты**, **идентификатор собрания BlueJeans**, **секретный код модератора**, **полное имя** , hello **компании** из текстовых полей, связанных с действительной учетной записи AAD, которые должны tooprovision hello.
    
    b. Нажмите кнопку **Add User**(Добавить пользователя).

>[!NOTE]
>Можно использовать любые другие BlueJeans пользователя средства создания учетных записей или интерфейсы API, предоставляемые BlueJeans tooprovision учетных записей пользователей AAD. 
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooBlueJeans доступа.

![Назначение пользователя][200] 

**tooassign tooBlueJeans Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **BlueJeans**.

    ![Настройка единого входа](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки BlueJeans плитки в панели доступа hello приветствия, должно появиться страница входа BlueJeans приложения.
Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_203.png

