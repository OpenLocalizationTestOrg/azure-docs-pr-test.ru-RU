---
title: "aaaAdd владельцы и пользователи в Azure DevTest Labs | Документы Microsoft"
description: "Добавьте в DevTest Labs Azure с помощью портала Azure hello или PowerShell владельцы и пользователи"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 4f51d9a5-2702-45f0-a2d5-a3635b58c416
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: 2a98f5fe1efbd7c23e0d97f58f47c37462aed3b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-owners-and-users-in-azure-devtest-labs"></a>Добавление владельцев и пользователей в Azure DevTest Labs
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/How-to-set-security-in-your-DevTest-Lab/player]
> 
> 

Доступом к Azure DevTest Labs управляет [служба управления доступом на основе ролей Azure (RBAC)](../active-directory/role-based-access-control-what-is.md). С помощью RBAC, можно разделить обязанностей в рамках команды в *ролей* которой предоставлять только hello объем tooperform toousers необходимости доступа к своей работы. RBAC предусматривает такие три основные роли: *Владелец*, *Пользователь DevTest Labs* и *Участник*. В этой статье вы узнаете, какие действия могут выполняться в каждом из трех основных ролей RBAC hello. После этого вы узнаете, как лаборатории tooa пользователей tooadd - оба через hello портала и через сценарий PowerShell и каким образом пользователи tooadd на hello уровня подписки.

## <a name="actions-that-can-be-performed-in-each-role"></a>Действия, которые можно выполнять в каждой роли
Пользователю можно назначить одну из трех основных ролей:

* Владелец
* Пользователь DevTest Labs
* Участник

Hello Следующая таблица показывает hello действия, выполненные пользователями в каждой из этих ролей.

| **Действия, которые могут выполнять пользователи с этой ролью** | **Пользователь DevTest Labs** | **Владелец** | **Участник** |
| --- | --- | --- | --- |
| **Задачи лаборатории** | | | |
| Добавление пользователей tooa лаборатории |Нет |Да |Нет |
| Обновление параметров стоимости |Нет |Да |Да |
| **Базовые задачи виртуальных машин** | | | |
| Добавление и удаление пользовательских образов |Нет |Да |Да |
| Добавление, обновление и удаление формул |Да |Да |Да |
| Разрешенные образы Azure Marketplace |Нет |Да |Да |
| **Задачи виртуальных машин** | | | |
| Создание виртуальных машин |Да |Да |Да |
| Запуск, остановка и удаление виртуальных машин |Только виртуальные машины, созданные пользователем hello |Да |Да |
| Обновление политик виртуальных машин |Нет |Да |Да |
| Добавление и удаление дисков данных виртуальных машин |Только виртуальные машины, созданные пользователем hello |Да |Да |
| **Задачи артефактов** | | | |
| Добавление и удаление репозиториев артефактов |Нет |Да |Да |
| Применение артефактов |Да |Да |Да |

> [!NOTE]
> Если пользователь создает виртуальную Машину, этот пользователь будет автоматически назначено toohello **владельца** роль hello создания виртуальной Машины.
> 
> 

