---
title: "Руководство по интеграции Azure Active Directory с Dropbox for Business | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Dropbox для бизнеса."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f3a42e4-6897-4234-af84-b47c148ec3e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 0fb01eab4f7c6c4516eac64a4343e46ea221f98d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-dropbox-for-business-for-automatic-user-provisioning"></a>Руководство по настройке автоматической подготовки пользователей в Dropbox for Business

Цель этого учебника Hello — tooshow hello действия, которые следует tooperform в Dropbox для бизнеса и Azure AD tooautomatically подготовки и Отмена подготовки учетных записей пользователей из Azure AD tooDropbox для бизнеса.

## <a name="prerequisites"></a>Предварительные требования

Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:

*   клиент Azure Active Directory;
*   подписка Dropbox for Business с поддержкой единого входа.
*   Учетная запись пользователя в Dropbox for Business с разрешениями администратора группы.

## <a name="assigning-users-toodropbox-for-business"></a>Назначение пользователей tooDropbox для бизнеса

Azure Active Directory использует называемый «назначения» toodetermine пользователей, которые должны получать доступ tooselected приложений. В контексте hello автоматический подготовки пользователей. учетной записи синхронизируются только hello пользователей и групп, назначенных» «tooan приложения в Azure AD.

Для настройки и включения hello подготовки службы, требуется toodecide какие пользователи или группы в Azure AD представляют Привет пользователей, которым требуется доступ tooyour Dropbox для бизнес-приложения. После приняла решение, можно назначить эти пользователи tooyour Dropbox для бизнес-приложения в соответствии с инструкциями hello здесь:

[Назначить пользователю или группе tooan корпоративного приложения](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toodropbox-for-business"></a>Важные советы для назначения пользователей tooDropbox для бизнеса

*   Рекомендуется один назначенный tooDropbox для бизнеса tootest hello настройки подготовки пользователя Azure AD. Дополнительные пользователи и/или группы можно назначить позднее.

*   При назначении tooDropbox пользователя для бизнеса, необходимо выбрать допустимой роли пользователя. роль «Доступ по умолчанию» Hello не работает для подготовки...

## <a name="enable-automated-user-provisioning"></a>Включение автоматической подготовки пользователей

Этот раздел поможет выполнить подключение tooDropbox к Azure AD для учетной записи пользователя организации подготовки API и настройке подготовки службы toocreate hello, обновления и отключить учетные записи пользователей, назначенные в Dropbox для бизнеса на основе пользователя и группы Назначение в Azure AD.

>[!Tip]
>Можно также выбрать tooenabled на основе SAML единого входа для Dropbox для бизнеса, следуя инструкциям hello в [портал Azure](https://portal.azure.com). Единый вход можно настроить независимо от автоматической подготовки, хотя эти две возможности дополняют друг друга.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure автоматический подготовки пользователей. учетной записи:

1. В hello [портал Azure](https://portal.azure.com), Обзор toohello **Azure Active Directory > корпоративных приложений > все приложения** раздела.

2. Если вы уже настроили Dropbox для бизнеса для единого входа, поиск экземпляра Dropbox для бизнеса, с помощью поля поиска hello. В противном случае выберите **добавить** и выполните поиск **Dropbox для бизнеса** в галерее приложения hello. Выберите из результатов поиска hello Dropbox для бизнеса и добавьте его tooyour список приложений.

3. Выберите свой экземпляр Dropbox для бизнеса, а затем выберите hello **Provisioning** вкладки.

4. Набор hello **режим подготовки** слишком**автоматического**. 

    ![подготовка](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/provisioning.png)

5. В разделе hello **учетные данные администратора** щелкните **авторизовать**. Откроется диалоговое окно входа в Dropbox for Business в новом окне браузера.

6. На hello **входа toolink tooDropbox с Azure AD** диалогового окна входа в tooyour Dropbox для бизнеса.

     ![Подготовка учетных записей пользователей](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "Подготовка учетных записей пользователей")

7. Убедитесь, что хотелось бы tooyour изменения toomake Azure Active Directory разрешение toogive Dropbox для бизнеса. Нажмите кнопку **Разрешить**.
    
      ![Подготовка учетных записей пользователей](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "Подготовка учетных записей пользователей")

8. В hello портал Azure, щелкните **проверить подключение** tooensure Azure AD могут подключаться tooyour Dropbox для бизнес-приложения. При сбое подключения hello убедитесь Dropbox для бизнеса учетная запись имеет разрешения администратора команды и повторите hello **«Авторизовать»** еще один шаг.

9. Введите адрес электронной почты hello пользователя или группы, которые должны получить уведомления о подготовке ошибки в hello **уведомление по электронной почте** поле и установите флажок "hello".

10. Нажмите кнопку **Сохранить**.

11. Установите hello сопоставлений **tooDropbox синхронизации Azure Active Directory-пользователи для бизнеса.**

12. В hello **сопоставления атрибутов** просмотрите hello атрибутов пользователей, которые синхронизируются из tooDropbox Azure AD для бизнеса. Здравствуйте, атрибуты, выбранные в качестве **сопоставление** свойства, используемые toomatch hello учетных записей пользователей в Dropbox для бизнеса для операций обновления. Выберите toocommit кнопку hello сохранить все изменения.

13. tooenable hello подготовки службы Azure AD для Dropbox для бизнеса, изменение hello **состояние подготовки** слишком**на** в разделе "Параметры" hello

14. Нажмите кнопку **Сохранить**.

Он запускает hello первоначальной синхронизации все пользователи и группы, назначенные tooDropbox для бизнеса в hello пользователей и группы раздела. Начальная синхронизация Hello принимает tooperform больше времени, чем последующие синхронизации, которые происходят примерно каждые 20 минут при условии, что запущена служба hello. Можно использовать hello **сведения о синхронизации** статьи toomonitor хода выполнения и следуйте ссылки tooprovisioning отчеты о действиях, которые описывают все действия, выполняемые hello подготовки службы на клиенте Dropbox для бизнес-приложения.

Теперь можно создать тестовую учетную запись. Дождитесь копирование минут too20 tooverify, hello учетная запись была синхронизирована tooDropbox для бизнеса.

Об успешном завершении цикла подготовки пользователя говорит соответствующий статус.

![Назначение пользователей](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "Назначение пользователей")


## <a name="additional-resources"></a>Дополнительные ресурсы

* [Управление подготовкой учетных записей пользователей для корпоративных приложений](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Настройка единого входа](active-directory-saas-dropboxforbusiness-tutorial.md)