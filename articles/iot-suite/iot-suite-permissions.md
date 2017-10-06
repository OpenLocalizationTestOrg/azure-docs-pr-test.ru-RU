---
title: "aaaAzure IoT Suite и Azure Active Directory | Документы Microsoft"
description: "Описывает, как Azure IoT Suite использует Azure Active Directory toomanage разрешения."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 246228ba-954a-4d96-b6d6-e53e4590cb4f
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: dobett
ms.openlocfilehash: 4768630f2de4bb431731fbd4e8929232bc80b9f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-on-hello-azureiotsuitecom-site"></a>Разрешения на сайт azureiotsuite.com hello

## <a name="what-happens-when-you-sign-in"></a>Что происходит при входе

Здравствуйте, войдите в первый раз [azureiotsuite.com][lnk-azureiotsuite], hello сайту определяет, основано на hello в настоящее время уровни разрешений hello выбранного клиента Azure Active Directory (AAD) и Azure подписка.

1. Во-первых toopopulate hello список клиентов показано далее tooyour username, hello сайта выясняется, из Azure какие клиенты AAD, вы принадлежите. В настоящее время hello сайта только могут получить токены пользователя для одного клиента одновременно. Таким образом при переключении клиентов с помощью раскрывающегося списка hello в правом верхнем углу hello сайта hello входе вы toothat клиента tooobtain hello токены для этого клиента.

2. После этого сайта hello выясняется, из подписки, которые связаны с hello выбранного клиента Azure. Вы видите hello доступные подписки, при создании новых предварительно настроенных решений.

3. Наконец hello сайта получает все ресурсы hello в подписках hello и группы ресурсов отмечен как предварительно настроенных решений и заполняет hello плитки на домашней странице приветствия.

Hello в следующих разделах описаны hello ролей, управляющих доступа toohello предварительно настроенных решений.

## <a name="aad-roles"></a>Роли AAD

роли AAD Hello hello возможность подготовки предварительно настроенных решений для управления пользователями в предварительно настроенных решений.

Дополнительные сведения о ролях администратора в AAD см. в статье [Назначение ролей администратора в Azure AD][lnk-aad-admin]. Hello текущего статье основное внимание уделяется hello **глобального администратора** и hello **пользователя** ролей каталога, как используется hello предварительно настроенных решений.

### <a name="global-administrator"></a>Глобальный администратор

В одном клиенте AAD может быть несколько глобальных администраторов.

* При создании клиент AAD, вы, по умолчанию hello глобального администратора из этого клиента.
* глобальный администратор Hello можно подготовить предварительно настроенных решений и назначается **администратора** роли для приложения hello в свой клиент AAD.
* Если другой пользователь в hello же клиента AAD создается приложение, роль по умолчанию hello предоставил — глобальный администратор toohello **ReadOnly**.
* Глобальный администратор может назначить tooroles пользователей для приложений, использующих hello [портал Azure][lnk-portal].

### <a name="domain-user"></a>Пользователь домена

На каждый клиент AAD может приходиться много пользователей домена.

* Пользователь домена можно подготовить предварительно настроенных решений по hello [azureiotsuite.com] [ lnk-azureiotsuite] сайта. По умолчанию, пользователь домена hello предоставляется hello **администратора** роли в hello подготовить приложение.
* Пользователь домена может создавать приложения с помощью скрипт build.cmd hello в hello [azure iot удаленного мониторинга][lnk-rm-github-repo], [azure-iot — диагностическое обслуживание] [ lnk-pm-github-repo], или [-iot подключен фабрики azure] [ lnk-cf-github-repo] репозитория. Однако роль по умолчанию hello предоставлено является пользователем домена toohello **ReadOnly**, так как пользователь домена не имеет разрешений роли tooassign.
* Если другой пользователь в клиенте AAD hello создается приложение, пользователь домена hello назначается hello **ReadOnly** роли по умолчанию для этого приложения.
* Пользователь домена не может назначать роли для приложений, поэтому он не может добавлять пользователей к ролям или присваивать пользователям роли для приложения, даже если он подготовил это приложение.

### <a name="guest-user"></a>Гостевой пользователь

