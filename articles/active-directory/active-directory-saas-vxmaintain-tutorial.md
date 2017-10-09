---
title: "Руководство по интеграции Azure Active Directory с vxMaintain | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и vxMaintain."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 841a1066-593c-4603-9abe-f48496d73d10
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 937ea276d898986fc5a953c96fddabdc8940309f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-vxmaintain"></a>Руководство по интеграции Azure Active Directory с vxMaintain

В этом учебнике вы узнаете, как vxMaintain toointegrate с Azure Active Directory (Azure AD).

Такая интеграция обеспечивает несколько важных преимуществ. Вы можете:

- Элемент управления в Azure AD, имеющего доступ к toovxMaintain.
- Включите tooautomatically пользователей при входе в toovxMaintain с единого входа (SSO) с помощью своих учетных записей Azure AD.
- Управление учетными записями в одном централизованном месте: hello портал Azure.

toolearn более об интеграции приложений SaaS с Azure AD, в разделе [доступ к приложению и единый вход в Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с vxMaintain требуется hello следующих элементов:

- подписка Azure AD;
- подписка vxMaintain с поддержкой единого входа.

> [!NOTE]
> При тестировании hello шаги в этом учебнике, рекомендуется не использовать в производственной среде.

tootest hello шаги в этом учебнике, придерживайтесь следующих рекомендаций:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. 

сценарий Hello, описывающий этот учебник состоит из двух основных компонентов.

* Добавление vxMaintain из галереи hello
* Настройка и проверка единого входа в Azure AD

## <a name="add-vxmaintain-from-hello-gallery"></a>Добавление vxMaintain из коллекции hello
интеграции hello tooconfigure vxMaintain с Azure AD, вы должны vxMaintain tooadd из списка tooyour коллекции hello управляемых приложений SaaS.

vxMaintain tooadd из галереи hello hello следующие:

1. В hello [портал Azure](https://portal.azure.com)в левой области hello, выберите hello **Azure Active Directory** кнопки. 

    ![Кнопка Hello Azure Active Directory][1]

2. Щелкните **Корпоративные приложения** > **Все приложения**.

    ![панель «Корпоративных приложений» Hello][2]
    
3. приложения, в hello tooadd **все приложения** выберите **новое приложение**.

    ![Здравствуйте, «Новое приложение» кнопки][3]

4. Введите в поле поиска hello **vxMaintain**.

    ![Hello «В единого входа режим» раскрывающегося списка](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_search.png)

5. В списке результатов hello выберите **vxMaintain**, а затем выберите **добавить**.

    ![ссылка vxMaintain Hello](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в vxMaintain с использованием тестового пользователя Britta Simon.

Для toowork единого входа Azure AD необходима toohello tooknow hello vxMaintain аналог пользователя Azure AD. То есть необходимо установить связи между hello пользователя Azure AD и соответствующий пользователь vxMaintain hello.

tooestablish hello связи, назначьте hello vxMaintain **имя пользователя** значение как hello Azure AD **Username** значение.

tooconfigure и Azure AD SSO с помощью vxMaintain завершения hello следующие стандартные блоки тестов.

### <a name="configure-azure-ad-sso"></a>Настройка единого входа Azure AD

В этом разделе можно включить единый вход Azure AD в hello портал Azure и настройки единого входа в вашем приложении vxMaintain, выполнив hello ниже:

1. В hello в hello портала Azure **vxMaintain** странице интеграции приложений выберите **единого входа**.

    ![Здравствуйте, команда «Единый вход»][4]

2. tooenable единого входа, в hello **режим-** раскрывающемся списке выберите **входа на базе SAML**.
 
    ![Hello команды на основе SAML на «вход»](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_samlbase.png)

3. В разделе **vxMaintain URL-адреса и домена**, hello следующие:

    ![Здравствуйте, vxMaintain разделе URL-адреса и домена](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_url.png)

    а. В hello **идентификатор** введите URL-адрес имеет hello синтаксис:`https://<company name>.verisae.com`

    b. В hello **URL-адрес ответа** введите URL-адрес имеет hello синтаксис:`https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`

    > [!NOTE] 
    > Hello выше значения не являются реальными. Дополнить фактический идентификатор hello и URL-адрес ответа. значения tooobtain hello, обратитесь в службу hello [vxMaintain поддержки](http://www.verisae.com/contact-us).
 
4. В разделе **сертификат подписи SAML**выберите **метаданные в формате XML**и сохраните файл tooyour hello метаданных компьютера.

    ![раздел «Сертификат подписи SAML» Hello](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_certificate.png) 

5. Щелкните **Сохранить**.

    ![Кнопка "Сохранить" Hello](./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_400.png)

6. tooconfigure **vxMaintain** единого входа, загружаются hello отправки **метаданные в формате XML** файл toohello [vxMaintain поддержки](http://www.verisae.com/contact-us).

> [!TIP]
> При настройке приложения hello, могут читать четкими версию перед инструкции в hello hello [портал Azure](https://portal.azure.com). После добавления приложение hello с hello **Active Directory** > **корпоративных приложений** раздел, выберите hello **Single Sign-On** вкладку, а затем hello доступа внедренные документации из hello **конфигурации** раздела. 
>
>toolearn Дополнительные сведения о функции hello внедренные документации, в разделе [управление единого входа для корпоративных приложений](https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
В этом разделе создайте тестового пользователя Саймон Britta в hello портал Azure, выполнив hello ниже:

![Hello Azure AD тестового пользователя][100]

1. В hello **портал Azure**в левой области hello, выберите hello **Azure Active Directory** кнопки.

    ![Кнопка «Azure Active Directory» Hello](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_01.png) 

2. список пользователей, toodisplay go слишком**пользователей и групп** > **всех пользователей**.
    
    ![Здравствуйте, «Все пользователи» ссылки](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)  
    Hello **всех пользователей** откроется диалоговое окно. 

3. tooopen hello **пользователя** выберите **добавить**.
 
    ![Кнопка "Добавить" Hello](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_03.png) 

4. В hello **пользователя** диалогового окна поле, hello следующие:
 
    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** поле введите адрес электронной почты hello тестового пользователя Саймон Britta.

    c. Выберите hello **Показать пароль** флажок, а затем значение hello примечание, созданный в hello **пароль** поле.

    d. Нажмите кнопку **Создать**.
 
### <a name="create-a-vxmaintain-test-user"></a>Создание тестового пользователя vxMaintain

В этом разделе вы создадите тестового пользователя Britta Simon в vxMaintain. Пользователи tooadd на платформе vxMaintain hello, работать с [vxMaintain поддержки](http://www.verisae.com/contact-us). Прежде чем использовать единый вход, создание и активация пользователей hello.

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите тестового пользователя toouse Britta Simon Azure единого входа путем предоставления доступа toovxMaintain. toodo таким образом, hello следующие:

![Тестовый пользователь в списке отображаемое имя hello][200] 

1. В hello портал Azure **приложений** просмотреть, перейдите в слишком**каталога** представление > **корпоративных приложений** > **всех приложений**.

    ![Здравствуйте, «Все приложения» ссылки][201] 

2. В hello **приложений** выберите **vxMaintain**.

    ![ссылка vxMaintain Hello](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_app.png) 

3. Выберите в левой области hello **пользователей и групп**.

    ![Hello ссылку «Пользователи и группы»][202] 

4. Выберите **добавить** и затем в hello **добавить назначение** выберите **пользователей и групп**.

    ![Hello ссылку «Пользователи и группы»][203]

5. В hello **пользователей и групп** диалогового окна hello **пользователей** выберите **Britta Simon**и затем выберите hello **выберите** кнопки.

7. В hello **добавить назначение** выберите **назначить**.
    
### <a name="test-your-azure-ad-single-sign-on"></a>Проверка единого входа Azure AD

В этом разделе можно проверить конфигурацию единого входа Azure AD с помощью панели доступа hello.

Выбор hello **vxMaintain** плитки в панели доступа hello следует приложения vxMaintain tooyour автоматического входа.

Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="next-steps"></a>Дальнейшие действия

* [Список руководств по интеграции приложений SaaS с Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_203.png

