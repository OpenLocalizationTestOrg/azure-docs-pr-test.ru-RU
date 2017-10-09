---
title: "aaaAdd лаборатории tooa ВМ в Azure DevTest Labs | Документы Microsoft"
description: "Узнайте, как tooadd лаборатории tooa виртуальной машины в Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: tarcher
ms.openlocfilehash: 82838e4349550db56de311264c188140b9556b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-vm-tooa-lab-in-azure-devtest-labs"></a>Добавьте лаборатории tooa ВМ в Azure DevTest Labs
Если вы уже [создали свою первую виртуальную машину](devtest-lab-create-first-vm.md), скорее всего, вы использовали предварительно загруженный [образ Мarketplace](devtest-lab-configure-marketplace-images.md). Теперь следует tooadd последующие виртуальные машины tooyour лаборатории можно также *базового* , либо [пользовательского образа](devtest-lab-create-template.md) или [формула](devtest-lab-manage-formulas.md). Этот учебник поможет выполнить с помощью hello Azure портала tooadd лаборатории tooa ВМ в DevTest Labs.

В этой статье также показано, как toomanage hello артефакты для виртуальной Машины в лаборатории.

## <a name="steps-tooadd-a-vm-tooa-lab-in-azure-devtest-labs"></a>Действия tooadd лаборатории tooa ВМ в Azure DevTest Labs
1. Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Выберите **более служб**, а затем выберите **DevTest Labs** из списка hello.
1. Выберите из списка hello лабораториям hello лаборатории, в которой будет toocreate hello виртуальной Машины.  
1. В лаборатории hello **Обзор** колонке выберите **+ добавить**.  

    ![Кнопка добавления виртуальной машины](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. На hello **выберите базовый** колонке выберите база для hello виртуальной Машины.
1. На hello **виртуальной машины** колонки, введите имя для новой виртуальной машины hello в hello **имя виртуальной машины** текстовое поле.

    ![Колонка виртуальной машины лаборатории](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. Введите **имя пользователя** , которой предоставляются права администратора на виртуальной машине hello.  
1. Если вы хотите toouse пароль хранится в вашей [секретное хранилище](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store)выберите **сохраненного секрета**и укажите значение ключа, которое соответствует tooyour секрет (пароль). В противном случае введите пароль в hello текстовое поле с меткой **введите значение**.
1. Hello **тип диска виртуальной машины** определяет, какой тип диска хранилища допустим для hello виртуальных машин в лаборатории hello.
1. Выберите **размер виртуальной машины** и выберите один из hello предопределенные элементы, определяющие hello процессорных ядер, объем оперативной памяти и размер жесткого диска hello toocreate hello виртуальной Машины.
1. Выберите **артефакты** - списке hello артефактов - выберите и настройте hello артефакты, что требуется tooadd toohello базового образа.
    **Примечание:** Если вы будете новый Labs tooDevTest или настройка артефакты, см. toohello [Добавление существующих артефактов tooa ВМ](#add-an-existing-artifact-to-a-vm) статьи, а затем вернитесь сюда, после завершения.
1. Выберите **Дополнительные параметры** сеть виртуальной Машины hello tooconfigure параметры и срок действия параметров. 

   tooset параметр истечения срока действия, выберите значок toospecify hello календаря, дата, на котором hello виртуальной Машины будут автоматически удалены.  По умолчанию hello виртуальных Машин никогда не истекает. 
1. Если требуется tooview или копировать hello шаблона диспетчера ресурсов Azure, см. toohello [шаблона Azure Resource Manager, Сохранить](#save-azure-resource-manager-template) раздела и после завершения вернитесь сюда.
1. Выберите **создать** tooadd hello указан лаборатории toohello виртуальной Машины.
1. Hello лаборатории колонке hello состояния создания виртуальной Машины hello - сначала отображает как **создание**, затем по мере **под управлением** после hello, виртуальная машина запущена.

> [!NOTE]
> [Добавить виртуальную Машину claimable](devtest-lab-add-claimable-vm.md) показано, как toomake hello claimable виртуальной Машины так, чтобы оно было доступно для использования любым пользователем в лаборатории hello.
>
>

## <a name="add-an-existing-artifact-tooa-vm"></a>Добавление существующих артефактов tooa виртуальной Машины
Существующие артефакты можно добавить при создании виртуальной машины. Для каждого занятия включает артефакты из hello открытый репозиторий артефактов DevTest Labs, а также артефакты, что вы создали и добавлены tooyour владельцем репозиторий артефактов.

* Azure DevTest Labs *артефакты* позволяют указывать *действия* выполняются при подготовке hello виртуальной Машины, такие как запуск скриптов Windows PowerShell, выполнение команд Bash и установка программного обеспечения.
* Артефакт *параметры* позволяют настраивать hello артефакта для определенного сценария

артефакты toocreate. в статье toodiscover hello статьи, [как tooauthor собственные артефактов для использования с DevTest Labs](devtest-lab-artifact-author.md).

1. Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Выберите **более служб**, а затем выберите **DevTest Labs** из списка hello.
1. Выберите из списка hello лабораториям лаборатории hello, содержащей виртуальную Машину hello, с которой необходимо toowork.  
1. Выберите **My virtual machines** (Мои виртуальные машины).
1. Выберите hello требуемого виртуальной Машины.
1. Выберите **Артефакты**. 
1. Выберите **Apply artifacts** (Применить артефакты).
1. На hello **применить артефакты** колонки, выберите hello артефакта нужно tooadd toohello виртуальной Машины.
1. На hello **Добавить артефакт** колонки, введите значения параметров требуется hello и любые дополнительные параметры, которые необходимы.  
1. Выберите **добавить** toohello артефактов и возврат hello tooadd **применить артефакты** колонку.
1. Продолжайте добавлять артефакты, необходимые для виртуальной машины.
1. После добавления вашего артефакты, вы можете [изменить порядок hello, какие hello выполнения артефакты](#change-the-order-in-which-artifacts-are-run). Можно также вернуться к нему слишком[Просмотр или изменение артефакта](#view-or-modify-an-artifact).
1. После добавления артефактов выберите **Применить**.

## <a name="change-hello-order-in-which-artifacts-are-run"></a>Изменение порядка hello, в котором выполняются артефактов
По умолчанию действия hello артефактов hello выполняются в порядке hello, в котором они добавлены toohello виртуальной Машины. Hello ниже показано, как toochange hello порядок выполнения артефакты какие hello.

1. Вверху hello hello **применить артефакты** колонки, hello выберите ссылку, указывающее hello количество артефактов, которые были добавлены toohello виртуальной Машины.
   
    ![Число добавленных tooVM артефактов](./media/devtest-lab-add-vm-with-artifacts/devtestlab-add-artifacts-blade-selected-artifacts.png)
1. На hello **выбранных артефактов** артефакты hello колонки, операции перетаскивания в hello требуемого порядка. **Примечание:** Если возникли проблемы при перетаскивании артефактов hello, убедитесь, что при перетаскивании из hello левая сторона артефакта hello. 
1. По окончании нажмите кнопку **ОК** .  

## <a name="view-or-modify-an-artifact"></a>просмотру или изменению артефакта
Hello ниже показано, как tooview или изменить параметры hello артефакта:

1. Вверху hello hello **применить артефакты** колонки, hello выберите ссылку, указывающее hello количество артефактов, которые были добавлены toohello виртуальной Машины.
   
    ![Число добавленных tooVM артефактов](./media/devtest-lab-add-vm-with-artifacts/devtestlab-add-artifacts-blade-selected-artifacts.png)
1. На hello **выбранных артефактов** колонки, выберите hello артефакта, должны быть tooview, или изменить.  
1. На hello **Добавить артефакт** колонки, внесите любые необходимые изменения, а затем выберите **ОК** tooclose hello **Добавить артефакт** колонку.
1. Выберите **ОК** tooclose hello **выбранных артефактов** колонку.

## <a name="save-azure-resource-manager-template"></a>Сохранение шаблона Azure Resource Manager
Шаблон диспетчера ресурсов Azure предоставляет toodefine декларативным способом множественного повторного развертывания. Hello следующие шаги поясняют, как toosave hello шаблона диспетчера ресурсов Azure для hello созданной виртуальной Машине.
После сохранения шаблона hello диспетчера ресурсов Azure можно использовать слишком[развернуть новые виртуальные машины с помощью Azure PowerShell](../azure-resource-manager/resource-group-overview.md#template-deployment).

1. На hello **виртуальной машины** колонке выберите **шаблон ARM представления**.
2. На hello **шаблона диспетчера ресурсов Azure представление** колонку, текст шаблона выберите hello.
3. Копировать выделенный текст hello toohello-буфер обмена.
4. Выберите **ОК** tooclose hello **колонке Просмотр шаблона Azure Resource Manager**.
5. Откройте текстовый редактор.
6. Вставьте текст hello шаблона из буфера обмена hello.
7. Сохраните файл hello для последующего использования.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a>Дальнейшие действия
* Один раз hello, виртуальная машина будет создана, можно подключиться toohello виртуальной Машины, выбрав **Connect** на колонки hello виртуальной Машины.
* Узнайте, каким образом слишком[создать пользовательские артефакты для виртуальной Машины DevTest Labs](devtest-lab-artifact-author.md).
* Просмотр hello [коллекции шаблонов Azure Resource Manager DevTest Labs QuickStart](https://github.com/Azure/azure-devtestlab/tree/master/Samples).
