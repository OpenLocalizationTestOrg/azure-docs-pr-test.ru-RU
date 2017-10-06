---
title: "Руководство. Интеграция Azure Active Directory с Aha! | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Aha!."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ad955d3d-896a-41bb-800d-68e8cb5ff48d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: d844db3c0a035560e6fb275017215171743fba56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-aha"></a>Руководство. Интеграция Azure Active Directory с Aha!

В этом учебнике вы узнаете, как toointegrate Aha! с Azure Active Directory (Azure AD).

Интеграция Aha! с помощью Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooAha!
- Можно включить на пользователей tooautomatically get вошедшего tooAha! с использованием учетной записи Azure AD.
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Aha!, требуется hello следующих элементов:

- подписка Azure AD;
- Подписка Aha! с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Aha! из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-aha-from-hello-gallery"></a>Добавление Aha! из галереи hello
Интеграция hello tooconfigure Aha! в Azure AD необходимо tooadd Aha! из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Aha! из галереи hello выполните следующие шаги hello.**

1. В hello ** [портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Aha!**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-aha-tutorial/tutorial_aha_search.png)

5. В панели результатов hello выберите **Aha!**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-aha-tutorial/tutorial_aha_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в приложение Aha! с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow, какой пользователь hello аналога в Aha! — пользователь tooa в Azure AD. Другими словами связи между пользователя Azure AD и hello, связанные с пользователем в Aha! необходимо установить toobe.

В Aha!, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и Azure AD тестирования единого входа с Aha!, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user) ** -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание Aha! Тестовый пользователь](#creating-an-aha-test-user) ** -toohave аналог Саймон Britta в Aha! Это связанный toohello представление пользователя Azure AD.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on) ** -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в Aha! приложении Aha!.

**tooconfigure Azure AD единого входа с Aha!, выполните следующие шаги hello:**

1. В hello в hello портала Azure **Aha!** щелкните **Единый вход**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-aha-tutorial/tutorial_aha_samlbase.png)

3. На hello **Aha! URL-адреса и домена** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-aha-tutorial/tutorial_aha_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.aha.io/session/new`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.aha.io`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить значения hello фактический URL-адрес входа и идентификатор. Обратитесь к [группе Группа поддержки клиента](https://www.aha.io/company/contact) tooget эти значения. 
 
4. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-aha-tutorial/tutorial_aha_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-aha-tutorial/tutorial_general_400.png)

6. В другом окне браузера войдите в tooyour Aha! в качестве администратора.

7. В меню в верхней части hello hello выберите **параметры**.

    ![Параметры](./media/active-directory-saas-aha-tutorial/IC798950.png "Параметры")

8. Выберите раздел **Учетная запись**.
   
    ![Профиль](./media/active-directory-saas-aha-tutorial/IC798951.png "Профиль")

9. Нажмите **Безопасность и единый вход**.
   
    ![Безопасность и единый вход](./media/active-directory-saas-aha-tutorial/IC798952.png "Безопасность и единый вход")

10. В разделе **Единый вход** в качестве **поставщика удостоверений** выберите **SAML 2.0**.
   
    ![Безопасность и единый вход](./media/active-directory-saas-aha-tutorial/IC798953.png "Безопасность и единый вход")

11. На hello **Single Sign-On** конфигурации выполните следующие шаги hello:
    
    ![Единый вход](./media/active-directory-saas-aha-tutorial/IC798954.png "Единый вход")
    
       а. В hello **имя** текстовом поле введите имя для конфигурации.

       b. Для параметра **Configure using** (Использовать при настройке) выберите значение **Файл метаданных**.
   
       c. tooupload скачанный файл метаданных, щелкните **Обзор**.
   
       d. Нажмите кнопку **Обновить**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello ** Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-an-aha-test-user"></a>Создание тестового пользователя Aha!

toolog tooenable Azure AD пользователи в tooAha!, их необходимо подготовить в Aha!.  

В случае, когда hello Aha!, Подготовка — это автоматизированная задача. С вашей стороны никакие действия не требуются.

Пользователи создаются автоматически при необходимости hello первой единого входа попытки.

>[!NOTE]
>Вы можете использовать любые другие средства создания учетной записи пользователя Aha! или API, предоставляемые Aha! tooprovision учетных записей пользователей AAD.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooAha!.

![Назначение пользователя][200] 

**tooassign tooAha Britta Simon!, выполните следующие шаги hello:**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Aha!**.

    ![Настройка единого входа](./media/active-directory-saas-aha-tutorial/tutorial_aha_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

Tootest параметры единого входа, откройте панель доступа hello. Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-aha-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-aha-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-aha-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-aha-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-aha-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-aha-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-aha-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-aha-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-aha-tutorial/tutorial_general_203.png

