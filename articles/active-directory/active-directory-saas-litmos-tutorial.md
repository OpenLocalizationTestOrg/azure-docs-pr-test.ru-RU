---
title: "Учебник. Интеграция Azure Active Directory с Litmos | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Litmos."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: jeedes
ms.assetid: cfaae4bb-e8e5-41d1-ac88-8cc369653036
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 026fd10058760f2d63d185ef4aa9d7de3b82525e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-litmos"></a>Руководство по интеграции Azure Active Directory с Litmos

В этом учебнике вы узнаете, как toointegrate Litmos с Azure Active Directory (Azure AD).

Интеграция с Azure AD Litmos предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooLitmos.
- Можно включить на пользователей tooautomatically get вошедшего tooLitmos (Single Sign-On) с помощью своих учетных записей Azure AD.
- Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Litmos требуется hello следующих элементов:

- подписка Azure AD;
- подписка Litmos с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Litmos из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-litmos-from-hello-gallery"></a>Добавление Litmos из галереи hello
tooconfigure hello интеграции Litmos в Azure AD, вы должны tooadd Litmos из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Litmos из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Кнопка Hello Azure Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Hello корпоративных приложений колонку][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Кнопка нового приложения Hello][3]

4. Введите в поле поиска hello **Litmos**выберите **Litmos** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.

    ![Litmos в списке результатов hello](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе описана настройка и проверка единого входа Azure AD в Litmos с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Litmos является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Litmos должен установить toobe.

В Litmos, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Litmos, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Litmos](#create-a-litmos-test-user)**  -toohave аналог Саймон Britta в Litmos, который представляет связанный toohello Azure AD пользователя.
4. **[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Litmos.

**tooconfigure Azure AD единого входа с Litmos, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Litmos** странице интеграции приложения щелкните **единого входа**.

    ![Ссылка "Настройка единого входа"][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_samlbase.png)

3. На hello **URL-адреса и домена Litmos** выполните следующие шаги hello:

    ![Сведения о домене и URL-адресах единого входа приложения Litmos](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_url.png)

    а. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.litmos.com/account/Login`

    b. В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.litmos.com/integration/samllogin`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить эти значения hello фактический идентификатор и ответ по URL-адресу, которые рассматриваются далее в учебнике или контакт [Litmos поддержки](https://www.litmos.com/contact-us/) tooget эти значения.

4. На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_certificate.png)

5. В составе конфигурации hello требуется toocustomize hello **атрибутов токена SAML** Litmos приложения.

    ![Раздел "Атрибут"](./media/active-directory-saas-litmos-tutorial/tutorial_attribute.png)
           
    | Имя атрибута   | Значение атрибута |   
    | ---------------  | ----------------|
    | FirstName |user.givenname |
    | LastName  |user.surname |
    | Email |user.mail |

    а. Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.

    ![Добавление атрибута](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_04.png)

    ![Диалоговое окно "Добавление атрибута"](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_05.png)

    b. В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.

    c. Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.
    
    d. Нажмите кнопку **ОК**.     

6. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-litmos-tutorial/tutorial_general_400.png)

7. В другом окне браузера, сайт компании Litmos tooyour входа от имени администратора.

8. Hello hello левой панели навигации щелкните **учетные записи**.
   
    ![Раздел "Accounts" (Учетные записи) на стороне приложения][22] 

9. Нажмите кнопку hello **интеграции** вкладки.
   
    ![Вкладка "Integrations" (Интеграция)][23] 

10. На hello **интеграции** Перейдите вниз слишком**интеграции сторонних производителей**, а затем нажмите кнопку **SAML 2.0** вкладку.
   
    ![Раздел "SAML 2.0"][24] 

11. Скопируйте значение hello в **hello конечная точка SAML для litmos:** и вставьте его в hello **URL-адрес ответа** текстовое поле в hello **URL-адреса и домена Litmos** раздела на портале Azure. 
   
    ![Конечная точка SAML][26] 

12. В вашей **Litmos** приложения, выполните следующие шаги hello:
    
     ![Приложение Litmos][25] 
     
     а. Выберите команду **Enable SAML**(Включить SAML).
    
     b. Откройте сертификат в кодировке base-64 в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **сертификат X.509 SAML** текстового поля.
     
     c. Нажмите кнопку **Сохранить изменения**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

   ![Создание тестового пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-litmos-tutorial/create_aaduser_01.png)

2. слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-litmos-tutorial/create_aaduser_02.png)

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-litmos-tutorial/create_aaduser_03.png)

4. В hello **пользователя** диалогового окна выполните следующие шаги hello:

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-litmos-tutorial/create_aaduser_04.png)

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.

    c. Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.

    d. Щелкните **Создать**.
  
### <a name="create-a-litmos-test-user"></a>Создание тестового пользователя Litmos

Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в Litmos.  
Hello Litmos приложений поддерживает только времени подготовки. Это означает учетной записи пользователя автоматически создается при необходимости во время попытки tooaccess hello приложения с помощью панели доступа hello.

**toocreate пользователя с именем Саймон Britta в Litmos, выполните следующие шаги hello.**

1. В другом окне браузера, сайт компании Litmos tooyour входа от имени администратора.

2. Hello hello левой панели навигации щелкните **учетные записи**.
   
    ![Раздел "Accounts" (Учетные записи) на стороне приложения][22] 

3. Нажмите кнопку hello **интеграции** вкладки.
   
    ![Вкладка "Integrations" (Интеграция)][23] 

4. На hello **интеграции** Перейдите вниз слишком**интеграции сторонних производителей**, а затем нажмите кнопку **SAML 2.0** вкладку.
   
    ![SAML 2.0][24] 
    
5. Установите флажок **Autogenerate Users** (Автоматически создавать пользователей).
   
    ![Автоматическое создание пользователей][27] 

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooLitmos доступа.

![Назначение пользователям ролей hello][200] 

**tooassign tooLitmos Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Litmos**.

    ![ссылка Litmos Hello в списке приложений hello](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_app.png)  

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Hello ссылку «Пользователи и группы»][202]

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![область назначения, добавьте Hello][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".  

При нажатии кнопки Litmos плитки в панели доступа hello приветствия, вы должны получить автоматически вошедшего tooyour Litmos приложения. 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_04.png
[21]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_60.png
[22]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_61.png
[23]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_62.png
[24]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_63.png
[25]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_64.png
[26]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_65.png
[27]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_66.png

[100]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_203.png

