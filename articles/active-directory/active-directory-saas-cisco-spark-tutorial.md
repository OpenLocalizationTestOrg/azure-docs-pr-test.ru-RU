---
title: "Учебник. Интеграция Azure Active Directory с Cisco Spark | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Cisco Spark."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c47894b1-f5df-4755-845d-f12f4c602dc4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 386c4fd816095e1c61de01dd1dee1bbd00311a04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-spark"></a>Учебник. Интеграция Azure Active Directory с Cisco Spark

В этом учебнике вы узнаете, как toointegrate Cisco усилить с Azure Active Directory (Azure AD).

Интеграция Cisco Spark в Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooCisco Spark
- Можно включить на пользователей tooautomatically get вошедшего tooCisco Spark (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Cisco Spark требуется hello следующих элементов:

- подписка Azure AD;
- подписка Cisco Spark с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Cisco Spark из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-cisco-spark-from-hello-gallery"></a>Добавление Cisco Spark из галереи hello
tooconfigure hello интеграции Cisco Spark в Azure AD, вы должны tooadd Cisco Spark из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Spark Cisco из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Cisco Spark**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_search.png)

5. В панели результатов hello выберите **Cisco Spark**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Cisco Spark с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Cisco Spark является tooa в Azure AD. Другими словами связи между пользователя Azure AD и hello связанных пользователей в Cisco Spark должен установить toobe.

В Cisco Spark, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Cisco Spark, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Cisco Spark](#creating-a-cisco-spark-test-user)**  -toohave аналог Саймон Britta в Spark Cisco, представление связанных toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Cisco Spark.

**tooconfigure Azure AD единого входа с Cisco Spark, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Cisco Spark** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_samlbase.png)

3. На hello **URL-адреса и домена Spark Cisco** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес как:`https://web.ciscospark.com/#/signin`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://idbroker.webex.com/<companyname>`

    > [!NOTE] 
    > Это значение приведено для справки. Измените значение этого параметра hello фактический идентификатор. Обратитесь к [группа поддержки клиента Cisco Spark](https://support.ciscospark.com/) tooget это значение. 
 
4. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_certificate.png) 

5. Cisco Spark приложение ожидает, что определенные атрибуты утверждения SAML toocontain hello. Настройте следующие атрибуты для данного приложения hello. Вы можете управлять hello значения этих атрибутов из hello **атрибуты пользователя** раздел на странице интеграции приложений. пример Hello следующий снимок экрана для этого.
    
    ![Настройка единого входа](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_07.png) 

6. В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна, настроить атрибутов токена SAML, как показано в приведенном выше рисунке hello и выполнять hello следующие шаги:
    
    | Имя атрибута  | Значение атрибута |
    | --------------- | -------------------- |    
    |   uid    | user.userprincipalname |   

    а. Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.

    ![Настройка единого входа](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_04.png)

    ![Настройка единого входа](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_05.png)
    
    b. В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.
    
    c. Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.
    
    d. Нажмите кнопку **ОК**.

7. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_400.png)

8. Войдите в слишком[управления совместной работы облачной Cisco](https://admin.ciscospark.com/) с учетными данными администратора.

9. Выберите **параметры** и на странице приветствия **проверки подлинности** щелкните **изменить**.
   
    ![Настройка единого входа](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_10.png)
    
10. Выберите **Integrate a 3rd-party identity provider. (Дополнительно)**  и последовательно выберите toohello следующий экран.

11. На hello **импортировать метаданные поставщика удостоверений** страница, либо перетащите файл метаданных hello Azure AD на странице приветствия или использовать браузер параметр hello файл toolocate и отправить файл метаданных hello Azure AD. Затем выберите **Require certificate signed by a certificate authority in Metadata (more secure)** (Требовать наличия в метаданных сертификата, подписанного центром сертификации) и нажмите кнопку **Next** (Далее). 
    
    ![Настройка единого входа](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_11.png)

12. Выберите **Test SSO Connection** (Проверить подключение для единого входа) и, когда откроется новая вкладка браузера, пройдите аутентификацию Azure AD, выполнив вход.

13. Вернуть toohello **управления совместной работы облачной Cisco** вкладка «браузер». При успешном выполнении теста hello выберите **это проверка выполнена успешно. Enable Single Sign-On option** (Этот тест прошел успешно. Включить единый вход) и нажмите кнопку **Next** (Далее).

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-cisco-spark-test-user"></a>Создание тестового пользователя Cisco Spark

В этом разделе описано, как создать пользователя Britta Simon в Cisco Spark. В этом разделе описано, как создать пользователя Britta Simon в Cisco Spark.

1. Go toohello [управления совместной работы облачной Cisco](https://admin.ciscospark.com/) с учетными данными администратора.

2. Щелкните **Пользователи** и **Управление пользователями**.
   
    ![Настройка единого входа](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_12.png) 

3. В hello **управление пользовательскими** выберите **вручную добавить или изменить пользователей** и нажмите кнопку **Далее**.

4. Выберите **Names and Email address** (Имя, фамилия и электронный адрес). Затем заполните hello текстовом поле следующим образом:
   
    ![Настройка единого входа](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_13.png) 
    
    а. В hello **имя** введите **Britta**. 
    
    b. В hello **Фамилия** введите **Simon**.
    
    c. В hello **адрес электронной почты** введите  **britta.simon@contoso.com** .

5. Нажмите кнопку hello, а также tooadd Britta Simon входа. Затем щелкните **Далее**.

6. В hello **Добавление служб для пользователей** окно, нажмите кнопку **Сохранить** и затем **Готово**.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooCisco Spark.

![Назначение пользователя][200] 

**tooassign tooCisco Britta Simon Spark, выполните hello следующие шаги.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Cisco Spark**.

    ![Настройка единого входа](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".

Если щелкнуть плитку Cisco Spark hello в hello панели доступа, вы должны получить tooyour автоматически вошедшего Cisco Spark приложения.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_060.png
[100]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_203.png

