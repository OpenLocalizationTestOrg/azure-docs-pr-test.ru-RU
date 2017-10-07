---
title: "Руководство по интеграции Azure Active Directory с Tableau Server | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Tableau сервером."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c1917375-08aa-445c-a444-e22e23fa19e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: feb2087bd6ae6ddcb920901e6719688fc95ae287
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-server"></a>Учебник. Интеграция Azure Active Directory с Tableau Server

В этом учебнике вы узнаете, как toointegrate Tableau Server в Azure Active Directory (Azure AD).

Интеграция сервера Tableau с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooTableau сервера
- Можно включить на пользователей tooautomatically get вошедшего tooTableau сервера (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с сервером Tableau, требуется hello следующих элементов:

- подписка Azure AD;
- подписка Tableau Server с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление сервера Tableau из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-tableau-server-from-hello-gallery"></a>Добавление сервера Tableau из галереи hello
tooconfigure hello интеграции Tableau Server в Azure AD, вы должны tooadd Tableau сервера из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Tableau сервера из галереи hello выполните hello следующие шаги.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Tableau сервера**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_search.png)

5. В панели результатов hello, выберите **сервера Tableau**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Tableau Server для тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Tableau Server является tooa в Azure AD. Другими словами связи между пользователя Azure AD и hello связанных пользователей на сервере Tableau должен установить toobe.

В сервере Tableau, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с сервера Tableau, необходимы следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя сервера Tableau](#creating-a-tableau-server-test-user)**  -toohave аналог Саймон Britta Server Tableau, которое представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в Tableau серверное приложение.

**tooconfigure Azure AD единого входа с сервером Tableau, выполните следующие шаги hello.**

1. В hello в hello портала Azure **сервера Tableau** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_samlbase.png)

3. На hello **URL-адреса и доменом сервера Tableau** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://azure.<domain name>.link`
    
    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://azure.<domain name>.link`

    c. В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://azure.<domain name>.link/wg/saml/SSO/index.html`
     
    > [!NOTE] 
    > Hello выше значения не реальные значения. Более поздней версии обновляются значениями hello hello фактический URL-адрес и идентификатор, на странице конфигурации сервера Tableau hello. 

4. Tableau серверное приложение ожидает утверждения SAML hello в определенном формате. Настройка следующих утверждений для этого приложения hello. Вы можете управлять hello значения этих атрибутов из hello **«Атрибуты пользователя»** раздел на странице интеграции приложений. Hello следующем снимке экрана показан пример для hello же.
    
    ![Настройка единого входа](./media/active-directory-saas-tableauserver-tutorial/3.png)
    
5. В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна, настроить атрибутов токена SAML, как показано в приведенном выше рисунке hello и выполнять hello следующие шаги:
    
    | Имя атрибута | Значение атрибута |
    | ---------------| --------------- |    
    | Имя пользователя | *user.displayname* |

    а. Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.

    ![Настройка единого входа](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_04.png)

    ![Настройка единого входа](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_05.png)
    
    b. В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.
    
    c. Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.
    
    d. Нажмите кнопку **ОК**.


6. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_certificate.png) 

7. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS>
8. tooget единого входа, настроенному для вашего приложения, необходимо клиента сервера Tableau tooyour toosign вход в систему с правами администратора.
   
   а. В конфигурации сервера Tableau hello, щелкните hello **SAML** вкладки.
  
    ![Настройка единого входа](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_001.png) 
  
   b. Установка флажка hello **использование SAML для единого входа**.
   
   c. URL-адрес возврата tableau сервера — URL-адрес, Tableau сервер пользователи будут получать доступ к, таких как http://tableau_server hello. Мы не рекомендуем использовать http://localhost. URL-адреса с конечной косой чертой (например http://tableau_server/) не поддерживаются. Копировать **URL-адрес возврата сервера Tableau** и вставьте его tooAzure AD **на URL-адрес входа** текстовое поле в **Tableau домена сервера и URL-адреса** раздела.
   
   d. Идентификатор сущности SAML — идентификатор сущности hello однозначно определяет ваш сервер Tableau установки toohello поставщика удостоверений. Можно ввести URL-адрес сервера Tableau еще раз, при необходимости, но он не имеет toobe Tableau URL-адрес сервера. Копировать **идентификатор сущности SAML** и вставьте его tooAzure AD **идентификатор** текстовое поле в **Tableau домена сервера и URL-адреса** раздела.
     
   д. Нажмите кнопку hello **экспорт метаданных файла** и откройте его в приложение hello текстового редактора. Найдите URL-адрес службы утверждения потребителя с Http Post и индексом 0, а также копировать hello URL-адрес. Теперь вставьте tooAzure AD **URL-адрес ответа** текстовое поле в **URL-адреса и доменом сервера Tableau** раздела.
   
   f. Найдите файл метаданных федерации, Скачанный с портала Azure, а затем передать его в hello **файл метаданных поставщика удостоверений SAML**.
   
   ж. Нажмите кнопку hello **ОК** кнопки странице конфигурации сервера Tableau hello.
   
    >[!NOTE] 
    >Клиент имеет tooupload сертификаты в конфигурации единого входа SAML Server Tableau hello и может получить пропущена в hello потока единого входа.
    >Если требуется справка настройки SAML на сервере Tableau затем см. в статье toothis [Настройка SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).
    >
<CE>

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-tableau-server-test-user"></a>Создание тестового пользователя Tableau Server

Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в Tableau Server. Необходимо tooprovision всем пользователям hello hello Tableau server. 

Username hello пользователя должен соответствовать hello значение, которое вы настроили в Azure AD hello пользовательский атрибут **username**. С hello правильное сопоставление интеграции hello должно работать [Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).

>[!NOTE]
>Если вам требуется toocreate пользователя вручную, необходимы toocontact hello Tableau Server администратора в вашей организации.
> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooTableau сервера.

![Назначение пользователя][200] 

**tooassign tooTableau Britta Simon сервера, выполните hello следующие шаги.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Tableau сервера**.

    ![Настройка единого входа](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello Tableau Server плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Tableau серверного приложения.
Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_203.png

