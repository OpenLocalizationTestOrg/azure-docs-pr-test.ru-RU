---
title: "Руководство по интеграции Azure Active Directory с ArcGIS Online | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и ArcGIS Online."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9e132a4-29e7-48bf-beb9-4148e617c8a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: f3dd55d798cf3256fb2758e011f33946baa405ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-arcgis-online"></a>Руководство по интеграции Azure Active Directory с ArcGIS Online

В этом учебнике вы узнаете, как toointegrate ArcGIS Online с Azure Active Directory (Azure AD).

Интеграция ArcGIS Online с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего tooArcGIS доступ через Интернет
- Можно включить на пользователей tooautomatically get вошедшего tooArcGIS сети (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

<!--## Overview

tooenable single sign-on with ArcGIS Online, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in ArcGIS Online.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с ArcGIS Online требуется hello следующих элементов:

- подписка Azure AD;
- подписка ArcGIS Online с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление ArcGIS Online из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-arcgis-online-from-hello-gallery"></a>Добавление ArcGIS Online из галереи hello
tooconfigure hello интеграции ArcGIS сети в Azure AD, вы должны tooadd ArcGIS сети из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd ArcGIS сети из галереи hello выполните hello следующие шаги.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. Нажмите кнопку **новое приложение** кнопку сверху "hello" hello диалоговое окно tooadd новое приложение.

    ![Приложения][3]

4. Введите в поле поиска hello **ArcGIS Online**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_search.png)

5. В панели результатов hello выберите **ArcGIS Online**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в ArcGIS Online с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в ArcGIS сети является tooa в Azure AD. Другими словами связи между пользователя Azure AD и hello связанных пользователей в ArcGIS документации должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** ArcGIS документации.

tooconfigure и тестирования Azure AD единого входа в ArcGIS Online, необходимы следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя, прошедшего ArcGIS Online](#creating-an-arcgis-online-test-user)**  -toohave аналог Саймон Britta документации ArcGIS, представление связанных toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в ArcGIS документации приложения.

**tooconfigure Azure AD единого входа в ArcGIS Online выполните следующие шаги hello.**

1. В hello в hello портала Azure **ArcGIS Online** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_samlbase.png)

3. На hello **URL-адреса и домена ArcGIS** выполните следующий шаг hello:

    ![Настройка единого входа](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_url.png)

    В hello **URL-адрес входа** текстовое значение hello типа, используя следующий шаблон hello:`https://<company>.maps.arcgis.com`

    > [!NOTE] 
    > Это значение не реальными hello. Измените значение этого параметра hello фактический URL-адрес входа. Обратитесь к [группа поддержки клиента в сети ArcGIS](http://support.esri.com/) tooget это значение. 

4. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.

    ![Настройка единого входа](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-arcgis-tutorial/tutorial_general_400.png)

6. В другом окне веб-браузера войдите на свой корпоративный веб-сайт ArcGIS в качестве администратора.

7. Щелкните **EDIT SETTINGS** (Изменить параметры).

    ![Изменение параметров](./media/active-directory-saas-arcgis-tutorial/ic784742.png "Изменение параметров")

8. Щелкните **Security**(Безопасность).

    ![Безопасность](./media/active-directory-saas-arcgis-tutorial/ic784743.png "Безопасность")

9. В разделе **Enterprise Logins** (Корпоративные имена для входа) установите флажок **Set Identity Provider** (Задать поставщик удостоверений).

    ![Корпоративные имена входа](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Корпоративные имена входа")

10. На hello **Настройка поставщика удостоверений** конфигурации выполните следующие шаги hello:
   
    ![Назначение поставщика удостоверений](./media/active-directory-saas-arcgis-tutorial/ic784745.png "Назначение поставщика удостоверений")
   
    а. В hello **имя** текстовом поле введите имя вашей организации.

    b. Для **метаданные для hello поставщика удостоверений предприятия будут передаваться с помощью**выберите **файл**.

    c. tooupload скачанный файл метаданных, щелкните **выбрать файл**.

    d. Щелкните **SET IDENTITY PROVIDER** (Задать поставщик удостоверений).

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_01.png) 

2. Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_02.png) 

3. Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из Саймон Britta.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-an-arcgis-online-test-user"></a>Создание тестового пользователя ArcGIS Online

В порядке tooenable toolog пользователей Azure AD в ArcGIS Online их необходимо подготовить в ArcGIS Online.  
В случае hello документации ArcGIS Подготовка осуществляется вручную.

**tooprovision учетной записи пользователя, выполните следующие шаги hello.**

1. Войдите в tooyour **ArcGIS** клиента.

2. Щелкните **INVITE MEMBERS** (Пригласить участников).
   
    ![Приглашение участников](./media/active-directory-saas-arcgis-tutorial/ic784747.png "Приглашение участников")

3. Щелкните переключатель **Add members automatically without sending an email** (Добавлять участников автоматически без отправки электронного сообщения) и нажмите кнопку **NEXT** (Далее).
   
    ![Автоматическое добавление участников](./media/active-directory-saas-arcgis-tutorial/ic784748.png "Автоматическое добавление участников")

4. На hello **члены** диалогового окна выполните следующие шаги hello:
   
     ![Добавление и просмотр](./media/active-directory-saas-arcgis-tutorial/ic784749.png "Добавление и просмотр")
    
     а. Введите hello **электронной почты**, **имя**, и **Фамилия** действительной учетной записи AAD, вы хотите tooprovision.
  
     b. Нажмите кнопку **ADD AND REVIEW** (Добавить и просмотреть).
5. Просмотрите данные hello введенные данные и нажмите кнопку **добавить ЧЛЕНОВ**.
   
    ![Добавление участника](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Добавление участника")
        
    > [!NOTE]
    > Hello владельцем учетной записи Azure Active Directory получит сообщение электронной почты и выполните их учетных записей tooconfirm ссылку, чтобы она стала активной.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooArcGIS доступа через Интернет.

![Назначение пользователя][200] 

**tooassign Britta Simon tooArcGIS через Интернет, выполнять hello следующие шаги:**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **ArcGIS Online**.

    ![Настройка единого входа](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello ArcGIS Online плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour ArcGIS интерактивных приложений.
Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_203.png

