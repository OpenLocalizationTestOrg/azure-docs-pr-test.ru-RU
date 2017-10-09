---
title: "aaaCreate первой виртуальной Машины в лабораторной среде в Azure DevTest Labs | Документы Microsoft"
description: "Узнайте, как toocreate первой виртуальной машины в лабораторной среде в Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: fbc5a438-6e02-4952-b654-b8fa7322ae5f
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/24/2017
ms.author: tarcher
ms.openlocfilehash: 4c3257efca9be6fdd190eaac1db731464e07fcfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-vm-in-a-lab-in-azure-devtest-labs"></a>Создание первой виртуальной машины в лаборатории в Azure DevTest Labs

При первоначальном доступ к DevTest Labs toocreate первой ВМ, скорее всего этого с помощью предварительно загруженных [образа marketplace базовый](devtest-lab-configure-marketplace-images.md). Позднее вы также будете может toochoose из [пользовательского образа и формула](devtest-lab-add-vm.md) при создании дополнительных виртуальных машин. 

Этот учебник знакомит с помощью hello Azure портала tooadd первый tooa лаборатории для виртуальной Машины в DevTest Labs.

## <a name="steps-tooadd-your-first-vm-tooa-lab-in-azure-devtest-labs"></a>Шаги tooadd первый tooa лаборатории для виртуальной Машины в Azure DevTest Labs
1. Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Выберите **более служб**, а затем выберите **DevTest Labs** из списка hello.
1. Выберите из списка hello лабораториям hello лаборатории, в которой будет toocreate hello виртуальной Машины.  
1. В лаборатории hello **Обзор** колонке выберите **+ добавить**.  

    ![Кнопка добавления виртуальной машины](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. На hello **выберите базовый** колонке выберите образа marketplace для hello виртуальной Машины.
1. На hello **виртуальной машины** колонки, введите имя для новой виртуальной машины hello в hello **имя виртуальной машины** текстовое поле.

    ![Колонка виртуальной машины лаборатории](./media/devtest-lab-add-vm/devtestlab-lab-add-first-vm.png)

1. Введите **имя пользователя** , которой предоставляются права администратора на виртуальной машине hello.  
1. Введите пароль в hello текстовое поле с меткой **введите значение**.
1. Hello **тип диска виртуальной машины** определяет, какой тип диска хранилища допустим для hello виртуальных машин в лаборатории hello.
1. Выберите **размер виртуальной машины** и выберите один из hello предопределенные элементы, определяющие hello процессорных ядер, объем оперативной памяти и размер жесткого диска hello toocreate hello виртуальной Машины.
1. Выберите **артефакты** - списке hello артефактов - выберите и настройте hello артефакты, что требуется tooadd toohello базового образа.
    **Примечание:** Если вы будете новый Labs tooDevTest или настройка артефакты, см. toohello [Добавление существующих артефактов tooa ВМ](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) статьи, а затем вернитесь сюда, после завершения.
1. Выберите **создать** tooadd hello указан лаборатории toohello виртуальной Машины.

   Hello лаборатории колонке hello состояния создания виртуальной Машины hello - сначала отображает как **создание**, затем по мере **под управлением** после hello, виртуальная машина запущена.

## <a name="next-steps"></a>Дальнейшие действия
* Один раз hello, виртуальная машина будет создана, можно подключиться toohello виртуальной Машины, выбрав **Connect** на колонки hello виртуальной Машины.
* Извлечение [добавления виртуальных Машин лаборатории tooa](devtest-lab-add-vm.md) более полные сведения о добавлении последующих виртуальных машин в лаборатории.
* Просмотр hello [коллекции шаблонов Azure Resource Manager DevTest Labs QuickStart](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).
