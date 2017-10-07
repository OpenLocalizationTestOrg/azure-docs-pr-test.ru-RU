---
title: "Руководство по интеграции Azure Active Directory с песочницей Salesforce | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и песочницы Salesforce."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bab73fda-6754-411d-9288-f73ecdaa486d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: 06ff50050845383a602b0edd6fca953ddd37cebd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-salesforce-sandbox-for-automatic-user-provisioning"></a>Руководство по настройке песочницы Salesforce для автоматической подготовки пользователей

Цель этого учебника Hello — tooshow hello действия, которые следует tooperform в песочницу Salesforce и Azure AD tooautomatically подготовки и Отмена подготовки учетных записей пользователей из Azure AD tooSalesforce "песочницы".

## <a name="prerequisites"></a>Предварительные требования

Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:

*   клиент Azure Active Directory;
*   У вас должен быть действительный клиент для работы с песочницей Salesforce for Work или песочницей Salesforce for Education. Для любой из этих служб можно воспользоваться бесплатной пробной учетной записью.
*   Учетная запись пользователя в песочнице Salesforce с разрешениями администратора группы.

## <a name="assigning-users-toosalesforce-sandbox"></a>Назначение пользователей tooSalesforce "песочницы"

Azure Active Directory использует называемый «назначения» toodetermine пользователей, которые должны получать доступ tooselected приложений. В контексте hello автоматический подготовки пользователей. учетной записи синхронизируются только hello пользователей и групп, назначенных» «tooan приложения в Azure AD.

Для настройки и включения hello подготовки службы, требуется toodecide какие пользователи или группы в Azure AD представляют Привет пользователей, которым требуется доступ tooyour приложение песочницы Salesforce. После приняла решение, можно назначить эти пользователи tooyour приложение песочницы Salesforce, следуя инструкциям hello:

[Назначить пользователю или группе tooan корпоративного приложения](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toosalesforce-sandbox"></a>Важные советы для назначения пользователей tooSalesforce "песочницы"

* Рекомендуется один назначенный tooSalesforce "песочницы" tootest hello настройки подготовки пользователя Azure AD. Дополнительные пользователи и/или группы можно назначить позднее.

* При назначении пользователю tooSalesforce "песочницы", необходимо выбрать допустимой роли пользователя. роль «Доступ по умолчанию» Hello не работает для подготовки.

> [!NOTE]
> Это приложение импортирует пользовательские роли из песочницы Salesforce в рамках hello, какой клиент hello, при назначении пользователей может потребоваться tooselect процесса инициализации.

## <a name="enable-automated-user-provisioning"></a>Включение автоматической подготовки пользователей

Этот раздел поможет выполнить подключение подготовки API учетной записи пользователя песочницы tooSalesforce Azure AD и настройке подготовки службы toocreate hello, обновления и отключить пользователей, назначенные учетные записи в песочницу Salesforce на основе пользователей и группы Назначение в Azure AD.

>[!Tip]
>Можно также выбрать tooenabled на основе SAML Single Sign-On для песочницы Salesforce, следуя инструкциям hello в [портал Azure](https://portal.azure.com). Единый вход можно настроить независимо от автоматической подготовки, хотя эти две возможности дополняют друг друга.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure автоматический подготовки пользователей. учетной записи:

Цель этого раздела Hello является toooutline как tooenable пользователя Подготовка пользователя Active Directory учетных записей tooSalesforce "песочницы".

1. В hello [портал Azure](https://portal.azure.com), Обзор toohello **Azure Active Directory > корпоративных приложений > все приложения** раздела.

2. Если вы уже настроили песочницы Salesforce для единого входа, поиск экземпляра с помощью поля поиска hello песочницы Salesforce. В противном случае выберите **добавить** и выполните поиск **песочницы Salesforce** в галерее приложения hello. Выберите песочницы Salesforce из результатов поиска hello и добавить его в список tooyour приложений.

3. Выберите свой экземпляр песочницы Salesforce, а затем выберите hello **Provisioning** вкладки.

4. Набор hello **режим подготовки** слишком**автоматического**. 
    ![подготовка](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/provisioning.png)

5. В разделе hello **учетные данные администратора** статьи, предоставляют hello следующие параметры конфигурации:
   
    а. В hello **имя пользователя администратора** введите имя учетной записи Salesforce, имеет hello **системный администратор** профиля в Salesforce.com.
   
    b. В hello **пароль администратора** текстового поля, типа hello пароль для этой учетной записи.

6. tooget песочницы Salesforce маркера безопасности, откройте новую вкладку и войти в hello же учетная запись администратора песочницы Salesforce. На hello правом верхнем углу страницы приветствия, щелкните свое имя и нажмите кнопку **мои параметры**.

     ![Включение автоматической подготовки пользователей](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-my-settings.png "Включение автоматической подготовки пользователей")
7. На панели навигации слева hello, нажмите кнопку **личных** tooexpand hello соответствующий раздел и нажмите кнопку **Сброс личного токена безопасности**.
  
    ![Включение автоматической подготовки пользователей](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-personal-reset.png "Включение автоматической подготовки пользователей")
8. На hello **Сброс личного токена безопасности** щелкните hello **сбросить токен безопасности** кнопки.

    ![Включение автоматической подготовки пользователей](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-reset-token.png "Включение автоматической подготовки пользователей")
9. Проверьте папки "Входящие" hello электронной почты для этой учетной записи администратора. Найдите сообщение электронной почты от Salesforce Sandbox.com, содержащий hello новый маркер безопасности.
10. Hello токена, перейдите tooyour окна Azure AD скопируйте и вставьте его в hello **сокета маркера** поля.

11. В hello портал Azure, щелкните **проверить подключение** tooensure Azure AD могут подключаться tooyour приложение песочницы Salesforce.

12. В hello **уведомление по электронной почте** введите hello адрес электронной почты пользователя или группы, которые должны получать уведомления о подготовке ошибки и установите флажок "hello".

13. Нажмите кнопку **Сохранить**.  
    
14.  Установите hello сопоставлений **tooSalesforce синхронизации Azure Active Directory — пользователи "песочницы".**

15. В hello **сопоставления атрибутов** просмотрите hello атрибутов пользователей, которые синхронизируются из Azure AD tooSalesforce "песочницы". Здравствуйте, атрибуты, выбранные в качестве **сопоставление** свойства, используемые toomatch hello учетных записей пользователей в песочницу Salesforce для операций обновления. Выберите toocommit кнопку hello сохранить все изменения.

16. tooenable hello подготовки службы Azure AD для песочницы Salesforce, изменение hello **состояние подготовки** слишком**на** в разделе "Параметры" hello

17. Нажмите кнопку **Сохранить**.


Он запускает hello Первоначальная синхронизация всех пользователей и/или группам назначается tooSalesforce "песочницы" в разделе hello пользователей и групп. Начальная синхронизация Hello принимает tooperform больше времени, чем последующие синхронизации, которые происходят примерно каждые 20 минут при условии, что запущена служба hello. Можно использовать hello **сведения о синхронизации** статьи toomonitor хода выполнения и следуйте ссылки tooprovisioning отчеты о действиях, которые описывают все действия, выполняемые hello подготовки службы в приложение песочницы Salesforce.

Теперь можно создать тестовую учетную запись. Дождитесь копирование минут too20 tooverify, hello учетная запись была синхронизирована toosalesforce.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Управление подготовкой учетных записей пользователей для корпоративных приложений](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Настройка единого входа](active-directory-saas-salesforcesandbox-tutorial.md)