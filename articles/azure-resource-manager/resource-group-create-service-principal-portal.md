---
title: "aaaCreate удостоверение для приложения Azure в портале | Документы Microsoft"
description: "Описывает уровень доступа tooresources toocreate новое приложение Azure Active Directory и службы-участника, который может использоваться с элементом управления доступом на основе hello в toomanage диспетчера ресурсов Azure."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 7068617b-ac5e-47b3-a1de-a18c918297b6
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 9624715ac612f42df6f9e9e67b8233bd4b914174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-portal-toocreate-an-azure-active-directory-application-and-service-principal-that-can-access-resources"></a>Использование портала toocreate приложения Azure Active Directory и участника-службы, могут обращаться к ресурсам

Если у вас есть приложение, которое требуется tooaccess или изменить ресурсы, необходимо настроить приложение Azure Active Directory (AD) и назначить tooit hello необходимые разрешения. Этот подход является более предпочтительным, чем toorunning приложение hello в своих собственных учетных данных, так как:

* Можно назначить разрешения удостоверение приложения toohello, отличаются от собственных разрешений. Как правило эти разрешения являются ограниченными tooexactly какие hello приложению toodo.
* У вас приложение hello toochange учетные данные при изменении ваши обязанности. 
* При выполнении сценария автоматической можно использовать проверку подлинности сертификата tooautomate.

В этом разделе показано, как tooperform те проходит через портал hello. Этот раздел посвящен приложения одного клиента, где приложение hello предполагаемого toorun только одной организации. Обычно однотенантная архитектура используется для создания бизнес-приложений в рамках организации.
 
## <a name="required-permissions"></a>Необходимые разрешения
toocomplete в этом разделе, необходимо иметь достаточные разрешения tooregister приложения с клиентом Azure AD и назначить роли tooa приложения hello в вашей подписке Azure. Давайте убедитесь, что имеется hello нужные разрешения tooperform эти действия.

