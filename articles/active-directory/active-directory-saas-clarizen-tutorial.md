---
title: "Учебник. Интеграция Azure Active Directory с Clarizen | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Clarizen."
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
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: f24ccda3b90e5df9a203a444dfda905043b30276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clarizen"></a>Руководство. Интеграция Azure Active Directory с Clarizen

В этом учебнике вы узнаете, как toointegrate Azure Active Directory (Azure AD) с Clarizen. Это интеграция дает hello следующие преимущества:

- Можно управлять, в Azure AD, кто имеет доступ tooClarizen.
- Вы можете включить вашей toobe пользователям автоматически входить в tooClarizen (единый вход) с помощью своих учетных записей Azure AD.
- Вы можете управлять учетными записями в одном централизованном месте hello портал Azure.

сценарий Hello в этом учебнике состоит из двух основных задач.

1. Добавление Clarizen из коллекции hello.
2. Настройка и проверка единого входа в Azure AD.

Дополнительные сведения об интеграции приложений SaaS с Azure AD см. в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования
tooconfigure интеграция Azure AD с Clarizen, необходимо hello следующих элементов:

- подписка Azure AD;
- подписка Clarizen с поддержкой единого входа.

tootest hello шаги в этом учебнике, придерживайтесь следующих рекомендаций:

- Проверьте единый вход Azure AD в тестовой среде. Не используйте рабочую среду без необходимости.
- Если у вас нет тестовой среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="add-clarizen-from-hello-gallery"></a>Добавление Clarizen из коллекции hello
tooconfigure интеграция Clarizen hello в Azure AD, добавить Clarizen из hello коллекции tooyour список управляемых приложений SaaS.

