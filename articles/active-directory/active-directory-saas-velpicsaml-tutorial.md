---
title: "Руководство по интеграции Azure Active Directory с Velpic SAML | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Velpic SAML."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 613947d8fe95113382a2cdc0f79ce9eda85a0127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-velpic-saml"></a>Руководство. Интеграция Azure Active Directory с Velpic SAML

В этом учебнике вы узнаете, как toointegrate Velpic SAML в Azure Active Directory (Azure AD).

Интеграция с Azure AD Velpic SAML предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooVelpic SAML
- Можно включить на пользователей tooautomatically get вошедшего tooVelpic SAML (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал управления Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Velpic SAML требуется hello следующих элементов:

- подписка Azure AD;
- подписка на приложение Velpic SAML с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не следует использовать рабочую среду при отсутствии необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Velpic SAML из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-velpic-saml-from-hello-gallery"></a>Добавление Velpic SAML из галереи hello
tooconfigure hello интеграции Velpic SAML в Azure AD, вы должны tooadd Velpic SAML из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Velpic SAML из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портала управления Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".

    ![Приложения][3]

4. Введите в поле поиска hello **Velpic SAML**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_search.png)

5. В панели результатов hello выберите **Velpic SAML**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Velpic SAML с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Velpic SAML является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Velpic SAML должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Velpic SAML.

tooconfigure и теста Azure AD единого входа с Velpic SAML, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Velpic SAML](#creating-a-velpic-saml-test-user)**  -toohave аналог Саймон Britta в Velpic SAML, представление связанных toohello Azure AD ей.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал управления Azure hello и настройки единого входа в приложении Velpic SAML.

**tooconfigure Azure AD единого входа с Velpic SAML, выполните следующие шаги hello.**

1. На портале управления Azure hello на hello **Velpic SAML** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна, как **режим** выберите **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_samlbase.png)

3. Введите сведения hello в hello **URL-адреса и домена SAML Velpic** раздел -

    ![Настройка единого входа](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_url.png)

    а. В hello **URL-адрес входа** текстовое поле, значение типа hello как:`https://<sub-domain>.velpicsaml.net`

    b. В hello **идентификатор** текстовое поле, вставить hello **«Единый вход на URL-адрес»** значение`https://auth.velpic.com/saml/v2/<entity-id>/login`
    
    > [!NOTE]
    > Обратите внимание, что hello URL-адрес входа будут предоставляться hello team Velpic SAML и значение идентификатора, будут доступны при настройке hello надстройки SSO на ОСНОВЕ Velpic SAML стороны. Необходимо toocopy, от Velpic SAML страницы приложения и вставьте его здесь.

4. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.

    ![Настройка единого входа](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_400.png)

6. На hello раздел конфигурации Velpic SAML нажмите кнопку настроить SAML Velpic tooopen Настройка единого входа окна. Скопируйте идентификатор сущности SAML hello из hello краткий справочник.

7. В другом окне веб-браузера войдите на корпоративный сайт Velpic SAML с правами администратора.

8. Щелкните **управление** вкладку и перейти слишком**интеграции** раздел, где требуется tooclick на **подключаемые модули** кнопку toocreate нового подключаемого модуля для входа в систему.

    ![Подключаемый модуль](./media/active-directory-saas-velpicsaml-tutorial/velpic_1.png)

9. Щелкните hello **«Добавить подключаемый модуль»** кнопки.
    
    ![Подключаемый модуль](./media/active-directory-saas-velpicsaml-tutorial/velpic_2.png)

10. Щелкните hello **SAML** плитку на странице приветствия добавить подключаемый модуль.
    
    ![Подключаемый модуль](./media/active-directory-saas-velpicsaml-tutorial/velpic_3.png)

11. Введите имя hello hello нового подключаемого модуля SAML и нажмите кнопку hello **«Add»** кнопки.

    ![Подключаемый модуль](./media/active-directory-saas-velpicsaml-tutorial/velpic_4.png)

12. Введите сведения о hello следующим образом:

    ![Подключаемый модуль](./media/active-directory-saas-velpicsaml-tutorial/velpic_5.png)

    а. В hello **имя** текстовое поле, имя типа hello SAML подключаемого модуля.

    b. В hello **URL-адрес издателя** текстовое поле, вставить hello **идентификатор сущности SAML** копируются hello **Настройка входа** окно hello портал Azure.

    c. В hello **конфигурации поставщика метаданных** отправить hello файл метаданные в формате XML, который был загружен с портала Azure.

    d. Вы также можете tooenable SAML на время подготовки, включив hello **«Автоматическое создание новых пользователей»** флажок. Если этот флаг не включен, пользователь не существует в Velpic, произойдет ошибка входа hello из Azure. Если флаг hello не включена hello пользователя будет автоматически подготовить в Velpic во время hello имени входа. 

    д. Копировать hello **единый вход на URL-адрес** из hello текстовое поле и вставить его в hello портал Azure.
    
    f. Щелкните **Сохранить**.

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя на портале управления Azure hello, вызывается Саймон Britta.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал управления Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_01.png) 

2. Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_02.png) 

3. Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-velpic-saml-test-user"></a>Создание тестового пользователя Velpic SAML

Этот шаг необязателен обычно как приложение hello поддерживает только в время подготовки пользователей. Hello автоматическую подготовку пользователя не включено Создание пользователя вручную можно сделать, как описано ниже.

Войдите на корпоративный сайт Velpic SAML с правами администратора и выполните следующие действия.
    
1. Выберите вкладку "Управление" и перейдите tooUsers раздела, затем щелкните на новых пользователей tooadd кнопки.

    ![добавить пользователя](./media/active-directory-saas-velpicsaml-tutorial/velpic_7.png)

2. На hello **«Создать нового пользователя»** диалогового окна выполните следующие шаги hello.

    ![user](./media/active-directory-saas-velpicsaml-tutorial/velpic_8.png)
    
    а. В hello **имя** текстовое поле, имя первого типа hello Саймон Britta.

    b. В hello **Фамилия** текстового поля, типа hello Фамилия Саймон Britta.

    c. В hello **имя пользователя** текстовом поле введите имя пользователя hello объекта Саймон Britta.

    d. В hello **электронной почты** текстовом поле введите адрес электронной почты hello Саймон Britta учетной записи.

    д. Остальные сведения hello является необязательным, можно заполнить его при необходимости.
    
    f. Щелкните **СОХРАНИТЬ**.  

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа, предоставляя свой доступ tooVelpic SAML.

![Назначение пользователя][200] 

**tooassign tooVelpic Britta Simon SAML, выполните hello следующие шаги.**

1. На портале управления Azure hello, открыть представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Velpic SAML**.

    ![Настройка единого входа](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

1. При нажатии кнопки hello Velpic SAML плитки в панели доступа hello, должно появиться страница входа Velpic SAML приложения. Вы увидите hello **«Войти с Azure AD»** кнопку на страницу входа hello.

    ![Подключаемый модуль](./media/active-directory-saas-velpicsaml-tutorial/velpic_6.png)

2. Щелкните hello **«Войти с Azure AD»** toolog кнопки в tooVelpic с помощью учетной записи Azure AD.


## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_203.png

