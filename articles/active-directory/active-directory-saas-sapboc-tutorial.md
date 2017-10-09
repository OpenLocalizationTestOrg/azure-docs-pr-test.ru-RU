---
title: "Руководство по интеграции Azure Active Directory с SAP Business Object Cloud | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и облаком объекта SAP Business."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 6c5e44f0-4e52-463f-b879-834d80a55cdf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: a3e9bd93897271531f91bcbc50cd361e8a20551e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-object-cloud"></a>Руководство по интеграции Azure Active Directory с SAP Business Object Cloud

В этом учебнике вы узнаете, как toointegrate SAP Business объекта облака в Azure Active Directory (Azure AD).

Вы получаете hello при интеграции SAP Business объекта облака в Azure AD следующие преимущества:

- В Azure AD можно управлять, у кого есть доступ tooSAP объекта облачные бизнес.
- Вы автоматически вход вашей tooSAP пользователей облака объект бизнес с помощью единого входа и учетная запись пользователя Azure AD.
- Вы можете управлять учетными записями в один, централизованно, hello портал Azure.

toolearn Дополнительные сведения о программное обеспечение как услуга (SaaS) интеграции приложений с Azure AD, в разделе [доступ к приложению и единый вход в Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooset интеграции с Azure AD с облаком объекта SAP Business необходимо hello следующих элементов:

- подписка Azure AD;
- подписка SAP Business Object Cloud с поддержкой единого входа.

> [!NOTE]
> Если вы тестируете hello шаги в этом учебнике, мы рекомендуем не проверяют их в рабочей среде.

Рекомендации для тестирования hello шаги в этом учебнике.

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить бесплатную пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. 

Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление объекта облака SAP Business из коллекции hello.
2. Настройка и проверка единого входа Azure AD.

## <a name="add-sap-business-object-cloud-from-hello-gallery"></a>Добавление объекта облака SAP Business из коллекции hello
tooset hello интеграции облачных объекта Business SAP в Azure AD в галерее hello, добавить объект облака SAP Business tooyour список управляемых приложений SaaS.

tooadd SAP Business объекта облака из галереи hello:

1. В hello [портал Azure](https://portal.azure.com)в левом меню hello, выберите **Azure Active Directory**. 

    ![Кнопка Hello Azure Active Directory][1]

2. Перейдите в колонку **Корпоративные приложения** и выберите **Все приложения**.

    ![страница приложений корпоративного Hello][2]
    
3. Выберите новое приложение tooadd **новое приложение**.

    ![Кнопка нового приложения Hello][3]

4. Введите в поле поиска hello, **SAP Business объекта облака**.

    ![поле поиска Hello](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_search.png)

5. В панели результатов hello, выберите **SAP Business объекта облака**и выберите **добавить**.

    ![SAP Business объекта облака в списке результатов hello](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_addfromgallery.png)

##  <a name="set-up-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа Azure AD

В этом разделе описана настройка и проверка единого входа Azure AD в SAP Business Object Cloud с использованием тестового пользователя *Britta Simon*.

Для единого входа toowork Azure AD требуется пользователь аналог tooknow hello Azure AD в облаке объекта SAP Business. Ссылочное отношение между пользователем Azure AD и hello связанных пользователей в облаке объекта SAP Business должно быть установлено.

tooestablish hello ссылка связи в облаке объекта SAP Business, **Username**, присвойте значение hello hello **имя пользователя** в Azure AD.

tooconfigure и теста Azure AD единого входа с бизнес объектом SAP облака, полный hello следующие задачи:

1. [Настройка единого входа Azure AD](#set-up-azure-ad-single-sign-on) Настраивает эту функцию toouse пользователя.
2. [Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user) Тесты Azure AD единого входа с пользователем hello Саймон Britta.
3. [Создание тестового пользователя SAP Business Object Cloud](#create-an-sap-business-object-cloud-test-user) Создает аналог Саймон Britta в SAP Business объекта облака, связанного toohello представление hello пользователя Azure AD.
4. [Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user). Устанавливает toouse Britta Simon Azure AD единого входа.
5. [Проверка единого входа](#test-single-sign-on) Подтверждает, что эта конфигурация hello работает.

### <a name="set-up-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе включении Azure AD одним входом в портал Azure hello. и настроить его в приложении SAP Business Object Cloud.

tooset копирование Azure AD единого входа с облаком объекта SAP Business:

1. В hello в hello портала Azure **SAP Business объекта облака** странице интеграции приложений выберите **единого входа**.

    ![Выбор параметра "Единый вход"][4]

2. На hello **единого входа** страницы, для **режим**выберите **входа на базе SAML**.
 
    ![Выбор параметра "Вход на основе SAML"](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_samlbase.png)

3. В разделе **SAP бизнес-объекта облачной среде и URL-адреса**полный hello следующие действия:

    1. В hello **URL-адрес входа** введите URL-адрес, имеющий hello следующий шаблон: 
    | |
    |-|-|
    | `https://<sub-domain>.sapanalytics.cloud/` |
    | `https://<sub-domain>.sapbusinessobjects.cloud/` |

    2. В hello **идентификатор** введите URL-адрес, имеющий hello следующий шаблон:
    | |
    |-|-|
    | `<sub-domain>.sapbusinessobjects.cloud` |
    | `<sub-domain>.sapanalytics.cloud` |

    ![Домены и URL-адреса приложения SAP Business Object Cloud](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_url.png)
 
    > [!NOTE] 
    > значения Hello в эти URL-адреса являются исключительно для демонстрационных целей. Обновление hello значениями hello фактическое входа URL-адрес и идентификатор URL-адрес. tooget hello URL-адрес входа, обратитесь в службу hello [группа поддержки SAP Business объекта облака клиента](https://www.sap.com/product/analytics/cloud-analytics.support.html). URL-адрес идентификатора hello можно получить, загрузив hello SAP Business объекта облачных метаданных из консоли администрирования hello. Это объясняется далее в учебнике hello. 

4. В разделе **Сертификат подписи SAML** выберите **XML метаданных**. Сохраните файл метаданных hello на вашем компьютере.

    ![Выбор XML метаданных](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_certificate.png) 

5. Щелкните **Сохранить**.

    ![Нажатие кнопки "Сохранить"](./media/active-directory-saas-sapboc-tutorial/tutorial_general_400.png)

6. В другом окне браузера Войдите на сайте компании SAP Business объекта облака tooyour с правами администратора.

7. Выберите **Меню** > **Система** > **Администрирование**.
    
    ![Выбор параметров "Меню", "Система" и "Администрирование"](./media/active-directory-saas-sapboc-tutorial/config1.png)

8. На hello **безопасности** вкладке, выберите hello **изменить** значок (перо).
    
    ![На вкладке Безопасность hello выберите значок редактирования hello](./media/active-directory-saas-sapboc-tutorial/config2.png)  

9. В качестве **метода проверки подлинности** выберите **SAML Single Sign-On (SSO)** (Единый вход SAML (SSO)).

    ![Выберите SAML Single Sign-On для метода проверки подлинности hello](./media/active-directory-saas-sapboc-tutorial/config3.png)  

10. toodownload hello поставщика метаданных службы (шаг 1) выберите **загрузить**. В файле метаданных hello, найдите и скопируйте hello **entityID** значение. В hello Azure портала в разделе **SAP бизнес-объекта облачной среде и URL-адреса**, вставьте значение hello в hello **идентификатор** поле.

    ![Скопируйте и вставьте значение entityID hello](./media/active-directory-saas-sapboc-tutorial/config4.png)  

11. tooupload hello поставщика метаданных службы (шаг 2) в файле hello, загруженного из hello портал Azure в разделе **метаданных поставщика удостоверений отправить**выберите **отправить**.  

    ![Нажатие кнопки "Отправить" в разделе Upload Identity Provider metadata (Отправить метаданные поставщика удостоверений)](./media/active-directory-saas-sapboc-tutorial/config5.png)

12. В hello **атрибут пользователя** список атрибутов пользователя выберите hello (шаг 3), требуется toouse вашей реализации. Этот атрибут пользователя сопоставляет toohello поставщика удостоверений. пользовательский атрибут на странице приветствия пользователя, используйте hello tooenter **пользовательские сопоставления SAML** параметр. Или можно выбрать либо **электронной почты** или **идентификатор пользователя** как атрибут пользователя hello. В нашем примере мы выбрали **электронной почты** так, как мы сопоставим hello утверждение идентификатора пользователя с hello **userprincipalname** атрибута в hello **атрибуты пользователя** раздела hello Портал Azure. Это обеспечивает уникальный адрес электронной почты пользователя, который отправляется toohello SAP Business объекта облачного приложения в каждом успешный ответ SAML.

    ![Выбор атрибута пользователя](./media/active-directory-saas-sapboc-tutorial/config6.png)

13. Учетная запись hello tooverify с поставщиком удостоверений hello (шаг 4) в hello **учетные данные входа (электронной почты)** введите адрес электронной почты пользователя hello. Выберите **Проверить учетную запись**. система Hello Добавление учетной записи пользователя toohello учетных данных для входа.

    ![Ввод электронного адреса и нажатие кнопки "Проверить учетную запись"](./media/active-directory-saas-sapboc-tutorial/config7.png)

14. Выберите hello **Сохранить** значок.

    ![Значок "Сохранить"](./media/active-directory-saas-sapboc-tutorial/save.png)

> [!TIP]
> Можно прочитать краткое версии этих инструкций в hello [портал Azure](https://portal.azure.com), тогда как при настройке приложения! После добавления приложения hello, выбрав **Active Directory** > **корпоративных приложений**выберите hello **Single Sign-On** вкладки. Можно получить доступ к документации hello внедрены в hello **конфигурации** раздел hello нижней части страницы приветствия. Чтобы узнать больше, ознакомьтесь со [встроенной документацией по Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
В этом разделе создайте тестового пользователя с именем Britta Simon в hello портал Azure.

toocreate тестового пользователя в Azure AD:

1. В hello в левом меню hello, портале Azure выберите **Azure Active Directory**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_01.png) 

2. toodisplay hello список пользователей, выберите **пользователей и групп**, а затем выберите **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** выберите **добавить**.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_03.png) 

4. В hello **пользователя** диалоговое окно, полный hello, следующие шаги:
 
    1. В hello **имя** введите **BrittaSimon**.

    2. В hello **имя пользователя** введите адрес электронной почты hello hello пользователя Саймон Britta.

    3. Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.

    4. Нажмите кнопку **Создать**.

        ![диалоговое окно приветствия пользователя](./media/active-directory-saas-sapboc-tutorial/create_aaduser_04.png) 

    ![Создание пользователя Azure AD][100]

### <a name="create-an-sap-business-object-cloud-test-user"></a>Создание тестового пользователя SAP Business Object Cloud

Необходимо подготовить пользователей Azure AD в облаке объекта SAP Business, прежде чем они смогут войти в tooSAP объекта облачные бизнес. В SAP Business Object Cloud подготовка выполняется вручную.

tooprovision учетной записи пользователя:

1. Войдите в tooyour SAP Business объекта облаке на сайте компании от имени администратора.

2. Выберите **Меню** > **Безопасность** > **Пользователи**.

    ![Добавление сотрудника](./media/active-directory-saas-sapboc-tutorial/user1.png)

3. На hello **пользователей** , tooadd новые сведения о пользователе, выберите  **+** . 

    ![Страница добавления пользователей](./media/active-directory-saas-sapboc-tutorial/user4.png)

    Затем выполните следующие шаги hello:

    1. В hello **идентификатор пользователя** введите идентификатор hello hello пользователя, таких как **Britta**.

    2. В hello **имя** введите имя первого hello hello пользователя, таких как **Britta**.

    3. В hello **ФАМИЛИЯ** введите hello фамилию пользователя hello, таких как **Simon**.

    4. В hello **ОТОБРАЖАЕМОЕ имя** введите полное имя пользователя hello hello как **Britta Simon**.

    5. В hello **электронной почты** введите адрес электронной почты hello hello пользователя, как  **brittasimon@contoso.com** .

    6. На hello **Выбор ролей** выберите hello соответствующую роль для пользователя hello и затем выберите **ОК**.

      ![Выбрать роль](./media/active-directory-saas-sapboc-tutorial/user3.png)

    7. Выберите hello **Сохранить** значок.  


### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе позволяют hello пользователя Britta Simon toouse Azure AD единого входа путем предоставления hello пользователя учетной записи доступа tooSAP объекта облачные бизнес.

tooassign tooSAP Britta Simon объекта облачные бизнес:

1. В hello портал Azure откройте представление приложения hello, а затем перейдите toohello представления каталога. Перейдите в колонку **Корпоративные приложения** и выберите **Все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **SAP Business объекта облака**.

    ![Настройка единого входа](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_app.png) 

3. Выберите в меню слева hello, **пользователей и групп**.

    ![Выбор параметра "Пользователи и группы"][202] 

4. Выберите **Добавить**. Затем на hello **добавить назначение** выберите **пользователей и групп**.

    ![Страница добавления назначения Hello][203]

5. На hello **пользователей и групп** страницы в список пользователей, выберите hello **Britta Simon**.

6. На hello **пользователей и групп** выберите **выберите**.

7. На hello **добавить назначение** выберите **назначить**.

![Назначение пользователям ролей hello][200] 
    
### <a name="test-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При выборе hello объекта облака SAP Business плитки в панели доступа hello вы должны автоматически входить в tooyour SAP Business объекта облачного приложения.

Дополнительные сведения о панели доступа hello см. в разделе [панели доступа введение toohello](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по toointegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_203.png

