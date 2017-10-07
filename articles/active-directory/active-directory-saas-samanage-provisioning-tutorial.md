---
title: "Руководство по настройке Samanage для автоматической подготовки пользователей с помощью Azure Active Directory | Документация Майкрософт"
description: "Узнайте, как tooconfigure Azure Active Directory tooautomatically подготовки и Отмена подготовки учетных записей пользователей tooSamanage."
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
ms.openlocfilehash: 6cb36d2cc6ce33da4f8ebba65d138bfd4f2aca9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-samanage-for-automatic-user-provisioning"></a>Руководство по настройке Samanage для автоматической подготовки пользователей


Цель этого учебника Hello — hello действия, которые следует tooperform в Samanage и Azure AD tooautomatically подготовки и Отмена подготовки учетных записей пользователей из Azure AD tooSamanage tooshow. 

## <a name="prerequisites"></a>Предварительные требования

Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:

*   клиент Azure Active Directory;
*   Клиент Samanage с hello [специалистов плана](https://www.samanage.com/pricing/) или лучше включена 
*   учетная запись пользователя в Samanage с разрешениями администратора. 

> [!NOTE]
> Hello подготовки интеграции Azure AD использует hello [Samanage REST API](https://www.samanage.com/api/), это — tooSamanage доступных команд в hello Professional плана или более высокий уровень.

## <a name="assigning-users-toosamanage"></a>Назначение пользователей tooSamanage

Azure Active Directory использует называемый «назначения» toodetermine пользователей, которые должны получать доступ tooselected приложений. В контексте hello автоматический подготовки пользователей. учетной записи синхронизируются только hello пользователей и групп, назначенных» «tooan приложения в Azure AD. 

Для настройки и включения hello подготовки службы, требуется toodecide какие пользователи или группы в Azure AD представляют Привет пользователям требуется доступ к приложению Samanage tooyour. После приняла решение, можно назначить эти приложения Samanage tooyour пользователей в соответствии с инструкциями hello здесь:

[Назначить пользователю или группе tooan корпоративного приложения](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toosamanage"></a>Важные советы для назначения пользователей tooSamanage

*   Рекомендуется один назначенный hello tootest tooSamanage настройки подготовки пользователя Azure AD. Дополнительные пользователи и/или группы можно назначить позднее.

*   При назначении tooSamanage пользователя, необходимо выбрать либо hello **пользователя** роли или другой допустимый конкретного приложения (если доступно) в диалоговом окне приветствия назначения. Hello **доступа по умолчанию** роль не будет работать для подготовки, и эти пользователи будут пропускаться.

> [!NOTE]
> Добавлены функции hello подготовки службы считывает все пользовательские роли, определенные в Samanage, а импортирует их в Azure AD, где они могут быть выбраны в диалоговом окне выберите роль hello. Эти роли будут отображаться в hello портал Azure, после включения hello подготовки службы, и завершена одного цикла синхронизации.

## <a name="configuring-user-provisioning-toosamanage"></a>Настройка подготовки tooSamanage пользователей 

Этот раздел поможет выполнить подключение учетной записи пользователя в Azure AD tooSamanage подготовки API и настройке подготовки службы toocreate hello, обновления и отключить учетные записи пользователей, назначенные в Samanage, в зависимости от назначения пользователей и групп в Azure AD.

> [!TIP]
> Можно также выбрать tooenabled на основе SAML Single Sign-On для Samanage, следуя инструкциям hello в [портал Azure](https://portal.azure.com). Единый вход можно настроить независимо от автоматической подготовки, хотя эти две возможности дополняют друг друга.


### <a name="configure-automatic-user-account-provisioning-toosamanage-in-azure-ad"></a>Настройте учетную запись автоматического пользователя подготовки tooSamanage в Azure AD.


1. В hello [портал Azure](https://portal.azure.com), Обзор toohello **Azure Active Directory > корпоративных приложений > все приложения** раздела.

2. Если вы уже настроили для единого входа Samanage, поиск экземпляра Samanage, с помощью поля поиска hello. В противном случае выберите **добавить** и выполните поиск **Samanage** в галерее приложения hello. Выберите Samanage из результатов поиска hello и добавить его в список tooyour приложений.

3. Выберите свой экземпляр Samanage, а затем выберите hello **Provisioning** вкладки.

4. Набор hello **режим подготовки** слишком**автоматического**.

    ![Подготовка Samanage](./media/active-directory-saas-samanage-provisioning-tutorial/Samanage1.png)

5. В разделе hello **учетные данные администратора** раздел, входной hello **пользователя с правами администратора и пароль администратора** вашей Samanage учетной записи. 

6. В hello портал Azure, щелкните **проверить подключение** tooensure Azure AD можно подключить приложение tooyour Samanage. При сбое подключения hello, убедитесь, что ваша учетная запись Samanage имеет разрешения администратора и повторите шаг 5.

7. Введите адрес электронной почты hello пользователя или группы, которые должны получить уведомления о подготовке ошибки в hello **уведомление по электронной почте** поле и проверьте hello флажок «Отправить уведомление по электронной почте при возникновении сбоя».

8. Щелкните **Сохранить**. 

9. Установите hello сопоставлений **tooSamanage синхронизации Azure Active Directory — пользователи**.

10. В hello **сопоставления атрибутов** просмотрите hello атрибутов пользователей, которые синхронизируются из tooSamanage Azure AD. Здравствуйте, атрибуты, выбранные в качестве **сопоставление** свойства, используемые toomatch hello учетных записей пользователей в Samanage для операций обновления. Выберите toocommit кнопку hello сохранить все изменения.

11. tooenable hello подготовки службы Azure AD для Samanage, изменение hello **состояние подготовки** слишком**на** в hello **параметры** раздела

12. Щелкните **Сохранить**. 

Эта операция запускает hello первоначальной синхронизации все пользователи и группы, назначенные tooSamanage в hello пользователей и группы раздела. Начальная синхронизация Hello принимает tooperform больше времени, чем последующие синхронизации, которые происходят примерно каждые 20 минут при условии, что запущена служба hello. Можно использовать hello **сведения о синхронизации** статьи toomonitor хода выполнения и следуйте ссылки tooprovisioning отчеты о действиях, которые описывают все действия, выполняемые hello подготовки службы.

Дополнительные сведения о способ подготовки tooread hello Azure AD использует для входа см. в разделе [отчеты о автоматический подготовки пользователей. учетной записи](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).


## <a name="additional-resources"></a>Дополнительные ресурсы

* [Управление подготовкой учетных записей пользователей для корпоративных приложений](active-directory-enterprise-apps-manage-provisioning.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Дальнейшие действия

* [Узнайте, каким образом ведет журнал tooreview и получать отчеты о действиях по подготовке](active-directory-saas-provisioning-reporting.md)