## <a name="add-an-owner-or-user-at-hello-lab-level"></a>Добавить владельца или пользователя на уровне hello лаборатории
Владельцы и пользователи могут добавляться на уровне лаборатории hello через портал Azure hello. Можно также добавить внешних пользователей с допустимой [учетной записью Майкрософт (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account).
следующие шаги Hello проводит пользователя через процесс добавления лаборатории tooa владельцами или пользователями в Azure DevTest Labs hello:

1. Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Выберите **дополнительные службы**, а затем выберите **DevTest Labs** из списка hello.
3. Выберите из списка hello лабораториям hello требуемой лаборатории.
4. В колонке hello лаборатории выберите **конфигурации**. 
5. На hello **конфигурации** колонке выберите **пользователей**.
6. На hello **пользователей** колонке выберите **+ добавить**.
   
    ![Добавить пользователя](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
7. На hello **выберите роль** колонки, hello выберите нужную роль. Здравствуйте, раздел [действия, которые могут быть выполнены в каждой роли](#actions-that-can-be-performed-in-each-role) списки hello различные действия, выполненные пользователями в hello владельца, DevTest пользователя или участника роли.
8. На hello **Добавление пользователей** колонки, введите адрес электронной почты hello или имя пользователя hello требуется tooadd в указанной роли hello. Если не удается найти пользователя hello, сообщение об ошибке описывается проблема hello. При обнаружении hello пользователя этот пользователь перечислены и выбраны. 
9. Щелкните **Выбрать**.
10. Выберите **ОК** tooclose hello **добавить доступ** колонку.
11. При возвращении toohello **пользователей** колонке hello пользователь был добавлен.  

## <a name="add-an-external-user-tooa-lab-using-powershell"></a>Добавить лаборатории tooa внешнего пользователя, с помощью PowerShell
Кроме того при tooadding пользователей в hello портал Azure, можно добавить лаборатории tooyour внешнего пользователя, с помощью сценария PowerShell. В hello просто следующий пример, измените значения параметров hello под hello **toochange значения** комментарий.
Вы можете получить hello `subscriptionId`, `labResourceGroup`, и `labName` значения из колонки лаборатории hello в hello портал Azure.

> [!NOTE]
> Образец Hello скрипта предполагается, что, hello указанный пользователь был добавлен в качестве гостя toohello Active Directory и завершится ошибкой, если это не так hello. пользователь не зарегистрирован в hello лаборатории tooa Active Directory, tooadd использовать hello Azure портала tooassign hello tooa роль пользователя согласно инструкциям в разделе "hello" [добавьте владельца или пользователя на уровне лаборатории hello](#add-an-owner-or-user-at-the-lab-level).   
> 
> 

    # Add an external user in DevTest Labs user role tooa lab
    # Ensure that guest users can be added toohello Azure Active directory:
    # https://azure.microsoft.com/en-us/documentation/articles/active-directory-create-users/#set-guest-user-access-policies

    # Values toochange
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource name here>"
    $labName = "<Enter lab name here>"
    $userDisplayName = "<Enter user's display name here>"

    # Log into your Azure account
    Login-AzureRmAccount

    # Select hello Azure subscription that contains hello lab. 
    # This step is optional if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Retrieve hello user object
    $adObject = Get-AzureRmADUser -SearchString $userDisplayName

    # Create hello role assignment. 
    $labId = ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    New-AzureRmRoleAssignment -ObjectId $adObject.Id -RoleDefinitionName 'DevTest Labs User' -Scope $labId

## <a name="add-an-owner-or-user-at-hello-subscription-level"></a>Добавление владельца или пользователя на уровне подписки hello
Разрешения Azure переносятся из родительской области toochild область в Azure. Таким образом, владельцы подписки Azure, содержащей лаборатории, автоматически являются владельцами этих лабораторий. Они также являются hello виртуальные машины и другие ресурсы, созданные пользователями лаборатории hello и hello Azure DevTest Labs службы. 

Можно добавить дополнительных владельцев лаборатории tooa через колонки hello лаборатории в hello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040). Однако hello добавлена владельца области администрирования более узкий выше владельца подписки hello области. Например hello добавлены владельцы имеют полный доступ toosome hello ресурсов, созданные в подписке hello hello DevTest Labs службы. 

tooadd tooan владелец подписки Azure, выполните следующие действия.

1. Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Выберите **более служб**, а затем выберите **подписки** из списка hello.
3. Выберите подписку требуемого hello.
4. Щелкните значок **Доступ** . 
   
    ![Доступ к пользователям](./media/devtest-lab-add-devtest-user/access-users.png)
5. На hello **пользователей** колонке выберите **добавить**.
   
    ![Добавить пользователя](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
6. На hello **выберите роль** колонке выберите **владельца**.
7. На hello **Добавление пользователей** колонки, введите имя или адрес электронной почты hello hello пользователя требуется tooadd в качестве владельца. Если не удается найти пользователя hello, появляется сообщение об ошибке, поясняющий hello. Если hello пользователь найден, этот пользователь будет помещен в hello **пользователя** текстовое поле.
8. Выберите имя hello найти пользователя.
9. Щелкните **Выбрать**.
10. Выберите **ОК** tooclose hello **добавить доступ** колонку.
11. При возвращении toohello **пользователей** колонке hello пользователь добавлен в качестве владельца. Этот пользователь будет владельца любого labs, созданных под этой подпиской и таким образом может tooperform владельца задачи. 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