### <a name="check-azure-active-directory-permissions"></a>Проверка разрешений в Azure Active Directory
1. Войдите в tooyour учетную запись Azure через hello [портал Azure](https://portal.azure.com).
2. Выберите **Azure Active Directory**.

     ![Выбор Azure Active Directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)
3. В Azure Active Directory выберите **Параметры пользователя**.

     ![Выбор параметров пользователя](./media/resource-group-create-service-principal-portal/select-user-settings.png)
4. Проверьте hello **регистрации приложения** параметр. Если задать слишком**Да**, не являющихся администраторами пользователи могут регистрировать приложения AD. Этот параметр означает, что любой пользователь в клиенте Azure AD hello можно зарегистрировать приложение. Можно продолжить слишком[прав доступа к подпискам Azure проверьте](#check-azure-subscription-permissions).

     ![Проверка регистрации приложений](./media/resource-group-create-service-principal-portal/view-app-registrations.png)
5. Если параметр регистрации приложения hello задано слишком**нет**, только администраторы могут регистрировать приложения. Необходимо toocheck ли ваша учетная запись имеет права администратора для клиента Azure AD hello. В разделе "Быстрые задачи" щелкните **Обзор**, а затем выберите **Найти пользователя**.

     ![Пункт "Найти пользователя"](./media/resource-group-create-service-principal-portal/find-user.png)
6. Найдите свою учетную запись и выберите ее.

     ![Поиск пользователя](./media/resource-group-create-service-principal-portal/show-user.png)
7. В разделе со сведениями об учетной записи щелкните **Роль каталога**. 

     ![Пункт "Роль каталога"](./media/resource-group-create-service-principal-portal/select-directory-role.png)
8. Просмотрите назначенную роль каталога в Azure AD. Если ваша учетная запись назначена роль пользователя toohello, но hello параметр регистрации приложения (из предыдущих шагах hello) является ограниченной tooadmin пользователей, попросите вашего администратора tooeither назначить вы tooan роль администратора или tooenable пользователей tooregister приложений.

     ![Просмотр роли](./media/resource-group-create-service-principal-portal/view-role.png)

### <a name="check-azure-subscription-permissions"></a>Проверка прав доступа к подпискам Azure
В подписке Azure учетной записи должно быть `Microsoft.Authorization/*/Write` доступ к tooassign tooa роль AD. Это действие предоставляется посредством hello [владельца](../active-directory/role-based-access-built-in-roles.md#owner) роли или [администратор доступа пользователя](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) роли. Если ваша учетная запись назначается toohello **участника** роли, у вас достаточно разрешений. Вы получите ошибку при попытке роль участника tooa tooassign hello службы. 

toocheck разрешения по подписке:

1. Если вы не уже видите учетной записи Azure AD из предыдущих шагах hello, выберите **Azure Active Directory** hello левой панели.

2. Найдите свою учетную запись Azure AD. В разделе "Быстрые задачи" щелкните **Обзор**, а затем выберите **Найти пользователя**.

     ![Пункт "Найти пользователя"](./media/resource-group-create-service-principal-portal/find-user.png)
2. Найдите свою учетную запись и выберите ее.

     ![Поиск пользователя](./media/resource-group-create-service-principal-portal/show-user.png) 
     
3. Щелкните **Ресурсы Azure**.

     ![Выбор ресурсов](./media/resource-group-create-service-principal-portal/select-azure-resources.png) 
3. Просмотр назначенных ролей и определите tooassign соответствующие разрешения роли приложения tooa AD. Если это не так, попросите администратора вашей подписки tooadd вы tooUser доступа к роли администратора. Следующие изображения hello назначенный toohello роли-владельца для двух подписок, это означает, что этот пользователь имеет достаточные разрешения является пользователь hello. 

     ![Просмотр разрешений](./media/resource-group-create-service-principal-portal/view-assigned-roles.png)

## <a name="create-an-azure-active-directory-application"></a>Создание приложения Azure Active Directory
1. Войдите в tooyour учетную запись Azure через hello [портал Azure](https://portal.azure.com).
2. Выберите **Azure Active Directory**.

     ![Выбор Azure Active Directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)

4. Щелкните **Регистрация приложений**.   

     ![Пункт "Регистрация приложений"](./media/resource-group-create-service-principal-portal/select-app-registrations.png)
5. Выберите **Добавить**.

     ![Действие "Добавить приложение"](./media/resource-group-create-service-principal-portal/select-add-app.png)

6. Укажите имя и URL-адрес для приложения hello. Выберите либо **веб-приложения и API** или **собственного** для типа приложения hello требуется toocreate. После задания значения hello, выберите **создать**.

     ![указание имени приложения](./media/resource-group-create-service-principal-portal/create-app.png)

Приложение создано.

## <a name="get-application-id-and-authentication-key"></a>Получение идентификатора приложения и ключа проверки подлинности
Программным способом входа в систему требуется идентификатор hello для приложения и ключ проверки подлинности. те значения, tooget hello используйте следующие шаги:

1. В Azure Active Directory в разделе **Регистрация приложений** выберите нужное приложение.

     ![Выбор приложения](./media/resource-group-create-service-principal-portal/select-app.png)
2. Копировать hello **идентификатор приложения** и сохранить ее в коде приложения. Здравствуйте, приложения hello [образцы приложений](#sample-applications) значение toothis, что идентификатор hello клиента см. раздел.

     ![Идентификатор клиента](./media/resource-group-create-service-principal-portal/copy-app-id.png)
3. Выберите ключ проверки подлинности toogenerate **ключей**.

     ![Пункт "Ключи"](./media/resource-group-create-service-principal-portal/select-keys.png)
4. Введите описание ключа hello и длительность для ключа hello. Затем нажмите кнопку **Сохранить**.

     ![Сохранение ключа](./media/resource-group-create-service-principal-portal/save-key.png)

     После сохранения ключа hello, отображается значение hello hello ключа. Скопируйте это значение невозможно, поскольку ключ может tooretrieve hello позже. Значение ключа hello предоставить toolog идентификатор приложения hello в как приложение hello. Сохраните значение ключа hello, где приложение может вернуть их.

     ![сохраненный ключ](./media/resource-group-create-service-principal-portal/copy-key.png)

## <a name="get-tenant-id"></a>Получение идентификатора клиента
Программным способом входа в систему необходимо ИД клиента toopass hello вместе с запросом проверки подлинности. 

1. Идентификатор клиента hello tooget, выберите **свойства** для вашего клиента Azure AD. 

     ![Выбор свойств Azure AD](./media/resource-group-create-service-principal-portal/select-ad-properties.png)

2. Копировать hello **каталог с Идентификатором**. Это и есть ваш идентификатор клиента.

     ![Идентификатор клиента](./media/resource-group-create-service-principal-portal/copy-directory-id.png)

## <a name="assign-application-toorole"></a>Назначьте toorole приложения
tooaccess ресурсам в подписке, необходимо назначить роль tooa приложения hello. Решите, какую роль представляет hello нужные разрешения для приложения hello. toolearn о hello доступным ролям, в разделе [RBAC: встроенные роли](../active-directory/role-based-access-built-in-roles.md).

Можно установить область hello на уровне hello hello подписки, группы ресурсов или ресурсов. Разрешения, наследуемые toolower уровни области действия. Например для добавления роли модуля чтения toohello приложения для группы ресурсов есть может считать группы ресурсов hello и все ресурсы, которые он содержит.

1. Перейти на уровень toohello области, в которых надо tooassign hello приложению. Например, tooassign роль в области hello подписки, выберите **подписки**. Или же вы можете выбрать группу ресурсов либо отдельный ресурс.

     ![выбрать подписку](./media/resource-group-create-service-principal-portal/select-subscription.png)

2. Выберите приложение hello tooassign hello определенной подписки (группа ресурсов или ресурсов) для.

     ![выбрать подписку для назначения](./media/resource-group-create-service-principal-portal/select-one-subscription.png)

3. Выберите **Управление доступом (IAM)**.

     ![выбрать доступ](./media/resource-group-create-service-principal-portal/select-access-control.png)

4. Выберите **Добавить**.

     ![выбрать "добавить"](./media/resource-group-create-service-principal-portal/select-add.png)
6. Выберите роль hello нужно tooassign toohello приложения. Hello на рисунке показаны hello **чтения** роли.

     ![выбрать роль](./media/resource-group-create-service-principal-portal/select-role.png)

8. Найдите приложение и выберите его.

     ![Поиск приложения](./media/resource-group-create-service-principal-portal/search-app.png)
9. Выберите **ОК** toofinish назначение роли hello. Вы видите приложение hello списка пользователей, назначенных роли tooa для данной области.

## <a name="log-in-as-hello-application"></a>Войдите в систему как приложение hello

Настройка приложения в Azure Active Directory завершена. У вас есть код и ключа toouse для входа в приложение hello. приложение Hello назначается роль tooa делает ее определенные действия, которые они могут выполнять. Сведения о входе в систему как hello приложения с помощью различных платформ см. в разделе:

* [PowerShell](resource-group-authenticate-service-principal.md#provide-credentials-through-powershell)
* [Интерфейс командной строки Azure](resource-group-authenticate-service-principal-cli.md#provide-credentials-through-azure-cli)
* [REST](/rest/api/#create-the-request)
* [.NET](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [Java](/java/azure/java-sdk-azure-authenticate)
* [Node.js](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [Python](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [Ruby](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)


## <a name="next-steps"></a>Дальнейшие действия
* tooset копирование многопользовательского приложения, в разделе [tooauthorization руководство разработчика с hello API диспетчера ресурсов Azure](resource-manager-api-authentication.md).
* toolearn о политике безопасности, в разделе [управления доступом на основе ролей Azure](../active-directory/role-based-access-control-configure.md).  
* Список доступных действий, которые могут быть предоставлены или запрещены toousers см. в разделе [операций поставщика ресурсов диспетчера ресурсов Azure](../active-directory/role-based-access-control-resource-provider-operations.md).
