---
title: "Руководство по настройке Slack для автоматической подготовки пользователей с помощью Azure Active Directory | Документация Майкрософт"
description: "Узнайте, как tooconfigure Azure Active Directory tooautomatically подготовки и Отмена подготовки учетных записей пользователей tooSlack."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: sakula
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: asmalser-msft
ms.reviewer: asmalser
ms.openlocfilehash: d0a565bbe0bd7e229b9dd99b1ebbaf67d93a2206
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-slack-for-automatic-user-provisioning"></a>Tutorial: Configuring Slack for Automatic User Provisioning (Учебник. Настройка Slack для автоматической подготовки пользователей)


Hello цель этого учебника — tooshow hello действия, которые следует tooperform в Slack и Azure AD tooautomatically подготовки и Отмена подготовки учетных записей пользователей из Azure AD tooSlack. 

## <a name="prerequisites"></a>Предварительные требования

Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:

*   Клиент Azure Active Directory.
*   Резерв клиента с hello [плюс плана](https://aadsyncfabric.slack.com/pricing) или лучше включена 
*   Учетная запись пользователя в Slack с разрешениями администратора группы 

Примечание: hello подготовки интеграции Azure AD использует hello [Slack SCIM API](https://api.slack.com/scim) это tooSlack доступных команд в hello плюс плана или более поздней.

## <a name="assigning-users-tooslack"></a>Назначение пользователей tooSlack

Azure Active Directory использует называемый «назначения» toodetermine пользователей, которые должны получать доступ tooselected приложений. В контексте hello автоматический подготовки пользователей. учетной записи будут синхронизированы только hello пользователей и групп, назначенных» «tooan приложения в Azure AD. 

Для настройки и включения hello подготовки службы, вам потребуется toodecide какие пользователи или группы в Azure AD представляют Привет пользователям требуется доступ к приложению резерв tooyour. После приняла решение, можно назначить эти приложения резерв tooyour пользователей в соответствии с инструкциями hello здесь:

[Назначить пользователю или группе tooan корпоративного приложения](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-tooslack"></a>Важные советы для назначения пользователей tooSlack

*   Рекомендуется один назначить hello tootest tooSlack настройки подготовки пользователя Azure AD. Дополнительные пользователи и/или группы можно назначить позднее.

*   При назначении tooSlack пользователя, необходимо выбрать hello **пользователя** или роли «Группа» в диалоговом окне приветствия назначения. роль «Доступ по умолчанию» Hello не работает для подготовки.


## <a name="configuring-user-provisioning-tooslack"></a>Настройка подготовки tooSlack пользователей 

Этот раздел поможет выполнить подключение учетной записи пользователя в Azure AD tooSlack подготовки API и настройке подготовки службы toocreate hello, обновления и отключить учетные записи пользователей, назначенные в Slack, в зависимости от назначения пользователей и групп в Azure AD.

**Совет:** можно также выбрать tooenabled на основе SAML единого входа для Slack, следуя инструкциям hello в (портал Azure) [https://portal.azure.com]. Единый вход можно настроить независимо от автоматической подготовки, хотя эти две возможности дополняют друг друга.


### <a name="tooconfigure-automatic-user-account-provisioning-tooslack-in-azure-ad"></a>tooconfigure автоматическая учетная запись подготовки tooSlack в Azure AD:


1)  В hello [портал Azure](https://portal.azure.com), Обзор toohello **Azure Active Directory > корпоративных приложений > все приложения** раздела.

2) Если вы уже настроили резерв для единого входа, поиск экземпляра Slack, с помощью поля поиска hello. В противном случае выберите **добавить** и выполните поиск **Slack** в галерее приложения hello. Выберите Slack из результатов поиска hello и добавить его в список tooyour приложений.

3)  Выберите свой экземпляр резерва, а затем выберите hello **Provisioning** вкладки.

4)  Набор hello **режим подготовки** слишком**автоматического**.

![Подготовка Slack](./media/active-directory-saas-slack-provisioning-tutorial/Slack1.PNG)

5)  В разделе hello **учетные данные администратора** щелкните **авторизовать**. В новом окне браузера откроется диалоговое окно авторизации Slack. 