1. В hello [портал Azure](https://portal.azure.com)в левой области hello, щелкнув hello **Azure Active Directory** значок.

    ![Значок Azure Active Directory][1]

2. Щелкните **Корпоративные приложения**. Затем щелкните **Все приложения**.

    ![Выбор пунктов "Корпоративные приложения" и "Все приложения".][2]

3. Нажмите кнопку hello **добавить** кнопку вверху hello диалоговое окно «hello».

    ![Кнопка «Добавить» Hello][3]

4. Введите в поле поиска hello **Clarizen**.

    ![Введя «Clarizen» в поле поиска hello](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_000.png)

5. В области результатов hello, выберите **Clarizen**, а затем нажмите кнопку **добавить** tooadd приложения hello.

    ![При выборе Clarizen в области результатов hello](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_0001.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В следующих разделах hello Настройка и тестирование Azure AD единого входа на основе пользовательского теста hello Саймон Britta Clarizen.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Clarizen является tooa в Azure AD. Другими словами связи между пользователя Azure AD и hello связанных пользователей в Clarizen должен установить toobe. Установления этой связи, назначив значение hello **имя пользователя** в Azure AD в качестве значения hello **Username** в Clarizen.

tooconfigure и теста Azure AD единого входа с Clarizen завершения hello следующие стандартные блоки:

1. **[Настройка Azure AD единого входа](#configure-azure-ad-single-sign-on)**  tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Clarizen](#create-a-clarizen-test-user)**  toohave аналог Саймон Britta в Clarizen, представление связанных toohello Azure AD ей.
4. **[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#test-single-sign-on)**  tooverify ли hello works конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD
Включите Azure AD единым входом в портал Azure hello и настройки единого входа в вашем приложении Clarizen.

1. В hello в hello портала Azure **Clarizen** странице интеграции приложения щелкните **единого входа**.

    ![Выбор пункта "Единый вход"][4]

2. В hello **единого входа** диалоговом для **режим**выберите **входа на базе SAML** tooenable единого входа.

    ![Выбор параметра "Единый вход на основе SAML"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_01.png)

3. В hello **URL-адреса и домена Clarizen** выполните следующие шаги hello:

    ![Поля идентификатора и URL-адреса ответа](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_02.png)

    а. В hello **идентификатор** поле типа значение hello в виде: **Clarizen**

    b. В hello **URL-адрес ответа** введите URL-адрес, используя следующий шаблон hello: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**

    > [!NOTE]
    > Они не hello реальные значения. Фактический идентификатор toouse hello и URL-адрес ответа. Здесь мы рекомендуем использовать hello уникальное значение строки, так как идентификатор hello. фактические значения, обратитесь в службу hello hello tooget [Clarizen поддержки](https://success.clarizen.com/hc/en-us/requests/new).

4. На hello **сертификат подписи SAML** щелкните **Создание нового сертификата**.

    ![Нажатие кнопки "Создать новый сертификат"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_03.png)  

5. В hello **создать новый сертификат** диалоговое окно, щелкните значок календаря hello и выберите дату окончания действия. Нажмите кнопку **Сохранить**.

    ![Выбор и сохранение даты окончания действия](./media/active-directory-saas-clarizen-tutorial/tutorial_general_300.png)

6. В hello **сертификат подписи SAML** выберите **активировать новый сертификат**, а затем нажмите кнопку **Сохранить**.

    ![Установка флажка hello для создания нового сертификата hello active](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_04.png)

7. В hello **сертификат продолжения** диалоговое окно, нажмите кнопку **ОК**.

    ![Нажмите кнопку «ОК» tooconfirm требуется сертификат hello toomake active](./media/active-directory-saas-clarizen-tutorial/tutorial_general_400.png)

8. В hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Нажав кнопку загрузки hello toostart «Сертификат (Base64)»](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_05.png)

9. В hello **конфигурации Clarizen** щелкните **Настройка Clarizen** tooopen hello **Настройка входа** окна.

    ![Нажатие кнопки "Настроить Clarizen"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_06.png)

    ![Окно "Настройка единого входа" с файлами и URL-адресами](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_07.png)

10. В другом окне браузера Войдите на сайте компании tooyour Clarizen с правами администратора.

11. Щелкните свое имя пользователя и выберите пункт **Settings** (Параметры).

    ![Выбор пункта "Параметры" по именем пользователя](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "Параметры")

12. Нажмите кнопку hello **глобальные параметры** вкладки. Затем Далее слишком**федеративной проверки подлинности**, нажмите кнопку **изменить**.

    ![Вкладка "Глобальные параметры"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "Глобальные параметры")

13. В hello **федеративной проверки подлинности** диалогового окна выполните следующие шаги hello:

    ![Диалоговое окно "Федеративная проверка подлинности"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Федеративная проверка подлинности")

    а. Выберите **Enable Federated Authentication** (Включить федеративную проверку подлинности).

    b. Нажмите кнопку **отправить** tooupload загруженный сертификат.

    c. В hello **URL-адрес входа** введите значение hello **SAML единого входа URL-адрес службы** из окна конфигурации приложения hello Azure AD.

    d. В hello **URL-адрес выхода** введите значение hello **URL-адрес выхода** из окна конфигурации приложения hello Azure AD.

    д. Установите флаг **Использовать POST**.

    Е. Щелкните **Сохранить**.

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
В hello портал Azure Создание тестового пользователя вызывается Саймон Britta.

![Имя и адрес электронной почты пользователя теста hello Azure AD][100]

1. В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** значок.

    ![Значок Azure Active Directory](./media/active-directory-saas-clarizen-tutorial/create_aaduser_01.png)

2. Нажмите кнопку **пользователей и групп**, а затем нажмите кнопку **всех пользователей** toodisplay hello список пользователей.

    ![Выбор разделов "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_02.png)

3. Вверху hello диалоговое окно «hello», нажмите кнопку **добавить** tooopen hello **пользователя** диалоговое окно.

    ![Кнопка «Добавить» Hello](./media/active-directory-saas-clarizen-tutorial/create_aaduser_03.png)

4. В hello **пользователя** диалогового окна выполните следующие шаги hello:

    ![Диалоговое окно "Пользователь" с заполненными полями "Имя", "Адрес электронной почты" и "Пароль"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_04.png)

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** поле введите адрес электронной почты hello hello Саймон Britta учетной записи.

    c. Выберите **Показать пароль** и запишите значение hello **пароль**.

    d. Щелкните **Создать**.

### <a name="create-a-clarizen-test-user"></a>Создание тестового пользователя Clarizen
tooenable toosign пользователей Azure AD в tooClarizen, необходимо подготовить учетные записи пользователей. В случае hello объекта Clarizen Подготовка осуществляется вручную.

1. Войдите в tooyour Clarizen корпоративный сайт с правами администратора.

2. Выберите параметр **Пользователи**.

    ![Выберите пункт People (Пользователи)](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "Пользователи")

3. Нажмите кнопку **Пригласить пользователя**.

    ![Кнопка Invite User](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "Пригласить пользователя")

4. В hello **пригласить пользователя** диалогового окна выполните следующие шаги hello:

    ![Диалоговое окно Invite People](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "Приглашение пользователей")

    а. В hello **электронной почты** поле введите адрес электронной почты hello hello Саймон Britta учетной записи.

    b. Нажмите кнопку **Пригласить**.

    > [!NOTE]
    > Hello владельцем учетной записи Azure Active Directory получит сообщение электронной почты и выполните их учетных записей tooconfirm ссылку, чтобы она стала активной.

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя
Включите toouse Britta Simon Azure единого входа путем предоставления ее tooClarizen доступа.

![Назначение тестового пользователя][200]

1. На hello портал Azure, откройте представление приложения hello, Обзор toohello представления каталога, **корпоративных приложений**, а затем нажмите кнопку **все приложения**.

    ![Выбор пунктов "Корпоративные приложения" и "Все приложения".][201]

2. В списке приложений hello выберите **Clarizen**.

    ![При выборе Clarizen в списке hello](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_50.png)

3. Hello левой панели щелкните **пользователей и групп**.

    ![Выбор пункта "Пользователи и группы"][202]

4. Нажмите кнопку hello **добавить** кнопки. Затем в hello **добавить назначение** выберите **пользователей и групп**.

    ![Кнопка «Добавить» Hello и диалоговое окно «Добавление назначения» hello][203]

5. В hello **пользователей и групп** выберите **Britta Simon** hello списка пользователей.

6. В hello **пользователей и групп** диалоговое окно, нажмите кнопку hello **выберите** кнопки.

7. В hello **добавить назначение** диалоговое окно, нажмите кнопку hello **назначить** кнопки.

### <a name="test-single-sign-on"></a>Проверка единого входа
Тестирование конфигурации Azure AD единого входа с помощью панели доступа hello.

Если щелкнуть плитку Clarizen hello в hello панели доступа, вы должны автоматически входить в tooyour Clarizen приложения.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по toointegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_203.png
