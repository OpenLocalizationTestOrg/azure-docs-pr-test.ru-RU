---
title: "Руководство по интеграции Azure Active Directory с Jive | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Jive."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6fbfdbe7-d66c-4305-9fea-76d6a6a92830
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: b1c0d0bc2d79427c055f577fe5f9d30d10f1bbdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-jive-for-user-provisioning"></a>Руководство по настройке Jive для подготовки пользователей

Цель этого учебника Hello — hello действия, которые следует tooperform в Jive и Azure AD tooautomatically подготовки и Отмена подготовки учетных записей пользователей из Azure AD tooJive tooshow.

## <a name="prerequisites"></a>Предварительные требования

Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:

*   клиент Azure Active Directory;
*   подписка Jive с поддержкой единого входа;
*   учетная запись пользователя Jive с разрешениями администратора команды.

## <a name="assigning-users-toojive"></a>Назначение пользователей tooJive

Azure Active Directory использует называемый «назначения» toodetermine пользователей, которые должны получать доступ tooselected приложений. В контексте hello автоматический подготовки пользователей. учетной записи синхронизируются только hello пользователей и групп, назначенных» «tooan приложения в Azure AD.

Для настройки и включения hello подготовки службы, требуется toodecide какие пользователи или группы в Azure AD представляют Привет пользователям требуется доступ к приложению tooyour Jive. После приняла решение, можно назначить эти приложения Jive tooyour пользователей в соответствии с инструкциями hello здесь:

[Назначить пользователю или группе tooan корпоративного приложения](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toojive"></a>Важные советы для назначения пользователей tooJive

*   Рекомендуется один назначить hello tootest tooJive настройки подготовки пользователя Azure AD. Дополнительные пользователи и/или группы можно назначить позднее.

*   При назначении tooJive пользователя, необходимо выбрать допустимой роли пользователя. роль «Доступ по умолчанию» Hello не работает для подготовки.

## <a name="enable-user-provisioning"></a>Включение подготовки пользователей

Этот раздел поможет выполнить подключение учетной записи пользователя в Azure AD tooJive подготовки API и настройке подготовки службы toocreate hello, обновления и отключить учетные записи пользователей, назначенные в зависимости от назначения пользователей и групп в Azure AD Jive.

> [!TIP]
> Можно также выбрать tooenabled на основе SAML единого входа для Jive, следуя инструкциям hello в [портал Azure](https://portal.azure.com). Единый вход можно настроить независимо от автоматической подготовки, хотя эти две возможности дополняют друг друга.

### <a name="tooconfigure-user-account-provisioning"></a>Подготовка учетной записи пользователя tooconfigure:

Цель этого раздела Hello является toooutline как tooenable пользователя Подготовка пользователя Active Directory учетных записей tooJive.
В рамках этой процедуры не tooprovide требуется маркер безопасности пользователя, необходимо toorequest на сайте Jive.com.

1. В hello [портал Azure](https://portal.azure.com), Обзор toohello **Azure Active Directory > корпоративных приложений > все приложения** раздела.

2. Если вы уже настроили Jive для единого входа, поиск экземпляра с помощью поля поиска hello Jive. В противном случае выберите **добавить** и выполните поиск **Jive** в галерее приложения hello. Выберите Jive из результатов поиска hello и добавить его в список tooyour приложений.

3. Выберите свой экземпляр Jive, а затем выберите hello **Provisioning** вкладки.

4. Набор hello **режим подготовки** слишком**автоматического**. 

    ![подготовка](./media/active-directory-saas-jive-provisioning-tutorial/provisioning.png)

5. В разделе hello **учетные данные администратора** статьи, предоставляют hello следующие параметры конфигурации:
   
    а. В hello **имя пользователя администратора Jive** введите имя, которое имеет hello учетной записи Jive **системный администратор** профиля на сайте Jive.com.
   
    b. В hello **пароль администратора Jive** текстового поля, типа hello пароль для этой учетной записи.
   
    c. В hello **URL-адрес клиента Jive** в текстовое поле URL-адрес клиента Jive типа hello.
      
      > [!NOTE]
      > URL-адрес клиента Jive Hello является URL-адрес, используемый в вашей организации toolog в tooJive.  
      > Как правило, hello URL-адрес имеет следующий формат hello: **www.\< Организация\>. сайтом jive.com**.          

6. В hello портал Azure, щелкните **проверить подключение** tooensure Azure AD можно подключить приложение tooyour Jive.

7. Введите адрес электронной почты hello пользователя или группы, которые должны получить уведомления о подготовке ошибки в hello **уведомление по электронной почте** поле и установите флажок "hello" ниже.

8. Нажмите кнопку **Сохранить**.

9. Установите hello сопоставлений **tooJive синхронизации Azure Active Directory — пользователи.**

10. В hello **сопоставления атрибутов** просмотрите hello атрибутов пользователей, которые синхронизируются из tooJive Azure AD. Здравствуйте, атрибуты, выбранные в качестве **сопоставление** свойства, используемые toomatch hello учетных записей пользователей в Jive для операций обновления. Выберите toocommit кнопку hello сохранить все изменения.

11. tooenable hello подготовки службы Azure AD для Jive, изменение hello **состояние подготовки** слишком**на** в разделе "Параметры" hello

12. Нажмите кнопку **Сохранить**.

Он запускает hello первоначальной синхронизации все пользователи и группы, назначенные tooJive в hello пользователей и группы раздела. Начальная синхронизация Hello принимает tooperform больше времени, чем последующие синхронизации, которые происходят примерно каждые 20 минут при условии, что запущена служба hello. Можно использовать hello **сведения о синхронизации** статьи toomonitor хода выполнения и следуйте ссылки tooprovisioning отчеты о действиях, которые описывают все действия, выполняемые hello подготовки службы приложения Jive.

Теперь можно создать тестовую учетную запись. Дождитесь копирование минут too20 tooverify, hello учетная запись была синхронизирована tooJive.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Управление подготовкой учетных записей пользователей для корпоративных приложений](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Настройка единого входа](active-directory-saas-jive-tutorial.md)