В одном клиенте AAD может быть много гостевых пользователей. Гостевые пользователи обладают ограниченным набором прав в клиенте AAD hello. В результате гостевых пользователей не удается подготовить предварительно настроенных решений в клиенте AAD hello.

Дополнительные сведения о пользователях и ролях в Azure Active Directory см. в разделе hello следующие ресурсы:

* [Добавление новых пользователей или пользователей с учетными записями Майкрософт в Azure Active Directory][lnk-create-edit-users]
* [Назначить пользователей tooapps][lnk-assign-app-roles]

## <a name="azure-subscription-administrator-roles"></a>Роли администратора подписки Azure

роли администратора Azure Hello управлять toomap возможность hello клиент tooan AD подписки Azure.

Дополнительные сведения о роли администратора Azure hello в статье hello [как tooadd или изменить Соадминистратор Azure, администратор службы и учетной записи администратора][lnk-admin-roles].

## <a name="application-roles"></a>Роли приложений

роли приложения Hello управления доступа toodevices предварительно настроенного решения.

В подготовленном приложении существует две определенные и одна неявная роль.

* **Администрирование:** имеет полный доступ tooadd, управление, удаление устройств и изменить параметры.
* **Только для чтения.** Просмотр устройств, правил, действий, заданий и телеметрии.

Можно найти hello разрешения назначены роли tooeach в hello [RolePermissions.cs] [ lnk-resource-cs] исходный файл.

### <a name="changing-application-roles-for-a-user"></a>Изменение ролей приложений для пользователя

Можно использовать следующие процедуры toomake пользователя в Active Directory администратор предварительно настроенного решения hello.

Должен быть toochange роли глобального администратора AAD для пользователя:

1. Go toohello [портал Azure][lnk-portal].
2. Выберите **Azure Active Directory**.
3. Убедитесь, что вы используете directory hello, выбранное на azureiotsuite.com при подготовке решения. Если у вас несколько каталогов, связанных с подпиской, можно переключаться между их, если щелкнуть имя учетной записи в hello правой верхней части портала hello.
4. Щелкните **Корпоративные приложения**, а затем **Все приложения**.
4. Отобразите **все приложения** с состоянием **Любой**. Затем найдите приложения с именем вашего предварительно настроенного решения.
5. Щелкните имя приложения hello, совпадающим с именем предварительно настроенных решений hello.
6. Щелкните **Пользователи и группы**.
7. Выберите пользователя hello требуется tooswitch ролей.
8. Нажмите кнопку **назначить** и роли выберите hello (такие как **администратора**) хотелось бы tooassign toohello пользователя, щелкните флажок hello.

## <a name="faq"></a>Часто задаваемые вопросы

### <a name="im-a-service-administrator-and-id-like-toochange-hello-directory-mapping-between-my-subscription-and-a-specific-aad-tenant-how-do-i-complete-this-task"></a>Я администратором службы и как toochange hello каталогов сопоставление между подпиской и конкретного клиента AAD. Как выполнить эту задачу?

1. Go toohello [классический портал Azure][lnk-classic-portal], нажмите кнопку **параметры** в списке hello служб hello левой стороны.
2. Выберите подписку hello, которой вы хотите сопоставление каталога toochange hello в.
3. Щелкните **Изменить каталог**.
4. Выберите hello **каталога** хотелось бы toouse в раскрывающемся списке hello. Щелкните стрелку «вперед» hello.
5. Подтвердите сопоставление каталога hello и затронутых соадминистраторов. При перемещении из другого каталога, удаляются все соадминистраторы из исходного каталога hello hello.

### <a name="im-a-domain-usermember-on-hello-aad-tenant-and-ive-created-a-preconfigured-solution-how-do-i-get-assigned-a-role-for-my-application"></a>Я пользователя или члена домена на приветствия клиента AAD и создадим предварительно настроенных решений. Как мне получить роль для своего приложения?

Попросите toomake глобального администратора вы глобального администратора на hello AAD клиента, а затем назначьте роли toousers самостоятельно. Кроме того, попросите tooassign глобального администратора вы непосредственно роли. Если вы хотите toochange hello AAD клиента, который был развернут предварительно настроенного решения, см. следующий вопрос hello.

