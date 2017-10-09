---
title: "Управление доступом на основе ролей (RBAC) toocontrol aaaAzure toocreate права доступа к и управление запросами поддержки | Документы Microsoft"
description: "Azure toocontrol управления доступом на основе ролей (RBAC) toocreate права доступа и управления ими запросов на получение поддержки"
author: ganganarayanan
ms.author: gangan
ms.date: 1/31/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: 58a0ca9d-86d2-469a-9714-3b8320c33cf5
ms.openlocfilehash: c68a699ac870fa6bf371deb8ed0424848f39acf0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-role-based-access-control-rbac-toocontrol-access-rights-toocreate-and-manage-support-requests"></a>Azure toocontrol управления доступом на основе ролей (RBAC) toocreate права доступа и управления ими запросов на получение поддержки

[Управление доступом на основе ролей (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) обеспечивает точный контроль доступа в Azure.
Поддерживает создание запроса в hello портал Azure [portal.azure.com](https://portal.azure.com), использует toodefine модели RBAC в Azure, можно создавать и управлять запросов поддержки.
Доступ предоставляется путем назначения hello соответствующие RBAC роли toousers, группы и приложения в определенной области, который может быть подписки, группы ресурсов или ресурс.

Рассмотрим пример: как владелец группы ресурсов с разрешениями на чтение в области видимости hello подписки, можно управлять ресурсами hello в группе ресурсов hello, таких как веб-сайты, виртуальные машины и подсети.
Тем не менее при попытке toocreate запрос на техническую поддержку для ресурса виртуальной машины hello, возникнет следующая ошибка hello

![Ошибка подписки](./media/create-manage-support-requests-using-access-control/subscription-error.png)

В управлении запрос поддержки необходимо разрешение на запись или роли, имеющей hello поддерживает действие Microsoft.Support/* на возможности toocreate toobe область hello подписки и управление запросами на поддержку.

Hello следующей статьей объясняется, как можно использовать пользовательские toocreate управление доступом на основе ролей (RBAC) в Azure и управлять запросов поддержки в hello портал Azure.

## <a name="getting-started"></a>Приступая к работе

С помощью приведенном выше примере hello, будет может toocreate запрос на техническую поддержку для ресурса, если были назначены пользовательской роли RBAC в подписке hello владельцем подписки hello.
[Пользовательские роли RBAC](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) могут создаваться с помощью Azure PowerShell, Azure интерфейс командной строки (CLI) и hello REST API.

Свойство действия Hello пользовательские роли указывает, что hello Azure операций toowhich hello роль предоставляет доступ.
toocreate пользовательской роли для поддержки управления запроса hello роль должна иметь действие hello Microsoft.Support/*

Ниже приведен пример пользовательской роли, вы можете использовать toocreate и управлять поддерживает запросы.
Мы назвали этой роли «Участник запросов поддержки» и, как мы называем toohello настраиваемой роли в этой статье.

``` Json
{
    "Name":  "Support Request Contributor",
    "Id":  "1f2aad59-39b0-41da-b052-2fb070bd7942",
    "IsCustom":  true,
    "Description":  "Lets you create and manage support tickets.",
    "Actions":  [
                    "Microsoft.Support/*"
                ],
    "NotActions":  [
                   ],
    "AssignableScopes":  [
                             "/"
                         ]
}
```

Выполните hello действия, описанные в [в этом видеоролике](https://www.youtube.com/watch?v=-PaBaDmfwKI) toolearn как toocreate пользовательской роли для вашей подписки.

## <a name="create-and-manage-support-requests-in-hello-azure-portal"></a>Создание и управление ими запросов поддержки в hello портал Azure

Рассмотрим пример — вы являетесь владельцем hello подписки «Visual Studio подписки MSDN.»
Сергей является вашей однорангового узла, являющийся toosome владельца ресурса hello групп ресурсов в этой подписке и имеет подписки toohello разрешение "чтение".
Правильно toogive доступа tooyour однорангового узла, Joe, toocreate возможность hello и управление запросами в службу поддержки для hello ресурсов в данной подписке.

1. Первый шаг Hello — toogo toohello подписки и в поле «Параметры» появится список пользователей. Выберите пользователя hello Joe, кто имеет доступ для чтения на hello подписки и позволяет назначить новый toohim пользовательской роли.

    ![Добавление роли](./media/create-manage-support-requests-using-access-control/add-role.png)

2. В колонке «Пользователи» hello, щелкните «Добавить». Выберите hello пользовательской роли «Участник запросов поддержки» из списка hello ролей

    ![Добавление роли участника с доступом к службе поддержки](./media/create-manage-support-requests-using-access-control/add-support-contributor-role.png)

3. После выбора имени роли hello, нажмите «Добавить пользователей» и введите учетные данные электронной почты hello Джо. Нажмите "Выбрать".

    ![Добавление пользователей](./media/create-manage-support-requests-using-access-control/add-users.png)

4. Нажмите кнопку «ОК» tooproceed

    ![Предоставление доступа](./media/create-manage-support-requests-using-access-control/add-access.png)

5. Вы увидите hello пользователя с вновь добавленный hello пользовательской роли «Поддержка запроса участник» в подписке hello, для которого вы являетесь владельцем hello

    ![Добавлен пользователь](./media/create-manage-support-requests-using-access-control/user-added.png)

    При входе в портал hello Joe он видит toowhich подписки hello, когда он был добавлен.

7. Сергей нажимает кнопку «Нового запроса на обслуживание» из колонки «Справка и поддержка» hello и можно создать запросы на поддержку для «Visual Studio Ultimate с MSDN»

    ![Новый запрос на техническую поддержку](./media/create-manage-support-requests-using-access-control/new-support-request.png)

8. Нажав кнопку «Все поддерживают запросы» Joe можно просмотреть список запросов поддержки, созданному для этой подписки hello ![случае представление сведений](./media/create-manage-support-requests-using-access-control/case-details-view.png)

## <a name="remove-support-request-access-in-hello-azure-portal"></a>Удаление поддержки запрашивать доступ в hello портал Azure

Так же, как она возможных toogrant доступа tooa пользователя toocreate и управление запросами на поддержку это возможных tooremove доступ также пользователю hello.
tooremove hello toocreate возможность управлять запросов поддержки, перейдите toohello подписки, нажмите кнопку «Параметры» и нажмите кнопку hello пользователя (в данном случае Joe).
Щелкните правой кнопкой мыши имя роли hello, «Участник запросов поддержки» и нажмите кнопку «Удалить»

![Отзыв доступа для создания запросов на поддержку](./media/create-manage-support-requests-using-access-control/remove-support-request-access.png)

Если Сергей журналы портала toohello и пытается установить toocreate запрос на техническую поддержку, он обнаруживает hello следующая ошибка

![Ошибка подписки 2](./media/create-manage-support-requests-using-access-control/subscription-error-2.png)

Дмитрий не сможет просмотреть запросы на поддержку, щелкнув "Все запросы на поддержку".

![Представление сведений об обращении 2](./media/create-manage-support-requests-using-access-control/case-details-view-2.png)
