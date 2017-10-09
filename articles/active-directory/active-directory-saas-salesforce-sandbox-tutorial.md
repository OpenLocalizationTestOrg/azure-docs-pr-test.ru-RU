---
title: "Руководство по интеграции Azure Active Directory с песочницей Salesforce | Документация Майкрософт"
description: "Узнайте, как toouse песочницы Salesforce с Azure Active Directory tooenable единого входа, автоматизированной подготовки и многое другое!."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: deccd6a07b57c8ba56b7e1c3f3ab311813ca017b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a>Учебник. Интеграция Azure Active Directory с песочницей Salesforce

Цель этого учебника Hello — tooshow hello интеграцию Azure и песочницы Salesforce.  

>[!TIP]
>Для обратной связи, в разделе hello [страницы поддержки Azure](http://go.microsoft.com/fwlink/?LinkId=521878). 
> 

"Песочницы" предоставляют вы hello возможность toocreate несколько копий организации в отдельных средах для разных целей: разработки, тестирования и обучения — без нарушения hello данных и приложений в вашей рабочей среде Salesforce организация.  

Дополнительные сведения см. в [статье о песочницах](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US).

Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:

* Действующая подписка на Azure
* Песочница на сайте Salesforce.com.

Если вы еще нет действительной песочницы в Salesforce.com, то необходимо toocontact Salesforce.

Hello сценарий, описанный в этом руководстве состоит из hello следующие стандартные блоки.

1. Включение интеграции приложений hello для песочницы Salesforce
2. Настройка единого входа.
3. Включение домена
4. Настройка подготовки учетных записей пользователей
5. Назначение пользователей

![Сценарий](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "Сценарий")

## <a name="enable-hello-application-integration-for-salesforce-sandbox"></a>Включить hello интеграции приложений для песочницы Salesforce
Hello цель этого раздела — toooutline как интеграция приложения hello tooenable для песочницы Salesforce.

**Интеграция приложения hello tooenable для песочницы Salesforce, выполните hello следующие шаги.**

1. В hello классический портал Azure, hello левой области навигации, выберите **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")
2. Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.
3. Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.
   
   ![Приложения](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "Приложения")
4. tooopen hello **коллекцию приложений**, нажмите кнопку **добавить приложение**и нажмите кнопку **добавить приложение для моей организации toouse**.
   
   ![Что вам требуется toodo? ] (./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "Что вам требуется toodo?")
5. В hello **поле поиска**, тип **песочницы Salesforce**.
   
   ![Коллекция приложений](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "Коллекция приложений")
6. В области результатов hello выберите **песочницы Salesforce**и нажмите кнопку **завершить** tooadd приложения hello.
   
   ![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce Sandbox")
   
## <a name="configur-single-sign-on-sso"></a>Настройка единого входа

Цель этого раздела Hello — toooutline как tooSalesforce tooauthenticate tooenable пользователей с учетной записью в Azure AD, используя федерацию на основе hello SAML протокола.

**tooconfigure единого входа, выполните следующие шаги hello:**

1. В классический портал Azure, на hello hello **песочницы Salesforce** странице интеграции приложения щелкните **настроить единый вход** tooopen hello **Настройка единого входа** диалоговое окно.
   
   ![Настройка единого входа](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "Настройка единого входа")
2. На hello **предпочитаемый как toosign пользователей на tooSalesforce "песочницы"** выберите **Microsoft Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.
   
   ![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce Sandbox")
3. На hello **настроить URL-адрес приложения** страницы в hello **на URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello `http://company.my.salesforce.com`и нажмите кнопку **Далее**.
   
   ![Настройка URL-адреса приложения](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "Настройка URL-адреса приложения")
4. Если вы уже настроили единого входа для другого экземпляра песочницы Salesforce в вашем каталоге, то необходимо также настроить hello **идентификатор** toohave hello совпадает со значением hello **URL-адрес входа**. 
 * Hello **идентификатор** поле можно найти путем проверки hello **Показывать дополнительные параметры** флажок на hello **настроить URL-адрес приложения** страницы диалогового окна "hello".
5. На hello **настройки единого входа в песочницу Salesforce** щелкните **загрузки сертификата**, а затем сохраните файл сертификата hello на компьютере.
   
   ![Настройка единого входа](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "Настройка единого входа")
6. В другом окне веб-браузера войдите в свою песочницу Salesforce в качестве администратора.
7. В меню в верхней части hello hello выберите **установки**.
   
   ![Настройка](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Настройка")
8. Hello hello левой панели навигации щелкните **управления безопасностью**, а затем нажмите кнопку **параметры единого входа**.
   
   ![Параметры единого входа](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "Параметры единого входа")
9. На hello раздел параметров единого входа выполните следующие шаги hello.
   
   ![Параметры единого входа](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "Параметры единого входа")  
 1.  Установите флажок **SAML включен**. 
 2.  Нажмите кнопку **Создать**.
10. На hello SAML единого входа «параметры» выполните следующие шаги hello.
    
    ![Параметры единого входа SAML](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "Параметры единого входа SAML")  
 1. Hello в текстовое поле имя, введите имя hello hello конфигурации (например: *SPSSOWAAD\_тест*). 
 2. В классический портал Azure, на hello hello **настройки единого входа в песочницу Salesforce** диалоговой страницы, копировать hello **URL-адрес издателя** значение, а затем вставьте его в hello **издателя**текстового поля.
 3. В hello **идентификатор сущности** введите **https://test.salesforce.com** Если hello добавляется каталог tooyour первый экземпляр песочницы Salesforce. При добавлении экземпляра песочницы Salesforce, а затем для hello **идентификатор сущности** типа в hello **на URL-адрес входа**, которые должны быть в следующем формате:`http://company.my.salesforce.com`   
 4. Нажмите кнопку **Обзор** tooupload hello загрузить сертификат.  
 5. Как **типа удостоверения SAML**выберите **утверждение, содержащее hello идентификатор федерации из объекта пользователя hello**. 
 6. Как **расположения удостоверения SAML**выберите **удостоверение находится в элемент hello NameIdentifier оператора Subject hello**.
 7. В классический портал Azure, на hello hello **настройки единого входа в песочницу Salesforce** диалоговой страницы, копировать hello **URL-адрес удаленного входа** значение, а затем вставьте его в hello **поставщика удостоверений URL-адрес входа** текстового поля. 
 8. SFDC не поддерживает выход SAML.  Чтобы избежать этого, вставьте «https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0» в hello **URL-адрес выхода поставщика удостоверений** текстового поля.
 9. В поле **Service Provider Initiated Request Binding** (Связывание запросов, инициированных поставщиком услуг) выберите значение **HTTP POST**. 
 10. Щелкните **Сохранить**.
11. На hello классический портал Azure, выберите Подтверждение настройки единого входа hello и нажмите кнопку **завершить** tooclose hello **Настройка единого входа** диалогового окна.
    
    ![Настройка единого входа](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "Настройка единого входа")

## <a name="enable-your-domain"></a>Включение домена
В этом разделе предполагается, что вы уже создали домен.  Дополнительные сведения см. в разделе об [определении имени домена](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).

**tooenable к домену, выполните следующие шаги hello:**

1. Hello панели навигации слева щелкните **Управление доменами**, а затем нажмите кнопку **Мой домен.**
   
   ![Мой домен](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "Мой домен")
   
   >[!NOTE]
   >Убедитесь в правильности настройки домена. 
   > 
2. В hello **параметры страницы входа** щелкните **изменить**, затем, по мере **службы проверки подлинности**, выберите имя hello hello SAML единого входа параметр из предыдущего hello статьи, а затем щелкните **Сохранить**.
   
   ![Мой домен](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "Мой домен")

Как только домен настроен, пользователям следует использовать hello домена URL-адрес toologin toohello песочницы Salesforce.  

значение hello tooget hello URL-адреса, щелкните профиль единого входа hello, созданный в предыдущем разделе hello.

## <a name="configure-user-provisioning"></a>Настроить подготовку учетных записей пользователей
Цель этого раздела Hello является toooutline как tooenable пользователя Подготовка пользователя Active Directory учетных записей tooSalesforce "песочницы".

**tooconfigure подготовки пользователей, выполните следующие шаги hello.**

1. На портале Salesforce hello hello верхней панели навигации выберите ваш tooexpand имя меню пользователя:
   
   ![Мои параметры](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "Мои параметры")
2. Меню пользователя, выберите **мои параметры** tooopen вашей **мои параметры** страницы.
3. Hello левой панели щелкните **личных** tooexpand hello личный раздел, а затем нажмите кнопку **Сброс личного токена безопасности**:
   
   ![Мои параметры](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "Мои параметры")
4. На hello **Сброс личного токена безопасности** щелкните **сбросить токен безопасности** toorequest сообщение электронной почты, содержащее ваш токен безопасности Salesforce.com.
   
   ![Новый маркер](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "Новый маркер")
5. Проверьте папку "Входящие" электронной почты на наличие сообщения от Salesforce.com со строкой темы**salesforce.com.com security confirmation**.
6. Просмотрите этот электронной почты и скопируйте hello значение токена безопасности.
7. В классический портал Azure, на hello hello **песочницы salesforce** странице интеграции приложения щелкните **Настройка подготовки пользователя** tooopen hello **Настройка подготовки пользователя**диалогового окна.
   
   ![Настроить подготовку учетных записей пользователей](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "Настроить подготовку учетных записей пользователей")
8. На hello **введите вашей песочницы Salesforce учетные данные tooenable автоматическую подготовку пользователей** укажите следующие параметры конфигурации hello:
   
   ![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce Sandbox")   
 1. В hello **имя пользователя администратора песочницы Salesforce** введите имя учетной записи Salesforce, имеет hello **системный администратор** профиля в Salesforce.com.
 2. В hello **пароль администратора песочницы Salesforce** текстового поля, типа hello пароль для этой учетной записи.
 3. В hello **токен безопасности пользователя** текстовое значение токена безопасности hello вставки.
 4. Нажмите кнопку **проверки** tooverify конфигурации.
 5. Нажмите кнопку hello **Далее** hello tooopen кнопку **Подтверждение** страницы.
9. На hello **Подтверждение** щелкните **завершить** toosave конфигурации.
   
## <a name="assigning-users"></a>Назначение пользователей

tootest конфигурацию, необходимо toogrant hello Azure AD пользователей с помощью tooit доступ вашего приложения путем назначения им tooallow.

**Пользователи tooassign tooSalesforce "песочницы", выполните hello следующие шаги.**

1. В hello классический портал Azure создайте тестовую учетную запись.
2. На hello ** песочницы Salesforce ** странице интеграции приложения щелкните **назначить пользователей**.
   
   ![Назначение пользователей](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "Назначение пользователей")
3. Выберите тестового пользователя, нажмите кнопку **назначить**, а затем нажмите кнопку **Да** tooconfirm назначения.
   
   ![Да](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Да")

Теперь следует подождать 10 минут и убедиться в устранении учетной записи hello синхронизированные tooSalesforce "песочницы".

Tootest параметры единого входа, откройте панель доступа hello. Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](https://msdn.microsoft.com/library/dn308586).

