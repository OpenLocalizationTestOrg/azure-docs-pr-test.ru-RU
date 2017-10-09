---
title: "Руководство по интеграции Azure Active Directory с PerformanceCentre | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и PerformanceCentre."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65288c32-f7e6-4eb3-a6dc-523c3d748d1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 19781c0087093a67c70dc90072cf1a119bb2ade0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-performancecentre"></a>Руководство по интеграции Azure Active Directory с PerformanceCentre

В этом учебнике вы узнаете, как toointegrate PerformanceCentre с Azure Active Directory (Azure AD).

Интеграция с Azure AD PerformanceCentre предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooPerformanceCentre
- Можно включить на пользователей tooautomatically get вошедшего tooPerformanceCentre (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с PerformanceCentre требуется hello следующих элементов:

- подписка Azure AD;
- подписка PerformanceCentre с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление PerformanceCentre из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-performancecentre-from-hello-gallery"></a>Добавление PerformanceCentre из галереи hello
tooconfigure hello интеграции PerformanceCentre в Azure AD, вы должны tooadd PerformanceCentre из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd PerformanceCentre из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **PerformanceCentre**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_search.png)

5. В панели результатов hello выберите **PerformanceCentre**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в приложение PerformanceCentre с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в PerformanceCentre является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в PerformanceCentre должен установить toobe.

В PerformanceCentre, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с PerformanceCentre, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя PerformanceCentre](#creating-a-performancecentre-test-user)**  -toohave аналог Саймон Britta в PerformanceCentre, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении PerformanceCentre.

**tooconfigure Azure AD единого входа с PerformanceCentre, выполните следующие шаги hello.**

1. В hello в hello портала Azure **PerformanceCentre** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_samlbase.png)

3. На hello **URL-адреса и домена PerformanceCentre** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`http://companyname.performancecentre.com/saml/SSO`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`http://companyname.performancecentre.com`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить значения hello фактический URL-адрес входа и идентификатор. Обратитесь к [группа поддержки клиента PerformanceCentre](https://www.performancecentre.com/contact-us/) tooget эти значения. 

4. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-performancecentre-tutorial/tutorial_general_400.png)

6. На hello **конфигурации PerformanceCentre** щелкните **Настройка PerformanceCentre** tooopen **Настройка входа** окна. Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_configure.png) 

7. Tooyour входа **PerformanceCentre** сайт компании от имени администратора.

8. На вкладке hello hello левой стороны, нажмите кнопку **Настройка**.
   
    ![Единый вход в Azure AD][10]

9. На вкладке hello hello левой стороны, нажмите кнопку **Разное**, а затем нажмите кнопку **единого входа**.
   
    ![Единый вход в Azure AD][11]

10. В поле **Protocol** (Протокол) выберите **SAML**.
   
    ![Единый вход в Azure AD][12]

11. Откройте скачанный файл метаданных в блокноте копирования содержимого hello, вставьте его в hello **метаданные поставщика удостоверений** текстовое поле, а затем нажмите кнопку **Сохранить**.
   
    ![Единый вход в Azure AD][13]

12. Убедитесь, что hello значения для hello **сущности базовый URL-адрес** и **URL-адрес идентификатор сущности** заданы правильно.
    
     ![Единый вход в Azure AD][14]

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-performancecentre-test-user"></a>Создание тестового пользователя PerformanceCentre

Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в PerformanceCentre.

**toocreate пользователя с именем Саймон Britta в PerformanceCentre, выполните следующие шаги hello.**

1. Войдите на tooyour PerformanceCentre сайт компании от имени администратора.

2. В меню слева hello hello выберите **Interrelate**и нажмите кнопку **создать участника**.
   
    ![Создание пользователя][400]

3. На hello **между — создать участника** диалоговое окно, выполните следующие шаги hello:
   
    ![Создание пользователя][401]
    
    а. Тип hello необходимые атрибуты для Саймон Britta в соответствующие текстовые поля.
    
    >[!IMPORTANT]
    >Имя пользователя Britta должен быть атрибут в PerformanceCentre hello так же, как hello имя пользователя в Azure AD.
    
    b. Выберите значение **Client Administrator** (Администратор клиента) в поле **Choose Role** (Выберите роль).
    
    c. Щелкните **Сохранить**. 

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooPerformanceCentre доступа.

![Назначение пользователя][200] 

**tooassign tooPerformanceCentre Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **PerformanceCentre**.

    ![Настройка единого входа](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".  

При нажатии кнопки hello PerformanceCentre плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour PerformanceCentre приложения.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_06.png
[11]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_07.png
[12]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_08.png
[13]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_09.png
[14]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_10.png

[100]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_203.png
[400]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_11.png
[401]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_12.png

