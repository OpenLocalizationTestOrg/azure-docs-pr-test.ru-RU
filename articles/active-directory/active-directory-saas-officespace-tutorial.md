---
title: "Руководство по интеграции Azure Active Directory с OfficeSpace Software | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и OfficeSpace Software."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 95d8413f-db98-4e2c-8097-9142ef1af823
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: b53afb648b8a6057c32c782d857e34c06e152c67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-officespace-software"></a>Учебник. Интеграция Azure Active Directory с OfficeSpace Software

В этом учебнике вы узнаете, как toointegrate OfficeSpace Software с Azure Active Directory (Azure AD).

Интеграция OfficeSpace Software с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooOfficeSpace программного обеспечения.
- Можно включить на пользователей tooautomatically get вошедшего tooOfficeSpace программного обеспечения (Single Sign-On) с помощью своих учетных записей Azure AD.
- Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с OfficeSpace Software необходимо hello следующих элементов:

- подписка Azure AD;
- подписка OfficeSpace Software с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление OfficeSpace Software из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-officespace-software-from-hello-gallery"></a>Добавление OfficeSpace Software из галереи hello
tooconfigure hello интеграции OfficeSpace Software в Azure AD, вы должны tooadd OfficeSpace Software из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd OfficeSpace Software из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Кнопка Hello Azure Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Hello корпоративных приложений колонку][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Кнопка нового приложения Hello][3]

4. Введите в поле поиска hello **OfficeSpace Software**выберите **OfficeSpace Software** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.

    ![Список результатов OfficeSpace Software в hello](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе описана настройка и проверка единого входа Azure AD в OfficeSpace Software с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в OfficeSpace Software является tooa в Azure AD. Иными словами связи между пользователя Azure AD и связанных пользователей hello в OfficeSpace Software необходимо установить toobe.

В OfficeSpace Software, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с OfficeSpace Software, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя OfficeSpace Software](#create-a-officespace-software-test-user)**  -toohave аналог Саймон Britta в OfficeSpace Software, представление связанных toohello Azure AD пользователя.
4. **[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложение OfficeSpace Software.

**tooconfigure Azure AD единого входа с OfficeSpace Software, выполните следующие шаги hello.**

1. В hello в hello портала Azure **OfficeSpace Software** странице интеграции приложения щелкните **единого входа**.

    ![Ссылка "Настройка единого входа"][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_samlbase.png)

3. На hello **URL-адреса и домена программного обеспечения OfficeSpace** выполните следующие шаги hello:

    ![Сведения о домене и URL-адресах единого входа для приложения OfficeSpace Software](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.officespacesoftware.com/users/sign_in/saml`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`<company name>.officespacesoftware.com`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить значения hello фактический URL-адрес входа и идентификатор. Обратитесь к [OfficeSpace клиентское программное обеспечение поддержки](mailto:support@officespacesoftware.com) tooget эти значения. 

4. Приложение OfficeSpace Software ожидает утверждения SAML hello в определенном формате. Выполните настройку следующих утверждений для этого приложения hello. Вы можете управлять hello значения этих атрибутов из hello»**атрибуты пользователя**» на странице интеграции приложения. пример Hello следующий снимок экрана для этого.
    
    ![Настройка атрибута](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_attribute.png)

5. В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна выберите **user.mail** как **идентификатор пользователя** и для каждой строки показано в следующей таблице hello выполните следующие шаги hello.
    
    | Имя атрибута | Значение атрибута |
    | --- | --- |    
    | email | user.mail |
    | name | user.displayname |
    | first_name | user.givenname |
    | last_name | user.surname |

    а. Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.

    ![Настройка при добавлении ](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_04.png)

    ![Настройка атрибута](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_05.png)
    
    b. В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.
    
    c. Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.
    
    d. Нажмите кнопку **ОК**.
 
6. На hello **сертификат подписи SAML** раздел, hello копирования **ОТПЕЧАТОК** значение hello сертификата.

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_certificate.png) 

7. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-officespace-tutorial/tutorial_general_400.png)

8. На hello **конфигурации программного обеспечения OfficeSpace** щелкните **Настройка OfficeSpace Software** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Конфигурация OfficeSpace Software](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_configure.png) 

9. В другом окне веб-браузера войдите в свой клиент OfficeSpace Software в качестве администратора.

10. Go слишком**параметры** и нажмите кнопку **соединители**.

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_002.png)

11. Щелкните **SAML Authentication** (Аутентификация SAML).

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_003.png)

12. В hello **проверку подлинности SAML** выполните следующие шаги hello:

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_004.png)

    а. В hello **URL-адрес выхода поставщика** текстовое значение hello вставить **URL-адрес выхода** скопирован из портала Azure.

    b. В hello **URL-адрес назначения idp клиента** текстовое значение hello вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure.

    c. Вставить hello **отпечаток** значение, которое было скопировано из портала Azure в hello **отпечаток сертификата IDP клиента** текстового поля. 

    d. Нажмите кнопку **Сохранить параметры**.


> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

   ![Создание тестового пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-officespace-tutorial/create_aaduser_01.png)

2. слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-officespace-tutorial/create_aaduser_02.png)

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-officespace-tutorial/create_aaduser_03.png)

4. В hello **пользователя** диалогового окна выполните следующие шаги hello:

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-officespace-tutorial/create_aaduser_04.png)

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.

    c. Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.

    d. Щелкните **Создать**.
 
### <a name="create-a-officespace-software-test-user"></a>Создание тестового пользователя OfficeSpace Software

Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в OfficeSpace Software. Приложение OfficeSpace Software поддерживает JIT-подготовку. Эта функция включена по умолчанию.

В этом разделе никакие действия с вашей стороны не требуются. Новый пользователь создается во время попытки tooaccess OfficeSpace Software, если он еще не существует.

> [!NOTE]
> Если требуется toocreate пользователя вручную, необходимо tooContact [OfficeSpace Software поддержки](mailto:support@officespacesoftware.com).

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooOfficeSpace программного обеспечения.

![Назначение пользователям ролей hello][200] 

**tooassign tooOfficeSpace Britta Simon программное обеспечение, выполните hello следующие шаги.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **OfficeSpace Software**.

    ![Hello OfficeSpace Software ссылку в списке приложений hello](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_app.png)  

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Hello ссылку «Пользователи и группы»][202]

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![область назначения, добавьте Hello][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки OfficeSpace Software плитки в панели доступа hello hello, вы должны получить tooyour автоматически подписан в приложение OfficeSpace Software.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_203.png