### <a name="how-do-i-switch-hello-aad-tenant-my-remote-monitoring-preconfigured-solution-and-application-are-assigned-to"></a>Как переключаться клиента AAD hello назначаются Мой удаленного мониторинга предварительно настроенных решений и приложений?

Можно запустить развернутую облачную службу со страницы <https://github.com/Azure/azure-iot-remote-monitoring> и повторить развертывание в новом клиенте AAD. Поскольку являются, по умолчанию является глобальным администратором при создании клиент AAD имеется tooadd разрешения пользователей и назначить роли пользователей toothose.

1. Создайте каталог AAD в hello [портал Azure][lnk-portal].
2. Go слишком<https://github.com/Azure/azure-iot-remote-monitoring>.
3. Выполните команду `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (например, `build.cmd cloud debug myRMSolution`).
4. При появлении запроса установите hello **tenantid** toobe клиент только что созданный вместо предыдущего клиента.

### <a name="i-want-toochange-a-service-administrator-or-co-administrator-when-logged-in-with-an-organisational-account"></a>Я хочу toochange администратором служб или Соадминистратора, войдя в систему с учетной записью работы

См. в статье поддержка hello [изменение администратора службы и Соадминистратор, войдя в систему с учетной записью работы][lnk-service-admins].

### <a name="why-am-i-seeing-this-error-your-account-does-not-have-hello-proper-permissions-toocreate-a-solution-please-check-with-your-account-administrator-or-try-with-a-different-account"></a>Почему появляется ошибка «Ваша учетная запись не имеет toocreate hello соответствующие разрешения решения. Обратитесь к администратору учетной записи или попробуйте использовать другую учетную запись»

Рассмотрим следующие схемы рекомендации hello.

![][img-flowchart]

> [!NOTE]
> При продолжении toosee hello ошибка после проверки глобального администратора в клиенте AAD hello и соадминистратор для подписки hello, попросите администратора учетной записи удаления пользователя hello и переназначить необходимых разрешений в указанном порядке. Во-первых добавить пользователя hello как глобальный администратор, а затем добавьте пользователя в качестве соадминистратора на hello подписки Azure. Если проблемы не удается устранить, обратитесь в службу [справки и поддержки][lnk-help-support].

### <a name="why-am-i-seeing-this-error-when-i-have-an-azure-subscription-an-azure-subscription-is-required-toocreate-pre-configured-solutions-you-can-create-a-free-trial-account-in-just-a-couple-of-minutes"></a>Почему эта ошибка появляется при наличии подписки Azure? «Подписка Azure является обязательным toocreate предварительно настроенных решений. Вы можете создать бесплатную пробную учетную запись всего за несколько минут".

Если точно известно, что у вас есть подписка Azure, проверить сопоставление для вашей подписки клиентов hello и убедитесь, что клиент правильно hello выбран в раскрывающемся списке hello. Если были проверены hello требуемого правильность клиента, выполните hello предшествующий схемы и проверить сопоставление hello о подписке и этого клиента AAD.

## <a name="next-steps"></a>Дальнейшие действия
toocontinue изучения IoT Suite см. способы [настроить предварительно настроенных решений][lnk-customize].

[img-flowchart]: media/iot-suite-permissions/flowchart.png

[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-rm-github-repo]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-pm-github-repo]: https://github.com/Azure/azure-iot-predictive-maintenance
[lnk-cf-github-repo]: https://github.com/Azure/azure-iot-connected-factory
[lnk-aad-admin]: ../active-directory/active-directory-assign-admin-roles.md
[lnk-classic-portal]: https://manage.windowsazure.com/
[lnk-portal]: https://portal.azure.com/
[lnk-create-edit-users]: ../active-directory/active-directory-create-users.md
[lnk-assign-app-roles]: ../active-directory/active-directory-coreapps-assign-user-azure-portal.md
[lnk-service-admins]: https://azure.microsoft.com/support/changing-service-admin-and-co-admin/
[lnk-admin-roles]: ../billing/billing-add-change-azure-subscription-administrator.md
[lnk-resource-cs]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/DeviceAdministration/Web/Security/RolePermissions.cs
[lnk-help-support]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
