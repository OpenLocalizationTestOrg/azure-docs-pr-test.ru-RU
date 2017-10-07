---
title: "Руководство по интеграции Azure Active Directory с Citrix GoToMeeting | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Citrix GoToMeeting."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f59fedb-2cf8-48d2-a5fb-222ed943ff78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 3c6eed5309dfa384c292b0cf63f8aa58988add81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-citrix-gotomeeting-for-automatic-user-provisioning"></a>Руководство по настройке Citrix GoToMeeting для автоматической подготовки пользователей

Цель этого учебника Hello — tooshow hello действия, которые следует tooperform в Citrix GoToMeeting и Azure AD tooautomatically подготовки и Отмена подготовки учетных записей пользователей из Azure AD tooCitrix GoToMeeting.

## <a name="prerequisites"></a>Предварительные требования

Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:

*   клиент Azure Active Directory;
*   подписка Citrix GoToMeeting с поддержкой единого входа;
*   учетная запись пользователя в Citrix GoToMeeting с разрешениями администратора группы.

## <a name="assigning-users-toocitrix-gotomeeting"></a>Назначение пользователей tooCitrix GoToMeeting

Azure Active Directory использует называемый «назначения» toodetermine пользователей, которые должны получать доступ tooselected приложений. В контексте hello автоматический подготовки пользователей. учетной записи синхронизируются только hello пользователей и групп, назначенных» «tooan приложения в Azure AD.

Для настройки и включения hello подготовки службы, требуется toodecide какие пользователи или группы в Azure AD представляют Привет пользователей, которым требуется доступ tooyour приложение Citrix GoToMeeting. После приняла решение, можно назначить эти пользователи tooyour приложение Citrix GoToMeeting в соответствии с инструкциями hello здесь:

[Назначить пользователю или группе tooan корпоративного приложения](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toocitrix-gotomeeting"></a>Важные советы для назначения пользователей tooCitrix GoToMeeting

*   Рекомендуется один назначенный tooCitrix GoToMeeting tootest hello настройки подготовки пользователя Azure AD. Дополнительные пользователи и/или группы можно назначить позднее.

*   При присвоении пользователя tooCitrix GoToMeeting, необходимо выбирать допустимой роли пользователя. роль «Доступ по умолчанию» Hello не работает для подготовки.

## <a name="enable-automated-user-provisioning"></a>Включение автоматической подготовки пользователей

Этот раздел поможет выполнить подключение подготовки API учетной записи пользователя GoToMeeting tooCitrix Azure AD и настройке подготовки службы toocreate hello, обновления и отключить пользователей, назначенные учетные записи в Citrix GoToMeeting на основе пользователей и группы Назначение в Azure AD.

> [!TIP]
> Можно также выбрать tooenabled на основе SAML единого входа для Citrix GoToMeeting, следуя инструкциям hello в [портал Azure](https://portal.azure.com). Единый вход можно настроить независимо от автоматической подготовки, хотя эти две возможности дополняют друг друга.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure автоматический подготовки пользователей. учетной записи:

1. В hello [портал Azure](https://portal.azure.com), Обзор toohello **Azure Active Directory > корпоративных приложений > все приложения** раздела.

2. Если вы уже настроили Citrix GoToMeeting для единого входа, поиск экземпляра с помощью поля поиска hello Citrix GoToMeeting. В противном случае выберите **добавить** и выполните поиск **Citrix GoToMeeting** в галерее приложения hello. Выберите из результатов поиска hello Citrix GoToMeeting и добавьте его tooyour список приложений.

3. Выберите свой экземпляр Citrix GoToMeeting, а затем выберите hello **Provisioning** вкладки.

4. Набор hello **Provisioning** режиме слишком**автоматического**. 

    ![подготовка](./media/active-directory-saas-citrixgotomeeting-provisioning-tutorial/provisioning.png)

5. В области hello раздел учетные данные администратора выполните следующие шаги hello.
   
    а. В hello **имя пользователя администратора Citrix GoToMeeting** текстовом поле введите имя пользователя hello администратора.

    b. В hello **пароль администратора Citrix GoToMeeting** в текстовое поле пароля администратора hello.

6. В hello портал Azure, щелкните **проверить подключение** tooensure Azure AD могут подключаться tooyour приложение Citrix GoToMeeting. При сбое подключения hello, убедитесь в вашей учетной записи Citrix GoToMeeting имеет разрешения администратора команды и повторите hello **«Учетные данные администратора»** еще один шаг.

7. Введите адрес электронной почты hello пользователя или группы, которые должны получить уведомления о подготовке ошибки в hello **уведомление по электронной почте** поле и установите флажок "hello".

8. Нажмите кнопку **Сохранить**.

9. Установите hello сопоставлений **синхронизации Azure Active Directory — пользователи tooCitrix GoToMeeting.**

10. В hello **сопоставления атрибутов** просмотрите hello атрибутов пользователей, которые синхронизируются из Azure AD tooCitrix GoToMeeting. Здравствуйте, атрибуты, выбранные в качестве **сопоставление** свойства, используемые toomatch hello учетных записей пользователей в Citrix GoToMeeting для операций обновления. Выберите toocommit кнопку hello сохранить все изменения.

11. tooenable hello подготовки службы Azure AD для Citrix GoToMeeting, изменение hello **состояние подготовки** слишком**на** в разделе "Параметры" hello

12. Нажмите кнопку **Сохранить**.

Он запускает hello Первоначальная синхронизация всех пользователей и/или группам назначается tooCitrix GoToMeeting в разделе hello пользователей и групп. Начальная синхронизация Hello принимает tooperform больше времени, чем последующие синхронизации, которые происходят примерно каждые 20 минут при условии, что запущена служба hello. Можно использовать hello **сведения о синхронизации** статьи toomonitor хода выполнения и следуйте ссылки tooprovisioning отчеты о действиях, которые описывают все действия, выполняемые hello подготовки службы в приложении Citrix GoToMeeting.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Управление подготовкой учетных записей пользователей для корпоративных приложений](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Настройка единого входа](active-directory-saas-citrix-gotomeeting-tutorial.md)


