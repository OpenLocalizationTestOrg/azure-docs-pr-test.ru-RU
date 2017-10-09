---
title: "Руководство по интеграции Azure Active Directory с FreshDesk | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и FreshDesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2a3e5aa-7b5a-4fe4-9285-45dbe6e8efcc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 577a5eb6d9b1bc03030a2b47f63d375869c903bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshdesk"></a>Руководство по интеграции Azure Active Directory с FreshDesk

В этом учебнике вы узнаете, как toointegrate FreshDesk с Azure Active Directory (Azure AD).

Интеграция FreshDesk с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooFreshDesk
- Можно включить на пользователей tooautomatically get вошедшего tooFreshDesk (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал управления Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с FreshDesk требуется hello следующих элементов:

- подписка Azure AD;
- подписка FreshDesk с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не следует использовать рабочую среду при отсутствии необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление FreshDesk из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-freshdesk-from-hello-gallery"></a>Добавление FreshDesk из галереи hello
tooconfigure hello интеграции FreshDesk в Azure AD, вы должны tooadd FreshDesk из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd FreshDesk из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портала управления Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".

    ![Приложения][3]

4. Введите в поле поиска hello **FreshDesk**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_search.png)

5. В панели результатов hello выберите **FreshDesk**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в приложение FreshDesk с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в FreshDesk является tooa в Azure AD. Другими словами связи между пользователя Azure AD и hello связанных пользователей в FreshDesk требуется toobe установлено.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в FreshDesk.

tooconfigure и теста Azure AD единого входа с FreshDesk, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя FreshDesk](#creating-a-freshdesk-test-user)**  -toohave аналог Саймон Britta в FreshDesk, представление связанных toohello Azure AD ей.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал управления Azure hello и настройки единого входа в ваше приложение Freshservice.

**tooconfigure Azure AD единого входа с FreshDesk, выполните следующие шаги hello.**

1. На портале управления Azure hello на hello **FreshDesk** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна, как **режим** выберите **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_samlbase.png)

3. На hello **URL-адреса и домена FreshDesk** статьи, введите hello **URL-адрес входа** как: `https://<tenant-name>.freshdesk.com` или любое другое значение имеет предлагаемых Freshdesk.

    ![Настройка единого входа](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_url.png)

    > [!NOTE] 
    > Обратите внимание, что это значение используется только в качестве примера. Вместо него необходимо указать фактический URL-адрес для входа. Для получения этого значения обратитесь в [службу поддержки клиентов FreshDesk](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg).  

4. На hello **сертификат подписи SAML** щелкните **сертификат** и сохраните hello сертификата на компьютере.

    ![Настройка единого входа](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-freshdesk-tutorial/tutorial_general_400.png)

6. На hello **конфигурации FreshDesk** щелкните **Настройка FreshDesk** tooopen Настройка входа окна. Скопируйте hello SAML единого входа URL-адрес службы и URL-адрес выхода из hello **краткий справочник** раздела.

    ![Настройка единого входа](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_configure.png)

7. В другом окне браузера войдите на свой корпоративный веб-сайт Freshdesk в качестве администратора.

8. В меню в верхней части hello hello выберите **администратора**.
   
   ![Администратор](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "Администратор")

9. В hello **Общие параметры** щелкните **безопасности**.
   
   ![Безопасность](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "Безопасность")

10. В hello **безопасности** выполните следующие шаги hello:
   
    ![Единый вход](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "Единый вход")
   
    а. Выберите для параметра **Single Sign On (SSO)** (Единый вход) значение **On** (Включено).

    b. Выберите **Единый вход SAML**.

    c. Тип hello **SAML единого входа URL-адрес службы** скопирован из портала Azure в hello **URL-адрес входа SAML** текстового поля.

    d. Тип hello **URL-адрес выхода** скопирован из портала Azure в hello **URL-адрес выхода** текстового поля.

    д. Копировать hello **отпечаток** из сертификата hello загружен с портала Azure и вставьте его в hello **отпечаток сертификата безопасности** текстового поля.  
 
    >[!TIP]
    >Дополнительные сведения см. в разделе [как tooretrieve значение отпечатка сертификата](http://youtu.be/YKQF266SAxI). 
    
    f. Щелкните **Сохранить**.


### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя на портале управления Azure hello, вызывается Саймон Britta.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал управления Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_01.png) 

2. Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_02.png) 

3. Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-freshdesk-test-user"></a>Создание тестового пользователя FreshDesk

В порядке tooenable toolog пользователей Azure AD в FreshDesk их необходимо подготовить во FreshDesk.  
В случае hello объекта FreshDesk Подготовка выполняется вручную.

**tooprovision учетных записей пользователей, выполните следующие действия hello:**

1. Войдите в tooyour **Freshdesk** клиента.
2. В меню в верхней части hello hello выберите **администратора**.
   
   ![Администратор](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "Администратор")

3. В hello **Общие параметры** щелкните **агенты**.
   
   ![Агенты](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "Агенты")

4. Нажмите **Создать агента**.
   
    ![Создание агента](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "Создание агента")

5. В диалоговом окне сведений об агенте hello выполните hello следующие шаги.
   
   ![Сведения об агенте](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "Сведения об агенте")
   
   а. В hello **полное имя** текстовое поле, имя типа hello hello Azure AD счета tooprovision.

   b. В hello **электронной почты** текстового поля, типа hello Azure AD адрес электронной почты учетной записи hello Azure AD будет tooprovision.

   c. В hello **заголовок** текстовом поле введите название hello hello Azure AD счета tooprovision.

   d. Выберите **Agents role** (Роль агента) и нажмите кнопку **Assign** (Назначить).
       
   д. Щелкните **Сохранить**.     
   
    >[!NOTE]
    >Владелец учетной записи Hello Azure AD получит сообщение электронной почты, включает в себя учетную запись hello tooconfirm ссылку, перед его активации. 
    > 
    
    >[!NOTE]
    >Можно использовать любые другие Freshdesk пользователя средства создания учетных записей или интерфейсы API, предоставляемые Freshdesk tooprovision учетных записей пользователей AAD. tooFreshDesk.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа, предоставляя свой доступ панель инструментов.

![Назначение пользователя][200] 

**tooassign tooFreshDesk Britta Simon выполните следующие шаги hello.**

1. На портале управления Azure hello, открыть представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **FreshDesk**.

    ![Настройка единого входа](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello FreshDesk плитки в панели доступа hello, вы должны получить входа страницы tooget вошедшего tooyour приложение Freshservice.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_203.png

