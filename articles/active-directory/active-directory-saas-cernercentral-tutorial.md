---
title: "Руководство по интеграции Azure Active Directory с Cerner Central | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и центр Cerner."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2bc549d-d286-4679-854e-bb67c62b0475
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 3493d180e8f229b7cd228769f780f10208114889
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cerner-central"></a>Руководство. Интеграция Azure Active Directory с Cerner Central

В этом учебнике вы узнаете, как toointegrate центральный Cerner с Azure Active Directory (Azure AD).

Интеграция с Azure AD центральный Cerner предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooCerner центральный
- Можно включить на пользователей tooautomatically get вошедшего tooCerner центральный (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с центрального Cerner требуется hello следующих элементов:

- подписка Azure AD;
- утвержденная системная учетная запись Cerner Central.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление центральный Cerner из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-cerner-central-from-hello-gallery"></a>Добавление центральный Cerner из галереи hello
tooconfigure hello интеграции центральный Cerner в Azure AD, вы должны tooadd центральный Cerner из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd центральный Cerner из галереи hello выполните hello следующие шаги.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопки на диалоговое окно приветствия.

    ![Приложения][3]

4. Введите в поле поиска hello **Cerner центральный**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_search.png)

5. В панели результатов hello выберите **центральный Cerner**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описаны настройка и проверка единого входа Azure AD в Cerner Central с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в центральный Cerner является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в центральный Cerner должен установить toobe.

tooconfigure и теста Azure AD единого входа с центрального Cerner, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя центральный Cerner](#creating-a-cerner-central-test-user)**  -toohave аналог Саймон Britta в центральный Cerner, являющийся представлением пользовательского hello связанного toohello Azure AD.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении центральный Cerner.

**tooconfigure Azure AD единого входа с центрального Cerner выполните следующие шаги hello.**

1. В hello в hello портала Azure **центральный Cerner** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_samlbase.png)

3. На hello **URL-адреса и домена центра Cerner** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_url.png)

    а. В hello **идентификатор** текстовое значение hello типа с помощью hello следующие шаблоны:
    
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcerner.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |

    b. В hello **URL-адрес ответа** текстовое поле, введите URL-адрес, используя hello следующие шаблоны: 
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/sso` |
    | `https://cernercentral.com/<instasncename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://<subdomain>.sandboxcernercentral.com/<instancename>` |

    > [!NOTE] 
    > Эти значения не являются реальными hello. Обновите эти значения с hello фактический идентификатор и ответ URL-адрес. Обратитесь к [Cerner центральная группа поддержки](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations) tooget эти значения.
 
4. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-cernercentral-tutorial/tutorial_general_400.png)

5. toogenerate hello **метаданные** URL-адрес, выполните следующие шаги hello:

    а. Щелкните **Регистрация приложений**.
    
    ![Настройка единого входа](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appregistrations.png)
   
    b. Нажмите кнопку **конечные точки** tooopen **конечные точки** диалоговое окно.  
    
    ![Настройка единого входа](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpointicon.png)

    c. Нажмите кнопку toocopy hello копирования **документа МЕТАДАННЫХ ФЕДЕРАЦИИ** URL-адрес и вставьте его в Блокнот.
    
    ![Настройка единого входа](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpoint.png)
     
    d. Теперь перейдите на странице свойств toohello **центральный Cerner** и копирования hello **идентификатор приложения** с помощью **копирования** кнопку и вставьте его в Блокнот.
 
    ![Настройка единого входа](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appid.png)

    д. Создать hello **URL-адрес метаданных** с помощью hello следующий шаблон:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`

6. tooconfigure единого входа на **центральный Cerner** параллельно, необходимо toosend hello **URL-адрес метаданных** слишком[Cerner центр поддержки](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations). Они настроить hello единого входа для интеграции hello toocomplete стороне приложений.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure. 

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить**.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из Саймон Britta.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-cerner-central-test-user"></a>Создание тестового пользователя Cerner Central

Приложение **Cerner Central** разрешает аутентификацию посредством любого поставщика федеративных удостоверений. Если пользователь может toolog в домашней страницы приложения toohello, они включаются в федерацию и не требуется вручную подготовки.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooCerner центральный.

![Назначение пользователя][200] 

**tooassign tooCerner Britta Simon центральный, выполните hello следующие шаги.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Cerner центральный**.

    ![Настройка единого входа](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello центральный Cerner плитки в панели доступа hello, вы должны получить tooyour автоматически подписан на центральный Cerner приложения. Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_203.png

