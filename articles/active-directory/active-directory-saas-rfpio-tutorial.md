---
title: "Руководство по интеграции Azure Active Directory с RFPIO | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и RFPIO."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 87187076-7b50-4247-814f-f217b052703f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: e0c692276276edd8f859e73d81cf54d75a65957a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rfpio"></a>Руководство по интеграции Azure Active Directory с RFPIO

В этом учебнике вы узнаете, как toointegrate RFPIO с Azure Active Directory (Azure AD).

Интеграция с Azure AD RFPIO предоставляет hello следующие преимущества:

- Позволяет контролировать в Azure AD, имеющего доступ tooRFPIO.
- Можно включить на пользователей tooautomatically get вошедшего tooRFPIO (Single Sign-On) с помощью своих учетных записей Azure AD.
- Вы можете управлять учетными записями в одном централизованном месте--hello портал Azure.

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с RFPIO требуется hello следующих элементов:

- подписка Azure AD;
- подписка RFPIO с поддержкой единого входа.

> [!NOTE]
> Не рекомендуется использовать в этом учебнике шаги hello tootest в рабочей среде.

tootest hello шаги в этом учебнике, придерживайтесь следующих рекомендаций:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. сценарий Hello, описанные в этом учебнике состоит из двух основных компонентов.

1. Добавление RFPIO из галереи hello.
2. Настройка и проверка единого входа Azure AD.

## <a name="add-rfpio-from-hello-gallery"></a>Добавление RFPIO из коллекции hello
tooconfigure hello интеграции RFPIO в Azure AD, вы должны tooadd RFPIO из списка tooyour коллекции hello управляемых приложений SaaS.

### <a name="tooadd-rfpio-from-hello-gallery"></a>tooadd RFPIO из галереи hello

1. В hello  **[портал Azure](https://portal.azure.com)**, на левой панели навигации hello, выберите hello **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в колонку **Корпоративные приложения** и выберите **Все приложения**.

    ![Приложения][2]
    
3. tooadd нового приложения, выберите hello **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **RFPIO**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_search.png)

5. Hello панели результатов выберите **RFPIO**, а затем выберите hello **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в приложение RFPIO с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow какие hello отношение установлено между пользователя аналога в RFPIO и пользователя в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в RFPIO должен установить toobe.

В RFPIO, присвойте значение hello **имя пользователя** в Azure AD в качестве значения hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с RFPIO, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**--tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**--tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя RFPIO](#creating-a-rfpio-test-user)**  --toohave аналог Саймон Britta в RFPIO, который представляет связанный toohello Azure AD пользователя.
4. **[Назначить hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**--tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  tooverify--Если конфигурация hello работает.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении RFPIO.

**tooconfigure Azure AD единого входа с RFPIO, выполните следующие шаги hello.**

1. В hello в hello портала Azure **RFPIO** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_samlbase.png)

3. На hello **RFPIO доменов и URL-адреса** статьи, при желании tooconfigure приложения hello в **IDP** инициировал режим:

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url.png)

    а. В hello **идентификатор** текстовом поле введите URL-адрес hello:`https://www.rfpio.com`

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url1.png)

    b. Установите флажок **Показать дополнительные параметры URL-адресов**,

    c. В hello **состояние ретрансляции** текстовом поле введите строковое значение. Обратитесь к [RFPIO поддержки](https://www.rfpio.com/contact/) tooget это значение. 

4. Установите флажок **Показать дополнительные параметры URL-адресов**, При необходимости приложение hello tooconfigure в **SP** инициировал режим:   

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url2.png)

    В hello **URL-адрес входа** текстовом поле введите URL-адрес hello:`https://www.app.rfpio.com`

5. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_certificate.png) 

6. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/tutorial_general_400.png)

7. В другом окне браузера, toohello входа **RFPIO** веб-сайта от имени администратора.

8. Щелкните раскрывающийся список левом углу нижней hello.

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/app1.png)

9. Щелкните hello **параметры организации**. 

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/app2.png)

10. Щелкните hello **функции и ИНТЕГРАЦИИ**.

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/app4.png)

11. В hello **Настройка единого входа SAML** щелкните **изменить**.

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/app3.png)

12. В этом разделе выполните следующие действия.

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/app5.png)
    
    а. Скопируйте содержимое hello hello **загружены метаданные в формате XML** и вставьте его в hello **конфигурацию удостоверения** поля.

    > [!NOTE]
    >загрузить содержимое hello toocopy **метаданные в формате XML** используйте **Notepad ++** или правильную **редактора XML**. 

    b. Щелкните **Проверить**.

    c. После нажатии кнопки **проверки**, зеркало **SAML(Enabled)** tooon.

    d. Нажмите кнопку **Submit**(Отправить).

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="create-a-rfpio-test-user"></a>Создание тестового пользователя RFPIO

Пользователи toolog tooenable Azure AD в tooRFPIO, их необходимо подготовить в RFPIO.  
В случае RFPIO hello Подготовка выполняется вручную.

**tooprovision учетной записи пользователя, выполните следующие шаги hello.**

1. Войдите в систему tooyour RFPIO сайт компании как администратор.

2. Щелкните раскрывающийся список левом углу нижней hello.

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/app1.png)

3. Щелкните hello **параметры организации**. 

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/app2.png)

4. Щелкните **TEAM MEMBERS** (Участники команды).

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/app6.png)

5. Щелкните **ADD MEMBERS** (Добавить участников).

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/app7.png)

6. В hello **добавить новые элементы** раздела. выполните следующие действия.

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/app8.png)

    а. Ввод **адрес электронной почты** в hello **введите один адрес электронной почты в строке** поля.

    b. Выберите **роль** в соответствии с требованиями.

    c. Щелкните **ADD MEMBERS** (Добавить участников).
        
    > [!NOTE]
    > Владелец учетной записи Azure Active Directory Hello получает сообщение электронной почты и соответствует tooconfirm ссылку свою учетную запись, чтобы она стала активной.

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooRFPIO доступа.

![Назначение пользователя][200] 

**tooassign tooRFPIO Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **RFPIO**.

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки RFPIO плитки в панели доступа hello hello, вы должны получить автоматически вошедшего tooyour RFPIO приложения.
Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников о том, как toointegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_203.png

