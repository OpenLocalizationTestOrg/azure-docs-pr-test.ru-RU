---
title: "aaaAdd claimable лаборатории tooa ВМ в Azure DevTest Labs | Документы Microsoft"
description: "Узнайте, как tooadd лаборатории tooa claimable виртуальной машины в Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: f671e66e-9630-4e30-a131-a6bad9ed9c11
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: tarcher
ms.openlocfilehash: fe6385ae2e59b9636b82aec250dc3a1f8a40ba5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-claimable-vm-tooa-lab-in-azure-devtest-labs"></a>Добавить claimable лаборатории tooa ВМ в Azure DevTest Labs
Добавить claimable лаборатории tooa ВМ в аналогичные toohow способом вы [Стандартная виртуальная машина добавляется](devtest-lab-add-vm.md) — *базового* , либо [пользовательского образа](devtest-lab-create-template.md), [формула](devtest-lab-manage-formulas.md), или [образа Marketplace](devtest-lab-configure-marketplace-images.md). Этот учебник поможет выполнить с помощью hello Azure портала tooadd claimable лаборатории tooa ВМ в DevTest Labs и показывает процесс hello hello tooclaim ВМ подписан пользователь.

> [!NOTE]
> При развертывании виртуальных машин лаборатории через [шаблоны Azure Resource Manager](devtest-lab-create-environment-from-arm.md), можно создать claimable виртуальных машин, установка hello **allowClaim** tootrue свойства в разделе "Свойства" hello.
>
>

## <a name="steps-tooadd-a-claimable-vm-tooa-lab-in-azure-devtest-labs"></a>Tooadd действия claimable лаборатории tooa ВМ в Azure DevTest Labs
1. Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Выберите **более служб**, а затем выберите **DevTest Labs** из списка hello.
1. Выберите из списка hello лабораториям hello лаборатории, необходимо toocreate hello claimable виртуальной Машины.  
1. В лаборатории hello **Обзор** колонке выберите **+ добавить**.  

    ![Кнопка добавления виртуальной машины](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. На hello **выберите базовый** колонке выберите база для hello виртуальной Машины.
1. На hello **виртуальной машины** колонки, введите имя для новой виртуальной машины hello в hello **имя виртуальной машины** текстовое поле.

    ![Колонка виртуальной машины лаборатории](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. Введите **имя пользователя** , которой предоставляются права администратора на виртуальной машине hello.  
1. Если вы хотите toouse пароль хранится в вашей [секретное хранилище](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store)выберите **сохраненного секрета**и укажите значение ключа, которое соответствует tooyour секрет (пароль). В противном случае введите пароль в hello текстовое поле с меткой **введите значение**.
1. Hello **тип диска виртуальной машины** определяет, какой тип диска хранилища допустим для hello виртуальных машин в лаборатории hello.
1. Выберите **размер виртуальной машины** и выберите один из hello предопределенные элементы, определяющие hello процессорных ядер, объем оперативной памяти и размер жесткого диска hello toocreate hello виртуальной Машины.
1. Выберите **артефакты** из списка hello артефактов, выберите и настройте hello артефакты, что требуется tooadd toohello базового образа. Если вы будете новый Labs tooDevTest или настройка артефакты, см. toohello [Добавление существующих артефактов tooa ВМ](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) статьи, а затем вернитесь сюда, после завершения.
1. Выберите **Дополнительные параметры** сеть виртуальной Машины hello tooconfigure параметры и срок действия параметров. В разделе **утверждения параметры**, выберите **Да** машины hello toomake claimable.

  ![Выберите toomake hello claimable виртуальной Машины.](./media/devtest-lab-add-vm/devtestlab-claim-VM-option.png)

1. Если требуется tooview или копировать hello шаблона диспетчера ресурсов Azure, см. toohello [шаблона Azure Resource Manager, Сохранить](devtest-lab-add-vm.md#save-azure-resource-manager-template) раздела и после завершения вернитесь сюда.
1. Выберите **создать** tooadd hello указан лаборатории toohello виртуальной Машины.
1. Hello лаборатории колонке hello состояния создания виртуальной Машины hello - сначала отображает как **создание**, затем по мере **под управлением** после hello, виртуальная машина запущена.


## <a name="using-a-claimable-vm"></a>Использование запрашиваемой виртуальной машины

Пользователь может утверждений все виртуальные Машины, из списка «Claimable виртуальные машины» hello, выполнив одно из следующих действий:

* Из списка «Claimable виртуальные машины» hello нижней части колонки Обзор лаборатории hello hello, щелкните правой кнопкой мыши на одном из hello виртуальных машин в списке hello и выберите **утверждения машины**.

 ![Запрос определенной запрашиваемой виртуальной машины](./media/devtest-lab-add-vm/devtestlab-claim-VM.png)


* Вверху hello hello **Обзор** колонке выберите **утверждений любой**. Случайное виртуальной машине назначается из списка hello claimable виртуальных машин.

 ![Запрос любой запрашиваемой виртуальной машины](./media/devtest-lab-add-vm/devtestlab-claim-any.png)


Выбранная пользователем запрашиваемая виртуальная машина перемещается в список раздела "My virtual machines" (Мои виртуальные машины). Ее не могут повторно запрашивать другие пользователи.

## <a name="next-steps"></a>Дальнейшие действия
* Один раз hello, виртуальная машина будет создана, можно подключиться toohello виртуальной Машины, выбрав **Connect** на колонки hello виртуальной Машины.
* Просмотр hello [DevTest Labs Azure Resource Manager QuickStart коллекции шаблонов](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)
