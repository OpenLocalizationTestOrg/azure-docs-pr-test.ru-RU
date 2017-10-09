---
title: "Руководство по интеграции Azure Active Directory с Qualtrics | Документация Майкрософт"
description: "Узнайте, как toouse Qualtrics с Azure Active Directory tooenable единого входа, автоматизированной подготовки и многое другое!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 4df889ab-2685-4d15-a163-1ba26567eeda
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 941642e74b90bb13a5ce37ce6665cfa32cd86016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qualtrics"></a>Учебник. Интеграция Azure Active Directory с Qualtrics
Цель этого учебника Hello — tooshow hello интеграцию Azure и Qualtrics.  

Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:

* Действующая подписка на Azure
* Подписка Qualtrics с поддержкой единого входа.

После завершения этого учебника, пользователи hello Azure AD, назначенные tooQualtrics будет может toosingle вход в приложение hello на корпоративном сайте Qualtrics (вход поставщиком услуг инициировал) или с помощью hello [toohello введение Получить доступ к панели](active-directory-saas-access-panel-introduction.md).

Hello сценарий, описанный в этом руководстве состоит из hello следующие стандартные блоки.

1. Включение hello интеграции приложений для Qualtrics
2. Настройка единого входа.
3. Настройка подготовки учетных записей пользователей
4. Назначение пользователей

![Сценарий](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "Сценарий")

## <a name="enabling-hello-application-integration-for-qualtrics"></a>Включение hello интеграции приложений для Qualtrics
Hello цель этого раздела — toooutline как интеграция приложения hello tooenable для Qualtrics.

**интеграции приложения hello tooenable для Qualtrics, выполните следующие шаги hello.**

1. В hello классический портал Azure, hello левой области навигации, выберите **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")
2. Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.
3. Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.
   
   ![Приложения](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "Приложения")
4. Нажмите кнопку **добавить** hello нижней части страницы приветствия.
   
   ![Добавление приложения](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "Добавление приложения")
5. На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.
   
   ![Добавление приложения из коллекции](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "Добавление приложения из коллекции")
6. В hello **поле поиска**, тип **Qualtrics**.
   
   ![Коллекция приложений](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "Коллекция приложений")
7. В области результатов hello выберите **Qualtrics**и нажмите кнопку **завершить** tooadd приложения hello.
   
   ![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")
   
## <a name="configure-single-sign-on"></a>Настройка единого входа

Цель этого раздела Hello — toooutline как tooQualtrics tooauthenticate tooenable пользователей с учетной записью в Azure AD, используя федерацию на основе hello SAML протокола.

**tooconfigure единого входа, выполните следующие шаги hello:**

1. В классический портал Azure, на hello hello **Qualtrics** странице интеграции приложения щелкните **настроить единый вход** tooopen hello **Настройка единого входа** диалогового окна.
   
   ![Настройка единого входа](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "Настройка единого входа")
2. На hello **предпочитаемый как toosign пользователей на tooQualtrics** выберите **Microsoft Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.
   
   ![Настройка единого входа](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "Настройка единого входа")
3. На hello **настроить URL-адрес приложения** страницы в hello **Qualtrics на URL-адрес входа** в текстовое поле введите URL-адрес (например: «*https://ssotest2ut1.qualtrics.com*») и нажмите кнопку **Далее**.
   
   ![Настройка URL-адреса приложения](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "Настройка URL-адреса приложения")
4. На hello **настройки единого входа в Qualtrics** щелкните **загрузить метаданные**, а затем сохраните файл метаданных hello на компьютере.
   
   ![Настройка единого входа](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "Настройка единого входа")
5. Отправьте hello метаданных файла toohello поддержки qualtrics.
   
   >[!NOTE]
   >Настройка единого входа Hello имеет toobe выполненных hello поддержки qualtrics. Сразу после завершения настройки hello, вы получите уведомление.
   > 
   > 
6. На hello классический портал Azure, выберите Подтверждение настройки единого входа hello и нажмите кнопку **завершить** tooclose hello **Настройка единого входа** диалогового окна.
   
   ![Настройка единого входа](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "Настройка единого входа")
   
## <a name="configure-user-provisioning"></a>Настроить подготовку учетных записей пользователей

Нет элемента действия для вас tooconfigure подготовки пользователей tooQualtrics. Когда назначенный пользователь пытается toolog в Qualtrics с помощью панели доступа hello, Qualtrics проверяет, существует ли пользователь hello.  

Если учетная запись пользователя отсутствует, Qualtrics автоматически создает ее.

## <a name="assign-users"></a>Назначить пользователей
tootest конфигурацию, необходимо toogrant hello Azure AD пользователей с помощью tooit доступ вашего приложения путем назначения им tooallow.

**tooQualtrics tooassign пользователей, выполните следующие шаги hello.**

1. В hello классический портал Azure создайте тестовую учетную запись.
2. На hello **Qualtrics** странице интеграции приложения щелкните **назначить пользователей**.
   
   ![Назначение пользователей](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "Назначение пользователей")
3. Выберите тестового пользователя, нажмите кнопку **назначить**, а затем нажмите кнопку **Да** tooconfirm назначения.
   
   ![Да](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Да")

Tootest параметры единого входа, откройте панель доступа hello. Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

