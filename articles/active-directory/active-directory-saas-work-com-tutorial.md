---
title: "Руководство. Интеграция Azure Active Directory с Work.com | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Work.com."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 98e6739e-eb24-46bd-9dd3-20b489839076
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: dcdc51c884abd78c945b649de99f942d32373cf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workcom"></a>Руководство. Интеграция Azure Active Directory с Work.com

В этом учебнике вы узнаете, как toointegrate Work.com с Azure Active Directory (Azure AD).

Интеграция Work.com с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooWork.com
- Можно включить на пользователей tooautomatically get вошедшего tooWork.com (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Work.com требуется hello следующих элементов:

- подписка Azure AD;
- Подписка Work.com с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Work.com из коллекции hello
2. Настройка и проверка единого входа в Azure AD

## <a name="add-workcom-from-hello-gallery"></a>Добавление Work.com из коллекции hello
tooconfigure hello интеграции Work.com в Azure AD, вы должны tooadd Work.com из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Work.com из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Work.com**выберите **Work.com** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.

    ![Добавление из коллекции](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Work.com с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Work.com является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Work.com должен установить toobe.

В Work.com, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Work.com, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Work.com](#create-a-workcom-test-user)**  -toohave аналог Саймон Britta в Work.com, который представляет связанный toohello Azure AD пользователя.
4. **[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложение Work.com.

>[!NOTE]
>tooconfigure единый вход, вы должны toosetup пользовательское имя домена Work.com еще. Требуется по крайней мере домена toodefine имя, проверить имя домена и развернуть ее tooyour всей организации.

**tooconfigure Azure AD единого входа с Work.com, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Work.com** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Параметр "Вход на основе SAML"](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_samlbase.png)

3. На hello **URL-адреса и домена Work.com** выполните hello следующее:

    ![Раздел "Домены и URL-адреса приложения Work.com"](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_url.png)

    В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`http://<companyname>.my.salesforce.com`

    > [!NOTE] 
    > Это значение приведено для справки. Измените значение этого параметра hello фактический URL-адрес входа. Обратитесь к [группа поддержки клиент Work.com](https://help.salesforce.com/articleView?id=000159855&type=3) tooget это значение. 

4. На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Раздел "Сертификат подписи SAML"](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить"](./media/active-directory-saas-work-com-tutorial/tutorial_general_400.png)

6. На hello **конфигурации Work.com** щелкните **Настройка Work.com** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Раздел "Настройка Work.com"](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_configure.png) 
7. Войдите в tooyour Work.com клиента от имени администратора.

8. Go слишком**установки**.
   
    ![Настройка](./media/active-directory-saas-work-com-tutorial/ic794108.png "Настройка")

9. На панели навигации слева hello в hello **Администрирование** щелкните **Управление доменами** tooexpand hello соответствующий раздел и нажмите кнопку **Мой домен** tooopen hello  **Мой домен** страницы. 
   
    ![Мой домен](./media/active-directory-saas-work-com-tutorial/ic767825.png "Мой домен")

10. tooverify, домен настроен неправильно, убедитесь, что он находится в "**шаг 4 развернут tooUsers**» и просмотрите вашей»**мои параметры домена**».
   
    ![Домен развернутые tooUser](./media/active-directory-saas-work-com-tutorial/ic784377.png "tooUser домена развертывания")

11. Войдите в систему tooyour Work.com клиента.

12. Go слишком**установки**.
    
    ![Настройка](./media/active-directory-saas-work-com-tutorial/ic794108.png "Настройка")

13. Разверните hello **управления безопасностью** меню, а затем нажмите **параметры единого входа**.
    
    ![Параметры единого входа](./media/active-directory-saas-work-com-tutorial/ic794113.png "Параметры единого входа")

14. На hello **параметры единого входа** диалогового окна выполните следующие шаги hello:
    
    ![Включение SAML](./media/active-directory-saas-work-com-tutorial/ic781026.png "Включение SAML")
    
    а. Установите флажок **SAML включен**.
    
    b. Нажмите кнопку **Создать**.

15. В hello **SAML единого входа параметры** выполните следующие шаги hello:
    
    ![Параметры единого входа SAML](./media/active-directory-saas-work-com-tutorial/ic794114.png "Параметры единого входа SAML")
    
    а. В hello **имя** текстовом поле введите имя для конфигурации.  
       
    > [!NOTE]
    > Предоставить значение для **имя** автоматически заполнять hello **имя API** текстового поля.
    
    b. В **издателя** текстовое значение hello вставить **идентификатор сущности SAML** скопирован из портала Azure.
    
    c. сертификат tooupload hello загружен из портала Azure щелкните **Обзор**.
    
    d. В hello **идентификатор сущности** введите `https://salesforce-work.com`.
    
    д. Как **типа удостоверения SAML**выберите **утверждение, содержащее hello идентификатор федерации из объекта пользователя hello**.
    
    f. Как **расположения удостоверения SAML**выберите **удостоверение находится в hello элемент NameIdentfier оператора Subject hello**.
    
    ж. В **URL-адрес входа поставщика удостоверений** текстовое значение hello вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure.

    h. В **URL-адрес выхода поставщика удостоверений** текстовое значение hello вставить **URL-адрес выхода** скопирован из портала Azure.
    
    i. В поле **Service Provider Initiated Request Binding** (Связывание запросов, инициированных поставщиком услуг) выберите значение **HTTP POST**.
    
    j. Щелкните **Сохранить**.

16. В классическом портала Work.com hello левой области навигации, выберите **Управление доменами** tooexpand hello соответствующий раздел и нажмите кнопку **Мой домен** tooopen hello **Мой домен**страницы. 
    
    ![Мой домен](./media/active-directory-saas-work-com-tutorial/ic794115.png "Мой домен")

17. На hello **Мой домен** страницы в hello **фирменная символика страницы входа** щелкните **изменить**.
    
    ![Фирменная символика страницы входа](./media/active-directory-saas-work-com-tutorial/ic767826.png "Фирменная символика страницы входа")

14. На hello **фирменная символика страницы входа** страницы в hello **службы проверки подлинности** раздела, название hello вашей **настройки единого входа SAML** отображается. Выберите его, а затем нажмите кнопку **Сохранить**.
    
    ![Фирменная символика страницы входа](./media/active-directory-saas-work-com-tutorial/ic784366.png "Фирменная символика страницы входа")

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-work-com-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Выберите "Пользователи и группы" > "Все пользователи".](./media/active-directory-saas-work-com-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Добавить](./media/active-directory-saas-work-com-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-work-com-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="create-a-workcom-test-user"></a>Создание тестового пользователя Work.com
Для Azure Active Directory пользователей toobe может toosign в они должны быть подготовленных tooWork.com. В случае hello Work.com Подготовка выполняется вручную.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure подготовки пользователей, выполните следующие шаги hello.
1. Войдите на tooyour сайт компании Work.com с правами администратора.

2. Go слишком**установки**.
   
    ![Настройка](./media/active-directory-saas-work-com-tutorial/IC794108.png "Настройка")
3. Go слишком**Управление пользователями \> пользователей**.
   
    ![Управление пользователями](./media/active-directory-saas-work-com-tutorial/IC784369.png "Управление пользователями")

4. Щелкните **Новый пользователь**.
   
    ![Все пользователи](./media/active-directory-saas-work-com-tutorial/IC794117.png "Все пользователи")

5. В hello пользователя изменить раздел, выполните следующие шаги в атрибутах допустимым Azure hello текстовые поля, связанные с учетной записью AD, которые должны tooprovision hello:
   
    ![Изменение пользователя](./media/active-directory-saas-work-com-tutorial/ic794118.png "Изменение пользователя")
   
    а. В hello **имя** в текстовое поле типа hello **имя** пользователя hello **Britta**.
    
    b. В hello **Фамилия** в текстовое поле типа hello **Фамилия** пользователя hello **Simon**.
    
    c. В hello **псевдоним** в текстовое поле типа hello **имя** пользователя hello **BrittaS**.
    
    d. В hello **электронной почты** в текстовое поле типа hello **адрес электронной почты** пользователя  **Brittasimon@contoso.com** .
    
    д. В hello **имя пользователя** текстовое поле, введите имя пользователя, например  **Brittasimon@contoso.com** .
    
    f. В hello **псевдоним** текстовом поле введите значение **псевдоним** пользователя **Simon**.
    
    ж. Выберите значения параметров **Role** (Роль), **User License** (Пользовательская лицензия) и **Profile** (Профиль).
    
    h. Щелкните **Сохранить**.  
      
    > [!NOTE]
    > Владелец учетной записи Hello Azure AD получит сообщение электронной почты, включая учетную запись hello tooconfirm ссылку, чтобы она стала активной.
    > 
    > 

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooWork.com доступа.

![Назначение пользователя][200] 

**tooassign tooWork.com Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Work.com**.

    ![Work.com в списке приложений](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello Work.com плитки в панели доступа hello, вы должны получить tooyour автоматически подписан в приложение Work.com.
Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_203.png