6) В новом окне приветствия войти в Slack, с помощью учетной записи администратора команды. в hello результирующее диалоговое окно авторизации, выберите hello резерв команды, которые tooenable инициализацию и затем выберите **авторизовать**. Hello Azure портала toocomplete после ее завершения, возвращаемый toohello настройки подготовки.

![Диалоговое окно авторизации](./media/active-directory-saas-slack-provisioning-tutorial/Slack3.PNG)

7) В hello портал Azure, щелкните **проверить подключение** tooensure Azure AD можно подключить tooyour резерв приложение. При сбое подключения hello, убедитесь, что резерв учетная запись имеет разрешения администратора команды и повторите попытку шаг «Авторизовать» hello.

8) Введите адрес электронной почты hello пользователя или группы, которые должны получить уведомления о подготовке ошибки в hello **уведомление по электронной почте** поле и установите флажок "hello" ниже.

9) Щелкните **Сохранить**. 

10) Установите hello сопоставлений **tooSlack синхронизации Azure Active Directory — пользователи**.

11) В hello **сопоставления атрибутов** просмотрите hello атрибутов пользователей, которые будут синхронизированы из tooSlack Azure AD. Обратите внимание, что атрибуты, выбранные в качестве hello **сопоставление** свойства будут использоваться toomatch hello учетных записей пользователей в Slack для операций обновления. Выберите toocommit кнопку hello сохранить все изменения.

12) tooenable hello подготовки службы Azure AD для Slack, изменение hello **состояние подготовки** слишком**на** в hello **параметры** раздела

13) Щелкните **Сохранить**. 

Это приведет к запуску hello первоначальной синхронизации все пользователи и группы, назначенные tooSlack в hello пользователей и группы раздела. Обратите внимание, что hello начальной синхронизации будет иметь tooperform больше времени, чем последующие синхронизации, которые происходят примерно каждые 10 минут, при условии, что запущена служба hello. Можно использовать hello **сведения о синхронизации** статьи toomonitor хода выполнения и следуйте ссылки tooprovisioning отчеты о действиях, описывающих все действия, выполняемые hello подготовки службы в приложении резерв.

## <a name="optional-configuring-group-object-provisioning-tooslack"></a>[Необязательно] Настройка подготовки tooSlack объекта группы 

При необходимости можно включить hello подготовки группы объектов из tooSlack Azure AD. Это поведение отличается от «присвоение группы пользователей», в этом объекте фактической группой hello Кроме tooits члены будут реплицированы с tooSlack Azure AD. Например, если в Azure AD есть группа с именем "Моя группа", идентичная группа с именем "Моя группа" будет создана в Slack.

### <a name="tooenable-provisioning-of-group-objects"></a>tooenable Подготовка группы объектов:

1) Установите hello сопоставлений **tooSlack синхронизации группы Azure Active Directory**.

2) В колонке сопоставление атрибутов hello задайте tooYes включено.

3) В hello **сопоставления атрибутов** просмотрите hello группы атрибутов, которые будут синхронизированы из tooSlack Azure AD. Обратите внимание, что атрибуты, выбранные в качестве hello **сопоставление** свойства будут групп используется toomatch hello в Slack для операций обновления. 

4) Щелкните **Сохранить**.

Это приведет к tooSlack объекты, связанные с любой группы в hello **пользователей и групп** статьи полностью синхронизируются с Azure AD tooSlack. Можно использовать hello **сведения о синхронизации** статьи toomonitor хода выполнения и следуйте ссылки tooprovisioning отчеты о действиях, описывающих все действия, выполняемые hello подготовки службы в приложении резерв.


## <a name="additional-resources"></a>Дополнительные ресурсы

* [Управление подготовкой учетных записей пользователей для корпоративных приложений](active-directory-enterprise-apps-manage-provisioning.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)
