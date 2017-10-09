---
title: "Руководство. Интеграция Azure Active Directory с приложением Wdesk | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Wdesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 06900a91-a326-4663-8ba6-69ae741a536e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 2c278a5e4f50cc362663efc0f826ff0c0fcf6e7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wdesk"></a>Руководство. Интеграция Azure Active Directory с Wdesk

В этом учебнике вы узнаете, как toointegrate Wdesk с Azure Active Directory (Azure AD).

Интеграция с Azure AD Wdesk предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooWdesk
- Можно включить на пользователей tooautomatically get вошедшего tooWdesk (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если необходимо, чтобы tooknow см. Дополнительные сведения об интеграции приложений SaaS в Azure AD. [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Wdesk требуется hello следующих элементов:

- подписка Azure AD;
- подписка Wdesk с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Wdesk из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-wdesk-from-hello-gallery"></a>Добавление Wdesk из галереи hello
tooconfigure hello интеграции Wdesk в Azure AD, вы должны tooadd Wdesk из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Wdesk из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Wdesk**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_search.png)

5. В панели результатов hello выберите **Wdesk**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в приложение Wdesk с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Wdesk является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Wdesk должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Wdesk.

tooconfigure и теста Azure AD единого входа с Wdesk, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Wdesk](#creating-a-wdesk-test-user)**  -toohave аналог Саймон Britta в Wdesk, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Wdesk.

**tooconfigure Azure AD единого входа с Wdesk, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Wdesk** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_samlbase.png)

3. На hello **URL-адреса и домена Wdesk** статьи, при желании tooconfigure приложения hello в **поставщика Удостоверений** инициируемых режиме выполняется hello следующие шаги:

    ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url.png)

    а. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`

    b. В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`

4. Установите флажок **Показать дополнительные параметры URL-адресов**, При необходимости приложение hello tooconfigure в **SP** инициировал режим, выполните следующий шаг hello:

    ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url1.png)

    В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`
     
    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить значения hello фактический идентификатор, URL-адрес ответа и URL-адрес входа. Вы можете получить эти значения из портала WDesk, при настройке единого входа hello. 
  
5. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_certificate.png) 

6. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_general_400.png)
    
7. В другом окне браузера, tooWdesk входа в систему с учетной записью администратора безопасности.

8. В левом нижнем hello, щелкните **администратора** и выберите **администратор учетной записи**:
 
     ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

9. Администратор Wdesk перейдите слишком**безопасности**, затем **SAML** > **параметры SAML**:

    ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig2.png)

10. В разделе **Общие параметры**, проверьте hello **включить SAML Single Sign On**:

    ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig3.png)

11. В разделе **подробные сведения о поставщике службы**, выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig4.png)

      а. Копировать hello **URL-адрес входа** и вставьте его в **URL-адрес входа** текстовое поле на портале Azure.
   
      b. Копировать hello **URL-адрес метаданных** и вставьте его в **идентификатор** текстовое поле на портале Azure.
       
      c. Копировать hello **URL-адрес потребителя** и вставьте его в **URL-адрес ответа** текстовое поле на портале Azure.
   
      d. Нажмите кнопку **Сохранить** об изменениях hello Azure toosave портала.      

12. Нажмите кнопку **настроить параметры поставщика удостоверений** tooopen **изменение параметров поставщика удостоверений** диалогового окна. Нажмите кнопку **выбрать файл** toolocate hello **Metadata.xml** файл, сохраненный с портала Azure, затем передать его.
    
    ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig5.png)
  
13. Нажмите кнопку **Сохранить изменения**.

    ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfigsavebutton.png)

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-wdesk-test-user"></a>Создание тестового пользователя Wdesk

Пользователи toolog tooenable Azure AD в tooWdesk, их необходимо подготовить в Wdesk. В Wdesk подготовка выполняется вручную.

**tooprovision учетной записи пользователя, выполните следующие шаги hello.**

1. Войдите с учетной записью администратора безопасности tooWdesk.
2. Перейдите в слишком**администратора** > **администратор учетной записи**.

     ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

3. Щелкните элемент **Members** (Участники) в разделе **People** (Люди).

4. Теперь щелкните **Add Member** tooopen **Add Member** диалоговое окно. 
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser1.png)  

5. В **пользователя** текста введите hello имя пользователя как  **brittasimon@contoso.com**  и нажмите кнопку **Продолжить** кнопки.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser3.png)

6.  Введите сведения hello, как показано ниже:
  
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser4.png)
 
    а. В **электронной почты** текста введите hello электронной почты пользователя, таких как  **brittasimon@contoso.com** .

    b. В **имя** текста введите имя пользователя, такие как hello **Britta**.

    c. В **Фамилия** текста введите hello фамилию пользователя как **Simon**.

7. Щелкните кнопку **Save Member** (Сохранить участника).  

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser5.png)

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooWdesk доступа.

![Назначение пользователя][200] 

**tooassign tooWdesk Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Wdesk**.

    ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello Wdesk плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Wdesk приложения.
Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).


## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_203.png

