---
title: "Руководство по интеграции Azure Active Directory с Salesforce | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Salesforce."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 49384b8b-3836-4eb1-b438-1c46bb9baf6f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: a916be8dbf0b4c6173cda873936a53cd1f3ff12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-salesforce-for-automatic-user-provisioning"></a>Руководство по настройке Salesforce для автоматической подготовки пользователей

Цель этого учебника Hello — tooshow hello действия требуется tooperform в Salesforce и Azure AD tooautomatically подготовки и Отмена подготовки учетных записей пользователей из Azure AD tooSalesforce.

## <a name="prerequisites"></a>Предварительные требования

Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:

*   клиент Azure Active Directory;
*   У вас должен быть действительный клиент для работы с Salesforce for Work или Salesforce for Education. Для любой из этих служб можно воспользоваться бесплатной пробной учетной записью.
*   Учетная запись пользователя в Salesforce с разрешениями администратора группы.

## <a name="assigning-users-toosalesforce"></a>Назначение пользователей tooSalesforce

Azure Active Directory использует называемый «назначения» toodetermine пользователей, которые должны получать доступ tooselected приложений. В контексте hello автоматический подготовки пользователей. учетной записи синхронизируются только hello пользователей и групп, назначенных» «tooan приложения в Azure AD.

Для настройки и включения hello подготовки службы, требуется toodecide какие пользователи и группы в Azure AD представляют Привет пользователей, которым требуется доступ к приложению Salesforce tooyour. После приняла решение, можно назначить эти приложения пользователям tooyour Salesforce, следуя инструкциям hello:

[Назначить пользователю или группе tooan корпоративного приложения](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toosalesforce"></a>Важные советы для назначения пользователей tooSalesforce

*   Рекомендуется один назначенный hello tootest tooSalesforce настройки подготовки пользователя Azure AD. Дополнительные пользователи и/или группы можно назначить позднее.

*  При назначении tooSalesforce пользователя, необходимо выбрать допустимой роли пользователя. роль «Доступ по умолчанию» Hello не работает для подготовки

    > [!NOTE]
    > Это приложение импортирует пользовательские роли из Salesforce в рамках hello подготовке, какой клиент hello может потребоваться tooselect при назначении пользователей

## <a name="enable-automated-user-provisioning"></a>Включение автоматической подготовки пользователей

Этот раздел поможет выполнить подключение учетной записи пользователя в Azure AD tooSalesforce подготовки API и настройке подготовки службы toocreate hello, обновления и отключить учетные записи пользователей, назначенные в Salesforce, в зависимости от назначения пользователей и групп в Azure AD .

>[!Tip]
>Можно также выбрать tooenabled на основе SAML единого входа для Salesforce, следуя инструкциям hello в [портал Azure](https://portal.azure.com). Единый вход можно настроить независимо от автоматической подготовки, хотя эти две возможности дополняют друг друга.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure автоматический подготовки пользователей. учетной записи:

Цель этого раздела Hello является toooutline как tooenable пользователя Подготовка пользователя Active Directory учетных записей tooSalesforce.

1. В hello [портал Azure](https://portal.azure.com), Обзор toohello **Azure Active Directory > корпоративных приложений > все приложения** раздела.

2. Если вы уже настроили Salesforce для единого входа, поиск экземпляра Salesforce с помощью поля поиска hello. В противном случае выберите **добавить** и выполните поиск **Salesforce** в галерее приложения hello. Выберите Salesforce из результатов поиска hello и добавить его в список tooyour приложений.

3. Выберите свой экземпляр Salesforce, а затем выберите hello **Provisioning** вкладки.

4. Набор hello **режим подготовки** слишком**автоматического**. 
![подготовка](./media/active-directory-saas-salesforce-provisioning-tutorial/provisioning.png)

5. В разделе hello **учетные данные администратора** статьи, предоставляют hello следующие параметры конфигурации:
   
    а. В hello **имя пользователя администратора** введите имя, которое имеет hello учетной записи Salesforce **системный администратор** профиля в Salesforce.com.
   
    b. В hello **пароль администратора** текстового поля, типа hello пароль для этой учетной записи.

6. tooget Salesforce маркера безопасности, откройте новую вкладку и войти в hello же учетная запись администратора Salesforce. На hello правом верхнем углу страницы приветствия, щелкните свое имя и нажмите кнопку **мои параметры**.

     ![Включение автоматической подготовки пользователей](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-my-settings.png "Включение автоматической подготовки пользователей")
7. На панели навигации слева hello, нажмите кнопку **личных** tooexpand hello соответствующий раздел и нажмите кнопку **Сброс личного токена безопасности**.
  
    ![Включение автоматической подготовки пользователей](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-personal-reset.png "Включение автоматической подготовки пользователей")
8. На hello **Сброс личного токена безопасности** щелкните **сбросить токен безопасности** кнопки.

    ![Включение автоматической подготовки пользователей](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-reset-token.png "Включение автоматической подготовки пользователей")
9. Проверьте папки "Входящие" hello электронной почты для этой учетной записи администратора. Найдите сообщение электронной почты от Salesforce.com, содержащий hello новый маркер безопасности.
10. Hello токена, перейдите tooyour окна Azure AD скопируйте и вставьте его в hello **сокета маркера** поля.

11. В hello портал Azure, щелкните **проверить подключение** tooensure Azure AD можно подключить приложение tooyour Salesforce.

12. В hello **уведомление по электронной почте** введите hello адрес электронной почты пользователя или группы, которые должны получать уведомления о подготовке ошибки и установите флажок "hello" ниже.

13. Нажмите кнопку **Сохранить**.  
    
14.  Установите hello сопоставлений **tooSalesforce синхронизации Azure Active Directory — пользователи.**

15. В hello **сопоставления атрибутов** просмотрите hello атрибутов пользователей, которые синхронизируются из tooSalesforce Azure AD. Обратите внимание, что атрибуты, выбранные в качестве hello **сопоставление** свойства, используемые toomatch hello учетные записи пользователей в Salesforce для операции обновления. Выберите toocommit кнопку hello сохранить все изменения.

16. tooenable hello подготовки службы Azure AD для Salesforce, изменение hello **состояние подготовки** слишком**на** в разделе "Параметры" hello

17. Нажмите кнопку **Сохранить**.

При этом запустится hello первоначальной синхронизации все пользователи и группы, назначенные tooSalesforce в hello пользователей и группы раздела. Обратите внимание, что начальная синхронизация hello принимает tooperform больше времени, чем последующие синхронизации, которые происходят примерно каждые 20 минут при условии, что запущена служба hello. Можно использовать hello **сведения о синхронизации** статьи toomonitor хода выполнения и следуйте ссылки tooprovisioning отчеты о действиях, которые описывают все действия, выполняемые hello подготовки службы приложения Salesforce.

Теперь можно создать тестовую учетную запись. Дождитесь копирование минут too20 tooverify, hello учетная запись была синхронизирована tooSalesforce.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Управление подготовкой учетных записей пользователей для корпоративных приложений](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Настройка единого входа](active-directory-saas-salesforce-tutorial.md)