---
title: "Руководство по интеграции Azure Active Directory с NetSuite | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Netsuite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dafa0864-aef2-4f5e-9eac-770504688ef4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7cf205d5bda5333872fb589e57f4779a8670b595
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netsuite"></a>Руководство по интеграции Azure Active Directory с NetSuite

В этом учебнике вы узнаете, как toointegrate Netsuite с Azure Active Directory (Azure AD).

Интеграция Netsuite с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooNetsuite
- Можно включить на пользователей tooautomatically get вошедшего tooNetsuite (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Netsuite требуется hello следующих элементов:

- подписка Azure AD;
- подписка Netsuite с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Netsuite из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-netsuite-from-hello-gallery"></a>Добавление Netsuite из галереи hello
tooconfigure hello интеграции Netsuite в Azure AD, вы должны tooadd Netsuite из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Netsuite из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. Нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна "hello".

    ![Приложения][3]

4. Введите в поле поиска hello **Netsuite**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_search.png)

5. В панели результатов hello выберите **Netsuite**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в приложение Netsuite с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Netsuite является tooa в Azure AD. Иными словами связи между пользователя Azure AD и hello связанных пользователей в Netsuite требуется установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Netsuite.

tooconfigure и теста Azure AD единого входа с Netsuite, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Netsuite](#creating-a-netsuite-test-user)**  -toohave аналог Саймон Britta в Netsuite, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в свое приложение Netsuite.

**Azure AD tooconfigure единого входа с Netsuite, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Netsuite** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_samlbase.png)

3. На hello **URL-адреса и домена Netsuite** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_url.png)

    В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello: `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs``https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`

    > [!NOTE] 
    > Это значение приведено для примера. Значение hello обновления с hello фактический URL-адрес ответа. Обратитесь к [Netsuite поддержки](http://www.netsuite.com/portal/services/support.shtml) tooget это значение.
 
4. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.

    ![Настройка единого входа](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-netsuite-tutorial/tutorial_general_400.png)

6. На hello **конфигурации Netsuite** щелкните **Настройка Netsuite** tooopen **Настройка входа** окна. Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_configure.png) 

7. Откройте новую вкладку в браузере и войдите как администратор корпоративного сайта NetSuite.

8. Щелкните hello панели инструментов вверху hello страницы приветствия **установки**, нажмите кнопку **диспетчер установки**.

    ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

9. Из hello **задачи настройки** выберите **интеграции**.

    ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-integration.png)

10. В hello **управление проверкой подлинности** щелкните **SAML Single Sign-on**.

    ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-saml.png)

11. На hello **Настройка SAML** выполните следующие шаги hello:
   
    а. Копировать hello **SAML единого входа URL-адрес службы** значение из **краткий справочник** раздел **Настройка входа** и вставьте его в hello **поставщика удостоверений Страница входа** в Netsuite.

    ![Настройка единого входа](./media/active-directory-saas-netsuite-tutorial/ns-saml-setup.png)
  
    b. В NetSuite выберите раздел **Primary Authentication Method** (Основной метод проверки подлинности).

    c. Для hello поля с меткой **метаданные поставщика удостоверений SAMLV2**выберите **отправьте файл метаданных поставщика Удостоверений**. Нажмите кнопку **Обзор** tooupload hello метаданные файла, загруженного с портала Azure.

    ![Настройка единого входа](./media/active-directory-saas-netsuite-tutorial/ns-sso-setup.png)

    г) Нажмите кнопку **Submit**(Отправить).

12. В Azure AD установите флажок **Просмотреть и изменить все другие атрибуты пользователей** и добавьте атрибут.

    ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-attributes.png)

13. Для hello **имя атрибута** введите в `account`. Для hello **значение атрибута** введите идентификатора учетной записи в Netsuite. Это значение является константой, а изменение с записью. Инструкции о том, как toofind свой идентификатор учетной записи приведены ниже:

      ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-add-attribute.png)

    а. В Netsuite, щелкните **установки** меню hello верхней панели навигации.

    b. Выберите в списке hello **задачи настройки** раздел hello левом меню навигации, выберите hello **интеграции** и нажмите кнопку **предпочтений относительно служб Web**.

    c. Ваш ИД учетной записи Netsuite скопируйте и вставьте его в hello **значение атрибута** в Azure AD.

    ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-account-id.png)

14. Прежде чем пользователи могут выполнять единый вход в Netsuite, их необходимо сначала назначить hello соответствующие разрешения в Netsuite. Следуйте инструкциям hello ниже tooassign эти разрешения.

    а. Hello верхней панели навигации выберите команду меню **установки**, нажмите кнопку **диспетчер установки**.
      
      ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    b. Выберите меню навигации слева hello **пользователи и роли**, нажмите кнопку **управление ролями**.
      
      ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-manage-roles.png)

    c. Нажмите кнопку **Создать роль**.

    d. Введите в **имя** для новой роли и выберите hello **единого входа только** флажок.
      
      ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-new-role.png)

    д. Щелкните **Сохранить**.

    f. В меню в верхней части hello hello выберите **разрешений**. Затем щелкните **Настройка**.
      
       ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-sso.png)

    g. Выберите **Set Up SAM Single Sign-on** (Настройка единого входа управления лицензиями) и нажмите кнопку **Add** (Добавить).

    h. Щелкните **Сохранить**.

    i. Hello верхней панели навигации выберите команду меню **установки**, нажмите кнопку **диспетчер установки**.
      
       ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    j. Выберите меню навигации слева hello **пользователи и роли**, нажмите кнопку **Управление пользователями**.
      
       ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-manage-users.png)

    k. Выберите тестового пользователя. Нажмите кнопку **Изменить**.
      
       ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-edit-user.png)

    l. В диалоговом окне приветствия ролей, выберите роль hello, вы создали и нажмите кнопку **добавить**.
      
       ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-add-role.png)

    m. Щелкните **Сохранить**.
    
> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_01.png) 

2.  hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_02.png) 

3. Вверху hello hello диалоговое окно, нажмите кнопку **добавить** tooopen hello **пользователя** диалогового окна.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**. 

### <a name="creating-a-netsuite-test-user"></a>Создание тестового пользователя Netsuite

В этом разделе вы создадите в Netsuite пользователя с именем Britta Simon. Netsuite поддерживает JIT-подготовку. Эта функция включена по умолчанию.
В этом разделе никакие действия с вашей стороны не требуются. Если пользователь еще не существует в Netsuite, создается новый, при попытке tooaccess Netsuite.


### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooNetsuite доступа.

![Назначение пользователя][200] 

**tooassign tooNetsuite Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Netsuite**.

    ![Настройка единого входа](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

tootest входа параметры единого, откройте hello панель доступа по адресу [https://myapps.microsoft.com](https://myapps.microsoft.com/)входа в hello тестовую учетную запись и нажмите кнопку **Netsuite**.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Руководство по настройке Google Apps для автоматической подготовки пользователей](active-directory-saas-netsuite-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_203.png

