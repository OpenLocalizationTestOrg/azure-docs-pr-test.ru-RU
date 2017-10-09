---
title: "Учебник. Интеграция Azure Active Directory с Marketo | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Marketo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b88c45f5-d288-4717-835c-ca965add8735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 87f88cde4f027f99a83c1ab3b318247bb4d658ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-marketo"></a>Руководство. Интеграция Azure Active Directory с Marketo

В этом учебнике вы узнаете, как toointegrate Marketo с Azure Active Directory (Azure AD).

Интеграция Marketo с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooMarketo
- Можно включить на пользователей tooautomatically get вошедшего tooMarketo (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Marketo требуется hello следующих элементов:

- подписка Azure AD;
- подписка Marketo с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Marketo из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-marketo-from-hello-gallery"></a>Добавление Marketo из галереи hello
tooconfigure hello интеграции Marketo в Azure AD, вы должны tooadd Marketo из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Marketo из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Marketo**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_search.png)

5. В панели результатов hello выберите **Marketo**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Marketo для тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Marketo является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Marketo должен установить toobe.

В Marketo, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Marketo, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Marketo](#creating-a-marketo-test-user)**  -toohave аналог Саймон Britta в Marketo, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Marketo.

**tooconfigure Azure AD единого входа с Marketo, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Marketo** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_samlbase.png)

3. На hello **URL-адреса и домена Marketo** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_url.png)

    а. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://saml.marketo.com/sp`

    b. В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://login.marketo.com/saml/assertion/\<munchkinid\>`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновите эти значения с hello фактический идентификатор и ответ URL-адрес. Обратитесь к [Marketo поддержки](http://investors.marketo.com/contactus.cfm) tooget эти значения.
 
4. На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_general_400.png)

6. На hello **конфигурации Marketo** щелкните **Настройка Marketo** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_configure.png) 

7. tooget Munchkin идентификатор приложения, войдите в tooMarketo, используя учетные данные администратора и выполните следующие действия:
   
    а. Войдите в приложение tooMarketo, используя учетные данные администратора.
   
    b. Нажмите кнопку hello **администратора** кнопку на верхней панели навигации панели hello.
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    c. Перейдите в меню toohello интеграции и нажмите кнопку hello **Munchkin ссылку**.
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_11.png)
   
    d. Скопируйте hello Munchkin код на экране приветствия и завершения URL-адрес ответа в мастер настройки hello Azure AD.
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_12.png) 

8. hello tooconfigure единого входа в приложение hello выполните hello шаги, описанные ниже.
   
    а. Войдите в приложение tooMarketo, используя учетные данные администратора.
   
    b. Нажмите кнопку hello **администратора** кнопку на верхней панели навигации панели hello.
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    c. Перейдите в меню toohello интеграции и нажмите кнопку **Single Sign On**.
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_07.png) 
   
    d. Щелкните tooenable hello параметры SAML **изменить** кнопки.
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_08.png) 
   
    д. **Включите** параметры единого входа.
   
    f. Вставить hello **идентификатор сущности SAML**, в hello **ИД издателя** текстового поля.
   
    ж. В hello **идентификатор сущности** текстовом поле введите URL-адрес hello как `http://saml.marketo.com/sp`.
   
    h. Выберите hello местоположение идентификатора пользователя как **элемент идентификатора имени**.
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_09.png)
   
    > [!NOTE]
    > Если ваш идентификатор пользователя не значение имени участника-пользователя, а затем значение hello изменения на вкладке атрибут hello.
   
    i. Отправьте сертификат hello, который вы скачали из мастера настройки Azure AD. **Сохранить** hello параметры.
   
    j. Изменение параметров перенаправления страницы приветствия.
   
    k. Вставить hello **SAML единого входа URL-адрес службы** в hello **URL-адрес входа** текстового поля.
   
    l. Вставить hello **URL-адрес выхода** в hello **URL-адрес выхода** текстового поля.
   
    m. В hello **URL-адрес ошибки**, копия вашего **URL-адрес экземпляра Marketo** и нажмите кнопку **Сохранить** кнопку toosave параметры.
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_10.png)

9. tooenable hello единого входа для пользователей, завершения hello, следующие действия:
   
    а. Войдите в приложение tooMarketo, используя учетные данные администратора.
   
    b. Нажмите кнопку hello **администратора** кнопку на верхней панели навигации панели hello.
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    c. Перейдите toohello **безопасности** меню и выберите пункт **параметры входа**.
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_13.png)
   
    d. Проверьте hello **единого входа требуется** параметр и **Сохранить** hello параметры.
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_14.png)

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-marketo-test-user"></a>Создание тестового пользователя Marketo

В этом разделе описано, как создать пользователя Britta Simon в приложении Marketo. Выполните эти шаги toocreate пользователя на платформе Marketo.

1. Войдите в приложение tooMarketo, используя учетные данные администратора.

2. Нажмите кнопку hello **администратора** кнопку на верхней панели навигации панели hello.
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 

3. Перейдите toohello **безопасности** меню и выберите пункт **пользователей и ролей**
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_19.png)  

4. Нажмите кнопку hello **пригласить нового пользователя** ссылку на вкладку "пользователи" hello
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_15.png) 

5. В hello пригласить нового пользователя мастер заполнения hello следующую информацию
   
    а. Введите пользователя hello **электронной почты** адрес в текстовом поле hello
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_16.png)
   
    b. Введите hello **имя** в текстовом поле hello
   
    c. Введите hello **Фамилия** в текстовом поле hello
   
    d. Щелкните **Далее**

6. В hello **разрешений** вкладке, выберите hello **userRoles** и нажмите кнопку **Далее**
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_17.png)
7. Нажмите кнопку hello **отправки** кнопку toosend hello пользователю приглашение
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_18.png)

8. Пользователь получает уведомление по электронной почте hello и имеет hello tooclick ссылку и измените пароль tooactivate hello hello-учетной записи. 

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooMarketo доступа.

![Назначение пользователя][200] 

**tooassign tooMarketo Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Marketo**.

    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello Marketo плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Marketo приложения.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_203.png

