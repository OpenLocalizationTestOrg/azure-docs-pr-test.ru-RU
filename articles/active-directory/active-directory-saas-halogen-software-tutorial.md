---
title: "Руководство по интеграции Azure Active Directory с Halogen Software | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и имеющий программного обеспечения."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ca2298d-9a0c-4f14-925c-fa23f2659d28
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: bdb67de713771d6e306f287c4b13895f6336f7ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halogen-software"></a>Учебник. Интеграция Azure Active Directory с Halogen Software

В этом учебнике вы узнаете, как toointegrate имеющий программного обеспечения в Azure Active Directory (Azure AD).

Интеграция имеющий программного обеспечения в Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooHalogen программного обеспечения
- Можно включить на пользователей tooautomatically get вошедшего tooHalogen программного обеспечения (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с программным обеспечением имеющий требуется hello следующих элементов:

- подписка Azure AD;
- подписка Halogen Software с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария

В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление программного обеспечения имеющий из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-halogen-software-from-hello-gallery"></a>Добавление программного обеспечения имеющий из галереи hello

tooconfigure hello интеграции имеющий программного обеспечения в Azure AD, вы должны tooadd имеющий программного обеспечения из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd имеющий программного обеспечения из галереи hello выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **программного обеспечения имеющий**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_search.png)

5. В панели результатов hello, выберите **программного обеспечения имеющий**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Halogen Software для тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в программном обеспечении имеющий является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в программном обеспечении имеющий должен установить toobe.

В программном обеспечении имеющий, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с имеющий программного обеспечения, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя программного обеспечения имеющий](#creating-a-halogen-software-test-user)**  -toohave аналог Саймон Britta имеющий программного обеспечения, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении имеющий программного обеспечения.

**tooconfigure Azure AD единого входа с программным обеспечением имеющий выполните следующие шаги hello.**

1. В hello в hello портала Azure **программного обеспечения имеющий** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_samlbase.png)

3. На hello **URL-адреса и имеющий программного обеспечения домена** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://global.hgncloud.com/<companyname>`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello: `https://global.halogensoftware.com/<companyname>`,`https://global.hgncloud.com/<companyname>`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить значения hello фактический URL-адрес входа и идентификатор. Обратитесь к [имеющий клиентское программное обеспечение поддержки](https://support.halogensoftware.com/) tooget эти значения. 
 


4. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-halogen-software-tutorial/tutorial_general_400.png)

6. В другом окне браузера, tooyour входа **программного обеспечения имеющий** приложение от имени администратора.

7. Нажмите кнопку hello **параметры** вкладки. 
   
    ![Что такое Azure AD Connect?][12]

8. Hello панели навигации слева щелкните **конфигурация SAML**. 
   
    ![Что такое Azure AD Connect?][13]

9. На hello **конфигурация SAML** выполните следующие шаги hello: 

    ![Что такое Azure AD Connect?][14]

     а. В качестве значения поля **Уникальный идентификатор** выберите **NameID**.

     b. В качестве значения поля **Unique Identifier Maps To** (Уникальный идентификатор сопоставляется с) выберите **Имя пользователя**.
  
     c. tooupload скачанный файл метаданных, щелкните **Обзор** tooselect hello файла, а затем **передать файл**.
 
     d. Конфигурация tootest hello, нажмите кнопку **запустить тест**. 
    
    >[!NOTE]
    >Требуется toowait приветственное сообщение «*hello SAML проверка завершена. Закройте это окно*". Закройте окно браузера открытый hello. Hello **включить SAML** флажок доступна только в том случае, если проверка hello завершена. 
     
     д. Выберите **Включить SAML**.
    
     Е. Нажмите кнопку **Сохранить изменения**. 

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_04.png) 

    а. В hello **имя** в текстовое поле имя типа как **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-halogen-software-test-user"></a>Создание тестового пользователя Halogen Software

Цель этого раздела Hello — toocreate пользователя с именем Britta Simon имеющий программного обеспечения.

**toocreate пользователя с именем Britta Simon имеющий программного обеспечения, выполните следующие шаги hello.**

1. Войдите на tooyour **программного обеспечения имеющий** приложение от имени администратора.

2. Нажмите кнопку hello **центра пользователей** , а затем щелкните **Create User**.
   
    ![Что такое Azure AD Connect?][300]  

3. На hello **нового пользователя** диалогового окна выполните следующие шаги hello:
   
    ![Что такое Azure AD Connect?][301]

    а. В hello **имя** в текстовое поле имя первого типа hello пользователя как **Britta**.
    
    b. В hello **Фамилия** текстовое поле, тип фамилию пользователя hello как **Simon**. 

    c. В hello **Username** введите **Britta Simon**, hello имя пользователя как hello портал Azure.

    d. В hello **пароль** введите пароль для Britta.
    
    д. Щелкните **Сохранить**.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooHalogen программного обеспечения.

![Назначение пользователя][200] 

**tooassign tooHalogen Britta Simon программное обеспечение, выполните hello следующие шаги.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **программного обеспечения имеющий**.

    ![Настройка единого входа](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".

Если щелкнуть плитку программного обеспечения имеющий hello в hello панели доступа, следует получать автоматически вошедшего tooyour имеющий программного приложения.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_12.png

[13]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_13.png

[14]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_14.png

[100]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_203.png

[300]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_300.png

[301]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_301.png
