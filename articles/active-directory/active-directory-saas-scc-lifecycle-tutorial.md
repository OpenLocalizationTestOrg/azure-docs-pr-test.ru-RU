---
title: "Руководство по интеграции Azure Active Directory с SCC LifeCycle | Документация Майкрософт"
description: "Узнайте, как toouse SCC LifeCycle с Azure Active Directory tooenable единого входа, автоматизированной подготовки и многое другое!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 9748bf38-ffc3-4d51-a1ae-207ce57104fa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: c10c313c5fc157ed70d2ccecfb930a8a765f8444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a>Учебник. Интеграция Azure Active Directory с SCC LifeCycle
Цель этого учебника Hello — tooshow hello интеграцию Azure и SCC LifeCycle.  

Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:

* Действующая подписка на Azure
* Подписка SCC LifeCycle с поддержкой единого входа.

После завершения этого учебника, Здравствуйте, пользователи Azure AD, назначенные tooSCC жизненного цикла будет может toosingle входа в приложение hello на корпоративном сайте SCC LifeCycle (инициированный поставщиком вход службы) или с помощью hello [введение Панель доступа toohello](active-directory-saas-access-panel-introduction.md).

Hello сценарий, описанный в этом руководстве состоит из hello следующие стандартные блоки.

1. Включение hello интеграции приложений для SCC LifeCycle
2. Настройка единого входа.
3. Настройка подготовки учетных записей пользователей
4. Назначение пользователей

![Сценарий](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Сценарий")

## <a name="enable-hello-application-integration-for-scc-lifecycle"></a>Включить hello интеграции приложений для SCC LifeCycle
Hello цель этого раздела — toooutline как интеграция приложения hello tooenable для SCC LifeCycle.

**Интеграция приложения hello tooenable для SCC LifeCycle, выполните hello следующие шаги.**

1. В hello классический портал Azure, hello левой области навигации, выберите **Active Directory**.
   
    ![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")
2. Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.
3. Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.
   
    ![Приложения](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "Приложения")
4. Нажмите кнопку **добавить** hello нижней части страницы приветствия.
   
    ![Добавление приложения](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Добавление приложения")
5. На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.
   
    ![Добавление приложения из коллекции](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Добавление приложения из коллекции")
6. В hello **поле поиска**, тип **SCC LifeCycle**.
   
    ![Коллекция приложений](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "Коллекция приложений")
7. В области результатов hello выберите **SCC LifeCycle**и нажмите кнопку **завершить** tooadd приложения hello.
   
    ![SCC LifeCycle](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")
   
## <a name="configure-single-sign-on"></a>Настройка единого входа

Цель этого раздела Hello — toooutline, каким образом пользователи tooenable tooauthenticate tooSCC жизненного цикла с помощью учетной записи в Azure AD, используя федерацию на основе hello SAML протокола.

**tooconfigure единого входа, выполните следующие шаги hello:**

1. В классический портал Azure, на hello hello **SCC LifeCycle** странице интеграции приложения щелкните **настроить единый вход** tooopen hello ** Настройка единого входа ** диалогового окна.
   
    ![Настройка единого входа](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Настройка единого входа")
2. На hello **предпочитаемый как toosign пользователей на tooSCC жизненного цикла** выберите **Microsoft Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.
   
    ![Настройка единого входа](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Настройка единого входа")
3. На hello **настроить URL-адрес приложения** страницы в hello **на URL-адрес входа** текстовое поле, введите URL-адрес hello используется ваш toosign пользователей на tooyour SCC LifeCycle приложения, используя следующий шаблон hello»*https:// bs1.SCC.com/lc7/Welcome/Customer/PICTtest.aspx*», а затем нажмите кнопку **Далее**.
   
    ![Настройка URL-адреса приложения](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "Настройка URL-адреса приложения")
4. На hello **настройки единого входа в SCC LifeCycle** щелкните **загрузить метаданные**, а затем сохраните файл метаданных на локальном компьютере.
   
   ![Настройка единого входа](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Настройка единого входа")
5. Пересылка этого tooSCC файл метаданных группе поддержки жизненного цикла.
   
   >[!NOTE]
   >Единый вход имеет toobe включаемые hello группа поддержки SCC LifeCycle.
   > 
   > 

6. На hello классический портал Azure, выберите Подтверждение настройки единого входа hello и нажмите кнопку **завершить** tooclose hello **Настройка единого входа** диалогового окна.
   
    ![Настройка единого входа](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Настройка единого входа")
   
## <a name="configure-user-provisioning"></a>Настроить подготовку учетных записей пользователей

В порядке tooenable toolog пользователей Azure AD в SCC LifeCycle их необходимо подготовить в SCC LifeCycle. Нет элемента действия для вас tooconfigure подготовки пользователей tooSCC жизненного цикла.

Когда назначенный пользователь пытается toolog в SCC LifeCycle учетная запись SCC LifeCycle создается автоматически при необходимости.

>[!NOTE]
>Можно использовать любые другие SCC LifeCycle пользователя средства создания учетных записей или интерфейсы API, предоставляемые SCC LifeCycle tooprovision учетных записей пользователей AAD.
> 
> 

## <a name="assign-users"></a>Назначить пользователей
tootest конфигурацию, необходимо toogrant hello Azure AD пользователей с помощью tooit доступ вашего приложения путем назначения им tooallow.

**Пользователи tooassign tooSCC жизненного цикла, выполните hello следующие шаги.**

1. В hello классический портал Azure создайте тестовую учетную запись.
2. На hello ** SCC LifeCycle ** странице интеграции приложения щелкните **назначить пользователей**.
   
    ![Назначение пользователей](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "Назначение пользователей")
3. Выберите тестового пользователя, нажмите кнопку **назначить**, а затем нажмите кнопку **Да** tooconfirm назначения.
   
    ![Да](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Да")

Tootest параметры единого входа, откройте панель доступа hello. Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

