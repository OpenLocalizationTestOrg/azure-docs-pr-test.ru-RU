---
title: "Руководство по настройке GitHub для автоматической подготовки пользователей с помощью Azure Active Directory | Документация Майкрософт"
description: "Узнайте, как tooconfigure Azure Active Directory tooautomatically подготовки и Отмена подготовки учетных записей пользователей tooGitHub."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: asmalser-msft
ms.openlocfilehash: c1f0f7a42e4f8a94db3f409cd463e13bb1bc13bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-github-for-automatic-user-provisioning"></a>Руководство по настройке GitHub для автоматической подготовки пользователей


Цель этого учебника Hello — hello действия, которые следует tooperform в GitHub и Azure AD tooautomatically подготовки и Отмена подготовки учетных записей пользователей из Azure AD tooGitHub tooshow. 

## <a name="prerequisites"></a>Предварительные требования

Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:

*   клиент Azure Active Directory;
*   Клиент Github с hello [бизнес-планом](https://help.github.com/articles/organization-billing-plans/#business-plan) или лучше включена 
*   учетная запись пользователя в GitHub с разрешениями администратора. 

> [!NOTE]
> Hello подготовки интеграции Azure AD использует hello [GitHub SCIM API](https://developer.github.com/v3/scim/), являющийся tooGithub доступные команды на бизнес-планом hello и более.

## <a name="assigning-users-toogithub"></a>Назначение пользователей tooGitHub

Azure Active Directory использует называемый «назначения» toodetermine пользователей, которые должны получать доступ tooselected приложений. В контексте hello автоматический подготовки пользователей. учетной записи синхронизируются только hello пользователей и групп, назначенных» «tooan приложения в Azure AD. 

Перед Настройка и включение hello подготовки службы, необходимо toodecide какие пользователи или группы в Azure AD представляют Привет пользователям требуется доступ к приложению tooyour GitHub. После приняла решение, можно назначить эти приложения пользователям tooyour GitHub в соответствии с инструкциями hello здесь:

[Назначить пользователю или группе tooan корпоративного приложения](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toogithub"></a>Важные советы для назначения пользователей tooGitHub

*   Рекомендуется один назначенный hello tootest tooGitHub настройки подготовки пользователя Azure AD. Дополнительные пользователи и/или группы можно назначить позднее.

*   При назначении tooGitHub пользователя, необходимо выбрать либо hello **пользователя** роли или другой допустимый конкретного приложения (если доступно) в диалоговом окне приветствия назначения. Hello **доступа по умолчанию** роль не будет работать для подготовки, и эти пользователи будут пропускаться.


## <a name="configuring-user-provisioning-toogithub"></a>Настройка подготовки tooGitHub пользователей 

Этот раздел поможет выполнить подключение учетной записи пользователя в Azure AD tooGitHub подготовки API и настройке подготовки службы toocreate hello, обновления и отключить учетные записи пользователей, назначенные в GitHub, в зависимости от назначения пользователей и групп в Azure AD.

> [!TIP]
> Можно также выбрать tooenabled на основе SAML Single Sign-On для GitHub, следуя инструкциям hello в [портал Azure](https://portal.azure.com). Единый вход можно настроить независимо от автоматической подготовки, хотя эти две возможности дополняют друг друга.


### <a name="configure-automatic-user-account-provisioning-toogithub-in-azure-ad"></a>Настройка учетной записи автоматического пользователя подготовки tooGitHub в Azure AD


1. В hello [портал Azure](https://portal.azure.com), Обзор toohello **Azure Active Directory > корпоративных приложений > все приложения** раздела.

2. Если вы уже настроили GitHub для единого входа, поиск экземпляра с помощью поля поиска hello GitHub. В противном случае выберите **добавить** и выполните поиск **GitHub** в галерее приложения hello. Выберите GitHub из результатов поиска hello и добавить его в список tooyour приложений.

3. Выберите свой экземпляр GitHub, а затем выберите hello **Provisioning** вкладки.

4. Набор hello **режим подготовки** слишком**автоматического**.

    ![Подготовка GitHub](./media/active-directory-saas-github-provisioning-tutorial/GitHub1.png)

5. В разделе hello **учетные данные администратора** щелкните **авторизовать**. В новом окне браузера откроется диалоговое окно авторизации GitHub. 

6. В новом окне приветствия войдите в GitHub с помощью учетной записи администратора. В hello полученный авторизации диалоговом выберите hello tooenable инициализацию и затем выберите группу GitHub **авторизовать**. Hello Azure портала toocomplete после ее завершения, возвращаемый toohello настройки подготовки.

    ![Диалоговое окно авторизации](./media/active-directory-saas-github-provisioning-tutorial/GitHub2.png)

7. В hello портал Azure, входной **URL-адрес клиента** и нажмите кнопку **проверить подключение** tooensure Azure AD можно подключить приложение tooyour GitHub. При сбое подключения hello, убедитесь в вашей учетной записи GitHub имеет разрешения администратора и **URL-адрес клиента** введено правильно, а затем повторите hello, «Авторизовать» еще один шаг (могут составлять **URL-адрес клиента** правилом: «https : //api.github.com/scim/v2/organizations/ + < Organizations_name >», можно найти организации в рамках учетной записи GitHub: **параметры** > **организаций**).

    ![Диалоговое окно авторизации](./media/active-directory-saas-github-provisioning-tutorial/GitHub3.png)

8. Введите адрес электронной почты hello пользователя или группы, которые должны получить уведомления о подготовке ошибки в hello **уведомление по электронной почте** поле и проверьте hello флажок «Отправить уведомление по электронной почте при возникновении сбоя».

9. Щелкните **Сохранить**. 

10. Установите hello сопоставлений **tooGitHub синхронизации Azure Active Directory — пользователи**.

11. В hello **сопоставления атрибутов** просмотрите hello атрибутов пользователей, которые синхронизируются из tooGitHub Azure AD. Здравствуйте, атрибуты, выбранные в качестве **сопоставление** свойства, используемые toomatch hello учетные записи пользователей в GitHub для операции обновления. Выберите toocommit кнопку hello сохранить все изменения.

12. tooenable hello подготовки службы Azure AD для GitHub, изменение hello **состояние подготовки** слишком**на** в hello **параметры** раздела

13. Щелкните **Сохранить**. 

Эта операция запускает hello первоначальной синхронизации все пользователи и группы, назначенные tooGitHub в hello пользователей и группы раздела. Начальная синхронизация Hello принимает tooperform больше времени, чем последующие синхронизации, которые происходят примерно каждые 20 минут при условии, что запущена служба hello. Можно использовать hello **сведения о синхронизации** статьи toomonitor хода выполнения и следуйте ссылки tooprovisioning отчеты о действиях, которые описывают все действия, выполняемые hello подготовки службы.

Дополнительные сведения о способ подготовки tooread hello Azure AD использует для входа см. в разделе [отчеты о автоматический подготовки пользователей. учетной записи](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).


## <a name="additional-resources"></a>Дополнительные ресурсы

* [Управление подготовкой учетных записей пользователей для корпоративных приложений](active-directory-enterprise-apps-manage-provisioning.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Дальнейшие действия

* [Узнайте, каким образом ведет журнал tooreview и получать отчеты о действиях по подготовке](active-directory-saas-provisioning-reporting.md)
