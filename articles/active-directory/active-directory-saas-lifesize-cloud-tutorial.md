---
title: "Учебник. Интеграция Azure Active Directory с Lifesize Cloud | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и облаком Lifesize."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 75fab335-fdcd-4066-b42c-cc738fcb6513
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: ae599907e872571b3220de7122006c7db8db4a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lifesize-cloud"></a>Учебник. Интеграция Azure Active Directory с Lifesize Cloud

В этом учебнике вы узнаете, как toointegrate Lifesize облака в Azure Active Directory (Azure AD).

Интеграция с Azure AD Lifesize облако предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooLifesize облака
- Можно включить на пользователей tooautomatically get вошедшего tooLifesize облака (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с облаком Lifesize требуется hello следующих элементов:

- подписка Azure AD;
- подписка Lifesize Cloud с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Lifesize облака из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-lifesize-cloud-from-hello-gallery"></a>Добавление Lifesize облака из галереи hello
tooconfigure hello интеграция Lifesize облака в Azure AD, вы должны tooadd Lifesize облако из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Lifesize облака из галереи hello выполните hello следующие шаги.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Lifesize облака**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_search.png)

5. В панели результатов hello, выберите **облака Lifesize**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD.
В этом разделе описана настройка и проверка единого входа Azure AD в Lifesize Cloud с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в облаке Lifesize является tooa в Azure AD. Другими словами связи между пользователя Azure AD и hello связанных пользователей в облаке Lifesize должен установить toobe.

В облаке Lifesize присвоить значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и тестирования Azure AD единого входа с облаком Lifesize, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя облака Lifesize](#creating-a-lifesize-cloud-test-user)**  -toohave аналог Саймон Britta в облаке Lifesize, представление связанных toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в Lifesize облачного приложения.

**tooconfigure Azure AD единого входа с облаком Lifesize выполните следующие шаги hello.**

1. В hello в hello портала Azure **облака Lifesize** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_samlbase.png)

3. На hello **URL-адреса и домена облака Lifesize** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://login.lifesizecloud.com/ls/?acs`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://login.lifesizecloud.com/<companyname>`

     
4. Проверьте **Показывать дополнительные параметры URL-адреса**, выполните следующий шаг hello:  
   
    ![Настройка единого входа](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url1.png)

    В hello **ретрансляции состояние** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://webapp.lifesizecloud.com/?ent=<identifier>`
   
   > [!NOTE] 
   >Обратите внимание на то, что они не hello реальные значения. имеется tooupdate эти значения с hello фактический URL-адрес входа, статус ретрансляции и идентификатора. Обратитесь к [группа поддержки клиента облака Lifesize](https://www.lifesize.com/support) tooget URL-адрес входа и значений идентификаторов, чтобы получить значение состояния ретрансляции из конфигурации единого входа, которая описывается далее в учебнике hello.

4. На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_400.png)

6. На hello **конфигурации облака Lifesize** щелкните **Настройка облака Lifesize** tooopen **Настройка входа** окна. Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_configure.png) 

7. tooget SSO настроен для вашего приложения, имя входа в hello Lifesize облачного приложения с правами администратора.

8. В hello правом верхнем углу щелкните свое имя и нажмите кнопку на hello **параметры обработки**.
   
    ![Настройка единого входа](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_06.png)

9. В параметры обработки щелкните hello hello **Настройка единого входа** ссылку. Откроется страница hello настройку единого входа для экземпляра.
   
    ![Настройка единого входа](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_07.png)

10. Теперь можно настройте следующие значения в пользовательский Интерфейс для настройки единого входа hello hello.    
   
    ![Настройка единого входа](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_08.png)
    
    а. В **издатель поставщика удостоверений** текстовое значение hello вставить **идентификатор сущности SAML** скопирован из портала Azure.

    b.  В **URL-адрес входа** текстовое значение hello вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure.

    c. Откройте сертификат в кодировке base-64 в блокноте, загруженные из портала Azure hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **сертификат X.509** текстового поля.
  
    d. В атрибут SAML hello сопоставления для hello имя текстового поля введите значение hello как **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**
    
    д. В сопоставлении атрибут SAML hello для hello **Фамилия** текстовом поле введите значение hello как **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**
    
    f. В сопоставлении атрибут SAML hello для hello **электронной почты** текстовом поле введите значение hello как **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**

11. можно щелкнуть hello конфигурации hello toocheck **тест** кнопки.
   
    >[!NOTE]
    >Для успешного тестирования требуется мастер настройки toocomplete hello в Azure AD и также предоставить доступ toousers или группы, которые можно выполнить проверку hello.

12. Включите hello единого входа, установив на hello **Включить единый вход** кнопки.

13. Теперь щелкните hello **обновление** кнопку, чтобы все параметры hello сохраняются. Это создаст значение RelayState hello. Hello копирования RelayState значение, которое создается в текстовом поле hello, вставьте его в hello **состояние ретрансляции** текстовое поле в разделе **URL-адреса и домена облака Lifesize** раздела. 

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-lifesize-cloud-test-user"></a>Создание тестового пользователя Lifesize Cloud

В этом разделе описано, как создать пользователя Britta Simon в приложении Lifesize Cloud. Lifesize Cloud поддерживает автоматическую подготовку пользователей. После успешной проверки подлинности в Azure AD hello пользователя будут автоматически подготовлены приложения hello. 

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooLifesize облака.

![Назначение пользователя][200] 

**tooassign tooLifesize Britta Simon облака, выполните hello следующие шаги.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Lifesize облака**.

    ![Настройка единого входа](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello облака Lifesize плитки в панели доступа hello, должно появиться страница входа Lifesize облачного приложения.
Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_203.png

