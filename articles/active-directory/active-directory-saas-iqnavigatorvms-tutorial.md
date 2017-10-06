---
title: "Руководство по интеграции Azure Active Directory c IQNavigator VMS | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и IQNavigator виртуальных МАШИН."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a8a09b25-dfa5-4c31-aea2-53bf1853b365
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 5a5a7dd3f427acfba2f0ae10552a7179db730118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-iqnavigator-vms"></a>Руководство по интеграции Azure Active Directory c IQNavigator VMS

В этом учебнике вы узнаете, как toointegrate IQNavigator виртуальные МАШИНЫ в Azure Active Directory (Azure AD).

Интеграция IQNavigator ВМ с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooIQNavigator виртуальные МАШИНЫ
- Можно включить на пользователей tooautomatically get вошедшего tooIQNavigator виртуальных МАШИН (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с виртуальными Машинами IQNavigator требуется hello следующих элементов:

- подписка Azure AD;
- подписка IQNavigator VMS с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление виртуальных МАШИН IQNavigator из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-iqnavigator-vms-from-hello-gallery"></a>Добавление виртуальных МАШИН IQNavigator из галереи hello
tooconfigure hello интеграция IQNavigator виртуальных машин в Azure AD, вы должны tooadd IQNavigator виртуальных МАШИН из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd IQNavigator ВМ из галереи hello выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **IQNavigator ВМ**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_search.png)

5. В панели результатов hello, выберите **виртуальные МАШИНЫ IQNavigator**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в IQNavigator VMS с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в виртуальных Машинах IQNavigator является tooa в Azure AD. Другими словами связи между пользователя Azure AD и hello связанных пользователей на виртуальных Машинах IQNavigator должен установить toobe.

На виртуальных Машинах IQNavigator, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и тестирования Azure AD единого входа с виртуальными Машинами IQNavigator, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя ВМ IQNavigator](#creating-a-iqnavigator-vms-test-user)**  -toohave аналог Саймон Britta в виртуальных Машинах IQNavigator, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении IQNavigator виртуальных МАШИН.

**tooconfigure Azure AD единый вход с виртуальной Машиной IQNavigator, выполните следующие шаги hello.**

1. В hello в hello портала Azure **виртуальные МАШИНЫ IQNavigator** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_samlbase.png)

3. На hello **URL-адреса и виртуальными Машинами домена IQNavigator** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_url.png)

    а. В hello **идентификатор** текстовом поле введите URL-адрес hello:`iqn.com`

    b. В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.iqnavigator.com/security/login?client_name=https://sts.window.net/<instance name>`

4. Проверьте **Показывать дополнительные параметры URL-адреса**, выполните следующий шаг hello:

    ![Настройка единого входа](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_url1.png)

    В hello **ретрансляции состояние** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.iqnavigator.com`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновите эти значения с фактическим URL-адрес ответа и ретрансляции состоянием hello. Обратитесь к [IQNavigator виртуальные МАШИНЫ клиента поддержки](https://www.beeline.com/iqn-product-support/) tooget эти значения. 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_400.png)

6. toogenerate hello **метаданные** URL-адрес, выполните следующие шаги hello:

    а. Щелкните **Регистрация приложений**.
    
    ![Настройка единого входа](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_appregistrations.png)
   
    b. Нажмите кнопку **конечные точки** tooopen **конечные точки** диалоговое окно.  
    
    ![Настройка единого входа](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_endpointicon.png)

    c. Нажмите кнопку toocopy hello копирования **документа МЕТАДАННЫХ ФЕДЕРАЦИИ** URL-адрес и вставьте его в Блокнот.
    
    ![Настройка единого входа](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_endpoint.png)
     
    d. Теперь перейдите на странице свойств toohello **IQNavigator ВМ** и копирования hello **идентификатор приложения** с помощью **копирования** кнопку и вставьте его в Блокнот.
 
    ![Настройка единого входа](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_appid.png)

    д. Создать hello **URL-адрес метаданных** с помощью hello следующий шаблон:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`

7. Значение идентификатора уникального пользователя hello ожидать приложению IQNavigator в утверждение идентификатора имени hello. Клиента можно сопоставить hello правильное значение для утверждения идентификатора имени hello. В этом случае мы сопоставленной hello пользователя. UserPrincipalName в целях демонстрации hello. Однако в соответствии с tooyour параметры организации следует сопоставить hello правильное значение для него.   

    ![Настройка единого входа](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_attribute.png)

8. На hello **конфигурации виртуальных МАШИН IQNavigator** щелкните **настроить виртуальные МАШИНЫ IQNavigator** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_configure.png) 

9. tooconfigure единого входа на **виртуальные МАШИНЫ IQNavigator** параллельно, необходимо toosend hello **URL-адрес метаданных**, **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** слишком [Группа поддержки виртуальных МАШИН IQNavigator](https://www.beeline.com/iqn-product-support/). Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-iqnavigator-vms-test-user"></a>Создание тестового пользователя IQNavigator VMS

Цель этого раздела Hello — toocreate пользователя с именем Britta Simon в виртуальных Машинах IQNavigator. Работать с [группа поддержки виртуальных МАШИН IQNavigator](https://www.beeline.com/iqn-product-support/) tooadd пользователей hello в hello виртуальные МАШИНЫ IQNavigator учетной записи.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooIQNavigator виртуальных МАШИН.

![Назначение пользователя][200] 

**tooassign tooIQNavigator Britta Simon виртуальных МАШИН, выполните hello следующие шаги.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **IQNavigator ВМ**.

    ![Настройка единого входа](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello виртуальные МАШИНЫ IQNavigator плитки в панели доступа hello, вы должны получить tooyour автоматически подписан на виртуальные МАШИНЫ IQNavigator приложения.
Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_203.png

