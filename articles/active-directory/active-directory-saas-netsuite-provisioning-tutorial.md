---
title: "Руководство по интеграции Azure Active Directory с NetSuite | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Netsuite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8a6d3994-ee33-4a6f-b0a2-9d0389467f16
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 5bb2989c1296b9f2abc9e8c84855731adc484aab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-netsuite-for-automatic-user-provisioning"></a>Руководство по настройке Netsuite для автоматической подготовки пользователей

Цель этого учебника Hello — hello действия, которые следует tooperform в Netsuite и Azure AD tooautomatically подготовки и Отмена подготовки учетных записей пользователей из Azure AD tooNetsuite tooshow.

## <a name="prerequisites"></a>Предварительные требования

Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:

*   клиент Azure Active Directory;
*   подписка Netsuite с поддержкой единого входа;
*   учетная запись пользователя в Netsuite с разрешениями администратора команды.

## <a name="assigning-users-toonetsuite"></a>Назначение пользователей tooNetsuite

Azure Active Directory использует называемый «назначения» toodetermine пользователей, которые должны получать доступ tooselected приложений. В контексте hello автоматический подготовки пользователей. учетной записи синхронизируются только hello пользователей и групп, назначенных» «tooan приложения в Azure AD.

Для настройки и включения hello подготовки службы, требуется toodecide какие пользователи или группы в Azure AD представляют Привет пользователям требуется доступ к приложению Netsuite tooyour. После приняла решение, можно назначить эти приложения Netsuite tooyour пользователей в соответствии с инструкциями hello здесь:

[Назначить пользователю или группе tooan корпоративного приложения](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toonetsuite"></a>Важные советы для назначения пользователей tooNetsuite

*   Рекомендуется один назначенный hello tootest tooNetsuite настройки подготовки пользователя Azure AD. Дополнительные пользователи и/или группы можно назначить позднее.

*   При назначении tooNetsuite пользователя, необходимо выбрать допустимой роли пользователя. роль «Доступ по умолчанию» Hello не работает для подготовки.

## <a name="enable-user-provisioning"></a>Включение подготовки пользователей

Этот раздел поможет выполнить подключение учетной записи пользователя в Azure AD tooNetsuite подготовки API и настройке подготовки службы toocreate hello, обновления и отключить учетные записи пользователей, назначенные в Netsuite, в зависимости от назначения пользователей и групп в Azure AD.

> [!TIP] 
> Можно также выбрать tooenabled на основе SAML Single Sign-On для Netsuite, следуя инструкциям hello в [портал Azure](https://portal.azure.com). Единый вход можно настроить независимо от автоматической подготовки, хотя эти две возможности дополняют друг друга.

### <a name="tooconfigure-user-account-provisioning"></a>Подготовка учетной записи пользователя tooconfigure:

Цель этого раздела Hello является toooutline как tooenable пользователя Подготовка пользователя Active Directory учетных записей tooNetsuite.

1. В hello [портал Azure](https://portal.azure.com), Обзор toohello **Azure Active Directory > корпоративных приложений > все приложения** раздела.

2. Если вы уже настроили Netsuite для единого входа, поиск экземпляра Netsuite, с помощью поля поиска hello. В противном случае выберите **добавить** и выполните поиск **Netsuite** в галерее приложения hello. Выберите Netsuite из результатов поиска hello и добавить его в список tooyour приложений.

3. Выберите свой экземпляр Netsuite, а затем выберите hello **Provisioning** вкладки.

4. Набор hello **режим подготовки** слишком**автоматического**. 

    ![подготовка](./media/active-directory-saas-netsuite-provisioning-tutorial/provisioning.png)

5. В разделе hello **учетные данные администратора** статьи, предоставляют hello следующие параметры конфигурации:
   
    а. В hello **имя пользователя администратора** введите имя, которое имеет hello, учетной записи Netsuite **системный администратор** Netsuite.com назначен профиль.
   
    b. В hello **пароль администратора** текстового поля, типа hello пароль для этой учетной записи.
      
6. В hello портал Azure, щелкните **проверить подключение** tooensure Azure AD можно подключить приложение Netsuite tooyour.

7. В hello **уведомление по электронной почте** введите hello адрес электронной почты пользователя или группы, которые должны получать уведомления о подготовке ошибки и установите флажок "hello".

8. Нажмите кнопку **Сохранить**.

9. Установите hello сопоставлений **tooNetsuite синхронизации Azure Active Directory — пользователи.**

10. В hello **сопоставления атрибутов** просмотрите hello атрибутов пользователей, которые синхронизируются из tooNetsuite Azure AD. Обратите внимание, что атрибуты, выбранные в качестве hello **сопоставление** свойства, используемые toomatch hello учетных записей пользователей в Netsuite для операций обновления. Выберите toocommit кнопку hello сохранить все изменения.

11. tooenable hello подготовки службы Azure AD для Netsuite, изменение hello **состояние подготовки** слишком**на** в разделе "Параметры" hello

12. Нажмите кнопку **Сохранить**.

Он запускает hello первоначальной синхронизации все пользователи и группы, назначенные tooNetsuite в hello пользователей и группы раздела. Обратите внимание, что начальная синхронизация hello принимает tooperform больше времени, чем последующие синхронизации, которые происходят примерно каждые 20 минут при условии, что запущена служба hello. Можно использовать hello **сведения о синхронизации** статьи toomonitor хода выполнения и следуйте ссылки tooprovisioning отчеты о действиях, описывающих все действия, выполняемые hello подготовки службы приложения Netsuite.

Теперь можно создать тестовую учетную запись. Дождитесь копирование минут too20 tooverify, hello учетная запись была синхронизирована tooNetsuite.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Управление подготовкой учетных записей пользователей для корпоративных приложений](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Настройка единого входа](active-directory-saas-netsuite-tutorial.md)