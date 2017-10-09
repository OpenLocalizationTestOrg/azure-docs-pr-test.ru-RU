---
title: "Учебник. Интеграция Azure Active Directory с DocuSign | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и DocuSign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 294cd6b8-74d7-44bc-92bc-020ccd13ff12
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 8562a8f9e05fb72d3331507b7da5c6afee38f9b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-docusign-for-user-provisioning"></a>Руководство по настройке DocuSign для подготовки пользователей

Цель этого учебника Hello — hello действия, которые следует tooperform в DocuSign и Azure AD tooautomatically подготовки и Отмена подготовки учетных записей пользователей из Azure AD tooDocuSign tooshow.

## <a name="prerequisites"></a>Предварительные требования

Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:

*   клиент Azure Active Directory;
*   подписка DocuSign с поддержкой единого входа;
*   учетная запись пользователя в DocuSign с разрешениями администратора группы.

## <a name="assigning-users-toodocusign"></a>Назначение пользователей tooDocuSign

Azure Active Directory использует называемый «назначения» toodetermine пользователей, которые должны получать доступ tooselected приложений. В контексте hello автоматический подготовки пользователей. учетной записи синхронизируются только hello пользователей и групп, назначенных» «tooan приложения в Azure AD.

Для настройки и включения hello подготовки службы, требуется toodecide какие пользователи или группы в Azure AD представляют Привет пользователям требуется доступ к приложению DocuSign tooyour. После приняла решение, можно назначить эти приложения DocuSign tooyour пользователей в соответствии с инструкциями hello здесь:

[Назначить пользователю или группе tooan корпоративного приложения](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toodocusign"></a>Важные советы для назначения пользователей tooDocuSign

*   Рекомендуется один назначенный hello tootest tooDocuSign настройки подготовки пользователя Azure AD. Дополнительные пользователи и/или группы можно назначить позднее.

*   При назначении tooDocuSign пользователя, необходимо выбрать допустимой роли пользователя. роль «Доступ по умолчанию» Hello не работает для подготовки.

## <a name="enable-user-provisioning"></a>Включение подготовки пользователей

Этот раздел поможет выполнить подключение учетной записи пользователя в Azure AD tooDocuSign подготовки API и настройке подготовки службы toocreate hello, обновления и отключить учетные записи пользователей, назначенные в DocuSign, в зависимости от назначения пользователей и групп в Azure AD.

> [!Tip]
> Можно также выбрать tooenabled на основе SAML Single Sign-On для DocuSign, следуя инструкциям hello в [портал Azure](https://portal.azure.com). Единый вход можно настроить независимо от автоматической подготовки, хотя эти две возможности дополняют друг друга.

### <a name="tooconfigure-user-account-provisioning"></a>Подготовка учетной записи пользователя tooconfigure:

Цель этого раздела Hello является toooutline как tooenable пользователя Подготовка пользователя Active Directory учетных записей tooDocuSign.

1. В hello [портал Azure](https://portal.azure.com), Обзор toohello **Azure Active Directory > корпоративных приложений > все приложения** раздела.

2. Если вы уже настроили DocuSign для единого входа, поиск экземпляра DocuSign с помощью поля поиска hello. В противном случае выберите **добавить** и выполните поиск **DocuSign** в галерее приложения hello. Выберите DocuSign из результатов поиска hello и добавить его в список tooyour приложений.

3. Выберите свой экземпляр DocuSign, а затем выберите hello **Provisioning** вкладки.

4. Набор hello **режим подготовки** слишком**автоматического**. 

    ![подготовка](./media/active-directory-saas-docusign-provisioning-tutorial/provisioning.png)

5. В разделе hello **учетные данные администратора** статьи, предоставляют hello следующие параметры конфигурации:
   
    а. В hello **имя пользователя администратора** введите имя, которое имеет hello учетной записи DocuSign **системный администратор** профиля в DocuSign.com.
   
    b. В hello **пароль администратора** текстового поля, типа hello пароль для этой учетной записи.

6. В hello портал Azure, щелкните **проверить подключение** tooensure Azure AD можно подключить приложение tooyour DocuSign.

7. В hello **уведомление по электронной почте** введите hello адрес электронной почты пользователя или группы, которые должны получать уведомления о подготовке ошибки и установите флажок "hello".

8. Нажмите кнопку **Сохранить**.

9. Установите hello сопоставлений **tooDocuSign синхронизации Azure Active Directory — пользователи.**

10. В hello **сопоставления атрибутов** просмотрите hello атрибутов пользователей, которые синхронизируются из tooDocuSign Azure AD. Здравствуйте, атрибуты, выбранные в качестве **сопоставление** свойства, используемые toomatch hello учетных записей пользователей в DocuSign для операций обновления. Выберите toocommit кнопку hello сохранить все изменения.

11. tooenable hello подготовки службы Azure AD для DocuSign, изменение hello **состояние подготовки** слишком**на** в разделе "Параметры" hello

12. Нажмите кнопку **Сохранить**.

Он запускает hello первоначальной синхронизации все пользователи и группы, назначенные tooDocuSign в hello пользователей и группы раздела. Начальная синхронизация Hello принимает tooperform больше времени, чем последующие синхронизации, которые происходят примерно каждые 20 минут при условии, что запущена служба hello. Можно использовать hello **сведения о синхронизации** статьи toomonitor хода выполнения и следуйте ссылки tooprovisioning отчеты о действиях, которые описывают все действия, выполняемые hello подготовки службы в приложении DocuSign.

Теперь можно создать тестовую учетную запись. Дождитесь копирование минут too20 tooverify, hello учетная запись была синхронизирована tooDocuSign.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Управление подготовкой учетных записей пользователей для корпоративных приложений](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Настройка единого входа](active-directory-saas-docusign-tutorial.md)