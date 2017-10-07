---
title: "Руководство. Интеграция Azure Active Directory с Citrix ShareFile | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Citrix ShareFile."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: e14fc310-bac4-4f09-99ef-87e5c77288b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2017
ms.author: jeedes
ms.openlocfilehash: d7eaf140e56c40f9f621062849dd8558588ffd1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-sharefile"></a>Руководство. Интеграция Azure Active Directory с Citrix ShareFile

В этом учебнике вы узнаете, как toointegrate Citrix ShareFile с Azure Active Directory (Azure AD).

Интеграция Citrix ShareFile с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooCitrix ShareFile.
- Можно включить на пользователей tooautomatically get вошедшего tooCitrix ShareFile (Single Sign-On) с помощью своих учетных записей Azure AD.
- Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Citrix ShareFile требуется hello следующих элементов:

- подписка Azure AD;
- подписка Citrix ShareFile с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Citrix ShareFile из коллекции hello
2. Настройка и проверка единого входа в Azure AD

## <a name="add-citrix-sharefile-from-hello-gallery"></a>Добавление Citrix ShareFile из коллекции hello
tooconfigure hello интеграции Citrix ShareFile в Azure AD, вы должны tooadd Citrix ShareFile из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Citrix ShareFile из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Кнопка Hello Azure Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Hello корпоративных приложений колонку][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Кнопка нового приложения Hello][3]

4. Введите в поле поиска hello **Citrix ShareFile**выберите **Citrix ShareFile** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.

    ![Список результатов Citrix ShareFile в hello](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе описана настройка и проверка единого входа Azure AD в Citrix ShareFile с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Citrix ShareFile является tooa в Azure AD. Другими словами связи между пользователя Azure AD и hello связанных пользователей в Citrix ShareFile должен установить toobe.

В Citrix ShareFile, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Citrix ShareFile, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Citrix ShareFile](#create-a-citrix-sharefile-test-user)**  -toohave аналог Саймон Britta в Citrix ShareFile, который представляет связанный toohello Azure AD пользователя.
4. **[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе вы включите Azure AD единым входом в портал Azure hello и настроить единый вход в приложение Citrix ShareFile.

**tooconfigure Azure AD единого входа с Citrix ShareFile, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Citrix ShareFile** странице интеграции приложения щелкните **единого входа**.

    ![Ссылка "Настройка единого входа"][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_samlbase.png)

3. На hello **URL-адреса и домена Citrix ShareFile** выполните следующие шаги hello:

    ![Сведения о домене и URL-адресах единого входа приложения Citrix ShareFile](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_url.png)
    
    В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenant-name>.sharefile.com/saml/login`

    > [!NOTE] 
    > Это значение приведено для справки. Измените значение этого параметра hello фактический URL-адрес входа. Обратитесь к [группа поддержки клиента Citrix ShareFile](https://www.citrix.co.in/products/sharefile/support.html) tooget это значение. 

4. На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-sharefile-tutorial/tutorial_general_400.png)

6. На hello **конфигурации Citrix ShareFile** щелкните **Настройка Citrix ShareFile** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка Citrix ShareFile](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_configure.png) 

7. В другом окне веб-браузера войдите на свой корпоративный веб-сайт **Citrix ShareFile** в качестве администратора.

8. Щелкните hello панели инструментов в верхней части hello **администратора**.

9. В области навигации слева hello выберите **настройки единого входа**.
   
    ![Администрирование учетной записи](./media/active-directory-saas-sharefile-tutorial/ic773627.png "Администрирование учетной записи")

10. На hello **единого входа и конфигурации SAML 2.0** в разделе **основные параметры**, выполните следующие шаги hello:
   
    ![Единый вход](./media/active-directory-saas-sharefile-tutorial/ic773628.png "Единый вход")
   
    а. Выберите команду **Enable SAML**(Включить SAML).
    
    b. В **издатель IDP / идентификатор сущности** текстовое значение hello вставить **идентификатор сущности SAML** скопирован из портала Azure.

    c. Нажмите кнопку **изменений** Далее toohello **сертификат X.509** поле, а затем отправить hello сертификат, загруженный из hello портал Azure.
    
    d. В **URL-адрес входа** текстовое значение hello вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure.
    
    д. В **URL-адрес выхода** текстовое значение hello вставить **URL-адрес выхода** скопирован из портала Azure.

11. Нажмите кнопку **Сохранить** на портале управления Citrix ShareFile hello.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

   ![Создание тестового пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-sharefile-tutorial/create_aaduser_01.png)

2. слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-sharefile-tutorial/create_aaduser_02.png)

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-sharefile-tutorial/create_aaduser_03.png)

4. В hello **пользователя** диалогового окна выполните следующие шаги hello:

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-sharefile-tutorial/create_aaduser_04.png)

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.

    c. Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.

    d. Щелкните **Создать**.
 
### <a name="create-a-citrix-sharefile-test-user"></a>Создание тестового пользователя Citrix ShareFile

В порядке tooenable toolog пользователей Azure AD в Citrix ShareFile их необходимо подготовить в Citrix ShareFile. В случае hello объекта Citrix ShareFile Подготовка выполняется вручную.

**tooprovision учетной записи пользователя, выполните следующие шаги hello.**

1. Войдите в tooyour **Citrix ShareFile** клиента.

2. Последовательно выберите пункты **Manage Users \> Manage Users Home \> + Create Employee** (Управление пользователями > Управление домашним ресурсом пользователей > + Создать сотрудника).
   
   ![Создание сотрудника](./media/active-directory-saas-sharefile-tutorial/IC781050.png "Создание сотрудника")

3. На hello **основные сведения** выполните следующие действия:
   
   ![Основные сведения](./media/active-directory-saas-sharefile-tutorial/IC799951.png "Основные сведения")
   
   а. В hello **адрес электронной почты** в текстовое поле введите адрес электронной почты hello Саймон Britta как  **brittasimon@contoso.com** .
   
   b. В hello **имя** введите **имя** пользователя как **Britta**.
   
   c. В hello **Фамилия** введите **Фамилия** пользователя как **Simon**.

4. Нажмите кнопку **Add User**(Добавить пользователя).
  
   >[!NOTE]
   >Владелец учетной записи Azure AD Hello получит сообщение электронной почты и выполните их учетных записей tooconfirm ссылку, чтобы она стала активной. Можно использовать любые другие Citrix ShareFile пользователя средства создания учетных записей или интерфейсы API, предоставляемые Citrix ShareFile tooprovision учетных записей пользователей Azure AD.

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooCitrix ShareFile.

![Назначение пользователям ролей hello][200] 

**tooassign Britta Simon tooCitrix ShareFile, выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Citrix ShareFile**.

    ![Hello Citrix ShareFile ссылку в списке приложений hello](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_app.png)  

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Hello ссылку «Пользователи и группы»][202]

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![область назначения, добавьте Hello][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello Citrix ShareFile плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour приложение Citrix ShareFile.
Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_203.png

