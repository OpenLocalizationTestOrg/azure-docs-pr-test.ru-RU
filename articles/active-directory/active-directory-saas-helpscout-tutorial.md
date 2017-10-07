---
title: "Учебник. Интеграция Azure Active Directory с Help Scout | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и помочь Scout."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0aad9910-0bc1-4394-9f73-267cf39973ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: jeedes
ms.openlocfilehash: 58edd140eb1eb5980796ca743b5f7acd891729a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-help-scout"></a>Учебник. Интеграция Azure Active Directory с Help Scout

В этом учебнике вы узнаете, как toointegrate помочь агент с Azure Active Directory (Azure AD).

Вы получаете следующие преимущества от интеграции с Azure AD помогают Scout hello:

- В Azure AD можно контролировать, кто имеет доступ tooHelp Scout.
- Можно автоматически войти вашей пользователей tooHelp Scout с помощью единого входа и учетная запись пользователя Azure AD.
- Вы можете управлять учетными записями в один, централизованно, hello портал Azure.

toolearn Дополнительные сведения о программное обеспечение как услуга (SaaS) интеграции приложений с Azure AD, в разделе [доступ к приложению и единый вход в Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooset интеграции с Azure AD с Scout справки требуется hello следующих элементов:

- подписка Azure AD;
- подписка Help Scout с включенным единым входом. 

> [!NOTE]
> Если вы тестируете hello шаги в этом учебнике, мы рекомендуем не проверяют их в рабочей среде.

Рекомендации для тестирования hello шаги в этом учебнике.

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить бесплатную пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. 

Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление справки Scout из коллекции hello.
2. Настройка и проверка единого входа Azure AD.

## <a name="add-help-scout-from-hello-gallery"></a>Добавление справки Scout из коллекции hello
tooset копирование hello интеграция справки Scout с Azure AD в галерее hello, добавление справки Scout tooyour список управляемых приложений SaaS.

tooadd Scout справки из галереи hello:

1. В hello [портал Azure](https://portal.azure.com)в левом меню hello, выберите **Azure Active Directory**. 

    ![Кнопка Hello Azure Active Directory][1]

2. Перейдите в колонку **Корпоративные приложения** и выберите **Все приложения**.

    ![страница приложений корпоративного Hello][2]
    
3. Выберите новое приложение tooadd **новое приложение**.

    ![Кнопка нового приложения Hello][3]

4. Введите в поле поиска hello, **Scout справки**. В результатах поиска hello, выберите **справки Scout**, а затем выберите **добавить**.

    ![Справка Scout в списке результатов hello](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_addfromgallery.png)

## <a name="set-up-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа Azure AD

В этом разделе описана настройка и проверка единого входа Azure AD в Help Scout с использованием тестового имени пользователя *Britta Simon*.

Для единого входа toowork Azure AD необходима пользователя Azure AD аналог tooknow hello в Scout справки. Связи между пользователя Azure AD и связанных пользователей hello в справке Scout должно быть установлено.

tooestablish hello ссылка связи в Scout справки, **Username**, присвойте значение hello hello **имя пользователя** в Azure AD.

tooconfigure и теста Azure AD единого входа с Scout справки, полный hello следующие задачи:

1. [Настройка единого входа Azure AD](#set-up-azure-ad-single-sign-on) Настраивает эту функцию toouse пользователя.
2. [Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user) Тесты Azure AD единого входа с пользователем hello Саймон Britta.
3. [Создание тестового пользователя Help Scout](#create-a-help-scout-test-user) Создает аналог Саймон Britta Scout справки, связанный toohello представление hello пользователя Azure AD.
4. [Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user). Устанавливает toouse Britta Simon Azure AD единого входа.
5. [Проверка единого входа](#test-single-sign-on) Подтверждает, что эта конфигурация hello работает.

### <a name="set-up-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе можно настроить Azure AD единым входом в портал Azure hello. а затем настроите его в приложении Help Scout.

tooset копирование Azure AD единого входа с Scout справки:

1. В hello в hello портала Azure **справки Scout** странице интеграции приложений выберите **единого входа**.
 
    ![Ссылка "Настройка единого входа"][4]

2. На hello **единого входа** страницы, для **режим**выберите **входа на базе SAML**.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_samlbase.png)

3. В разделе **URL-адреса и помочь домена Scout**, если требуется tooset приложения hello в режиме инициированный IDP, полный hello, следующие шаги:

    1. В hello **идентификатор** введите URL-адрес, имеющий hello следующий шаблон:`urn:auth0:helpscout:<instancename>`

    2. В hello **URL-адрес ответа** введите URL-адрес, имеющий hello следующий шаблон:`https://helpscout.auth0.com/login/callback?connection=<instancename>`

    ![Сведения о домене и URL-адресах единого входа приложения Help Scout](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url.png)

4. Tooset приложения hello в режиме, инициированные SP, установите hello **Показывать дополнительные параметры URL-адреса** флажок, а затем hello следующие:

    * В hello **URL-адрес входа** введите URL-адрес, имеющий следующий формат hello:`https://secure.helpscout.net/members/login/`

    ![Сведения о домене и URL-адресах единого входа приложения Help Scout](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url1.png)
 
    > [!NOTE] 
    > значения Hello в эти URL-адреса являются исключительно для демонстрационных целей. Обновление значений hello hello фактический идентификатор URL-адреса и URL-адрес ответа. обратитесь в службу tooget эти значения [Scout помочь группе поддержки](mailto:help@helpscout.com). 

5. В разделе **сертификат подписи SAML**выберите **метаданные в формате XML**и затем сохраните файл метаданных hello на вашем компьютере.

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_certificate.png) 

6. Щелкните **Сохранить**.

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-helpscout-tutorial/tutorial_general_400.png)
    
7. tooset копирование одного входа на стороне справки Scout hello, отправлять hello загружены метаданные XML файл toohello [Scout помочь группе поддержки](mailto:help@helpscout.com). Группа поддержки справки Scout Hello применяется этот параметр, чтобы правильно настроенной hello SAML единого входа для соединения с обеих сторон.

> [!TIP]
> Можно прочитать краткое версии этих инструкций в hello [портал Azure](https://portal.azure.com), тогда как при настройке приложения! После добавления приложения hello, выбрав **Active Directory** > **корпоративных приложений**выберите hello **Single Sign-On** вкладки. Можно получить доступ к документации hello внедрены в hello **конфигурации** раздел hello нижней части страницы приветствия. Чтобы узнать больше, ознакомьтесь со [встроенной документацией по Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

В этом разделе в hello портал Azure Создание тестового пользователя с именем Саймон Britta.

![Создание тестового пользователя Azure AD][100]

toocreate тестового пользователя в Azure AD:

1. В hello в левом меню hello, портале Azure выберите **Azure Active Directory**.

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-helpscout-tutorial/create_aaduser_01.png)

2. toodisplay hello список пользователей, выберите **пользователей и групп**, а затем выберите **всех пользователей**.

    ![Выбор элементов "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-helpscout-tutorial/create_aaduser_02.png)

3. tooopen hello **пользователя** диалоговом вверху hello hello **всех пользователей** выберите **добавить**.

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-helpscout-tutorial/create_aaduser_03.png)

4. В hello **пользователя** диалоговое окно, полный hello, следующие шаги:

    1. В hello **имя** введите **BrittaSimon**.

    2. В hello **имя пользователя** введите электронный адрес пользователя Саймон Britta hello.

    3. Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.

    4. Нажмите кнопку **Создать**.

        ![диалоговое окно приветствия пользователя](./media/active-directory-saas-helpscout-tutorial/create_aaduser_04.png)

 
### <a name="create-a-help-scout-test-user"></a>Создание тестового пользователя Help Scout

Hello объекта этого раздела — toocreate пользователя с именем Саймон Britta в Scout справки. Help Scout поддерживает JIT-подготовку. Эта функция включена по умолчанию.

В этом разделе нет не toocomplete действие или задача. Если пользователь еще не существует в Scout справки, новый создается при попытке tooaccess Scout справки.

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе позволяют hello пользователя Britta Simon toouse Azure AD единого входа путем предоставления hello пользователя учетной записи доступа к tooHelp Scout.

![Назначение пользователям ролей hello][200] 

tooassign tooHelp Britta Simon Scout:

1. В hello портал Azure откройте представление приложения hello, а затем перейдите toohello представления каталога. Перейдите в колонку **Корпоративные приложения** и выберите **Все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Scout справки**.

    ![ссылку справки Scout Hello в списке приложений hello](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_app.png)  

3. Выберите в меню слева hello, **пользователей и групп**.

    ![Hello пользователей и групп каналу][202]

4. Выберите **Добавить**. Затем на hello **добавить назначение** выберите **пользователей и групп**.

    ![область назначения, добавьте Hello][203]

5. На hello **пользователей и групп** страницы в список пользователей, выберите hello **Britta Simon**.

6. На hello **пользователей и групп** выберите **выберите**.

7. На hello **добавить назначение** выберите **назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При выборе плитки помогают Scout hello в панель доступа hello вы должны автоматически входить в tooyour Scout справки приложения.

Дополнительные сведения о панели доступа см. в разделе [панели доступа введение toohello](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по toointegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_203.png

